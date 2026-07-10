# Finite Markov Chain Results in Evolutionary Computation: A Tour d'Horizon

Günter Rudolph Universität Dortmund, Fachbereich Informatik XI, D-44 221 Dortmund

Abstract. The theory of evolutionary computation has been enhanced rapidly during the last decade. This survey is the attempt to summarize the results regarding the limit and finite time behavior of evolutionary algorithms with finite search spaces and discrete time scale. Results on evolutionary algorithms beyond finite space and discrete time are also presented but with reduced elaboration.

Keywords: evolutionary algorithms, limit behavior, finite time behavior

# 1. Introduction

The field of evolutionary computation is mainly engaged in the development of optimization algorithms which design is inspired by principles of natural evolution. In most cases, the optimization task is of the following type: Find an element $x ^ { \ast } \in \chi$ such that $f ( x ^ { * } ) \geq f ( x )$ for all $x \in \mathcal { X }$ , where $f : \mathcal { X }  \mathbb { R }$ is the objective function to be maximized and $\chi$ the search set.

In the terminology of evolutionary computation, an individual is represented by an element of the Cartesian product $\chi \times \mathcal { A }$ , where $\mathcal { A }$ is a possibly empty set collecting additional search state information. The fitness of an individual $( x , a ) \in \mathcal { X } \times \mathcal { A }$ is given by the objective function value $f ( x )$ . A population consists of $n < \infty$ individuals and is thus an element of the product space $( { \mathcal { X } } \times { \mathcal { A } } ) ^ { n }$ . During each iteration of an evolutionary algorithm the population is modified by a number of successive probabilistic transformations. At the beginning of each iteration the $n$ members of the population are called the parents which produce $n ^ { \prime } < \infty$ off spring by random variation: For each offspring two or more parents are selected and they are used to generate a preliminary offspring by recombination. Subsequently, each preliminary offspring is mutated at random yielding a final offspring. After all $n ^ { \prime }$ offspring have been produced in this manner the current population consist of $n + n ^ { \prime }$ individuals. To keep the population at constant size $n$ , a selection method decides which parents and/or offspring will serve as parents in the next iteration. Now the process repeats until some stopping criterion is fulfilled.

Evidently, the resulting new population only depends on the state of the current population in a probabilistic manner. This fact, known as the Markov property, reveals that Markov processes are appropriate models for the probabilistic behavior of evolutionary algorithms. The welldeveloped theory of Markov processes may be divided into twelve sub-fields according to the following characteristics of the true process under consideration:

The state space may be finite, denumerable or not denumerable.   
The evolution may happen in discrete or continuous time.   
The transition probabilities may depend on the time parameter or not.

Since the population size is finite the state space of the associated Markov process is finite (denumerable or not denumerable) if the search set is finite (denumerable or not denumerable). Therefore the Markov theory of evolutionary algorithms may be classified analogously. Most results are available for evolutionary algorithms with time-homogeneous transitions and (1) finite search space in discrete time, (2) not denumerable search space $\mathbb { R } ^ { \ell }$ in discrete as well as continuous time.

This survey will concentrate on the first class including the case of time-inhomogeneous transitions.

# 2. Limit Behavior in Finite Space and Discrete Time

Let $X _ { k } = ( X _ { k , 1 } , X _ { k , 2 } , . . . , X _ { k , n } )$ be the random population of size $n \ < \ \infty$ at step $k \geq 0$ and $F _ { k } = \operatorname* { m a x } \{ f ( X _ { k , i } ) : i = 1 , \dots , n \}$ the best fitness value within the population at step $k \geq 0$ . As soon as the random variable $F _ { k }$ attains the value of the global maximum $f ^ { * }$ it is ensured that the population contains an individual representing the global solution of the maximization problem. Ideally, this event should happen after a finite number of steps with probability one and regardless of the initialization of the evolutionary algorithm. This desirable property can be formalized as follows.

# Definition 2.1.

Let random variable $T = \operatorname* { m i n } \{ k \ \geq \ 0 \ : \ F _ { k } = \ f ^ { * } \}$ denote the first hitting time of the global solution. An evolutionary algorithm is said to visit the global optimum in finite time with probability one if $\mathsf { P } \{ T < \infty \} = 1$ regardless of the initialization.

Since it may be generally supposed that in practical implementations of evolutionary algorithms the best solution found in the course of the evolution is kept in memory, the property above guarantees that the global optimum will be found in finite time and never be lost although the population itself may loose the global solution once it was found. Thus, the property above alone does not exclude that the random sequence $\left( F _ { k } : k \ge 0 \right)$ oscillates freely without tending to a limit. There are evolutionary algorithms that show exactly such a behavior. But it can also be observed that there exist versions of evolutionary algorithms for which the random sequence $\left( F _ { k } : k \ge 0 \right)$ "converges" to the limit $f ^ { * }$ . Notice that the deterministic concept of the "convergence to the optimum" is not appropriate because the state transitions of an evolutionary algorithm are of stochastic nature. In order to clarify the exact semantic of a phrase like "the EA converges to the global optimum" one has at first to distinguish between the various modes of stochastic convergence [1].

# Definition 2.2.

Let $D _ { 0 } , D _ { 1 } , \ldots$ be non-negative random variables defined on a probability space $( \Omega , { \mathcal { A } } , { \mathsf { P } } )$ . The sequence $\left( D _ { k } : k \ge 0 \right)$ is said to converge completely to zero if $\textstyle \sum _ { k = 0 } ^ { \infty } \mathsf { P } \{ D _ { k } > \epsilon \} < \infty$ for any $\epsilon > 0$ , to converge with probability 1 (w.p.1) or almost surely (a.s.) to zero if $\mathsf { P } \{ \mathsf { l i m } _ { k \to \infty } D _ { k } =$ $0 \} = 1$ , to converge in probability to zero if ${ \mathsf P } \{ D _ { k } > \epsilon \} = o ( 1 )$ as $k  \infty$ for any $\epsilon > 0$ , and to converge in mean to zero if $\mathsf { E } [ D _ { k } ] = o ( 1 )$ as $k  \infty$ .

Complete convergence implies convergence with probability 1 while both convergence with probability 1 and convergence in mean implies convergence in probability. The reverse implications are wrong in general [1]. But if the sequence $\left( D _ { k } : k \ge 0 \right)$ is upper bounded by some finite constant then convergence in probability implies convergence in mean. With these definitions one can assign a rigorous meaning to the notion of the convergence of an evolutionary algorithm.

# Definition 2.3.

Let $( X _ { k } : k \ge 0 )$ be the sequence of populations generated by some evolutionary algorithm and let $F _ { k } = \operatorname* { m a x } \{ f ( X _ { k , 1 } ) , . . . , f ( X _ { k , n } ) \}$ denote the best objective function value of the population of size $n < \infty$ at generation $k \geq 0$ . An evolutionary algorithm is said to converge completely (with probability 1, in probability, in mean) to the global maximum $f ^ { * } = \operatorname* { m a x } \{ f ( x ) : x \in \mathcal { X } \}$ of objective function $f : \mathcal { X } \ \to \ \mathbb { R }$ if the nonnegative random sequence $\left( D _ { k } \ : \ k \ \ge \ 0 \right)$ with $D _ { k } = f ^ { * } - F _ { k }$ converges completely (with probability 1, in probability, in mean) to zero.

At this point it should be noted that the property of visiting the global solution with probability one is a precondition for convergence but that the additional property of convergence does not automatically indicate any advantage with respect to finding the global solution.

# 2.1. Time-Homogeneous Transitions

In principle, the question whether some evolutionary algorithm will visit the global optimum in finite time and, if so, whether it will converge in some mode to the optimum or not may be answered by modeling the specific evolutionary algorithm under consideration as a finite Markov chain so that the existing powerful results from Markov chain theory [2, 3] can be exploited. Completely specified Markov chain models of a certain evolutionary algorithm were derived (apparently independently) in [4] and [5, 6]. But it is not necessary to build a quantitatively exact Markov model for each variant of an evolutionary algorithm in order to investigate the limit behavior. Instead, qualitative models are sufficient for this purpose. The idea to characterize the limit behavior of the evolutionary algorithm by the properties of the variation and selection operators was realized in [7]. This approach is adopted here. Actually, almost all results presented in this subsection are already given in [7, 8]. Subsequent publications offered some minor extensions in case of specific combination of variation and selection operators [9, 10, 11, 12] or from a more abstract point of view [13, 14]. In retrospective, one may say that the intensive elaboration of these issues during the past years has finally led to simple proofs which do not require Markov chain theory any more. This is demonstrated next.

Let $( x _ { 1 } , x _ { 2 } , \ldots , x _ { n } ) \in { \mathcal { X } } ^ { n }$ denote the population of parents. An offspring is produced as follows: At first, $\rho$ parents are selected to serve as mates for the recombination process. This operation is denoted by

$$
{ \mathrm { m a t } } : { \mathcal { X } } ^ { n }  { \mathcal { X } } ^ { \rho }
$$

where $2 \leq \rho \leq n$ . These individuals are then recombined by the procedure

$$
\operatorname { r e c o } : \mathcal { X } ^ { \rho }  \mathcal { X }
$$

yielding a preliminary offspring. Finally, a mutation via

$$
\operatorname* { m u t } : \mathcal { X } \to \mathcal { X }
$$

yields the complete offspring. After all $m$ offspring have been produced in this manner the selection procedure

$$
\operatorname { s e l } : { \mathcal { X } } ^ { k } \to X ^ { n }
$$

decides which offspring and possibly parents $( k \geq n )$ will serve as the new parents in the next iteration. Thus, a single iteration of the evolutionary algorithm can be described as follows:

$$
\forall i \in \{ 1 , . . . , m \} : x _ { i } ^ { \prime } = \operatorname* { m u t } \big ( \operatorname { r e c o } \big ( \operatorname* { m a t } \big ( x _ { 1 } , . . . , x _ { n } \big ) \big ) \big )
$$

$$
\left( y _ { 1 } , \ldots , y _ { n } \right) = \left\{ { \begin{array} { c l } { \operatorname { s e l } ( x _ { \pi ( 1 ) } , \ldots , x _ { \pi ( q ) } , x _ { 1 } ^ { \prime } , \ldots , x _ { m } ^ { \prime } ) } & { { \mathrm { ( p a r e n t s ~ a n d ~ o f f s p r i n g ) } } } \\ { \operatorname { s e l } ( x _ { 1 } ^ { \prime } , \ldots , x _ { m } ^ { \prime } ) } & { { \mathrm { ( o n l y ~ o f f s p r i n g ) } } } \end{array} } \right.
$$

where $1 \leq q \leq n$ and $\pi ( 1 ) , \ldots , \pi ( n )$ is a permutation of the indices $1 , \ldots , n$ such that $f ( x _ { \pi ( 1 ) } ) \geq$ $f ( x _ { \pi ( 2 ) } ) \geq \cdot \cdot \cdot \geq f ( x _ { \pi ( n ) } )$ . This formulation includes selection methods that choose from the offspring and a subset of parents under the restriction that the best parent is a member of this subset.

After this operational description of evolutionary algorithms one is in the position of defining some assumptions about the properties of the variation and selection operators:

${ \mathrm { ( A _ { 1 } ) } } \forall x \in ( x _ { 1 } , \ldots , x _ { n } ) : \mathsf { P } \{ x \in \mathrm { r e c o } ( \mathrm { m a t } ( x _ { 1 } , \ldots , x _ { n } ) ) \} \geq \delta _ { r } > 0 .$   
$\left( \mathrm { A } _ { 2 } \right)$ For every pair $x , y \in { \mathcal { X } }$ there exists a finite path $x _ { 1 } , x _ { 2 } , \ldots , x _ { k }$ of pairwise distinct points with $x _ { 1 } = x$ and $x _ { k } = y$ such that $\mathsf { P \{ \ x }  _ { i + 1 } = \mathsf { m u t } ( x _ { i } ) \} \ge \delta _ { m } > 0$ for all $i = 1 , \ldots , k - 1$ .   
$\left( \mathrm { A } _ { 2 } ^ { \prime } \right)$ For every pair $x , y \in { \mathcal { X } }$ holds $\mathsf { P } \{ y = \mathrm { m u t } ( x ) \} \ge \delta _ { m } > 0$ .   
$\left( \mathrm { A } _ { 3 } \right)$ $\forall x \in \left( x _ { 1 } , \ldots , x _ { k } \right) : \mathsf { P } \{ x \in \mathrm { s e l } ( x _ { 1 } , \ldots , x _ { k } ) \} \subseteq \delta _ { s } > 0 .$   
$\left( \mathrm { A } _ { 4 } \right)$ Let $v _ { k } ^ { * } ( x _ { 1 } , . . . , x _ { k } ) \ = \ \operatorname* { m a x } \{ f ( x _ { i } ) \ : \ i = \ 1 , . . . , k \}$ denote the best fitness value within a population of $k$ individuals $( k \geq n )$ . The selection method fulfills the condition

$$
\begin{array} { r } { \mathsf { P } \{ v _ { n } ^ { * } ( \mathrm { s e l } ( x _ { 1 } , . . . , x _ { k } ) ) = v _ { k } ^ { * } ( x _ { 1 } , . . . , x _ { k } ) \} = 1 . } \end{array}
$$

Assumption $\left( \mathrm { A } _ { 1 } \right)$ means that every parent may be selected for mating and is not altered by recombination with minimum probability $\delta _ { r } > 0$ . Assumption $\left( \mathrm { A } _ { 2 } \right)$ ensures that every individual can be changed to an arbitrary other individual by a finite number of successive mutations, whereas assumption $\left( \mathrm { A } _ { 2 } ^ { \prime } \right)$ asserts the same but within a single mutation. Assumption $\left( \mathrm { A } _ { 3 } \right)$ guarantees that every individual competing for survival may survive with minimum probability $\delta _ { s } > 0$ , whereas assumption $\left( \mathrm { A } _ { 4 } \right)$ makes sure that the best individual among the competitors in the selection process will survive with probability one.

# Theorem 2.1.

If the assumptions $\left( \mathrm { A } _ { 1 } \right) , \left( \mathrm { A } _ { 2 } \right)$ , and $\left( \mathrm { A } _ { 3 } \right)$ are valid then the evolutionary algorithm visits the global optimum after a finite number of iterations with probability one, regardless of the initialization. If assumption $\mathrm { ( A _ { 4 } ) }$ is valid additionally and the selection method chooses from parents as well as offspring then the evolutionary algorithm converges completely and in mean to the global optimum regardless of the initialization.

Proof: Let $\mathcal { X } ^ { \ast } = \{ x \in \mathcal { X } : f ( x ) = f ^ { \ast } \}$ be the set of globally optimal solutions. Owing to assumption $\left( \mathrm { A } _ { 2 } \right)$ there exists a finite path from an arbitrary $x \notin \mathcal { X } ^ { \ast }$ to some $x ^ { * } \in \mathcal { X } ^ { * }$ that can be traversed by successive mutations. Let $k _ { x }$ be the length of the shortest path between $x \notin \mathcal { X } ^ { \ast }$ to the set $\chi ^ { \ast }$ and $k ^ { * } = \operatorname* { m a x } \{ k _ { x } : x \notin \mathcal { X } ^ { * } \}$ .

Now consider an arbitrary parent $x$ of some population. Assumption $\left( \mathrm { A } _ { 1 } \right)$ ensures that this parent passes the recombination process without being altered at least with probability $\delta _ { r } > 0$ . The probability that this preliminary offspring transitions to the next point of the shortest path towards $\chi ^ { \ast }$ by mutation is guaranteed to be at least $\delta _ { m } ~ > ~ 0$ by assumption $\left( \mathrm { A } _ { 2 } \right)$ . Owing to assumption $\left( \mathrm { A } _ { 3 } \right)$ this offspring will survive the selection process at least with probability $\delta _ { s } > 0$ . Thus, the probability that parent $x$ transitions to a parent representing the next point on the shortest path to $\chi ^ { \ast }$ is at least $\delta _ { r } \cdot \delta _ { m } \cdot \delta _ { s } > 0$ . A $k _ { x }$ -fold repetition of this argumentation shows that the probability of a transition from $x \notin \mathcal { X } ^ { \ast }$ into the set $\chi ^ { \ast }$ at iteration $k _ { x }$ is at least $\left( \delta _ { r } \cdot \delta _ { m } \cdot \delta _ { s } \right) ^ { k _ { x } - 1 } \cdot \delta _ { r } \cdot \delta _ { m } > 0$ . Therefore it can be asserted that the probability of visiting a globally optimal solution after $k ^ { * }$ iterations is at least $\delta = ( \delta _ { r } \cdot \delta _ { m } \cdot \delta _ { s } ) ^ { k ^ { * } - 1 } \cdot \delta _ { r } \cdot \delta _ { m } > 0$ regardless of the true instantiation of $x \notin \mathcal { X } ^ { \ast }$ . Consequently, the probability that a globally optimal solution has not been found after $k$ iterations is at most $\left( 1 - \delta \right) ^ { \lfloor k / k ^ { * } \rfloor }$ which converges exponentially fast to zero as $k  \infty$ . This immediately implies $\mathsf { P } \{ T < \infty \}$ , i.e., a global optimum will be visited for the first time after a finite number of iterations with probability one. This proves the first part of the theorem.

As for the second part, suppose that the global optimum was found for the first time at iteration $k _ { 0 }$ . Assumption $\mathrm { ( A _ { 4 } ) }$ guarantees that this offspring will be a parent of the next iteration, since neither an old parent nor another offspring can be better than this one. Thus,

$$
\mathsf { P } \{ F _ { k } < f ^ { * } \} = \mathsf { P } \{ f ^ { * } - F _ { k } > 0 \} = \mathsf { P } \{ D _ { k } > 0 \} \le ( 1 - \delta ) ^ { \lfloor k / k ^ { * } \rfloor } \to 0
$$

as $k  \infty$ . This proves convergence in probability. Since

$$
\sum _ { k = 0 } ^ { \infty } \mathsf { P \{ \phi D _ { k } > 0 \mathrm { ~ } \} } \le \sum _ { k = 0 } ^ { \infty } ( 1 - \delta ) ^ { \lfloor k / k ^ { * } \rfloor } \le \frac { 1 } { 1 - ( 1 - \delta ) ^ { 1 / k ^ { * } } } < \infty
$$

one obtains even complete convergence to the global optimum. Finally, convergence in mean follows from convergence in probability and the fact that the sequence $\left( F _ { k } : k \ge 0 \right)$ is bounded.

A variation of this result is given next.

# Corollary 2.1.

Theorem 2.1 remains valid if the assumptions $\mathrm { ( A _ { 1 } ) }$ , $\left( \mathrm { A } _ { 2 } \right)$ , and $\left( \mathrm { A } _ { 3 } \right)$ are replaced by assumption $\left( \mathrm { A } _ { 2 } ^ { \prime } \right)$ .

As can be seen from assumptions $\left( \mathrm { A } _ { 2 } \right)$ or $\left( \mathrm { A } _ { 2 } ^ { \prime } \right)$ , the reachability of the optimum is guaranteed solely by the properties of the mutation operators. The potential positive effects of recombination are completely neglected. Notice that an EA without recombination ( $\begin{array} { r } { \delta _ { r } = 1 ) } \end{array}$ will always visit the optimum, whereas an EA without mutation but with a usual recombination operator does not have this guarantee [10]. This observation might have been the reason why Evans [15] suggested the following modified EA "without" mutation.

Let $\chi = \{ 0 , 1 \} ^ { \ell }$ . The population consist of $n + 2$ parents. Two distinguished parents are protected, i.e., they pass through all stages of the life cycle with probability one, but they participate in the mating and recombination process. In the initial population, the first protected individual is chosen at random and the second protected individual is set to the binary complement of the first one. Suppose that the recombination process employs uniform crossover of two parents, i.e., each entry of the offspring's bit vector is independently chosen either from the first or from the second parent with the same probability. Moreover, assume that the two protected individuals can be chosen for mating with some minimum probability $\delta _ { c } > 0$ . If this event occurs then the optimal solution is assembled with probability $2 ^ { - \ell } > 0$ . Notice that this is equivalent to generating an individual uniformly at random. As a consequence, the probability to find the optimum within one step is at least $\delta _ { c } 2 ^ { - \ell } > 0$ and it is guaranteed that the optimum will be visited in finite time with probability one. Needless to say, the concept of protected individuals in nothing more than a disguised method of permitting mutations.

The next result complements and partially sharpens Theorem 1 and Corollary 1.

# Theorem 2.2.

An evolutionary algorithm visits the global optimum infinitely often if assumption $\left( \mathrm { A } _ { 2 } ^ { \prime } \right)$ or the assumptions $\left( \mathrm { A } _ { 1 } \right)$ , $\left( \mathrm { A } _ { 2 } \right)$ , and $\left( \mathrm { A } _ { 3 } \right)$ are valid. If the selection method only chooses from the offspring then the sequence $\left( F _ { k } : k \ge 0 \right)$ will not converge to the global optimum, even if assumption $\left( \mathrm { A } _ { 4 } \right)$ is valid.

Proof: The proof of Theorem 1 has already shown that conditions $\left( \mathrm { A } _ { 2 } ^ { \prime } \right)$ or $\left( \mathrm { A } _ { 1 } \right)$ , $\left( \mathrm { A } _ { 2 } \right)$ , $\left( \mathrm { A } _ { 3 } \right)$ are sufficient to find the optimum in finite with probability one. Assume that the optimum has been visited at step $k _ { 1 }$ for the first time and that the population looses all optimal individuals at step $k _ { 2 } > k _ { 1 }$ . Then the same assumptions guarantee that the optimum will be found again in finite time with probability one at step $k _ { 3 } > k _ { 2 }$ , and possibly lost again and found again and so forth ad nauseam. This proves the first part of the theorem.

As for the second part, let the selection method only choose from the offspring and assume that the optimum is contained in the current population (possibly several times). Even if all optimal parents pass through the recombination process without being altered, assumption $\left( \mathrm { A } _ { 2 } \right)$ as well as $\left( \mathrm { A } _ { 2 } ^ { \prime } \right)$ ensures that each individual is mutated with some minimum probability. As a consequence, there is a minimum probability $\delta _ { L } > 0$ that all individuals being optimal before mutation are mutated to non-optimal individuals. Since the probability of this event is strictly bounded from zero, the population will loose the optimum in finite time with probability one. But the optimum will be found again, and lost again ... in short: The sequence $\left( F _ { k } : k \ge 0 \right)$ of the best fitness value within a population at step $k \geq 0$ oscillates forever preventing the property of stochastic convergence.

The assumptions and their implications presented so far are valid for the vast majority of evolutionary algorithms with finite search space and time-homogeneous transitions. But every conference on evolutionary computation gives birth to new versions of evolutionary algorithms that do not necessarily fit in this framework. In this case, the assumptions and proofs must be adapted. For example, it was recently shown that Corollary 1 can be generalized to situations in which the set of fitness values is only partially in lieu of totally ordered [16]. Actually, only the assumptions regarding the selection methods were generalized.

# 2.2. Time-Inhomogeneous Transitions

The development of evolutionary algorithms with time-inhomogeneous transitions was motivated by the observation that a specific popular evolutionary algorithm fulfilling the preconditions of Theorem 2 did apparently not converge, and by the fact that there existed convergence proofs for stochastic optimization algorithms with time-inhomogeneous transitions [4, 17]. The previous subsection has already disclosed the reason for non-convergence of the sequence $\left( F _ { k } : k \ge 0 \right)$ . The optimum is found and lost infinitely often. Needless to say, stochastic convergence with time-inhomogeneous transitions also requires the precondition that the optimum will be found in finite time with probability one. But if the optimum is not guaranteed to stay in the population, then it is necessary that it will be found again. In order to prevent everlasting oscillation of the sequence $\left( F _ { k } : k \ge 0 \right)$ it must be ensured that the event of finding the optimum happens infinitely often whereas the event of loosing the optimum happens only finitely often. Actually, this is the decisive property that must be shown when proving global convergence of an evolutionary algorithm—may the transitions be time-homogeneous or not.

The Borel-Cantelli Lemma and its extension are actually sufficient to establish conditions for stochastic convergence of an evolutionary algorithm. Since EAs have the Markov property the condition is as follows: Let $\alpha _ { k }$ be the probability of loosing the optimum and $\beta _ { k }$ the probability of finding the optimum at step $k$ . If

$$
\sum _ { k } \alpha _ { k } < \infty \qquad \mathrm { a n d } \qquad \sum _ { k } \beta _ { k } = \infty
$$

then the event of loosing the optimum happens finitely often with probability 1 whereas the probability of visiting the optimum happens infinitely often with probability one. Thus, the probability of loosing the optimum must decrease faster than the probability of finding the optimum.

Davis [4, 17] tried to establish this property by introducing a time-dependent decreasing schedule for the probability of mutating an individual of an evolutionary algorithm with selection from offspring only. Clearly, a decreasing mutation probability leads to decreasing sequences of both probabilities $\alpha _ { k }$ and $\beta _ { k }$ . But there is problem: The rate of decrease is of the same order for both sequences. As a consequence, both sequences either converge or diverge, i.e., either the optimum is not found with probability one or the sequence $( F _ { k } : k \ge 0 ) $ oscillates forever. This observation reveals that the selection mechanism must be time-dependent.

Mahfoud and Goldberg [18] used time-homogeneous mutations fulflling assumption $\left( \mathrm { A } _ { 2 } ^ { \prime } \right)$ and adopted the time-inhomogeneous selection method as it is known from simulated annealing. Assumption $\left( \mathrm { A } _ { 2 } ^ { \prime } \right)$ ensures $\beta _ { k } = \beta > 0$ and hence the divergence of the sequence $\left( \beta _ { k } : k \ge 0 \right)$ while the simulated annealing like selection method yields the convergence of the sequence $\left( \alpha _ { k } : k \ge 0 \right)$ .

Cerf employed the Freidlin/Wentzel theory of dynamical perturbed systems to prove global convergence for time-dependent schedules for recombination, mutation, and selection operators [19, 20] while Suzuki [21], Lozano et al. [22], as well as He and Kang [23] came to similar results via Markov chain theory. Since most of these results are specialized to certain combinations of variation and selection operators, it is refrained from reproducing all assumptions here.

# 3. Finite Time Behavior in Finite Space and Discrete Time

The examination of the finite time behavior of evolutionary algorithms cannot be treated in the same general manner as it is possible for the limit behavior. Apart from the problem type under consideration, the choice and parameterization of the variation and selection operators have a significant impact on the finite time behavior of evolutionary algorithms. As a consequence, the theoretical studies are restricted to certain problem classes and simple evolutionary algorithms yet.

Most results are available for maximizing real-valued fitness functions with domain $\chi =$ $\mathbb { B } ^ { \ell } = \{ 0 , 1 \} ^ { \ell }$ . This problem is called the pseudo-boolean optimization problem [24] and it is known to be NP-hard in general [25]. But there are classes of pseudo-boolean optimization problems with reduced computational complexity.

Here, it is assumed that the time of calculating the fitness value $f ( x )$ for $x \in \mathbb { B } ^ { \ell }$ is bounded by a polynomial in $\ell$ . Since the population size is finite, the number of fitness evaluations is an appropriate measure to assess the efficiency of an evolutionary algorithm. Evidently, for this purpose one needs a stopping rule that indicates the termination of the stochastic process. Unless there is a efficiently computable criterion to decide whether the optimum has been found or not, one has to define another stopping rule that may depend on the entire history of the process. Let $\mathcal { H } _ { k }$ contain the information available to the process until iteration $k \geq 0$ . Then the stopping rule $\tau ( \mathcal { H } _ { k } )$ indicates termination at step $k \geq 0$ if it evaluates to 1, and continuation of the process if it evaluates to 0. Notice that a stopping rule induces a random stopping time

$S = \operatorname* { m i n } \left\{ k \geq 0 : \tau ( \mathcal { H } _ { k } ) = 1 \right\}$ in general. After these preparations one is in the position to offer a criterion for efficient evolutionary algorithms.

# Definition 3.1.

Let $F _ { k } ^ { * } = \operatorname* { m a x } \{ F _ { k - 1 } ^ { * } , F _ { k } \}$ for $k \geq 1$ and $F _ { 0 } ^ { * } = F _ { 0 }$ denote the best fitness value found until iteration $k ~ \geq ~ 0$ . An evolutionary algorithm is said to be efficient for a problem class $\mathcal { C }$ if $\mathsf { E } [ S ] \leq \mathrm { p o l y } _ { 1 } ( \ell )$ and $\mathsf { P } \{ F _ { S } ^ { \ast } = f ^ { \ast } \} \ge 1 / \mathsf { p o l y } _ { 2 } ( \ell )$ for every instance of $\mathcal { C }$ , where $\mathrm { p o l y } _ { 1 } ( \cdot )$ and $\mathrm { p o l y } _ { 2 } ( \cdot )$ are two polynomial functions of the problem dimension $\ell$ .

The association of the term "efficient" with this criterion is justified by the algorithmic technique known as probability amplification or probability boosting [26]. Suppose there exists an efficient EA for some problem class with $1 / \mathrm { p o l y } _ { 2 } ( \ell ) \le \mathsf { P } \{ F _ { S } ^ { \ast } = f ^ { \ast } \} < 1$ . The probability that the optimal solution is not found after $r$ independent runs (possibly in parallel) of the EA is at most $( 1 - 1 / \mathrm { p o l y } _ { 2 } ( \ell ) ) ^ { r }$ . The choice $r = k \cdot \mathrm { p o l y } _ { 2 } ( \ell )$ with $k ~ \in ~ \mathbb { N }$ leads to a total expected sequential runtime $r \in [ S ]$ which remains polynomial in $\ell$ , whereas the probability of not finding the optimum in $r$ runs decreases exponentially in $k$ .

If $\mathsf { E } [ S ] \leq \mathrm { p o l y } _ { 1 } ( \ell )$ and $\mathsf { P } \{ F _ { S } ^ { * } = f ^ { * } \} = 1$ , then the evolutionary algorithm always gives the optimal solution. The only variation from one run to another is its random running time, whose distribution has to be studied. Theoretical work regarding evolutionary algorithms with random stopping time is rarely available. Hulin [27] suggested a stopping rule that is optimal in a certain Bayesian sense, but the goodness of this stopping rule in the sense of Definition 3.1 was studied empirically only. Aytug and Koehler [28] developed bounds on the number of iterations $s$ required to achieve the validity of the inequality ${ \mathsf { P } } \{ { \mathsf { \Pi } } F _ { s } ^ { * } = f ^ { * } { \mathsf { \Pi } } \} \ge \alpha$ for some prescribed $\alpha > 0$ . Their final results were designated to be trivial since they did not take into consideration the function to be maximized. This omission finally led to an optimal parameterization under which the EA degenerates to pure random search with population size $n = 1$ . As a consequence, the bound on $s$ was not polynomial but exponential in the problem dimension $\ell$ . This observation reveals the necessity of restricting the analysis to certain problem classes whose special properties can be exploited in order to achieve non-trivial results.

As in the work of Aytug and Koehler [28] let the stopping rule not depend on the history of the evolutionary process. More specifically, the EA is stopped after a prescribed number $s$ of iterations so that the random stopping time $S$ degenerates to the constant $s$ with $\mathsf { E } [ S ] = s$ and $\mathsf { V } [ S ] = 0$ . Moreover, it is assumed that the EA only employs mutation and elitist selection. Notice that this assumption implies $F _ { k } \ = \ F _ { k } ^ { * }$ for all $k ~ \geq 0$ . Two types of mutations will be considered here:

$\left( \mathrm { M } _ { 1 } \right) ,$ An individual $x \in \mathbb { B } ^ { \ell }$ is mutated by drawing an index uniformly at random and inverting the associated entry in $x$ .   
$( \mathrm { M } _ { 2 }$ An individual $x \in \mathbb { B } ^ { \ell }$ is mutated by inverting each entry in $x$ independently with probability $p \in ( 0 , 1 )$ .

Originally, the results to be presented shortly have been derived for an evolutionary algorithm with population size $n = 1$ , which is usually termed the $( 1 + 1 )$ -EA. But it is easy to see that an EA with larger population size cannot be worse than the $( 1 + 1 )$ -EA with respect to the number of iterations. Moreover, the (positive) results are based on bounds on the expected first hitting time $\mathsf { E } [ T ]$ . The relationship between $T$ and the criterion of Definition 3.1 is established as follows:

Since $\mathsf { P } \{ F _ { s } ^ { * } = f ^ { * } \} = \mathsf { P } \{ T \leq s \}$ for every $s \geq 0$ , one may use the Markov inequality to obtain $\mathsf { P \{ }  { F }  _ { s } ^ { * }  { \neq } f ^ { * }  { \} = \mathsf { P \{ }  { T } } > s \textnormal { \scriptsize \{ } \le \mathsf { E } [ T ] / s $ . Assume it can be shown that $\mathsf { E } [ T ] \leq \mathrm { p o l y } _ { 1 } ( \ell )$ for every instance of a specific problem class $\mathcal { C }$ , where the bound $\mathrm { p o l y } _ { 1 } ( \ell )$ is explicitly known. If the stopping time is set to $s = c \mathrm { p o l y } _ { 1 } ( \ell )$ with $c \geq 1 + 1 / \mathrm { p o l y } _ { 2 } ( \ell )$ for an arbitrary polynomial $\mathrm { p o l y } _ { 2 } ( \ell )$ , then

$$
\mathsf { P } \{ F _ { s } ^ { * } \neq f ^ { * } \} \leq \frac { \mathsf { E } [ T ] } { s } = \frac { \mathsf { E } [ T ] } { c \mathrm { p o l y } _ { 1 } ( \ell ) } \leq \frac { \mathrm { p o l y } _ { 1 } ( \ell ) } { c \mathrm { p o l y } _ { 1 } ( \ell ) } = \frac { 1 } { c }
$$

and finally

$$
{ \sf P } \{ { \cal F } _ { s } ^ { * } = f ^ { * } \} \ge 1 - \frac { 1 } { c } \ge \frac { 1 } { \mathrm { p o l y } _ { 2 } ( \ell ) + 1 }
$$

for every instance of problem class $\mathcal { C }$ . Thus, the development of a polynomial upper bound for $\mathsf { E } [ T ]$ is sufficient for proving the efficiency of the evolutionary algorithm for a specific problem class.

# Definition 3.2.

A function $f : \mathbb { B } ^ { \ell } \to \mathbb { R }$ is said to be modular if $f ( x \wedge y ) + f ( x \vee y ) = f ( x ) + f ( y )$ for all $x , y \in \mathbb { B } ^ { \ell }$ .

It is easy to see that a function $f : \mathbb { B } ^ { \ell } \to \mathbb { R }$ is modular if and only if it is linear, i.e., $f ( x ) =$ $\begin{array} { r } { c _ { 0 } + \sum _ { i = 1 } ^ { \ell } c _ { i } x _ { i } } \end{array}$ with $c _ { i } \in \mathbb { R }$ . For example, the fitness function $f ( x ) = \ell - H ( x , x ^ { * } )$ based on the Hamming distance $H ( x , x ^ { * } )$ between some $x \in \mathbb { B } ^ { \ell }$ and a target pattern $x ^ { * } \in \mathbb { B } ^ { \ell }$ is linear and therefore modular. The special case with target vector $x ^ { * } = ( 1 , \ldots , 1 ) ^ { \prime } \in \mathbb { B } ^ { \ell }$ is known known as the 'counting ones problem.' Bäck [29] and independently Mühlenbein [30] made the first steps towards an upper bound on the expected first hitting time. While Bäck derived the complete finite Markov chain model for the $( 1 + 1 )$ EA with mutations of type $\left( \mathrm { M } _ { 2 } \right)$ , Mühlenbein developed an approximation for the expected first hitting time under simplifying assumptions. Later it was shown [13] that Mühlenbein's approach can be combined with Bäck's Markov chain model to achieve the upper bound $\mathsf { E } [ T ] \leq \ell \left( \log \ell + 1 \right) \exp ( 1 )$ under mutations of type $\left( \mathrm { { M } _ { 2 } } \right)$ with $p = 1 / \ell$ . In general, the results are as follows:

# Theorem 3.1.

Let the fitness function $f : \mathbb { B } ^ { \ell } \to \mathbb { R }$ be modular. If the evolutionary algorithm only uses mutation and elitist selection then

(a) $\mathsf { E } [ T ] \geq \ell \log \ell$ under $\left( \mathrm { M } _ { 1 } \right)$ .   
(b) $\mathsf { E } [ T ] = \Omega ( \ell \log \ell )$ under $\left( \mathrm { M } _ { 2 } \right)$ with $p = 1 / \ell$ .   
(c) $\mathsf { E } [ T ] \leq \ell \left( \log \ell + 1 \right)$ under $\left( \mathrm { M } _ { 1 } \right)$ .   
(d) $\mathsf { E } [ T ] = O ( \ell \log \ell )$ under $\left( \mathrm { { M } _ { 2 } } \right)$ with $p = 1 / \ell$ .

Proof: For part (b) and (d) see [31], for part (c) see [13, p. 98]. As for part (a), the basic argument from the proof of part (b) may be used: In the worst case, the algorithm starts at a point that is the binary complement of the optimum. Thus, every bit in the vector must be inverted at least once in order to reach the optimum by successive mutations.

Assume that $i ~ < ~ \ell$ different bits are already inverted. Then there are $\ell - i$ different bits that needs to be inverted. Since the index of the entry to be mutated is chosen uniformly at random, the probability that one of these $\ell - i$ bits will be inverted is $( \ell - i ) / \ell$ . The expected time that such an event occurs is just $\ell / \left( \ell - i \right)$ . As soon as this event has happened, $i + 1$ bits are inverted at least once and the argumentation repeats until all $\ell$ bits are inverted at least once. As a consequence, the expected number of mutations required to invert each bit at least once is given by

$$
\sum _ { i = 0 } ^ { \ell - 1 } { \frac { \ell } { \ell - i } } = \ell \sum _ { i = 1 } ^ { \ell } { \frac { 1 } { i } } \geq \ell \log \ell
$$

which proves part (a) of the theorem.

Thus, modular functions can be efficiently maximized by an evolutionary algorithm with both versions of mutations. The next class of pseudo-boolean functions strictly includes the class of modular functions.

# Definition 3.3.

A function $f : \mathbb { B } ^ { \ell } \to \mathbb { R }$ is said to be pseudo-modular if simultaneously

$$
\begin{array} { r l r } { \operatorname* { m i n } \{ f ( x ) , f ( y ) \} } & { \leq } & { \operatorname* { m a x } \{ f ( x \wedge y ) , f ( x \vee y ) \} } \\ { \operatorname* { m a x } \{ f ( x ) , f ( y ) \} } & { \geq } & { \operatorname* { m i n } \{ f ( x \wedge y ) , f ( x \vee y ) \} } \end{array}
$$

for all $x , y \in \mathbb { B } ^ { \ell }$ .

A non-modular instance of this class is the pseudo-boolean function

$$
f ( x ) = \sum _ { i = 1 } ^ { \ell } \prod _ { j = 1 } ^ { i } x _ { j } .
$$

It is easily seen [13, p. 114] that $f ( x \wedge y ) = \operatorname* { m i n } \left\{ f ( x ) , f ( y ) \right\}$ and $f ( x \vee y ) \geq \operatorname* { m a x } \{ f ( x ) , f ( y ) \}$ and there are pairs $( x , y )$ for which the inequality is strict. Thus,

$$
\operatorname* { m i n } \{ f ( x ) , f ( y ) \} = f ( x \wedge y ) \leq \operatorname* { m a x } \{ f ( x ) , f ( y ) \} \leq f ( x \vee y )
$$

and hence

$$
f ( x \wedge y ) = \operatorname* { m i n } \{ f ( x \wedge y ) , f ( x \vee y ) \} \leq \operatorname* { m a x } \{ f ( x \wedge y ) , f ( x \vee y ) \} = f ( x \vee y )
$$

which immediately implies the pseudo-modularity of function (1). The general problem has not been studied yet. But for this specific instance the following result is available.

# Proposition 3.1.

The expected first hitting time of the $( 1 + 1 )$ EA with fitness function (1) is bounded by

Proof: See [13], p. 105 for part (a) and p. 102 for part (b).

Hammer et al. [32] presented a hierarchy of classes of pseudo-boolean functions that strictly include each other. Therefore it may be useful to investigate the most general class of this hierarchy since the existence of a polynomial bound on the expected first hitting would imply that this bound is valid for all problem classes within this hierarchy. This top hierarchy class, which includes injective pseudo-modular functions, is characterized as follows.

# Definition 3.4.

An injective function $f : \mathbb { B } ^ { \ell } \to \mathbb { R }$ is called unimax if there is a unique locally maximizing point $x ^ { * } \in \mathbb { B } ^ { \ell }$ .

In general, an element $x ^ { * } \in \mathbb { B } ^ { \ell }$ is a locally maximizing point of a pseudo-boolean function $f : \mathbb { B } ^ { \ell } \to \mathbb { R }$ if $f ( x ^ { * } ) \geq f ( x )$ for all $x \in \mathbb { B } ^ { \ell }$ with Hamming distance $H ( x , x ^ { * } ) = 1$ [24, p. 135]. If the function $f ( \cdot )$ is injective then the inequality is actually always strict. This leads to subtle differences between the various definitions especially in the case of pseudo-boolean functions that are termed unimodal. Even worse, these subtle differences in the definitions may have a huge impact on the extent of the resulting class and its complexity. For example, Rudolph [33, 13] shows that the definition of unimodality used in [34, 35] includes the class of surjective boolean functions $f : \mathbb { B } ^ { \ell } \to \mathbb { B }$ for which the unique satisfying truth assignment is sought for. In contrast, the definitions given in [32, 33, 13] (albeit slightly different) ensure that for every $x \in \mathbb { B } ^ { \ell }$ there exists a path along adjacent vertices of the hypercube $\mathbb { B } ^ { \ell }$ with increasing function values leading to the global optimum. This property is also valid for unimax functions, even if they are not injective.

In any case, the problem of maximizing unimax functions is challenging task for it is known [36] that the decision version of this problem is in NP∩co-NP but it is unknown whether the the optimization problem can be solved in polynomial time or not. The difficulty associated with this class is caused by the existence of problem instances for which the only increasing path along the vertices of $\mathbb { B } ^ { \ell }$ may be exponentially long. Examples for such instances have been constructed in [32, 35]. Although the general case remains an open field of research there is a noteworthy result.

# Proposition 3.2.

Let the unimax fitness function $f : \mathbb { B } ^ { \ell } \to \mathbb { R }$ be the long "Root2"-path problem given in [35]. The expected first hitting time of the $( 1 + 1 )$ -EA can be bounded by

(a) $\mathsf { E } [ T ] \ge 3 \cdot \ell \cdot 2 ^ { ( \ell - 1 ) / 2 } - 2 \ell$ under $\left( \mathrm { M } _ { 1 } \right)$ , (b) $\mathsf { E } [ T ] \leq ( \ell ^ { 3 } - \ell ) \exp ( 1 ) / 2$ under $\left( \mathrm { { M } _ { 2 } } \right)$ with $p = 1 / \ell$ , if the EA starts at the bottom of the increasing path.

Proof: See [33] or [13], section 5.1.2.2.

Evidently, it is not hopeless to tackle unimax problems with evolutionary algorithms provided they employ mutations of type $\left( \mathrm { { M } _ { 2 } } \right)$ with $p = ~ 1 / \ell$ . The poor performance under mutations of type $\left( \mathrm { M } _ { 1 } \right)$ is due to the fact that the $( 1 + 1 )$ -EA only can move along the path of adjacent vertices, whereas type $\left( \mathrm { M } _ { 2 } \right)$ offer the chance of taking shortcuts along the path by inverting several bits simultaneously. In fact, since an exponentially long path must be folded several times to fit into the box $\mathbb { B } ^ { \ell }$ it may be speculated that the bit patterns of elements on the path are "relatively regular." This regularity might be exploited by a population of individuals that produce offspring by some kind of crossover/recombination. Horn et al. [35] provide empirical evidence that this conjecture is not too far-fetched.

Other hierarchies of classes of pseudo-boolean function are presented in Crama [37]. Here, the top hierarchy classes are known to be solvable in polynomial time. But already at a low level of these hierarchies there is a problem class that reveals some limitations of evolutionary algorithms.

# Definition 3.5.

A function $f : \mathbb { B } ^ { \ell } \to \mathbb { R }$ is called almost-positive if the coeficients of all nonlinear terms are non-negative.

An instance of this problem class is the pseudo-boolean function

$$
f ( x ) = \ell - \sum _ { i = 1 } ^ { \ell } x _ { i } + ( \ell + 1 ) \prod _ { i = 1 } ^ { \ell } x _ { i } .
$$

# Proposition 3.3.

The expected first hitting time of the $( 1 + 1 )$ -EA with fitness function (2) can be bounded by

(a) $\mathsf { E } [ T ] = \infty$ under $\begin{array} { r } { ( \mathrm { M } _ { 1 } ) } \end{array}$ ), unless being started at the optimum;   
(b) $\mathsf { E } [ T ] \geq \ell ^ { \ell }$ under $\left( \mathrm { { M } _ { 2 } } \right)$ with $p = 1 / \ell$ with worst starting point;   
(c) $\mathsf { E } [ T ] \geq [ ( \ell + 1 ) ^ { \ell } - 1 ] / 2 ^ { \ell }$ under $\left( \mathrm { M } _ { 2 } \right)$ with $p = 1 / \ell$ and random starting point.

Proof: See [13], pp. 116-117.

It should be noted that lower bounds on the expected first hitting time that are exponential in $\ell$ do generally not imply the absence of a bound $\mathsf { P } \{ F _ { s } ^ { * } = f ^ { * } \} \ge 1 / \mathrm { p o l y } ( \ell )$ for some stopping time $s = { \mathrm { p o l y } } ( \ell )$ . For this particular problem, however, this implication is unfortunately true.

Two points in conclusion: First, the behavior of evolutionary algorithms can be studied numerically provided that the transition matrix of the associated Markov chain is known [38, 39]. But this approach is manageable only for moderately large populations and problem dimensions because of the exponentially growing transition matrices and the inevitable rounding errors during the calculations. Moreover, this approach does not lead to theoretical results as they were presented here. The size of the state space and hence the transition matrices can be decreased considerably by a technique that is called lumping or grouping of states [2]. This technique in conjunction with a modification of the original Markov chain to a simpler Markov chain with either better or worse performance than the original one is extensively exploited in the proofs cited in this section.

Second, Vitányi [40] suggested to seek for evolutionary algorithms whose associated Markov chain is rapidly mixing, i.e., Markov chains that quickly approach their stationary distribution. Assume that the Markov chain reaches stationarity up to some small $\epsilon > 0$ in a number of iterations that is a polynomial in $\ell$ . If the probability of being in an optimal state is larger than $1 / \mathrm { p o l y } ( \ell )$ then the associated evolutionary algorithm is efficient in the sense of Definition

3.1. Although the toy problem dedicated to demonstrate this "paradigm" is not convincing (since pure random search works equally well for this problem) the idea itself deserves closer examination.

# 4. Beyond Finite State Space and Discrete Time

# 4.1. Infinite Population Size

Even if the search set $\chi$ is finite, the state space of the Markov chain becomes infinitely large as soon as the population is assumed to be infinitely large. Since the point of view from an infinitely large population implies that the de facto probabilistic trajectory of the evolutionary algorithm is appropriately described by the iteration of the expected one-step transitions, it is clear that these models may show a qualitative behavior that is completely different to the true behavior of an evolutionary algorithm with a finite population. Vitányi [40] offers a nice example of this fact. But under certain conditions, these models can lead to considerable insight into the dynamics of evolutionary algorithms [41].

The popularity of infinite population models with finite search space [5, 42, 43, 44, 45, 46, 47, 48, 49, 50] is probably due to the fact that an infinite population in conjunction with the smoothing effect of the expectation operator leads to a non-linear deterministic dynamical system with continuous state space. Although such dynamical systems are easier to characterize than those with probabilistic and discontinuous state transitions, much work has been devoted to the determination of these systems' fixed points and their stability [51, 52, 53, 54, 55, 56, 57].

The models taken from quantitative genetics [58, 59] essentially also assume infinite populations. And not surprisingly, infinite population models are also present in non-finite search spaces [60, 61].

# 4.2. Continuous Space and Discrete Time

In case of search space $\chi = \mathbb { R } ^ { \ell }$ , the convergence theory of stochastic optimization algorithms resembling a $( 1 + 1 ) { - } \mathrm { E A }$ dates back to the mid-60s [62] and was further developed in [63, 64, 65, 66, 67] under various assumptions. Interestingly, these authors did not use the theory of Markov processes for their proofs. Instead, their proofs are solely based on the Borel-Cantelli Lemma and its extensions. The same observation can be made in the proof of Born [68], who developed a population-based evolutionary algorithm with "genetic load" and proved its convergence to the optimum with probability one. The analysis of population-based algorithms relying on mutation and selection from a Markovian point of view was exhaustively treated in [69, chapter 5]. The extension of this theory in case of additional recombination was considered in [70, 71].

The modeling and analysis of non-elitist evolutionary algorithms in terms of supermartingales (another family of stochastic processes) was suggested in [72] and extensively used in [13]; even certain EAs for multi-objective optimization can be analyzed in this manner [73]. Although this approach only offers sufficient conditions for global convergence with probability one it may have a pleasant by-product: Under certain conditions one immediately obtains bounds on the average convergence velocity. Actually, it often suffices to determine the average convergence velocity. For, if the EA converges in mean with a certain minimum rate then the supermartingale convergence theorem implies convergence with probability one (see [13] for a more detailed discussion).

In the light of this observation, the much earlier established results regarding average convergence rates are graded up instantly. For example, Rechenberg [74] proved a linear average convergence rate towards the minimum of an $\ell .$ -dimensional equally scaled paraboloid for the $( 1 + 1 ) { - } \mathrm { E A }$ with normally distributed mutations. Schumer and Steiglitz [75] proved the same in case of mutations that are uniformly distributed on the surface of an l-dimensional hyperball. These results were generalized for strongly convex objective functions under spherically symmetric mutation distributions [76, 77, 78] and mutations distributions with independent marginals [79].

Linear convergence rates can also be shown for EAs with a single parents but multiple offspring [80]. This result was later successively generalized in various directions [81, 82, 83, 84] accompanied by a steady simplification of the mathematical apparatus. The convergence rate of evolutionary algorithms with multiple parents and offspring were investigated by Rechenberg [85], Beyer [86, 87], and Rudolph [13] under various variation operators (including recombination).

So far, the publications regarding average convergence rates tacitly presupposed that the EA is able to determine the Euclidean length of the gradient at arbitrary positions of the search space in order to adjust the mutation distributions appropriately—an assumption that is usually not justified in practice. In real world evolutionary algorithms this task is accomplished by a mechanism termed 'self-adaptation' (see e.g. [88]), but, despite first steps in this direction [89], a mathematically rigorous proof of this property is still pending.

# 4.3. Continuous Space and Time

Evolutionary algorithms with continuous time may be interpreted as follows: The period between the completion of two successive reproduction cycles is interpolated. In this case, the truly discrete time process is embedded into continuous time. Then, combining the theory of analysis and probability, one shows that a convergent subsequence may be extracted and identifies the limit of the sequence as a solution of an ordinary differential equation. This general approach was developed by Ljung [90] and subsequently extended by many others. The monograph by Benveniste et al. [91] offers a detailed account on this method. So-called stochastic approximation algorithms have been extensively studied in this manner. Yin et al. [92, 93] showed that some versions of evolutionary algorithms may be formulated as stochastic approximation algorithms so that only few modifications to the existing theory for stochastic approximations algorithms led to various conditions for global convergence with probability one or weaker modes.

Ebeling and various coauthors [94, 95, 96, 97, 98] took a more abstract point of view. They specified continuous-time models via differential equations that should behave similar to existing evolutionary algorithms. For example, the Fisher-Eigen equation

$$
\frac { \partial } { \partial t } P ( x , t ) = ( f ( x ) - < f > ) P ( x , t ) + D \Delta P ( x , t )
$$

where $\mathit { D } > 0$ is a diffusion constant, $\Delta$ the Laplace operator, and

$$
< f > ( t ) = { \frac { \int f ( x ) ~ P ( x , t ) ~ d x } { \int P ( x , t ) ~ d x } }
$$

the average of the population's fitness at generation $t ~ \geq 0$ , models proportional selection by the first term in equation (3) and mutations via a Gaussian diffusion process by the second term. Under certain conditions on the fitness function $f ( \cdot )$ the solution of equation (3) permits the determination of the limit ${ \bf \Phi } ( t  \infty$ ) of the population's distribution $P ( x , t )$ at time $t \geq 0$ . A more thorough presentation of this approach was given by ABelmeier [99]. Although this approach principally presupposes an infinitely large population, the dynamics of $P ( x , t )$ often characterizes the dynamics of the discrete time EA surprisingly well.

# 5. Concluding Remarks

This survey is an attempt to summarize finite Markov chains results in the field of evolutionary computation. The main focus was devoted to the limit and finite time behavior of evolutionary algorithms. But there are of course other theoretical questions that might be of interest. Moreover, there are also other techniques and tools that have been applied to examining specific properties of evolutionary algorithms. Apart from Markov chains one can find methods like schema analysis, dimensional analysis, orthogonal functions analysis, as well as approaches via quantitative genetics, statistical physics, and quadratical dynamical systems (see [100] for a brief introduction and key references).

But despite these enhanced activities during the last decade we currently have not more than a first layer of a theoretical foundation of evolutionary computation. Needless to say, there are many challenges that must be encountered in future—but their coverage would not only be a contribution to the field of evolutionary computation but also to the more general field of the analysis of complex systems.

# Acknowledgment

This survey was made in the course of the Collaborative Research Center "Design and Management of Complex Technical Processes and Systems by Means of Computational Intelligence Methods" (SFB 531). Financial support by the Deutsche Forschungsgemeinschaft (DFG) is gratefully acknowledged.

# Список литературы

[1] E. Lukacs. Stochastic Convergence. Academic Press, New York, 2nd edition, 1975.   
[2] M. Iosifescu. Finite Markov Processes and Their Applications. Wiley, Chichester, 1980.   
[3] E. Seneta. Non-negative Matrices and Markov Chains. Springer, New York, 2nd edition, 1981.   
[4] T. E. Davis. Toward an extrapolation of the simulated annealing convergence theory onto the simple genetic algorithm. PhD thesis, University of Florida, Gainesville, 1991.   
[5] M. D. Vose and G. E. Liepins. Punctuated equilibria in genetic search. Complex Systems, 5(1):3144, 1991.   
[6] A. E. Nix and M. D. Vose. Modeling genetic algorithms with Markov chains. Annals of Mathematics and Artificial Intelligence, 5:7988, 1992.   
[7] A. E. Eiben, E. H. L. Aarts, and K. M. van Hee. Global convergence of genetic algorithms: A markov chain analysis. In H.-P. Schwefel and R. Männer, editors, Parallel Problem Solving from Nature, pages 4-12. Springer, Berlin and Heidelberg, 1991.   
[8] E. H. L. Aarts, A. E. Eiben, and K. H. van Hee. A general theory of genetic algorithms. Technical Report 89/08, Eindhoven University of Technology, Department of Computer Science, 1989.   
[9] S. Arunkumar and T. Chockalingam. Genetic search algorithms and their randomized operators. Computers and Mathematics with Applications, 25(5):91100, 1993.   
[10] D. B. Fogel. Asymptotic convergence properties of genetic algorithms and evolutionary programming: Analysis and experiments. Cybernetics and Systems, 25(3):389-407, 1994.   
[11] G. Rudolph. Convergence properties of canonical genetic algorithms. IEEE Transactions on Neural Networks, 5(1):96-101, 1994.   
[12] J. Suzuki. A markov chain analysis on simple genetic algorithms. IEEE Transactions on Systems, Man, and Cybernetics, 25(4):655659, 1995.   
[13] G. Rudolph. Convergence Properties of Evolutionary Algorithms. Kova, Hamburg, 1997.   
[14] A. Agapie. Genetic algorithms: Minimal conditions for convergence. In J. K. Hao, E. Lutton, E. Ronald, M. Schoenauer, and D. Snyers, editors, Artificial Evolution: Third European Conference; selected papers / AE '97, pages 183-193. Springer, Berlin, 1998.   
[15] I. K. Evans. Enhancing recombination with the complementary surrogate genetic algorithm. In Proceedings of the 4th IEEE International Conference on Evolutionary Computation (ICEC'97), pages 97-102. IEEE Press, Piscataway (NJ), 1997.   
[16] G. Rudolph. Evolutionary search for minimal elements in partially ordered finite sets. In V. W. Porto, N. Saravanan, D. Waagen, and A. E. Eiben, editors, Evolutionary Programming VII, Proceedings of the 7th Annual Conference on Evolutionary Programming, pages 345353. Springer, Berlin, 1998.   
[17] T. E. Davis and J. Principe. A markov chain framework for the simple genetic algorithm. Evolutionary Computation, 1(3):269288, 1993.   
[18] S. W. Mahfoud and D. E. Goldberg. Parallel recombinative simulated annealing: A genetic algorithm. Parallel Computinq, 21(1):128, 1995.   
[19] R. Cerf. The dynamics of mutation-selection algorithms with large population sizes. Annales de l'Institut Henri Poincaré, Probabilités et Statistiques, 32(4):455-508, 1996.   
[20] R. Cerf. A new genetic algorithm. Annals of Applied Probability, 6(3):778-817, 1996.   
[21] J. Suzuki. A further result on the markov chain model of genetic algorithm and its application to a simulated annealing-like strategy. IEEE Transactions on Systems, Man, and Cybernetics—Part B, 28(1):95-102, 1998.   
[22] J. A. Lozano, P. Larrañaga, M. Graña, and F. X. Albizuri. Genetic algorithms: Bridging the convergence gap. Theoretical Computer Science, 214, 1999 (in press).   
[23] J. He and K. Kang. On the convergence rates of genetic algorithms. Theoretical Computer Science, 214, 1999 (in press).   
[24] P. L. Hammer and S. Rudeanu. Boolean Methods in Operations Research and Related Areas. Springer, Berlin and Heidelberg, 1968.   
[25] M. R. Garey and D. S. Johnson. Computers and Intractability: A Guide to the Theory of NP-Completeness. Freeman, New York, 1979.   
[26] R. Motwani and P. Raghavan. Randomized Algorithms. Cambridge University Press, New York (NY), 1995.   
[27] M. Hulin. An optimal stop criterion for genetic algorithms: A Bayesian approach. In T. Bäck, editor, Proceedings of the 7th International Conference on Genetic Algorithms (ICGA '97), pages 135-142. Morgan Kaufmann, San Francisco (CA), 1997.   
[28] H. Aytug and G. J. Koehler. Stopping criteria for finite length genetic algorithms. INFORMS Journal on Computing, 8(2):183191, 1996.   
[29] T. Bäck. The interaction of mutation rate, selection, and self-adaptation within a genetic algorithm. In R. Männer and B. Manderick, editors, Parallel Problem Solving from Nature, 2, pages 85-94. North Holland, Amsterdam, 1992.   
[30] H. Mühlenbein. How genetic algorithms really work I: Mutation and hillclimbing. In R. Männer and B. Manderick, editors, Parallel Problem Solving from Nature, 2, pages 1525. North Holland, Amsterdam, 1992.   
[31] S. Droste, T. Jansen, and I. Wegener. A rigorous complexity analysis of the $( 1 + 1 )$ evolution strategy for separable functions with boolean inputs. In Proceedings of the 5th IEEE International Conference on Evolutionary Computation (ICEC'98), pages 499-504. IEEE Press, Piscataway (NJ), 1998.   
[32] P. L. Hammer, B. Simeone, T. M. Liebling, and D. de Werra. From linear separability to unimodality: a hierachy of pseudo-boolean functions. SIAM Journal of Discrete Mathematics, 1(2):174184, 1988.   
[33] G. Rudolph. How mutation and selection solve long path-problems in polynomial expected time. Evolutionary Computation, 4(2):195205, 1996.   
[34] A. N. Antamoshkin, V. N. Saraev, and E. S. Semenkin. Optimization of unimodal monotone pseudoboolean functions. Kybernetika, 26(5):432441, 1990.   
[35] J. Horn, D. E. Goldberg, and K. Deb. Long path problems. In Y. Davidor, H.-P. Schwefel, and R. Männer, editors, Parallel Problem Solving from Nature, 3, pages 149158.Springer, Berlin and Heidelberg, 1994.   
[36] D.S. Johnson, C. H. Papadimitriou, and M. Yannakakis. How easy is local search? Journal of Computer and System Sciences, 37(1):79100, 1988.   
[37] Y. Crama. Recognition problems for special classes of polynomials in 01 variables. Mathematical Programming, 44:139155, 1989.   
[38] K. A. De Jong, W. M. Spears, and D. F. Gordon. Using markov chains to analyze GAFOs. In L. D. Whitley and M. D. Vose, editors, Foundations on Genetic Algorithms, 3, pages 115137. Morgan Kaufmann, San Fransisco (CA), 1995.   
[39] W. M. Spears and K. A. De Jong. Analyzing GAs using markov chain models with semantically ordered and lumped states. In R. K. Belew and M. D. Vose, editors, Foundations of Genetic Algorithms, 4, pages 85-100. Morgan Kaufmann, San Francisco (CA), 1997.   
[40] P. Vitányi. Genetic fitness optimization using rapidly mixing Markov chains. In S. Arikawa and A. K. Sharma, editors, Proceedings of the 7th International Workshop on Algorithmic Learning Theory (ALT '96), pages 67-82. Springer, Berlin, 1996.   
[41] E. van Nimwegen, J. P. Crutchfield, and M. Mitchell. Statistical dynamics of the royal road genetic algorithm. Theoretical Computer Science, 214, 1999 (in press).   
[42] Y. Rabinovich and A. Wigderson. An analysis of a simple genetic algorithm. In R. K. Belew and L. B. Booker, editors, Proceedings of the Fourth Conference on Genetic Algorithms, pages 215221. Morgan Kaufmann, San Mateo, 1991.   
[43] M. Srinivas and L. M. Patnaik. Binomially distributed populations for modelling GAs. In S. Forrest, editor, Proceedings of the Fifth International Conference on Genetic Algorithms, pages 138145. Morgan Kaufmann, San Mateo (CA), 1993.   
[44] U. K. Chakraborty and D.G. Dastidar. Using reliability analysis to estimate the number of generations to convergence in genetic algorithms. Information Processing Letters, 46:199- 209, 1993.   
[45] H. Dawid. A markov chain analysis of genetic algorithms with a state dependent fitness function. Complex Systems, 8(6):407-417, 1994.   
[46] A. Prügel-Bennett and J. L. Shapiro. Analysis of genetic algorithms using statistical mechanics. Physical Review Letters, 72(9):1305-1309, 1994.   
[47] B. Goertzel. A convergence theorem for the simple GA with population size tending to infinity. In Proceedings of the IEEE 2nd International Conference on Evolutionary Computation, Vol. 1, pages 7479. IEEE Press, 1995.   
[48] S. Voget. A central limit theorem for the population process of genetic algorithms. Complex Systems, 9(4):267285, 1995.   
[49] S. Voget. Theoretical analysis of genetic algorithms with infinite population size. Complex Systems, 10(3):167183, 1996.   
[50] J. Shapiro and A. Prügel-Bennett. Genetic algorithm dynamics in a two-well potential. In R. K. Belew and M. D. Vose, editors, Foundations of Genetic Algorithms, 4, pages 101-116. Morgan Kaufmann, San Francisco (CA), 1997.   
[51] M. D. Vose and A. H. Wright. Stability of vertex fixed points and applications. In L. D. Whitley and M. D. Vose, editors, Foundations on Genetic Algorithms, 3, pages 103-113. Morgan Kaufmann, San Fransisco (CA), 1995.   
[52] M. D. Vose and A. H. Wright. Simple genetic algorithms with linear fitness. Evolutionary Computation, 2(4):347368, 1994.   
[53] A. H. Wright and Vose D. Finiteness of the fixed point set for the simple genetic algorithm. Evolutionary Computation, 3(3):299309, 1995.   
[54] G. J. Koehler. A proof of the Vose-Liepins conjecture. Annals of Mathematics and Artificial Intelligence, 10(4):409422, 1994.   
[55] S. Bhattacharyya and G. J. Koehler. An analysis of non-binary genetic algorithms with cardinality $2 ^ { v }$ . Complex Systems, 8(4):227256, 1994.   
[56] G. J. Koehler. Diagonalizing the simple GA mixing matrix. In R. K. Belew and M. D. Vose, editors, Foundations of Genetic Algorithms, 4, pages 5-51. Morgan Kaufmann, San Francisco (CA), 1997.   
[57] A. H. Wright and G. Bidwell. A search for counterexamples to two conjectures on the simple genetic algorithm. In R. K. Belew and M. D. Vose, editors, Foundations of Genetic Algorithms, 4, pages 73-84. Morgan Kaufmann, San Francisco (CA), 1997.   
[58] H. Mühlenbein and D. Schlierkamp-Voosen. Predictive models for the breeder genetic algorithm I: Continuous parameter optimization. Evolutionary Computation, 1(1):2549, 1993.   
[59] H. Mühlenbein and D. Schlierkamp-Voosen. The science of breeding and its application to the breeder genetic algorithm (BGA). Evolutionary Computation, 1(4):335-360, 1993.   
[60] S. M. Ermakov and A. A. Zhiglyavskij. On random search for a global extremum. Theory of Probability and its Applications, 28(1):136141, 1983.   
[61] X. Qi and F. Palmieri. Theoretical analysis of evolutionary algorithms with infinite population size in continuous space, part I: basic properties. IEEE Transactions on Neural Networks, 5(1):102119, 1994.   
[62] M. Driml and O. Hans. On a randomized optimization procedure. In J. Kozenik, editor, Transactions of the 4th Prague Conference on Information Theory, Statistical Decision Functions and Random Processes (held at Prague 1965), pages 273-276. Czechoslovak Academy of Sciences, Prague, 1967.   
[63] L. P. Devroye. On the convergence of statistical search. IEEE Transactions on Systems, Man, and Cybernetics, 6(1):4656, 1976.   
[64] U. G. Oppel and M. Hohenbichler. Auf der Zufallssuche basierende Evolutions-prozesse. In B. Schneider and U. Ranft, editors, Simulationsmethoden in der Medizin und Biologie, pages 130155. Springer, Berlin, 1978.   
[65] K. Marti. On accelerations of the convergence in random search methods. Methods of Operations Research, 37:391406, 1980.   
[66] F. J. Solis and R. J.-B. Wets. Minimization by random search techniques. Mathematics of Operations Research, 6:1930, 1981.   
[67] J. Pintér. Convergence properties of stochastic optimization procedures. Mathematische Operationsforschung und Statistik, Series Optimization, 15:405-427, 1984.   
[68] J. Born. Evolutionsstrategien zur numerischen Lösung von Adaptationsaufgaben. Dissertation A, Humboldt-Universität, Berlin, 1978.   
[69] A. A. Zhigljavsky. Theory of global random search. Kluwer, AA Dordrecht, The Netherlands, 1991.   
[70] C. C. Peck and A. P. Dhawan. Genetic algorithms as global random search methods: An alternative perspective. Evolutionary Computation, 3(1):39-80, 1995.   
[71] G. Rudolph. Convergence of evolutionary algorithms in general search spaces. In Proceedings of the Third IEEE Conference on Evolutionary Computation, pages 50-54. IEEE Press, Piscataway (NJ), 1996.   
[72] G. Rudolph. Convergence of non-elitist strategies. In Proceedings of the First IEEE Conference on Evolutionary Computation, Vol. 1, pages 63-66. IEEE Press, Piscataway (NJ), 1994.   
[73] G. Rudolph. On a multi-objective evolutionary algorithm and its convergence to the pareto set. In Proceedings of the 1998 IEEE International Conference on Evolutionary Computation, pages 511-516. IEEE Press, Piscataway (NJ), 1998.   
[74] I. Rechenberg. Evolutionsstrategie: Optimierung technischer Systeme nach Prinzipien der biologischen Evolution. Frommann-Holzboog Verlag, Stuttgart, 1973.   
[75] M. A. Schumer and K. Steiglitz. Adaptive step size random search. IEEE Transactions on Automatic Control, 13:270276, 1968.   
[76] G. Rappl. Konvergenzraten von Random Search Verfahren zur globalen Optimierung. Dissertation, Hochschule der Bundeswehr München, Germany, 1984.   
[77] G. Rappl. On linear convergence of a class of random search algorithms. Zeitschrift für angewandte Mathematik und Mechanik (ZAMM), 69(1):37-45, 1989.   
[78] G. Rudolph. Local convergence rates of simple evolutionary algorithms with cauchy mutations. IEEE Transactions on Evolutionary Computation, 1(4):249-258, 1998.   
[79] G. Rudolph. Convergence rates of simple evolutionary algorithms under factorizing mutation distributions. In J. K. Hao, E. Lutton, E. Ronald, M. Schoenauer, and D. Snyers, editors, Artificial Evolution: Third European Conference; selected papers / AE '97, pages 275285. Springer, Berlin, 1998.   
[80] H.-P.Schwefel. Evolutionsstrategie und numerische Optimierung. Dissertation, Technische Universität Berlin, 1975.   
[81] A. Scheel. Beitrag zur Theorie der Evolutionsstrategie. Dissertation, TU Berlin, Berlin, 1985.   
[82] T. Bäck, G. Rudolph, and H.-P. Schwefel. Evolutionary programming and evolution strategies: Similarities and differences. In D. B. Fogel and W. Atmar, editors, Proceedings of the 2nd Annual Conference on Evolutionary Programming, pages 11-22. Evolutionary Programming Society, La Jolla (CA), 1993.   
[83] H.-G. Beyer. Toward a theory of evolution strategies: Some asymptotical results from the $( 1 \div \lambda ) -$ theory. Evolutionary Computation, 1(2):165-188, 1993.   
[84] G. Rudolph. Convergence rates of evolutionary algorithms for a class of convex objective functions. Control and Cybernetics, 26(3):375390, 1997.   
[85] I. Rechenberg. Evolutionsstrategie '94. Frommann-Holzboog Verlag, Stuttgart, 1994.   
[86] H.-G. Beyer. Toward a theory of evolution strategies: The $( \mu , \lambda )$ theory. Evolutionary Computation, 2(4):381407, 1994.   
[87] H.-G. Beyer. Toward a theory of evolution strategies: On the benefits of sex — the $( \mu / \mu , \lambda )$ theory. Evolutionary Computation, 3(1):81-111, 1995.   
[88] T. Bäck and H.-P. Schwefel. An overview of evolutionary algorithms for parameter optimization. Evolutionary Computation, 1(1):1-23, 1993.   
[89] H.-G. Beyer. Toward a theory of evolution strategies: Self-adaptation. Evolutionary Computation, 3(3):311347, 1995.   
[90] L. Ljung. Analysis of recursive stochastic algorithms. IEEE Transactions on Automatic Control, 22:551575, 1977.   
[91] A. Benveniste, M. Métivier, and P. Priouret. Adaptive Algorithms and Stochastic Approximations. Springer, Berlin and Heidelberg, 1990.   
[92] G. Yin, G. Rudolph, and H.-P. Schwefel. Establishing connections between evolutionary algorithms and stochastic approximation. Informatica, 6(1):93-116, 1995.   
[93] G. Yin, G. Rudolph, and H.-P. Schwefel. Analyzing $( 1 , \lambda )$ evolution strategy via stochastic approximation methods. Evolutionary Computation, 3(4):473489, 1995.   
[94] R. Feistel and W. Ebeling. Models of Darwinian processes and evolutionary principles. BioSystems, 15:291299, 1982.   
[95] W. Ebeling and A. Engel. Models of evolutionary systems and their application to optimization problems. Systems Analysis, Modelling, Simulation, 3(5):377-385, 1986.   
[96] T. ABelmeier, W. Ebeling, and H. Rosé. Analytical and numerical investigations of evolutionary algorithms in continuous space. In H.-M. Voigt, W. Ebeling, I. Rechenberg, and H.-P. Schwefel, editors, Parallel Problem Solving From Nature — PPSN IV, pages 112121. Springer, Berlin, 1996.   
[97] T. ABelmeyer and W. Ebeling. Unified description of evolutionary strategies over continous parameter spaces. BioSystems, 41(3):167-178, 1997.   
[98] T. ABelmeier, W. Ebeling, and H. Rosé. Evolutionary strategies of optimization. Physical Review E, 56(1):11711180, 1997.   
[99] T. ABelmeier. Schrödinger-Operatoren und Evolutionäre Strategien. Dissertation, Humboldt-Universität zu Berlin, Institut für Physik, 1997.   
100] A. E. Eiben and G. Rudolph. Theory of evolutionary algorithms: A birds eye view. Theoretical Computer Science, 214, 1999 (in press).