# Schema Theory

Schema theory is Holland’s original theoretical explanation for how GAs work

I The theory is based on the concept of a schema (plural schemata)

Definition: For chromosomes of length ( in an alphabet 4. a schema is asbst of the sacin which llh romoss sha particular set of defined values

articular set of defined values I Schemata are represented as strings in the original alphabet extended with a wildcard symbol (e.g. ")   
I E.g. for = 0, 1 , the schema (1 ) represents the chromosomes A  { }  (100), (101), (110), (111)

{   } I Schemata have two characteristics, order and length

I Definition: The order of a schema is the number of defined (non-wildcard) bpositions it has   
Definition: The length of a schema is the distance between its first and last defined positions

# Schemata

I Schemata can be interpreted in three obvious ways

I Set-theoretically Schemata define subsets of the set of al possible chromosomes   
I Geometrically I Schemata define hyperplanes on an -dimensional hypercube   
I Functionally I Schemata define periodic functions of different frequency

# Implicit Parallelism

# The Schema Theorem

Schema theory is based on the idea of implicit parallelism

I Any chromosome is a member of 2\` schemata

I For each locus the chromosome can be represented by a schema having either the chromosome's actual value at its corresponding locus. or the wildcard

I A population of size N could contain up to $N 2 ^ { \ell }$ different schemata However the usual figure will be much lower, due to simila chromosomes, particularly as the population converges

I By evaluating a chromosome’s fitness, according to Holland’s ideas, we are simultaneously evaluating many schemata l.e. we are parallelising the search of the solution space

# The Schema Theorem

The Schema Theorem analyses what happens to schemata as the The Schema GA executes

I We shall present the theorem based on the Simple GA

I I.e. fitness-proportional, generational selection, 1X and single-point mutation.

I First we must define the fitness of a schema S at time t as the mean fitness of the strings in the population that are members of it

$$
f ( S , t ) = \frac { \displaystyle \sum _ { x \in S \cap R } t ( x ) } { | S \cap P _ { t } | }
$$

Next, we define the fitness ratio of the schema's fitness to the population mean fitness

I First we analyse how the expected number of instances of a schema changes through selection alone

I From the definition of fitness proportional selection, this is given by

$$
\begin{array} { r } { E ( N _ { \bar { 3 } , t + 1 } ) = r ( \bar { S } , t ) N _ { \bar { 3 } , t } } \end{array}
$$

$$
r ( S , t ) = \frac { t ( S , t ) } { \overline { { f } } ( t ) }
$$

I This ignores the constructive and destructive effects of genetic operators on schemata

# The Schema Theorem

# The Schema Theorem

# The Schema Theorem

I Next we calculate the probability with which a schema may be destroyed by crossover alone as

$$
1 - \chi \frac { I _ { S } } { \ell - 1 } P _ { e } ( S , t )
$$

I wher $I _ { \mathcal { S } }$ is the length of schema S, and $P _ { \theta }$ is the probability the other parent is not a member of schema S

I N.B. we ignore the possibility of another instance of schema S being created through crossover

The Schema Theorem derives results for what happens to a schema independent of other schemata in the population Hence the probablity above is a lower-bound on the probability that a schema is transmitted to the next generation To make the probabilty fully indenendent of other schemata in the population, we can se $P _ { \theta } ( S , t ) = 1$ , so the independent lower bound is

$$
1 - \chi \frac { I _ { 5 } } { \ell - 1 }
$$

Now we calculate the probability with which a schema may be destroyed by mutation alone

I where k is the order of schema S

I Again, this probability is a lower bound, as we are not considering the possibility that an instance of schema S can be created through mutation

$$
( 1 - \mu ) ^ { \mu _ { 4 } } \geq 1 - \mu k _ { 5 }
$$

Our simplified version (the r.h.s. of the inequality) comes from assuming µ is small, so we can ignore terms $\mu ^ { a }$ for q > 1

$$
E ( N _ { S , t + 1 } ) \geq ( 1 - \chi \frac { I _ { S } } { \ell - 1 } - \mu k _ { S } ) r ( S , t ) N _ { S , t }
$$

Interpreting the above expression as involving a selection component and a loss component gives a nice parallel with the Breeder's Equation from quantitative genetics

$$
R = s h ^ { 2 }
$$

I where R is the response to selection, s is the selection coefficient, and h2 is the heritability coefficient (N.B. not h raised to the 2nd power)

I The Schema Theorem is used to make several further arguments The Building Block Hypothesis I The Building Block HypothesisI The Two-Armed Bandit Analogy The Principle of Minimum Alphabets

# The Building Block Hypothesis

From the Schema Theorem we know that the representation of a schema S in the population should increase when

$$
r ( S , t ) \geq 1 + \chi \frac { l _ { S } } { \ell - 1 } + \mu k _ { S }
$$

I Short, low-order schemata will be unlikely to be disrupted by crossover and mutation. hence require a fitness ratio only slightly above 1 to spread Long, high-order schemata are much more vulnerable to disruption, so require correspondingly higher fitness ratios

I So, a GA should work well when it can combine short, low-order schemata (building blocks) to form better solutions I The assumption that this is how a GA works is termed the building block hypothesis

# The Two-Armed Bandit Analogy

I Holland drew an analogy between competition amongst schemata, and the two-armed bandit   
I The two-armed (or n-armed) bandit is a problem from statistical decision theory I Given a ‘bandit’ with two (or n) arms each returning different, noisy rewards, what is the best trial-allocation strategy to maximise future expected reward?   
I Holland argued that by allocating exponentially increasing numbers of   
trials to the superior schemata, the GA approximates the optimal strategy For the GA there are actually several bandits, all with many more than two arms As we are solving a non-linear problem. the order in which the bandits are solved is likely to be important I Despite this, Holland argued the theory could still be applied by placing a lower bound on the loss incured by choosing an incorrect schema competition winner

# Summary

I Holland also argued for the optimality of binary encoding, using schema theory   
I The implicit parallelism argument suggests we should try to maximise the number of schemata processed simultaneously   
I The number of possible schemata for an alphabet is $| A + 1 | ^ { \varepsilon }$   
This will be maximised when chromosome lenath < is maximised. which to store some fixed amount of information occurs when is minimised The smallest possible value of is, . binary encoding |A|      I So the maximum number of possible schemata is achieved by binary encoding

The Schema Theory tracks changes in frequency of representation of subsets of the search space (schemata), independent of the other schemata in the population

I Its formulation reveals the conflicting pressures of positive selection, and destructive genetic operators

I It has been used to make some proposals about how GAs (should) work

The Building Block Hypothesis I The Building Block HypothesisI The Two-Armed Bandit Analogy The Principle of Minimum Alphabets

I But is it a good explanation of GA behaviour?