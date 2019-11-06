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
    * e.g. When we spend money on digital advertising, we increase sales. But, if we spend an extremely high amount on digital advertising, spending more does not increase sales at all.
* Causal Goodhart - In this category of failure modes, the actions taken by the regulator change the relationship between the goal and the metric.
  * Shared Cause Intervention - Both the metric and the goal are caused by a common factor. The regulator intervenes in the common factor and breaks the causal relationship.
    * e.g. An advertising campaign causes both a higher click-through rate and more revenue. After learning this, we put a ton of money into advertising. After that intervention, the correlation between our click-through rate and our revenue is likely to be smaller than before our intervention.
  * Intermediary Intervention - In this case, The Goal causes a factor, X, which causes The Metric. The regulator intervenes in X, breaking the causal relationship between The Goal and The Metric.
    * e.g. We want to train a reinforcement learning agent to race a boat around a track in a video game. Winning the race gives the agent a large number of points, so we use points as our Metric. Instead of trying to win the race, the agent learns to do [donuts in an isolated lagoon](https://www.youtube.com/embed/tlOIHko8ySg) to score points.
    * e.g. More generally, it is a relatively common failure mode of reinforcement learning systems that they figure out a way to obtain the reward without performing the task. This is called [reward tampering](https://arxiv.org/abs/1908.04734v2).
  * Metric Manipulation - In this case, the regulator intervenes directly in the metric, breaking the relationship with the goal.
    * A student has a goal of learning physics. Instead of going to class and doing the homework, she hacks into the school computer and gives herself a passing grade at the end of term.
* Non-Causal Goodhart effects in Causal Systems - In these cases, the regulator is mistaken about the form of the causal relationship
  * Ignored Shared Cause - The regulator assumes there is a causal link between The Metric and The Goal when really, they have a shared cause.
    * e.g. The advertising department runs a very successful TV ad campaign on Sundays. The data science team does not know about this advertising campaign and notices that customers who shop on Sundays spend more money than other customers. The data science team assumes that getting customers to shop on Sunday instead of during the week will increase revenue.
  * Ignored intermediary - The regulator ignores an intermediary cause
  * Ignored additional cause - The regulator ignores an additional cause
* Adversarial Goodhart - In adversarial Goodhart examples, there are multiple actors. The other actors may have misaligned goals with the regulator, or the regulator may attempt to incentivise the other actors in a way that is harmful.
  * Adversarial Misalignment / Campbell's Law - In this case, the other agents are trying to corrupt The Metric because they have a goal other than the regulator's goal. 
    * e.g. A standardized test is used to determine which students will get the best employment and higher education opportunities. The students train specifically for the standardized test instead of their broader eduction.
    * e.g. Internet users [train a chatbot to say racist and offensive things](https://www.theverge.com/2016/3/24/11297050/tay-microsoft-chatbot-racist) because they think its funny.
    * e.g. A puppy is very well behaved until its owner leaves the house and then it causes destruction all over the house.
  * The Cobra Effect - In this case, the regulator incentivises an agent or agents toward The Metric, but the agents are not aligned on the regulator's Goal.
    * e.g. British authorities in India offered a bounty for dead snakes in an attempt to reduce the number of snakes in the countryside. People started breeding snakes to collect the bounty and the number of snakes increased as a result.
    * e.g. A factory offers an incentive for the workers to produce a large number of widgets. As a result, the factory produces very small widgets in enormous quantities. The widgets are too small to be useful to the company.

### Glossary
* **The Metric / The Proxy** - The objective that is being optimized for. The paper alternates between referring to a metric or the proxy.
* **The Goal** - The "real" objective that one wants to optimize for by solving the optimization problem using the metric. We can not directly act on the goal because of incomplete knowledge, so we act on the metric/proxy.
* **The Regulator** - An agent who makes decisions to optimize the metric/proxy.

### See Also
* [Goodhart Taxonomy](https://www.alignmentforum.org/posts/EbFABnst8LsidYs5Y/goodhart-taxonomy)
* [Classifying Specification Problems as Variants of Goodhart's Law](https://vkrakovna.wordpress.com/2019/08/19/classifying-specification-problems-as-variants-of-goodharts-law/)
