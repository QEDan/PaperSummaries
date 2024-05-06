# Summary of Hopfield Networks is All You Need (blog post)
## Dan Mazur, May 2024
## Prepared for the Learn Data Science Reading Meetup, Vancouver, BC

[Hopfield Networks Is All You Need]([https://arxiv.org/abs/1611.03530](https://ml-jku.github.io/hopfield-layers/)) - Ramsauer, et al

### What problem are they trying to solve?

[Hopfield networks](https://en.wikipedia.org/wiki/Hopfield_network) are models of neural networks based on the [Ising model](https://en.wikipedia.org/wiki/Ising_model) of magnetic materials in physics. 
In 2016 and 2017, changes were made to the energy function of Hopfield networks to greatly expand the memory capacity and make them much more practical. 
The resulting models are called [modern Hopfield networks](https://en.wikipedia.org/wiki/Modern_Hopfield_network). Sometimes, the earlier Hopfield networks are called "classical" Hopfield networks.

The authors were exploring other possible Energy functions for Hopfield networks that might give further improvements or interesting properties. Specifically, they were looking for energy functions that would give
greater memory capacity and convergence speeds.

### Why is this an interesting problem?

Neural networks and deep learning have many practical applications and have become an extremely important part of many technologies and businesses. This research focuses on finding new architectures that 
could make neural networks more efficient at storing and using data, improving the memory capacity of neural networks.

### What did they do?

They proposed a new energy function. It is the logarithm of the negative energy of the modern Hopfield network energy function, plus a quadratic term. In the blog post, their new energy function is equation (18),
the modern Hopfield network energy function is equation (12) or (13), and the classical Hopfield network energy function is equation (3). 

They show that this energy function:
* has exponential storage capacity
* converges globally to a local minimum in a single step
* is differentiable and can be used in neural networks

They created three open-source layers in PyTorch that can be used for deep learning:
* Hopfield for associating and processing two sets. Examples are the transformer attention, which associates keys and queries, and two point sets that have to be compared.
* HopfieldPooling for fixed pattern search, pooling operations, and memories like LSTMs or GRUs. The state (query) pattern is static and can be learned.
* HopfieldLayer for storing fixed patterns or learning internal prototypes. The stored (key) patterns are static and can be learned.


### What did they find?

Besides finding an energy function with very useful properties, they also found a surprising link to the [self-attention mechanism](https://armanasq.github.io/nlp/self-attention/) in Transformers. 
Specifically, The update of the new energy function is the self-attention of transformer networks. This is what inspires their title, 
since the paper that inspired transformers was called [Attention is All You Need](https://arxiv.org/abs/1706.03762).

This link allows the authors to analyze transformers through the lens of hopfield networks. They find that the heads of transformers perform in the first layers preferably
global averaging and in higher layers partial averaging via metastable states.

They find that their layer implementations are able to achieve state-of-the-art results on a variety of machine learning tasks.

