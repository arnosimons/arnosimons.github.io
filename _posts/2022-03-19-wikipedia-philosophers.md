---
layout: post
title:  "Wikipedia Science Maps: Philosophers"
date:   2022-03-19
tags:
  - philosophy
  - text-analytics
  - network-analysis
---

<small>This post is part of a series on how to draw cool maps of science with Wikipedia data. In each episode I will present a different method and/or type of map and provide you with a concrete Python code example. I will not explain the code in much detail since I assume that you already know Python well enough to follow. If you don't, I recommend checking out the many free Python turorials online.</small>

Today, I'm showing you how to make this network of philosophers:

<img src="/img/wiki-philosophers/all.png"/>
<img src="/img/wiki-philosophers/all_zoom.png"/>

Does the shape of this network remind you of a brain or Jellyfish, too? 🧠🎊 

Ok, so what you see here is how famous and not so famous philosophers are connected to each other because Wikipedians have associated them in this way. More precisely, the nodes you see in this network represent Wikipedia articles on philosophers, and the edges represent hyperlink connections Wikipedia editors have created between these articles. If only the article of one philosopher points via a hyperlink to the article of another one, I set the edge weight to 1. If hyperlinks are two-directional, I set the edge weight to 2.

The size of a name represents the betweenness centrality of the associated node and can be interpreted as a measure for how many paths between any two philosophers will pass through this node. As we see, Aristotle, Immanuel Kant, Plato, and Karl-Marx are the leading figures in this regard.

A name's color indicates to which "community" that philosopher belongs. To define these communities, I used the [Louvain method](https://en.wikipedia.org/wiki/Louvain_method), a widely-used alghorithm that optimizes the relative density of edges inside communities with respect to edges outside communities. 

Overall, the found communities seem to make sense. For example, here are communities of Ancient Greek and Roman philosophers intermingling with Persian and scholastic philosophers.

<img src="/img/wiki-philosophers/greek.png" />


To be honest, changing the random seed for initializing the alghorithm yielded slightly different communities each time, but this is a known problem. While a number of indicators have been proposed to guide the choice of "the best" community structure, I have not even opened that box. My philosopher's network is just a toy example after all.
 



So how did I make it?


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
        # response.encoding = "utf-8"
        return BeautifulSoup(response.content, 'html.parser')
    return BeautifulSoup("", 'html.parser')
```

Then we tell Python the urls of the four philosopher lists, open each, make a `soup`, single out the `mw-parser-output`, and iterate through all list entries to extract the hyperlink and name of each mentioned philosopher (`item.a["href"].split("/wiki/")[-1]: item.a["title"]`) into a dictionary named `philosophers`.

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

...to be continued!
