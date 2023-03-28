# First example of an evolutionary algorithm

In this section, a basic evolutionary algorithm for solving the
[Knapsack Problem](https://en.wikipedia.org/wiki/Knapsack_problem#Definition)
(KP) is presented.

The KP is a common NP-hard problem and could be categorised as an resource
allocation problem. Herein, we will address the 0-1 variant of the KP, i.e.
objects cannot be divided into fragments. As a result, given an item, it
can be included into the knapsack (1) or not (0).

Having a set of items, each with a profit and a weight, the objective is to
maximise the total profit of the items included into the knapsack, while
satisfying the knapsack maximum capacity constraint.

The reader is referred to this
[web KP solver](https://cristianabrante.github.io/GeneticsJsKnapsack/)
implemented by Cristian Abrante by using the TypeScript library
[GeneticsJS](https://geneticsjs.github.io/GeneticsJS/index.html).

## Individual representation and population initialisation

For the individual representation, i.e. how to encode a solution for the KP, we could
use an array of 0 and 1 integer values, to decide if a particular item is included or
not into the knapsack. A better approach would be to use an array of boolean values,
however.

As a result, we could write a function in Python that initialises a population of
individuals, where each individual or solution is represented by an array of
boolean values.

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
the items are given by the array `weights`, while their profits are given by the array `values`.
As a result, we could have used `len(values)` instead of using `len(weights)` (both arrays
should contain the same number of values).

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

Since we are interested in maximising the total profit, while satisfying the maximum capacity
constraint, the larger the fitness value, the fitter the individual and the better from
the optimisation perspective. Bearing the above in mind, those individuals with a fitness
value equal to 0 will be considered as unfeasible, since they do not satisfy the maximum
capacity constraint.

## Parent selection strategy

For the parent selection strategy, we could consider a *roulette wheel* selection mechanism,
also known as *fitness proportional selection*.

```python
# define the parent selection function
def select_parents(population, fitnesses):
    total_fitness = sum(fitnesses)
    probabilities = [fitness / total_fitness for fitness in fitnesses]
    parents = []
    for i in range(2):
        selected = False
        while not selected:
            rand = random.uniform(0, 1)
            accum = 0
            for j in range(len(population)):
                accum += probabilities[j]
                if rand < accum:
                    parents.append(population[j])
                    selected = True
                    break
    return parents
```

Given a `population` of solutions and the `fitnesses` of those solutions, the function
`select_parents` returns an array with two solutions representing the selected parents.

First, an array `probabilities` is computed by dividing the fitness of every individual
in the population by the sum of fitnesses of all individuals (`total_fitness`). Hence,
the addition of all the probabilities should be close to 1.

Once probabilities are calculated, two parents have to be selected. For selecting each of both
parents, a random number is generated in the range $[0, 1)$ through `random.uniform(0, 1)`.
If the random number generated is lower than the cumulative probability of an individual,
then that individual is selected as a parent. As a result, the larger the fitness of an
individual, the higher their probability of being selected as a parent (it has a larger share
of the roulette wheel). The above is the reason why this strategy is called fitness
proportional selection or roulette wheel selection.

It is important to note at this point that, since unfeasible individuals are assigned a
fitness equal to 0, their selection probability will be equal to 0 as well.

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

## Evolutionary approach

In this particular case, since a binary representation is being used, the evolutionary approach
is a traditional GA.

```python
# define the genetic algorithm
def genetic_algorithm():
    population = initialize_population()
    for i in range(num_generations):
        fitnesses = [fitness(solution) for solution in population]
        children_population = []
        while (len(children_population) < population_size):
          parents = select_parents(population, fitnesses)
          children = crossover(parents)
          children_population.extend([mutate(child) for child in children])
        population = children_population
    fitnesses = [fitness(solution) for solution in population]
    best_fitness = max(fitnesses)
    best_solution = population[fitnesses.index(best_fitness)]
    best_weight = sum(weights[i] for i in range(len(weights)) if best_solution[i])
    return (best_solution, best_fitness, best_weight)
```

It can be noted that it follows the general framework of an EA and makes use of the
different functions introduced in previous lines. The number of iterations or
generations performed by the GA has been selected as the stopping criterion.
At the same time, the GA incorporates a *generational* survivor selection scheme with
no elitism, i.e. in every generation the whole children population survives for the next
generation (the whole parent population is discarded). The approach returns the best
solution found, as well as its fitness and total weight.

In order to run the GA, we could have the following script that uses the functions
implemented above:

```python
import random

# define the problem instance
weights = [10, 20, 30, 40, 50]
values = [100, 50, 150, 200, 300]
max_weight = 100

# define genetic algorithm parameters
population_size = 10
num_generations = 100
mutation_rate = 0.1

# run the genetic algorithm and print the result
best_solution, best_fitness, best_weight = genetic_algorithm()
print("Best solution:", best_solution)
print("Best fitness:", best_fitness)
print("Best weight:", best_weight)
```

First of all, we define the weights and profits of the set of items that could
be introduced into the knapsack. The capacity of the knapsack is defined as well.
Then, the parameters of the GA are set:

* Population size: 10 individuals
* Stopping criterion: 100 generations
* Mutation rate: 0.1

Finally, the GA is run by calling function `genetic_algorithm`. It is important to
note at this point that, since an EA, and particularly, this GA, is a stochastic
approach, different runs will produce different results.

## Exercises

1. If you have knowledge about Object-oriented Programming (OOP) implement the above
algorithm as a Python class.
2. With the current parent selection mechanism, could both parents be the same individual? If so,
how could we modify `select_parents` to avoid that behaviour? At the same time, `select_parents`
could crash if `total_fitness` becomes 0. How could you fix the above?
3. Could you write a function to implement a parent selection mechanism based on a
binary tournament?
4. With the current crossover operator, what does happen if both parents are the same individual?
5. Could you write a function to implement a *Uniform Crossover*?
6. In the current version of our GA, the crossover operator is always applied, i.e. the
crossover rate is equal to 1. Sometimes, this is not suitable, so it would be great to
have a crossover rate that decides if the crossover operator is applied or not. Before
applying it, a random number in the range $[0, 1]$ must be generated. If the said random
number is lower than the crossover rate, then the crossover is applied by producing two
new children. Otherwise, both parents become the new children in the offspring population.
7. What value should we use for the mutation rate if we only want to modify one gene at maximum?
8. How could you use the number of function evaluations as the stopping criterion in the GA?
9. How could you incorporate elitism in the survivor selection scheme?
10. Could you write a version of the GA where a *replace-worst* survivor strategy is considered?
11. The GA works with an even population size. What set of changes would you incorporate to
also allow an odd population size?
12. Could you test your GA with some [hard instances proposed by Pisinger](http://hjemmesider.diku.dk/~pisinger/codes.html)?
