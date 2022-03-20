---
layout: post
title:  Wikipedia's Philosophers
date:   2022-03-19
tags:
  - philosophy
  - text-analytics
  - network-analysis
---

In this post I want to share a method and Python code, which I've developed for drawing maps of science from Wikipedia data. Here is my example:

<img src="/img/wiki-philosophers/all_zoom.png" />

This map represents the collective effort of Wikipedians to draw socio-intellectual linkages between philosophers of public interest. Each node, i.e. name, in the network corresponds to the title of a Wikipedia article on a specific philosopher. Each link represent a one- or two-directional hyperlink between two Wikipedia articles.


## Nodes from lists!

Wikipedians are obsessed with lists of all sorts—--so obsessed, in fact, that they have not only created lists of lists but a [List of lists of lists](https://en.wikipedia.org/wiki/List_of_lists_of_lists):

> This is a list of lists of lists, an article that is a list of articles that are themselves lists of article lists. In other words, each of the articles linked here is an index to multiple lists on a topic. Some of the linked articles may contain lists of lists as well.

Ok, let's see...["Philosophy"](https://en.wikipedia.org/wiki/List_of_lists_of_lists#Philosophy)...["Lists of philosophers"](https://en.wikipedia.org/wiki/Lists_of_philosophers)...["Lists of philosophers by name"](https://en.wikipedia.org/wiki/Lists_of_philosophers#Lists_of_philosophers_by_name). Bingo!




>"[Philosophy](https://en.wikipedia.org/wiki/Philosophy) \[...\] is the study of general and fundamental questions, such as those about existence, reason, knowledge, values, mind, and language." 

> "A [philosopher](https://en.wikipedia.org/wiki/Philosopher) is someone who practices philosophy [...but] A philosopher may also be someone who has worked in the humanities or other sciences which over the centuries have split from philosophy, such as the arts, history, economics, sociology, psychology, linguistics, anthropology, theology, and politics."
