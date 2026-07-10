# Lecture 12: GAs as Markov Processes

# Markov Processes

Markov Processes are state-transition processes that satisfy the Markov Property

> Definition: the Markov property is the property that the probability distribution over the next possible states of a system depends only on the current state

The Markov Property is satisfied by many interesting systems, e.g

Cellular Automata Finite State Automata Genetic Algorithms

A GA satisfies the Markov Property if we specify each possible population as a separate state

> Then the probability of generating any population is a function only of the current population, and the operators used

# Markov Processes

A Markov Process can be defined by a transition matrix

The transition matrix defines the probability of reaching each possible state, from each possible state

So for a transition matrix

$$
Q = \left( \begin{array} { c c c } { { \frac { 1 } { 4 } } } & { { 1 } } & { { 0 } } \\ { { \frac { 1 } { 2 } } } & { { 0 } } & { { 1 } } \\ { { \frac { 1 } { 4 } } } & { { 0 } } & { { 0 } } \end{array} \right)
$$

the entry $Q _ { j , j }$ is the probability that row state i is reached from column state j

E.g. $\begin{array} { r } { Q _ { 1 , 0 } = \frac { 1 } { 2 } } \end{array}$

Each column is a probability distribution over states

The transition matrix is a stochastic matrix The entries must all be non-negative, and columns must sum to one

# Markov Chains

A sequence of states in a Markov Process is referred to as a Markov Chain

For any state at time t, the probability distribution over states at time $t + 1$ will be given by the transition matrix

In general we can calculate the probability distribution at time $t$ from any probability distribution over states at time t — 1, through simple matrix multiplication $p ( t ) = Q p ( t - 1 )$

$p ( t )$ is the column vector giving the probability distribution over states Knowing which state we are in is just a special kind of vector $p ( t )$ in which one entry is 1 and all others are 0

In fact we can calculate the probability distribution over states for any t in the future, given some initial probability distribution $p ( 0 )$

$$
p ( t ) = Q ^ { t } p ( 0 )
$$

# Limiting Distributions

If the transition matrix for a Markov Process is primitive, we can calculate the limiting probability distribution over the different states

Definition: A transition matrix is primitive (or regular) if $Q ^ { t }$ has all non-zero entries for some $t \geq 0$ I.e. there is a non-zero probability of reaching every possible state at some arbitrary point far enough into the future

Theorem (Perron-Frobenius): For any primitive stochastic matrix Q, $Q ^ { \infty } = \operatorname* { l i m } _ { t \to \infty } Q ^ { t }$ exists, where each column of ${ \sf Q } ^ { \infty }$ is the unique probability vector $q$ s.t. $Q q = q$ (i.e. $q$ is an eigenvector of Q with eigenvalue 1). $q = \operatorname* { l i m } _ { t \to \infty } Q ^ { t } p ( 0 )$ for any $p ( 0 )$ , and all entries of $q$ are non-negative.

> l.e. in the limit of infinite time we can calculate the expected distribution over the different possible states the process can be in

# Absorbing States

If a transition matrix is not primitive it may have absorbing states

> An absorbing state is one which, once entered by the process, willnever be left > They are identified by a 1 on the diagonal of the transition matrix

If an absorbing state can ultimately be reached from any state in the process, the Markov Chain will eventually reach an absorbing state and stay in it

In such a case we can calculate the limiting transition matrix $\mathsf { Q } ^ { \infty }$

# Absorbing States - Limiting Transition Matrix

Definition: a transition matrix is reducible if its states can be reordered to give a transition matrix of the form

$$
\boldsymbol { \mathsf { Q } } = \left[ \begin{array} { l l } { I } & { R } \\ { 0 } & { S } \end{array} \right]
$$

where I is the identity matrix, and 0 is the zeroes matrix

Theorem (Matrix Reducibility): for a reducible transition matrix Q

$$
\operatorname* { l i m } _ { t  \infty } Q ^ { t } = [ \begin{array} { l l } { I } & { R ( I - S ) ^ { - 1 } } \\ { 0 } & { 0 } \end{array} ]
$$

So for a reducibile matrix we can calculate the limiting transition matrix The matrix $( I - S ) ^ { - 1 }$ is called the fundamental matrix and is very useful

> N.B. the order of the identity matrix I used in calculating the fundamental matrix may differ from that in the decomposition of Q above

$$
\mathsf { T i m e  t o \ A b s o r p t i o n }
$$

Using the fundamental matrix we can also calculate the expected time to reach an absorbing state from any non-absorbing state

Theorem (Time to Absorption): Given a reducible transition matrix $\mathsf Q$ , the times to absorption from each of the states $k$ are the entries $a _ { k }$ in the vector

$$
{ \pmb a } = 1 ( I - S ) ^ { - 1 }
$$

where 1 is the ones matrix

$$
\mathsf { a r k o v } \mathsf { C h a i n \mathsf { A n a l y s i s } o f G A s }
$$

To apply the techniques of Markov Chain analysis to a GA, we need to

Identify the states of the process > Calculate the transition matrix

The first of these is quite straightforward

The states of the process are all the possible populations Given that a population can contain duplicates, for population size N and search space $\mathcal { C }$ the number of possible states is

$$
\binom { | { \mathcal { C } } | + N - 1 } { N }
$$

# Calculating the Transition Matrix

With all possible populations as states, we have a Markov Process

> The next state (population) depends (stochastically) only on the current population

We shall assume that the transition matrix does not change over time > Hence we have a homogenous Markov Process

With the states identified, we can now calculate the transition probabilities between states, i.e. the transition matrix

# Analysir ns

We begin by representing a population as a vector

$$
\pmb { v } = ( v _ { 0 } , v _ { 1 } , . . . , v _ { | \mathcal { C } | - 1 } )
$$

where each $V _ { k }$ is the number of copies of point $k$ in the search space, and

$$
\sum _ { k = 0 } ^ { n - 1 } v _ { k } = N
$$

The for fitness proportional selection, the probability of an individual representing point i in the search space being selected in a particular population v is

$$
P ( i | v ) _ { 1 } = \frac { v _ { i } f ( i ) } { \displaystyle \sum _ { j \in \mathcal { C } } v _ { j } f ( j ) }
$$

# Analy n

$$
\mathsf { s i n g } \mathsf { t h e \thinspace S i m p l e \thinspace G A - S e l e c t i o }
$$

Given the probability of selection $P ( i | v )$ we can calculate the probability of generating a population $u$ from population v, by using the multinomial distribution

$$
P ( u | v ) = N ! \prod _ { i \in \mathcal { C } } \frac { P ( i | v ) _ { 1 } ^ { u _ { i } } } { u _ { i } ! }
$$

Next we extend the probability expression $P ( i | v ) _ { 1 }$ to take account of the mutation and crossover operators

To do this we shall first need to construct mixing matrices for these operators...

# Mixing Matrices

A mixing matrix gives the probability of producing each possible offspring chromosome for every possible parent chromosome(s)

A mixing matrix is thus an $^ { n + }$ 1-dimensional matrix, where n is the number of parents involved in producing an offspring

Hence the mixing matrix $M$ for the mutation operator is 2-dimensional

$M _ { i , j }$ gives the probability that the operator applied to chromosome j produces chromosome i

E.g. for standard mutation on binary strings of length $\ell =$ 2 we can calculate

$$
\begin{array} { r } { \left( \begin{array} { c c c c } { ( 1 - \mu ) ^ { 2 } } & { \mu ( 1 - \mu ) } & { \mu ( 1 - \mu ) } & { \mu ^ { 2 } } \\ { \mu ( 1 - \mu ) } & { ( 1 - \mu ) ^ { 2 } } & { \mu ^ { 2 } } & { \mu ( 1 - \mu ) } \\ { \mu ( 1 - \mu ) } & { \mu ^ { 2 } } & { ( 1 - \mu ) ^ { 2 } } & { \mu ( 1 - \mu ) } \\ { \mu ^ { 2 } } & { \mu ( 1 - \mu ) } & { \mu ( 1 - \mu ) } & { ( 1 - \mu ) } \end{array} \right) } \end{array}
$$

# Mixing Matrices

For crossover, the number of parents involved is 2

Assuming 1 offspring is produced, we thus need a 3-dimensional matrix M where $M _ { i , j , k }$ is the probability that parents i and j produce offspring $k$ through crossover

However we can simplify by calculating the probability that an arbitrary chromosome is produced

$$
M ( 0 ) = \left( \begin{array} { c c } { { \cdot \cdot } } & { { \cdot \cdot \cdot } } \\ { { \ : } } & { { \cdot \cdot } } \end{array} \right)
$$

where $M _ { i , j } ( 0 )$ is the probability that chromosomes i and j produce the all-zeroes chromosome through application of the crossover operator Now we can calculate any point in the full 3-dimensional matrix through a permutation

$$
M _ { i , j } ( k ) = M _ { i \oplus k , j \oplus k } ( 0 )
$$

where i, j and k are the binary representations of the corresponding matrix indices, and $\oplus$ is XOR

$$
\mathsf { i n g \ t h e \mathsf { S i m p l e \mathsf { G A } - M u t a t i o n } }
$$

> Given our mixing matrix, which we label $U$ , the probability of generating individual i through selection then mutation is

$$
P ( i | v ) _ { 2 } = \sum _ { j \in \mathcal { C } } U _ { i , j } P ( j | v ) _ { 1 }
$$

So the two-operator transition matrix is defined by

$$
P ( u | v ) = N ! \prod _ { i \in \mathcal { C } } \frac { P ( i | v ) _ { 2 } ^ { u _ { i } } } { u _ { i } ! }
$$

Suppose that U contains only non-zero entries, as it would for standard bitwise mutation with $\mu > 0$

If there are no zero entries in $U$ , the matrix is primitive and there can be no absorbing states > The GA does not converge, and we can calculate the limiting probability distribution over the states with the Perron-Frobenius theorem

# Analysing

$$
\mathsf { g } \mathsf { t h e } \mathsf { S i m p l e } \mathsf { G A } - \mathsf { C r o s s o v e r }
$$

If we have the crossover mixing matrix M(0) and permutations on it as previously described, we can calculate the probability of producing chromosome $k$ from chromosomes i and $j$ using mutation, selection and crossover

$$
P ( k | v ) _ { 3 } = \sum _ { i , j \in \mathcal { C } } M _ { i , j } ( k ) P ( i | v ) _ { 2 } P ( j | v ) _ { 2 }
$$

As any reasonable crossover operator should be able to produce any chromosome k given suitable parents $j$ and $j$ , the sum in the above expression will be greater than zero

Also we have already shown $P ( i | v ) _ { 2 } > 0$ for all i

So the transition matrix is now

$$
P ( u | v ) = N ! \prod _ { i \in \mathcal { C } } \frac { P ( i | v ) _ { 3 } ^ { u _ { i } } } { u _ { i } ! }
$$

# and is primitive

$$
\mathsf { A n a l y s i n g : h e S i m p l e G A }
$$

We have shown that a GA with or without crossover is primitive

It has no absorbing states, hence does not converge It's limiting distribution is calculable

Theorem (Davis-Principe): If $\mathsf Q$ is the primitive transition-matrix for a GA with non-zero mutation rate, the limiting distribution is given by

$$
q _ { v } = \frac { | \mathsf { Q } _ { v } - I | } { \displaystyle \sum _ { u } | \mathsf { Q } _ { u } - I | }
$$

where $q _ { v }$ is the probability of population v, and the matrix $Q _ { u }$ is the matrix $\mathsf Q$ with the uth column replaced by zeroes

This formalises the intuition that mutation acts to prevent population convergence

# GA Non-Convergence

Consider the example of a search space $\{ 0 0 , 0 1 , 1 0 , 1 1 \}$ denoted $\mathcal { C } = \{ 0 , 1 , 2 , 3 \}$

The fitness function is $\pmb { f } ( \pmb { x } ) = \pmb { X } + \pmb { 1 }$ > I.e. $f ( 0 ) = 1 , f ( 3 ) = 4$ ,etc.

.The mixing matrix for standard mutation with $\mu =$ 0.1 is

$$
U = \left( \begin{array} { c c c c } { { 0 . 8 1 } } & { { 0 . 0 9 } } & { { 0 . 0 9 } } & { { 0 . 0 1 } } \\ { { 0 . 0 9 } } & { { 0 . 8 1 } } & { { 0 . 0 1 } } & { { 0 . 0 9 } } \\ { { 0 . 0 9 } } & { { 0 . 0 1 } } & { { 0 . 8 1 } } & { { 0 . 0 9 } } \\ { { 0 . 0 1 } } & { { 0 . 0 9 } } & { { 0 . 0 9 } } & { { 0 . 8 1 } } \end{array} \right)
$$

For population size $N = 4$ there are ${ \binom { 7 } { 4 } } = 3 5$ possible populations We can calculate the $3 5 \times 3 5$ transition matrix for fitness proportional selection and mutation

# GA Non-Convergence

Applying the Davis-Principe theorem gives us the limiting distribution over all possible populations

The highest probability populations in this limiting distribution are

<table><tr><td rowspan=1 colspan=1>Population</td><td rowspan=1 colspan=1>Probability</td></tr><tr><td rowspan=1 colspan=1>(0,0,0,4)</td><td rowspan=1 colspan=1>0.143</td></tr><tr><td rowspan=1 colspan=1>(0,0,1,3)</td><td rowspan=1 colspan=1>0.124</td></tr><tr><td rowspan=1 colspan=1>(0,1,0,3)</td><td rowspan=1 colspan=1>0.102</td></tr></table>

I.e. the most probable population is that containing only copies of the optimal solution

But, 15 possible populations contain no copies of the optimal solution, and the cumulative probability of these populations is approximately 17%

The GA will not converge, regardless of how long it is run for > This can be demonstrated empirically Exercise: Run multiple replicates of a simple GA without crossover on the above fitness function, and compare the proportion of optimal and suboptimal populations with the theoretical limits

$$
\mathsf { G A C o n v e r g e n c e }
$$

We have proved that a GA with mutation does not converge

Convergence non-proofs are less compelling arguments for using a search heuristic than convergence proofs!

How can we modify the GA so that we can prove convergence?

We might anneal the mutation rate   
> As in simulated annealing, we progressively reduce the mutation rate to restrict the search   
> However there is no guarantee the GA will converge to the optimal population

$$
\mathsf { G A C o n v e r g e n c e - E l i t i s m }
$$

Elitism can also give us provable convergence

Elitism guarantees that for the best individual $k$ in the population at time t, then at time $t +$ 1

k remains in the population, or A better solution than $k$ is in the population

Now the fitness of the best individual in the population is a monotonically increasing sequence with an upper-bound given by the optimal fitness value in the search space

# GA Convergence - Elitism

Convergence can be proved by showing that the sequence is a supermartingale

> Definition: For a stochastic sequence $X _ { 0 } , X _ { 1 } , X _ { 2 } , \dots$ and function $D$ mapping members of this sequence to the real numbers, a new stochastic sequence $D _ { 0 } , D _ { 1 } , D _ { 2 } , \ldots$ can be generated by $D _ { t } = D ( X _ { t } )$ .If the function $D$ is bounded and $E ( D _ { t + 1 } | X _ { t } ) \leq D _ { t }$ , then the sequence $D _ { t }$ is a supermartingale

Non-negative supermartingales converge almost certainly to some limit, so we can prove

Theorem (Rudolph): If $X _ { t }$ is a population at time t and $\pmb { f } ( X _ { t } )$ is the fitness of the fittest individual in $X _ { t }$ .Then for an arbitrary elitist GA the sequence $D _ { t } = f ^ { * } - f ( X _ { t } )$ , where $\pmb { f } ^ { * }$ is the fitness of the best possible solution, forms a non-negative supermartingale which converges almost certainly to zero

This is an intuitive idea, but it is nice to have a proof > We can also approximate the expected time to convergence using the absorbing states theorem on a simplified Markov process

# Calculating with Markov Chains

Markov Chain analysis can be used to analyse GA behaviour without explicitly manipulating transition matrices for realistics GAs

However, the number of possible populations (N+|C|-1)rapidly becomes unmanageable even for comparitively small $N$ and $\mathcal { C }$

To make the resulting transition matrices manageable we can apply a state aggregation technique

> Identify states sufficiently similar to be aggregated   
> Recalculate the transition matrix to take account of the new aggregated states

> Recalculate the probability of entering the aggregated states from all other states

> Recalculate the probability of reaching all other states from the aggregated states

> Calculate the probability of staying within the aggregated states

# Calculating with Markov Chains - State Aggregation

We seek states that have an identical probability distribution over the next state to be visited in the chain

> Once in one of these states, it is irrelevant which of the states we are actually in   
> These states can be aggregated into a single state without changing the behaviour of the Markov Chain   
> They can be identified by having identical columns in the transition matri

Finding states with identical distributions is unlikely, so we can aggregate other states that are in some way similar

We can compare the sum of squares difference between two matrix columns and aggregate if it is under some thereshold $\epsilon$ ,i.e. if for two matrix columns u and v

$$
\left\| u - v \right\| ^ { 2 } < \epsilon
$$

where

$$
\left\| u - v \right\| ^ { 2 } = \sum _ { k } ( P ( k | u ) - P ( k | v ) ) ^ { 2 }
$$

# Calculating with Markov Chains - Matrix Recalculation

As we aggregate states, we must recalculate the transition probabilities they are involved in

The probability of entering the newly aggregated state is simply calculated as

$$
P ( \{ u , v \} | k ) = P ( u | k ) + P ( v | k )
$$

# Calculating with Markov Chains - Matrix Recalculation

The probability of going to another state from the newly aggregated state is calculated as the weighted mean probability of the transitions from each of the original states

> The weights are estimates of the probabilities of entering each of the original states, obtained by summing the probabilities in the rows of the transition matrix for each of those states

$$
W _ { u } = \sum _ { j } P ( u | j )
$$

$$
w _ { v } = \sum _ { j } P ( v | j )
$$

So the the column in the transition matrix for the newly aggregated state is given by

$$
P ( k | \{ u , v \} ) = \frac { w _ { u } P ( k | u ) + w _ { v } P ( k | v ) } { w _ { u } + w _ { v } }
$$

# Calculating with Markov Chains - Matrix Recalculation

Finally, we calculate the probability of staying within the newly aggregated state

As for the probability of leaving the aggregated state, we must estimate the probability we are in each of the original states

The probability of staying within the new state is again a weighted mean

$$
\} | \{ u , v \} ) = \frac  w _ { u } ( P ( u | u ) + P ( v | u ) ) + w _ { v } ( P (
$$

# Calculating with Markov Chains

With these approximation tools we can simplify our transition matrix in two main way

One pass, in which we only aggregate original states Multipass, in which we aggregate aggregated states

By varying e we have a speed-accuracy trade-off

High epsilon aggregates more states, hence increases calculation speed with the transition matrix...   
...but at the expense of accuracy of the approximation   
And vice-versa