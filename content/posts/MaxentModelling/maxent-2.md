---
title: "Maximum Entropy Model - The details (Part 2/3)"
date: 2018-12-06T19:02:00+05:30
---

### Model representation

**Output value:** 
> $y_i \in Y$
> where $Y$ is a finite set $\{y_1, y_2,...,y_n\}$

Let's take for example, the translation model from [my previous post]({{< ref "./maxent-1.md" >}})

The task is to find the best translation of the word _in_ to French. From the training data we infer that the translations of _in_ to French typically is one of the following
_{dans, en, à, au cours de, pendant}_

here, $Y = \{dans, en, à, au cours de, pendant\}$

**Contextual Information:**

In generating the output $y$ there could be contextual information that influences the output, example, the words sorrounding _in_ in a sentence.

This is represented as:

> $x_i \in X$
> where $X$ is a finite set $\{x_1, x_2,..,x_n\}$

**Empirical Probability Distribution:**

This is nothing but the probability that _you can count_ in your training data.

Example: If event A occurs m times in your training data and there are n observations,  then the empirical probability of A is

$p̃(A) = \frac{m}{n}$

We take a large number of training samples $(x_1, y_1), (x_2, y_2)...,(x_N, y_N)$

and calculate the empirical probability as

$p̃(y_i, x_i) = \frac{number\ of\ times\ (y_i, x_i)\ occurs\ in\ the\ sample}{N}$

#### Features and Constraints**

Our goal is to construct a statistical model of the process which generated the training sample $p̃(y,x)$

**Feature Function/Feature**

This is a function that models the observation $y_i$ given some _context_ $x_i$ 

Example:
Going back to the translation of _in_, we might observe in the training sample that _in_ translates as _en_ every time _April_ follows _in_

here the context $x_i$ is _April follows in_ and the output $y_i$ is _en_

$f(y_i, x_i) = \\begin{cases}
              1\ if\ y = en\ and\ April\ follows\ in \\\ 
              0\ otherwise \\\
          \\end{cases}$


The [expected value](https://en.wikipedia.org/wiki/Expected_value#Finite_case) of $f(Y, X)$ w.r.t the **empirical probability distribution** $p̃(y_i, x_i)$ is given by:

> $p̃(f) = \sum_{x,y}p̃(y_i, x_i)f(y_i, x_i)$ ---- (1)

Say we compute a model $p(y|x)$ 
i.e, probability of output $y$ [condtioned](http://setosa.io/conditional/) upon $x$

We represent the _feature function's_ expected probability w.r.t the __model $p(y|x)$__ as follows

> $p(f) = \sum_{x,y}p̃(x)p(y|x)f(y,x)$ ---- (2)
> where $p̃(x)$ is the _empirical probability_ of $x$

**Constraints**

$p(y,x)$ is the _joint probability_ of x and y

$p(y|x)$ is the [_conditional probability_](https://en.wikipedia.org/wiki/Conditional_probability) of the output $y$ given a context $x$

By definition of conditional probability, we must have

$p(y,x) = p(y|x)p(x)$

Ideally, _empirical probability_ and the _model_ must match. i.e., the output of the _model_ must be exactly the same as what we can measure

based on this assumption, we add the following contsraint

> $p̃(f) = p(f)$ ---- (3)

**Constraint Equation**

Combining (1), (2) and (3)

we write our _constraint equation_ as 

$ \sum_{x,y} p̃(x)p(y|x)f(y,x) = $ $ \sum p̃(x)p(y|x)f(y,x)$

**The Maxent Principle**

The [conditional entropy](https://en.wikipedia.org/wiki/Conditional_entropy) $H(Y|X)$ is given as

$H(Y|X) = - \sum_{y_i,x_i} p(y_i, x_i)\ log\ p(y|x)$

Or

$H(Y|X) = - \sum_{y_i,x_i} p̃(x)p(y|x)\ log\ p(y|x)$

Following the [principle of maximum entropy]({{< ref "./maxent-1.md" >}}), of all possible models $p(y|x)$ we choose the one with the maximum entropy

$p^* = \underset{p \in C}{\mathrm{argmax} H(p)}$

Where $C$ is a set of constraints $C = \{c_1, c_2,..., c_n\}$

### The primal problem

The problem now becomes one of finding

$p^* = \underset{p \in C}{\mathrm{argmax} H(p)}$

Subject to the following constraints:

1. $p(y|x) \ge 0\ for\ all\  x,y $
2. $\sum_{y}p(y|x) = 1\ for\ all\ x$
3. $ \sum_{x,y} p̃(x)p(y|x)f(y,x) = $ $ \sum p̃(x)p(y|x)f(y,x)$


This [constrained optimization](https://www.khanacademy.org/math/multivariable-calculus/applications-of-multivariable-derivatives/lagrange-multipliers-and-constrained-optimization/v/constrained-optimization-introduction) problem is solved using the Lagrangian

### The equation for optimization

The parametric form of the constrained optimization problem is

$p^*(y|X) = \frac{e^{\sum_{i}\lambda_if_i(y_i,x_i)}}{\sum_y e^{\sum_i\lambda_i f_i(y_i, x_i)}}$

Now we have the problem of finding value for parameter $\lambda$ that gives us the maximum value for y

### References

1. Maxent Modelling Tutorial - https://www.cs.cmu.edu/afs/cs/user/aberger/www/html/tutorial/node3.html

2. A Simple Introduction to Maximum Entropy Models for Natural Language Processing - https://repository.upenn.edu/cgi/viewcontent.cgi?article=1083&context=ircs_reports

3. [Jaynes, 1957] Jaynes, E. T. (1957). Information Theory and Statistical Mechanics. _Physical Review_, 106:620-630

4. https://en.wikipedia.org/wiki/Expected_value#Finite_case

5. https://people.eecs.berkeley.edu/~klein/papers/maxent-tutorial-slides.pdf