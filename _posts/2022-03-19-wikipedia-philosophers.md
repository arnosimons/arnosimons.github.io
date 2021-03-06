---
layout: post
title:  "Wikipedia's Map of Philosophers"
date:   2022-03-19
themes:
  - Open Science & Technology
  - Science Communication
  - Discourse Analytics
---

Wikipedia is a great source for free knowledge, including knowledge about science and science history. For example, we can mine the collective effort of Wikipedians to draw a socio-intellectual map of philosophers, which, conincidentally, looks like a brain. Or rather like a jellyfish?

<img src="/img/wiki-philosophers/all_zoom.png"/>

...zooming out...

<img src="/img/wiki-philosophers/all.png"/>

What you see here is how 1598 ["notable-enough"](https://en.wikipedia.org/wiki/Wikipedia:Notability_(people)) philosophers are connected to each other because Wikipedians have associated them in this way. More precisely, the nodes you see in this network represent Wikipedia articles on philosophers, and the edges represent hyperlink connections Wikipedia editors have created between these articles.

The size of a name represents the betweenness centrality of the associated node and can be interpreted as a normalized measure for how many shortest paths between any two philosophers will lead through this node. Unsurprisingly it turns out that Aristotle, Immanuel Kant, Plato, and Karl-Marx are the leading figures in this regard.

A name's color indicates to which "community" that philosopher belongs. To detect communities, I used the [Louvain method](https://en.wikipedia.org/wiki/Louvain_method), a widely-used alghorithm that optimizes the relative density of edges inside communities with respect to edges outside communities.

Overall, the communities seem to make sense. For example, here are communities of Ancient Greek and Roman philosophers intermingling with Persian and scholastic philosophers.

<img src="/img/wiki-philosophers/ancients.png" />

Here we find the "continentalists" next to the "Marxists":

<img src="/img/wiki-philosophers/continentalists.png" />

And finally, the "Enlightenment scholars" next to the "utilitarianist", the "pragmatists", and the "analytical philosophers".

<img src="/img/wiki-philosophers/analyticals.png" />

To produce the final graph layout I switched over to Gephi, ["a free visualization and exploration software for all kinds of graphs and networks"](https://gephi.org/). Yes, there would have been ways to draw similar (or better) layouts in Python. But convenience. The spacial layout was archieved by applying the ForceAtlas 2 alghorithm, which was ["designed for the Gephi user experience"](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0098679).


I developed this map as a little exercise for a class I taught on text mining. If you're interested in the actual Python coding behind it, here you go:


## Modules first!

For our example we need a couple of pretty amazing python libraries. To import them, just write: 

```python
# for scraping
import requests
from bs4 import BeautifulSoup
from bs4.element import NavigableString, Tag

# for graphs
import networkx as nx
import networkx.algorithms.community as nx_comm

# for data and plotting
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
```


## Nodes from lists

The first step in creating our little network is to collect a set of nodes, that is philosophers. We could approach this task by writing down all philosophers that come into our mind, or we could look names up in books titled "The greatest philosophers of all times" or worse. However, since we are using Wikipedia, we better make sure that for each name we pick, there is a corresponding Wikipedia article. 

My trick was to make use of a very strange habbit of Wikipedians. Have you been aware that Wikipedians are obsessed with lists of all sorts? In fact, the epitome of this collective obsession is the notorious [List of lists of lists](https://en.wikipedia.org/wiki/List_of_lists_of_lists): 

> This is a list of lists of lists, an article that is a list of articles that are themselves lists of article lists. In other words, each of the articles linked here is an index to multiple lists on a topic. Some of the linked articles may contain lists of lists as well.

Meta-meta-overdose! But why not start here? Ok, let's see...there we go: ["Philosophy"](https://en.wikipedia.org/wiki/List_of_lists_of_lists#Philosophy)...and yes...a ["Lists of philosophers"](https://en.wikipedia.org/wiki/Lists_of_philosophers). Click to decend from the meta-meta level to the meta level. And there we go again: 
four different ["Lists of philosophers by name"](https://en.wikipedia.org/wiki/Lists_of_philosophers#Lists_of_philosophers_by_name). Bingo!


Before we actually scrape these lists, we first define a function that takes a given url as input, downloads and parses the html and returns the parsed representation as a `soup` object.


```python
def get_soup(url):
    response = requests.get(url)
    if response.ok:
        return BeautifulSoup(response.content, 'html.parser')
    return BeautifulSoup("", 'html.parser')
```

Then we tell Python the urls of the four philosopher lists, open each, make a soup, single out the `"mw-parser-output"`, and iterate over all list entries to extract the hyperlink and name of each mentioned philosopher as a key-value pair in a dictionary named `philosophers`.

```python
urls = [
    "https://en.wikipedia.org/wiki/" + title
    for title in [
        "List_of_philosophers_(A%E2%80%93C)",
        "List_of_philosophers_(D%E2%80%93H)",
        "List_of_philosophers_(I%E2%80%93Q)",
        "List_of_philosophers_(R%E2%80%93Z)",
    ]
]

philosophers = {
    item.a["href"].split("/wiki/")[-1]: item.a["title"]
    for url in urls
    for child in get_soup(url).find("div", {"class":"mw-parser-output"}).contents
    for item in child 
    if child.name == "ul"
    if item.name == "li"
}
print(len(philosophers))
```

## Edges from hyperlinks

Now we must mine the mutual connections between all these Wikipedia philosopher articles. I defined "connection" has the existence of a hyperlink between articles. So, let's iterate through our `philosophers` dictionary, open each associated Wikipedia article and search for only those hyperlinks, i.e.  `href` values in `<a>` tags, that match the urls of any of the philosophers in our dictionary. This ensures that we stay within the list of names of philosophers mines in the previous step, which was a deliberate choice I made. All matches are then collected in a set of node pairs. To do this efficiently in Python, I made use of set comprehension.


```python
edges = set(
    (value, philosophers[a["href"].split("/wiki/")[-1]])
    for key, value in philosophers.items()
    if get_soup(WIKI_BASE_URL + key)
    for child in get_soup(WIKI_BASE_URL + key).find("div", {"class":"mw-parser-output"}).contents
    if child.name in ALLOWED_TAGS
    for a in child.find_all("a")
    if a.has_attr("href")
    and a["href"].split("/wiki/")[-1] in philosophers
)
print(len(edges))
```

## Make the graph

Given the nodes and edges, we can now create our graph. Note that while hyperlinks are inherently directional, I modelled the philosophers' network network as an undirected graph, mainly to simplify the modularity detection. To compensate a bit for this loss of directional information, I decided to set the edge weight to 2 if two philosopher articles were mutually connected by hyperlinks and to 1 if only one of the two articles directed to the other.  

```python
G = nx.Graph()
for a, b in edges:
    if (b, a) in G.edges:
        G.edges[(b, a)]["weight"] += 1
    else:
        G.add_edge(a, b, weight=1)
print(f"Graph has {len(G.nodes)} nodes and {len(G.edges)} edges")
```
The next step was to get rid of a few philosophers that were unconnected to the main network. Again this was for practical reasons only. What I effectively did was to keep only the largest connected component of the graph.


```python
cc = sorted(nx.connected_components(G), key=len, reverse=True)
keep = cc[0]
G.remove_nodes_from([n for n in G.nodes if not n in keep])
print(f"Number of components: {len(cc)}")
print(f"Size of all components: {[len(c) for c in cc]}")
print(f"Reduced Graph has {len(G.nodes)} nodes and {len(G.edges)} edges")
```

## Calculate betweenness centrality and communities

Once we have our largest connected component, let's find out who are the most "important" philosophers in terms of their centrality in the graph. I picked betweenness centrality because it is often used in this context, but again with the caveat that we treated hyperlinks as undirected here, which is not what they actually are. In other words, betweennes scores might have been a little bit different had we used a directed graph. 

```python
nx.set_node_attributes(G, nx.betweenness_centrality(G), name="betweenness_centrality")
```

Modeling the graph as undirected comes in very handy for the detection of communities, since it allows us to use the Louvain method right off the shelf. In Python that is:

```python
communities = sorted(nx_comm.louvain_communities(
    G,  
    threshold=1,
    resolution=1,
    seed=123,
), key=len, reverse=True)
for cid, c in enumerate(communities):
    for node in c:
        G.nodes[node]['louvain_community'] = cid
print(f'Number of communities: {len(communities)}')
```

As you can see, in the `for` loop we add the commuity ids as an attribute to the node data, so we can later use it in Gephi to color the nodes.

Now, we can export the graph and switch over to Gephi for visualization, which I will not cover here. If you're interested, check out the many good Gephi tutorials online.

```python
nx.write_gexf(G, "wiki_philosophers.gexf")
```
