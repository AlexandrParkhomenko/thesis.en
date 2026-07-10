Treating a GA as a Markov Process gave us some powerful analytical Treatitools

I Limiting distribution over states I Limiting transition matrix Expected time to reach an absorbing state

With a little work we can adapt our Markov Process treatment of the

Definition: A dynamical system is a mathematical formalisation of a system whose trajectory in a space evolves according to some rule By treating a GA as a dynamical system we can analyse it in terms of its trajectory in the snace of nossible nopulations

# Population Dynamics

I For the Markov Chain analysis of a GA we represented a population as a vector

$$
\pmb { v } = ( \pmb { v } _ { 0 } , \pmb { v } _ { 1 } , . . . , \pmb { v } _ { | \mathcal { L } | - 1 } )
$$

where each v is the number of copies of point k in the search space, $c$ and

$$
\sum _ { k = 0 } ^ { c - 1 } v _ { k } = N
$$

I We can remove the dependence on population size if we divide by $N$ giving a population vector

$$
\pmb { p } = ( p _ { 0 } , p _ { 1 } , . . . , p _ { | c | - 1 } )
$$

Now the population vector represents the of the population that are copies of each point in the search space N.B. recall that v and hence p are actually column vectors

# Population Dynamics

I The population vector p is a unit vector, i.e.

$$
\sum _ { k = 0 } ^ { | c | - 1 } p _ { k } = 1
$$

I So all possible populations lie within the unit simplex

Definition: A simplex is the simplest geometrical shape that can be represented in an n-dimensional space

I E.g. In 2-dimensions the simplex is a line I In 3-dimensions a triangle In 4udimensions a tetrahedeon I Etc...

The unit simplex in an -dimensional space is the shape having the n vertices (1 0 . . . 0) , (0 1 . . . 0) ,

. . , (0 0 . . . 1)

Possible populations are points within the simplex, but clearly such points can only correspond to points with rational coordinates

I I.e. vectors of the form p = ( v1 v2 . . . v|C| )

The simplex contains al points with real coordinates. i.e. rational and irrational

$$
\Lambda = \left\{ x \in \mathbb { R } ^ { n } : x _ { k } \geq 0 { \mathrm { ~ f o r ~ a l l ~ } } k { \mathrm { ~ a n d ~ } } \sum _ { k = 0 } ^ { | c | - 1 } x _ { k } = 1 \right\}
$$

I As $N \to \infty$ the set of points corresponding to possible populations → ∞        becomes in the simplex, and the simplex is their

I To describe the evolution of the dynamical system, we need a generational operator mapping points in the simplex back into the simplex

I Apart from representing population proportions, another interpretation of the population vector p is a probability distribution over all the points in the search space

Then the generational operator gives the probability distribution over all possible populations in the next generation, given the current population I Thus the generational operator is the equivalent of the Markov Process transition matrix

# Population Dynamics

# Population Dynamics - Selection

I We can also intepret the generational operator as creating a population distribution

Theorem (Vose): If the population vector p is the current population, the expected next population is (p)

In finite populations stochastic effects willead to deviations from the exnected next nonulation

The variance of this deviation will decrease as N increases

I The variance of this deviation will decrease as N increases I For infinite populations the variance will be zero so the population will behave deterministially G gives the infinite pooulation behaviou

GI We can iterate the application of to calculate the (expected) population trajectory from its initial state

I Construction of the generational operator is done in the same way as construction of the transition matrix for Markov Chain analysis

We start with selection only

From the previous lecture, the incidence vector based probability of From the prselection is

I Dividing through by N we obtain

We can specify the selection operator $\mathcal { F }$ in matrix form

I we consider our fitness function as a vector f  R whose entries $f _ { k } = f ( k \in \mathcal { C } )$ then the selection operator is

$$
\mathcal { F } ( \boldsymbol { p } ) - \frac { d _ { 1 2 \beta } ( f ) \varrho } { f \tau _ { \beta } }
$$

where diag f is the diagonal matrix with the entries from vector f on its diagonal, e.g.

$$
\operatorname { d i a g } ( { \begin{array} { c c c } { \{ 1 } & { 2 } & { 3 \} } \end{array} } ) - \left( { \begin{array} { c c c } { 1 } & { 0 } & { 0 } \\ { 0 } & { 2 } & { 0 } \\ { 0 } & { 0 } & { 3 } \end{array} } \right)
$$

The vertices of the simplex are fixed points of fitness proportional selection I Each corresponds to a different uniform population I They are absorbing states under Markov Chain analysis

Other fixed points also exist

TeCon ul A   ndvials all ha same fitness value, then

$$
{ \mathcal { H } } \{ \theta _ { k } : k \in A \} = \left\{ \sum _ { k \in A } \alpha _ { k } \theta _ { k } : \alpha _ { k } \geq 0 { \mathrm { ~ f o r ~ a l l ~ } } k { \mathrm { ~ a n d ~ } } \sum \alpha _ { k } = 1 \right\}
$$

is the convex hull of the vertices, and all members of this set are fixed points of fitness proportional selection

I So the fixed points of fitness proportional selection are

The vertices of the simplex These correspond to all the possible uniform populations   
I Mixed populations (points inside the simplex) containing individuals with the same fitness

The vertices of the simplex are always stable fixed points

I Mixed populations are only stable fixed points in the infinite population case

In the finite population case, finite population effects wil lead the In the finite population case, finite population effectspopulation away from mixed population fixed points through a combination of selection and genetic drift

# Population Dynamics - Mutation

I Mutation can easily be incorporated into the generational operator, using the mixing matrix $\upsilon$ as considered in the last lecture

The mutation operator is thus

$$
\boldsymbol { u } ( p ) = \boldsymbol { U } p
$$

I So the combined selection and mutation operator is

$$
{ \mathcal { U } } \circ { \mathcal { F } } ( p ) = { \frac { U \mathrm { d i a g } ( t ) p } { f ^ { T } p } }
$$

# Population Dynamics - Crossover

# Population Dynamics - Fixed Points

I Crossover is also incorporated by using the mixing matrix M(k) we saw in the last lecture

# Population Dynamics

I The entries i,j of $M ( k )$ are the probabilities that chromosomes i and j combine through crossover to produce chromosome k

Many crossover operators are not symmetric I E.g. UX with Bernoulli parameter = 0.5

6  However, we can construct a symmetric matrix M by taking mean probabilities, i.e. the entries i,j of M are

$$
\frac { M _ { i , i } ( k ) + M _ { i , i } ( k ) } { 2 }
$$

I With such a matrix the crossover operator is given by

$$
\mathcal { X } ( \rho ) _ { \ast } = p ^ { T } M _ { \ast } \rho
$$

I We have so far defined three main operators

I — selection F  — mutation U  I — crossover

XI The mutation and crossover operators can be composed to give what is known as the mixing operator

$$
\mathcal { M } = \mathcal { X } \circ \mathcal { U }
$$

I The generational operator can be constructed by composing any of the operators, e.g.

$$
\mathscr { G } = \mathscr { M } \circ \mathscr { F }
$$

I In general we can find the fixed points of the dynamical system by finding the eigenvectors of the matrix representing the generational operator

I E.g. for the fixed points are the eigenvectors of the matrix

I N.B. the eigenvectors must be normalised so their entries sum to one, to meet our condition for population vectors   
I The corresponding eigenvalue of the eigenvector is the mean population fitness for that fixed point

# Population Dynamics - Fixed Points

# Population Dynamics - Fixed Points

# Population Dynamics - Metastability

I Not all fixed points will necessarily correspond to real populations

The fxed points may be irrational, or not correspond to rational numbers with denominator N   
They may also lie outside the simplex I E.g. eigenvectors with negative entries

However. a more general form of the Perron-Frobenius theorem from the last lecture is useful. and tells us that

I If the matrix version of the operator has only positive entries then it has G   exactly one eigenvector (fixed point) inside the simplex   
I This is the leading eigenvector, i.e. the eigenvector with largest eigenvalue, or mean population fitness   
I This fixed point is a global attractor

I While the single interior fixed point tells us where the infinite population GA will end up, the other fixed points are also important in any analysis of finite population behaviour

To analyse this, we consider the force induced by the generational operato $\mathcal { G }$ at a point in the simplex p

$$
\mathcal { G } ( \boldsymbol { p } ) - \boldsymbol { p }
$$

I So the force is the distance that a population moves under application of the generational operator I Near a fixed point the force will be very low At a fixed point the force will be zero

I A population at a point inside the simplex may pass very close to a fixed point just outside the simplex

The force on the population will be low in this vicinity, so a finite population may spend some time there

I A finite population may not be able to exactly ‘hit’ a fixed point I In the vicinity of the fixed point the force will also be low, and again the population may spend some time there

Such population states as the above can be referred to as metastable states

Population Dynamics - Neutrality

# The Dynamical Systems Model

I Connected sets of points within the simplex may have very low force on them   
I Hence a finite population will tend to drift between these points according to stochastic effects   
I Such a set of points can be referred to as a neutral network I Neutral networks have attracted some interest, particularly as a means to escape local optima   
I What advantages does the Dynamical Systems formulation offer us?   
I We have seen some elementary analyses Analysis of trajectories I Analysis of fixed points other than the global attractor I Analysis of finite population behaviour around fixed points

I Convergence/nonconvergence properties of trajectories under different operators I Selection with mutation converges, but does crossover? What are the requirements for to be focussed? G    I Structure preserving properties of operators with a given representation I E.g. all bit-mask crossover operators provably respect schema membership There are many open questions...