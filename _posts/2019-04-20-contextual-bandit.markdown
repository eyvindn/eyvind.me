---
layout: post
mathjax: true
title:  "Contextual Bandits - what are they? (draft)"
date:   2019-04-20 11:11:11 -0400
---
### DRAFT

Multi-armed bandit problems (often monickered 'bandit problems') are a well studied field of reinforcement learning. 

Dipendra et. al introduce the concept of "contextual bandit" in their approach to training a reinforcement learning agent in their first [instruction following paper][dipendra-contextual-bandit]. 

TODO:
- briefly summarize/remind readers of the definition of a multi-armed bandit
- introduce the concept of a contextual bandit
    - talk about the limitations (i.e. reward shaping function has to have a ["potential function"][reward-shaping-potential] property to prove convergence in training)
- briefly discuss some new approaches to immediate rewards - ["curiosity" paper][curiosity]

[dipendra-contextual-bandit]: https://arxiv.org/pdf/1704.08795.pdfi
[reward-shaping-potential]: http://cseweb.ucsd.edu/~ewiewior/03principled.pdf
[curiosity]: https://arxiv.org/pdf/1705.05363.pdf
