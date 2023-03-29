# Measuring the performance of an evolutionary algorithm

In this section, a brief description of metrics to assess the performance of
an stochastic approach, and particularly, an evolutionary algorithm, is given.

Evolutionary algorithms take some of their decisions using randomness. Bearing
the above in mind, given the same input, the output is likely to be different. As
a result, every run needs to be repeated several times. Hence, performance
metrics are usually based on statistics.

## Running time

The running time of an evolutionary algorithm depends on two main factors:

* The size of the instance addressed.
* The parameterisation of the evolutionary algorithm, e.g. the stopping criterion
(if it is different to the execution time itself, i.e. number of generations or
number of fitness function evaluations), the population size or the crossover rate.
* The features of the machine where the algorithm is run.

Considering the same instance as an input, the time invested by the algorithm changes
depending on the values given to its parameters. For instance, if the stopping criterion
is set to a particular number of generations, the running time will change with the
population size. In this particular example, the larger the population, the higher
the running time.

At the same time, for a predefined set of parameter values, the running time of the
approach will increase with the size of the particular instance being solved.

The running time of an evolutionary algorithm is an important performance metric.
The ideal scenario is that an evolutionary algorithm provides the optimal solution
to a particular instance of a problem in the lowest possible budget of time.

Nevertheless, evolutionary algorithms do not ensure to provide the optimal solution.
Therefore, the running time must be taken carefully when measuring their performance.
If the running time of the approach is small, but the solutions provided are not good,
the metric becomes unreliable.

For this reason, a common approach is to establish a predefined quality level that
the algorithm should achieve to consider the execution successful. Then, the time
invested by the approach in achieving that quality level is measured. Moreover,
several repetitions are considered, and some statistics are computed over the set
of measured running times: minimum, maximum, mean or median, among others.

If the optimal solution is known, that quality level can be easily fixed. Otherwise,
something common is to fix the quality level in terms of the best solution found ever
or even during the runs.

Finally, it is worth noting that since the execution time of a particular algorithm
depends on the machine that it is run, comparing the running time of different
approaches executed in machines with different characteristics is unfair.

## Evolution of the mean fitness



## Evolution of the diversity

## Comparison to other approaches
