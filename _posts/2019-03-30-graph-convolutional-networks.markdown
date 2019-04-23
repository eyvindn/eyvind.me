---
layout: post
mathjax: true
title:  "Knowledge Graph Embeddings - what are they?"
date:   2019-03-30 11:11:11 -0400
categories: jekyll update
---
Over the past few years neural network encoders have become increasingly multi-modal. Despite being inherent universal function approximators, a great challenge in applying them to various forms of data
is finding ways of representing this data in a manner that's conducive for the network to ingest. Some examples of such methods of going from a raw data point to an encoding or embedding are:
- word embeddings (originally word2vec, now the standard approach for any token-based NN)
- convolutions over raw pixel data (any image ingesting NN, essentially)
- dilated convolutions over raw waveform data (Wavenet)

However, one category that hasn't seen as much publicity (and success, to some degree) is knowledge bases and/or ontologies. The difference between a knowledge base and an ontology is somewhat subtle and an area of discussion. For the purposes of this post I won't get into the weeds in this distinction. For now, I will abuse terminology and treat them as more or less the same thing.  

Knowledge bases are extremely familiar to anyone who worked with early approached to AI based of symbolic systems. They come in many forms but very often they are encoded into graphs. Graphs, in turn, are defined by a set of vertices and a set of associated edges (which may be directed, or undirected). A common approach to defining a knowledge base/ontology is to encode the inherent structure into these vertices and edges by assigning a node to a semantic category or idea, and assigning relations between such ideas as edges between the nodes. 

An extremely simple example is the ontology for human families - in this case nodes represent the unique invididuals in the family and the relations would be their familial relations ("son of", "grandfather to", "first cousin of", etc.). Often the nodes in a knowledge graph are referred to as "entities" and the edges are referred to as "relations". For more information on onotologies and knowledge graphs, see [this blog post][ontology-blog-post]. There is no clear, intuitive way to feed such an ontology graph into a neural network (although, while trying, you could relish in the fact that you are trying to feed a graph into a graph...). 

On first thought, something like an adjacency matrix might come to mind as a way to do this. After all, adjacency matrices are an important structure used for more advanced analysis of graphs, including in spectral graph theory. This is indeed a subject of much study in the field of Graph Convolution Networks (GCNs)! In short, GCNs create embeddings by passing the adjacency matrix for a graph through a series of dense layers in a network, finally outputting an $NxM$ matrix, giving a size $M$ embedding to $N$ nodes in the graph. However, to define the adjacency matrix you need to have knowledge of the entire graph and all it's edges, and if the graph changes (i.e. nodes are added), you have to recreate this adjacency matrix. Additionally, adjacency matrices do not lend themselves to unknown or undefined relations (or relations which might be inferred from other relations), which are common in many knowledge bases and ontologies. 

A different approach is Knowledge Graph Embeddings (KGEs). One of the seminal papers in the field introduced the concept of neural tensor networks (NTNs). NTNs present a way to generate an embedding for each node in a graph based off of its relation to other nodes in the graph, but without using the adjacency matrix. Most papers treating knowledge graphs seem to have been inspired by this approach, so it is worth summarizing the key points. 

NTNs, and later approaches to KGEs tend to tread a knowledge graphs as a set of triplets of the following form:

$$<e_i, r_k, e_j>$$

Where $e_i$ and $e_j$ are entities in the graph, and $r_k$ is some relation. Often, the entities themselves are represented by some embedding, i.e. $e_i \in R^v$ where $v$ is the size of the embedding, and $r_k$ is a "matrix-embedding" - $r_k \in R^{q \times z}$. 

It then defines a function on these triplets which outputs a score in $[0,1]$ or sometimes $[-1,1]$:

$$f(e_i, r_k, e_j) \mapsto [-1, 1]$$

Which represents the "score" for the relation $r$ existing between $e_i$ and $e_j$. In other words Training is performed by stochastic sampling of such triplets from the graph, and performing back-propagation over the embeddings for the entities and for the relation. This encourages the embeddings to capture inherent information about the structure of the network simply by entities co-occuring during this stochastic sampling during training of the network. 

At this point, we have trained embeddings for all the entities, and the network can be used for a task called "knowledge graph completion". This is the most common application of KGEs currently, and it involves inferring relations between existing entities in the graph that are not already defined as relations. Re-using our previous example - if A is the "son of" B, and B is the "son of" C, we'd want our network to infer a relationship of the type "grandfather to" between C and A, if this edge already does not exist. 

However, having an embedding of the entities in a KG is inherently useful a number of other tasks. An interesting paper by [Pezeshkpour et al.][pezeshkpour] applies KGEs to other multi-modal forms of data external to the knowledge graph. They take pictures, descriptions and other multi-modal data and apply the same technique to "map this" into the knowledge graph. For these non-graph entities, they apply various encoders (convolutions over images, LSTMs over textual descriptions, etc.) to produce an embedding for that entitiy which they then feed into a scoring function as above. Such an approach allows maintaining an internal knowledge graph representation of your ontology and having a robust way to embed external data onto this knowledge graph.  


[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/i
[ontology-blog-post]: https://medium.com/predict/where-ontologies-end-and-knowledge-graphs-begin-6fe0cdede1ed
[pezeshkpour]: https://www.aclweb.org/anthology/D18-1359
