COMSM0302: Evolutionary Computing James Marshall

# Welcome

I Welcome to COMSM0302: Evolutionary Computing!   
I What is Evolutionary Computing?   
I Evolutionary Computing (EC) is a collection of ‘nature-inspired’ heuristic optimisation techniques for ‘hard’ problems, e.g. I Genetic Algorithms (GA) I Genetic Programming (GP) I Evolutionary Strategies (ES)   
I Compare with traditional exact optimisation approaches for sufficiently ‘simple’ problems I Linear Programming   
I ...and other heuristic algorithms I Simulated Annealing

# Syllabus

I Implementation

Genetic Algorithms   
I Genetic Programming   
I Other EC algorithms   
I Applications in optimisation and modelling

Descriptive models   
I Predicting behaviour   
Fundamental limits on search and optimisation

# Curriculum

20 hours of lectures, weeks 1-10

Wednesday 9:00 (1.60 QB)

I Friday 16:10 (1.11a MVB)

I Wednesday 10:00 (3.14 MVB)

Will be posted on the unit webpage before each lecture I Will be posted on the unit webpage before each lecture I Supplementary material, worked exercises, etc. will be presented during lectures.. all is useful and examinable, take notes!

lectures... all is useful and I 50% coursework, 50% exam

Genetic Algorithm assignment (30%, deadline 1st December) I Genetic Programming assignment (20%, deadline 8th December) I Theory exam (50%, January 2007)

I Additional unassessed self-learning exercises (mixture of

I I am available to answer questions during my office hour I For routine programming enquiries, use the help-desk (MVB 3.19) Answers provided after 1 week I Use these to prepare for the coursework and exam

# Curriculum

# I Lectures

<table><tr><td>Week</td><td>Topic</td></tr><tr><td>1</td><td>Introduction / Simple Genetic Algorithm</td></tr><tr><td>1</td><td>GA: Representations &amp; Operators</td></tr><tr><td>2</td><td>GA: Populations &amp; Selection</td></tr><tr><td>2</td><td>GA: Advanced Operators &amp; Techniques</td></tr><tr><td>3</td><td>GA for Grouping Problems</td></tr><tr><td>3</td><td>Overview of Genetic Programming</td></tr><tr><td>4</td><td>GP: Case Studies</td></tr><tr><td>4</td><td>GP: Case Studies</td></tr><tr><td>5</td><td>GP: Case Studies</td></tr><tr><td>5</td><td>No Free Lunch Theorems</td></tr></table>

# Curriculum

#

<table><tr><td>Week</td><td>Topic</td></tr><tr><td>6</td><td>Schema Theory</td></tr><tr><td>6</td><td>GAs as Markov Processes</td></tr><tr><td></td><td>Dynamical Systems GA Model</td></tr><tr><td></td><td>Statistical Mechanics Approximation of GA</td></tr><tr><td>8</td><td>Predicting GA Performance</td></tr><tr><td>8</td><td>Fitness Landscapes</td></tr><tr><td>9</td><td>Memetic Algorithms</td></tr><tr><td>9</td><td>Evolution Strategies</td></tr><tr><td>10</td><td>Estimation of Distribution Algorithms</td></tr><tr><td>10</td><td>Artificial Life &amp; Modelling</td></tr></table>

# Course Texts

I Recommended texts

I Reeves, C. R. and Rowe, J. E. Genetic Algorithms - Principles and Perspectives: A Guide to GA Theory, 2003. Falkenauer. E. Genetic Algorithms and Grouping Problems. 1998.

Holland, J. H. Adaptation in Natural and Artificial Systems: An Introductory Analysis with Applications to Biology, Control and Artificial Intelligence. 1975 (2nd ed. 1992).   
Goldberg, D. E. Genetic Algorithms in Search, Optimization and Machine   
Learning. 1989.   
Mitchell. M. An Introduction to Genetic Algorithms. 1998.

I All texts are in the library

# What is Evolutionary Computing?

Evolutionary Computing is a collection of 'nature-inspired' heuristic Evolutionary Computing is a optimisation techniques, e.g. Genetic Aloorithms I Genetic Programming I Evolutionary Strategies I Mostly inspired by ‘neo-Darwinian’ evolutionary theory...

# Darwin, Mendel and the Modern Synthesis

I 1859 - publication of the ‘Origin of Species’ by one Charles Darwin I Explained evolution as due to natural selection acting on heritable variation I Very similar ideas proposed by T. H. Huxley at about the same time   
I 1865 - Gregor Mendel presents his work on ‘Experiments in Plant Hybridisation’ I Demonstrated the particulate nature of inheritance (Darwin had assumed it was blending)   
I These two achievements together paved the way for the ‘Modern Synthesis’...

I One problem that had worried Darwin was ‘regression’ of traits Darwin assumed blending of heritable material I Darwin assumed blending of heritable material I Hence the ‘value’ of any trait would tend to converge in a population as evolution progressed I The resulting lack of variation in the population would give natural selection nothing to act on, so evolution would stall

Mendel’s results went un-noticed by evolutionists for about 30 years

# The Modern Synthesis (aka neo-Darwinism)

I Once rediscovered, Mendel’s laws of particulate (i.e. genetic) inheritance were incorporated into Darwinian evolutionary theory   
I The result was the ‘modern synthetic theory of evolution’, or 'neo-Darwinism' Emphasises natural selection acting on genetic variation in populations I Primarily mathematical in nature, modelling gene spread in populations I Population genetics Quantitative genetics   
Subsequently. the physical basis of particulate inheritance was found I Discovery of DNA by James Watson and Francis Crick, 1962 Nobel Laureates in Medicine

# The Emergence of Evolutionary Computing

I Evolutionary ideas were being applied in optimisation as early as the mid 20th century, e.g.

I Box (1957) Evolutionary operation: a method for increasing industrial productivity. Applied Statistics 6, 81-101   
Bremermann (1962) Optimization through evolution and recombination. Bremermann (1962) OptimizIn: Self-Organizing Systems.

I In the 1970’s Genetic Algorithms became a prominent research area

I John Holland presented a mathematical definition of GAs, and theory explaining their performance I Holland (1975) Adaptation in Natural and Artificial Systems   
Holland was mainly interested in adaptive systems. but his student Ken Holland was mainly interested in adaptive systems, but his student Ken suite of problems I De Jong (1975) An Analysis of the Behavior of a Class of Genetic Adaptive Systems. PhD thesis, University of Michigan

# The Simple Genetic Algorithm

What is the the 'Simple Genetic Algorithm'?   
Genetic algorithms have many variations on a central theme I Choice of selection operator I Choice of genetic operators   
The SGA is the canonical description of what a GA is I Here we will describe the SGA according to Holland’s original proposals   
The SGA is also used to refer to Michael Vose's mathematical description of a GA I Vose (1999) The Simple Genetic Algorithm: Foundation and Theory

#

I Before we introduce the SGA, we must introduce some terminology I Chromosome - a solution to the problem the GA is solving, encoded as a fixed length string in some finite alphabet I Gene - a position on the chromosome which can take a particular value I Locus - see gene Allele - a value that a gene can take (e.g. 0 or 1 in binary chromosomes) I Population - the set of chromosomes the GA is acting on I Fitness - the objective value of the solution a chromosome encodes for a poblem I Fitness/objective function - the function that returns the objective value of a given solution I Selection - the mechanism for choosing chromosomes to reproduce, based on their fitness Parent - a chromosome selected for reproduction Offspring - the chromosome resulting from reproduction of one or more Parents Crossover - the process of recombining alleles from multiple parents during reproduction to produce offspring I Mutation - the process of randomly replacing offsprings’ alleles with randomly chosen alternatives during reproduction

# The Simple Genetic Algorithm

# Selection

# Selection

generate initial chromosome population;   
while termination criterion not met do evaluate population fitness; while insufficient offspring created do select parents by fitness; if crossover condition satisfied then perform crossover; end if mutation condition satisfied then select chromosome for mutation; perform mutation; end add offspring to population; end select new population;   
end   
A key idea of the GA is that parents should be selected based on their fitness   
I The simplest way of doing this is using roulette wheel selection I Each chromosome i in the population $\mathcal { P }$ is assigned a probability of selection p based on its fitness f as a proportion of total population fitness:

$$
\rho _ { i } = \frac { t _ { i } } { \displaystyle \sum _ { j \in P } t _ { j } }
$$

I So for a given population we construct a single-pointer ‘roulette wheel’ where each chromosome’s proportion of the wheel is given by the equation above   
I To select a parent for reproduction we uniformly sample from [0, 1) I i.e. we spin the roulette wheel once and see which chromosome its pointer indicates

I Having selected a parent we then reproduce that parent according to our operators, parameters, e

I According to our parameters we may apply crossover, and/or mutation, and/or any other operators   
I Often crossover rate (probability of applying crossover during reproduction) is referred to as χ   
I Similarly mutation rate (per gene probability of mutation during reproduction) by µ

I Usually population size is held constant...

I ...we continue selecting and reproducing until we have enough offspring to replace the current generation I Hence such a GA is called a ‘generational’ GA

# Single-Point Crossover

I The simplest representations use a binary alphabet I In fact, as we’ll see later, Holland argued for the optimality of binary encoding We shall assume binary chromosomes for the Simple GA

Holland’s initial proposal for genetic recombination in GAs was single-point crossover (1X)   
I For a pair of parent chromosomes of length , we (uniformly) choose at random an integer from 1 2 1   
{       − } I We then exchange portions of each chromosome, combining the substring left of the cutpoint from one chromosome with the substring right of the cutpoint from the other chromosome, and vice versa I e.g. the parent chromosomes 11111 and 00000 with the randomly selected crossover point at position 3... I ...yield the offspring chromosomes 11100 and 00011   
I We now have two offpsring chromosomes, each containing alleles from both parent chromosomes   
I Optionally we can discard one of the offspring if we only require one offspring

# Mutation

I During reproduction mutation occurs at a (usually low) rate, in addition to crossover   
I Normally mutation rate is expressed as a per-gene probability   
I If a gene is mutated, its current allele is exchanged for a different randomly selected allele I If our chromosomes are binary strings, there is only one other possible allele and the gene is simply bit-flipped   
I A typical mutation rate might be on the order of 0.01 probability of mutation per gene ‘transcribed’

# Recap - The Simple GA

# A Simple Example - Unitation

The Simple GA

generate initial population;   
while termination criterion unsatisfied do evaluate population; select parents; reproduce; replace population with offspring;

#

I Let us work through a simple example of the SGA solving a problem Problem - Oneax (binary fixed-length chromosome. fitness is number of ones in chromosome; an example of a function of unitation) N.B. Onemax is not a good problem to apoly a GA to as the fitness function N.B. Onemax is not a good problem to apply a GA to as the fitness func used for illustration. Chromosome length (t) = 5 I Population size (N) = 4 I Crossover rate (1X) (χ) = 1.0 I Mutation rate (µ) = 0.5

I Genetic operators

I Single-point crossover (1X) - recombines alleles from two parents into offspring

I Exercise: Implement the SGA on the Onemax function in a language of your choice