---
title: "Maximum Entropy Model - Intuition (Part 1/2)"
date: 2018-12-04T19:02:00+05:30
---

### Principle of Maximum Entropy

> "In making inferences on the basis of partial information we must use that probability distribution which has _maximum entropy_ subject to whatever is known. This is the only _unbiased_ assignment we can make; to use any other would amount to arbitrary assumption of information which,___by hypothesis, we do not have___" - [Jaynes, 1957]

If you are unfamiliar with the term _information entropy_, refer to [my previous post]({{< ref "../InformationTheoryEntropy/information_entropy.md" >}})

Say, you know that a person, Sally, has only shirts in 5 colours that she wears to work everyday. 

The shirts are red, blue, green, yellow and pink in colour.  

If this is all you knew and you were asked to __calculate the probability__ that Sally would were a _pink_ shirt on a given day, what would your response be?

I hope your answer was: 20% or 1/5

The reason that is the correct answer, is because, without any other information, all we can assume is that Sally wears any of the shirts on a given day ___with equal probability___

i.e., if $X$ is the random variable represnting the choice of colour on a given day, you would assign

p(X = red) = 1/5<br/>
p(X = blue) = 1/5<br/>
p(X = green) = 1/5<br/>
p(X = yellow) = 1/5<br/>
p(X = pink) = 1/5<br/>

If you recall, from [my previous post]({{< ref "../InformationTheoryEntropy/information_entropy.md" >}}), we know that 

>Entropy is maximum when all probabilities are equally distributed

Why? Because, entropy is a measure of _unpredictability_ of a system, if all events in the system are equally likely, then the unpredicatbility is the highest

Intuitively, what we have done here by assigning equal probability to all outcomes is _follow the principle of maximum entropy_

### Maximum Entropy Model - Motivating Example

Say, we are building a English to French translator.

To do this, we collect a large sample of translations by an expert translator. We will use observations from this dataset to build our model.

Let's zoom into one small part of the problem, the translation of the word _in_.

To understand the best translation for the word _in_ in French, we look through our dataset and come up with all possible translations of _in_ to French. 

We notice that, _in_ has always been translated to one of the following five French phrases: _{ dans, en, à, au cours de, pendant }_

__Representation__

$p(dans) = \frac{1}{5}$ 

Probability that the translation of _in_ to French is _dans_ is $\frac{1}{5}$

__Model__

If we have the fiven 5 words to choose from, then

> $p(dans) + p(en) + p(à) + p(au cours de) + p(pendant) = 1$

This will be our first _constraint_, the model will have to always obey this.

There are infinite possibilities that obey this contatraint.

_For Ex:_
  $p(pendant) = \frac{1}{2}$ & $p(dans) = \frac{1}{2}$

obeys the constraint. But, we obviously cannot begin there.

We will always begin with probabilities that will _maximize entropy_ 

i.e.,

$p(dans) = \frac{1}{5}$ <br/>
$p(en) = \frac{1}{5}$ <br/>
$p(à) = \frac{1}{5}$ <br/>
$p(au cours de) = \frac{1}{5}$ <br/>
$p(pendant) = \frac{1}{5}$ <br/>

This model, which allocates the total probability evenly among the five possible phrases, is the most uniform model subject to our knowledge.

Say, we look through our data again and find that, approximately 30% of the time the translation for _in_ was _dans_ or _en_

Now we have two constraints

> $p(dans) + p(en) + p(à) + p(au cours de) + p(pendant) = 1$ <br/>
> $p(dans) + p(en) = \frac{1}{3}$

Once again, of all the possible probability distributions we assume the one that has _maximum entropy_

$p(dans) = \frac{3}{20}$ <br/>
$p(en) = \frac{3}{20}$ <br/>
$p(à) = \frac{7}{30}$ <br/>
$p(au cours de) = \frac{7}{30}$ <br/>
$p(pendant) = \frac{7}{30}$ <br/>

Say, in another pass through the data we figure out that, in half the cases the translation of _in_ was _dans_ or _à_

So, we now have 3 constraints

> $p(dans) + p(en) + p(à) + p(au cours de) + p(pendant) = 1$ <br/>
> $p(dans) + p(en) = \frac{1}{3}$ <br/>
> $p(dans) + p(à) = \frac{1}{2}$ <br/>

We can once again look for the most uniform distribution that satifies these constraints.

But, this time the choice is not as obvious. As we have added complexity, we have encountered two problems

1. What exactly is meant by _uniform_ and how can one measure the _uniformity_ of the model?

2. How do we find a uniform model subject to the set of constraints like we have placed in the example above?

_Maxent model_  answers both these questions.
Intuitively, the principle is simple
> Model all that is known, assume nothing about that which is unkown.

### References

1. Maxent Modelling Tutorial - https://www.cs.cmu.edu/afs/cs/user/aberger/www/html/tutorial/node3.html

2. A Simple Introduction to Maximum Entropy Models for Natural Language Processing - https://repository.upenn.edu/cgi/viewcontent.cgi?article=1083&context=ircs_reports

3. [Jaynes, 1957] Jaynes, E. T. (1957). Information Theory and Statistical Mechanics. _Physical Review_, 106:620-630
