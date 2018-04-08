# Summary of Self-Normalizing Neural Networks
## Dan Mazur, March 2018
## Prepared for the [Advanced Data Science Reading Meetup](https://www.meetup.com/LearnDataScience/events/248105899/), Vancouver, BC

[Self-Normalizing Neural Networks](https://arxiv.org/abs/1706.02515) - Klambauer, et al

### What problem are they trying to solve?
The success of deep learning is driven primarily by advances in computer vision using convolutional neural networks (CNNs) and sequence modeling (such as natural language processing) using recurrent neural networks (RNNs). In contrast, deep "vanilla" neural networks (i.e. feed-forward neural networks (FNNs)) have not produced many success stories. Deep learning is conspicuously absent from most Kaggle competitions that do not involve vision or sequential tasks. Instead, we see traditional machine learning methods such as gradient boosting, random forests, and support vector machines winning the competitions. When FNNs are used, they are often shallow. Why isn't deep learning more successful outside of vision and sequential tasks?

The authors believe that the reason FNNs are less successful than RNNs and CNNs is that they are more sensitive to perturbations of the normalization of the inputs to each layer of the network. The instabilities are the result of stochastic gradient descent (SGD), stochastic regularization (like dropout), and estimation of the normalization parameters. They propose a new activation, called a scaled exponential linear unit (SELU), which help to stabilize the normalization and prevent exploding and vanishing gradients.

### Why is this an interesting problem?
Deep learning has been revolutionary for computer vision and sequential tasks. If we can understand how to have similar success for other machine learning tasks, we might enjoy similar revolutions in achieving high performance on other types of tasks. We do not have a complete theoretical explanation of why CNNs and RNNs have been so successful compared to other methods, and this paper tests a new hypothesis that helps to explain the relative success between FNNs and CNNs/RNNs.


### How has this been attempted previously?
Many researchers have attempted to get good performance from deep FNNs with varying amounts of success. The authors do not review all of the attempts that have been tried, but simply observe the lack of FNNs in state-of-the-art systems. This paper is the first to discuss that the issue may be caused by instabilities of normalization.

### What did they do?
The SELU activation is given by the equation,

![Definition of SELU activation function](http://latex.codecogs.com/svg.latex?%7B%5Crm%20selu%7D%28x%29%20%5C%20%26%3D%20%5C%20%5Clambda%20%5C%20%5Cbegin%7Bcases%7D%20x%20%26%20%5Ctext%7Bif%20%7D%20x%20%3E%200%20%5C%5C%20%5Calpha%20e%5E%7Bx%7D-%5Calpha%20%26%20%5Ctext%7Bif%20%7D%20x%20%5Cleq%200%20%5Cend%7Bcases%7D%20%5C%20.)

![activation functions](https://github.com/QEDan/PaperSummaries/blob/master/images/SelfNormalizingNeuralNetworks/activationFunctions_out.png)

In the figure above, the SELU activation function is shown as the purple curve in comparison to other common activation functions such as the ReLU (blue).

The authors prove that the SELU activation function results in self-normalizing neural networks. Specifically, the mapping between the mean and variance of one layer to the mean, ![mu](http://latex.codecogs.com/svg.latex?\mu), and variance, ![nu](http://latex.codecogs.com/svg.latex?\nu), of the next layer has a stable fixed point at ![mu=0](http://latex.codecogs.com/svg.latex?\mu=0), ![nu=1](http://latex.codecogs.com/svg.latex?\nu=1) when ![alpha=1.6733](http://latex.codecogs.com/svg.latex?\alpha=1.6733) and ![lambda=1.0507](http://latex.codecogs.com/svg.latex?\lambda=1.0507)

The computer-assisted proof is given in a 90 page appendix, although an overview is given on page 5 beneath Theorem 1. The authors use the [Banach Fixed Point Theorem](https://en.wikipedia.org/wiki/Banach_fixed-point_theorem) to show that there is a unique fixed point and that it is stable and attracting.

![Arrows](https://github.com/QEDan/PaperSummaries/blob/master/images/SelfNormalizingNeuralNetworks/Figure2_arrows_new-crop.png
)

The above figure shows the stable fixed point. The mapping is applied between each layer of a deep neural network. Through repeated applications of the mapping, the neural network activations are normalized because the distributions are driven toward the stable fixed point.

In addition to this self-normalizing property, the authors also prove some additional properties of SNNs:
- They do not suffer from exploding gradients (Theorem 2)
- They do not suffer from vanishing gradients (Theorem 3)
- The weights can be initialized to fulfill the constraints required in the proof
- The dropout regularization algorithm can be modified to preserve the self-normalizing properties of the network (alpha dropout)


### What did they find?
The authors test their ideas empirically by comparing with other FNN techniques on a variety of benchmark classification tasks. The benchmark tasks are:
- 121 UCI Machine Learning Repository datasets
- Drug discovery: The Tox21 challenge dataset
- Astronomy: Prediction of pulsars in the HTRU2 dataset

![cifar10](https://github.com/QEDan/PaperSummaries/blob/master/images/SelfNormalizingNeuralNetworks/cifar10.png) ![mnist](https://github.com/QEDan/PaperSummaries/blob/master/images/SelfNormalizingNeuralNetworks/mnist.png)

The authors also provide these training curves comparing the training of a variety of FNN architectures on CIFAR10 (left) and MNIST (right)

The authors find that across a large variety of tasks, deep SNN architectures outperform other FNN architectures. The best performing SNNs are typically much deeper than the best performing non-SNN FNNs.



### What has the response been from other researchers?
The preprint for this paper was published only a few months ago, so it is hard to evaluate the impact. It has already been [cited dozens of times](http://adsabs.harvard.edu/cgi-bin/nph-ref_query?bibcode=2017arXiv170602515K&amp;refs=CITATIONS&amp;db_key=PRE). Many researchers are making use of this activation function for their own research, and several papers have compared the performance of SELU activations with other options empirically (e.g. [The "Swish" paper](https://arxiv.org/abs/1710.05941)). Somewhat ironically, many of the researchers citing this paper are using SELU activations in CNNs and RNNs for computer vision and sequential tasks.

### Other summaries
- [An intro to self-normalising neural networks (SNN)](https://medium.com/@damoncivin/self-normalising-neural-networks-snn-2a972c1d421) -Damon Civin
- [SELU — Make FNNs Great Again (SNN)](https://towardsdatascience.com/selu-make-fnns-great-again-snn-8d61526802a9) -Elior Cohen
- [Paper Review: Self-Normalizing Neural Networks](http://www.erogol.com/paper-review-self-normalizing-neural-networks/) -Erogol

### Implementation/Code
- [Authors' Tensorflow implementations on Github](https://github.com/bioinf-jku/SNNs)

### Glossary
- [Activation Function](https://en.wikipedia.org/wiki/Activation_function) - The function in an ANN that defines the output from a neuron given its inputs.
- [Artificial Neural Network (ANN)](https://en.wikipedia.org/wiki/Artificial_neural_network) - A strategy for building machine learning models based on a collection of nodes (artificial neurons) in a network.
- [Banach Fixed Point Theorem](https://en.wikipedia.org/wiki/Banach_fixed-point_theorem) - A mathematical theorem that guarantees unique [fixed points](https://en.wikipedia.org/wiki/Fixed_point_(mathematics)) in self-mapping metric spaces under certain conditions.
- [Convolutional Neural Netowrk (CNN)](https://en.wikipedia.org/wiki/Convolutional_neural_network) - A neural network architecture that uses convolutions to achieve translation invariance between input features. They have become the standard strategy for computer vision tasks.
- [Dropout Regularization](https://en.wikipedia.org/wiki/Dropout_(neural_networks)) - A method for preventing overfitting in a neural network by randomly choosing nodes to remove from the network.
- Exploding and [vanishing gradient problem](https://en.wikipedia.org/wiki/Vanishing_gradient_problem) - Certain conditions in a neural network can cause the gradients of the loss function to become very large or very small and this makes it difficult to solve the optimization problem.
- [Fixed point](https://en.wikipedia.org/wiki/Fixed_point_(mathematics)) - A point on a function's domain that is mapped to itself by the function.
- [Normalization](https://en.wikipedia.org/wiki/Normalization_(statistics)) - Transforming a data set to have zero mean and unit variance (i.e. variance=1). This helps to standardize the scales involved between different dimensions in the data.
- [Recurrent Neural Network (RNN)](https://en.wikipedia.org/wiki/Recurrent_neural_network) - A network architecture usually used for sequential data where previous (or later) elements of the sequence are inputs to a neuron in addition to the current element of the sequence.
