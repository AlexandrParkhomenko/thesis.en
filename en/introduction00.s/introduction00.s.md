# COMSM0302: Evolutionary Computing James Marshall

Welcome to COMSM0302: Evolutionary Computing!

What is Evolutionary Computing?

Evolutionary Computing (EC) is a collection of 'nature-inspired' heuristic optimisation techniques for hard' problems, e.

Genetic Algorithms (GA) Genetic Programming (GP) Evolutionary Strategies (ES)

Compare with traditional exact optimisation approaches for sufficiently 'simple' problems

Linear Programming > ..•

...and other heuristic algorithms

Simulated Annealing > ..•

# Syllabus

Implementation

Genetic Algorithms Genetic Programming Other EC algorithms Applications in optimisation and modelling

Theory

Descriptive models   
Predicting behaviour   
Fundamental limits on search and optimisation

# Curriculum

20 hours of lectures, weeks 1-10

Office hour

Notes

Will be posted on the unit webpage before each lecture > Supplementary material, worked exercises, etc. will be presented during lectures... all is useful and examinable, take notes!

$50 \%$ coursework, $50 \%$ exam

Genetic Algorithm assignment $( 3 0 \%$ , deadline early December) Genetic Programming assignment $( 2 0 \%$ , deadline early December) Theory exam $( 5 0 \%$ , January)

Additional unassessed self-learning exercises (mixture of implementation and theory)

I am available to answer questions during my office hour For routine programming enquiries, use the help-desk (MVB 3.19) Answers provided after 1 week Use these to prepare for the coursework and exam

# Curriculum

Lectures

<table><tr><td rowspan=1 colspan=1>Week</td><td rowspan=1 colspan=1>Topic</td></tr><tr><td rowspan=1 colspan=1>1</td><td rowspan=1 colspan=1>Introduction / Simple Genetic Algorithm</td></tr><tr><td rowspan=1 colspan=1>1</td><td rowspan=1 colspan=1>GA: Representations &amp; Operators</td></tr><tr><td rowspan=1 colspan=1>2</td><td rowspan=1 colspan=1>GA: Populations &amp; Selection</td></tr><tr><td rowspan=1 colspan=1>2</td><td rowspan=1 colspan=1>GA: Advanced Operators &amp; Techniques</td></tr><tr><td rowspan=1 colspan=1>3</td><td rowspan=1 colspan=1>GA for Grouping Problems</td></tr><tr><td rowspan=1 colspan=1>3</td><td rowspan=1 colspan=1>Overview of Genetic Programming</td></tr><tr><td rowspan=1 colspan=1>4</td><td rowspan=1 colspan=1>GP:CaseStudies</td></tr><tr><td rowspan=1 colspan=1>4</td><td rowspan=1 colspan=1>GP:CaseStudies</td></tr><tr><td rowspan=1 colspan=1>5</td><td rowspan=1 colspan=1>GP:CaseStudies</td></tr><tr><td rowspan=1 colspan=1>5</td><td rowspan=1 colspan=1>No FreeLunch Theorems</td></tr></table>

Lectures

<table><tr><td rowspan=1 colspan=1>Week</td><td rowspan=1 colspan=1>Topic</td></tr><tr><td rowspan=1 colspan=1>6</td><td rowspan=1 colspan=1>Schema Theory</td></tr><tr><td rowspan=1 colspan=1>6</td><td rowspan=1 colspan=1>GAs as Markov Processes</td></tr><tr><td rowspan=1 colspan=1>7</td><td rowspan=1 colspan=1>Dynamical Systems GA Model</td></tr><tr><td rowspan=1 colspan=1>7</td><td rowspan=1 colspan=1>Statistical Mechanics Approximation of GA</td></tr><tr><td rowspan=1 colspan=1>8</td><td rowspan=1 colspan=1>Predicting GA Performance</td></tr><tr><td rowspan=1 colspan=1>8</td><td rowspan=1 colspan=1>Fitness Landscapes</td></tr><tr><td rowspan=1 colspan=1>9</td><td rowspan=1 colspan=1>Memetic Algorithms</td></tr><tr><td rowspan=1 colspan=1>9</td><td rowspan=1 colspan=1>Evolution Strategies</td></tr><tr><td rowspan=1 colspan=1>10</td><td rowspan=1 colspan=1>Estimation of Distribution Algorithms</td></tr><tr><td rowspan=1 colspan=1>10</td><td rowspan=1 colspan=1>Artificial Life &amp; Modelling</td></tr></table>

# Course Texts

Recommended texts

Reeves, C. R. and Rowe, J. E. Genetic Algorithms - Principles and Perspectives: A Guide to GA Theory. 2003.

> Falkenauer, E. Genetic Algorithms and Grouping Problems. 1998.

Background texts

Holland, J. H. Adaptation in Natural and Artificial Systems: An Introductory Analysis with Applications to Biology, Control and Artificial Intelligence. 197 (2nd ed. 1992). > Goldberg, D. E. Genetic Algorithms in Search, Optimization and Machine Learning. 1989. Mitchell, M. An Introduction to Genetic Algorithms. 1998.

All texts are in the library

Errata sheet for Reeves and Rowe on unit homepage

$$
\mathsf { V h a t i s E v o l u t i o n a r y C o m p u t i n g }
$$

Evolutionary Computing is a collection of 'nature-inspired' heuristic optimisation techniques, e.g.

Genetic Algorithms Genetic Programming Evolutionary Strategies

Mostly inspired by 'neo-Darwinian' evolutionary theory..

# Darwin, Mendel and the Modern Synthesis

1859 - publication of the 'Origin of Species' by one Charles Darwin

Explained evolution as due to natural selection acting on heritable variation > Very similar ideas proposed by A. R. Wallace at about the same time

1865 - Gregor Mendel presents his work on 'Experiments in Plant Hybridisation'

Demonstrated the particulate nature of inheritance (Darwin had assumed it was blending)

These two achievements together paved the way for the 'Modern Synthesis'..

# The Modern Synthesis (aka neo-Darwinism)

One problem that had worried Darwin was 'regression' of traits

Darwin assumed blending of heritable material Hence the 'value' of any trait would tend to converge in a population as evolution progressed > The resulting lack of variation in the population would give natural selectior nothing to act on, so evolution would stall

Mendel's results went un-noticed by evolutionists for about 30 years

# The Modern Synthesis (aka neo-Darwinism)

Once rediscovered, Mendel's laws of particulate (i.e. genetic) inheritance were incorporated into Darwinian evolutionary theory

The result was the 'modern synthetic theory of evolution', or 'neo-Darwinism'

Emphasises natural selection acting on genetic variation in populations Primarily mathematical in nature, modelling gene spread in populations

Population genetics Quantitative genetics

Subsequently, the physical basis of particulate inheritance was found

> Discovery of DNA by James Watson and Francis Crick, 1962 Nobel Laureates in Medicine

# The Emerg ng

Evolutionary ideas were being applied in optimisation as early as the mid 20th century, e.g.

> Box (1957) Evolutionary operation: a method for increasing industrial productivity. Applied Statistics 6, 81-101   
> Bremermann (1962) Optimization through evolution and recombination. In: Self-Organizing Systems.

n the 1970's Genetic Algorithms became a prominent research area > John Holland presented a mathematical definition of GAs, and theory explaining their performance

> Holland (1975) Adaptation in Natural and Artificial Systems > Holland was mainly interested in adaptive systems, but his student Ken De Jong catalysed reseach on for GAs for optimisation, formulating a test suite of problems

> De Jong (1975) An Analysis of the Behavior of a Class of Genetic Adaptive Systems. PhD thesis, University of Michigan

# The Simple Genetic Algorithm

$$
\mathsf { T h e S i m p l e G e n e t i c A l g o r i t h m }
$$

What is the the 'Simple Genetic Algorithm'?

Genetic algorithms have many variations on a central theme

Choice of selection operator Choice of genetic operators

The SGA is the canonical description of what a GA is

> Here we will describe the SGA according to Holland's original proposals

The SGA is also used to refer to Michael Vose's mathematical description of a GA

Vose (1999) The Simple Genetic Algorithm: Foundation and Theory

# Terminology

Before we introduce the SGA, we must introduce some terminology

> Chromosome - a solution to the problem the GA is solving, encoded as a fixed length string in some finite alphabet   
> Gene - a position on the chromosome which can take a particular value   
> Locus - see gene Allele - a value that a gene can take (e.g. 0 or 1 in binary chromosomes) Population - the set of chromosomes the GA is acting on Fitness - the objective value of the solution a chromosome encodes for a problem   
> Fitness/objective function - the function that returns the objective value of a given solution   
> Selection - the mechanism for choosing chromosomes to reproduce, based on their fitness   
> Parent - a chromosome selected for reproduction   
> Offspring - the chromosome resulting from reproduction of one or more Parents   
> Crossover - the process of recombining alleles from multiple parents during reproduction to produce offspring   
> Mutation - the process of randomly replacing offsprings' alleles with randomly chosen alternatives during reproduction

# The Simple Genetic Algorithm

generate initial chromosome population;   
while termination criterion not met do evaluate population fitness; while insufficient offspring created do select parents by fitness; if crossover condition satisfied then perform crossover; end if mutation condition satisfied then select chromosome for mutation; perform mutation; end add offspring to population; end select new population;   
end

# Selection

A key idea of the GA is that parents should be selected based on their fitness

The simplest way of doing this is using roulette wheel selection

Each chromosome $j$ in the population $P$ is assigned a probability of selection $p _ { j }$ based on its fitness $\pmb { f } _ { j }$ as a proportion of total population fitness:

$$
p _ { i } = \frac { f _ { i } } { \displaystyle \sum _ { j \in P } f _ { j } }
$$

So for a given population we construct a single-pointer 'roulette wheel' where each chromosome's proportion of the wheel is given by the equation above

To select a parent for reproduction we uniformly sample from [0, 1 i.e. we spin the roulette wheel once and see which chromosome its pointer indicates

Having selected a parent we then reproduce that parent according to our operators, parameters, etc.

> According to our parameters we may apply crossover, and/or mutation, and/or any other operators   
> Often crossover rate (probability of applying crossover during reproduction) is referred to as $\chi$   
> Similarly mutation rate (per gene probability of mutation during reproduction) by $\mu$

Usually population size is held constant...

...we continue selecting and reproducing until we have enough offspring to replace the current generation

> Hence such a GA is called a 'generational' GA

# Representation

The simplest representations use a binary alphabet > In fact, as we'l see later, Holland argued for the optimality of binary encoding > We shall assume binary chromosomes for the Simple GA

# Single-Point Crossover

Holland's initial proposal for genetic recombination in GAs was single-point crossover (1X)

For a pair of parent chromosomes of length $\ell$ , we (uniformly) choose at random an integer from $\{ 1 , 2 , \ldots , \ell - 1 \}$

We then exchange portions of each chromosome, combining the substring left of the cutpoint from one chromosome with the substring right of the cutpoint from the other chromosome, and vice versa

e.g. the parent chromosomes 11111 and 00000 with the randomly selected crossover point at position 3... > ...yield the offspring chromosomes 11100 and 00011

We now have two offpsring chromosomes, each containing alleles from both parent chromosomes

Optionally we can discard one of the offspring if we only require one offspng

During reproduction mutation occurs at a (usually low) rate, in addition to crossover

Normally mutation rate is expressed as a per-gene probability

If a gene is mutated, its current allele is exchanged for a different randomly selected allele

> If our chromosomes are binary strings, there is only one other possible allele and the gene is simply bit-flipped

A typical mutation rate might be on the order of 0.01 probability of mutation per gene 'transcribed'

$$
{ \mathsf { R e c a p } } - { \mathsf { T h e } } { \mathsf { S i m p l e } } { \mathsf { G A } }
$$

The Simple GA

generate initial population;   
while termination criterion unsatisfied do evaluate population; select parents; reproduce; replace population with offspring;

# end

Genetic operators

Single-point crossover (1X) - recombines alleles from two parents into offspring Mutation - randomly changes alleles in offspring at a very low rate

$$
\mathsf { A S i m p l e } \mathsf { E x a m p l e } \cdot \mathsf { U n i t a t i o n }
$$

Let us work through a simple example of the SGA solving a problem > Problem - Onemax (binary fixed-length chromosome, fitness is number of ones in chromosome; an example of a function of unitation)

N.B. Onemax is not a good problem to apply a GA to as the fitness function in linearly separable (e.g. hill-climbing will do much better), but it is often used for illustration

Chromosome length $( \ell ) = 5$ Population size $( N ) = 4$ Crossover rate (1X) $( \chi ) = 1 . 0$ Mutation rate $( \mu ) = 0 . 5$

Exercise: Implement the SGA on the Onemax function in a language of your choice