# Drift Analysis and Average Time Complexity of Evolutionary Algorithms \*

Jun He Department of Computer Science Northern Jiaotong University Beijing 100044, P. R. China

Xin Yaot School of Computer Science The University of Birmingham Birmingham B15 2TT, U.K. Email: x.yao@cs.bham.ac.uk

December 21, 2000

# Abstract

The computational time complexity is an important topic in the theory of evolutionary algorithms (EAs). This paper reports some new results on the average time complexity of EAs. Based on drift analysis, some useful drift conditions for deriving the time complexity of EAs are studied, including conditions under which an EA will take no more than polynomial time (in problem size) to solve a problem and conditions under which an EA will take at least exponential time (in problem size) to solve a problem. The paper first presents the general results, and then uses several problems as examples to illustrate how these general results can be applied to concrete problems in analyzing the average time complexity of EAs. While previous work only considered $( 1 + 1 )$ EAs without any crossover, the EAs considered in this paper are fairly general, which use a finite population, crossover, mutation, and selection.

# Keywords

Evolutionary algorithms, time complexity, random sequences, drift analysis, stochastic inequalities.

# 1 Introduction

Evolutionary algorithms (EAs) are a powerful class of adaptive search algorithms [1, 4, 5]. They have been used to solve many combinatorial problems with success in recent years. However, theories on explaining why and how EAs work are still relatively few in spite of recent efforts [6]. The computational time complexity of EAs is largely unknown, except for a few simple cases [7, 8, 9, 10, 11]. Ambati et al. [8] and Fogel [9] estimated the computational time complexity of their EAs on the traveling salesman problem. No theoretical results were given. Rudolph [10] proved that $( 1 + 1 )$ EAs with mutation probability $p _ { m } = 1 / n$ , where $n$ is the number of bits in a binary string (i.e., individual) and $p _ { m }$ is the mutation probability, converge in average time $O ( n \log n )$ for the ONE-MAX problem. Droste et al. [11] carried out a rigorous complexity analysis of $( 1 + 1 )$ EAs for linear functions with Boolean inputs. However, all of these results were based on EAs with a population size of 1 and without any crossover operators. Nimwegen et al. [12, 13] developed a theory which predicts the total number of fitness function evaluations needed to reach a global optimum by epochal dynamics as a function of mutation rate and population size. However, no relationship to the problem size was studied. He et al. [14, 15] showed that genetic algorithms (GAs) may take exponential average time to solve some deceptive problems.

This paper presents a more general theory about the average time complexity of EAs. The motivation of this study is to establish a general theory for a class of EAs, rather than a particular EA. The theory can then be used to derive specific complexity results for different EAs on different problems. The theory has been developed using drift analysis [16, 17] — a very useful technique in analyzing random sequences. It can be used to estimate the first hitting time by estimating the drift of a random sequence. To our best knowledge, this is the first attempt that drift analysis is introduced into the theoretical study of evolutionary computation. One of the major advantages of using drift analysis is that it is often easier to estimate the drift than to estimate the first hitting time directly. The techniques of drift analysis can also be applied to random sequences which are not Markovian [16].

The basic idea of this paper is as follows. We first model the evolution of an EA population as a random sequence, e.g., a Markov chain. A population of multiple individuals will be considered. Both crossover and mutation are included in the EA. Then we analyzed the drift of this sequence to and from the optimal solution (assuming we are solving an optimization problem). Various bounds on the first hitting time will be derived under different drift conditions. Some drift conditions cause the random sequence to drift away from the optimal solution, while other drift conditions enable the sequence to drift towards the optimal solution. We wil study the conditions which are used to determine the time complexity of an EA to solve a problem, whether in polynomial time (in problem size) or in exponential time.

To illustrate the application of the above general theory, we will apply the theoretical results to several well-known problems, including a classical combinatorial optimization problem — the subset sum problem. It is shown in this paper that a certain family of subset sum problems can be solved by an EA within polynomial time, while other families of subset sum problems will need at least exponential time to solve. Although the EAs used in our study do not include all possible variations of EAs, they do represent a fairly large class of EAs which have multiple individuals and use both crossover and mutation.

The rest of this paper is organized as follows: Section 2 introduces briefly EAs and drift analysis. Section 3 studies the conditions under which EAs can solve a problem within polynomial time on average. A general theorem is first presented. Then examples, including the subset sum problem, are studied to show the application of the theorem. Section 4 studies the conditions under which EAs need at least exponential computation time to solve a problem. Both a general theorem and an application of the theorem are given. Section 5 discusses some weaker drift conditions for the subset sum problem. Finally, Section 6 concludes with a brief summary of the paper and some future work.

# 2 Evolutionary Algorithms and Drift Analysis

# 2.1 Evolutionary Algorithms

The combinatorial optimization problem considered in this paper can be described as follows: Given a finite state space $S$ and a function $f ( x ) , x \in S$ , find

$$
\operatorname* { m a x } \{ f ( x ) ; x \in S \} .
$$

Assume $x ^ { * }$ is one state with the maximum function value, and $f _ { \mathrm { m a x } } = f ( x ^ { * } )$ .

The EA for solving the combinatorial optimization problem can be described as follows:

1. Initialization: generate, either randomly or heuristically, an initial population of $2 N$ individuals, denoted by ${ \xi } _ { 0 } = ( x _ { 1 } , \cdots , x _ { 2 N } )$ , and let $k \gets 0$ , where $N > 0$ is an integer. For any population $\xi _ { k }$ , define $f ( \xi _ { k } ) = \operatorname* { m a x } \{ f ( x _ { i } ) ; x _ { i } \in \xi _ { k } \}$ .

2. Generation: generate a new (intermediate) population by crossover and mutation (or any other operators for generating offspring), and denote it as $\xi _ { k + 1 / 2 }$ .

3. Selection: select and reproduce $2 N$ individuals from populations $\xi _ { k + 1 / 2 }$ and $\xi _ { k }$ , and obtain another (new intermediate) population $\xi _ { k + S }$ .

4. If $f ( \xi _ { k + S } ) = f _ { \mathrm { m a x } }$ , then stop; otherwise let $\xi _ { k + 1 } = \xi _ { k + S }$ and $k \gets k + 1$ , and go to step 2.

Obviously the above description includes a wide range of EAs using crossover, mutation and selection. The description does not set any restrictions on the type of crossover, mutation or selection schemes used. It includes EAs which use crossover or mutation alone. The EA framework given above is closer to evolution strategies [2] and evolutionary programming [3] than to GAs [4] in the sense that selection is applied after crossover and/or mutation. However, the main results given in this paper, i.e., Theorems 1 and 10 are independent of any such implementation details. In fact, they hold for virtually any stochastic search algorithms.

# 2.2 Drift Analysis

Assume $x ^ { * }$ is an optimal point, and let $d ( x , x ^ { * } )$ be the distance between a point $x$ and $x ^ { * }$ . If there are more than one optimal point (that is, a set $S ^ { * }$ ), we use $d ( x , S ^ { * } ) = \operatorname* { m i n } \{ d ( x , x ^ { * } ) : x ^ { * } \in S ^ { * } \}$ as the distance between individual $x$ and the optimal set $S ^ { * }$ . In short we denote the distance by $d ( x )$ . Usually $d ( x )$ satisfies $d ( x ^ { * } ) = 0$ and $d ( x ) > 0$ for any $x \notin S ^ { * }$ . However, in some parts of this paper, we will consider a pseudo-distance $d ( x )$ which allows $d ( x ) = 0$ for some $x \notin S ^ { * }$ .

Given a population $X = \{ x _ { 1 } , \cdots , x _ { 2 N } \}$ , let

$$
d ( X ) = \operatorname* { m i n } \{ d ( x ) : x \in X \} ,
$$

which is used to measure the distance of the population to the optimal solution.

The sequence $\{ d ( \xi _ { k } ) ; k = 0 , 1 , 2 , \cdot \cdot \cdot \}$ generated by the EA is a random sequence. The sequence can be modeled by a homogeneous Markov chain if no self-adaptation is used [18].

The drift of the random sequence $\{ d ( \xi _ { k } ) , k = 0 , 1 , \cdot \cdot \cdot \}$ at time $k$ is defined by

$$
\Delta ( d ( \xi _ { k } ) ) = d ( \xi _ { k + 1 } ) - d ( \xi _ { k } ) .
$$

Define the stopping time of an EA as $\tau = \operatorname* { m i n } \{ k ; d ( \xi _ { k } ) = 0 \}$ , which is the first hitting time on the optimal solution. The task now is to investigate the relationship between the expect first hitting time $\tau$ and the problem size $n$ . In this paper, we focus on the following question: under what conditions of the drift $\Delta ( d ( \xi _ { k } ) )$ can we estimate the expect first hitting time $E [ \tau ]$ ? In particular, we study the conditions under which an EA is guaranteed to find the optimal solution in polynomial time on average and conditions under which an EA takes at least exponential time on average to find the optimal solution.

The idea behind drift analysis is quite straightforward. It can be explained (by sacrificing mathematical rigor) using a deterministic algorithm as an example. Assume the distance between the starting solution and the optimal solution is $d$ , and a deterministic algorithm is used to solve an optimization problem. If the drift towards the optimal solution is greater than $\Delta$ at each time step (i.e., iteration), we would need at most $d / \Delta$ time steps to find the optimal solution. Hence the key issue here is to estimate $\Delta$ . Sasaki and Hajek [19] have successfully used this method to estimate the time complexity of simulated annealing for the maximum matching problem.

# 3 Conditions for Polynomial Average Computation Time

# 3.1 Drift Conditions

In this section, we study under which drift conditions an EA can solve an optimization problem in polynomial average time.

Condition 1 There exists a polynomial of problem size $n$ , $h _ { 0 } ( n ) > 0$ , such that

$$
d ( X ) \leq h _ { 0 } ( n )
$$

for any given population $X$ .

This condition says that the distance from any population to the optimal solution is bounded by a polynomial function of the problem size.

Condition 2 At any time $k \geq 0$ , if population $\xi _ { k }$ satisfies $d ( \xi _ { k } ) > 0$ , then there exists a polynomial of problem size $n$ , $h _ { 1 } ( n ) > 0$ , such that

$$
E [ d ( \xi _ { k } ) - d ( \xi _ { k + 1 } ) \mid d ( \xi _ { k } ) > 0 ] \geq \frac { 1 } { h _ { 1 } ( n ) } .
$$

This condition indicates that the drift of the random sequence $\{ d ( \xi _ { k } ) ; k = 0 , 1 , 2 , \cdot \cdot \cdot \}$ toward the optimal solution is always positive and bounded by an inverse polynomial.

Now we give the following main result in the section.

Theorem 1 If $\{ d ( \xi _ { k } ) ; k = 0 , 1 , 2 , \cdot \cdot \cdot \}$ satisfies Conditions 1 and $\boldsymbol { \mathcal { Z } }$ , then starting from any initial population $X$ with $d ( X ) > 0$ ,

$$
E [ \tau \mid d ( \xi _ { 0 } ) > 0 ] \leq h ( n ) ,
$$

where $h ( n )$ is a polynomial of problem size $n$ .

Proof: According to Condition 2, we know that $\{ d ( \xi _ { k } ) ; k = 0 , 1 , 2 , \cdot \cdot \cdot \}$ in fact is a super-martingale [20]. Since $0 \leq d ( \xi _ { k } ) \leq h _ { 0 } ( n )$ , it converges almost everywhere [20], and

$$
\operatorname* { l i m } _ { k \to \infty } { \cal E } [ d ( \xi _ { k } ) \mid d ( \xi _ { 0 } ) > 0 ] = 0 .
$$

According to the definition of stopping time $\tau$ , we have $d ( \xi _ { \tau } ) = 0$ .Hence,

$$
E [ d ( \xi _ { \tau } ) \mid d ( \xi _ { 0 } ) > 0 ] = 0 .
$$

For any time $k \geq 1$ ,

$$
E [ d ( \xi _ { k } ) \mid d ( \xi _ { 0 } ) > 0 ] = E [ E [ d ( \xi _ { k - 1 } ) + \Delta ( d ( \xi _ { k - 1 } ) ) \mid \xi _ { k - 1 } ] \mid d ( \xi _ { 0 } ) > 0 ] .
$$

According to Condition 2, we have for $k - 1 < \tau$ ,

$$
E [ d ( \xi _ { k - 1 } ) + \Delta ( d ( \xi _ { k - 1 } ) ) \mid \xi _ { k - 1 } ] \leq d ( \xi _ { k - 1 } ) - { \frac { 1 } { h _ { 1 } ( n ) } } .
$$

Therefore

$$
E [ d ( \xi _ { k } ) \mid d ( \xi _ { 0 } ) > 0 ] \leq E [ d ( \xi _ { k - 1 } ) - \frac { 1 } { h _ { 1 } ( n ) } \mid d ( \xi _ { 0 } ) > 0 ] .
$$

By induction on $k$ , we can get

$$
E [ d ( \xi _ { k } ) \mid d ( \xi _ { 0 } ) > 0 ] \leq E \left[ d ( \xi _ { 0 } ) - { \frac { k } { h _ { 1 } ( n ) } } \mid d ( \xi _ { 0 } ) > 0 \right] .
$$

Hence we have

$$
\begin{array} { r l } { 0 = E [ d ( \xi _ { \tau } ) \mid d ( \xi _ { 0 } ) > 0 ] } & { \leq E \left[ d ( \xi _ { 0 } ) - \frac { \tau } { h _ { 1 } ( n ) } \mid d ( \xi _ { 0 } ) > 0 \right] } \\ & { \leq E [ d ( \xi _ { 0 } ) ] - \frac { 1 } { h _ { 1 } ( n ) } E [ \tau \mid d ( \xi _ { 0 } ) > 0 ] . } \end{array}
$$

According to the above inequality and Condition 1,

$$
E [ \tau \mid d ( \xi _ { 0 } ) > 0 ] \leq E [ d ( \xi _ { 0 } ) ] h _ { 1 } ( n ) \leq h _ { 0 } ( n ) h _ { 1 } ( n ) .
$$

Let $h ( n ) = h _ { 0 } ( n ) h _ { 1 } ( n )$ . We arrive at

$$
E [ \tau \mid d ( \xi _ { 0 } ) > 0 ] \leq h ( n ) .
$$

Under certain stronger conditions, we can get some stronger results.

Condition 3 Let $d _ { \operatorname* { m a x } } = \{ d ( x ) : x \in S \}$ , and the interval $[ 0 , d _ { \mathrm { m a x } } ]$ be divided into $L + 1$ sub intervals: $d _ { 0 } \equiv 0 < d _ { 1 } < . . . < d _ { L } < d _ { L + 1 } \equiv d _ { \mathrm { m a x } }$ , where $L > 0$ is an integer.

(a) For any $l ( 0 ~ \le ~ l ~ \le ~ L )$ , if at time $k$ , the population $\xi _ { k }$ enters the interval $[ 0 , d _ { l } ]$ , i.e., $d ( \xi _ { k } ) \leq d _ { l }$ , then after that time, the population will not return to the interval $( d _ { l } , d _ { L + 1 } ]$ again, i.e., for any $t \geq k$ : $d ( \xi _ { t } ) \leq d _ { l }$ ;

(b) $A t$ any time $k$ , if the population $\xi _ { k }$ is in the interval $( d _ { l } , d _ { l + 1 } ]$ , then the drift satisfies:

$$
E [ d ( \xi _ { k } ) - d ( \xi _ { k + 1 } ) \mid d _ { l } < d ( \xi _ { k } ) \leq d _ { l + 1 } ] \geq { \frac { 1 } { h _ { l } ( n ) } } ,
$$

where $h _ { l } \left( n \right) > 0$ .

Theorem 2 If $\{ d ( \xi _ { k } ) ; k = 0 , 1 , \cdot \cdot \cdot \}$ satisfies Condition $\boldsymbol { \mathcal { J } }$ , then starting from any initial population $\xi _ { 0 }$ with $d ( \xi _ { 0 } ) > 0$ ,

$$
E [ \tau \mid d ( \xi _ { 0 } ) > 0 ] \leq \sum _ { l = 0 } ^ { L } h _ { l } ( n ) ( d _ { l + 1 } - d _ { l } ) .
$$

Proo:Let' consider the worst case with the initial population $d ( \xi _ { 0 } ) = d _ { L + 1 }$

For any $l$ with $0 \leq l \leq L$ , define $\tau _ { L + 1 } = 0$ and

$$
\tau _ { l } = \operatorname* { m i n } \{ t : d ( \xi _ { t } ) \leq d _ { l } \} .
$$

It is easy to see that $\tau = \tau _ { 0 } = \left( \tau _ { L } - \tau _ { L + 1 } \right) + \left( \tau _ { L - 1 } - \tau _ { L } \right) + \cdot \cdot \cdot + \left( \tau _ { 0 } - \tau _ { 1 } \right) .$

Given any $l$ with $0 \leq l \leq L$ , according to Condition 3(b), we know

$$
E [ d ( \xi _ { k } ) - d ( \xi _ { k + 1 } ) \mid d _ { l } < d ( \xi _ { k } ) \leq d _ { l + 1 } ] \geq { \frac { 1 } { h _ { l } ( n ) } } .
$$

Then according to Condition $\mathrm { 3 ( a ) }$ and Theorem 1, we have

$$
E [ \tau _ { l } - \tau _ { l + 1 } \ | \ d _ { l } < d ( \xi _ { k } ) \le d _ { l + 1 } ] \le h _ { l } ( n ) ( d _ { l + 1 } - d _ { l } ) .
$$

Hence

$$
E [ \tau \mid \xi _ { 0 } ] \leq \sum _ { l = 0 } ^ { L } h _ { l } ( n ) ( d _ { l + 1 } - d _ { l } ) .
$$

Condition 4 Let $d _ { \operatorname* { m a x } } = \{ d ( x ) : x \in S \}$ , and the interval $[ 0 , d _ { \mathrm { m a x } } ]$ be divided into $L + 1$ subintervals: $d _ { 0 } \equiv 0 < d _ { 1 } < . . . < d _ { L } < d _ { L + 1 } \equiv d _ { \mathrm { \tiny m a x } } .$ ,where $L > 0$ is an integer. At any time $k \geq 0$ , if the population $\xi _ { k }$ is in the interval $( d _ { l } , d _ { \mathrm { m a x } } ]$ , then the drift satisfies:

$$
E [ d ( \xi _ { k } ) - d ( \xi _ { k + 1 } ) \mid d ( \xi _ { k } ) \geq d _ { l } ] \geq \frac { 1 } { h _ { l } ( n ) } ,
$$

where $h _ { l } \left( n \right) > 0$ .

Theorem 3 If $\{ d ( \xi _ { k } ) ; k = 0 , 1 , \cdot \cdot \cdot \}$ satisfies Condition 4, then starting from any initial population $\xi _ { 0 }$ with $d ( \xi _ { 0 } ) > 0$ ,

$$
E [ \tau \mid d ( \xi _ { 0 } ) > 0 ] \leq \sum _ { l = 0 } ^ { L } h _ { l } ( n ) ( d _ { l + 1 } - d _ { l } ) .
$$

Proof: The proof is simliar to that of Theorem 2.

Using the same analytical technique as those used in Theorem 1, we can obtain easily the following results.

Condition 5 For some population $X$ ,

$$
d ( X ) \geq h _ { 0 } ( n ) ,
$$

where $h _ { 0 } ( n ) > 0$ is a function of problem size $n$ .

Condition 6 There exists a polynomial function, $h _ { 1 } ( n ) > 0$ , of problem size n such that

$$
E [ d ( \xi _ { k } ) - d ( \xi _ { k + 1 } ) \mid \xi _ { k } = X ] \leq { \frac { 1 } { h _ { 1 } ( n ) } }
$$

for any time $k$ and population $X$ with $d ( X ) > 0$ .

Theorem 4 If $\{ d ( \xi _ { k } ) ; k = 0 , 1 , \cdot \cdot \cdot \}$ satisfies Conditions $5$ and $\it 6$ , then starting from the initial population with $d ( X ) \geq h _ { 0 } ( n )$ ,

$$
E [ \tau \mid \xi _ { 0 } = X ] \geq h ( n ) ,
$$

where $h ( n ) = h _ { 0 } ( n ) h _ { 1 } ( n )$ is a function of problem size $n$ .

Proof: Similar to the proof of Theorem 1.

# 3.2 The Subset Sum Problem

EAs have been applied to the subset sum problem in practice [22]. The problem can be described as follows: Given a set $W _ { n } = \{ w _ { 1 } , \cdot \cdot \cdot , w _ { n } \}$ of $n$ integers and a large integer $C$ , find a subset $S$ of $W$ such that the sum of the elements in $S$ are closest to but not exceeding $C$ . The subset sum problem is NP-complete. The partition problem can be polynomially transformed to it [23].

A solution $S$ to the subset sum problem can be represented by a string $x = \left( s _ { 1 } \cdots s _ { n } \right)$ where $s _ { i } \in \{ 0 , 1 \}$ . The presence of $w _ { i }$ in $S$ means that $s _ { i } = 1$ while its absence is represented by $s _ { i } = 0$ . A feasible solution to the subset sum problem is a string $x = ( s _ { 1 } \cdot \cdot \cdot s _ { n } )$ , $s _ { i } \in \{ 0 , 1 \}$ , such that

$$
\sum _ { i = 1 } ^ { n } w _ { i } s _ { i } \leq C ,
$$

where $\textstyle F ( x ) = \sum _ { j = 1 } ^ { n } w _ { i } s _ { i }$ maximizes the objective function (without exceedings $C$ ).

The fitness function can be defined as $f ( x ) = - ( C - F ( x ) + ( 1 - \theta ) F ( x ) )$ , where $\theta = 1$ when $x$ is feasible and $\theta = 0$ when $x$ otherwise. Notice that $( 0 \cdots 0 )$ is a feasible solution.

In this subsection, we are interesting in a particular family of subset sum problems $\{ W _ { n } , n =$ $1 , 2 , \cdots \}$ , $n$ is an integer, for which an EA can find the optimal solution within polynomial average time.

The family of problems we focus on is $\{ W _ { 1 } , W _ { 2 } , \cdots , W _ { n } , \cdot \cdot \cdot \}$ , where

$$
\begin{array} { c l } { { W _ { n } } } & { { = \big \{ w _ { 1 } , \cdots , w _ { n } \big \} , } } \\ { { } } & { { w _ { 1 } , w _ { 2 } , \cdots , w _ { n } \mathrm { ~ a r e ~ p o s i t i v e s } , } } \\ { { C } } & { { = \displaystyle \sum _ { i = 1 } ^ { n } w _ { i } s _ { i } . } } \end{array}
$$

It is obvious that $x = ( 1 \cdots 1 )$ is the unique optimal solution and any subset of $W _ { n }$ is a feasible solution. This prolem is, in fact, the linear function problem [11].

The EA for solving the family of subset sum problems follows the structure given in Section 2. The crossover, mutation and selection are implemented as follows.

$x = ( s _ { 1 } ^ { ( x ) } \cdot \cdot \cdot s _ { n } ^ { ( x ) } )$ and $y = ( s _ { 1 } ^ { ( y ) } \cdot \cdot \cdot s _ { n } ^ { ( y ) } )$ from the population $\xi _ { k }$ , choose a crossover point $m \in \{ 1 , \cdots , n - 1 \}$ at random and exchange all bits after the $m ^ { t h }$ bit between two individuals to form two new individuals $x ^ { \prime }$ and $y ^ { \prime }$ .

$$
\begin{array} { l } { { x ^ { \prime } = \bigl ( s _ { 1 } ^ { ( x ) } \cdot \cdot \cdot s _ { m - 1 } ^ { ( x ) } s _ { m } ^ { ( y ) } s _ { m + 1 } ^ { ( y ) } \cdot \cdot \cdot s _ { n } ^ { ( y ) } \bigr ) , } } \\ { { y ^ { \prime } = \bigl ( s _ { 1 } ^ { ( y ) } \cdot \cdot \cdot s _ { m - 1 } ^ { ( y ) } s _ { m } ^ { ( x ) } s _ { m + 1 } ^ { ( x ) } \cdot \cdot \cdot s _ { n } ^ { ( x ) } \bigr ) . } } \end{array}
$$

A new intermediate population $\xi _ { k + C }$ of $2 N$ individuals will be formed after crossover.

The mutation operator is the bit mutation. Given an individual $x = ( s _ { 1 } \cdot \cdot \cdot s _ { n } ) $ in $\xi _ { k + C }$ , choose a single bit $s _ { i }$ at random from it and flip the bit. Another new intermediate population $\xi _ { k + M }$ of $2 N$ individuals is formed after mutation.

Selection used implements a kind of probabilistic elitism. $2 N$ individuals are selected from $\xi _ { k }$ and $\xi _ { k + M }$ as follows: the best individual with the highest fitness is copied with probability at least $1 - e ^ { - n }$ to the new population $\xi _ { k + S }$ , and other individuals are assigned a survival probability according to their fitness. Any selection scheme can be used as long as fitter individuals were assigned higher probabilities.

Theorem 5 Given the family of subset sum problems and the EA to solve them. For any initial population $X$ with $d ( X ) > 0$ ,

$$
E [ \tau \mid \xi _ { 0 } = X ] \leq h ( n )
$$

where $h ( n )$ is a polynomial of $n$ .

Proof:

Define the distance function $d ( x )$ as:

$$
d ( x ) = \sum _ { i = 1 } ^ { n } \mid s _ { i } - 1 \mid
$$

According to Theorem 1, we need to verify that the random sequence, $\{ d ( \xi _ { k } ) , k = 0 , 1 , \cdot \cdot \cdot \}$ , satisfies Conditions 1 and 2.

From the definition of the above distance and Eq.(2), we know that for any population $X$ .

$$
d ( X ) \leq n .
$$

Hence the random sequence $\{ d ( \xi _ { k } ) ; k = 0 , 1 , \cdot \cdot \cdot \}$ satisfies Condition 1.

For any time $k \geq 0$ , and population $\xi _ { k }$ with $d ( \xi _ { k } ) > 0$ , we now investigate the impact of crossover on the drift. One of the three events may happen after crossover: (1) event $I \{ d ( \xi _ { k + C } ) <$ $d ( \xi _ { k } ) \}$ ,(2) event $I \{ d ( \xi _ { k + C } ) = d ( \xi _ { k } ) \}$ , or (3) event $I \{ d ( \xi _ { k + C } ) > d ( \xi _ { k } ) \}$ .

We first show that event $I \{ d ( \xi _ { k + C } ) > d ( \xi _ { k } ) \}$ cannot happen. In other words, crossover does not produce a worse intermediate population. Assume $x _ { 1 }$ and $x _ { 2 }$ are two individuals in population $\xi _ { k }$ , and $y _ { 1 }$ and $y _ { 2 }$ are their offspring. Since the crossover does not increase or decrease the amount of ones in individuals $x _ { 1 }$ and $x _ { 2 }$ , we have

$$
d ( y _ { 1 } ) + d ( y _ { 2 } ) = d ( x _ { 1 } ) + d ( x _ { 2 } ) .
$$

That is,

$$
d ( y _ { 1 } ) - d ( x _ { 1 } ) = - ( d ( y _ { 2 } ) - d ( x _ { 2 } ) ) .
$$

This means that the increase of one individual's drift will be the decrease of another individual's drift. So the crossover will not make the intermediate population $\xi _ { k + C }$ worse. Event $I \{ d ( \xi _ { k + C } ) >$ $d ( \xi _ { k } ) \}$ cannot happen.

Assume that event $I \{ d ( \xi _ { k + C } ) = d ( \xi _ { k } ) \}$ has happened. Then one of the following three events may happen subsequently: (a) event $I \{ d ( \xi _ { k + M } ) < d ( \xi _ { k + C } ) \}$ , (b) event $I \{ d ( \xi _ { k + M } ) = d ( \xi _ { k + C } ) \}$ , and (c) event $I \{ d ( \xi _ { k + M } ) > d ( \xi _ { k + C } ) \}$ .

Event $I \{ d ( \xi _ { k + M } ) = d ( \xi _ { k + C } ) \}$ cannot happen because the mutation always happens.

The probability of event $I \{ d ( \xi _ { k + M } ) < d ( \xi _ { k + C } ) \}$ is not less than $1 / n$ (if $d ( \xi _ { k + C } ) > 0 )$ , and the probability of event $I \{ d ( \xi _ { k + M } ) > d ( \xi _ { k + C } ) \}$ is not greater than $( n - 1 ) / n$ If $d ( \xi _ { k + C } ) = 0$ , then the population $\xi _ { k + C }$ has one individual with the maximum fitness.

Assume that event $I \{ d ( \xi _ { k + C } ) < d ( \xi _ { k } ) \}$ has happened. Then one of the following three events may happen subsequently: $\left( \mathbf { a } ^ { \prime } \right)$ event $I \{ d ( \xi _ { k + M } ) < d ( \xi _ { k + C } ) \}$ , $\mathrm { ( b ^ { \prime } ) }$ event $I \{ d ( \xi _ { k + M } ) = d ( \xi _ { k + C } ) \}$ , and $\displaystyle ( \mathrm { c } ^ { \prime } )$ event $I \{ d ( \xi _ { k + M } ) > d ( \xi _ { k + C } ) \}$ .

The probablities of the three events are similar to those analysed in the cas $I \{ d ( \xi _ { k + C } ) =$ $d ( \xi _ { k } ) \}$ .

Now let's examine the role of selection: the individual with the best fitness will appear in the next population $\xi _ { k + S }$ with probability $1 - e ^ { - n }$ , so the probability $P ( d ( \xi _ { k + S } ) < d ( \xi _ { k } ) \mid d ( \xi _ { k + M } ) <$ $d ( \xi _ { k } ) )$ is not less than $1 - e ^ { - n }$ and the probability $P ( d ( \xi _ { k + S } ) > d ( \xi _ { k } ) \mid d ( \xi _ { k + M } ) < d ( \xi _ { k } ) )$ is not more than $e ^ { - n }$ . The probability $P ( d ( \xi _ { k + S } ) > d ( \xi _ { k } ) \mid d ( \xi _ { k + M } ) > d ( \xi _ { k } ) )$ is not more than $e ^ { - n }$ . And the event $I \{ d ( \xi _ { k + S } ) < d ( \xi _ { k } ) \mid d ( \xi _ { k + M } ) > d ( \xi _ { k } ) \}$ cannot happen.

Considering all the different cases discussed above, we have

$$
\begin{array} { r l } & { E [ ( d \{ \xi _ { k + 1 } \} ) - d \{ \xi _ { k } \} ] \ ( d \{ \xi _ { k } \} > \mathbb { I } ) } \\ { = } & { E [ ( d \{ \xi _ { k + 1 } \} - d \{ \xi _ { k } \} ) ] \ [ d \{ d \{ \xi _ { k + 1 } \} - d \{ \xi _ { k + 1 } \} , d \{ \xi _ { k + 1 } d \} < d \{ \xi _ { k + 1 } c \} , d \{ \xi _ { k + 1 } s \} < d \{ \xi _ { k } \} ] } \\ & { + ( d \{ \xi _ { k } \} > \mathbb { I } ) } \\ & { + L [ ( d \{ \xi _ { k + 1 } \} ) - d \{ \xi _ { k } \} ] \mathcal { I } ( d \{ \xi _ { k - c } \} < d \{ \xi _ { k } \} , d \{ \xi _ { k + 1 } \} ) < d \{ \xi _ { k + c } \} , d \{ \xi _ { k + s } \} > d \{ \xi _ { k + s } \} > d \{ \xi _ { k } \} ] } \\ & { + L [ ( d \{ \xi _ { k + 1 } \} ) - d \{ \xi _ { k } \} ] \mathcal { I } ( d \{ \xi _ { k + c } \} < d \{ \xi _ { k } \} , d \{ \xi _ { k + 1 } \} > \mathcal { I } , d \{ \xi _ { k + c } \} ) } \\ & { + L [ ( d \{ \xi _ { k + 1 } \} ) > \mathbb { I } ] } \\ & { + L [ ( d \{ \xi _ { k } \} ) , \ \xi \} ] \ } \\ & { + \frac { d } { d \{ \xi _ { k } \} } ( d \{ \xi _ { k + 1 } \} ) - d \{ \xi _ { k } \} ] \mathcal { I } ( d \{ \xi _ { k + c } \} < d \{ \xi _ { k } \} , d \{ \xi _ { k + 1 } \} > d \{ \xi _ { k + c } \} , d \{ \xi _ { k + s } \} > d \{ \xi _ { k } \} ) } \\ & { + L [ ( d \{ \xi _ { k + 1 } \} ) - d \{ \xi _ { k } \} ] \mathcal { I } ( d \{ \xi _ { k + c } \} < d \{ \xi _ { k } \} , d \{ \xi _ { k + 1 } \} ) + \mathcal { I } ( \{ \xi _ { k + c } \} , d \{ \xi _ { k + 1 } \} > d \{ \xi _ { k } \} ) } \\ & { + L [ ( d \{ \xi _ { k + 1 } \} ) , } \\ &  + L [ ( d \{ \xi _ { k } \} ) , \xi \} ] \end{array}
$$

In other words,

$$
\begin{array} { r l } & { E [ d ( \xi _ { k + 1 } ) - d ( \xi _ { k } ) \mid d ( \xi _ { k } ) > 0 ] } \\ { \leq } & { ( - 1 ) P ( d ( \xi _ { k + C } ) < d ( \xi _ { k } ) , d ( \xi _ { k + M } ) < d ( \xi _ { k + C } ) \mid d ( \xi _ { k } ) > 0 ) ( 1 - e ^ { - n } ) } \\ & { + ( n - 1 ) P ( d ( \xi _ { k + C } ) < d ( \xi _ { k } ) , d ( \xi _ { k + M } ) < d ( \xi _ { k + C } ) \mid d ( \xi _ { k } ) > 0 ) e ^ { - n } } \\ & { + ( - 1 ) P ( d ( \xi _ { k + C } ) < d ( \xi _ { k } ) , d ( \xi _ { k } ) > d ( \xi _ { k + M } ) > d ( \xi _ { k + C } ) \mid d ( \xi _ { k } ) > 0 ) ( 1 - e ^ { - n } ) } \\ & { + ( n - 1 ) P ( d ( \xi _ { k + C } ) < d ( \xi _ { k } ) , d ( \xi _ { k + M } ) > d ( \xi _ { k + C } ) \mid d ( \xi _ { k } ) > 0 ) e ^ { - n } } \\ & { + ( - 1 ) P ( d ( \xi _ { k + C } ) = d ( \xi _ { k } ) , d ( \xi _ { k + M } ) < d ( \xi _ { k + C } ) \mid d ( \xi _ { k } ) > 0 ) ( 1 - e ^ { - n } ) } \\ & { + ( n - 1 ) P ( d ( \xi _ { k + C } ) = d ( \xi _ { k } ) , d ( \xi _ { k + M } ) < d ( \xi _ { k + C } ) \mid d ( \xi _ { k } ) > 0 ) ( 1 - e ^ { - n } ) } \\ & { + ( n - 1 ) P ( d ( \xi _ { k + C } ) = d ( \xi _ { k } ) , d ( \xi _ { k + M } ) < d ( \xi _ { k + C } ) \mid d ( \xi _ { k } ) > 0 ) e ^ { - n } } \\ & { + ( n - 1 ) P ( d ( \xi _ { k + C } ) = d ( \xi _ { k } ) , d ( \xi _ { k + M } ) > d ( \xi _ { k + C } ) \mid d ( \xi _ { k } ) > 0 ) e ^ { - n } } \end{array}
$$

In arriving at the above inequality, we have used the fact that $| ~ d ( \xi _ { k + 1 } ) - d ( \xi _ { k } ) ~ | \le n - 1$ Since

$$
( - 1 ) P ( d ( \xi _ { k + C } ) < d ( \xi _ { k } ) , d ( \xi _ { k } ) > d ( \xi _ { k + M } ) > d ( \xi _ { k + C } ) \mid d ( \xi _ { k } ) > 0 ) ( 1 - e ^ { - n } ) < 0
$$

and

$$
P \left( d ( \xi _ { k + C } ) < d ( \xi _ { k } ) \mid d ( \xi _ { k } > 0 ) \right) + P \left( d ( \xi _ { k + C } ) = d ( \xi _ { k } ) \mid d ( \xi _ { k } > 0 ) \right) = 1 ,
$$

we have

$$
\begin{array} { r l } & { ~ E [ \{ \xi _ { k } , \} _ { 1 } ] = \frac { 1 } { \beta } \langle \xi _ { k } | , ~ \xi _ { k } \rangle = \langle \xi _ { k } | , } \\ { \leq } & { \langle - 1 \} ^ { p } \alpha \{ \xi _ { k + 1 } , \xi _ { k } ^ { \prime } \} , ~ d \xi _ { k } \rangle = \langle \xi _ { k } \rangle = \frac { 1 } { \beta } \frac { 1 } { n } ( 1 - \varepsilon ^ { - \beta } ) } \\ & { + ( n - 1 ) ^ { p } r ^ { \alpha } ( d \{ \xi _ { k } \} _ { 1 } ) = d \{ \xi _ { k } \} , ~ d \{ \xi _ { k } \} > 0 , ~ \frac { 1 } { n } \varepsilon , } \\ & { + ( n - 1 ) ^ { p } r ^ { \alpha } d \{ \xi _ { k + 1 } , \sigma \} < d \{ \xi _ { k } \} , ~ d \{ \xi _ { k } \} > 0 , ~ \frac { 1 } { n } \varepsilon , } \\ & { + ( n - 1 ) ^ { p } r ^ { \beta } d \{ \xi _ { k + 1 } , \sigma \} < d \{ \xi _ { k } \} , ~ d \{ \xi _ { k } \} > 0 , ~ \frac { 1 } { n } \varepsilon ^ { - \beta } } \\ & { + ( - 1 ) ^ { p } r ^ { \beta } ( d \{ \xi _ { k + 1 } , \varepsilon \} = d \{ \xi _ { k } \} ) , ~ d \{ \xi _ { k } \} > 0 , ~ \frac { 1 } { n } \varepsilon ^ { - \beta } , } \\ & { + ( n - 1 ) ^ { p } r ^ { \beta } ( d \{ \xi _ { k } \} _ { 1 } ) = d \{ \xi _ { k } \} , ~ d \{ \xi _ { k } \} > 0 , ~ \frac { 1 } { n } \varepsilon ^ { - \beta } , } \\ & { + ( n - 1 ) ^ { p } r ^ { \alpha } d \{ \xi _ { k + 1 } , \sigma \} = \langle \xi _ { k } \rangle , ~ d \{ \xi _ { k } \} > 0 , ~ \frac { 1 } { n } \varepsilon ^ { - \beta } , } \\ &  ~ \{ ( n - 1 ) ^ { p } r ^ { \beta } d \{ \xi _ { k + 1 } , \sigma \} = d \{ \xi _ { k } \} , ~ \beta \} & { ~ } \\ & { \leq } & { \langle - 1 \} \frac { 1 } { n } ( 1 - \varepsilon ^ { - \beta } ) + 2 ( \beta + 1 ) \frac { n - 1 } { n } \varepsilon , } \\ { \leq } &  - \frac { 1 } { n } - \mathrm \end{array}
$$

Let

$$
h _ { 1 } ( n ) = \frac { n } { 1 - e ^ { - n } - 2 ( n - 1 ) ^ { 2 } e ^ { - n } } ,
$$

then when $n  + \infty$ , $h _ { 1 } ( n ) = O ( n )$ . Hence,

$$
E [ d ( \xi _ { k + 1 } ) - d ( \xi _ { k } ) \mid d ( \xi _ { k } ) > 0 ] \leq - { \frac { 1 } { h _ { 1 } ( n ) } }
$$

and

$$
\operatorname* { l i m } _ { n \to \infty } \frac { - 1 } { h _ { 1 } ( n ) } < 0 ,
$$

where

$$
h _ { 1 } ( n ) = { \cal { O } } ( n ) .
$$

So we have proven that the random sequence $\{ d ( \xi _ { k } ) ; k = 0 , 1 , \cdot \cdot \cdot \}$ satisfies Condition 2. According to Theorem 1, we know

$$
E [ \tau \mid \xi _ { 0 } = X ] \leq h ( n )
$$

where $h ( n ) = O ( n ^ { 2 } )$ .

# 3.3 Other Problems

In order to show the power and generality of our main results, we wll use some of the problems given in [7] as examples to derive EA's computation time by verifying drift conditions given previously. Rudolph's survey [7] is probably the most comprehesive overview of recent results on the finite time behavior of EAs in finite space and discrete time. It is worth noting that the EA used in this section is more general than the $( 1 + 1 )$ EA used in [7]. A $( 2 N + 2 N )$ EA without crossover is used in this section.

The results shown in this section illustrate that drift analysis can be used to deriveEA's aveae computation time for a variety of different problems.

Let $S = \{ ( s _ { 1 } \cdot \cdot \cdot s _ { n } ) , s _ { i } \in \{ 0 , 1 \} \}$ be the chromosome representation. The mutation and selection are implemented as follows.

A kind of uniform bit mutation is used. For any individual $x = \left( s _ { 1 } \cdots s _ { n } \right) $ in $\xi _ { k }$ , each bit $s _ { i }$ will flip with a mutation rate $p _ { m } > 0$ . A new intermediate population $\xi _ { k + M }$ of $2 N$ individuals is formed after mutation.

$( 2 N + 2 N )$ elitism is implemented as the selection scheme. In other words, the $2 N$ individuals with the highest fitness from populations $\xi _ { k }$ and $\xi _ { k + M }$ are copied to the new population $\xi _ { k + S }$ .

# 3.3.1 Linear Functions

A function $f : S  R$ is linear if $\begin{array} { r } { f ( x ) = c _ { 0 } + \sum _ { i = 1 } ^ { n } c _ { i } s _ { i } } \end{array}$ where coefficients $c _ { i } \in R$ [7]. If $c _ { i } \geq 0$ for all $c _ { i }$ , then it is clear that $( 1 \cdots 1 )$ is the only optimal solution.

Theorem 6 For the linear function with positive coeffients $c _ { 1 } > c _ { 2 } > \cdot \cdot \cdot > c _ { n } > 0$ , the $E A$ with mutation probability $p _ { m } = 1 / n$ needs an average $O ( n \ln n )$ steps to reach the optimal solution.

Proof: Define the distance function $\begin{array} { r } { d ( x ) = \sum _ { i = 1 } ^ { n } ( 1 - s _ { i } ) } \end{array}$ . Since $0 \leq d ( x ) \leq n$ , we can divide $[ 0 , d _ { \mathrm { m a x } } ]$ into $n$ intervals $d _ { 0 } < d _ { 1 } < d _ { 2 } < \cdot \cdot \cdot < d _ { n }$ where $d _ { l } \ = \ l$ for $0 \leq l \leq n$ . We will use Theorem 3 to prove the result.

Assume at time $k \geq 0$ , the population $\xi _ { k }$ satisfy $d ( \xi _ { k } ) > d _ { l - 1 }$ where $l \in \{ 1 , \cdots , n \}$ . Without the loss of generality, assume $d ( \xi _ { k } ) = d _ { l }$ (other cases can be proven in the same way). Then

$$
\begin{array} { r c l } { { E [ d ( \xi _ { k } ) - d ( \xi _ { k + 1 } ) ] } } & { { = } } & { { E [ ( d ( \xi _ { k } ) - d ( \xi _ { k + 1 } ) ) I \{ d ( \xi _ { k } ) > d ( \xi _ { k + 1 } ) \} ] } } \\ { { } } & { { } } & { { + E [ ( d ( \xi _ { k } ) - d ( \xi _ { k + 1 } ) ) I \{ d ( \xi _ { k } ) < d ( \xi _ { k + 1 } ) \} ] . } } \end{array}
$$

First let's consider $E [ ( d ( \xi _ { k } ) - d ( \xi _ { k + 1 } ) ) I \{ d ( \xi _ { k } ) > d ( \xi _ { k + 1 } ) \} ]$ . Let $x$ be the best individual in population $\xi _ { k }$ . The probability of its flipping one of its $l ~ ^ { 6 6 } 0 ^ { 9 }$ bits while keeping its $n - l$ "1" bits unchanged is $\begin{array} { r } { C _ { l } ^ { 1 } \frac { 1 } { n } \left( 1 - \frac { 1 } { n } \right) ^ { n - l } } \end{array}$ . Hence

$$
E [ ( d ( \xi _ { k } ) - d ( \xi _ { k + 1 } ) ) I \{ d ( \xi _ { k } ) > d ( \xi _ { k + 1 } ) \} ] \ge \frac { l } { n } \left( 1 - \frac { 1 } { n } \right) ^ { n - l } .
$$

Secondly let's consider $E [ ( d ( \xi _ { k } ) - d ( \xi _ { k + 1 } ) ) I \{ d ( \xi _ { k } ) < d ( \xi _ { k + 1 } ) \} ]$ . Let $x$ be the best individual in $\xi _ { k }$ . Assume that event $I \{ d ( \xi _ { k } ) < d ( \xi _ { k + 1 } ) \} ]$ happens, then it implies event $I ^ { \prime }$ : i.e., one of its $l ^ { ~ 6 6 } 0 ^ { 9 }$ bits must flip (In fact the leftmost bit among all flipping bits must flip from $^ { 6 6 } 0 ^ { 9 }$ to $^ { 6 6 } 1 ^ { \mathfrak { s } }$ becasue of $c _ { 1 } > c _ { 2 } > \cdots > c _ { n }$ and elitist selection), and at least two of its $n - l$ $1 ^ { \mathfrak { s } }$ bits must also fip. So the probability of event $I \{ d ( \xi _ { k } ) < d ( \xi _ { k + 1 } ) \}$ happening is no more than that of event $I ^ { \prime }$ . Event $I ^ { \prime }$ can be further divided into the following cases:

1. One of the $^ { 6 6 } 0 ^ { 9 }$ bits in $x$ becomes 1, and two of the $^ { 6 6 } 1 ^ { \mathfrak { s } }$ bits become 0. The probability of this happening is

$$
\frac { l } { n } C _ { n - l } ^ { 2 } \left( \frac { 1 } { n } \right) ^ { 2 } \left( 1 - \frac { 1 } { n } \right) ^ { n - l - 2 } < \frac { l } { n } \frac { 1 } { 2 ! } \left( 1 - \frac { 1 } { n } \right) ^ { n - l } .
$$

2. One of the $^ { 6 6 } 0 ^ { 9 }$ bits in $x$ becomes 1, and three of the $^ { 6 6 } 1 ^ { \mathfrak { s } }$ bits become 0. The probability of this happening is

$$
\frac { l } { n } C _ { n - l } ^ { 3 } \left( \frac { 1 } { n } \right) ^ { 3 } \left( 1 - \frac { 1 } { n } \right) ^ { n - l - 3 } < \frac { l } { n } \frac { 1 } { 3 ! } \left( 1 - \frac { 1 } { n } \right) ^ { n - l } .
$$

3. ...

Hence we get

$$
E [ ( d ( \xi _ { k } ) - d ( \xi _ { k + 1 } ) ) I \{ d ( \xi _ { k } ) < d ( \xi _ { k + 1 } ) \} ] > \frac { l } { n } \left( \frac { - 1 } { 2 ! } + \frac { - 2 } { 3 ! } + \cdot \cdot \right) \left( 1 - \frac { 1 } { n } \right) ^ { n - l } .
$$

So

$$
E [ d ( \xi _ { k } ) - d ( \xi _ { k + 1 } ) ] \ge \frac { l } { n } \left( 1 + \frac { - 1 } { 2 ! } + \frac { - 2 } { 3 ! } + \cdot \cdot \cdot \right) \left( 1 - \frac { 1 } { n } \right) ^ { n - l } \ge c \frac { l } { n } ,
$$

where $c > 0$ is a constant. In other words, Condition 4 holds.

According to Theorem 3,

$$
E [ \tau ] \leq c \sum _ { l = n } ^ { 1 } { \frac { n } { l } } = O ( n \ln n ) .
$$

# 3.3.2 Pseudo-modular Functions

A function $f : S  R$ is pseudo-modular if

$$
\begin{array} { r l r } { \operatorname* { m i n } \{ f ( x ) , f ( y ) \} } & { \leq } & { \operatorname* { m a x } \{ f ( x \wedge y ) , f ( x \vee y ) \} } \\ { \operatorname* { m a x } \{ f ( x ) , f ( y ) \} } & { \leq } & { \operatorname* { m i n } \{ f ( x \wedge y ) , f ( x \vee y ) \} , } \end{array}
$$

for all $x , y \in S$ [7].

An example of the pseudo-modular function is the function

$$
f ( x ) = \sum _ { i = 1 } ^ { n } \prod _ { j = 1 } ^ { i } s _ { j } .
$$

Theorem 7 The expected first-hitting time of the $E A$ for the fitness function (6) is $E [ \tau ] \leq n ^ { 2 } ( e - 1 )$ when mutation rate $p _ { m } = 1 / n$ .

Proo:For ftness function (6), the optimal solution is $( 1 \cdots 1 )$ . Define the distance function $d ( x )$ as follows:

$$
d ( x ) = n - \sum _ { i = 1 } ^ { n } \prod _ { j = 1 } ^ { i } s _ { j } .
$$

We can divide $[ 0 , n ]$ into $n$ subintervals $d _ { 0 } < d _ { 1 } < \ldots < d _ { n }$ where $d _ { l } = l$ for $0 \leq l \leq n$ .

According to Theorem 2, we need to verify that $\{ d ( \xi _ { k } ) ; k = 0 , 1 , \cdot \cdot \cdot \}$ satisfies Condition 3.

First let's verify Condition $\mathrm { 3 ( a ) }$ . Since the EA adopts an elitist selection strategy, Condition 3(a) nolds automatically.

Second let's verify Condition 3(b). At any time $k \geq 0$ , if population $\xi _ { k }$ is in the interval $( d _ { l } , d _ { l + 1 } ]$ where $0 \leq l \leq n - 1$ , then there exists at least one indiviudal $x$ in $\xi _ { k }$ such that $d ( x ) = l + 1$ . The probability of $x$ becoming betteris no les than $\begin{array} { r } { \frac { 1 } { n } \left( 1 - \frac { 1 } { n } \right) ^ { n - l - 1 } } \end{array}$ Hence,

$$
E [ d ( \xi _ { k } ) - d ( \xi _ { k + 1 } ) ] \ge \frac { 1 } { n } \left( 1 - \frac { 1 } { n } \right) ^ { n - l - 1 } .
$$

That is, Condition 3(b) holds.

According to Theorem 2, we have

$$
E [ \tau \mid \xi _ { 0 } ] \leq \sum _ { l = 0 } ^ { n - 1 } n \left( 1 - { \frac { 1 } { n } } \right) ^ { - n + l + 1 } \leq n ^ { 2 } ( e - 1 ) .
$$

# 3.3.3 Unimax Functions

A function $f : S  R$ is unimax if there is a unique locally maximal point $x ^ { \ast } \in S$ [7]. The long path problem is a well known unimax problem.

A long path $P _ { n }$ (where the length $n$ of string is odd) is defined by a recursion with $P _ { 1 } = \{ 0 , 1 \}$ as the base path [21]. Given long path $P _ { n }$ , creat a subpath $S _ { 0 0 }$ by prepending $^ { 6 6 } 0 0 ^ { 9 }$ to each point in $P _ { n }$ and another subpath $S _ { 1 1 }$ by prepending $^ { 6 6 } 1 1 ^ { 9 }$ to each point in the reverse order in $P _ { n }$ . The bridge point is build from the last point in $P _ { n }$ prepending by $^ { 6 6 } 0 1 ^ { 9 }$ . Finally, concatenate subpath $S _ { 0 0 }$ , the bridge point and subpath $S _ { 1 1 }$ to obtain long path $P _ { n + 2 }$ . The length of the paths is described by the recurrence equations

$$
\mid P _ { 1 } \mid = 2 , \mid P _ { n + 2 } \mid = 2 \mid P _ { n } \mid + 1 ,
$$

whose solution is $\mid P _ { n } \mid = 3 \cdot 2 ^ { ( n - 1 ) / 2 } - 1$ for odd $n \geq 1$ Table 1 shows long path $P _ { 5 }$

Table 1: Long path $P _ { 5 }$ .   

<table><tr><td>Pos(x)</td><td>x</td><td>Pos(x)</td><td>x</td></tr><tr><td>0</td><td>00000</td><td>6</td><td>11110</td></tr><tr><td>1</td><td>00001</td><td>7</td><td>11111</td></tr><tr><td>2</td><td>00011</td><td>8</td><td>11011</td></tr><tr><td>3</td><td>00111</td><td>9</td><td>11001</td></tr><tr><td>4</td><td>00110</td><td>10</td><td>11000</td></tr><tr><td>5</td><td>10110</td><td></td><td></td></tr></table>

Given a point $x$ on a path $P _ { n }$ , define $P o s ( x )$ to be the position of $x$ on the path which is numbered from 0 to $3 \cdot 2 ^ { ( n - 1 ) / 2 } - 2$ For a point not in the path $P _ { n }$ , define $P o s ( x )$ to be $^ { - 1 }$ Then define the objective function $f ( x )$ as:

$$
f ( x ) = - ( 3 \cdot 2 ^ { ( n - 1 ) / 2 } - 2 ) + \left\{ \begin{array} { l l } { P o s ( x ) , } & { \mathrm { i f ~ } P o s ( x ) \geq 0 , } \\ { - \sum _ { i = 1 } ^ { n } s _ { i } , } & { \mathrm { o t h e r w i s e } . } \end{array} \right.
$$

Theorem 8 For the unimax function $( 7 )$ , starting from the bottom of the increasing path, the expected first hitting time of the $E A$ is $E [ \tau ] = O ( n ^ { 3 } )$ when mutation rate $p _ { m } = 1 / n$ .

Proof: Decompose space $S$ into a family of sets $\{ S _ { - 1 } , S _ { 0 } , \cdot \cdot \cdot , S _ { \left( n - 1 \right) / 2 } \}$ as follows [21]:

$$
\begin{array} { r l r l } & { S _ { 0 } } & { \cup } & { \{ ( 0 1 * * \cdot \cdot * ) \in P _ { n } \} } \\ & { S _ { 1 } } & { = \{ \left( 1 1 1 * \cdot \cdot \cdot * \right) \in P _ { n } \} } & { \cup } & { \{ \left( 1 1 0 1 * \cdot \cdot \cdot * \right) \in P _ { n } \} , } \\ & { S _ { 2 } } & { = \{ \left( 1 1 0 0 1 1 * \cdot \cdot \cdot \cdot * \right) \in P _ { n } \} } & { \cup } & { \{ \left( 1 1 0 0 1 * \cdot \cdot \cdot \cdot * \right) \in P _ { n } \} , } \\ & { \cdot \cdot } & { \in P _ { n } \} } \\ & { S _ { ( l - 3 ) / 2 } } & { = \{ \left( 1 1 0 0 \cdot \cdot \cdot 0 0 1 1 * \right) \in P _ { n } \} } & { \cup } & { \{ \left( 1 1 0 0 * \cdot \cdot \cdot 0 0 0 1 * \right) \in P _ { n } \} , } \\ & { S _ { ( l - 1 ) / 2 } } & { = \{ \left( 1 1 0 0 \cdot \cdot \cdot 0 0 0 0 * \right) \in P _ { n } \} , } \end{array}
$$

and $S _ { - 1 }$ includes all remained points.

Define the distance function $d ( x )$ as follows:

$$
\begin{array} { r l r } { d ( x ) = 0 , } & { \forall x \in S _ { ( n - 1 ) / 2 } } \\ { d ( x ) = 1 , } & { \forall x \in S _ { ( n - 3 ) / 2 } } \\ { \therefore } & { } & \\ { d ( x ) = ( n - 3 ) / 2 , } & { \forall x \in S _ { 1 } , } \\ { d ( x ) = ( n - 1 ) / 2 , } & { \forall x \in S _ { 0 } , } \\ { d ( x ) = ( n - 1 ) / 2 + \operatorname* { m i n } \{ \displaystyle \sum _ { i = 1 } ^ { n } \mid s _ { i } ^ { ( x ) } - s _ { i } ^ { ( y ) } \mid ; y \in P _ { n } \} , } & { \forall x \in S _ { - 1 } . } \end{array}
$$

In the following, we will prove that $\{ d ( \xi _ { k } ) , k = 0 , 1 , \cdot \cdot \cdot \}$ satisfies Condition 3.

Let $d _ { l } = l$ , we can divide $[ 0 , d _ { \mathrm { m a x } } ]$ into a finite number of subintervals $d _ { 0 } < d _ { 1 } < \dots < d _ { \operatorname* { m a x } }$

First, Condition $\mathrm { 3 ( a ) }$ holds because the EA adopts an elitism selection strategy.

Secondly, let's verify Condition $\mathrm { 3 ( b ) }$ . At any time $k \geq 0$ , if population $\xi _ { k }$ satisfies $d ( \xi _ { k } ) >$ $( n - 1 ) / 2$ , then no individual $x$ in the population is on path $P _ { n }$ . Let $x$ is the best individual in $\xi _ { k }$ then the probability of $x$ having a drift is at least $( 1 - 1 / n ) ^ { n - 1 } / n$ . The drift is at least 1. Hence,

$$
E \lbrack d ( \xi _ { k + 1 } ) - d ( \xi _ { k } ) \mid d ( \xi _ { k } ) > ( n - 1 ) / 2 \rbrack = \Omega ( n ^ { - 1 } ) .
$$

Now let's estimate the drift along the path. At any time $k \geq 0$ , if population $\xi _ { k }$ is in the interval $( d _ { l } , d _ { l + 1 } ]$ where $0 \leq l < ( n - 1 ) / 2$ , then at least one individual $x$ satisfies $d ( x ) = d _ { l + 1 }$ . If $x$ is a bridge point, the probability of a drift happening is at least $( 1 - 1 / n ) ^ { n - 1 } / n$ and the drift length is at least 1. If $x$ is not a bridge point, the probability of a drift happening is at least $( 1 - 1 / n ) ^ { n - 2 } / n ^ { 2 }$ and the drift length is at least 1. Summarising both cases, the expected drift on the path is:

$$
E [ d ( \xi _ { k + 1 } ) - d ( \xi _ { k } ) \mid d ( \xi _ { k } ) = l + 1 ] = \Omega ( n ^ { - 2 } ) .
$$

In other words, Condition $2 ( \mathrm { b } )$ holds.

According to Theorem 2, we come to the conclusion

$$
E [ \tau ] \leq \sum _ { l = n } ^ { 0 } { \cal O } ( n ) + \sum _ { l = ( n - 1 ) / 2 } ^ { 0 } { \cal O } ( n ^ { 2 } ) = { \cal O } ( n ^ { 3 } ) ,
$$

where the first part is the average time for points not on the path to reach the path, and the second part is the average time for points on the path to reach the optimal solution.

# 3.3.4 Almost Positive Functions

A function $f : S  R$ is almost-positive if the coefficients of all nonlinear terms are non-negative [7].

An example of almost-positive function is

$$
f ( x ) = n - \sum _ { i = 1 } ^ { n } s _ { i } + ( n + 1 ) \prod _ { i = 1 } ^ { n } s _ { i } .
$$

We can define the distance function as $\begin{array} { r } { d ( x ) = \sum _ { i = 1 } ^ { n } \mid s _ { i } - 1 \mid } \end{array}$

Theorem 9 The expected first-hitting time of the EA for the almost positive function (8) is $E [ \tau ] =$ $\Omega ( n ^ { n } )$ when mutation rate $p _ { m } = 1 / n$ and the EA starts from $d ( \xi _ { 0 } ) = n$ .

Proof: For the fitness function (8), the optimal solution is $( 1 \cdots 1 )$ . Indiviudal $x = ( 0 \cdots 0 )$ is the second best (maximum) point because $f ( x ) = n$ , but it is farthest from the optimal solution with $d ( x ) = n$ .

According to Theorem 4, we need to verify that $\{ d ( \xi _ { k } ) , k = 0 , 1 , \cdot \cdot \cdot \}$ satisfies Conditions 5 and 3.

First, let's assume that $d ( \xi _ { 0 } ) = n$ , i.e., the initial population is composed of individuals $( 0 \cdots 0 )$ only. Let $h _ { 0 } ( n ) = n$ , then Condition 5 holds.

Secondly, at any time $k \geq 0$ , if $\xi _ { k }$ satisfies $d ( \xi _ { k } ) = n$ , there are only two possible events which may happen after mutation and elitist selection: event $I \{ d ( \xi _ { k + 1 } ) = n \}$ or event $I \{ d ( \xi _ { k + 1 } ) = 0$ , because of elitist selection. Hence,

$$
E [ d ( \xi _ { k } ) - d ( \xi _ { k + 1 } ) \mid d ( \xi _ { k } ) = n ] \leq n \left( { \frac { 1 } { n } } \right) ^ { n } .
$$

Let $h _ { 1 } ( n ) = n ^ { n - 1 }$ , then Codintion 6 holds.

According to Theorem 4, we have $E [ \tau ] = \Omega ( n ^ { n } )$ .

# 4 Drift Conditions for Exponential Average Computation Time

# 4.1 Drift Conditions

In this subsection, we investigate the drift conditions under which EAs will take the average time exponential in the problem size $n$ to find the optimal solution. Our analysis is based on Hajek's earlier work [16].

In order to consider the case where an EA might not be able to find the exact optimal solution, but only an approximate solution, define the stopping time $\tau$ of an EA as: $\tau = \operatorname* { m i n } \{ k : d ( \xi _ { k } ) \leq d _ { b } \}$ where $d _ { b } \geq 0$ .

Condition 7 For any population $X$ with $d _ { b } < d ( X ) < d _ { a }$ , where $d _ { b } \geq 0$ and $d \sb a > 0$ ,

$$
E [ e ^ { - ( d ( \xi _ { k + 1 } ) - d ( \xi _ { k } ) ) } \mid \xi _ { k } = X , d _ { b } < d ( \xi _ { k } ) < d _ { a } ] \leq \rho < 1 ,
$$

where $\rho > 0$ is a constant.

This condition indicates that $( d _ { b } , d _ { a } )$ is a very diffcult interval to search. When the condition is satisfied, $d ( \xi _ { k + 1 } ) > d ( \xi _ { k } )$ . In other words, the offspring population is on average drifting away from the optimal solution, rather than getting closer to it.

Condition 8 For any population $X$ with $d ( X ) \geq d _ { a } , d _ { a } > 0$ ,

$$
E [ e ^ { - ( d ( \xi _ { k + 1 } ) - d _ { a } ) } \mid \xi _ { k } = X , d ( \xi _ { k } ) \geq d _ { a } ] \leq D ,
$$

where $D \geq 1$ is a constant.

The above condition indicates that a population in the interval $[ d _ { a } , + \infty )$ will not, on average, drift towards the optimal solution too much because $\left( d ( \xi _ { k + 1 } ) \right) \geq d _ { a } - \ln D$ .

Given the above two conditions, the following lemma and theorem can be shown by following Hajek's work on drift analysis [16].

Lemma 1 If $\{ d ( \xi _ { k } ) ; k = 0 , 1 , \cdot \cdot \cdot \}$ satisfies Conditions 7 and $\boldsymbol { \vartheta }$ , then forninal populan $\xi _ { 0 }$

$$
E \left[ e ^ { - d \left( \xi _ { k } \right) } \mid \tau > k - 1 , d \left( \xi _ { 0 } \right) \right] \leq \rho ^ { k } e ^ { - d \left( \xi _ { 0 } \right) } + \frac { 1 - \rho ^ { k } } { 1 - \rho } D e ^ { - d { \mathfrak a } } ,
$$

and

$$
P [ d ( \xi _ { k } ) \leq d _ { b } \ | \ \tau > k - 1 , d ( \xi _ { 0 } ) ] \leq \rho ^ { k } e ^ { - ( d ( \xi _ { 0 } ) - d _ { b } ) } + \frac { 1 - \rho ^ { k } } { 1 - \rho } D e ^ { - ( d _ { a } - d _ { b } ) } .
$$

Proof: Inequality (11) is clearly true for $k = 0$ .

For $k \geq 0$ and $\tau > k$ ,

$$
E [ e ^ { - d ( \xi _ { k + 1 } ) } \mid \tau > k , d ( \xi _ { 0 } ) ] = E [ E [ e ^ { - d ( \xi _ { k + 1 } ) } \mid \tau > k , d ( \xi _ { k } ) ] \mid d ( \xi _ { 0 } ) ] ,
$$

where

$$
\begin{array} { r l } & { E [ e ^ { - d ( \xi _ { k + 1 } ) } \mid \tau > k , d ( \xi _ { k } ) ] } \\ { = } & { E [ e ^ { - d ( \xi _ { k + 1 } ) } \mid \tau > k , d ( \xi _ { k } ) \ge d _ { a } ] + E [ e ^ { - d ( \xi _ { k + 1 } ) } \mid \tau > k , d ( \xi _ { k } ) < d _ { a } ] . } \end{array}
$$

The first term on the right-hand side of inequality (13) is upper-bounded by $D e ^ { - d _ { a } }$ according to Condition 8, and the second term is upper-bounded by $\dot { \rho } e ^ { - d ( \bar { \xi } _ { k } ) }$ according to Condition 7. Using these bounds we can arrive at

$$
E [ e ^ { - d ( \xi _ { k + 1 } ) } \mid \tau > k , d ( \xi _ { 0 } ) ] \leq \rho E [ e ^ { - d ( \xi _ { k } ) } \mid \tau > k - 1 , d ( \xi _ { 0 } ) ] + D e ^ { - d _ { a } } .
$$

By induction on $k$ , it is easy to show that the above inequality implies inequality (11) for all $k \geq 0$ .

Inequality (12) follows from inequality (11):

$$
\begin{array} { r l } & { E [ e ^ { - ( d ( \xi _ { k } ) - d _ { b } ) } \mid \tau > k - 1 , d ( \xi _ { 0 } ) ] } \\ { = } & { E [ E [ e ^ { - ( d ( \xi _ { k } ) - d _ { b } ) } \mid \tau > k - 1 , d ( \xi _ { k } ) \le d _ { b } ] \mid d ( \xi _ { 0 } ) ] } \\ & { + E [ E [ e ^ { - ( d ( \xi _ { k } ) - d _ { b } ) } \mid \tau > k - 1 , d ( \xi _ { k } ) > d _ { b } ] \mid d ( \xi _ { 0 } ) ] } \\ { \ge } & { E [ E [ e ^ { - ( d ( \xi _ { k } ) - d _ { b } ) } \mid \tau > k - 1 , d ( \xi _ { k } ) \le d _ { b } ] \mid d ( \xi _ { 0 } ) ] } \\ { \ge } & { e ^ { 0 } P ( d ( \xi _ { k } ) \le d _ { b } \mid \tau > k - 1 , d ( \xi _ { 0 } ) ) . } \end{array}
$$

That is,

$$
\begin{array} { r } { P \left( d ( \xi _ { k } ) \leq d _ { b } \mid \tau > k - 1 , d ( \xi _ { 0 } ) \right) \leq E [ e ^ { - \left( d ( \xi _ { k } ) - d _ { b } \right) } \mid \tau > k - 1 , d ( \xi _ { 0 } ) ] . } \end{array}
$$

According to inequality (11) we have

$$
P ( d ( \xi _ { k } ) \le d _ { b } \ | \ d ( \xi _ { 0 } ) \ge d _ { a } ) \le \rho ^ { k } e ^ { - ( d ( \xi _ { 0 } ) - d _ { b } ) } + \frac { 1 - \rho ^ { k } } { 1 - \rho } D e ^ { - ( d _ { a } - d _ { b } ) } .
$$

The following theorem is the main result of this section.

Theorem 10 Assume Conditions 7 and 8 hold. If $d ( \xi _ { 0 } ) \ge d _ { a }$ , $D \geq 1$ and $\rho < 1$ , then there exist some $\delta _ { 1 } > 0$ and $\delta _ { 2 } > 0$ such that

$$
E [ \tau \mid d ( \xi _ { 0 } ) \geq d _ { a } ] \geq \delta _ { 1 } e ^ { \delta _ { 2 } ( d _ { a } - d _ { b } ) }
$$

Proof: Because $d ( \xi _ { 0 } ) \ge d _ { a }$ , we have

$$
e ^ { - ( d ( \xi _ { 0 } ) - d _ { b } ) } \leq e ^ { - ( d _ { a } - d _ { b } ) } .
$$

Since $D \geq 1$ and $\rho < 1$ , we can obtain

$$
\rho ^ { k } e ^ { - ( d ( \xi _ { 0 } ) - d _ { b } ) } \leq \frac { \rho ^ { k } } { 1 - \rho } D e ^ { - ( d _ { a } - d _ { b } ) } .
$$

According to inequality (12) and the above inequality,

$$
P ( d ( \xi _ { k } ) \le d _ { b } \mid \tau > k - 1 , d ( \xi _ { 0 } ) ) \le \frac { 1 } { 1 - \rho } D e ^ { - \left( d _ { a } - d _ { b } \right) } .
$$

By using the fact that $P ( \tau = k \mid d ( \xi _ { 0 } ) ) = P ( d ( \xi _ { k } ) \le d _ { b } , \tau > k - 1 \mid d ( \xi _ { 0 } ) )$ , we have

$$
\begin{array} { l l l } { P ( \tau > k \mid d ( \xi _ { 0 } ) ) } & { = } & { 1 - \displaystyle \sum _ { j = 1 } ^ { k } P ( \tau = j \mid d ( \xi _ { 0 } ) ) } \\ & { \ge } & { \operatorname* { m a x } \left( 0 , 1 - k \frac { D e ^ { - ( d _ { a } - d _ { b } ) } } { 1 - \rho } \right) . } \end{array}
$$

Therefore

$$
\begin{array} { r c l } { \displaystyle E [ \tau \mid d ( \xi _ { 0 } ) ] } & { = } & { \displaystyle \sum _ { j = 1 } ^ { + \infty } P ( \tau > j \mid d ( \xi _ { 0 } ) ) } \\ & & { \displaystyle \ge } & { \displaystyle \sum _ { k = 0 } ^ { + \infty } \operatorname* { m a x } _ { h = 0 } \left( 0 , 1 - k \frac { D e ^ { - ( d _ { a } - d _ { b } ) } } { 1 - \rho } \right) } \\ & { \displaystyle \ge } & { \displaystyle \frac { 1 - \rho } { 2 D } e ^ { d _ { a } - d _ { b } } . } \end{array}
$$

$\begin{array} { r } { \delta _ { 1 } = \frac { 1 - \rho } { 2 D } } \end{array}$ $\delta _ { 2 } = 1$

$$
E [ \tau \mid d ( \xi _ { 0 } ) \geq d _ { a } ] \geq \delta _ { 1 } e ^ { \delta _ { 2 } ( d _ { a } - d _ { b } ) } .
$$

# 4.2 The Subset Sum Problem Revisited

In this subsection, we consider another family of subset sum problems. We will show that some EAs described in this subsection take at least an exponential time on average to find the optimal solution.

The family of subset sum problems that we focus on in this subsection is $\{ W _ { 1 } , W _ { 2 } , \cdot \cdot \cdot , W _ { n } , \cdot \cdot \cdot \}$ , where

$$
W _ { n } = \{ w _ { 1 } , \cdots , w _ { n } \} ,
$$

$w _ { 1 } , w _ { 2 } , \cdots , w _ { n - 1 }$ are positives greater than $2 , w _ { n } = \sum _ { i = 1 } ^ { n - 1 } w _ { i } - 1 ;$

and

$$
C = w _ { n } .
$$

It is easy to see that the subset $\left\{ w _ { n } \right\}$ is the unique optimal solution and any subset of $W _ { n } - \{ w _ { n } \}$ is a feasible solution. This is a deceptive problem.

The EA used to solve the above family of problems follows the framework given in section 2 The crossover, mutation and selection are implemented as follows.

$x ~ = ~ ( s _ { 1 } ^ { ( x ) } \cdot \cdot \cdot s _ { n } ^ { ( x ) } )$ and $y =$ $( s _ { 1 } ^ { ( y ) } \cdot \cdot \cdot s _ { n } ^ { ( y ) } )$ from population $\xi _ { k }$ , choose a crossover point $m \in \{ 1 , \cdots , n - 1 \}$ at random and exchange all bits from the $m ^ { t h }$ bit between two individuals to form two new individuals $x ^ { \prime }$ and $y ^ { \prime }$ .

$$
\begin{array} { r c l } { { x ^ { \prime } } } & { { = } } & { { ( s _ { 1 } ^ { ( x ) } \cdot \cdot \cdot s _ { m - 1 } ^ { ( x ) } s _ { m } ^ { ( y ) } s _ { m + 1 } ^ { ( y ) } \cdot \cdot \cdot s _ { n } ^ { ( y ) } ) } } \\ { { y ^ { \prime } } } & { { = } } & { { ( s _ { 1 } ^ { ( y ) } \cdot \cdot \cdot s _ { m - 1 } ^ { ( y ) } s _ { m } ^ { ( x ) } s _ { m + 1 } ^ { ( x ) } \cdot \cdot \cdot s _ { n } ^ { ( x ) } ) } } \end{array}
$$

If an offspring is infeasible, one of the parents will be retained. A new intermediate populatior $\xi _ { k + C }$ of $2 N$ individuals will be formed after crossover.

Bit mutation is used in the EA. Given an individual $x = \left( s _ { 1 } \cdots s _ { n } \right) $ in $\xi _ { k + C }$ , choose a single bit $s _ { i }$ at random from it and flip the bit. If the offspring is infeasible, the parent will be retained. Another new intermediate population $\xi _ { k + M }$ of $2 N$ individuals is formed after mutation.

Selection in the EA can be regarded as a simple form of ranking. $2 N$ individuals are selected from $\xi _ { k }$ and $\xi _ { k + M }$ as follows: the best $2 N$ individuals are assigned a survival probability of $( 1 -$ $e ^ { - n } ) / 2 N$ each, and the worst $2 N$ individuals are assigned a survival probability of $e ^ { - n } / 2 N$ each. Yet another new intermediate population $\xi _ { k + S }$ of $2 N$ individuals is formed after selection. It should be noted that the selection used here is similar to but not the same as that used in Section 3.2. The chromosome representation used is the same as that described in Section 3.2.

Define

$$
d ( x ) = \lvert \sum _ { i = 1 } ^ { n } s _ { i } - 1 \rvert
$$

and

$$
d _ { \mathrm { m a x } } = \operatorname* { m a x } \{ d ( x ) ; x { \mathrm { ~ i s ~ a ~ f e a s i b l e ~ s o l u t i o n } } \} .
$$

Note that the distance is a pseudo-distance.

Given two individuals $x _ { 1 }$ and $x _ { 2 }$ with $d ( x _ { 1 } ) > d ( x _ { 2 } ) > 2$ , the fitness of $x _ { 1 }$ will be higher than that of $x _ { 2 }$ , that is $f ( x _ { 1 } ) > f ( x _ { 2 } )$ .

Let $\tau = \operatorname* { m i n } \{ k ; d ( \xi _ { k } ) = 0 \}$ , $d _ { a } = d _ { \operatorname* { m a x } } = n - 2$ $d _ { b } = 3 n / 4$ , and $\tau ^ { \prime } = \operatorname* { m i n } \{ k ; d ( \xi _ { k } ) \leq d _ { b } \}$ Obviously $E [ \tau ] \geq E [ \tau ^ { \prime } ]$ . The following theorem gives the main result of this section.

Theorem 11 For the random sequence, $\{ d ( \xi _ { k } ) ; k = 0 , 1 , \cdot \cdot \cdot \}$ , defined by the family of subset sum problems and the EA in this section, if $d ( \xi _ { 0 } ) \ge d _ { a }$ , then there exist two constants $\delta _ { 1 } > 0$ and $\delta _ { 2 } > 0$ such that

$$
E [ \tau \mid d ( \xi _ { 0 } ) \ge d _ { a } ] \ge \delta _ { 1 } \exp ( \delta _ { 2 } n )
$$

for sufficiently large $n$ .

Proof: According to Theorem 10, all we we need to show is to verify that Conditions 7 and 8 are satisfied.

First we show that Condition 7 can be satisfied, i.e.,

$$
E [ e ^ { - ( d ( \xi _ { k + 1 } ) - d ( \xi _ { k } ) ) } \mid d _ { b } < d ( \xi _ { k } ) < d _ { a } ] \leq \rho < 1 .
$$

After the crossover, one of the following three events may happen: event $I \{ d ( \xi _ { k + C } ) < d ( \xi _ { k } ) \}$ event $I \{ d ( \xi _ { k + C } ) = d ( \xi _ { k } ) \}$ or event $I \{ d ( \xi _ { k + C } ) > d ( \xi _ { k } ) \}$ .

Let $x _ { 1 }$ and $x _ { 2 }$ be two individuals in population $\xi _ { k }$ . Since crossover does not increase or decrease the amount of ones in individuals $x _ { 1 }$ and $x _ { 2 }$ , so event $I \{ d ( \xi _ { k + C } ) > d ( \xi _ { k } ) ) \}$ cannot happen.

Because $d ( \xi _ { k } ) > d _ { b } = 3 n / 4$ , $x _ { 1 }$ and $x _ { 2 }$ cannot be the optimal solution. Both of their $n ^ { t h }$ bits will be 0. The bits will still be 0 after crossover. Let $y _ { 1 }$ and $y _ { 2 }$ be offspring of $x _ { 1 }$ and $x _ { 2 }$ , we have $d ( y _ { 1 } ) > n / 4$ and $d ( y _ { 2 } ) > n / 4$ . Therefore, $d ( \xi _ { k + C } ) > n / 4$ ,

$$
\mid d ( \xi _ { k + C } ) - d ( \xi _ { k } ) \mid \leq { \frac { 3 n } { 4 } } - { \frac { n } { 4 } } + 1 = { \frac { n } { 2 } } + 1 .
$$

Assume that either event $I \{ d ( \xi _ { k + C } ) < d ( \xi _ { k } ) \}$ or event $I \{ d ( \xi _ { k + C } ) = d ( \xi _ { k } ) \}$ has happened. In either case, one of the following three events may happen after mutation: event $I \{ d ( \xi _ { k + M } ) <$ $d ( \xi _ { k + C } ) \}$ , event $I \{ d ( \xi _ { k + M } ) = d ( \xi _ { k + C } ) \}$ , or event $I \{ d ( \xi _ { k + M } ) > d ( \xi _ { k + C } ) \}$ . Since $d ( \xi _ { k + C } ) > n / 4$ , $d ( \xi _ { k + M } ) > n / 4 - 1 > 2$ .

As regard to the impact of selection on the drift, it is easy to see that

$$
\begin{array} { r c l } { { P ( d ( \xi _ { k + S } ) > d ( \xi _ { k } ) \mid 2 < d ( \xi _ { k } ) < d ( \xi _ { k + M } ) ) } } & { { \geq } } & { { ( \displaystyle \frac { 1 } { 2 N } ( 1 - e ^ { - n } ) ) ^ { 2 N } } } \\ { { } } & { { > } } & { { ( \displaystyle \frac { 1 - e ^ { - 1 } } { 2 N } ) ^ { 2 N } , } } \end{array}
$$

and

$$
P ( d ( \xi _ { k + S } ) < d ( \xi _ { k } ) \mid d ( \xi _ { k } ) > d ( \xi _ { k + M } ) > 2 ) \le \frac { 1 } { 2 N } e ^ { - n } .
$$

Summarizing all the above events, we have

$$
\begin{array} { r l } & { ~ E [ \{ \alpha \{ \hat { q } _ { k + 1 } \} , ~ \hat { q } _ { k } \} ] } \\ { = } & { ~ E [ \{ \alpha \{ \hat { q } _ { k + 1 } \} , ~ \hat { q } _ { k } \} ] } \\ &  ~ { \small \textsc { [ f i } ( \hat { \xi } _ { k + 1 } ) , ~ \hat { q } _ { k } \} ] } \\ &  ~ { \small \textsc { [ f i } ( \hat { \xi } _ { k + 1 } ) , ~ \hat { q } _ { k } \} ] } \\ &  ~ { \small \textsc { [ f i } ( \hat { \xi } _ { k + 1 } ) , ~ \hat { q } _ { k } \} ] } \\ &  ~ { \small \textsc { [ f i } ( \hat { \xi } _ { k + 1 } ) , ~ \hat { q } _ { k } \} ] } \\ &  ~ { \small \textsc { [ f i } ( \hat { \xi } _ { k + 1 } ) , ~ \hat { q } _ { k } \} ] } \\ &  ~ { \small \textsc { [ f i } ( \hat { \xi } _ { k + 1 } ) , ~ \hat { q } _ { k } \} ] } \\ &  ~ { \small \textsc { [ f i } ( \hat { \xi } _ { k + 1 } ) , ~ \hat { q } _ { k } \} ] } \\ &  ~ { \small \textsc { [ f i } ( \hat { \xi } _ { k + 1 } ) , ~ \hat { q } _ { k } \} ] } \\ &  ~ { \small \textsc { [ f i } ( \hat { \xi } _ { k + 1 } ) , ~ \hat { q } _ { k } \} ] } \\ &  ~ { \small \textsc { [ f i } ( \hat { \xi } _ { k + 1 } ) , ~ \hat { q } _ { k } \} ] } \\ &  ~ { \small \textsc { [ f i } ( \hat { \xi } _ { k + 1 } ) , ~ \hat { q } _ { k } \} ] } \\ &  ~ { \small \textsc { [ f i } ( \hat { \xi } _ { k + 1 } ) , ~ \hat { q } _ { k } \} ] } \\ &  ~ { \small \textsc { [ f i } ( \hat { \xi } _ { k + 1 } ) , ~ \hat { q } _ { k } \} } \\ &  ~ { \small \textsc { [ f i } ( \hat { \xi } _ { k + 1 } ) , ~ \hat { q } _ { k } \} ] \left( \hat { \xi } _ { k + 1 } , \hat { q } _ { k } \right) , d \{ \xi _ { k + 1 } \} ~ { \small \textsc { d } } _ { k } } \\ &  ~  \small \textsc { [ f i } ( \hat { \xi } _ { k + 1 } ) , \end{array}
$$

$$
\begin{array} { r l } & { \quad - \lambda _ { 1 } ^ { \mathrm { ~ i ~ j ~ } } \frac { \partial \lambda _ { 1 } } { \partial x _ { 2 } } \left( \lambda _ { 2 } ^ { \mathrm { ~ j ~ } } - \lambda _ { 1 } ^ { \mathrm { ~ j ~ } } \right) } \\ & { = \sqrt { \left( \lambda _ { 1 } ^ { ~ j ~ } + \lambda _ { 2 } ^ { \mathrm { ~ j ~ } } \right) } } \\ & { \quad - \lambda _ { 1 } ^ { \mathrm { ~ i ~ j ~ } } \frac { \partial \lambda _ { 1 } } { \partial x _ { 2 } } \sum _ { \alpha \leq i \leq 1 } ^ { \mathrm { ~ j ~ } } \lambda _ { 1 } ( \lambda _ { 1 } ^ { \mathrm { ~ j ~ } } + \lambda _ { 2 } ^ { \mathrm { ~ j ~ } } ) \lambda _ { 1 } ( \lambda _ { 1 } ^ { \mathrm { ~ j ~ } } - \lambda _ { 1 } ^ { \mathrm { ~ j ~ } } ) \lambda _ { 2 } ^ { \mathrm { ~ j ~ } } \left( \lambda _ { 1 } ^ { ~ j } + \lambda _ { 2 } ^ { \mathrm { ~ j } } \right) \lambda _ { 1 } ( \lambda _ { 1 } ^ { \mathrm { ~ j ~ } } - \lambda _ { 1 } ^ { \mathrm { ~ j ~ } } ) } \\ & { \quad - \lambda _ { 1 } ^ { \mathrm { ~ i ~ j ~ } } \frac { \partial \lambda _ { 1 } } { \partial x _ { 2 } } \sum _ { \alpha \leq i \leq 1 } ^ { \mathrm { ~ j ~ } } \lambda _ { 1 } ( \lambda _ { 1 } ^ { \mathrm { ~ j ~ } } - \lambda _ { 1 } ^ { \mathrm { ~ j ~ } } ) \lambda _ { 1 } ( \lambda _ { 1 } ^ { \mathrm { ~ j ~ } } - \lambda _ { 2 } ^ { \mathrm { ~ j ~ } } ) \lambda _ { 1 } ( \lambda _ { 1 } ^ { \mathrm { ~ j ~ } } - \lambda _ { 2 } ^ { \mathrm { ~ j ~ } } ) \lambda _ { 1 } ( \lambda _ { 1 } ^ { \mathrm { ~ j ~ } } - \lambda _ { 1 } ^ { \mathrm { ~ j ~ } } ) } \\ &  \quad + \lambda _ { 1 } ^ { \mathrm { ~ i ~ j ~ } } \frac { \partial \lambda _ { 1 } } { \partial x _ { 2 } } \sum _ { \alpha \leq i \leq 1 } ^ { \mathrm { ~ j ~ } } \lambda _ { 1 } ( \lambda _ { 1 } ^ { \mathrm { ~ j ~ } } - \lambda _ { 1 } ^ { \mathrm { ~ j ~ } } ) \lambda _ { 1 } ( \lambda _ { 1 } ^ { \mathrm { ~ j ~ } } - \lambda _ { 2 } ^  \end{array}
$$

Let

$$
\begin{array} { r l } & { p _ { 1 } = P ( d ( \xi _ { k + S } ) > d ( \xi _ { k + M } ) \mid d ( \xi _ { k + C } ) < d ( \xi _ { k } ) , d ( \xi _ { k + M } ) < d ( \xi _ { k + C } ) , d ( \xi _ { k + C } ) , d ( \xi _ { k } ) > d _ { b } ) , } \\ & { p _ { 2 } = P ( d ( \xi _ { k + S } ) > d ( \xi _ { k + M } ) \mid d ( \xi _ { k + C } ) < d ( \xi _ { k } ) , d ( \xi _ { k + M } ) = d ( \xi _ { k + C } ) , d ( \xi _ { k } ) > d _ { b } ) , } \\ & { p _ { 3 } = P ( d ( \xi _ { k + S } ) > d ( \xi _ { k + M } ) \mid d ( \xi _ { k + C } ) < d ( \xi _ { k } ) , d ( \xi _ { k + M } ) > d ( \xi _ { k + C } ) , d ( \xi _ { k + C } ) , d ( \xi _ { k } ) > \ d _ { b } ) , } \\ & { p _ { 4 } = P ( d ( \xi _ { k + S } ) > d ( \xi _ { k + M } ) \mid d ( \xi _ { k + C } ) = d ( \xi _ { k } ) , d ( \xi _ { k + M } ) < d ( \xi _ { k + C } ) , d ( \xi _ { k + C } ) , d ( \xi _ { k } ) > d _ { b } ) , } \\ & { p _ { 5 } = P ( d ( \xi _ { k + S } ) > d ( \xi _ { k + M } ) \mid d ( \xi _ { k + C } ) = d ( \xi _ { k } ) , d ( \xi _ { k + M } ) = d ( \xi _ { k } ) , d ( \xi _ { k + C } ) , d ( \xi _ { k } ) > d _ { b } ) , } \\ &  \bullet = \textup {  {  {  {  {  {  {  { \vert } } } } } } } } \lambda \times \textup {  {  {  {  {  {  {  { \vert } } } } } } } \lambda \lambda \{  {  {  {  {  {  {  {  } } } } } } } \lambda \lambda  {  {  {  {  {  } } } } } \lambda  {  {  {  {  } } } } \lambda  {  {  {  } } } } \end{array} ,
$$

$$
p _ { 6 } = P ( d ( \xi _ { k + S } ) > d ( \xi _ { k + M } ) \mid d ( \xi _ { k + C } ) = d ( \xi _ { k } ) , d ( \xi _ { k + M } ) > d ( \xi _ { k + C } ) , d ( \xi _ { k } ) > d _ { b } )
$$

where $p _ { 1 } , \cdots , p _ { 6 }$ are all greater than $\Big ( \frac { 1 - e ^ { - 1 } } { 2 N } \Big ) ^ { 2 N }$ Th   a drifting away from the optimal solution after selection.

According to Eq.(15) and the above analysis, we have

$$
\begin{array} { r l } & { E [ e ^ { - ( d ( \xi _ { k + 1 } ) - d ( \xi _ { k } ) ) } \mid d ( \xi _ { k } ) > d _ { b } ] } \\ { \leq } & { e ^ { n / 2 + 1 } P ( d ( \xi _ { k + C } ) < d ( \xi _ { k } ) , d ( \xi _ { k + M } ) < d ( \xi _ { k + C } ) \mid d ( \xi _ { k } ) > d _ { b } ) O ( e ^ { - n } ) } \\ & { + e ^ { 0 } P ( d ( \xi _ { k + C } ) < d ( \xi _ { k } ) , d ( \xi _ { k + M } ) < d ( \xi _ { k + C } ) \mid d ( \xi _ { k } ) > d _ { b } ) ( 1 - p _ { 1 } ) } \\ & { + e ^ { - 1 } P ( d ( \xi _ { k + C } ) < d ( \xi _ { k } ) , d ( \xi _ { k + M } ) < d ( \xi _ { k + C } ) \mid d ( \xi _ { k } ) > d _ { b } ) p _ { 1 } } \end{array}
$$

$$
\begin{array} { r l } & { \quad _ { 1 } \omega ^ { ( 2 ) + 1 } P _ { i } ( \{ \Phi _ { i } \} \leq \hat { C } _ { i } ^ { ( 1 ) } , \hat { C } _ { i } ^ { ( 1 ) } , \hat { C } _ { i } ^ { ( 1 ) } , \hat { C } _ { i } ^ { ( 1 ) } , \hat { C } _ { i } ^ { ( 1 ) } , \hat { C } _ { i } ^ { ( 1 ) } , \hat { C } _ { i } ^ { ( 1 ) } , \hat { C } _ { i } ^ { ( 1 ) } , \hat { C } _ { i } ^ { ( 1 ) } , \hat { C } _ { i } ^ { ( 1 ) } , \hat { C } _ { i } ^ { ( 1 ) } , \hat { C } _ { i } ^ { ( 1 ) } , \hat { C } _ { i } ^ { ( 1 ) } , } \\ & { \quad _ { 1 } \omega ^ { ( 3 ) } \hat { C } _ { i } \hat { C } _ { i } \hat { C } _ { j } \leq \hat { C } _ { i } \hat { C } _ { i } \hat { C } _ { j } \} \hat { C } _ { i } \hat { C } _ { j } \hat { C } _ { j } - \hat { C } _ { i } \hat { C } _ { i } \hat { C } _ { j } \hat { C } _ { j } \hat { C } _ { j } \hat { C } _ { j } \hat { C } _ { j } \hat { C } _ { j } \hat { C } _ { j } \hat { C } _ { j } \hat { C } _ { j } \hat { C } _ { j } \hat { C } _ { j } \hat { C } _ { j } \hat { C } _ { j } } \\ & { \quad _ { 1 } + \omega ^ { ( 1 ) } P _ { i } ( \{ C } _ { i } \hat { C } _ { i } \hat { C } _ { i } ^ { ( 1 ) } , \hat { C } _ { i } ^ { ( 1 ) } , \hat { C } _ { i } ^ { ( 1 ) } , \hat { C } _ { i } ^ { ( 1 ) } , \hat { C } _ { i } ^ { ( 1 ) } , \hat { C } _ { i } ^ { ( 1 ) } , \hat { C } _ { j } ^ { ( 1 ) } , \hat { C } _ { i } ^ { ( 1 ) } , \hat { C } _ { j } ^ { ( 1 ) } ,  \\ &  \quad _ { 1 } + \omega ^ { ( 1 ) } P _ { i } ( \{ \Phi _ { i } \} \leq \hat { C } _ { i } \hat { C } _ { j } \hat { C } _ { j } \hat { C } _ { j } \hat { C } _ { j } \hat { C } _ { j } \end{array}
$$

Let

$$
\begin{array} { r l } & { q _ { 1 } = P \big ( d ( \xi _ { k + C } ) < d ( \xi _ { k } ) , d ( \xi _ { k + M } ) < d ( \xi _ { k + C } ) \mid d ( \xi _ { k } ) > d _ { b } \big ) , } \\ & { q _ { 2 } = P \big ( d ( \xi _ { k + C } ) < d ( \xi _ { k } ) , d ( \xi _ { k + M } ) = d ( \xi _ { k + C } ) \mid d ( \xi _ { k } ) > d _ { b } \big ) , } \\ & { q _ { 3 } = P \big ( d ( \xi _ { k + C } ) < d ( \xi _ { k } ) , d ( \xi _ { k + M } ) > d ( \xi _ { k + C } ) \mid d ( \xi _ { k } ) > d _ { b } \big ) , } \\ & { q _ { 4 } = P \big ( d ( \xi _ { k + C } ) = d ( \xi _ { k } ) , d ( \xi _ { k + M } ) < d ( \xi _ { k + C } ) \mid d ( \xi _ { k } ) > d _ { b } \big ) , } \\ & { q _ { 5 } = P \big ( d ( \xi _ { k + C } ) = d ( \xi _ { k } ) , d ( \xi _ { k + M } ) = d ( \xi _ { k + C } ) \mid d ( \xi _ { k } ) > d _ { b } \big ) , } \\ & { q _ { 6 } = P \big ( d ( \xi _ { k + C } ) = d ( \xi _ { k } ) , d ( \xi _ { k + M } ) > d ( \xi _ { k + C } ) \mid d ( \xi _ { k } ) > d _ { b } \big ) . } \end{array}
$$

Since event $I \{ d ( \xi _ { k + C } ) > d ( \xi _ { k } ) \}$ cannot happen, we have

$$
\sum _ { i = 1 } ^ { 6 } q _ { i } = 1 .
$$

Now we arrive at

$$
\begin{array} { r l } & { E [ e ^ { - ( d ( \xi _ { k + 1 } ) - d ( \xi _ { k } ) ) } \mid d ( \xi _ { k } ) > d _ { b } ] } \\ { \leq } & { q _ { 1 } ( O ( e ^ { - n / 2 + 1 } ) + 1 - p _ { 1 } + e ^ { - 1 } p _ { 1 } ) } \\ & { + q _ { 2 } ( O ( e ^ { - n / 2 + 1 } ) + 1 - p _ { 2 } + e ^ { - 1 } p _ { 2 } ) } \\ & { + q _ { 3 } ( O ( e ^ { - n / 2 + 1 } ) + 1 - p _ { 3 } + e ^ { - 1 } p _ { 3 } ) } \\ & { + q _ { 4 } ( O ( e ^ { - n / 2 + 1 } ) + 1 - p _ { 4 } + e ^ { - 1 } p _ { 4 } ) } \\ & { + q _ { 5 } ( O ( e ^ { - n / 2 + 1 } ) + 1 - p _ { 5 } + e ^ { - 1 } p _ { 5 } ) } \\ & { + q _ { 6 } ( O ( e ^ { - n / 2 + 1 } ) + 1 - p _ { 6 } + e ^ { - 1 } p _ { 6 } ) . } \end{array}
$$

therine $1 - p _ { i } + e ^ { - 1 } p _ { i } < 1$ b $\textstyle \sum _ { i = 1 } ^ { 6 } q _ { i } = 1$ ad $\begin{array} { r } { \operatorname* { l i m } _ { n \to \infty } O ( e ^ { - n / 2 + 1 } ) = 0 } \end{array}$ , for sufiently large $n$ $\rho < 1$

$$
\begin{array} { l l } { { } } & { { E [ e ^ { - ( d ( \xi _ { k + 1 } ) - d ( \xi _ { k } ) ) } \mid d ( \xi _ { k } ) > d _ { b } ] } } \\ { { \leq } } & { { \displaystyle \sum _ { i = 1 } ^ { 6 } q _ { i } ( O ( e ^ { - n / 2 + 1 } ) + 1 - p _ { i } + e ^ { - 1 } p _ { i } ) } } \end{array}
$$

$$
\begin{array} { r l } { = } & { { } \displaystyle \sum _ { i = 1 } ^ { 6 } q _ { i } O ( e ^ { - n / 2 + 1 } ) + \sum _ { i = 1 } ^ { 6 } q _ { i } ( 1 - p _ { i } + e ^ { - 1 } p _ { i } ) } \\ { < } & { { } \displaystyle \rho < 1 . } \end{array}
$$

This shows that $\{ d ( \xi _ { k } ) ; k = 0 , 1 , \cdot \cdot \cdot \}$ satisfies Condition 7.

The following analysis shows that Condition 8 can also be satisfied.

Let population $\xi _ { k }$ have the property of $d ( \xi _ { k } ) = d _ { a } = d _ { \operatorname* { m a x } }$ , which implies that all individuals in the population are the same, i.e., $x _ { i } = ( 1 \cdots 1 0 )$ where $x _ { i }$ is an individual. Then the crossover has no influence on the drift, i.e., $d ( \xi _ { k + C } ) = d ( \xi _ { k } )$ .

There are only two events which may happen after mutation: (1) event $I \{ d ( \xi _ { k + M } ) < d ( \xi _ { k + C } ) \}$ , and (2) event $I \{ d ( \xi _ { k + M } ) = d ( \xi _ { k + C } ) \}$ . Event $I \{ d ( \xi _ { k + M } ) > d ( \xi _ { k + C } ) \}$ cannot happen as $d ( \xi _ { k + C } ) =$ $d _ { \mathrm { m a x } }$ .

Similarly, there are following two cases after selection: (1) event $I \{ d ( \xi _ { k + S } ) < d ( \xi _ { k } ) \}$ , and (2) event $I \{ d ( \xi _ { k + S } ) = d ( \xi _ { k } ) \}$ . Let the probability of the first event's happening be $p _ { 0 }$ and that of the second be $1 - p _ { 0 }$ .

By summarizing all the above events, we have

$$
\begin{array} { r l } & { E [ e ^ { - ( d ( \xi _ { k + 1 } ) - d _ { a } ) } \mid d ( \xi _ { k } ) = d _ { a } ] } \\ { = } & { E [ e ^ { 0 } I \{ d ( \xi _ { k + S } ) < d ( \xi _ { k } ) , d ( \xi _ { k + M } ) = d ( \xi _ { k + C } ) \mid d ( \xi _ { k } ) = d _ { a } \} ] } \\ & { + E [ e ^ { 0 } I \{ d ( \xi _ { k } + S ) < d ( \xi _ { k } ) , d ( \xi _ { k + M } ) < d ( \xi _ { k + C } ) \mid d ( \xi _ { k } ) = d _ { a } \} ] } \\ & { + E [ e ^ { 1 } I \{ d ( \xi _ { k + S } ) = d ( \xi _ { k } ) , d ( \xi _ { k + M } ) < d ( \xi _ { k + C } ) \mid d ( \xi _ { k } ) = d _ { a } \} ] } \\ { \leq } & { e ^ { 0 } + e ^ { 0 } p _ { 0 } + e ^ { 1 } ( 1 - p _ { 0 } ) } \\ { \leq } & { 2 + e . } \end{array}
$$

Let $D = 2 + e$ , we arrive at Condition 8.

According to Theorem 10 and the fact that

$$
d _ { a } - d _ { b } = n - 2 - 3 n / 4 = n / 4 - 2 ,
$$

there exist two positive numbers, $\delta _ { 1 }$ and $\delta _ { 2 }$ , such that

$$
E [ \tau \mid d ( \xi _ { 0 } ) \ge d _ { a } ] \ge E [ \tau ^ { \prime } \mid d ( \xi _ { 0 } ) \ge d _ { a } ] \ge \delta _ { 1 } e ^ { \delta _ { 2 } ( n / 4 - 2 ) } ,
$$

where $\delta _ { 1 }$ and $\delta _ { 2 }$ are independent of $n$ .

# 5 Discussion on Weaker Drift Conditions

Conditions 7 and 8 may not be easy to understand and verify for some applications, e.g., the subset sum problem. The question now is whether we could come up with some weaker and more intuitive drift conditions. This section discusses such conditions.

Assume that a distance function $d ( x )$ has been defined. Let $d _ { \operatorname* { m a x } } = \operatorname* { m a x } \{ d ( x ) : x \in X \}$ , and $d _ { b }$ and $d _ { a }$ be positive numbers such that $d _ { b } < d _ { a } \le d _ { \mathrm { m a x } }$ .

Condition 9 Let $X$ be a population such that $d _ { b } < d ( X ) < d _ { a }$ . Then

$$
E [ d ( \xi _ { k + 1 } ) - d ( \xi _ { k } ) \mid \xi _ { k } = X ] \geq C _ { 1 } ,
$$

where $C _ { 1 } > 0$ .

This condition is a simplified version of Condition 7. It implies that when a population $X$ is in the area $( d _ { a } , d _ { b } )$ , its offspring tends to drift away from, rather than move closer to, the optimal solution.

Condition 10 Let $X$ be a population such that $d ( X ) \geq d _ { a }$ . Then

$$
E [ d ( \xi _ { k + 1 } ) - d _ { a } \ | \ \xi _ { k } = X ] \ge - C _ { 2 } ,
$$

where $C _ { 2 } > 0$ .

This condition is a simplified version of Condition 8. It implies that for a population $X$ in the area $[ d _ { a } , + \infty )$ , its offsping will not drift too far away from $[ d _ { a } , + \infty )$ . The drift is bounded by $d _ { a } - C _ { 2 }$ .

An interesting question now is: Given a random sequence $\{ d ( \xi _ { k } ) ; k = 0 , 1 \cdots \}$ , generated by the EA for solving the subset sum problem, which satisfies Conditions 9 and 10, whether the average time $E [ \tau \mid \xi _ { 0 } = X ]$ is still at least exponential in the problem size $n$ starting from an initial population $X$ with $d ( X ) \geq d _ { a }$ ?

The answer to this question is negative. The two conditions are not sufficient to derive a positive answer although Condition 9 appears to imply a positive answer. We will show in the following using an example that the random sequence $\{ d ( \xi _ { k } ) ; k = 0 , 1 , \cdot \cdot \cdot \}$ satisfies both conditions, but EA's average computation time is polynomial in the problem size $n$ .

Consider a family of subset sum problems, $\{ W _ { 1 } , W _ { 2 } , \cdots , W _ { n } , \cdot \cdot \cdot \}$ , where

$$
W _ { n } = \{ w _ { 1 } , \cdots , w _ { n } \} ,
$$

$$
w _ { 1 } = w _ { 2 } = \cdot \cdot \cdot = w _ { n - 1 } = 2 n , w _ { n } = 2 n C _ { 0 } + 1 ,
$$

$$
C = 2 n C _ { 0 } + 1 ,
$$

where $C _ { 0 } \leq n / 2$ is an integer greater than 2.

It is obvious that the subset $\left\{ w _ { n } \right\}$ is the unique optimal solution. Any subset of $W _ { n } - \{ w _ { n } \}$ with no more than $C _ { 0 }$ elements is a feasible solution.

The EA for solving the above family of subset sum problems follows the framework given in Section 2, but its implementation is much simpler than the EAs used in previous sections. The same chromosome representation is used as before. The EA used here is a $( 1 + 1 )$ EA. It uses bit mutation. A single bit $s _ { i }$ is chosen at random from an individual and flipped. If the offspring is infeasible, the parent will be retained. A new intermediate population $\xi _ { k + M } = \{ y \}$ is formed after mutation.

In terms of selection, the individual with better fitness between $\xi _ { k }$ and $\xi _ { k + M }$ has a higher survival probability of $p$ , and that with worse fitness has a survival probability of $q = 1 - p$ ,where $p > q$ . The new intermediate population after selection will be $\xi _ { k + S } = \{ z \}$ .

Since $s ^ { * } = ( 0 \cdots 0 1 )$ is the optimal solution, define

$$
d ( x ) = \sum _ { i = 1 } ^ { n } \mid s _ { i } - s ^ { * } \mid , { \mathrm { ~ a n d } }
$$

$$
d _ { \mathrm { m a x } } = \operatorname* { m a x } \{ d ( x ) ; \ x { \mathrm { ~ i s ~ a ~ f e a s i b l e ~ s o l u t i o n } } \} .
$$

It is easy to see that if $d ( x _ { 1 } ) > d ( x _ { 2 } ) > 1$ , then $f \left( x _ { 1 } \right) > f \left( x _ { 2 } \right)$ .

Let $d _ { b } = 2$ and $d _ { a } = d _ { \operatorname* { m a x } }$ . We first verify that $\{ d ( \xi _ { k } ) ; k = 0 , 1 , \cdot \cdot \cdot \}$ satisfies Condition 9.

Let $\xi _ { k } ~ = ~ \{ x \}$ be the current population with $d _ { b } ~ < ~ d ( x ) ~ < ~ d _ { a }$ , and $\xi _ { k + M } ~ = ~ \{ y \}$ be the intermediate population after mutation. Then one of the following three events may happen: event $I \{ d ( y ) > d ( x ) \}$ , event $I \{ d ( y ) = d ( x ) \}$ or event $I \{ d ( y ) < d ( x ) \}$ .

S    l $I \{ d ( y ) >$ $d ( x ) \}$ happening is

$$
P ( d ( y ) > d ( x ) \mid d _ { b } < d ( x ) < d _ { a } ) = ( n - d ( x ) - 1 ) / n .
$$

The probability of event $I \{ d ( y ) = d ( x ) \}$ happening is

$$
P ( d ( y ) = d ( x ) \mid d _ { b } < d ( x ) < d _ { a } ) = 1 / n .
$$

The probability of event $I \{ d ( y ) < d ( x ) \}$ happening is

$$
P ( d ( y ) < d ( x ) \mid d _ { b } < d ( x ) < d _ { a } ) = d ( x ) / n .
$$

If event $I \{ d ( y ) < d ( x ) \}$ has happened, one of the following two events may happen: event $I \{ d ( z ) < d ( x ) \}$ or event $I \{ d ( z ) = d ( x ) \}$ . According to our selection scheme, the probability of event $I \{ d ( z ) = d ( x ) \}$ happening is $p$ and the probability of event $I \{ d ( z ) < d ( x ) \}$ happening is $q$ .

If event $I \{ d ( y ) > d ( x ) \}$ has happened, one of the following two events may happen: event $I \{ d ( z ) > d ( x ) \}$ or event $I \{ d ( z ) = d ( x ) \}$ . It is easy to see that the probability of event $I \{ d ( z ) >$ $d ( x ) \}$ happening is $p$ and the probability of event $I \{ d ( z ) = d ( x ) \}$ happening is $q$ .

Summarizing all the above events, we have

$$
\begin{array} { r l } & { E [ d ( \xi _ { k + 1 } ) - d ( \xi _ { k } ) \mid d _ { b } < d ( \xi _ { k } ) < d _ { a } ] } \\ { = } & { E [ ( d ( z ) - d ( x ) ) I \{ d ( y ) > d ( x ) , d ( z ) = d ( y ) \} \mid d _ { b } < d ( \xi _ { k } ) < d _ { a } ] } \\ & { + E [ ( d ( z ) - d ( x ) ) I \{ d ( y ) > d ( y ) , d ( z ) = d ( x ) \} \mid d _ { b } < d ( \xi _ { k } ) < d _ { a } ] } \\ & { + E [ ( d ( z ) - d ( x ) ) I \{ d ( y ) < d ( x ) , d ( z ) = d ( y ) \} \mid d _ { b } < d ( \xi _ { k } ) < d _ { a } ] } \\ & { + E [ ( d ( z ) - d ( x ) ) I \{ d ( y ) < d ( x ) , d ( z ) = d ( x ) \} \mid d _ { b } < d ( \xi _ { k } ) < d _ { a } ] } \\ { = } & { p \frac { n - d ( x ) - 1 } { n } - q \frac { d ( x ) } { n } } \\ { \geq } & { p \frac { n - d _ { a } - 1 } { n } - q \frac { d _ { a } } { n } . } \end{array}
$$

Since $d _ { a } = d _ { m a x } < C _ { 0 } \leq n / 2$ and $p > q$

$$
\begin{array} { r l } & { E [ d ( \xi _ { k + 1 } ) - d ( \xi _ { k } ) \mid d _ { b } < d ( \xi _ { k } ) < d _ { a } ] } \\ { \geq } & { p \frac { n - n / 2 - 1 } { n } - q \frac { n / 2 } { n } } \\ { \geq } & { \frac { 1 } { 4 } ( p - q ) } \end{array}
$$

vhen $n$ is sufficiently large. Let $C _ { 1 } = ( p - q ) / 4 > 0$ . Then Condition 9 is satisfied

Now we verify that $\{ d ( \xi _ { k } ) ; k = 0 , 1 , \cdot \cdot \cdot \}$ satisfies Condition 10.

From the definition of feasible solutions, we know that any subset with a cardinality greater than $C _ { 0 }$ is an infeasible solution. For any given individual $x$ with $d ( x ) = d _ { a } = d _ { \mathrm { m a x } }$ , let $y$ be its offspring after mutation. Then one of the following events may happen: event $I \{ d ( y ) = d _ { a } \}$ or event $I \{ d ( y ) < d _ { a } \}$ .

The probability of event $I \{ d ( y ) = d _ { a } \}$ happening is

$$
P ( d ( y ) = d ( x ) \mid d ( x ) = d _ { a } = d _ { m a x } ) = ( n - d _ { a } ) / n .
$$

The probability of event $I \{ d ( y ) < d _ { a } \}$ happening is

$$
P ( d ( y ) < d ( x ) \mid d ( x ) = d _ { a } = d _ { m a x } ) = d _ { a } / n .
$$

If event $I \{ d ( y ) = d _ { a } \}$ happens, then event $I \{ d ( z ) = d _ { a } \}$ happens with probability 1. If event $I \{ d ( y ) < d _ { a } \}$ happens, one of the following two may happen: event $I \{ d ( z ) = d _ { a } \}$ or event $I \{ d ( z ) < d _ { a } \}$ . It is clear that the probability of event $I \{ d ( z ) = d _ { a } \}$ happening is $p$ and the probability of event $I \{ d ( z ) < d _ { a } \}$ happening is $q$ .

Summarizing all the above events, we obtain

$$
\begin{array} { r l } & { E [ d ( \xi _ { k + 1 } ) - d _ { a } \ | \ d ( \xi _ { k } ) \geq d _ { a } ] } \\ { = } & { E [ ( d ( z ) - d _ { a } ) I \{ d ( z ) = d ( y ) , d ( y ) < d _ { a } \} \ | \ d ( \xi _ { k } ) \geq d _ { a } ] } \\ & { + E [ ( d ( z ) - d _ { a } ) I \{ d ( z ) = d _ { a } \} \ | \ d ( \xi _ { k } ) \geq d _ { a } ] } \\ { = } & { - q \frac { d _ { a } } { n } . } \end{array}
$$

Let $C _ { 2 } = q d _ { a } / n$ . Then Condition 10 is satisfied.

From the above analysis, we know that $\{ d ( \xi _ { k } ) ; k = 0 , 1 , \cdot \cdot \cdot \}$ satisfies Conditions 9 and 10. It appears that it would take at least an exponential time to reach the optimal solution. However, this is not the case. We can show that the EA's average computation time for solving the family of subset sum problems is polynomial in $n$ in spite of the fact that Conditions 9 and 10 can be satisfied.

Let $\xi _ { 0 }$ be any individual (feasible solution) with $d _ { b } < d ( \xi _ { 0 } ) \le d _ { \operatorname* { m a x } }$ , we will prove that

$$
P ( \xi _ { t = C _ { 0 } } = x ^ { * } \mid d _ { b } < d ( \xi _ { 0 } ) \le d _ { \operatorname* { m a x } } ) \ge \left( \frac { q } { n } \right) ^ { C _ { 0 } } q ,
$$

where $x ^ { * }$ represents the optimal population (i.e., solution).

According to the mutation defined in our EA, the probability of event $I \{ d ( \xi _ { k + M } ) < d ( \xi _ { k } ) \}$ happening is

$$
P ( d ( \xi _ { k + M } ) < d ( \xi _ { k } ) \mid d _ { b } < d ( \xi _ { k } ) \leq d _ { \operatorname* { m a x } } ) \geq { \frac { d ( x ) } { n } } \geq { \frac { 1 } { n } } .
$$

According to the selection, the probability of event $I \{ d ( \xi _ { k + 1 } ) = d ( \xi _ { k + M } ) \}$ happening is $q$ . So

$$
P ( d ( \xi _ { k + S } ) < d ( \xi _ { k } ) \mid d ( \xi _ { k + M } ) < d ( \xi _ { k } ) , d _ { b } < d ( \xi _ { k } ) \leq d _ { \operatorname* { m a x } } ) \geq \frac { q } { n } .
$$

Therefore

$$
\begin{array} { r l } & { P ( d ( \xi _ { t = C _ { 0 } } ) = 0 \mid d _ { b } < d ( \xi _ { 0 } ) \le d _ { \operatorname* { m a x } } ) } \\ { \ge } & { P ( \xi _ { t = C _ { 0 } } = x ^ { * } , I \{ d ( \xi _ { 0 } ) > d ( \xi _ { 1 } ) > d ( \xi _ { 2 } ) > \cdots > d ( \xi _ { t } ) \} \mid \xi _ { 0 } ) } \\ { \ge } & { \left( \frac { q } { n } \right) ^ { C _ { 0 } } q > 0 } \end{array}
$$

Since $\{ \xi _ { k } ; k = 0 , 1 , \cdot \cdot \cdot \}$ is homogeneous, we can obtain the following result:

$$
E [ \tau \mid \xi _ { 0 } ] = O ( n ^ { C _ { 0 } } ) .
$$

In other words, the average computation time to solve this family of problems is polynomial in the problem size.

# 6 Conclusions and Further Work

This paper presents a number of new results on the computational time complexity of EAs. It has established several general conditions under which EAs will have polynomial or exponential average time complexity. It also shows successfully how these general results can be applied to different problems.

This paper also introduces a new approach to analyzing EAs, i.e., by drift analysis. Instead of estimating the first hitting time directly (which may be difficult in some cases), we can estimate the drift (which may be easier) first and then use the result to derive the upper or lower bounds of the first hitting time. Using drift analysis, we have shown several important theorems. For example, Theorem 1 gives some general conditions under which an EA can solve a problem in polynomial time on average. Theorem 10 gives some general conditions under which an EA needs at least exponential computation time on average to solve a problem.

There are, however, much further work to be done to fully understand the computational time complexity of various EAs on different classes of problems.

1. This paper has assumed implicitly that the number of generations (or equivalently the number of fitness evaluations) is the most important factor in determining the order of EA's computation time. While this is true for a vast majority of EA applications where fitness evaluation is the most time consuming part of EA's execution time, it is possible in theory that the computation time of a single crossover, mutation and/or selection might be significant. In all EAs we considered in this paper, crossover and mutation only takes $O ( n )$ time and selection needs $O ( n \log n )$ , where $n$ is the problem size.

2. Algorithm parameters, e.g., mutation rate, may have a significant impact on the time complexity of an EA. It would be interesting to investigate how significant such impact is for different problems. In general, it would be quite interesting to investigate the average computation time of different EAs on a problem in order to gain some insights into the effectiveness and efficiency of different operators and parameter settings.

3. More strict drift conditions need to be studied in order to obtain tighter upper-bounds of the average computation time.

4. More analysis on well-known combinatorial problems, such as graph matching, should be carried out to gain more insights into the question where the real power of EAs is and when they are efficient.

# Acknowledgement

This work is partially supported by the State Key Laboratory of Software Engineering at Wuhan University, National Nature Science Foundation of China, the Australian Research Council, and the School of Computer Science, the University of Birmingham. Part of the work was done while the first author was visiting the School of Computer Science, University College, UNSW, ADFA, and the School of Computer Science, the University of Birmingham.

# Список литературы

[1] J. H. Holland, Adaptation in Natural and Artificial Systems (1st MIT Press Edn). Cambridge, MA: The MIT Press, 1992.   
[2] H.-P. Schwefel, Evolution and Optimum Seeking. New York, NY: John Wiley & Sons, 1995.   
[3] D. B. Fogel, System Identification Through Simulated Evolution: A Machine Learning Approach to Modeling. Needham Heights, MA: Ginn Press, 1991.   
[4] D. E. Goldberg, Genetic Algorithms in Search, Optimization, and Machine Learning. Reading, MA: Addison-Wesley, 1989.   
[5] Z. Michalewicz, Genetic Algorithms $^ +$ Data Structures $=$ Evolution Programs (3rd edition). Berlin, Germany: Springer-Verlag, 1996.   
[6] A. E. Eiben and G. Rudolph, "Theory of evolutionary algorithms: A bird eye view," Theoretical Computer Science, vol. 214, 1999.   
[7] G. Rudolph, "Finite Markov chain results in evolutionary computation: A tour d'Horizon," Fundamenta Informaticae, vol. 35, no. 1-4, pp. 6789, 1998.   
[8] B. K. Ambati, J. Ambati, and M. M. Mokhtar, "Heuristic combinatorial optimization by simulated Darwinian evolution: a polynomial time algorithm for the traveling salesman problem," Biological Cybernetics, vol. 65, pp. 3135, 1991.   
[9] D. B. Fogel, "Empirical estimation of the computation required to discover approximate solutions to the traveling salesman problem using evolutionary programming," in Proc. of the Second Ann. Conf. on Evol. Prog. (D. B. Fogel and W. Atmar, eds.), pp. 56-61, Evolutionary Programming Society, La Jolla, CA, 1993.   
[10] G. Rudolph, Convergence Properties of Evolutionary Algorithms. Hamburg: Verlag Dr. Kova, 1997.   
[11] S. Droste, T. Jansen, and I. Wegener, "A rigorous complexity analysis of the (1+1) evolutionary algorithm for linear functions with boolean inputs," Evolutionary Computation, vol. 6, no. 2, pp. 185196, 1998.   
[12] E. van Nimwegen, J. P. Crutchfield, and M. Mitchell, " Statistical dynamics of the royal road genetic algorithm". Theoretical Computer Science, vol.229, no.1, pp.41-102, 1999.   
[13] E. van Nimwegen and J. P. Crutchfield, "Optimizing epochal evolutionary search: Populationsize dependent theory". Machine Learning Journal. to appear.   
[14] J. He and H. Huang, "The computational time analysis of genetic algorithms," in Proceedings of the Fifth Chinese Joint Conference on Artificial Intelligence, (Xi'an, P.R. China), pp. 440- 443, Xi'an Jiaotong University Press, 1998.   
[15] J. He, H. Huang and L. Kang, "The computational time of genetic algorithms for fully deceptive problem," Chinese Journal of Computer, vol. 21, no. 9, pp. 999-1003, 1999.   
[16] B. Hajek, "Hitting time and occupation time bounds implied by drift analysis with applications," Adv. Appl. Probab., vol. 14, pp. 502525, 1982.   
[17] R. L. Tweedie, "Criteria for classifying general markov chains," Adv. Appl. Probab., vol. 8, pp. 737771, 1976.   
[18] J. He and L. Kang,"On the convergence rate of genetic alorithms." Theoretical Computer Science, vol. 229, no. 1/2, pp. 2339, 1999.   
[19] G. H. Sasaki and B. Hajek, "The time complexity of maximum matching by simulated annealing." J. ACM, vol. 35, no .2, pp. 387-403, 1988.   
[20] J. Neveu, Discrete-Parameter Martingales. North Holland, Amsterdam and Oxford, 1975.   
[21] G. Rudolph, "How mutation and selection solve long path problem in polynomial expected time." Evolutionary Computation, vol. 4, no. 2, pp. 195-205, 1996.   
[22] S. Khuri, T. Bäck, and J. Heitkötter, "An evolutionary approach to combinatorial optimization problems," in Proceedings of the 22nd Annual ACM Computer Science Conference (D. Cizmar, ed.), (New York), pp. 6673, ACM Press, 1994.   
[23] R. M. Karp, "Reducibility among combinatorial problems," in Complexity of Computer Computation (R. Miller and W. Thatcher, eds.), pp. 85-103, New York: Plenum, 1972.