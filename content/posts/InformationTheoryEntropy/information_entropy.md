---
title: "The idea of Information Entropy"
date: 2018-12-01T19:02:42+05:30
---

## Information Entropy

> Information entropy quantifies the average amount of information in an event.

We could also think of entropy as a measure of _unpredictability_.


### Information - Intuition

Let's consider the following three sentences

1. Tomorrow, the sun will rise from the East
2. The phone will ring in the next one hour
3. It will snow in [Mumbai](https://en.wikipedia.org/wiki/Mumbai) this winter

When we consider the _amount of information_ in the three sentences above, there are two ways to think about it.

- _How many bits_ do we require to transmit each sentence?
- _How much do we learn_ from each sentence?

The answers to these two questions don't necessarily have a relationship

The first sentence, _Tomorrow, the sun will rise from the East_ probably requires the most amount of bits to transmit the information.

But, in terms of what we learn, does it really tell us anything useful?

> It doesn't. The sun will rise from the East tomorrow with a _probability of 100%_ the sentence _adds no information_

The second sentence, _The phone will ring in the next one hour_ - tells us something we wouldn't know.

> Without any information, all we can guess about a phone ringing in the next hour is that _the probability that the phone rings is 50_, the sentence changes this probability to a _100%_. Therefore, we can say that this sentence _adds some information_

If we know anything about Mumbai, we would predict a _0% probability_ of snow

> When we read the third sentence, it's bound to raise some eyebrows. Nevertheless, it moves our estimate of probability from _0% to a 100_, that is adding a lot of information.

The intuition, I hope is beginning to build now. We see that lower the probability of an event happening, the more information we gain from a sentence that changes our estimate of the event's probability.

Or, we could say, _Information_ is _inversely proportional_ to the _probability of that event_

> $Information \propto \frac{1}{Probability\ of\ the\ event}$

Formally, this is defined as:

> For a discrete random variable $X$ with possible outcomes $x_i, i=1,2,3,..,n$, the _Self Information_ of the event $X=x_i$ is defined as:

> $I(x_i) = \log\{\frac{1}{p(x_i)}\}$ $= -log\ p(x_i)$

> Where, $p(x_i)$ is the probability that $X$ takes on the value $x_i$


### Information Entropy

Representation of Entropy $H(X)$

> $H(X) = -\sum_{x \in X} p(x)\log_2(p(x))$

Or, in other words, this is the _mean_ or _expectation_ of Information

#### Intuition

Let's go back to the _plain English_ definition of Entropy, i.e., "Entropy is a measure of _unpredictability_."

An intuition for why this is true can be achieved by the following graph

<img class="special-img-class" style="max-width:400px; max-height:450px" src="/img/information_entropy/Binary_entropy_plot.svg"/>

This is the graph for entropy for random variable $X$ with two possible outcomes.

Like, a coin toss, where we only have two states

Say, we represent this as follows:

> $X = {1,\ if\ Head = True; 0\ if Head = False}$

- If the coin is rigged,  and we know that a toss ___always___ results in a _head_, i.e., the probability $p(X = 1) = 1$

- Also, $p(X = 0) = 0$

Intuitively, if we already know this information, that the coin is rigged, there is _no uncertainity_, which means the entropy is 0

> $H(X) = - [ 1 \times \log_2(1) + 0 \times \log_2(0)] = 0$

If we had a fair coin, we have an equal chance of any result, i.e,

$P(X = 1) = 0.5$
$P(X = 0) = 0.5$

Then,

> $H(X) = - [ 0.5 \times \log_2(0.5) + 0.5 \times \log_2(0.5)] = 1$

This is the __highest possible value for entropy__ for this system, in other words, _anything can happen with equal probability_


### References:

1. NPTEL - Information Theory, Coding and Cryptography - https://nptel.ac.in/courses/108102117/1

2. Information Entropy - https://www.khanacademy.org/computing/computer-science/informationtheory/moderninfotheory/v/information-entropy

3. https://en.wikipedia.org/wiki/Entropy_(information_theory)

4. http://micro.stanford.edu/~caiwei/me334/Chap7_Entropy_v04.pdf

5. https://www.quora.com/Why-is-there-a-logarithmic-function-in-the-entropy-formula

6. https://revisionmaths.com/advanced-level-maths-revision/statistics/expectation-and-variance