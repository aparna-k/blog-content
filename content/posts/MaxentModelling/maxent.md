---
title: "Maximum Entropy Model"
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

### References

1. Maxent Modelling Tutorial - https://www.cs.cmu.edu/afs/cs/user/aberger/www/html/tutorial/node3.html

2. A Simple Introduction to Maximum Entropy Models for Natural Language Processing - https://repository.upenn.edu/cgi/viewcontent.cgi?article=1083&context=ircs_reports

3. [Jaynes, 1957] Jaynes, E. T. (1957). Information Theory and Statistical Mechanics. _Physical Review_, 106:620-630
