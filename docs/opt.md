# Optimisation problems and optimisation schemes

This section presents the basic concepts and the nomenclature that will be used
throughout the rest of this course. Particularly, the description and formal
definition of an optimisation problem in the single-objective field is given.
Moreover, a taxonomy which classifies the optimisation schemes available for
dealing with optimisation problems is provided.

## Single-objective problems

Optimisation is one of the most important topics for a wide range of fields in science
and technology, such as computer science, operational research, and artificial
intelligence, as well as in other areas like finance, business, and medicine.
Given an optimisation problem, there exist different feasible solutions, and therefore
the main aim of optimisation is to find the best possible solution to a problem
from among all feasible solutions. Hence, solving an optimisation problem requires
finding said best solution by taking into consideration certain objectives while at
the same time satisfying certain constraints.

In order to obtain a solution for an optimisation problem, several decisions involving
the problem domain must be made. For example, consider a variant of the knapsack
problem in which a set of items, each with its corresponding profit and
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
Problems or Multi-objective Optimisation Problems (MOPs). In single-objective
optimisation problems a scalar function is defined, while in the multi-objective
field a vector or multiple objective function is applied. In the knapsack
example, if a unique knapsack is considered, a scalar function is defined, and therefore
a single-objective variant of the knapsack problem is addressed, whereas if multiple
knapsacks are taken into account, each of them with its associated function, a
multi-objective variant of the problem is defined.

The single-objective optimisation problem can be handled using a wide variety of optimisation schemes.

A general **single-objective optimisation problem** is defined as minimising (or
maximising) $f(x)$ subject to $g_{i}(x) \leq 0$, $i = \{1, \ldots, m\}$ and
$h_{j}(x) = 0$, $j = \{1, \ldots, p\}$ $x \in \Omega$.

A solution or decision vector $x = (x_1, \ldots, x_n)$ is an $n$-dimensional vector.
It is important to note that $x$ can be a vector of continuous or discrete decision variables
(or even a mix), whereas the scalar function $f$ can also be continuous or discrete.
Moreover, $g_{i}(x) \leq 0$ and $h_{j}(x) = 0$ are inequality and equality constraints that
must be satisfied while optimising (minimising or maximising ) $f(x)$.
Hence, $\Omega$ contains all possible solutions $x$ that can be used to satisfy an evaluation of $f(x)$
and its constraints, i.e. $\Omega$ is the set that determines the *feasible region* of $x$.

The process of finding the global optimum---or global optima---of any function is referred to as
*Global Optimisation*. From now on, and without loss of generality, a single-objective optimisation
problem to be minimised will be considered. Taking this into account, the global minimum of a
single-objective problem is defined as follows.

Given a function $f: \Omega \subseteq \mathbb{R}^{n} \rightarrow \mathbb{R}$,
$\Omega \neq \emptyset$ for $x^\* \in \Omega$ the value $f^{\*} \stackrel{\vartriangle}{=} f(x^{*}) > -\infty$ is called a **global minimum**
if and only if

```math
   \forall x \in \Omega: f(x^{*}) \leq f(x)
```

Thus, $x^{\*}$ is called the *global minimum solution* and $f$ is denoted as the *objective function*.
Note that the inequality in the above equation indicates that several global minimum solutions could
exist for a single-objective optimisation problem.  The aim of obtaining the global minimum solution
(or solutions) is therefore known as the *global optimisation problem*.

## Optimisation schemes

A wide range of optimisation schemes has been designed for dealing with optimisation
problems.  These optimisation schemes can be classified using different taxonomies.
One of the most frequently used differentiates between  *exact algorithms* and *approximate algorithms*.
In order to use this classification, some notions regarding complexity theory are
first given in this section.
Among the approximate algorithms, *meta-heuristics* emerge as general optimisation
techniques and yield solutions of acceptable quality in a reasonable execution
time frame when solving a wide range of complex optimisation problems.
Meta-heuristics, in turn, can be divided into *trajectory-based methods* and
*population-based schemes*.
Trajectory-based methods only have to consider a unique solution, whereas population-based
approaches have to maintain a set of candidate solutions during the entire optimisation procedure.
Since this course focuses on population-based meta-heuristics, two of the main issues that arise
during their use, i.e. *premature convergence* and *parameter setting* are described. Finally,
a few notions concerning measuring the performance of optimisation schemes are presented
at the end of this section.

### Complexity theory

In this section, some results on tractability of problem solving are given.
Computational problems represent tasks that, in principle, can be solved by a computer.
A decision problem is a special type of computational problem whose answer is
either "yes" or "no". Decision problems can be *decidable* or *undecidable*.
The latter category includes problems for which an algorithm that solves
them will never exist, even having an unlimited amount of computational resources
and time. An example of an undecidable problem is the *halting problem*.
Determining the resources required by algorithms and problems is important.
This is precisely the goal of complexity analysis.

#### Algorithm complexity

Algorithms need time and space (memory) as resources for solving a problem.
An algorithm's complexity can prove useful when analysing its limitations and predicting its
resource requirements with a view to terminating its execution.
If the time frame is considered, the complexity of an algorithm is the number of steps
required to solve a problem whose size is equal to $n$, and is usually defined
considering the worst-case analysis. Knowing the exact number of steps is not necessary,
but an asymptotic bound of this number is required.

The $O$-notation is one of the most frequently used when analysing algorithms.
It is based on the asymptotic analysis and it can be used to compute the time and/or
space complexity of an algorithm. The asymptotic analysis of algorithms allows
characterising the growth rate of their complexity as a function of the problem size.
It is important to note that there exist two other well-known notations for analysing
algorithms. They are the $\Omega$-notation and the $\Theta$-notation.

If we consider the $O$-notation, an algorithm has a complexity
$f(n) = O(g(n))$ if there exist positive constants $n_0$ and $c$ such
that $\forall n > n_0, f(n) \leq c \cdot g(n)$

In other words, the function $g(n)$ is an upper bound for the function $f(n)$, i.e.
$f(n)$ grows asymptotically no higher than $g(n)$.

An algorithm is a **polynomial-time algorithm** if its time complexity is $O(p(n))$,
where $p(n)$ is a polynomial function of $n$.

Hence, a polynomial-time algorithm has a polynomial time complexity of $O(n^k)$, where $k$
is the degree of the upper bound polynomial function.

An algorithm is an **exponential-time algorithm** if its time complexity is $O(c^n)$,
where $c > 1$ is a real constant.

#### Problem complexity

A problem is *tractable* if there exists a polynomial-time algorithm that solves it.
In contrast, a problem is *intractable* if no polynomial-time algorithm exists that solves it.
Complexity theory commonly deals with decision problems. It also address other types of problems,
such as function problems and optimisation problems, among others.
However, we should note that any function problem or optimisation problem can always be reduced
to a decision problem. One of the main objectives of computational theory is to categorise
problems into complexity classes. A complexity class is a set of problems of related complexity.
Two of the most important complexity classes are $P$ and $NP$.

The **complexity class P** contains all decision problems which can be solved by a
deterministic algorithm in polynomial time.

A deterministic algorithm is polynomial for a decision problem $A$ if its complexity,
assuming the worst-case, is bounded by a polynomial function $p(n)$ where $n$ is the
input size of a given instance $\alpha$. Examples of problems belonging to the
complexity class $P$ are minimum spanning tree, shortest path problems,
and maximum flow networks, among others.

The **complexity class NP** contains all decision problems which can be solved
by a non-deterministic Turing machine in polynomial time.

We should note that each decision problem in $P$ is also a member of the class $NP$.
However, whether or not $P = NP$ is an open research question.
In other words, it has been shown that for every decision problem belonging to
the class $P$ there exists a non-deterministic Turing machine that can solve it
in polynomial time. However, it is not known whether for every decision problem
belonging to the class $NP$ there exists a deterministic algorithm that solves
it in polynomial time.

A decision problem $A$ is **reduced polynomially** to a decision problem $B$ if,
for all input instances $\alpha$ for $A$, an input instance $\beta$ for $B$ can be
built in polynomial time, such that the answer to the instance $\alpha$ is "yes"
if and only if the answer to the instance $\beta$ is "yes".

A decision problem $A \in NP$ is **NP-complete** if all other problems that
belong to the class $NP$ can be reduced polynomially to $A$.

A direct claim of this definition is that if a deterministic polynomial-time algorithm
exists to solve an $NP$-complete problem, then all problems of class $NP$ might
be solved in polynomial time. $NP$-complete problems are the hardest $NP$ problems
to solve.

A problem $A$ is $NP$-hard if and only if there exists an $NP$-complete problem $B$
that can be reduced polynomially to $A$.

Informally, $NP$-hard problems are at least as hard as $NP$-complete problems.
However, it is important to note that $NP$-hard problems do not have to be included
in the class $NP$, since not all of them are decision problems. They can be
optimisation problems, for instance. Moreover, some $NP$-hard problems are not
included in the $NP$ class, despite being decision problems.
For instance, the halting problem is an $NP$-hard problem. It is also a decision
problem, but since it is undecidable, it is outside the class $NP$.
Finally, if an optimisation problem has an associated $NP$-complete decision problem,
said optimisation problem is $NP$-hard. The figure below shows the relationships among
the classes $P$, $NP$, $NP$-complete and $NP$-hard, considering $P \neq NP$.

![Relationship between different complexity classes ($P \neq NP$)](img/complexity_class.png)

$NP$-hard problems usually require exponential-time algorithms (unless $P = NP$) in
order to obtain the optimal solutions.
Most real complex applications are categorised as $NP$-hard optimisation problems.
Examples of $NP$-hard problems are scheduling problems, routing and covering problems,
or knapsack and cutting problems, among others.

Depending on a problem's complexity, it can be solved by *exact algorithms* or
by *approximate algorithms*. Exact approaches are able to obtain solutions
whose optimality is ensured. However, for $NP$-complete problems exact
algorithms cannot be applied (unless $P = NP$) since they become
non-polynomial-time algorithms, and therefore they are not able to provide
optimal solutions in a reasonable time for large instances.

In contrast, approximate or *heuristic* schemes are able to generate
high-quality solutions, even optimal ones, in a reasonable time. However,
using approximate algorithms does not guarantee that the optimal
solution will be found.

The next figure shows a possible taxonomy, which classifies
optimisation methods into exact and approximate schemes.

![Classification of optimisation methods](img/opt_sch_taxonomy.png)

### Exact algorithms

In the class of exact approaches, the following examples of classical methods can be
found: *dynamic programming*, *branch and bound methods*,
*A\* search methods*, and *constraint programming*, among others.
All the above approaches can be categorised as *enumerative methods*,
where the search for solutions involves exploring the whole feasible region and
dividing the optimisation problem into smaller sub-problems
by using the *divide and conquer strategy*.
When these sub-problems are solved, their solutions are combined in
order to obtain the complete solution of the initial problem.

#### Dynamic programming

Dynamic programming is based on dividing a problem into smaller sub-problems
that are then easier to solve. The optimal solution to the initial problem is thus
provided by obtaining the optimal solutions for each of the sub-problems, which
result from a sequence of partial decisions. In dynamic programming, the solution
to every solved sub-problem is stored in memory. In this way, solutions that have
been previously computed do not have to be recalculated. In addition, the procedure
does not enumerate the whole search space, since the partial decision sequences that
do not lead to the optimal solution are pruned.

#### Branch and bound and A* search methods

Branch and bound and A* search methods are based on an implicit
enumeration of all feasible solutions for a certain optimisation problem. In order
to explore the feasible region, a search tree with the following characteristics is
dynamically constructed:

* The root represents both the optimisation problem to be solved and, the whole
search space.
* The leaves represent the problem’s candidate solutions.
* The remaining nodes represent sub-problems.

In these methods, a bounding function is used to prune some of the sub-trees. This
function ensures that the search areas represented by these sub-trees do not have to
be searched in order to obtain the optimal solution to the problem.

#### Constraint programming

Constraint programming models optimisation problems as a set of variables
linked by a set of constraints. The variables take their values from a finite domain
of integers, with the constraints possibly having mathematical or symbolic forms.
Constraint programming is based on alternating *propagation* with search methods to
find a feasible solution. A propagation algorithm reduces (from variable domains)
the values that do not involve a feasible solution. Afterwards, a search algorithm
based on a search tree is executed in order to remove possible inconsistent values in
the variable domains. This search algorithm performs a branching step to divide the
current problem into sub-problems. Branching can instantiate a variable to a feasible
value or can add a new constraint. Thus, the problem of optimising an objective
function can be reduced to one of solving certain types of feasibility problems.

### Approximate algorithms

Approximate methods can be divided into two sub-classes:
*approximation algorithms* and *heuristic algorithms*.
Approximation algorithms provide demonstrable solution quality and provable run-time bounds.
In contrast, heuristics usually find reasonably good solutions in a reasonable time.
Heuristics can therefore be applied to large and difficult instances of a wide range of
complex problems. Heuristics can in turn be categorised into *tailored heuristics* and *meta-heuristics*.
Tailored heuristics are algorithms specifically designed to solve a particular problem
and/or instance, whereas meta-heuristics are general methods applicable for solving a wide
variety of optimisation problems. Meta-heuristics can be used as approaches that guide the
design of underlying heuristics in order to solve particular optimisation problems.

#### Approximation algorithms

Approximation algorithms guarantee that the solutions obtained are close enough to the global optimum.
An $\epsilon$-approximation algorithm is able to generate an approximate solution $s$ that is not less
than $\epsilon$ times the optimum solution $g$. Generally, $\epsilon$ is called the *approximation factor*
and it is used to establish the relative performance of the algorithm. This approximation factor can be a
constant or a function which depends on the size of the instance.

Approximation algorithms can be analysed to gain more knowledge regarding the difficulty of problems,
as a consequence of which more efficient heuristics can be designed. Nevertheless, approximation algorithms
are tailored approaches which depend on the problem at hand. In addition, these algorithms are not very
useful for complex applications because the approximated solutions are usually far from the global optimum.

#### Heuristic algorithms

A **heuristic** is a criterion, method, or principle for deciding which
of several alternative courses of action promises to be the most effective
in order to achieve some goal.

In order to design a heuristic, two main requirements have to be considered.
Firstly, a heuristic has to be simple and require a low consumption of computational
resources and time. Secondly, it has to make correct decisions instead of selecting bad choices.
Heuristics are usually tailor-made approaches that rely on information on
the problem or instance being solved to carry out their decisions.
Consequently, their design and implementation might become a difficult task.
Moreover, once a tailored heuristic is designed, it usually cannot be applied to
other optimisation problems and/or instances of the same problem.

In general, there are two main ways to apply heuristics: they can be used as stand-alone
optimisation techniques; or, they can be integrated together with other approaches.
In the second case, heuristics can help to improve the behaviour of other
methods, such as exact algorithms, by recommending the next set of candidate
solutions to be explored by the exact algorithm, for instance.
In contrast, other approaches can be used to improve the behaviour of heuristics,
like restarting, which as its name implies, restarts the heuristic when a certain
situation is detected, for example, stagnation over a certain number of iterations.
Finally, it is important to note that the combination of different heuristics might
improve the solutions obtained. However, this task is not easy and it might yield
improper results.

**Meta-heuristics** are top-level general strategies which guide other low-level heuristics
to search for feasible solutions in difficult domains.

In recent decades, meta-heuristics have been applied to a wide range of
fields, such as engineering design, aerodynamics, telecommunications, machine learning,
data mining, system modelling, signal processing, and planning and scheduling problems,
among others.
Meta-heuristics are general purpose strategies that, in general, do not make use of
problem-dependent information.
However, they can consider problem specific knowledge in the form of low-level heuristics
controlled by the top-level strategy.
The success of meta-heuristics stems from their ability to deal with large instances of
complex problems for which there are no applicable exact approaches.
Hence, the main aim of a meta-heuristic is to obtain solutions with "acceptable"
quality (close to the global optimum) in a reasonable time.
Meta-heuristics must therefore be designed with the aim of exploring the solution space
in a very efficient manner.
However, unlike exact or approximation algorithms, meta-heuristics are not able to
guarantee that global optima or even bounded solutions will be obtained.
Another drawback, which has become a significant research topic,
is to design effective stopping criteria for meta-heuristics.
Ideally, the execution would finish when convergence is detected, though actually detecting
this situation is an arduous task.
The most common stopping criterion is based on using an amount of
resources that is fixed before the execution starts, such as the execution time,
the number of iterations or the number of evaluations carried out on the objective
functions of the problem being solved.

One of the main issues that arise when designing meta-heuristics is striking the right
balance between the exploration of the whole search space (*diversification*) and
the exploitation of its most promising regions (*intensification*).
Promising regions are determined by the best solutions found at any given moment of the search
procedure.
Diversification tries to ensure that unexplored regions of the search space are
visited so that the search process is not bound to a reduced number of regions.
In contrast, intensification allows for a more exhaustive exploration of the search
space and thus aims to improve the quality of the best solutions
found by examining their neighbours.

A wide variety of meta-heuristics has been proposed, with the following being
among the most important: Ant Colony Optimisation (ACO), Artificial
Bee Colony (ABC), Artificial Immune System (AIS), Cultural Algorithms
CAs), Coevolutionary Algorithms (CEAs), Covariance Matrix Adaptation
Evolution Strategy (CMA-ES), Differential Evolution (DE), Estimation
of Distribution Algorithms (EDAs), Evolutionary Programming (EP),
Evolution Strategies (ES), Genetic Algorithms (GAs), Guided Local
Search (GLS), Genetic Programming (GP), Greedy Randomised Adaptive
Search Procedure (GRASP), Iterated Local Search (ILS), Particle
Swarm Optimisation (PSO), Simulated Annealing (SA), Scatter Search
(SS), Tabu Search (TS), and Variable Neighbourhood Search (VNS).

In this course we will focus on the study of a family of meta-heuristics that
includes some of the aforementioned approaches.
This family is called Evolutionary Algorithms (EAs) and it comprises a set of
population-based meta-heuristics inspired on biological evolution.
The family of EAs mainly includes
GAs, ES, EP, and GP, although EDAs, DE, CEAs, and CAs are also categorised as
EAs. Finally, Memetic Algorithms (MAs) are hybrid meta-heuristics that combine
a population-based approach with a Local Search (LS) procedure.

A large number of taxonomies for classifying meta-heuristics have been devised.
One of the most frequently used, establishes five different criteria to classify meta-heuristics.
The first one classifies them using *nature-inspired* methods and
*non-nature-inspired* approaches.
Most meta-heuristics are inspired by natural
processes, such as EAs, which are inspired by biological evolution, or ACO, ABC
and PSO, which are inspired by swarm intelligence.

Meta-heuristics can also be grouped into *deterministic* and *stochastic* methods.
Deterministic meta-heuristics, like TS, make their decisions considering deterministic
rules, i.e. given the same input instance for an optimisation problem, the same output is achieved.
In contrast, stochastic meta-heuristics, like SA or EAs, use randomness when making some decisions,
meaning that if the same input instance of an optimisation problem,
is given, the same output is not always obtained.
It is important to note that this feature significantly determines the way in which
the performance of meta-heuristics is measured.

Another criterion classifies meta-heuristics depending on whether they do not use information
dynamically extracted from the search process, such as GRASP, or they do,
like TS for example, which is based on using short-term and long-term memories in order to
avoid visiting already explored areas of the search space.

The most frequently used classification groups meta-heuristics into
*trajectory-based* approaches and *population-based* methods.
%
Trajectory-based schemes, like SA, have to deal with a unique solution during the
whole optimisation process, while population-based meta-heuristics, such as PSO
or EAs, have to maintain a set of solutions.
In trajectory-based algorithms the term trajectory refers to the "path" established
by the single solution in the search space during the optimisation procedure.
Consequently, trajectory-based meta-heuristics are also called *single-solution*
meta-heuristics.
We should mention that, generally, trajectory-based meta-heuristics are more oriented toward
intensification, while population-based meta-heuristics are more explorative methods.

Finally, meta-heuristics can be grouped depending on whether they are *iterative*
or *greedy* (also called *constructive*) techniques.
Iterative meta-heuristics, such as EAs and ILS, start with a unique solution
or a set of solutions and iteratively modify them by using certain operators until the
optimisation procedure ends.
Greedy meta-heuristics, like GRASP, on the other hand, build solutions from scratch,
assigning a value to each decision variable at each step of the optimisation procedure until
complete solutions are obtained.

### Premature convergence

Meta-heuristics have shown great promise to obtain solutions to difficult and complex
applications in a wide range of fields. However, they exhibit a tendency to
converge towards local optima for some problems, with the likelihood of this occurrence
depending on the shape of the fitness landscape. Several methods have
been designed with the aim of dealing with local optima stagnation. Some
of the simplest techniques rely on restarting the approach when stagnation is detected.
In other cases, a component that inserts randomness or noise into
the search is used. Maintaining some memory, as TS does, in order to avoid
exploring the same areas several times is also a typical approach. Finally,
population-based strategies intrinsically try to maintain the diversity of a solution
set. By recombining these solutions, a wider area of the decision space might be
explored.

In the particular case of population-based meta-heuristics, like EAs, *premature convergence*
is one of the most frequent drawbacks to be addressed. It appears when
every member of the population is in a sub-optimal region of the search space, and
therefore the optimisation scheme is not able to generate new individuals that outperform
their corresponding ancestors, i.e. there exists a loss of diversity caused by the use
of a finite population size. This phenomenon is also known as *genetic drift*, and it
is the main reason for the appearance of premature convergence.
Several methods have been devised for dealing with premature convergence. Most of
them preserve the diversity in a set of solutions. Some of the most frequently
used are the following:

* Increase the population size to avoid *genetic drift*.
* Apply mating restrictions such as *incest prevention*, i.e.,
keep very similar individuals from mating. This is also known as *speciation*.
* Perform *cataclysmic mutation*, i.e. highly disruptive mutations, when
diversity has been lost.
* Perform selection applying *fitness sharing*. In this case, highly similar
individuals are clustered and penalised by sharing the obtained fitness values among the members
of the group that lie in the same niche (i.e., those that are very close to each other either
in the decision space or the objective space).
* Apply *crowding-based selection* where each offspring replaces similar individuals in the
parent population.
* Use complex population structures, such as the *island-based model* or the
*cellular approaches*.

Diversity can help the optimisation procedure in two ways. Firstly, there exists a
relationship between diversity and the diversification and intensification capabilities
of EAs. Among other advantages, as previously stated, a proper balance between
diversification and intensification might allow the search space to be explored more
efficiently. Secondly, maintaining proper diversity might allow combining different
building blocks in crossover operations.

### Parameter setting

In addition to avoiding the problem of premature convergence, another arduous task
involves setting the parameters of a meta-heuristic. The problems of parameter setting
and premature convergence are closely related. If the parameter values of a
population-based meta-heuristic are chosen poorly, the balance between diversification
and intensification might become disproportionate, producing a loss of diversity
and, as a result, premature convergence. To configure a meta-heuristic, several
components and/or parameters must be specified. For instance, EAs have different
components, such as the mutation and crossover operators, which must be
defined. In addition, some parameters like the mutation and crossover rates—the
probabilities used to apply the aforementioned operators—must be also fixed. In
general, the performance of any meta-heuristic, and consequently the quality of the
solutions obtained, are highly dependent on these components and parameters. As
a result, it is vital that the parameters be properly set. In order to completely
configure a meta-heuristic, two types of information are required:

* *Symbolic*, also referred to as *qualitative*, *categoric* or *structure* parameters,
like the crossover and mutation operators of an EA.
* *Numeric*, also referred to as *quantitative* or *behavioural* parameters, such as
the crossover and mutation rates of an EA.

For both kinds of parameters, the different elements of the domain are known as
parameter values, and a parameter is instantiated by assigning it a value. The
main difference between the two types of parameters lies in the size and structure
of their respective domains. Symbolic parameters, like the crossover operator of an
EA, have a finite domain in which order is not established and a distance metric
is not defined. In contrast, numeric parameters, such as the mutation rate of an
EA, have an infinite domain in which a distance metric and an order can be defined
for the values. Thus, optimisation and search methods can readily be used to look
for the appropriate values of numeric parameters. However, in the case of symbolic
parameters, as noted above, distance metrics cannot be applied between two values,
and therefore optimisation schemes are not able to profit from the definition of these
types of metrics for setting said parameters.

Parameter setting strategies are commonly divided into two categories: *parameter
tuning* and *parameter control*. In parameter tuning, also called offline or endogenous
setting, the objective is to identify the best set of parameters for a given
meta-heuristic. Once a suitable parameter set is identified, an algorithm is executed
using the selected parameter values, which remain fixed for the full run. Traditionally,
parameter tuning has involved performing different executions of the same
meta-heuristic using different parameterisations. Afterwards, the parameterisation
that provides the best performance, i.e. the best solutions for the optimisation problem
in question, is selected. The main disadvantages of parameter tuning based on
this systematic approach are the following:

* Since the parameters interact, systematically testing all of their possible combinations
is practically impossible.
* The amount of computational resources and time invested in the process of
parameter tuning is huge, even if the parameters are independently optimised
regardless of their interactions.
* For a given problem, the selected parameter values are not necessarily optimal
for every stage of the optimisation procedure, even if the previous effort made
to tune them was significant.

In past decades, research into parameter tuning mainly focused on looking for a general
set of optimal values for the parameters of a specific algorithm, which allowed
promising results to be obtained across several optimisation problems.
However, it is now generally accepted by the research community that a single set
of parameters is unlikely to be optimal across a range of problems and that an
algorithm has to be specifically configured in order to successfully solve a given optimisation
problem. In fact, the *No Free Lunch* theorem provided evidence
from a theoretical point of view that a given optimisation method is not appropriate
for all optimisation problems. Hence, this has given rise to a significant field
of research in automated parameter tuning to enable an algorithm to be suitably
tuned for the optimisation problem at hand. Tuning methods have been applied to
a large number of meta-heuristics, including AISs, GAs, GLS, MAs or SA, for instance.
Moreover, a wide variety of parameter tuning approaches
used in different fields have been proposed, including the *sampling* and
*racing* methods. Regardless of the tuning method chosen, it is crucial to recognise
that parameters usually interact in highly non-linear ways, meaning they should
ideally be tuned simultaneously rather than independently. However, simultaneously
tuning several parameters requires a huge amount of experimentation
and is likely to be computationally infeasible. As a result, parameter tuning is often
performed considering the parameters independently, though this is likely to lead
to a sub-optimal set of parameters for the reasons given above. Moreover, several
studies have concluded that the use of a static set of parameters during a complete
run seems to be inappropriate. In fact, it has been
empirically and theoretically demonstrated that different values of parameters might
be optimal at different stages of the optimisation process. As a result, it
seems more appropriate to apply strategies that allow the parameter values to adapt
or change during the course of a run.

This is precisely the goal of parameter control, also known as online or exogenous
setting, which is based on designing a control strategy that dynamically
selects the most suitable parameter values to use at every stage of the search process.
A wide range of parameter control methods has been proposed in the literature.
They have been successfully applied to different meta-heuristics, such
as ES, DE, GAs, GRASP or PSOs. Most of them
are tailor-made methods, however, and depend on the specific meta-heuristic and its
parameters. Thus, it would be desirable to design generic parameter control schemes
that can be directly applied to different meta-heuristics and/or parameters.

### Performance measurement

After applying any optimisation scheme to a particular optimisation problem, its
performance must be measured in order to check whether the optimisation method is
suitable for the optimisation problem at hand. In the case of exact algorithms, since
they guarantee that the optimal solutions will be obtained, the most frequently used
metric to measure their performance is the time invested in obtaining said optimal
solutions. However, in the case of approximate algorithms, and particularly when
meta-heuristics are applied, other indicators have to be considered to measure their
performance. This is because meta-heuristics do not ensure that the optimal solutions
will be obtained. Moreover, a large number of meta-heuristics are stochastic
approaches. Performance metrics can be classified based on the following criteria:
*quality of the solutions*, *computational effort*, and *robustness*.

As concerns the quality of the solutions, performance metrics are generally based on
calculating the distance or the error between the solutions obtained and the optimal
ones. However, for a large number of optimisation problems the optimal solutions
are not known. For these cases, other solutions can be used as the reference set. The
most frequently used are lower/upper bound solutions, the best-known solutions or
solutions defined by the human decision maker considering any kind of requirement
for the problem at hand.

From the point of view of the computational effort, the metrics are closely related
to the stopping criterion selected for the meta-heuristic at hand. Among the most
widely applied metrics, it is important to mention the time invested in achieving a
certain stopping criterion, such as a prefixed quality level. However, this metric depends
on the hardware and software present in the machine where the optimisation
scheme is executed. As a result, another frequently used metric measures the number
of function evaluations needed to reach a certain stopping criterion. The main
drawback of this metric is that it is not suitable for optimisation problems whose
objective functions are not computationally expensive.

The robustness of a meta-heuristic is another possible criterion for grouping performance
metrics. The term robustness can be defined in several different ways. Firstly,
a meta-heuristic is robust if the variability of the results does not significantly increase
even if its parameters are modified. Another criterion defines a meta-heuristic
as robust if it performs reasonably well among a large set of problems and/or instances
with the same parameterisation. Lastly, if a stochastic meta-heuristic is
applied, a low deviation from the average in the results obtained by the stochastic
approach over several runs indicates that it is robust.

Finally, in order to determine whether the results obtained by different stochastic
methods present statistically significant differences, an statistical analysis is mandatory.
For instance, the following statistical procedure could be applied in an effort to
assign statistical confidence to the results. First a Shapiro-Wilk test is
performed to check whether the values of the results follow a normal (Gaussian)
distribution or not. If so, the Levene test checks for the homogeneity of
the variances. If samples have equal variances, an Analysis of Variance (ANOVA)
is done; otherwise, a Welch test is performed. For non-Gaussian distributions, the
non-parametric Kruskal-Wallis test is used. In every case, a significance level of 5%
is considered.
