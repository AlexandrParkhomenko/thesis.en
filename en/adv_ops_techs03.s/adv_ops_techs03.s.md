# Lecture 4: Advanced Operators and Techniques

# Inversion

We have seen variations on the basic operators so far

> Crossover

> Mutation

Holland's earliest work included a proposal for a further operator > Inversion

Holland implicitly recognised the positional bias of 1X

Inversion was his solution, intended to bring co-adapted alleles at distant loci closer together on the chromosome

The biological interpretation of the inversion operator is that it maintains linkage disequilibrium due to selection in the face of disruption by crossover

> Definition: two loci in a population are in linkage equilibrium if the frequency distribution of alleles at one locus is independent of the frequency distribution of alleles at the other locus

# Inversion

Data: $\ell$ — length of chromosome   
$i _ { 1 } \gets$ random integer between 0 and $\ell$ inclusive;   
$i _ { 2 } \gets$ random integer $\neq i _ { 1 }$ between 0 and $\ell$ inclusive;   
if ${ \dot { I } } _ { 1 } > { \dot { I } } _ { 2 }$ then swap $j _ { 1 }$ and $i _ { 2 }$ ;   
end   
for $I = \dot { I } _ { 1 }$ to $\lfloor ( I _ { 1 } + I _ { 2 } - 1 ) / 2 \rfloor$ do swap allele and index at locus I with allele and index a $\begin{array} { r } { i _ { 1 } + i _ { 2 } - 1 - I ; } \end{array}$   
end

# Inversion

An index is needed for each locus to preserve the meaning of the locus independent of its position on the chromosome

Prior to crossover, both parents must be reordered if their ordering is different

Some ordering must then be assigned to the offspring, perhaps randomly selected from one of the parents

Of course, inversion is redundant with operators such as UX, which do not have any positional bias

# Population Selection Schemes

We have previously looked at different selection operators

Roulette Wheel Selection (RWS) Stochastic Univeral Sampling (SUS)

These operators all used Holland's original generational selection scheme

Each iteration of the GA completely replaces the population with the offspring of those selected to reproduce

Other selection schemes exist > Overlapping Steady state $( \lambda , \mu )$ and $( \lambda + \mu )$ Elitism

# Overlappin ate Selection

Under selection let $1 \leq G \leq N$ individuals be selected for replacement   
These are replaced by G offspring from the reproduction phase   
If $1 < G < N$ we have overlapping generations   
G is sometimes referred to as the generation gap Clearly generational selection is a special case of overlapping selection where $\mathsf { G } = N$   
At the other extreme $G = 1$ > This is sometimes referred to as the steady state GA

$$
( \lambda , \mu ) \mathsf { a n d } ( \lambda + \mu )
$$

Selection schemes from Evolutionary Strategies are also applicable

$$
\boldsymbol { \cdot } ~ \left( \lambda , \mu \right)
$$

λ parents are selected for reproduction

> They produce $\mu \geq \lambda$ offspring

> The best $\lambda$ offspring are selected for the next generation

As for $( \lambda , \mu )$ , except the best individuals for the next generation are selected from the combined set of parents and offspring

N.B. $\mu$ here is not the same as $\mu$ for mutation rate

Typical selection and genetic operators do not guarantee that the best individual in the population will be in the next generation

Fitness proportional, rank and tournament selection may not select the best individual   
> Even if selected, crossover and mutation are likely to destroy the best individual

Thus the best solution found so far is frequently discarded by the GA

Elitism avoids this by always preserving it in the next generation > Remaining $N - 1$ individuals are replaced by new strings (assuming a generational GA)

# Further Measures of Selection

In the last lecture we saw how to calculate selection probabilities and selection pressure for certain selection schemes

Linear rank selection Soft tournament selection

Additional measures of selection for comparison of selection schemes exist

Selection intensity > Takeover time

# Selection Intensity

Selection pressure can be directly calculated from the selection probabilities under a particular selection scheme

Selection intensity is a measure taken on the behaviour of a selection scheme

$$
I ( t ) = \frac { \bar { \boldsymbol { f } } _ { s e I } ( t ) - \bar { \boldsymbol { f } } ( t ) } { \sigma _ { f ( t ) } }
$$

# Selection Intensity

Selection intensity is a post hoc measure of the difference in mean fitness of individuals selected for reproduction, and mean fitness of all individuals in the population

> Scaled by population standard deviation to allow meaningful comparison across cases   
> Applies only to generational GAs in this form, but elitist and steady state versions have been derived

Theoretical results have also been achieved, under the assumption of a normal fitness distribution

# Takeover Time

Selection can also be measured in terms of the time needed for the best individual to take over the entire population

Assuming no crossover and mutation, only selection

Empirical results can be obtained to compare various selection schemes

Theoretical results have been derived that agree well with empirical values

Takeover time for most selection strategies is ${ \cal O } ( \log N )$ Takeover time for fitness proportional selection s ${ \cal O } ( N \log N )$

Takeover time is related to the rate at which diversity is lost through selection

# Diversity Maintenance

Diversity is crucial for any kind of evolution (as we will see in detail later in the course)

Natural   
Artificial   
Evolutionary computation

Diversity can be maintained by various strategies

Modified selection / genetic operators Modified representations Fitness sharing schemes

Loss of diversity can be a signal to terminate an evolutionary algorithm

$$
\mathsf { v e r s i t y } \mathsf { P r e s e r v i n g \ O p e r a t o r s }
$$

We can use 'incest prevention' to maintain diversity

> Prevenosoverdviduals ho ilariy v threshold   
Similarity can be measured as the reciprocal of Hamming distance   
The threshold must be increased as selection results in population   
convergence

Alternatively we can implement a 'no duplicates' policy > Individuals are not inserted into the population if they match an individual already in the population

This requires comparing each new individual against every individual already in the population The naïve approach to this for a generational GA has $O ( N )$ time complexity

$$
\mathsf { v e r s i t y } \mathsf { P r e s e r v i n g \mathsf { O p e r a t o r s } }
$$

We can also force operators to produce novel offspring (i.e. not clones of either parent)

E.g. 1X applied to 1101001 and 1100010 will always generate a clone if the crossover point is any of the first three positions

We can identify suitable crossover points before applying the crossover operator

For binary chromosomes compute the XOR of the two parents > 0001011 for the example above

> Select a crossover point lying between the outermost 1s in the XOR string

# Fitness Sharing

We can also maintain diversity through modifying the selection mechanism

Fitness sharing, as its name suggests, shares fitness between individuals occupying the same niche

> Niche is a term from biology denoting a particular set of environmental conditions, to which an organism or organisms may become adapted

E.g. herbivores and carnivores are adapted, or specialised, to eat plants and other animals respectively

A simple linear sharing function such as

$$
h ( d _ { i j } ) = { \left\{ \begin{array} { l l } { 2 - { \frac { d _ { i j } } { D } } } & { { \mathrm { i f } } d _ { i j } < D } \\ { 1 } & { { \mathrm { o t h e r w i s e } } } \end{array} \right. }
$$

is evaluated for all pairs of individuals in the population

> $d _ { i j }$ is the distance between individuals i and j > $D$ is a tunable distance threshold

# Fitness Sharing

For every individual j we then compute the sum

$$
\varsigma _ { j } = \sum _ { i \neq j } h ( d _ { i j } )
$$

> then divide its raw fitness by $\varsigma _ { j }$ to give the adjusted fitness that will be used during selection

Hence very similar chromosomes (under some distance metric) will have their fitnesses reduced more than unique chromosomes

Care must be taken in choosing the distance metric

In particular, should it be based on genotypic or phenotypic distance? E.g. if $d _ { i j }$ were Hamming distance then as we have seen genetically similar individuals can have very different phenotypes, and vice versa

$$
\mathsf { D i p l o i d y a n d \mathsf { D o m i n a n c e } }
$$

All the representations we have seen in our examples so far allow one allele to occupy each locus

In biological terminology, this is haploidy

Haploidy is not typical in nature, diploidy is far more common

Each locus carries two alleles, which encode for some trait Often one allele is dominant over another

E.g. imagine that for eye colour in humans there are two alleles The brown eye allele is dominant (B), the blue eye allele is recessive (b) Then the homozygote bb encodes for blue eyes, the homozygote BB and the heterozygotes bB and Bb all encode for brown eyes

Alleles can also be partially dominant, or additive

# Diploidy and Dominance

Diploidy and dominance explain the ratio of offspring phenotypes that Mendel discovered

Intriguingly, for any distribution of phenotypes where the underlying allele frequencies are m and $n = 1 - m$ , one generation of random mating without selection results in a stable equilbrium

$$
E ( A A ) = m ^ { 2 } , E ( A a ) = 2 m n , E ( a a ) = n ^ { 2 }
$$

This is the Hardy-Weinberg equilibrium, from population genetics

Exercise: for the genotype frequency ratio $p : 2 q : r$ , derive the genotype frequency ratio after one generation of random mating without selection

The equilbrium demonstrates that, in the absence of selection, Mendelian genetics will not result in the spread or disappearance of dominant or recessive alleles

I.e. diploidy is diversity preserving in the absence of selection It was originally thought that dominance would lead to elimination of a recessive allele even in the absence of selection

$$
\mathsf { D i p l o i d y a n d \mathsf { D o m i n a n c e } }
$$

Diploidy and dominance are also a diversity preserving technique

If adominant trait is fiter that  ecessivcounterpart(),allele fr those recessive traits will still be preserved in the population despite negative selection   
> Dominance itself may evolve, so that the fitter trait is necessarily the dominant one   
> This could allow an improved evolutionary response to environmenta change, where relative fitnesses of traits are reversed

Hence diploidy and dominance could be useful in GAs

Particularly in GAs with non-static objective functions

# Diploidy and Dominance

Dominance and diploidy can be simply implemented in a GA

Assume 3 alleles

> 0: encodes for trait 0 1: recessively encodes for trait 1 2: dominantly encodes for trait 1

This gives the following dominance map

<table><tr><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>0</td><td rowspan=1 colspan=1>1</td><td rowspan=1 colspan=1>2</td></tr><tr><td rowspan=1 colspan=1>0</td><td rowspan=1 colspan=1>0</td><td rowspan=1 colspan=1>0</td><td rowspan=1 colspan=1>1</td></tr><tr><td rowspan=1 colspan=1>1</td><td rowspan=1 colspan=1>0</td><td rowspan=1 colspan=1>1</td><td rowspan=1 colspan=1>1</td></tr><tr><td rowspan=1 colspan=1>2</td><td rowspan=1 colspan=1>1</td><td rowspan=1 colspan=1>1</td><td rowspan=1 colspan=1>1</td></tr></table>

The phenotypic ratio for dominants of 3 to 1 is achieved for allele pairings of 0 with 1, and 0 with 2

Dominance can evolve through allele substitution of 1 for 2 and vice versa

# Termination

So far we have not considered when to stop the GA

We are probably applying the GA to a problem for which we do not know the global optimum Hence we may not be able to specify a termination criterion in terms of quality of solution discovered On the other hand we may be able to specify a termination criterion in terms of a solution that is 'good enough'

> We can term this satisficing

Given that evolution requires variability to act on, we could terminate the GA when population variability has fallen

> E.g. when some statistical measure of population diversity falls below a threshold   
> E.g. when an attempt is made to cross an individual with a clone of itself

Other common termination criteria are fixed number of generations, or fixed processing time, etc.

$$
\mathsf { M u l t i o b j e c t i v e ~ O p t i m i s a t i o n }
$$

Many optimisation algorithms, including EC, seek to optimise a single objective function

Many optimisation problems, however, have multiple conflicting objectives

I.e. multiple objective functions

The simple approach to solving this is to assign fitness as a weighted sum of the value of each of the separate objective functions

This requires us a priori to decide on the relative importance of the different objectives

As GAs (and most EC algorithms) are population based, we can take a different approach...

# Pareto Optimality

By using the concept of Pareto-optimality we can find a set of solutions that are all optimal compromises between the conflicting objectives

We can then examine this set and select one solution from it according to our needs > This approach is much more flexible

Pareto-optimality is a concept used in economics, game theory, etc.

> Definition: Solution A is dominated by solution B if solution B is better according to at least one objective, and no worse according to the other objectives

> Definition:A Pareto-optimal solution is one that is not dominated by any oher solution, i.e. it is one in which no objective can be improved without a deterioration in one or more of the other objectives

N.B. do not confuse the definitions of dominates and dominance!

$$
\mathsf { M u l t i o b j e c t i v e E C }
$$

Several approaches to using Pareto-optimality in EC are possible, e.g.

> Adjust the fitness function to favour non-dominated individuals 4 Rank-based selection assigning joint ranks to individuals

Assign rank 1 to all non-dominated individuals in the population, and remove Assign rank 2 to all remaining non-dominated individuals, and remove

> Select only dominated individuals for deletion from the population (in overlapping selection)