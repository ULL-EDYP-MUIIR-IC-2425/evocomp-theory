# Measuring the performance of an evolutionary algorithm

In this section, a brief description of metrics to assess the performance of
an stochastic approach, and particularly, an evolutionary algorithm, is given.
Examples are illustrated by means of the GA implemented in the
previous section for dealing with the KP.

EAs take some of their decisions using randomness. Bearing
the above in mind, given the same input, the output is likely to be different. As
a result, every run needs to be repeated several times. Hence, performance
metrics are based on statistics.

## Running time

The running time of an EA depends on three main factors:

* The size of the instance addressed.
* The parameterisation of the EA, e.g. the stopping criterion
(if it is different to the execution time itself, i.e. the number of generations or
the number of fitness function evaluations), the population size or the crossover rate.
* The features of the machine where the algorithm is run.

Considering the same instance as an input, the time invested by the algorithm changes
depending on the values given to its parameters. For instance, if the stopping criterion
is set to a particular number of generations, the running time will change with the
population size.

```python
import random
import time
import numpy

# define the problem instance (Pissinger's knapPI_11_20_1000_1 - http://hjemmesider.diku.dk/~pisinger/codes.html)
n = 20
weights = [582, 194, 679, 485, 396, 873, 594, 264, 462, 330, 582, 388, 291, 132, 660, 528, 970, 330, 582, 462]
profits = [114, 38, 133, 95, 612, 171, 918, 408, 714, 510, 114, 76, 57, 204, 1020, 816, 190, 510, 114, 714]
max_weight = 970

# define genetic algorithm parameters
population_size = 10
num_generations = 1000
mutation_rate = 0.05

# run the genetic algorithm and print the result
number_rep = 30
running_times = []

for i in range(number_rep):
  start = time.time()
  best_solution, best_fitness, best_weight = genetic_algorithm(num_generations, population_size, mutation_rate, n, profits, weights, max_weight)
  end = time.time()
  running_times.append(end - start)

print("Mean execution time", numpy.mean(running_times), "seconds")
```

Going on with the KP, in the above example, the algorithm is run for 1000 generations
with a population size of 10 indivuals, while in the example shown below, the algorithm is run for 1000
generations with a population size equal to 100 individuals. Both cases deal with the same instance.
As it can be observed, in the second case, the mean running time is larger in comparison to the mean
running time of the first case.

```python
import random
import time
import numpy

# define the problem instance (Pissinger's knapPI_11_20_1000_1 - http://hjemmesider.diku.dk/~pisinger/codes.html)
n = 20
weights = [582, 194, 679, 485, 396, 873, 594, 264, 462, 330, 582, 388, 291, 132, 660, 528, 970, 330, 582, 462]
profits = [114, 38, 133, 95, 612, 171, 918, 408, 714, 510, 114, 76, 57, 204, 1020, 816, 190, 510, 114, 714]
max_weight = 970

# define genetic algorithm parameters
population_size = 100
num_generations = 1000
mutation_rate = 0.05

# run the genetic algorithm and print the result
number_rep = 30
running_times = []

for i in range(number_rep):
  start = time.time()
  best_solution, best_fitness, best_weight = genetic_algorithm(num_generations, population_size, mutation_rate, n, profits, weights, max_weight)
  end = time.time()
  running_times.append(end - start)

print("Mean execution time", numpy.mean(running_times), "seconds")
```

At the same time, for a predefined set of parameter values, the running time of the
approach will increase with the size of the particular instance being solved.

```python
import random
import time
import numpy

# define the problem instance (Pissinger's knapPI_11_20_1000_1 - http://hjemmesider.diku.dk/~pisinger/codes.html)
n = 20
weights = [582, 194, 679, 485, 396, 873, 594, 264, 462, 330, 582, 388, 291, 132, 660, 528, 970, 330, 582, 462]
profits = [114, 38, 133, 95, 612, 171, 918, 408, 714, 510, 114, 76, 57, 204, 1020, 816, 190, 510, 114, 714]
max_weight = 970

# define genetic algorithm parameters
population_size = 10
num_generations = 1000
mutation_rate = 0.05

# run the genetic algorithm and print the result
number_rep = 30
running_times = []

for i in range(number_rep):
  start = time.time()
  best_solution, best_fitness, best_weight = genetic_algorithm(num_generations, population_size, mutation_rate, n, profits, weights, max_weight)
  end = time.time()
  running_times.append(end - start)

print("Mean execution time", numpy.mean(running_times), "seconds")
```

In the above example, the algorithm is run to solve an instance with 20 items, while in the example
shown below, the algorithm tries to solve an instance with 1000 items. In both cases, the population
size and the stopping criterion have been fixed to 10 individuals and 1000 generations, respectively.
As it can be noted, the mean time invested by the algorithm when solving the instance with 1000 items
is larger in comparison to the time invested when solving the instance with 20 items.

```python
import random
import time
import numpy

# define the problem instance (Pissinger's knapPI_11_1000_1000_1 - http://hjemmesider.diku.dk/~pisinger/codes.html)
n = 1000
weights = [582,194,679,485,396,873,594,264,462,330,582,388,291,132,660,528,970,330,582,462,776,194,594,970,396,330,198,485,528,462,582,388,594,679,66,198,396,660,66,660,594,330,594,582,388,291,594,485,396,132,594,194,97,776,388,594,528,132,132,582,485,264,388,660,132,330,462,582,594,330,264,198,679,679,97,582,97,198,679,660,264,291,776,66,291,594,198,660,594,66,873,194,660,873,873,132,873,528,776,396,594,330,660,873,97,462,594,485,132,970,582,873,776,132,528,528,485,396,194,388,330,776,198,594,873,132,198,396,970,330,132,198,528,660,264,132,97,198,462,679,198,291,528,485,66,679,776,330,970,462,97,396,264,132,679,66,194,970,194,291,388,388,194,679,66,660,66,462,660,776,776,660,873,970,485,462,291,970,291,462,528,679,198,528,66,582,291,388,660,198,132,396,776,582,594,528,264,679,330,970,970,97,485,462,582,462,198,873,660,582,396,970,132,873,388,330,594,485,485,679,660,330,66,660,194,97,388,582,660,291,97,66,330,970,66,396,873,970,582,528,594,873,132,970,528,462,97,388,970,970,776,396,679,396,388,66,660,594,198,291,660,194,291,291,194,528,388,198,594,873,462,396,873,660,873,396,594,776,970,264,388,388,264,330,873,132,97,388,462,594,679,528,264,485,388,462,264,970,396,462,388,528,264,194,776,198,194,396,970,776,132,66,660,388,485,873,132,660,873,528,679,97,396,132,66,582,660,330,66,198,528,528,396,66,388,679,660,776,679,264,66,396,594,97,194,264,132,970,198,132,132,66,528,132,198,873,396,462,194,194,679,970,660,660,132,97,198,388,194,594,873,528,194,528,66,396,66,97,97,264,970,582,330,396,485,660,485,97,66,970,776,97,97,485,194,594,66,194,660,194,388,264,582,679,388,388,776,873,66,660,594,396,582,132,388,396,330,582,388,594,396,462,132,873,679,291,264,679,97,528,594,485,776,462,97,679,970,330,388,582,194,264,388,582,528,970,194,873,264,679,264,264,582,97,194,594,970,873,582,679,291,396,330,462,388,462,582,582,132,66,679,462,679,396,873,528,528,264,970,776,388,291,528,194,776,970,194,291,97,194,97,582,660,330,485,679,660,330,528,291,594,388,97,291,873,132,132,594,485,970,396,582,194,66,396,970,396,396,194,97,776,462,594,776,528,330,679,462,582,873,330,264,660,776,264,66,582,66,660,873,594,291,528,485,776,582,132,330,582,485,528,396,594,873,132,679,291,198,594,679,528,330,194,462,97,97,132,132,388,194,582,132,330,291,388,132,970,66,198,528,873,66,660,66,970,264,679,594,396,485,97,97,776,660,194,97,582,291,485,873,388,264,485,194,776,776,132,194,485,291,462,679,388,970,594,66,194,462,264,264,396,776,485,528,132,776,396,582,388,194,66,264,582,582,388,660,528,330,776,970,660,582,462,528,873,873,97,594,462,462,388,198,485,396,66,66,582,776,873,528,528,291,873,528,528,132,388,660,873,132,264,970,873,679,97,97,198,132,330,198,198,594,594,291,132,396,485,462,194,97,776,970,660,776,873,462,873,594,582,388,970,970,528,462,388,660,194,97,97,873,198,388,970,776,776,679,194,679,582,528,97,873,132,396,462,873,132,776,660,660,679,462,776,66,970,970,970,462,396,776,66,582,873,582,660,388,198,66,485,291,97,873,485,66,66,528,388,97,582,396,97,194,970,485,462,679,462,679,66,582,660,970,264,330,660,388,198,528,462,462,679,776,660,873,194,97,97,396,97,291,970,66,264,388,330,660,388,194,388,679,970,485,291,396,264,198,396,485,132,330,66,485,462,873,582,970,291,198,330,198,970,291,660,660,970,396,66,291,594,873,97,264,679,873,396,194,97,582,396,97,462,970,660,388,582,679,132,679,970,66,873,594,396,582,776,388,485,485,776,132,582,776,291,679,264,264,970,396,679,132,873,528,132,970,485,66,264,132,528,462,594,291,873,264,264,194,388,388,198,970,485,679,485,194,194,330,660,291,264,679,528,291,485,528,264,194,198,462,194,330,66,776,528,264,528,198,528,396,194,388,462,776,132,291,873,97,264,198,776,291,485,462,388,97,970,873,594,388,97,776,485,97,97,679,873,194,660,132,388,660,264,485,264,582,396,528,594,594,528,970,970,330,396,582,194,388,132,660,485,330,388,660,291,660,396,873,132,582,132,198,873,97,264,660,396,388,594,194,582,198,970,132,582,660,970,594,291,198,873,264]
profits = [114,38,133,95,612,171,918,408,714,510,114,76,57,204,1020,816,190,510,114,714,152,38,918,190,612,510,306,95,816,714,114,76,918,133,102,306,612,1020,102,1020,918,510,918,114,76,57,918,95,612,204,918,38,19,152,76,918,816,204,204,114,95,408,76,1020,204,510,714,114,918,510,408,306,133,133,19,114,19,306,133,1020,408,57,152,102,57,918,306,1020,918,102,171,38,1020,171,171,204,171,816,152,612,918,510,1020,171,19,714,918,95,204,190,114,171,152,204,816,816,95,612,38,76,510,152,306,918,171,204,306,612,190,510,204,306,816,1020,408,204,19,306,714,133,306,57,816,95,102,133,152,510,190,714,19,612,408,204,133,102,38,190,38,57,76,76,38,133,102,1020,102,714,1020,152,152,1020,171,190,95,714,57,190,57,714,816,133,306,816,102,114,57,76,1020,306,204,612,152,114,918,816,408,133,510,190,190,19,95,714,114,714,306,171,1020,114,612,190,204,171,76,510,918,95,95,133,1020,510,102,1020,38,19,76,114,1020,57,19,102,510,190,102,612,171,190,114,816,918,171,204,190,816,714,19,76,190,190,152,612,133,612,76,102,1020,918,306,57,1020,38,57,57,38,816,76,306,918,171,714,612,171,1020,171,612,918,152,190,408,76,76,408,510,171,204,19,76,714,918,133,816,408,95,76,714,408,190,612,714,76,816,408,38,152,306,38,612,190,152,204,102,1020,76,95,171,204,1020,171,816,133,19,612,204,102,114,1020,510,102,306,816,816,612,102,76,133,1020,152,133,408,102,612,918,19,38,408,204,190,306,204,204,102,816,204,306,171,612,714,38,38,133,190,1020,1020,204,19,306,76,38,918,171,816,38,816,102,612,102,19,19,408,190,114,510,612,95,1020,95,19,102,190,152,19,19,95,38,918,102,38,1020,38,76,408,114,133,76,76,152,171,102,1020,918,612,114,204,76,612,510,114,76,918,612,714,204,171,133,57,408,133,19,816,918,95,152,714,19,133,190,510,76,114,38,408,76,114,816,190,38,171,408,133,408,408,114,19,38,918,190,171,114,133,57,612,510,714,76,714,114,114,204,102,133,714,133,612,171,816,816,408,190,152,76,57,816,38,152,190,38,57,19,38,19,114,1020,510,95,133,1020,510,816,57,918,76,19,57,171,204,204,918,95,190,612,114,38,102,612,190,612,612,38,19,152,714,918,152,816,510,133,714,114,171,510,408,1020,152,408,102,114,102,1020,171,918,57,816,95,152,114,204,510,114,95,816,612,918,171,204,133,57,306,918,133,816,510,38,714,19,19,204,204,76,38,114,204,510,57,76,204,190,102,306,816,171,102,1020,102,190,408,133,918,612,95,19,19,152,1020,38,19,114,57,95,171,76,408,95,38,152,152,204,38,95,57,714,133,76,190,918,102,38,714,408,408,612,152,95,816,204,152,612,114,76,38,102,408,114,114,76,1020,816,510,152,190,1020,114,714,816,171,171,19,918,714,714,76,306,95,612,102,102,114,152,171,816,816,57,171,816,816,204,76,1020,171,204,408,190,171,133,19,19,306,204,510,306,306,918,918,57,204,612,95,714,38,19,152,190,1020,152,171,714,171,918,114,76,190,190,816,714,76,1020,38,19,19,171,306,76,190,152,152,133,38,133,114,816,19,171,204,612,714,171,204,152,1020,1020,133,714,152,102,190,190,190,714,612,152,102,114,171,114,1020,76,306,102,95,57,19,171,95,102,102,816,76,19,114,612,19,38,190,95,714,133,714,133,102,114,1020,190,408,510,1020,76,306,816,714,714,133,152,1020,171,38,19,19,612,19,57,190,102,408,76,510,1020,76,38,76,133,190,95,57,612,408,306,612,95,204,510,102,95,714,171,114,190,57,306,510,306,190,57,1020,1020,190,612,102,57,918,171,19,408,133,171,612,38,19,114,612,19,714,190,1020,76,114,133,204,133,190,102,171,918,612,114,152,76,95,95,152,204,114,152,57,133,408,408,190,612,133,204,171,816,204,190,95,102,408,204,816,714,918,57,171,408,408,38,76,76,306,190,95,133,95,38,38,510,1020,57,408,133,816,57,95,816,408,38,306,714,38,510,102,152,816,408,816,306,816,612,38,76,714,152,204,57,171,19,408,306,152,57,95,714,76,19,190,171,918,76,19,152,95,19,19,133,171,38,1020,204,76,1020,408,95,408,114,612,816,918,918,816,190,190,510,612,114,38,76,204,1020,95,510,76,1020,57,1020,612,171,204,114,204,306,171,19,408,1020,612,76,918,38,114,306,190,204,114,1020,190,918,57,306,171,408]
max_weight = 4556

# define genetic algorithm parameters
population_size = 10
num_generations = 1000
mutation_rate = 0.001

# run the genetic algorithm and print the result
number_rep = 30
running_times = []

for i in range(number_rep):
  start = time.time()
  best_solution, best_fitness, best_weight = genetic_algorithm(num_generations, population_size, mutation_rate, n, profits, weights, max_weight)
  end = time.time()
  running_times.append(end - start)

print("Mean execution time", numpy.mean(running_times), "seconds")
```

The ideal scenario is that an EA provides the optimal solution
to a particular instance of a problem in the lowest possible budget of time.
Nevertheless, EAs do not ensure to provide the optimal solution. Consequently,
the running time must be taken carefully when measuring their performance.
If the running time of the approach is small, but the solutions provided are not good,
the metric becomes unreliable.

For this reason, a common approach is to establish a predefined quality level that
the algorithm should achieve to consider the execution successful. Then, the time
invested by the approach in achieving that quality level is measured. Moreover,
several repetitions are considered, and some statistics are computed over the set
of measured running times: minimum, maximum, mean or median, among others. If the
optimal solution is known, the quality level can be easily fixed. Otherwise,
something common is to fix the quality level in terms of the best solution found
ever or the best solution found during the runs carried out.

```python
def quality_level_satisfied(fitnesses, quality_level):
  for i in range(len(fitnesses)):
    if fitnesses[i] >= quality_level:
      return True
  return False

# define the genetic algorithm
def genetic_algorithm(quality_level, population_size, mutation_rate, n, profits, weights, max_weight):
    population = initialize_population(population_size, n)
    fitnesses = [fitness(solution, n, profits, weights, max_weight) for solution in population]
    
    while not quality_level_satisfied(fitnesses, quality_level):
        children_population = []
        while (len(children_population) < population_size):
          parents = select_parents(population, fitnesses, population_size)
          children = crossover(parents, n)
          children_population.extend([mutate(child, n, mutation_rate) for child in children])
        population = children_population
        fitnesses = [fitness(solution, n, profits, weights, max_weight) for solution in population]
    
    best_fitness = max(fitnesses)
    best_solution = population[fitnesses.index(best_fitness)]
    best_weight = sum(weights[i] for i in range(n) if best_solution[i])
    return (best_solution, best_fitness, best_weight)
```

The function `quality_level_satisfied` returns a `True` value if any individual
in the population has a fitness higher or equal to the quality level established.
Otherwise, it returns a `False` value. Then, the stopping criterion in the
function `genetic_algorithm` has been modified. Now the number of generations
is not considered. The algorithm will not stop until the quality level is satisfied
by, at least, one individual in the population.

```python
import random
import time
import numpy

# define the problem instance (Pissinger's knapPI_11_20_1000_1 - http://hjemmesider.diku.dk/~pisinger/codes.html)
n = 20
weights = [582, 194, 679, 485, 396, 873, 594, 264, 462, 330, 582, 388, 291, 132, 660, 528, 970, 330, 582, 462]
profits = [114, 38, 133, 95, 612, 171, 918, 408, 714, 510, 114, 76, 57, 204, 1020, 816, 190, 510, 114, 714]
max_weight = 970

# define genetic algorithm parameters
population_size = 100
mutation_rate = 0.05
quality_level = 1428

# run the genetic algorithm and print the result
number_rep = 30
running_times = []

for i in range(number_rep):
  start = time.time()
  best_solution, best_fitness, best_weight = genetic_algorithm(quality_level, population_size, mutation_rate, n, profits, weights, max_weight)
  end = time.time()
  running_times.append(end - start)

print(running_times)
print("Mean execution time", numpy.mean(running_times), "seconds")
```

As it can be observed, the `quality_level` has been fixed to the value 1428 in the example
shown above. That value is the fitness, i.e. the addition of the profits of those items
included into the knapsack, of one of the optimal solutions for that particular instance. Now,
it can be noted that running times are different considering different repetitions.

What would happen if the algorithm is not able to find a solution with the minimum quality
level set? How could it be modified?

```python
# define the genetic algorithm
def genetic_algorithm(quality_level, maximum_time, population_size, mutation_rate, n, profits, weights, max_weight):
    start = time.time()
    population = initialize_population(population_size, n)
    fitnesses = [fitness(solution, n, profits, weights, max_weight) for solution in population]
    elapsed_time = time.time() - start
    
    while (not quality_level_satisfied(fitnesses, quality_level)) and (elapsed_time < maximum_time):
        children_population = []
        while (len(children_population) < population_size):
          parents = select_parents(population, fitnesses, population_size)
          children = crossover(parents, n)
          children_population.extend([mutate(child, n, mutation_rate) for child in children])
        population = children_population
        fitnesses = [fitness(solution, n, profits, weights, max_weight) for solution in population]
        elapsed_time = time.time() - start
    
    best_fitness = max(fitnesses)
    best_solution = population[fitnesses.index(best_fitness)]
    best_weight = sum(weights[i] for i in range(n) if best_solution[i])
    return (best_solution, best_fitness, best_weight)
```

This version of the genetic algorithm considers the `maximum_time` allowed to run
in the stopping criterion. For those cases where the algorithm cannot satisfy the
minimum quality level established, it will end its execution once the maximum running
time is achieved.

```python
import random
import time
import numpy

# define the problem instance (Pissinger's knapPI_11_20_1000_1 - http://hjemmesider.diku.dk/~pisinger/codes.html)
n = 20
weights = [582, 194, 679, 485, 396, 873, 594, 264, 462, 330, 582, 388, 291, 132, 660, 528, 970, 330, 582, 462]
profits = [114, 38, 133, 95, 612, 171, 918, 408, 714, 510, 114, 76, 57, 204, 1020, 816, 190, 510, 114, 714]
max_weight = 970

# define genetic algorithm parameters
population_size = 100
mutation_rate = 0.05
quality_level = 1430
maximum_time = 2

# run the genetic algorithm and print the result

number_rep = 30
running_times = []

for i in range(number_rep):
  start = time.time()
  best_solution, best_fitness, best_weight = genetic_algorithm(quality_level, maximum_time, population_size, mutation_rate, n, profits, weights, max_weight)
  end = time.time()
  running_times.append(end - start)

print(running_times)
print("Mean execution time", numpy.mean(running_times), "seconds")
```

As it can be observed, now the quality level has been fixed to 1430, a value that any algorithm
will find for this particular instance. It can be noted how all the running times are close to
two seconds, which in fact is the `maximum_time` allowed to run the algorithm.

Finally, is worth noting at this point that since the execution time of a particular
algorithm depends on the machine where it is run, comparing the running time of
different approaches executed in machines with different characteristics would be unfair.
A much fairer approach, for those cases, would be tu run the algorithms by considering
a maximum number of fitness function evaluations as the stopping criterion.

## Evolution of the fitness

To analyse the convergence of an evolutionary algorithm, the evolution of the fitness is
usually studied. For instance, suppose the version of the genetic approach where the
stopping criterion is based on the number of generations performed.

```python
# define the genetic algorithm
def genetic_algorithm(num_generations, gen_period, population_size, mutation_rate, n, profits, weights, max_weight):
  population = initialize_population(population_size, n)
  fitnesses = [fitness(solution, n, profits, weights, max_weight) for solution in population]
  mean_fitnesses = []
  generations = []

  for i in range(num_generations):
    children_population = []
    while (len(children_population) < population_size):
      parents = select_parents(population, fitnesses, population_size)
      children = crossover(parents, n)
      children_population.extend([mutate(child, n, mutation_rate) for child in children])
    population = children_population
    fitnesses = [fitness(solution, n, profits, weights, max_weight) for solution in population]

    if (i % gen_period == 0):
      generations.append(i)
      mean_fitnesses.append(numpy.mean(fitnesses))

  best_fitness = max(fitnesses)
  best_solution = population[fitnesses.index(best_fitness)]
  best_weight = sum(weights[i] for i in range(len(weights)) if best_solution[i])
  return (best_solution, best_fitness, best_weight, generations, mean_fitnesses)
```

The GA has been slightly modified to save information about the mean fitness
of the individuals in the population every `gen_period` generations. Now the
function `genetic_algorithm` also returns that historical data. A visual
representation of that information could be obtained by means of the next example:

```python
import random
import time
import numpy
import matplotlib.pyplot as plt

# define the problem instance (Pissinger's knapPI_11_20_1000_1 - http://hjemmesider.diku.dk/~pisinger/codes.html)
n = 20
weights = [582, 194, 679, 485, 396, 873, 594, 264, 462, 330, 582, 388, 291, 132, 660, 528, 970, 330, 582, 462]
values = [114, 38, 133, 95, 612, 171, 918, 408, 714, 510, 114, 76, 57, 204, 1020, 816, 190, 510, 114, 714]
max_weight = 970

# define genetic algorithm parameters
population_size = 100
mutation_rate = 0.05
num_generations = 1000
gen_period = 10

# run the genetic algorithm and print the result
best_solution, best_fitness, best_weight, generations, mean_fitnesses = genetic_algorithm(num_generations, gen_period, population_size, mutation_rate, n, profits, weights, max_weight)

fig, ax = plt.subplots()
ax.plot(generations, mean_fitnesses)

ax.set_xlabel('Number of generations')
ax.set_ylabel('Mean fitness')
ax.set_title('Evolution of the mean fitness')

plt.show()
```

Nevertheless, as previously mentioned, we should repeat every execution to provide the results:

```python
import random
import time
import numpy
import matplotlib.pyplot as plt

# define the problem instance (Pissinger's knapPI_11_20_1000_1 - http://hjemmesider.diku.dk/~pisinger/codes.html)
n = 20
weights = [582, 194, 679, 485, 396, 873, 594, 264, 462, 330, 582, 388, 291, 132, 660, 528, 970, 330, 582, 462]
profits = [114, 38, 133, 95, 612, 171, 918, 408, 714, 510, 114, 76, 57, 204, 1020, 816, 190, 510, 114, 714]
max_weight = 970

# define genetic algorithm parameters
population_size = 100
mutation_rate = 0.05
num_generations = 100
gen_period = 1
num_repetitions = 30

# run the genetic algorithm and print the result
runs = []
for i in range(num_repetitions):
  best_solution, best_fitness, best_weight, generations, mean_fitnesses = genetic_algorithm(num_generations, gen_period, population_size, mutation_rate, n, profits, weights, max_weight)
  runs.append(mean_fitnesses)

fig, ax = plt.subplots()
ax.plot(generations, numpy.mean(runs, axis = 0))

ax.set_xlabel('Number of generations')
ax.set_ylabel('Mean fitness')
ax.set_title('Evolution of the mean fitness in 30 repetitions')

plt.show()
```

Once the GA finishes each of its repetitions, the historical data about the
mean fitness, i.e. `mean_fitnesses`, is added as a new row into the matrix `runs`. Then we calculate
the mean of the matrix `runs` by columns, by using the argument `axis=0` in the call to
the function `numpy.mean`. Although the mean fitness in the different repetitions increases and
decreases, in general terms, it can be observed an increment in the mean fitness at the end of the
runs in comparison to the beginning.

In a similar way, the evolution of the maximum fitness could be also visualised by slightly
modifying the function `genetic_algorithm`:

```python
# define the genetic algorithm
def genetic_algorithm(num_generations, gen_period, population_size, mutation_rate, n, profits, weights, max_weight):
  population = initialize_population(population_size, n)
  fitnesses = [fitness(solution, n, profits, weights, max_weight) for solution in population]
  mean_fitnesses = []
  max_fitnesses = []
  generations = []

  for i in range(num_generations):
    children_population = []
    while (len(children_population) < population_size):
      parents = select_parents(population, fitnesses, population_size)
      children = crossover(parents, n)
      children_population.extend([mutate(child, n, mutation_rate) for child in children])
    population = children_population
    fitnesses = [fitness(solution, n, profits, weights, max_weight) for solution in population]

    if (i % gen_period == 0):
      generations.append(i)
      mean_fitnesses.append(numpy.mean(fitnesses))
      max_fitnesses.append(numpy.max(fitnesses))

  best_fitness = max(fitnesses)
  best_solution = population[fitnesses.index(best_fitness)]
  best_weight = sum(weights[i] for i in range(len(weights)) if best_solution[i])
  return (best_solution, best_fitness, best_weight, generations, mean_fitnesses, max_fitnesses)
```

The only difference with respect to the previous version is that, now, not only information about
the mean of the fitness is saved in the array `mean_fitnesses`, but also information
about the maximum fitness is stored in the array `max_fitnesses`. In the following lines, an example
showing how to visualize both the evolution of the mean fitness and the evolution of the maximum
fitness is given:

```python
import random
import time
import numpy
import matplotlib.pyplot as plt

# define the problem instance (Pissinger's knapPI_11_20_1000_1 - http://hjemmesider.diku.dk/~pisinger/codes.html)
n = 20
weights = [582, 194, 679, 485, 396, 873, 594, 264, 462, 330, 582, 388, 291, 132, 660, 528, 970, 330, 582, 462]
profits = [114, 38, 133, 95, 612, 171, 918, 408, 714, 510, 114, 76, 57, 204, 1020, 816, 190, 510, 114, 714]
max_weight = 970

# define genetic algorithm parameters
population_size = 100
mutation_rate = 0.05
num_generations = 100
gen_period = 1
num_repetitions = 30

# run the genetic algorithm and print the result
run_mean_fitnesses = []
run_max_fitnesses = []
for i in range(num_repetitions):
  best_solution, best_fitness, best_weight, generations, mean_fitnesses, max_fitnesses = genetic_algorithm(num_generations, gen_period, population_size, mutation_rate, n, profits, weights, max_weight)
  run_mean_fitnesses.append(mean_fitnesses)
  run_max_fitnesses.append(max_fitnesses)

fig, (ax1, ax2) = plt.subplots(2, 1)

ax1.plot(generations, numpy.mean(run_mean_fitnesses, axis = 0))
ax1.set_xlabel('Number of generations')
ax1.set_ylabel('Mean fitness')
ax1.set_title('Evolution of the mean fitness in 30 repetitions')

ax2.plot(generations, numpy.mean(run_max_fitnesses, axis = 0))
ax2.set_xlabel('Number of generations')
ax2.set_ylabel('Max fitness')
ax2.set_title('Evolution of the max fitness in 30 repetitions')

fig.tight_layout()

plt.show()
```

It is important to note that, in the case of the plot showing the evolution of the maximum fitness, at some
generations, the mean of the maximum fitness decreases. The above is due to the survivor selection scheme
used in the GA, which is a pure generational approach with no elitism. What would happen if elitism is somehow
incorporated into the generational GA?

```python
# define the genetic algorithm
def genetic_algorithm(num_generations, gen_period, population_size, mutation_rate, n, profits, weights, max_weight):
  parent_population = initialize_population(population_size, n)
  parent_fitnesses = [fitness(solution, n, profits, weights, max_weight) for solution in parent_population]
  mean_fitnesses = []
  max_fitnesses = []
  generations = []

  for i in range(num_generations):
    children_population = []
    while (len(children_population) < population_size):
      parents = select_parents(parent_population, parent_fitnesses, population_size)
      children = crossover(parents, n)
      children_population.extend([mutate(child, n, mutation_rate) for child in children])

    # Generational survivor selection scheme with elitism
    best_parent_fitness = max(parent_fitnesses)
    best_parent = parent_population[parent_fitnesses.index(best_parent_fitness)]

    children_fitnesses = [fitness(child, n, profits, weights, max_weight) for child in children_population]
    best_child_fitness = max(children_fitnesses)
    best_child = children_population[children_fitnesses.index(best_child_fitness)]

    if best_child_fitness >= best_parent_fitness:
      parent_population = children_population
      parent_fitnesses = children_fitnesses
    else:
      parent_population.clear()
      parent_fitnesses.clear()
      parent_population.append(best_parent)
      parent_fitnesses.append(best_parent_fitness)
      parent_population.extend(children_population[1:])
      parent_fitnesses.extend(children_fitnesses[1:])

    if (i % gen_period == 0):
      generations.append(i)
      mean_fitnesses.append(numpy.mean(parent_fitnesses))
      max_fitnesses.append(max(parent_fitnesses))

  best_fitness = max(parent_fitnesses)
  best_solution = parent_population[parent_fitnesses.index(best_fitness)]
  best_weight = sum(weights[i] for i in range(len(weights)) if best_solution[i])
  return (best_solution, best_fitness, best_weight, generations, mean_fitnesses, max_fitnesses)
```

In every generation of this version of the GA, after generating the new children population,
the best parent and the best offspring are looked for. In the case that the fitness of the
best parent is worse than the fitness of the best children, the whole parent population is
discarded and the children population becomes the parent population for the next generation, i.e.
a pure generational survivor selection scheme is applied. Otherwise, the best parent is preserved
for the next generation and the remaining individuals are taken from the children population.

If the previous experiment is run with the last version of the GA, the plot with the evolution of
the maximum fitness will not show any decrease.

```python
import random
import time
import numpy
import matplotlib.pyplot as plt

# define the problem instance (Pissinger's knapPI_11_20_1000_1 - http://hjemmesider.diku.dk/~pisinger/codes.html)
n = 20
weights = [582, 194, 679, 485, 396, 873, 594, 264, 462, 330, 582, 388, 291, 132, 660, 528, 970, 330, 582, 462]
profits = [114, 38, 133, 95, 612, 171, 918, 408, 714, 510, 114, 76, 57, 204, 1020, 816, 190, 510, 114, 714]
max_weight = 970

# define genetic algorithm parameters
population_size = 100
mutation_rate = 0.05
num_generations = 100
gen_period = 1
num_repetitions = 30

# run the genetic algorithm and print the result
run_mean_fitnesses = []
run_max_fitnesses = []
for i in range(num_repetitions):
  best_solution, best_fitness, best_weight, generations, mean_fitnesses, max_fitnesses = genetic_algorithm(num_generations, gen_period, population_size, mutation_rate, n, profits, weights, max_weight)
  run_mean_fitnesses.append(mean_fitnesses)
  run_max_fitnesses.append(max_fitnesses)

fig, (ax1, ax2) = plt.subplots(2, 1)

ax1.plot(generations, numpy.mean(run_mean_fitnesses, axis = 0))
ax1.set_xlabel('Number of generations')
ax1.set_ylabel('Mean fitness')
ax1.set_title('Evolution of the mean fitness in 30 repetitions')

ax2.plot(generations, numpy.mean(run_max_fitnesses, axis = 0))
ax2.set_xlabel('Number of generations')
ax2.set_ylabel('Max fitness')
ax2.set_title('Evolution of the max fitness in 30 repetitions')

fig.tight_layout()

plt.show()
```

## Evolution of the diversity

In addition to the evolution of the fitness, it is also important to analyse the evolution
of the diversity in the population. The ideal scenario would be that the diversity is as
highest as possible at the beginning of the search process, with the EA **exploring** the
search space. At the end of the run, however, the diversity should be low, with the population
of the EA converging, i.e. **exploting** a the most promising region of the search space found.

Since in previous sections, a GA based on a binary representation of the solutions has been applied,
to measure the diversity in the population, the Hamming distance could be used.

```python
def hamming_diversity(population, population_size):
    total_distance = 0

    for i in range(population_size):
        for j in range(i + 1, population_size):
            distance = sum(a != b for a, b in zip(population[i], population[j]))
            total_distance += distance

    diversity = total_distance / (population_size * (population_size - 1) / 2)

    return diversity
```

Given two individuals, the number of different genes determines their Hamming distance. The above
function calculates the mean Hamming distance among all pairs of individuals.

For visualising the evolution of the diversity of both versions of the GA, i.e. the pure generational
GA and the generational GA with elitism, the source code of both approaches needs to be slightly
modified. The source code of the generational GA would be as follows.

```python
# define the genetic algorithm
def genetic_algorithm(num_generations, gen_period, population_size, mutation_rate, n, profits, weights, max_weight):
  population = initialize_population(population_size, n)
  fitnesses = [fitness(solution, n, profits, weights, max_weight) for solution in population]
  generations = []
  diversity = []

  for i in range(num_generations):
    children_population = []
    while (len(children_population) < population_size):
      parents = select_parents(population, fitnesses, population_size)
      children = crossover(parents, n)
      children_population.extend([mutate(child, n, mutation_rate) for child in children])
    population = children_population
    fitnesses = [fitness(solution, n, profits, weights, max_weight) for solution in population]

    if (i % gen_period == 0):
      generations.append(i)
      diversity.append(hamming_diversity(population))

  best_fitness = max(fitnesses)
  best_solution = population[fitnesses.index(best_fitness)]
  best_weight = sum(weights[i] for i in range(len(weights)) if best_solution[i])
  return (best_solution, best_fitness, best_weight, generations, diversity)
```

It can be observed that, every `gen_period` generations, the diversity of the current
population is calculated through the function `hamming_diversity` and stored in the
array `diversity`.

The source code of the generational GA with elitism is similar to the above.

```python
# define the genetic algorithm
def genetic_algorithm_elitism(num_generations, gen_period, population_size, mutation_rate, n, profits, weights, max_weight):
  parent_population = initialize_population(population_size, n)
  parent_fitnesses = [fitness(solution, n, profits, weights, max_weight) for solution in parent_population]
  generations = []
  diversity = []

  for i in range(num_generations):
    children_population = []
    while (len(children_population) < population_size):
      parents = select_parents(parent_population, parent_fitnesses, population_size)
      children = crossover(parents, n)
      children_population.extend([mutate(child, n, mutation_rate) for child in children])

    # Generational survivor selection scheme with elitism
    best_parent_fitness = max(parent_fitnesses)
    best_parent = parent_population[parent_fitnesses.index(best_parent_fitness)]

    children_fitnesses = [fitness(child, n, profits, weights, max_weight) for child in children_population]
    best_child_fitness = max(children_fitnesses)
    best_child = children_population[children_fitnesses.index(best_child_fitness)]

    if best_child_fitness >= best_parent_fitness:
      parent_population = children_population
      parent_fitnesses = children_fitnesses
    else:
      parent_population.clear()
      parent_fitnesses.clear()
      parent_population.append(best_parent)
      parent_fitnesses.append(best_parent_fitness)
      parent_population.extend(children_population[1:])
      parent_fitnesses.extend(children_fitnesses[1:])

    if (i % gen_period == 0):
      generations.append(i)
      diversity.append(hamming_diversity(parent_population, population_size))

  best_fitness = max(parent_fitnesses)
  best_solution = parent_population[parent_fitnesses.index(best_fitness)]
  best_weight = sum(weights[i] for i in range(len(weights)) if best_solution[i])
  return (best_solution, best_fitness, best_weight, generations, diversity)
```

Finally, the following example shows the evolution of the diversity by considering
30 repetitions of each GA version.

```python
import random
import time
import numpy
import matplotlib.pyplot as plt

# define the problem instance (Pissinger's knapPI_11_20_1000_1 - http://hjemmesider.diku.dk/~pisinger/codes.html)
n = 20
weights = [582, 194, 679, 485, 396, 873, 594, 264, 462, 330, 582, 388, 291, 132, 660, 528, 970, 330, 582, 462]
profits = [114, 38, 133, 95, 612, 171, 918, 408, 714, 510, 114, 76, 57, 204, 1020, 816, 190, 510, 114, 714]
max_weight = 970

# define genetic algorithm parameters
population_size = 100
mutation_rate = 0.05
num_generations = 100
gen_period = 1
num_repetitions = 30

# run the genetic algorithm and print the result
diversity_matrix = []
diversity_matrix_eli = []
for i in range(num_repetitions):
  best_solution, best_fitness, best_weight, generations, diversity = genetic_algorithm(num_generations, gen_period, population_size, mutation_rate, n, profits, weights, max_weight)
  best_solution_eli, best_fitness_eli, best_weight_eli, generations_eli, diversity_eli = genetic_algorithm_elitism(num_generations, gen_period, population_size, mutation_rate, n, profits, weights, max_weight)
  diversity_matrix.append(diversity)
  diversity_matrix_eli.append(diversity_eli)

fig, (ax1, ax2) = plt.subplots(2, 1)

ax1.plot(generations, numpy.mean(diversity_matrix, axis = 0))
ax1.set_xlabel('Number of generations')
ax1.set_ylabel('Mean diversity')
ax1.set_title('Evolution of the mean diversity in 30 repetitions - Generational GA')

ax2.plot(generations, numpy.mean(diversity_matrix_eli, axis = 0))
ax2.set_xlabel('Number of generations')
ax2.set_ylabel('Mean diversity')
ax2.set_title('Evolution of the mean diversity in 30 repetitions - Generational GA with elitism')

fig.tight_layout()

plt.show()
```

Visualising both plots, it can be noted that, as long the runs advance, the mean diversity decreases,
i.e., individuals in the population are less diverse or, in other words, more similar among them.

## Comparing different algorithms

In this section, a comparison among the previous GA and a random search procedure will be described.
The following code shows the source code of a possible random search implementation for the KP.

```python
def random_search(maximum_time, n, profits, weights, max_weight):
    start = time.time()
    best_fitness = 0
    best_weight = 0
    best_solution = []
    elapsed_time = time.time() - start

    while (elapsed_time < maximum_time):
        solution = [random.choice([True, False]) for i in range(n)]
        weight = sum(solution[i] * weights[i] for i in range(n))

        if weight <= max_weight:
            fitness = sum(solution[i] * profits[i] for i in range(n))

            if fitness > best_fitness:
                best_fitness = fitness
                best_solution = solution
                best_weight = weight
        elapsed_time = time.time() - start

    return (best_solution, best_fitness, best_weight)
```

Since both approaches will be run in a machine with the same characteristics, the maximum running
time has been selected as the stopping criterion. It can be observed that, while the current running
time is lower than the maximum execution time, a new solution is randomly generated. If the solution
satisfies the knapsack capacity constraint, the fitness of the said solution is computed. Finally,
the current solution is compared to the best solution found ever. It the former is better than the
latter, the former becomes the current best solution found.

The GA that makes use of the same stopping criterion will be as follows.

```python
# define the genetic algorithm
def genetic_algorithm(maximum_time, population_size, mutation_rate, n, profits, weights, max_weight):
  start = time.time()
  population = initialize_population(population_size, n)
  fitnesses = [fitness(solution, n, profits, weights, max_weight) for solution in population]
  elapsed_time = time.time() - start

  while (elapsed_time < maximum_time):
    children_population = []
    while (len(children_population) < population_size):
      parents = select_parents(population, fitnesses, population_size)
      children = crossover(parents, n)
      children_population.extend([mutate(child, n, mutation_rate) for child in children])
    population = children_population
    fitnesses = [fitness(solution, n, profits, weights, max_weight) for solution in population]
    elapsed_time = time.time() - start

  best_fitness = max(fitnesses)
  best_solution = population[fitnesses.index(best_fitness)]
  best_weight = sum(weights[i] for i in range(len(weights)) if best_solution[i])
  return (best_solution, best_fitness, best_weight)
```

Now, we have two different stochastic approaches whose performance could be compared.
To do so, as it has previously mentioned, several repetitions of the runs must be performed.

```python
import random
import time
import numpy as np

# define the problem instance (Pissinger's knapPI_11_20_1000_1 - http://hjemmesider.diku.dk/~pisinger/codes.html)
n = 20
weights = [582, 194, 679, 485, 396, 873, 594, 264, 462, 330, 582, 388, 291, 132, 660, 528, 970, 330, 582, 462]
profits = [114, 38, 133, 95, 612, 171, 918, 408, 714, 510, 114, 76, 57, 204, 1020, 816, 190, 510, 114, 714]
max_weight = 970

# define genetic algorithm parameters
population_size = 100
mutation_rate = 0.05

maximum_time = 0.2
number_reps = 30
rs_fitnesses = []
ga_fitnesses = []

for i in range(number_reps):
  rs_best_solution, rs_best_fitness, rs_best_weight = random_search(maximum_time, n, profits, weights, max_weight)
  rs_fitnesses.append(rs_best_fitness)
  ga_best_solution, ga_best_fitness, ga_best_weight = genetic_algorithm(maximum_time, population_size, mutation_rate, n, profits, weights, max_weight)
  ga_fitnesses.append(ga_best_fitness)
```

It can be noted that each run will take 0.2 seconds. Hence, both algorithms can be compared in a fair manner. Furthermore, the runs are repeated 30 times and the best fitness values returned by both algorithms are stored in arrays `rs_fitnesses` and `ga_fitnesses`.

Once we have gathered all the above information, we could, for instance, obtain a summary of some statistics or, even, show some boxplots with the fitness achieved through the runs.

```python
import pandas as pd
import matplotlib.pyplot as plt

data = pd.DataFrame({'rs': rs_fitnesses, 'ga': ga_fitnesses});
summary = data.describe()
print(summary)

fig, ax = plt.subplots()
data.boxplot(ax=ax)
ax.set_ylabel('Fitness')
plt.show()
```

For this particular example, it can be observed how the statistics of the results achieved by the GA are, generally speaking, better than the statistics of the results attained by the RS. The above is something that we expected since, the GA performs a better exploration of the decision space, since it makes use of information about the fitness for guiding the search procedure, something that the random search does not carry out.

Nevertheless, the above claim needs to be supported statistically, and as a result, a statistical comparison procedure must be applied to the results attained by both algorithms. As it was specified in the first section of these notes, the following statistical procedure could be applied in an effort to assign statistical confidence to the results. First a Shapiro-Wilk test is performed to check whether the values of the results follow a normal (Gaussian) distribution or not. If so, the Levene test checks for the homogeneity of the variances. If samples have equal variances, an Analysis of Variance (ANOVA) is done; otherwise, a Welch test is performed. For non-Gaussian distributions, the non-parametric Kruskal-Wallis test is used. In every case, a significance level of 5% is considered, by default.

```python
import scipy.stats as stats

def compare_samples(sample_1, sample_2, alpha=0.05):
  final_p_value = 0
  test_name = ""

  # Shapiro-Wilk is performed to check whether both samples follow a normal
  # distribution
  p_value_sample_1 = stats.shapiro(sample_1).pvalue
  p_value_sample_2 = stats.shapiro(sample_2).pvalue

  # If both are normal
  if p_value_sample_1 >= alpha and p_value_sample_2 >= alpha:
    # Levene checks if both samples have the same variance
    _, p_value_levene = stats.levene(sample_1, sample_2)
    # Equal variances
    if p_value_levene >= alpha:
        _, p_value_anova = stats.f_oneway(sample_1, sample_2)
        final_p_value = p_value_anova
        test_name = "ANOVA"
    # Not equal variances
    else:
        _, p_value_welch = stats.ttest_ind(sample_1, sample_2, equal_var=False)
        final_p_value = p_value_welch
        test_name = "WELCH"
  # No normality in both samples
  else:
    _, final_p_value = stats.kruskal(sample_1, sample_2)
    test_name = "KRUSKAL"

  return final_p_value, test_name
```

The function `compare_samples` gets two arrays as arguments with both samples to be compared.
The third argument, which is optional, allows the significance level of all statistical tests
performed to be fixed. The function returns the final p-value after having followed the above
statistical comparison procedure, in addition to the `test_name` that provided the said p-value.
If the p-value is lower than the significance level fixed, then the corresponding null hypothesis
is rejected:

* **ANOVA**: The null hypothesis is that both samples have an equal mean.
* **Welch**: The null hypothesis is that both samples have an equal mean.
* **Kruskal-Wallis**: The null hypothesis is that both samples have an equal median.

Bearing the above in mind, if `compare_samples` returns a p-value lower than the significance
level, the null hypothesis is rejected, which means that both samples present statistically
significant differences.

In the case of comparing two samples including the best fitness values achieved by two different
algorithms, the above means that the differences in performance between both approaches
are statistically significant.

Considering a maximisation problem, the algorithm obtaining the largest mean or median of the
results (depending on the statistical test providing the p-value) would be performing better
than the other.

```python
import random
import time
import pandas as pd
import matplotlib.pyplot as plt
import scipy.stats as stats

# define the problem instance (Pissinger's knapPI_11_20_1000_1 - http://hjemmesider.diku.dk/~pisinger/codes.html)
n = 20
weights = [582, 194, 679, 485, 396, 873, 594, 264, 462, 330, 582, 388, 291, 132, 660, 528, 970, 330, 582, 462]
profits = [114, 38, 133, 95, 612, 171, 918, 408, 714, 510, 114, 76, 57, 204, 1020, 816, 190, 510, 114, 714]
max_weight = 970

# define genetic algorithm parameters
population_size = 100
mutation_rate = 0.05

maximum_time = 0.2
number_reps = 30
rs_fitnesses = []
ga_fitnesses = []

for i in range(number_reps):
  rs_best_solution, rs_best_fitness, rs_best_weight = random_search(maximum_time, n, profits, weights, max_weight)
  rs_fitnesses.append(rs_best_fitness)
  ga_best_solution, ga_best_fitness, ga_best_weight = genetic_algorithm(maximum_time, population_size, mutation_rate, n, profits, weights, max_weight)
  ga_fitnesses.append(ga_best_fitness)

data = pd.DataFrame({'RS': rs_fitnesses, 'GA': ga_fitnesses});
summary = data.describe()
print(summary)

fig, ax = plt.subplots()
data.boxplot(ax=ax)
ax.set_ylabel('Fitness')
plt.show()

compare_samples(data["RS"], data["GA"])
```

If the above example is run, it is likely that the output shows a p-value, obtained by the Kruskal-Wallis test, which is
smaller than the significance level. This is an expected outcome. The GA obtains in almost all its executions the optimum
value for that particular instance, which means that the fitness values are not going to follow a normal distribution.
As a result, a Kruskal-Wallis test is performed, which compares the fitness values obtained by the GA against the fitness
values achieved by the random search. The resulting p-value is lower than the significance level because the median of the
results attained by the GA is statistically different to the median of the results provided by the random search. In fact,
the median of the former is larger in comparison to the median of the latter, thus concluding that the GA statistically
outperforms the random search in this particular example.
