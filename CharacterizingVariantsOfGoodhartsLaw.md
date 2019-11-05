# Characterizing Variants of Goodhart's Law
## Dan Mazur, November 2019
## Prepared for the [Advanced Data Science Reading Meetup](https://www.meetup.com/LearnDataScience/events/wwqpgryzpbjb/), Vancouver, BC

[Characterizing Variants of Goodhart's Law](https://arxiv.org/abs/1803.04585) - David Manheim, Scott Garrabrant

### What problem are they trying to solve?
This paper is a discussion that aims to categorize failure modes caused by overoptimizing a metric in optimization problems. 
The framework imagines an optimization problem with a metric and a true goal that are different depending on the failure mode.
We know the problem is "overoptimized" when further optimization is either ineffective or harmful toward the true goal.

### Why is this an interesting problem?
The failure modes discussed in this paper can help explain a wide variety of real-world problems. 
In data science work, we are often trying to optimize metrics, whether through machine learning, or applying decision theory 
to business problems. The metrics that we optimize are very rarely the true goal of our clients/employers. Therefore, 
we are always at risk of encountering these failure modes. Understanding how to think of these failures in a consistent framework,
and identifying the similarities and differences in the different variants can help us to avoid making mistakes.

### What are the failure modes?
* Regressional Goodhart - The most basic version. As your system becomes close to optimal, any difference between the goal and the metric may cause further optimization to move the system further away from the goal. 
  * e.g. In machine learning, the familiar example is "overfitting" where the metric is the training loss and the goal is the test loss, or another real-world performance metric.
* Extremal Goodhart - This failure mode occurs when the metric is useful for 'normal' examples, but when selecting for very extreme examples, the relationship between the metric and the goal is not as reliable. There are two ways this can occur:
  * Model Insufficiency - The expected relationship between the metric and the goal is simpler than the reality and breaks down. 
    * e.g. In machine learning: Underfitting. A linear model may fit well near where the training data were collected, but fail when selection pressure moves the metric toward regions where non-linear effects are important for the goal.
  * Change in Regime - The relationship between the goal and the metric may be different for different values of the metric. 
    * e.g. In basketball, it is generally good to have taller players on a team. But, extremely tall people may be more likely to have complications that prevent them from being good basketball players. [Robert Wadlow](https://en.wikipedia.org/wiki/Robert_Wadlow) was 8'11", but required leg braces for walking and had poor feeling in his legs and feed.
    * e.g. Humans evolved to optimize for eating sugar because they were valuable but scarce sources of energy. Today, many humans eat unhealthy amounts of sugar.
* Causal Goodhart - In this category of failure modes, the actions taken by the regulator change the relationship between the goal and the metric.
  * Shared Cause Intervention - Both the metric and the goal are caused by a common factor. The regulator intervenes in the common factor and breaks the causal relationship.
    * e.g. An advertising campaign causes both more customers and more media coverage. After learning this, we put a ton of money into advertising. After that intervention, the correlation between our customer aquisition and our media coverage is likely to be smaller than before our intervention.
  * Intermediary Intervention - In this case, The Goal causes a factor, X, which causes The Metric.
    * e.g. 
  * Metric Manipulation - 
* Adversarial Goodhart - 
  * Adversarial Misalignment / Campbell's Law - 
  * The Cobra Effect - 

### What did they find?
TODO

### Glossary
**The Metric / The Proxy** - The objective that is being optimized for. The paper alternates between referring to a metric or the proxy.
**The Goal** - The "real" objective that one wants to optimize for by solving the optimization problem using the metric. We can not directly act on the goal because of incomplete knowledge, so we act on the metric/proxy.
**The Regulator** - An agent who makes decisions to optimize the metric/proxy.
