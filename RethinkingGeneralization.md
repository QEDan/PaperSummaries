#Summary of Understanding Deep Learning Requires Rethinking Generalization#
##Dan Mazur, February 2017##
##Prepared for the Advanced Data Science Reading Meetup, Vancouver, BC##

[Understanding Deep Learning Requires Rethinking Generalization](https://arxiv.org/abs/1611.03530) - Zhang, et al

###What problem are they trying to solve?###
Deep [artificial neural networks](https://en.wikipedia.org/wiki/Artificial_neural_network) (ANNs) can exhibit a small difference between training and test performance. This is surprising in light of the huge number of free parameters involved in the optimization, which you might expect to cause overfitting (i.e. low training error, but high test error). The authors perform some experiments and calculations to test our best explanations for the effect.

###Why is this an interesting problem?###
We do not have a good theoretical explanation for this ability of neural networks to generalize so successfully. Nevertheless, they are wildly successful at creating generalizeable models in many domains. Understanding why will help us to interpret ANN models and may lead to principals that will guide researchers in designing model architectures.

###How has this been attempted previously?###
The paper discusses three popular explanations for the generalization performance of ANNs: VC-dimension, Rademacher complexity, and uniform stability.
* [VC-dimension](https://en.wikipedia.org/wiki/VC_dimension): - The cardinality of the largest set of points that the classification algorithm can shatter. 
* [Rademacher complexity](https://en.wikipedia.org/wiki/Rademacher_complexity) - Measures a model's capability of fitting all possible +/-1 binary label assignments.
* [Uniform stability] (https://en.wikipedia.org/wiki/Stability_(learning_theory)) - How sensitive an algorithm is to the replacement of a single example. This is a property of the algorithm and does not take into account the data or the labels.

Explicit regularization methods (e.g. weight decay, dropout, and data augmentation) are also often said to contribute to the generalizeability of ANNs.

###What did they do?###
The authors used several different flavours of randomization to experimentally study how the training and generalization performance of the ANNs would be affected:
* The networks were trained on a copy of the data after replacing the true labels with randomized ones.  
* In another variant, the networks were trained after replacing the true images by completely random pixels. 
* In a final variant, a smooth interpolation was used between the original images and the randomized pixels to study the ANNs performance as a function of the interpolation parameter.

With their experiments, they studied a selection of popular explicit regularization schemes: data augmentation, weight decay, and dropout.

In addition to the experimental approach, the authors also studied the ideas theoretically. The authors argue that the usual approach of discussing the expressivity of ANNs in terms of the continuous function domain that they are able to express is not as useful as studying the expressive power of ANNs on a finite sample of data. They construct a theoretical 2 layer [ReLU](https://en.wikipedia.org/wiki/Rectifier_(neural_networks)) network to study the expressivity of neural networks on a finite sample of data.

The role played by the implicit regularization provided by [stochastic gradient descent](http://stats.stackexchange.com/questions/153696/data-augmentation-techniques-for-general-datasets) in the ANN training process is studied theoretically by appealing to linear models.

###What did they find?###
Deep neural networks easily fit random labels. This is a hallmark of memorization.

Explicit regularization may improve generalization performance, but is neither necessary nor by itself sufficient for controlling generalization error.

There exists a two-layer neural network with [ReLU](https://en.wikipedia.org/wiki/Rectifier_(neural_networks)) activations and 2n+d weights that can represent any function on a sample size n in d dimensions. This means that even moderately-sized neural networks are capable of memorizing every training sample.

With linear models, stochastic gradient descent behaves as an implicit regularizer. However, this observation doesn't explain why certain ANN architectures perform better than others, since SGD is used in many different architectures. The authors suggest that it should get more attention for its role in the generalization performance of ANNs.

###What has the response been from other researchers?###
A more recent paper is a response to this "Rethinking Generalization" paper: [DEEP NETS DON’T LEARN VIA MEMORIZATION](https://openreview.net/pdf?id=rJv6ZgHYg) by Kreuger, et al.

This later paper is skeptical of the conclusions in the "Rethinking Generalization" paper. They reproduced the randomization experiments, but paid closer attention to the capacity of the trained networks, the time to convergence during training, and the complexity of the functions learned. They showed that although the neural networks can memorize random data, it is significantly more difficult for them to do so than with natural data. From their results, they came to the conclusion that massive memorization cannot explain the training and generalization performance of the networks. 

This casts doubt on the conclusion that the Zhang, et al team make in the "Conclusion" section: "Our results challenge the classical view of learning by showing that many successful neural networks easily have the effective capacity for sheer memorization. This leads us to believe that these models may very well make use of massive memorization when tackling the problems they are trained to solve." The basic experimental results of both papers are compatible with each other, as far as I can tell, but the conflict between different interpretations of the results highlights the difficulties in explaining the generalization ability of ANNs.

The debate rages on!

###Glossary
* [Artificial Neural Network](https://en.wikipedia.org/wiki/Artificial_neural_network) - A computational model consisting of interconnected artificial neurons. Machine learning problems can be solved by optimizing weights associated with the connections.
* [Data Augmentation](http://stats.stackexchange.com/questions/153696/data-augmentation-techniques-for-general-datasets) - A regularization technique where overfitting is prevented by creating additional training examples from the training set by applying transformations that do not affect the example's label. For image data, these transformations often include rotations, mirroring, adjusting the contrast, etc.
* [Dropout](https://en.wikipedia.org/wiki/Dropout_(neural_networks)) - A regularization method that prevents overfitting by randomly dropping neurons from the network during training.
* [Rademacher complexity](https://en.wikipedia.org/wiki/Rademacher_complexity) - Measures a model's capability of fitting all possible +/-1 binary label assignments.
* [Uniform stability] (https://en.wikipedia.org/wiki/Stability_(learning_theory)) - How sensitive an algorithm is to the replacement of a single example. This is a property of the algorithm and does not take into account the data or the labels.
* [ReLU](https://en.wikipedia.org/wiki/Rectifier_(neural_networks)) - Rectified Linear Unit. A non-linear activation function for artificial neurons. ReLU(x) = max(0,x).
* [Stochastic Gradient Descent](http://stats.stackexchange.com/questions/153696/data-augmentation-techniques-for-general-datasets) - An approximate method for solving an optimization problem, frequently used in ANNs. A sample of examples is used to compute an approximate gradient at each iteration.
* [VC-dimension](https://en.wikipedia.org/wiki/VC_dimension) - The cardinality of the largest set of points that the classification algorithm can shatter.
* [Weight Decay](https://en.wikipedia.org/wiki/Regularization_(mathematics)#Regularization_in_statistics_and_machine_learning) - A regularization method which restricts the complexity of the neural network (and therefore prevents overfitting) by penalizing large weights in the loss function.
