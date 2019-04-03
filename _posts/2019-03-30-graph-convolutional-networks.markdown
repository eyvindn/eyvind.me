---
layout: post
title:  "Graph Convolution Networks - what are they?"
date:   2019-03-30 11:11:11 -0400
categories: jekyll update
---
Over the past few years neural networks have become increasingly multi-modal. Despite being inherent universal function approximators, a great challenge in applying them to various forms of data
is finding ways of representing this data in a manner that's conducive for the network to ingest. Some examples of such encodings are:
- word embeddings
- convolutions over raw pixel data
- etc. 

However, one category that hasn't seen as much success is graphs. Graphs are defined by a set of vertices and a set of associated edges. There is no clear, intuitive way to feed a graph into a neural network (although you could relish in the fact that you are trying to feed a graph into a graph...). On first thought, something like an adjacency matrix might come to mind as a way to do this. After all, adjacency matrices are an important structure used for more advanced analysis of graphs, including in spectral graph theory.

A different approach is Graph Convolutions, and their associated forms. Inherently, graph convolutions present a way to generate an embedding for each node in a graph based off of its relation to other nodes in the graph. 

TODO:
- discuss original papers by Socher et. al 
- discuss variations on this concept (i.e. DistMult, ConvE)
- discuss later work on multi-modal embeddings into graphs using the same technique

[comment]: #{% highlight ruby %}
[comment]: #def print_hi(name)
[comment]: #  puts "Hi, #{name}"
[comment]: #end
[comment]: #print_hi('Tom')
[comment]: #=> prints 'Hi, Tom' to STDOUT.
[comment]: #{% endhighlight %}


[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
