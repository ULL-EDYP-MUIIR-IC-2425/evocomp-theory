# Basic concepts about Evolutionary Algorithms

This section provides a detailed discussion of the basic terms and concepts that
different variants of these types of approaches share. EAs are a family of
population-based metaheuristics inspired by natural evolution. They have been
successfully applied to a large number of complex applications in different
scientific and technological fields. In natural evolution, a given environment is
filled with a population of individuals that compete in order to survive and reproduce.
Hence, since the environment can only contain a limited number of individuals, survivor
selection mechanisms are required to keep the population from growing uncontrollably.
Natural selection promotes the most competitive individuals, i.e. those that adapt
better to the environment. This phenomenon is also known as the *survival of the fittest*.
Some of these survivors will be able to reproduce with the aim of obtaining even fitter
individuals.

| **Evolutionary process**       | **Resolution of an optimisation problem** |
| ------------------------------ | ------------------------------------------|
| Population                     | Set of solutions                          |
| Individual                     | Solution                                  |
| Fitness                        | Objective function                        |
| Environment                    | Optimisation problem                      |
| Genotype, Phenotype, Chromosome| Internal representation of a solution     |
| Gene                           | Decision variable                         |
| Allele                         | Value of a decision variable              |
| Locus                          | Position of a decision variable           |

<br/>

Continuing with metaphor between an evolutionary process and the resolution of
an optimisation problem (see Table above ) a *structure* or an *individual* is an encoded
solution to some problem. The codification of an individual or its internal representation
is known as the *genotype*, which is decoded to obtain the *phenotype*, or
decoded solution. If a *direct encoding* of the individuals is used, the genotype and
the phenotype are similar. A genotype is usually composed of one or more *chromosomes*,
and every chromosome in turn consists of several independent *genes*, which
take on certain values or *alleles*. A *locus* identifies the position of a gene within the
chromosome, and a set of chromosomes is called a *population*. Generally, an EA
requires both an objective function and a fitness function. The objective function
is located in the problem domain, and defines the optimality condition of the EA.
In contrast, the fitness function is situated in the algorithm domain, and measures
if a particular solution satisfies said optimality condition. Both functions, however,
are usually identical [70], at least in the single-objective case. Hence, an objective
function assigns a fitness value to every individual. This fitness value measures the
ability of the corresponding individual to survive and reproduce in the *environment*,
i.e. whether the solution is appropriate for the optimisation problem at hand. We
should note that herein direct encoding of the individuals is always used. In addition,
genotypes consist of a unique chromosome. Consequently, the terms genotype and chromosome
refer to the internal representation of an individual.

```text
1: Initialisation. Generate the initial parent population.
2: Evaluation. Evaluate all individuals in the initial parent population by applying the
   objective function in order to assign a fitness value to every individual.
3: while (stopping criterion is not satisfied) do
4:   Parent selection. Select the individuals from the parent population to build the
     mating pool.
5:   Variation. Apply the variation operators to the mating pool so as to create the
     offspring population.
6:   Evaluation. Evaluate the generated offspring via the objective function so as to
     assign a fitness value to every offspring.
7:   Survivor selection. Select individuals from among the parents and offspring to
     survive as the new parent population for the next generation.
8: end while
```

The majority of EAs share the same generic framework (see algorithm above).
During the initialisation stage (step 1) individuals are generated to fill the initial
parent population. This initial parent population is evaluated (step 2) through the
application of the objective function so as to assign a fitness value to every individual.
Then, at each iteration or *generation* of the EA, a set of steps is repeated. Firstly, the
parents that comprise the *mating pool* (step 4) are selected via the *parent selection*
or *mating selection* mechanism. Then, the *variation operators* are applied to the
mating pool to generate the offspring population (step 5). Particularly important
among the different variation operators are the *recombination* or *crossover* operator,
as well as the *mutation* operator. Once the offspring are obtained, they have
to be evaluated (step 6) by means of the objective function in order to assign them
a fitness value. Finally, a *replacement* or *survivor selection* operator is applied
(step 7) to determine the set of individuals from among the parents and the
offspring that are going to survive as the parent population for the next generation.
These four steps are repeated until a stopping criterion (step 3) is satisfied. A flow
chart representing a generation of an EA is shown below.

![Flow chart representing a generation (iteration) of an Evolutionary Algorithm](img/ea_flow.png)

From the above content, it can be observed that different components, such as the
survivor selection strategy or the variation operators, among others, have to be specified
in order to completely design an EA. Additionally, some of these components
incorporate the use of parameters, such as mutation and crossover rates, or the population
size, for instance, and consequently they must be also fixed in order to execute the
EA as designed. In particular, decisions regarding the following components must
be made during the design of an EA:

* **Individual’s representation, genotype, or chromosome**. The particular
representation will depend on the particular optimisation problem at hand, and
examples could be a binary string, a vector of discrete (integer) values and
vector of continuous (real) values, among others.
* **Population initialisation**. In the majority of cases the population is
filled with randomly generated individuals, although more sophisticated
approaches could also be applied.
* **Parent selection mechanism**. This method is responsible for selecting the individuals
from the parent population for the purpose of reproducing. One of the most
frequently used strategies is the  well-known *Binary Tournament* operator.
* **Variation operators**. The objective of the variation operators is to generate
offspring starting from the mating pool. The most widely applied variation approaches
are the crossover operator, such as the one-point crossover, and mutation operators,
like the bit-flip mutation.
* **Survivor selection strategy**. The survivor selection
mechanism is responsible for choosing, from among the current parents
and offspring, the individuals that will survive for the next generation. Examples
could be the *generational* and the *replace-worst* survivor selection strategies.
* **Stopping criterion**. One of the most frequently used stopping criteria are
the execution time or the number of evaluations involving the objective functions
of the problem being solved.

## Parent selection mechanisms

The main aim of the parent selection strategy is to select the individuals from
the parent population that are going to reproduce in order to generate the offspring.
Usually, these strategies are based on the fitness assigned to every individual. Hence,
the better the fitness of an individual, the greater its likelihood of being selected.
*Selection pressure* is the degree to which selection emphasises the fittest individuals,
and it is used by the parent selection and the survivor selection mechanisms in
order to guide the search procedure towards more promising regions. The higher
the selection pressure, the higher the probability that the fittest individuals survive.
Nevertheless, some individuals with a poor fitness should be considered for their
selection, because they might contribute with their genetic material to guide the
search process to unexplored areas where the global optimum could be found. The
fitness can be assigned in two different ways:

* *Direct fitness assignment*. The fitness values are directly associated with individuals.
* *Rank-based fitness assignment*. Each individual in the population is assigned
a rank, with this rank generally depending on its fitness value. For instance,
suppose a list in which individuals are sorted in descending order depending on
their fitness values. Hence, an individual is associated with its corresponding
rank in this list.

There exist different types of parent selection mechanisms. Some of them are based
on a direct fitness assignment, while other approaches are based on a rank-based
fitness assignment in order to carry out the selection. The most important ones
are Fitness Proportional selection, also called Roulette Wheel selection, Stochastic
Universal Sampling, Rank-based selection, and Tournament selection [109].

*Tournament selection* is, with no doubt, the parent selection strategy most widely used.
This operator selects one parent, and as a result, if `n` parents have to be selected,
the operator has to be applied `n` times. Tournament selection consists of two main steps.
Firstly, `k` individuals are randomly selected from the current parent population using a
uniform distribution. This random selection can be performed with replacement
or without replacement. If no replacement is considered, the `k` selected individuals
are discarded from subsequent tournaments, whereas with replacement, the `k` selected
individuals might be randomly selected again in future tournaments. In the
second step, a probability `p` is used to determine the winner of the tournament from
among the `k` possible candidates. The value of `p` represents the probability that the
fittest individual from among the `k` possible candidates will win the tournament. If
a deterministic tournament is carried out (`p = 1`), the fittest individual, i.e. the one
with the best fitness, is always selected as the winner of the tournament. However,
stochastic variants of this selection operator can be defined by letting `p < 1`.

Something very common is to consider a deterministic binary tournament (`p = 1; k = 2`)
as the parent selection strategy [109]. Whether replacement is used or not will
depend on the specific EA. The following figure shows its operation.

![Parent selection based on a deterministic binary tournament](img/tournament.png)

It can be observed how each circle represents an individual and the corresponding number
refers to its fitness value. In this example, the higher the fitness value, the fitter
the individual. One of the main benefits of tournament selection is that it does not
require any global knowledge about the population, since it is based on a direct
fitness assignment. As a result, it is conceptually simple and easy to implement.
Additionally, the selection pressure can be controlled by means of the tournament
size `k`. The larger the tournament size, the higher the number of randomly picked
individuals, and therefore the lower the probability that an individual with a poor
fitness will be selected. Thus, as the tournament size increases, the selection
pressure grows.

## Crossover operators

