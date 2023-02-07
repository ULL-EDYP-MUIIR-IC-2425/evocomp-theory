# Historial introduction to Evolutionary Computation

Early work on Evolutionary Computation (EC) was based on the application of evolutionary
systems such as optimisation methods, feedback-control approaches, or automatic tools to
generate computer programs. In this dissertation, evolutionary system refers to Darwinian
evolutionary systems, and consists of the following features [180]:

* There exists a population of individuals which compete for limited resources.
* Due to the birth and death of individuals, the population changes dynamically.
* The ability of an individual to reproduce and survive is called fitness.
* The fact that offspring are similar, but not identical, to their parents is known
as variational inheritance.

One of the first studies that influenced the emergence of EC was provided by Sewell
Wright in the 1930s [354]. Wright explained evolution as a process where the genetic
information of species is continuously changing by a trial and error mechanism. The
effect of this procedure is to optimise the adaptation of species to their environment.
During the same period, Walter Cannon also noted that natural evolution
was a learning process that proceeds by random trial and error [58]. Nevertheless,
it was not until the late 1950s that Hans Bremermann proposed the relationship between
evolution and mathematical optimisation [40, 41]. Hence, Bremermann can be
considered as one of the first practitioners of EC in the field of optimisation. Nowadays,
optimisation continues to be the largest area of application of EC. Other
early works were based on the usage of evolutionary systems as feedback-control
approaches, which altered their responses dynamically depending on the feedback
obtained from the system being controlled. From this point of view, an example was
the usage of an evolutionary system to evolve the control circuits of a robot [127].
Finally, evolutionary systems were also used in an attempt to generate computer
programs automatically. An example of this type of application was the design of
a “Learning Machine” that evolved sets of computer programs [126]. All this early
research work was the origin of several sub-areas of EC, like Evolutionary Programming (EP),
Evolution Strategies (ES), and Genetic Algorithms (GAs). A deeper insight into the origins
of EC can be found in [121].

In the 1960’s, the availability of "cheap" computers boosted the idea of implementing
evolutionary systems as computational algorithms to solve complex problems, thus
triggering a revolution in the field of EC. Among the most important contributions
were the ideas put forth by Rechenberg and Schwefel, Fogel, and Holland:

* Rechenberg and Schwefel formulated some ideas on how evolutionary processes
could be used to deal with real-valued optimisation problems [285]. ES were
born from these ideas.
* Fogel’s research work was based on applying the ideas of evolutionary processes
to the field of artificial intelligence [123]. His first works were based on
representing intelligent agents as finite state machines, which were evolved to
even more intelligent agents. His ideas allowed EP methods to emerge.
* Holland started to apply evolutionary processes so as to implement problem-independent
robust adaptive systems, whose decisions were carried out by taking
into consideration the feedback received from interacting with a particular
environment [160]. These ideas set the stage for the modern-day GAs.

Afterwards, the aim of most research activities during the 1970’s was twofold.
Firstly, to characterise the behaviour of the three aforementioned approaches, and
secondly, to better understand the way they could be used to solve problems. Decisions
on how best to implement these approaches were also investigated, such as
how to manage the population of individuals, or how to select the parents in order
to obtain the offspring, among other topics. As a result, three canonical EAs (EP,
ES, and GAs) resulted from all the research work performed during this decade.

In the case of EP, starting from a population of N parents, N offspring were generated
with each iteration of the algorithm. The fittest N individuals among the
parents and offspring were selected as the parent population for the next iteration
of the algorithm. The selection of the parents was deterministic, and each parent
evolved in order to produce a single offspring. Since the individuals were represented
by finite state machines, the offspring were obtained by the usage of a mutation operator
that was responsible for adding/deleting states/arcs.

With regard to ES, individuals were represented by a vector of D real variables,
because this approach originated with the aim of optimising real-valued functions.
One of the first proposals was named (1+λ)-ES. In each iteration of the algorithm,
λ offspring were created starting from a single parent, and the fittest individual
between the parent and the offspring was selected as the unique parent for the
next iteration. In order to obtain the offspring, a mutation operator based on a
Gaussian distribution with a mean equal to zero and a standard deviation equal
to σ (G(0, σ)) was applied. Subsequently, an adaptive variant of said mutation
operator was proposed. The value of σ was adapted through the use of the famous
“1/5 rule” proposed by Rechenberg [286].

In GAs, the individuals were represented by means of a binary string. Variation
operators (crossover and mutation) were applied to obtain N offspring starting
from N parents, and all offspring survived as the parent population for the next
iteration of the algorithm, i.e. no parents were selected to survive. This is known
as a generational survivor selection method. To generate the offspring, parents were
randomly selected, but proportionately to their fitness.

While the canonical EAs emerged from the 1970’s, the 1980’s were focused on applying
this set of algorithms to more complex problems, and on defining new algorithmic
proposals based on them. In the particular case of ES, different problems arose
when dealing with high-dimensional and multi-modal problems. Consequently, several
variants of the original ES algorithm were proposed, like the (μ+λ)-ES, which
generates λ offspring starting from μ parents, and selects the best μ from (μ + λ)
individuals as the parent population for the next iteration. Another proposal was
the (μ, λ)-ES, in which μ parents produce λ offspring, and the best μ individuals
to survive are selected from the λ offspring, i.e. no parents survive. In addition,
a different representation for the individuals was also introduced. It consisted of
D real variables of the problem and D real values for the standard deviation σ.
Each value σi, i = 1, . . . , D was used in order to perturbate the variable i through
a Gaussian distribution G(0, σi), and since these values were incorporated into the
representation of the individual, they changed during the optimisation procedure.
To modify these values, the “1/5 rule” was also used. In the case of GAs, something
similar happened, since they were widely applied to different optimisation problems.
The most common difficulties that emerged from the application of GAs involved
the convergence to global optima and stagnation in sub-optimal regions. As a result,
different solutions were proposed, such as the use of tournament selection as
a novel parent selection mechanism [142], or the use of elitism in the survivor selection
methods [88]. Another important topic of research was the modification of
the internal representation of individuals for GAs, by experimenting with other binary
representations, or by changing the original representation based on a binary
string for a real-valued representation. Moreover, some research topics remained
open, such as the application of GAs to other fields, like classifier systems or neural
networks, the definition of non-linear representations of variable size in order
to address other types of problems with GAs, or even the parallelisation of GAs.
Finally, a large amount of tailor-made EAs, which incorporated problem-dependent
information in the form of representations or operators specifically designed for the
problem at hand, were also proposed during this decade.

Until the 1990’s the research on ES, EP, and GAs had been carried out independently.
However, in the late 1980’s and early 1990’s a significant number of conferences
on this topic were held that allowed different research groups to exchange their
ideas and points of view. As a consequence, an agreement on the term Evolutionary
Computation was reached, and the first journal on the subject, also called Evolutionary
Computation, emerged. Due to this exchange of ideas, different modifications at the
implementation level were investigated for the canonical EAs. In the case
of ES, different crossover operators that improved the performance of this EA were
proposed [20]. With regard to GAs, the use of problem-dependent representations
and operators improved the behaviour of these types of algorithms [249]. Finally,
with the incorporation of internal representations and operators from the field of
ES, the application of EP was extended to other areas such as optimisation. As a
result, several novel EAs, like Genetic Programming (GP) [191], were born. Moreover,
many of the fundamental assumptions and underlying theories were revised in order to
strengthen and generalise the basis for the different paradigms based on EAs.
Finally, by the late 1990’s the field of EC had become a mature scientific discipline.
