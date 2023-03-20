# First example of an evolutionary algorithm

In this section, a basic evolutionary algorithm for solving the
[Knapsack Problem](https://en.wikipedia.org/wiki/Knapsack_problem#Definition)
(KP) is presented.

The KP is a common NP-hard problem and could be categorised as an resource
allocation problem. Herein, we will address the 0-1 version of the KP, i.e.
objects cannot be divided into fragments. As a result, given an item, it
can be included into the knapsack (1) or not (0).

Having a set of items, each with a profit and a weight, the objective is to
maximise the total profit of the items included into the knapsack, while
satisfying the knapsack maximum capacity constraint.

The reader is referred to this [web KP solver](https://cristianabrante.github.io/GeneticsJsKnapsack/)
implemented by Cristian Abrante by using the TypeScript library [GeneticsJS](https://geneticsjs.github.io/GeneticsJS/index.html).

## Individual representation and population initialisation

For the individual representation, i.e. how to encode a solution for the KP, we could
use an array of 0 and 1 values, to decide if a particular item is included or not
into the knapsack. A better approach would be to use an array of boolean values.

As a result, we could write a function in Python that initialises a population of
individuals, where each individual or solution is represented by the said array of
booleans.

```python
# define the initialisation function
def initialize_population():
    population = []
    for i in range(population_size):
        solution = [random.choice([True, False]) for i in range(len(weights))]
        population.append(solution)
    return population
```

As it can be observed, `population` is an array of individuals. Until
the population is not filled with `population_size` individuals, a new `solution` (individual)
is initialised by randomly selecting the items included into the knapsack. If an item is
included into the knapsack, a `True` value is used to represent the above. Otherwise, a `False`
value is assigned. The number of available items is given by `len(weights)`. The weights of
the items are given by the array `weights`.

## Fitness function

The fitness function determines how the search is going to be guided through the evolutionary
process.

```python
# define the fitness function
def fitness(solution):
    total_weight = sum(weights[i] for i in range(len(weights)) if solution[i])
    if total_weight > max_weight:
        return 0
    return sum(values[i] for i in range(len(values)) if solution[i])
```

Given a `solution`, first of all, the `total_weight` of the items included into the knapsack
is calculated. If the `total_weight` of the solution is larger than the maximum capacity of
the knapsack `max_weight`, then the function `fitness` will return
a 0 value. The above means that a fitness value equal to 0 will be assigned to the
corresponding individual. Otherwise, the fitness of the solution will be calculated
as the sum of the profits (`values`) of those items included into the knapsack.

Since we are interested in maximising the profit, while satisfying the maximum capacity
constraint, the larger the fitness value, the fitter the individual and the better from
the optimisation perspective. Bearing the above in mind, those individuals with a fitness
value equal to 0 will be considered as unfeasible.

## Parent selection strategy

For the parent selection strategy, we could consider a *Roulette Wheel* selection mechanism,
also known as *fitness proportional selection*.

```python
# define the parent selection function
def select_parents(population):
    fitnesses = [fitness(solution) for solution in population]
    total_fitness = sum(fitnesses)
    probabilities = [fitness / total_fitness for fitness in fitnesses]
    parents = []
    for i in range(2):
        selected = False
        while not selected:
            for j in range(len(population)):
                if random.random() < probabilities[j]:
                    parents.append(population[j])
                    selected = True
                    break
    return parents
```

Given a `population` of solutions, the function `select_parents` returns an array with
two solutions representing the selected parents.

First, an array `fitnesses` is initialised by calculating the fitness of every individual
in the population. Then, an array `probabilities` is computed by dividing the fitness of
every individual in the population by the sum of fitnesses of all individuals (`total_fitness`).

Once probabilities are calculated, two parents have to be selected. For selecting each of both
parents, random numbers are generated in the range $[0, 1)$ through `random.random()`. If the
random number generated is lower than the selection probability of an individual, then that
individual is selected as a parent. As a result, the larger the fitness of an individual,
the higher their probability of being selected as a parent. The above is the reason why this
strategy is called fitness proportional selection.

It is important to note at this point that, since unfeasible individuals are assigned a fitness
equal to 0, their selection probability will be the smallest possible. However, they could be
selected as parents at some point during the evolutionary process.

Finally, with this parent selection mechanism, could both parents be the same individual? If so,
how could we modify `select_parents` to avoid that behaviour?

## Crossover operator

We could use the well-known *One Point Crossover* as one of the variation operators.

```python
# define the crossover function
def crossover(parents):
    crossover_point = random.randint(1, len(weights) - 1)
    child1 = parents[0][:crossover_point] + parents[1][crossover_point:]
    child2 = parents[1][:crossover_point] + parents[0][crossover_point:]
    return [child1, child2]
```

As it can be observed, the function `crossover` gets an array with both parents as an argument,
and returns an array with two new children. First of all, it selects the `crossover_point` by
means of a call to the function `random.randint`, which randomly generates an integer value in
the range $[n, m]$. The crossover point splits each parent into two parts. Then, two children
(offspring) are produced by crossing both parents' parts.

With this crossover operator, what does happen if both parents are the same individual?

## Mutation operator

In the case of the mutation operator, since we are dealing with a binary representation of solutions,
the *Bit Flip Mutation* would be a suitable choice.

```python
# define the mutation function
def mutate(solution):
    for i in range(len(solution)):
        if random.random() < mutation_rate:
            solution[i] = not solution[i]
    return solution
```

The function `mutate` gets an individual and returns the individual modified. This operator
requires the definition of a `mutation_rate` in the range $[0, 1]$. For every gene in the individual,
a random number is generated, which if it is lower than the mutation rate, then the gene is fliped.

It can be noted that the larger the mutation rate, the larger the number of genes modified by the
mutation operator.

What value should we use for the mutation rate if we only want to modify one gene at maximum?
