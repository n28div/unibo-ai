# ML and theory of computation

How can we see ML as an input-output task? Encoding! There's a canonical way of seeing a problem as a function, or better its **characteristic function**, i.e. something telling us whether a function is inside or outside $\mathcal{L}$. Any learning algorithm actually computes a function having input the training data, producing in output classifiers. We are of course restricting the scope: we're talking about supervised learning.

Seeing data as binary strings is kinda easy: everything can be encoded as binary strings. But how about classifiers? Depending on the domain, the thing can be quite different! The classifier itself is a function: it takes data as input, and outputs a class. The output of learning is an algorithm itself!

The kind of rectangles we use to label data are not standard rectangles: the vertices are perfectly aligned with the axis. The algorithm knows that data are labeled according to a rectangle, but it doesn't know the actual rectangle. We'd like our classifier to converge to a correct one the more training data we add. Converge to what? The classifier that was _implicitly used_ when labeling the data.

Another crucial point is the following: how about how the data is created? Are we sure that the data _arrives_ in the right square? It may well happen that the distribution is not standard. We'd like our algorithm to be robust, i.e. independently on the distribution of the training data, the algorithm still produces good results. The algorithm is supposed to work for every possible distribution, not just for one.

We could define an algorithm that given the data, determines the smallest rectangle R including all the positive instances, then return R. This rectangle could be very different from the target. But it's not that easy to conclude that it is a wrong algorithm. The only thing we can hope for is that it is wrong on limits, while correctness holds for the majority of cases. We have to talk about **accuracy**.

We could consider accuracy as a parameter, by denoting how much of the data has to fit into the rectangle.Our classifier is now created by a function that takes **confidence** as a parameter, creating a classifier that has an **accuracy**.

This example only talks about rectangles. Let's now try to make the whole thing a little bit more generic.

The first important concept is that of an **instance space**, i.e. a space from which we draw data. In this case, we draw data from the bidimensional cartesian plane. **Concepts** are subsets of X. What is more important is a **concept class**, a collection of concepts, namely a subset of the set of all subsets of X. Among all possible properties, we are interested in some of them. A concept class kind of restricts our attention to those concepts which are interesting. Then, among the elements of the concept there's one called **target concept** which is what the learner wants to build a classifier for. Note that this is not known to the learner, which wants to understand it by examples.

This is not just about the data anymore, rather the confidence, the accuracy and EX(c,D), considerable as an _oracle_, which the algorithm can use to **produce labeled data** without knowing $c$ and $D$.
The algorithm queries the _oracle_, in this way we can model the fact than in this point of view the algorithm A is asked to **guarantee** a certain error parameter and confidence parameter, and based on that it queries the oracle a certain amount of times. Why is that? We want the algorithm to be error-aware.
If we couldn't query it as many times as we'd like, our algorithm would guarantee just a certain maximum level of accuracy/confidence, and these two parameters would be bounded by the number of examples we have. That's why we don't take the data as input, rather an _oracle_ that can be queried as many times as needed.

The error of any $h$ output of the algorithm is defined as the probability that for any $x$ drawn from any distribution, the output is different from the actual target concept.

A concept class is PAC learnable if there is an algorithm which can learn it, in the sense that we're kind of hinting between the lines previously. It is PAC learnable if there's an algorithm such that for every $c$, for every distribution, for bounded accuracy and confidence we have:

$$
\operatorname{Pr}\left[\operatorname{error}_{\mathbf{D}, c}(\mathcal{A}(E X(c, \mathbf{D}), \varepsilon, \delta))<\varepsilon\right]>1-\delta
$$

If you find out that your concept class is too hard to learn (not PAC learnable), you are trying to solve a task which is too complicated.

We assume concepts to be represented by binary string: **a representation class**.

Boolean vectors can be of arbitrary length, but if you fix the $n$ and you just construct and instance class of all boolean vectors. Boolean vectors aren't just assignments of truth values to variables, and one way of isolating a certain class of boolean vectors is just giving a formula, for example a CNF (a formula in propositional logic), you isolate some of these sets. The first example of representation class is the class of all conjunctions of literals. Any boolean function can be written in CNF, then any subsets of $\{0,1\}$ can be captured this way. Any subset of the instance class can be defined in this way! We can also consider $kCNF$s rather than one, though losing universality: not all boolean functions can be represented by CNFs of a certain degree (all clauses of at most $k$ literals).

Learning conjunctions of literals is possible: if your target concept is a conjunction of literals, the learning algorithm can just take in input data (boolean vectors) and $b$ telling it whether the $s$ is part of the concept, i.e. it satisfies the conjunction of literals $c$. Then, the internal state just becomes a conjunction of states, starting from a conjunction in which all literals are mentioned in the negated AND non-negated form, then as soon as the data comes, the state is updated.

#

[Previous section](4%20-%20Between%20feasible%20and%20unfeasible.md) · [Next Section](6%20-%20Computational%20Learning%20Theory.md) · [Solved exercises](Solved%20Exercises.md)
