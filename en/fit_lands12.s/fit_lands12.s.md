# Lecture 14: Fitness Functions and Landscapes

# Fitness Functions

So far we have examined most of the components of a GA in quite some detail   
One component we haven't paid much attention to so far is the fitness function   
We may be able to learn something about GA behaviour by analysing fitness functions, and the fitness landscapes they give rise to

# Fitness Functions - Analysis

An early attempt to analyse fitness functions and hence predict GA performance was via epistasis variance

Definition: Epistasis is the nonlinear interaction of two or more loci on some trait such as fitness > Epistasis is the multiple locus equivalent of dominance, which is defined for single loci

Epistasis will be significant in most GA problems

If there is no epistasis, then the problem is basically linear and is best solved by some other technique

If we can quantify the degree of epistasis in a problem we might gain some advantage

Identify the most appropriate technique for the problem > GAs are assumed to be best suited to problems with 'intermediate' epistasis   
Identify suitable encodings and operators > E.g. change in encoding might turn a linear fitness function into a non-linear one, and vice-versa

# Fitness Functions - Analysis

Analysis of the entire space of possible solutions is clearly impossible for any realistic optimisation problem we face

Hence we analyse epistasis variance in terms of a sample population

Mean fitness of the population $P$ is simply

$$
{ \bar { t } } = \sum _ { x \in P } { \frac { t ( x ) } { N } }
$$

Then the excess fitness value of a chromosome can be calculated as

$$
\delta ( x ) = f ( x ) - { \overline { { f } } }
$$

# Fitness Functions - Analysis

If allele a occur at locus i with frequency $N _ { i } ( a )$ , then the average value of that allele is

$$
A _ { i } ( a ) = \sum _ { x : x _ { i } = a } { \frac { f ( x ) } { N _ { i } ( a ) } }
$$

The excess fitness value of having allele a at locus $j$ is thus

$$
\delta _ { i } ( a ) = A _ { i } ( a ) - \overline { { f } }
$$

Summing these gives the excess genic value of chromosome x

$$
\delta _ { G } ( x ) = \sum _ { i = 0 } ^ { \ell - 1 } \delta _ { i } ( a )
$$

So the epistasis value is the difference between the fitness predicted by linear combination of the alleles of the chromosome, and the actual fitness of the chromosome

$$
\boldsymbol { \epsilon } ( \boldsymbol { x } ) = \boldsymbol { \delta } ( \boldsymbol { x } ) - \boldsymbol { \delta } _ { G } ( \boldsymbol { x } )
$$

# Fitness Functions - Analysis

Under this epistasis variance analysis it is seen that

$$
\sum _ { x } \delta ( x ) ^ { 2 } = \sum _ { i = 0 } ^ { \ell - 1 } \sum _ { a } \delta _ { i } ( a ) ^ { 2 } + \sum _ { x } \epsilon ( x ) ^ { 2 }
$$

l.e. > Total 'variance' $=$ Genic 'variance' $^ +$ Epistasis 'variance'

This is directly analogous to the result we get in statistics on   
partitioning Sum of Squares Error (SS) from Analysis of Variance   
(ANOVA) > Total SS $=$ Main effects SS $^ +$ Interaction SS

In fact the theory of epistastis variance was previously developed in the field of statistics called experimental design

# Fitness Functions - Analysis

Is epistasis variance useful for predicting GA performance on a fitness function?

There are two main problems with this approach

Sampling Signs of the interaction effects

Sampling

> As already observed the search space will be too large to fully analyse for epistasis variance   
4 So a random subset sample must be used instead   
> However this sample is likely to be far too small in comparison to the search space to guarantee meaningful results from the analysis

# Fitness Functions - Analysis

Signs of the interaction effects

ANOvA is only concerned with the absolute magnitude of the interaction effects

> Squaring the errors gives them all the same sign

For epistasis variance, however, the sign of the interaction effects is highly relevant

If the signs of the interaction effects on a locus match the sign of the genic effects at that locus, interaction simply reinforces the selective advantage of particular alleles   
> If the signs of the interaction effects on a locus differ from the sign of the genic effects at that locus, interaction interferes with the selective advantage of particular alleles

# Fitness Functions - Walsh Analysis

We can also analyse a fitness function with a useful tool known as the Walsh transform

The Walsh transform decomposes any boolean function into a superposition of boolean functions known as the Walsh functions

The Walsh transform is the boolean equivalent of the Fourier transform Like the Fourier transform, the Walsh transform is useful in signal processing, image processing, etc.

The Walsh transform is also useful in many area of GA analysis

# Fitness Functions - Walsh Analysis

The Walsh-transform of a function is

$$
f ( x ) = \sum _ { j = 0 } ^ { 2 ^ { \ell } - 1 } w _ { j } \psi _ { j } ( x )
$$

The $j .$ -th Walsh function of $x$ is defined as

$$
\psi _ { j } ( x ) = \prod _ { i = 1 } ^ { \ell } ( 1 - 2 x _ { i } ) ^ { j _ { i } }
$$

where $j _ { i }$ is the $j .$ -th bit of the binary vector representing the integer $j$ and similarly for Xi

The $j .$ -th Walsh coefficient of $f ( x )$ is defined as

$$
w _ { j } = \frac { 1 } { 2 ^ { \ell } } \sum _ { x = 0 } ^ { 2 ^ { \ell } - 1 } f ( x ) \psi _ { j } ( x ) .
$$

# Fitness Functions - Walsh Analysis

4 Walsh-decomposition can only be done on small enough function, but is useful for general theory

The Walsh coefficients crop up in many places

Epistasis variance Schema theory

$$
\mathsf { A n a l y s i s - E p i s t a s i s V a r i a n c e }
$$

For all binary chromosomes we can write the decomposition of effects on the fitness of string (0, 0, 0) as

$$
\vdash \alpha _ { 0 } + \beta _ { 0 } + ( \alpha \beta ) _ { 0 0 } + \gamma _ { 0 } + ( \alpha \gamma ) _ { 0 0 } + ( \beta \gamma ) _ { 0 0 }
$$

Then the fitness effects above are given by the Walsh coefficients arising from the Walsh-transform of the fitness function

$$
\begin{array} { c } { { \mu = W _ { 0 } } } \\ { { \alpha _ { 0 } = W _ { 1 } } } \\ { { \beta _ { 0 } = W _ { 2 } } } \\ { { ( \alpha \beta ) _ { 0 0 } = W _ { 3 } } } \\ { { \gamma _ { 0 } = W _ { 4 } } } \\ { { ( \alpha \gamma ) _ { 0 0 } = w _ { 5 } } } \\ { { ( \beta \gamma ) _ { 0 0 } = w _ { 6 } } } \\ { { ( \alpha \beta \gamma ) _ { 0 0 0 } = W _ { 7 } } } \end{array}
$$

$$
h \mathsf { A n a l y s i s - E p i s t a s i s V a r i a n c }
$$

The relationship between the Walsh coefficients and the variation terms can be understood as follows

The number of 1s in the binary version of the Walsh function's subscript gives the number of interaction effects represented by that coefficient > The position of those 1s represents which interaction effects are represented by that coefficient, by indexing from least significant bit to most significant bit the gene-level effect variables we have from the previous equation

$$
( 0 ) \alpha , ( 1 ) \beta , ( 2 ) \gamma , . . .
$$

E.g. $w _ { 0 } = w _ { 0 0 0 } = \mu$ (no interaction effects) E.g. $w _ { 3 } = w _ { 0 1 1 } = ( \alpha \beta ) _ { 0 0 }$

$$
\mathsf { h } \mathsf { A n a l y s i s - S c h e m a } \mathsf { T h e o r e r }
$$

Recall that schemata can be thought of as periodic binary functions

Walsh functions are also periodic binary functions

Hence we can also get schema fitness averages, by choosing the appropriate Walsh coefficients to combine

E.g. population mean fitness $= w _ { 0 }$ $\begin{array} { r l } & { f ( \ast \ast 0 ) = W _ { 0 } + W _ { 1 } } \\ & { f ( \ast \ast 1 ) = W _ { 0 } - W _ { 1 } } \\ & { \mathsf { E t c } . . . } \end{array}$

This can be used to construct deceptive fitness functions, by imposing appropriate conditions on the Walsh coefficients

# Deception

Deception is a historically important concept in the development of GA theory, and is based on the schema theory

The idea is that a fitness function will be hard for a GA if the schema fitnesses lead the GA away from the global optimum

> Such a function is described as deceptive

Goldberg proposed the following simple deceptive fitness functior

<table><tr><td>String</td><td>Fitness</td></tr><tr><td>000</td><td>7</td></tr><tr><td>001</td><td>5</td></tr><tr><td>010</td><td>5</td></tr><tr><td>011 100</td><td>0</td></tr><tr><td>101</td><td>3</td></tr><tr><td>110</td><td>0</td></tr><tr><td></td><td>0</td></tr><tr><td>111</td><td>8</td></tr></table>

Fitness is increased by removing ones from the string, but the global optimum contains only ones

# Fitness Landscapes

# Fitness Landscapes - History

Sewall Wright's idea of a fitness landscape for evolution through natural selection (below, from Wright (1932)) is also appealing for EC

![](images/1eca808fda6203830effe785b659d7afc31fff26ee23bdc2b7a26dbd2d989ca7.jpg)

Populations under selection seek to occupy fitness peaks separated by fitness valleys

# Fitness Landscapes - Definition

The analysis of fitness landscapes, and the behaviour of Evolutionary Algorithms on them, is an interesting area

To perform such analysis, we must first define what a fitness landscape is

Definition: A fitness landscape for a fitness function $f$ is a triple $\mathcal { L } = ( \mathcal { C } , t , d )$ , where $d : \mathcal { C } \times \mathcal { C } \to \mathbb { R } ^ { + } \cup \{ \infty \}$ is the distance measure, such that for all s, $t$ and $u$ in the search space $\mathcal { C }$

$$
d ( s , t ) \geq 0
$$

$$
d ( s , t ) = 0 \Leftrightarrow s = t
$$

$$
d ( s , u ) \leq d ( s , t ) + d ( t , u )
$$

If the measure is also symmetric, then we have a distance metric on points in our search space

# Fitness Landscapes - Neighbourhoods

Once we have a distance measure on the search space, we can define the concept of a neighbourhood

Definition: The neighbourhood $N ( S )$ of a point s in the search space is the set of points that can be reached from s by a single application of an operator $\omega$ . $d _ { \omega }$ to be the distance measure under the operator $\omega$ where

$$
t \in N ( s ) \Leftrightarrow d _ { \omega } ( s , t ) = 1
$$

The distance between non-neighbours is the length of the shortest path between them

The important thing to note is that for discrete optimisation problems neighbourhoods, and fitness landscapes, must be defined in terms of an operator

It contrasts with optimisation of functions such as $f : \mathbb { R } \to \mathbb { R }$ where the real number line gives a well defined neighbourhood structure independent of 'operator' > It is important for any analysis of a fitness landscape in terms of optima, etc.

# Fitness Landscapes - Isomorphism

Fitness landscapes may be isomorphic

> Definition: Two fitness landscapes are isomorphic if they are equivalent to each other under an appropriate change of representation and operator

E.g. consider the Bit-Flip (BF) and Complementary Crossover (CX) operators

BF neighbourhood

$N ( [ 0 0 0 0 0 ] ) = \{ ( 1 0 0 0 0 ) , ( 0 1 0 0 0 ) , ( 0 0 1 0 0 ) , (  $ 00010), (00001)}

> CX neighbourhood (1X with a complementary string)

$N ( [ 0 0 0 0 0 ] ) = \{ ( 0 0 0 0 1 ) , ( 0 0 0 1 1 ) , ( 0 0 1 1 1 ) , ( 0 0 1 1 1 ) , ( 0$ 01111),(11111)}

# Fitness Landscapes - Isomorphism

The fitness landscape with standard binary encoding and the CX operator, and the fitness landscape with Gray-encoding and the BF operator, are isomorphic

E.g. consider the neighbours of (00000) in both landscapes

<table><tr><td></td><td>BF-Neighbours</td><td>Gray-Integer</td></tr><tr><td rowspan="6">00000</td><td>00001</td><td>1</td></tr><tr><td>00010</td><td>3</td></tr><tr><td>00100</td><td>7</td></tr><tr><td>01000</td><td>15</td></tr><tr><td>10000</td><td>31</td></tr><tr><td>CX-Neighbours</td><td>binary-Integer</td></tr><tr><td>00000</td><td></td><td></td></tr><tr><td rowspan="6"></td><td>00001</td><td>1</td></tr><tr><td>00011</td><td>3</td></tr><tr><td>00111</td><td>7</td></tr><tr><td>01111</td><td>15</td></tr><tr><td>11111</td><td>31</td></tr><tr><td></td><td></td></tr></table>

This recalls the isomorphism results from Radcliffe & Surry's NFL proof

# Fitness

$$
\mathsf { L a n d s c a p e s \cdot L o c a l O p t i m a }
$$

Definition: A point $s \in { \mathcal { C } }$ on a fitness landscape $\mathcal { L } = ( \mathcal { C } , t , d )$ is a local optimum if for all $t \in N ( s )$ , $t ( s ) \geq t ( t )$

N.B. one (or more) of the local optima in the landscape will also be the   
global optimum/optima of the search space   
The number of local optima in a fitness landscape will be one important   
factor in performance of a search algorithm   
Even more important are the relative basins of attraction of the different   
optima > Definition: The basin of attraction of a local optimum is the set of points in the search space from which that local optimum will be attained under some search strategy

N.B. while the fitness landscape depends on the operator used but not on the search strategy, the basins of attraction also depend on the search strategy used

# Fitness Lan

$$
\mathsf { d s c a p e s \mathrm { \cdot B a s i n s \ o f \ A t t r a c t i o t } }
$$

Compare the basins of attraction under the BF operator of two different neighbourhood search strategies

Steepest ascent

<table><tr><td rowspan=1 colspan=1>Local optimum</td><td rowspan=1 colspan=1>01010</td><td rowspan=1 colspan=1>01100</td><td rowspan=1 colspan=1>00111</td><td rowspan=1 colspan=1>10000</td></tr><tr><td rowspan=1 colspan=1>Fitness</td><td rowspan=1 colspan=1>4100</td><td rowspan=1 colspan=1>3988</td><td rowspan=1 colspan=1>3803</td><td rowspan=1 colspan=1>3236</td></tr><tr><td rowspan=1 colspan=1>Basin size</td><td rowspan=1 colspan=1>20</td><td rowspan=1 colspan=1>3</td><td rowspan=1 colspan=1>4</td><td rowspan=1 colspan=1>5</td></tr></table>

First ascent

<table><tr><td rowspan=1 colspan=1>Local optimum</td><td rowspan=1 colspan=1>01010</td><td rowspan=1 colspan=1>01100</td><td rowspan=1 colspan=1>00111</td><td rowspan=1 colspan=1>10000</td></tr><tr><td rowspan=1 colspan=1>Fitness</td><td rowspan=1 colspan=1>4100</td><td rowspan=1 colspan=1>3988</td><td rowspan=1 colspan=1>3803</td><td rowspan=1 colspan=1>3236</td></tr><tr><td rowspan=1 colspan=1>Basin size</td><td rowspan=1 colspan=1>14</td><td rowspan=1 colspan=1>6</td><td rowspan=1 colspan=1>4</td><td rowspan=1 colspan=1>8</td></tr></table>

While the local optima are unchanged, the basins of attraction under the two different search algorithms are different

# Fitness Landscapes - Analysis

It is also possible to analyse specific problems (objective functions) under specific search neighbourhoods

Definition: Under objective function $f$ , for some neighbourhood $\mathcal { N }$ the graph Laplacian is

$$
\nabla ^ { 2 } f = \left( \sum _ { i = 1 } ^ { | N | } \delta _ { i } \right) / | N | .
$$

where $\delta _ { j }$ is the difference in objective value between the current search point and its $j .$ -th neighbour

So the graph Laplacian is the mean difference in objective value between a point in the search space and its neighbours

> This is analagous to the continuous-space Laplacian operator from physics, of interest when modelling wave propagation and other physical phenomena

# Fitness Landscapes - Analysis

Some objective functions and neighbourhoods induce a graph Laplacian for the search space $s$ of the form

$$
\nabla ^ { 2 } f + { \frac { K } { | S | } } f = 0
$$

for constant K

Consider the Symmetric Travelling Salesman Problem with objective function

$$
h = \sum _ { i = 1 } ^ { | S | } I _ { i , ( i + 1 ) \bmod | S | }
$$

where $I _ { j , j }$ is the length of the edge between vertices i and j > So we want to minimise $h$ during our search

# Fitness Landscapes - Analysis

Theorem (Grover1): The Travelling Salesman Problem with city pair swap neighbourhood and with 'normalised' objective function $\overline { { h } } = h - \langle h \rangle$ satisfies

$$
\nabla ^ { 2 } \overline { { h } } = - \frac { 4 } { | S | } \overline { { h } }
$$

I.e. the mean difference in neighbours' values is always a constant (negative) multiple of the value of the current solution

This is already interesting, because it tells us that uniformly at random swapping two cities in a tour is expected to result in an improved solutio when that solution is below average quality.. ...and a worse solution when that solution is above average quality > I.e. random search converges on average quality solutions

# Fitness Landscapes - Analysis

Graph Laplacians like those in the Symmetric TSP example can tell us further interesting things

Theorem (Grover2): for objective functions whose graph Laplacian has the form $\nabla ^ { 2 } f + K f / | { \cal S } | = 0$ , all local minima have $f \leq 0$ and all local maxima have $f \geq 0$

So all local minima are below average value and all local maxima are above average value   
Greedy local search until a local optimum is hit will definitely yield an above average solution

# Fitness Landscapes - Analysis

How long will it take local search to find a local optimum?

Theorem (Grover3): a greedy local search algorithm starting from an arbitrarily poor configuration will reach a local optimum in at most $O ( | S | L )$ iterations, where the best solution is at most $2 ^ { L }$ better than the average over the search space

> N.B. how $L$ relates to the problem is not addressed here.. if it is a constant this is good news!

Symmetric TSP with pair-swap neighbourhood is not unique in satisfying this requirement on the Graph Laplacian

It can also hold for other well known NP-complete problems

Min-cut graph partitioning Graph colouring Minimum weight partition

# Fitness Landscapes - Reference

> Grover, L. K. (1992) Local search and the local structure of NP-complete problems. Operations Research Letters 12, 235-243