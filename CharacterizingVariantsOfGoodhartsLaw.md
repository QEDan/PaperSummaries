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
TODO
* Regressional Goodhart - 
* Extremal Goodhart -
  * Model Insufficiency -
  * Change in Regime - 
* Causal Goodhart - 
  * Shared Cause - 
  * Intermediary Intervention - 
  * Metric Manipulation - 
* Adversarial Goodhart - 
  * Adversarial Misalignment / Campbell's Law - 
  * The Cobra Effect - 

### What did they find?
TODO

### Glossary
TODO
