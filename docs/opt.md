# Optimisation problems and optimisation schemes

This section presents the basic concepts and the nomenclature that will be used
throughout the rest of this course. Particularly, the description and formal
definition of an optimisation problem in the single-objective field is given.
Moreover, a taxonomy which classifies the optimisation schemes available for
dealing with optimisation problems is provided.

## Single-objective problems

Optimisation is one of the most important topics for a wide range of fields in science
and technology, such as computer science, operational research, and artificial
intelligence [75], as well as in other areas like finance, business, and medicine [211].
Given an optimisation problem, there exist different feasible solutions, and therefore
the main aim of optimisation is to find the best possible solution to a problem
from among all feasible solutions. Hence, solving an optimisation problem requires
finding said best solution by taking into consideration certain objectives while at
the same time satisfying certain constraints.

In order to obtain a solution for an optimisation problem, several decisions involving
the problem domain must be made. For example, consider a variant of the knapsack
problem [227, 235] in which a set of items, each with its corresponding profit and
weight, is given. The optimisation problem consists of deciding which items from
the set of candidate items will be stored into the knapsack so that the global profit
is maximised, while at the same time satisfying the constraint of maximum weight
that the knapsack is able to support. Different decisions are represented by a set
of decision variables, which is usually called the decision vector, and decisions are
carried out by assigning values to each variable belonging to the decision vector.
Continuing with the example of the knapsack problem, a possible decision vector
could contain a set of ones and zeros indicating whether an item is selected to be
stored or not.

The quality of a decision vector or solution has to be determined using certain criteria,
which are expressed as a computable function of the decision variables. Considering
this function, optimisation problems can be classified as Single-objective Optimisation
Problems or Multi-objective Optimisation Problems (MOPs). In singleobjective
optimisation problems a scalar function is defined, while in the multiobjective
field a vector or multiple objective function is applied. In the knapsack
example, if a unique knapsack is considered, a scalar function is defined, and therefore
a single-objective variant of the knapsack problem is addressed, whereas if multiple
knapsacks are taken into account, each of them with its associated function, a
multi-objective variant of the problem is defined.

The single-objective optimisation problem, as described in Definition 1 [70], can be
handled using a wide variety of optimisation schemes.

A general **single-objective optimisation problem** is defined as minimising (or
maximising) $f(x)$ subject to $g_{i}(x) \leq 0$, $i = \{1, \ldots, m\}$ and
$h_{j}(x) = 0$, $j = \{1, \ldots, p\}$ $x \in \Omega$.

A solution or decision vector $x = (x_1, \ldots, x_n)$ is an $n$-dimensional vector.
It is important to note that $x$ can be a vector of continuous or discrete decision variables
(or even a mix), whereas the scalar function $f$ can also be continuous or discrete.
Moreover, $g_{i}(x) \leq 0$ and $h_{j}(x) = 0$ are inequality and equality constraints that
must be satisfied while optimising (minimising or maximising ) $f(x)$.
Hence, $\Omega$ contains all possible solutions $x$ that can be used to satisfy an evaluation of $f(x)$
and its constraints, i.e. $\Omega$ is the set that determines the {\it feasible region} of $x$.

The process of finding the global optimum---or global optima---of any function is referred to as
*Global Optimisation*. From now on, and without loss of generality, a single-objective optimisation
problem to be minimised will be considered. Taking this into account, the global minimum of a
single-objective problem [16] is defined as follows.

Given a function $f: \Omega \subseteq \mathbb{R}^{n} \rightarrow \mathbb{R}$,
$\Omega \neq \emptyset$ for $x^\* \in \Omega$ the value $f^{\*} \stackrel{\vartriangle}{=} f(x^{*}) > -\infty$ is called a **global minimum**
if and only if

```math
   \forall x \in \Omega: f(x^{*}) \leq f(x)
```

Thus, $x^{\*}$ is called the *global minimum solution* and $f$ is denoted as the {\it objective function}.
Note that the inequality in the above equation indicates that several global minimum solutions could
exist for a single-objective optimisation problem.  The aim of obtaining the global minimum solution
(or solutions) is therefore known as the *global optimisation problem*.

## Optimisation schemes

