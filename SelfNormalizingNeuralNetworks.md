#Summary of Self-Normalizing Neural Networks#
##Dan Mazur, March 2018##
##Prepared for the Advanced Data Science Reading Meetup, Vancouver, BC##

[Self-Normalizing Neural Networks](https://arxiv.org/abs/1706.02515) - Klambauer, et al

###What problem are they trying to solve?###
The success of deep learning is driven primarily by advances in computer vision using convolutional neural networks (CNNs) and sequence modeling (such as natural language processing) using recurrent neural networks (RNNs). In contrast, deep "vanilla" neural networks (i.e. feed-forward neural networks (FNNs)) have not produced many success stories. Deep learning is conspicuously absent from most Kaggle competitions that do not involve vision or sequential tasks. Instead, we see traditional machine learning methods such as gradient boosting, random forests, and support vector machines winning the competitions. When FNNs are used, they are often shallow. Where Why isn't deep learning more successful outside of vision and sequential tasks?

The authors believe that the reason FNNs are less successful than RNNs and CNNs is that they are more sensitive to perturbations of the normalization of the inputs to each layer of a network by stochastic gradient descent (SGD), stochastic regularization (like dropout), and estimation of the normalization parameters. They propose a new activation, called a scaled exponential linear unit (SELU), which help to stabilize the normalization and prevent exploding and vanishing gradients.

###Why is this an interesting problem?###
Deep learning has been revolutionary for computer vision and sequential tasks. If we can understand how to have similar success for other machine learning tasks, we might enjoy similar revolutions in achieving high performance on other types of tasks. 

This problem is also of theoretical interest. We do not have a complete theoretical explanation of why CNNs and RNNs have been so successful compared to other methods. [todo: finish thought]


###How has this been attempted previously?###
Many researchers have attempted to get good performance from deep FNNs with varying amounts of success. The authors do not review all of the attempts that have been tried, but simply observe the lack of FNNs in state-of-the-art systems. This paper is the first to discuss that the issue may be caused by instabilities of normalization.

###What did they do?###
[TODO]

###What did they find?###
[TODO]

###What has the response been from other researchers?###
The preprint for this paper was published only a few months ago, so it is hard to evaluate the impact. It has already been [cited dozens of times](http://adsabs.harvard.edu/cgi-bin/nph-ref_query?bibcode=2017arXiv170602515K&amp;refs=CITATIONS&amp;db_key=PRE). Many researchers are making use of this activation function for their own research, and several papers have compared the performance of SELU activations with other options empirically (e.g. [The "Swish" paper](https://arxiv.org/abs/1710.05941)). Somewhat ironically, most of the researchers citing this paper are using SELU activations in CNNs and RNNs for computer vision and sequential tasks.

###Other summaries###
[An intro to self-normalising neural networks (SNN)](https://medium.com/@damoncivin/self-normalising-neural-networks-snn-2a972c1d421) -Damon Civin
[SELU — Make FNNs Great Again (SNN)](https://towardsdatascience.com/selu-make-fnns-great-again-snn-8d61526802a9) -Elior Cohen
[Paper Review: Self-Normalizing Neural Networks](http://www.erogol.com/paper-review-self-normalizing-neural-networks/) -Erogol

###Implementation/Code###
[Authors' Tensorflow implementations on Github](https://github.com/bioinf-jku/SNNs)

###Glossary
[Artificial Neural Network (ANN)](https://en.wikipedia.org/wiki/Artificial_neural_network)
[Convolutional Neural Netowrk (CNN)] (https://en.wikipedia.org/wiki/Convolutional_neural_network)
Exploding and vanishing gradient problem(TODO)
Normalization (TODO)
[Recurrent Neural Network (RNN)](https://en.wikipedia.org/wiki/Recurrent_neural_network)
