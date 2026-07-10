# Improving the performance of evolutionary algorithms for the multiobjective 0/1 knapsack problem using ε -dominance

Crina Grosan   
Department of Computer Science   
Faculty of Mathematics and Computer Science   
Babes-Bolyai University   
Cluj-Napoca 3400, Kogalniceanu 1   
Romania.   
Email: cgrosan@cs.ubbcluj.ro

Abstract— The 0/1 knapsack problem is a well known problem occurring in many real world problems. The problem is NP-Complete. The multiobjective 0/1 knapsack problem is a generalization of the 0/1 knapsack problem in which multiple knapsacks are considered. A new evolutionary algorithm for solving multiobjective $\mathbf { 0 } / \mathbf { 1 }$ knapsack problem is proposed in this paper. This algorithm used a $\varepsilon$ -dominance relation for direct comparison of two solutions. Several numerical experiments are performed using the best recent algorithms proposed for this problem. Experimental results clearly show that the proposed algorithm outperforms the existing evolutionary approaches for this problem.

# I. INTRODUCTION

In a multiobjective problem more than one objective has to be optimized while satisfying some constraints. The ideal case consists in finding the solution that optimizes all objectives simultaneously. But, with respect to the feasible space, this solution may not exist. In these situations there exists not only one solution but a set of efficient solutions in the sense that these solutions cannot be bettered without violating any other conditions associated with the optimization problem. The knapsack problem is a well known combinatorial problem. It has been well studied in the single objective context. It is also called a master problem since many combinatorial problems can be formulated as a knapsack problem.

The 0/1 knapsack problem is a widely studied problem due its practical importance. In the last years a generalization of this problem was well studied and many algorithms for solving this variant have been proposed. Of great interest are the evolutionary approaches for solving the multiobjective 0/1 knapsack problem. Many papers on the multiobjective knapsack problem and on the algorithms proposed for solving it can be found in the literature [1], [2], [3], [4], [8], [9], [10], [11], [12], [14], [15], [16], [17], [20]. In this paper, we propose a new evolutionary approach for multiobjective $_ { 0 / 1 }$ knapsack problem. We use the $\varepsilon$ -dominance concept which is a generalization of the standard Pareto concept.

In section $\mathrm { I I }$ of the paper both single and multiobjective 0/1 knapsack problems are presented. The description of the newly proposed algorithm is given in section III of the paper. The definition of $\varepsilon$ -dominance concept is also given in section III. Some comparisons with the most recent algorithms (such as SPEA2, NSGA II, PESA) are performed in section IV. A set of conclusions are given in section $\mathrm { V }$ of the paper.

# II. PROBLEM STATEMENT

The classical $_ { 0 / 1 }$ knapsack problem can be formulated as follow: a set of $n$ items and a knapsack of capacity $c$ are considered. Each item has a profit $p _ { j }$ and a weight $w _ { j }$ . The problem is to select a subset of the items whose total weight does not exceed knapsack capacity $c$ and whose total profit is maximum. Using the variables $x _ { j }$ (with $x _ { j } = 1$ if the item $j$ is selected and $x _ { j } = 0$ otherwise) the problem can be written:

$$
{ \mathrm { m a x i m i z e } } \sum _ { j = 1 } ^ { n } p _ { j } x _ { j }
$$

$$
{ \mathrm { s u b j e c t ~ t o ~ } } \sum _ { j = 1 } ^ { n } w _ { j } x _ { j } \leq c
$$

$$
\begin{array} { r l } { x _ { j } } & { { } \in \{ 0 , 1 \} , \mathrm { j } = \{ 1 , . . . , n \} . } \end{array}
$$

The problem can be extended for an arbitrary number of knapsacks. The multiobjective $_ { 0 / 1 }$ knapsack problem is defined as follows:

A set of n items and a set of $\mathrm { k }$ knapsacks are considered. For each item we know:

$$
\begin{array} { r } { p _ { i , j } - \mathrm { p r o f i t ~ o f ~ i t e m ~ } j \mathrm { ~ a c c o r d i n g ~ t o ~ k n a p s a c k ~ } i ; } \\ { w _ { i , j } - \mathrm { w e i g h t ~ o f ~ i t e m ~ } j \mathrm { ~ a c c o r d i n g ~ t o ~ k n a p s a c k ~ } i . } \end{array}
$$

The capacity of each knapsack $i$ is $c _ { i }$ .

The problem is to find a vector $x = ( x _ { 1 } , x _ { 2 } , \ldots , x _ { n } ) \quad \in$ $\{ 0 , 1 \} ^ { n }$ such that the capacity constraints

$$
e _ { i } ( x ) = \sum _ { j = 1 } ^ { n } w _ { i j } \cdot x _ { j } \leq c _ { i } , ( 1 \leq i \leq k )
$$

are satisfied and for which $f ( x ) = ( f _ { 1 } ( x ) , f _ { 2 } ( x ) , . . . , f _ { k } ( x ) )$ is maximum, where

$$
f _ { i } ( x ) = \sum _ { j = 1 } ^ { n } p _ { i j } \cdot x _ { j }
$$

and $x _ { j } = 1$ if the item $j$ is selected and $x _ { j } = 0$ otherwise.

Knapsack problem has been studied for the first time in late fifties. Since then a large number of algorithms and techniques have been proposed. Many exact algorithms for the single objective knapsack problem have been proposed in the literature. The most famous one have been proposed by Martello and Toth [13] and is a branch and bound procedure. The single objective knapsack problem can be also solved heuristically in order to approximate de optimal solution. A typical heuristic for the knapsack problem is the Greedy algorithm which can solve either small or large size problems in a polynomial time. For the multiobjective knapsack problem existing algorithms are essentially based on the branch and branch method [?]. These algorithms are different one from another according to the way the upper bounds are obtained. For instance, Shin solves, exactly, each of the k single constrained (k being the number of knapsacks), relaxed knapsack problems and select the minimum of the k objective functions as being the upper bound. Better algorithms have been proposed by using tighter upper bounds obtained with other relaxation techniques such as lagrangean, surrogate and composite relaxations [5]. Due to their exponential time complexity, exact algorithms are limited to small size instances.

# III. PROPOSED ALGORITHM

The proposed algorithm uses $\varepsilon$ -Pareto dominance relation between solutions.

We give here the definition of $\varepsilon$ -Pareto dominance concept which is a generalization of the Pareto dominance concept.

# Definition

Consider a maximization problem. Let $x , \ y$ be two decision vectors (solutions) from the search space. Solution $x \in \cdot$ -dominate $y$ if and only if the following conditions are fulfilled:

$$
\begin{array} { r l } & { f _ { i } ( x ) \quad \ge \quad f _ { i } ( y ) , \forall \quad i = 1 , 2 , . . . , n , } \\ & { \exists j \quad \in \{ 1 , 2 , . . . , n \} : f _ { j } ( x ) > f _ { j } ( y ) + \varepsilon . } \end{array}
$$

Each individual is a binary string. The value 1 for the position $j$ of the chromosome means that the item $j$ is selected to be included in a knapsack.

The proposed algorithm uses steady-state as its underlying mechanism and can be described as follows:

The algorithm starts with a population of randomly generated individuals. For each chromosome the total items weight for each knapsack is computed. If there are knapsacks for which the allowed capacity is exceeded the items starting with the one for which the proportion utility/weight has the smaller value are eliminated. This process continues until there are no knapsacks for which the capacity is exceeded. All nondominated solutions are computed using the $\varepsilon$ -dominance concept. The following steps are repeated until a termination condition is reached: Two nondominates solutions (the parents) are randomly chosen. The parents are recombined using uniform crossover operator and the offspring are mutated. For each offspring the procedure for eliminating items if the capacity of one of knapsacks is exceeded is used. The offspring enters the population and the dominated solutions are removed.

This algorithm is called $\varepsilon$ Multiobjective Knapsack Algorithm ( $\dot { \varepsilon }$ -MOKA).

The $\varepsilon$ -MOKA technique is depicted in Figure 1.

An individual is a set of selected items. Each knapsack is checked for overloading. If the total weight of the selected objects exceeds its capacity the items starting with the one for which the proportion utility/weight is lowest are eliminated. The procedure $e x c e e d ( p o p [ i ] , j )$ is used for each individual pop[i] from population and for each knapsack $j$ in order to determinate if there are knapsacks for which the capacity is exceeded. The procedure eliminate(pop[i], j) is used in order to eliminate items from $p o p [ i ]$ until the capacity of the knapsack $j$ is not exceeded.

# IV. EXPERIMENTAL RESULTS

We test our algorithm considering 750 items and two, three and four knapsacks respectively. The results obtained by $\varepsilon \cdot$ - MOKA are compared to the results obtained by SPEA2, NSGA II and PESA. For this comparison two metrics of performance are used: distance metric for the case when two knapsacks are considered and $C$ metric for the cases with three and four knapsacks. Each of these metrics is shortly presented in this section.

# A. Performance measures

In order the compare the performances of the new proposed algorithms with other algorithms two performance metrics are used. When two knapsacks are considered distance metric proposed by Grosan et al. in [6], [7] is used. When three and four knapsacks are considered the $C$ metric proposed by Zitzler [19] is used.

# Remark

If we want to apply distance metric we have to know the Pareto front. For this problem Pareto front is known for two dimensions (knapsacks) only. Consequently we cannot apply distance metric for the considered situations with three and four knapsacks.

1) Distance metric: This metric is defined in what follows:

Assume that the Pareto front is known. Let us denote by $P$ a set of Pareto optimal solutions. For each individual $i$ from the final population $F P$ distance (Euclidian distance or other suitable distance) $d _ { i j }$ to the all points $j$ of $P$ is computed.

The minimum distance:

$$
m i n d i s t _ { i } = \operatorname* { m i n } _ { j \in P } d _ { i j }
$$

is kept for each individual.

The average of these distances

$$
D M = \frac { \sum _ { i \in F P } \mathrm { m i n d i s t } _ { \mathrm { i } } } { | F P | }
$$

represents the measure of convergence (the distance) to the Pareto front.

# Remark

The lowest values for $D M$ indicate a better convergence.

2) $C$ metric: The $C$ metric was introduced by Zitzler [19]. Using $C$ metric two sets of nondominated solutions can be compared to each other. The definition of $C$ metric given in [19] is:

# Definition. (Coverage of two sets)

Let $X$ be the set of decision vectors for the considered problem and $A , B \subseteq { \cal { X } }$ two sets of decision vectors. The function $C$ maps the ordered pair $( A , B )$ into the interval [0,1]:

$$
C ( A , \ B ) = { \frac { | \{ b \in B \ / \ \exists a \in A : a \succeq b \} | } { | B | } } .
$$

Remarks

The value $C ( A , B ) = 1$ means that all decision vectors in $B$ are dominated by $A$ .

The value $C ( A , B ) = 0$ represent the situation when none of the points in $B$ are dominated by $A$ .

$C ( A , B )$ is not necessary equal to $1 - C ( B , A )$ .

# B. Numerical comparisons

In order to compare the results obtained by $\varepsilon$ -MOKA with the results obtained by SPEA2, NSGA II and PESA the instances with 750 items and two, three and four knapsacks are considered [19]. These cases are considered the most difficult for the multiobjective knapsack problem.

1) Parameter setting: General parameters of MOKA algorithm are presented in Table I.

The value of $\varepsilon$ for $\varepsilon$ -MOKA is chosen as follows: at the beginning of the search process this value is a large one. In this way a low dominance is ensured and this allow us to preserve many solutions in the first generations. After a number of iterations the value of $\varepsilon$ is decreased by 1. Reducing the value of $\varepsilon$ we will ensure the true Pareto dominance at the end of the search process.

The values of $\varepsilon$ for all considered situations are presented in Tables II, III and IV. The values of $\varepsilon$ for the case of two knapsacks are presented in Table $\mathrm { I I }$ .

TABLE I PARAMETERS USED BY $\varepsilon$ -MOKA, NSGA II, SPEA 2 AND PESA.   

<table><tr><td rowspan=1 colspan=1>Number ofitems</td><td rowspan=1 colspan=1>Number  ofknapsacks</td><td rowspan=1 colspan=1>Populationsize</td><td rowspan=1 colspan=1>Numberof  functionevaluations</td></tr><tr><td rowspan=3 colspan=1>750</td><td rowspan=3 colspan=1>2</td><td rowspan=3 colspan=1>250</td><td rowspan=1 colspan=1>125,000</td></tr><tr><td rowspan=1 colspan=1>240,000</td></tr><tr><td rowspan=1 colspan=1>480,000</td></tr><tr><td rowspan=3 colspan=1>750</td><td rowspan=3 colspan=1>3</td><td rowspan=3 colspan=1>300</td><td rowspan=1 colspan=1>150,000</td></tr><tr><td rowspan=1 colspan=1>288,000</td></tr><tr><td rowspan=1 colspan=1>576,000</td></tr><tr><td rowspan=3 colspan=1>750</td><td rowspan=3 colspan=1>4</td><td rowspan=3 colspan=1>400</td><td rowspan=1 colspan=1>175,000</td></tr><tr><td rowspan=1 colspan=1>336,000</td></tr><tr><td rowspan=1 colspan=1>672,000</td></tr></table>

TABLE V THE RESULTS OBTAINED FOR TWO KNAPSACKS BY $\varepsilon$ -MOKA, NSGA II, SPEA2 AND PESA. RESULTS ARE AVERAGED OVER 30 RUNS.   

<table><tr><td rowspan=1 colspan=1>Number offunctionsevaluations</td><td rowspan=1 colspan=1>ε-MOKA</td><td rowspan=1 colspan=1>NSGA II</td><td rowspan=1 colspan=1>SPEA 2</td><td rowspan=1 colspan=1>PESA</td></tr><tr><td rowspan=1 colspan=1>125,000</td><td rowspan=1 colspan=1>11990.6</td><td rowspan=1 colspan=1>12172.1</td><td rowspan=1 colspan=1>12047.8</td><td rowspan=1 colspan=1>12274</td></tr><tr><td rowspan=1 colspan=1>240,000</td><td rowspan=1 colspan=1>11711.2</td><td rowspan=1 colspan=1>12297.1</td><td rowspan=1 colspan=1>12221</td><td rowspan=1 colspan=1>12345.1</td></tr><tr><td rowspan=1 colspan=1>480,000</td><td rowspan=1 colspan=1>11516.4</td><td rowspan=1 colspan=1>12361.7</td><td rowspan=1 colspan=1>12298.4</td><td rowspan=1 colspan=1>12374.6</td></tr></table>

The results obtained in the case of three knapsacks by applying $C$ metric for 150,000 functions evaluations are presented in Table VI.

TABLE II THE VALUES OF $\varepsilon$ FOR THE CASE OF TWO KNAPSACKS.   

<table><tr><td rowspan=1 colspan=1>Number of func-tions evaluations</td><td rowspan=1 colspan=1>The value of ε</td><td rowspan=1 colspan=1>Number of genera-tions after which εbecomes ε-1</td></tr><tr><td rowspan=1 colspan=1>125,000</td><td rowspan=1 colspan=1>200</td><td rowspan=1 colspan=1>500</td></tr><tr><td rowspan=1 colspan=1>240,000</td><td rowspan=1 colspan=1>200</td><td rowspan=1 colspan=1>1000</td></tr><tr><td rowspan=1 colspan=1>480,000</td><td rowspan=1 colspan=1>500</td><td rowspan=1 colspan=1>800</td></tr></table>

The values of $\varepsilon$ for the case of three knapsacks are presented in Table III.

THE RESULTS OBTAINED FOR THREE KNAPSACKS BY $\varepsilon$ -MOKA, NSGA II, SPEA2 AND PESA CONSIDERING 150,000 FUNCTIONS EVALUATIONS.

RESULTS ARE AVERAGED OVER 30 RUNS.

TABLE VI   

<table><tr><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>ε-MOKA</td><td rowspan=1 colspan=1>NSGA II</td><td rowspan=1 colspan=1>SPEA 2</td><td rowspan=1 colspan=1>PESA</td></tr><tr><td rowspan=1 colspan=1>ε-MOKA</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>0.90301</td><td rowspan=1 colspan=1>0.939242</td><td rowspan=1 colspan=1>0.994266</td></tr><tr><td rowspan=1 colspan=1>NSGA II</td><td rowspan=1 colspan=1>0</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>0.976883</td><td rowspan=1 colspan=1>0.989555</td></tr><tr><td rowspan=1 colspan=1>SPEA 2</td><td rowspan=1 colspan=1>0</td><td rowspan=1 colspan=1>0.906996</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>0.990861</td></tr><tr><td rowspan=1 colspan=1>PESA</td><td rowspan=1 colspan=1>0</td><td rowspan=1 colspan=1>0.862837</td><td rowspan=1 colspan=1>0.908916</td><td rowspan=1 colspan=1></td></tr></table>

TABLE III THE VALUES OF $\varepsilon$ FOR THE CASE OF THREE KNAPSACKS.   

<table><tr><td rowspan=1 colspan=1>Number of func-tions evaluations</td><td rowspan=1 colspan=1>The value of ε</td><td rowspan=1 colspan=1>Number of genera-tions after which εbecomes ε-1</td></tr><tr><td rowspan=1 colspan=1>150,000</td><td rowspan=1 colspan=1>1000</td><td rowspan=1 colspan=1>500</td></tr><tr><td rowspan=1 colspan=1>288,000</td><td rowspan=1 colspan=1>1000</td><td rowspan=1 colspan=1>1000</td></tr><tr><td rowspan=1 colspan=1>576,000</td><td rowspan=1 colspan=1>1500</td><td rowspan=1 colspan=1>1000</td></tr></table>

The values 0 on first column means that no solution from the final population obtained by $\varepsilon$ -MOKA is dominated by solutions from final populations obtained by NSGA II, SPEA 2 and PESA. The values 0.9 on the first line means almost all solutions from final populations obtained by NSGA II, SPEA 2 and PESA are dominated by solutions obtained by $\varepsilon$ -MOKA.

The results obtained in the case of three knapsacks by applying $C$ metric for 288,000 functions evaluations are presented in Table VII.

The values of $\varepsilon$ for the case of four knapsacks are presented in Table IV.

TABLE IV THE VALUES OF $\varepsilon$ FOR THE CASE OF FOUR KNAPSACKS.   

<table><tr><td rowspan=1 colspan=1>Number of func-tions evaluations</td><td rowspan=1 colspan=1>The value of ε</td><td rowspan=1 colspan=1>Number of genera-tions after which εbecomes ε-1</td></tr><tr><td rowspan=1 colspan=1>175,000</td><td rowspan=1 colspan=1>1000</td><td rowspan=1 colspan=1>500</td></tr><tr><td rowspan=1 colspan=1>336,000</td><td rowspan=1 colspan=1>1000</td><td rowspan=1 colspan=1>1000</td></tr><tr><td rowspan=1 colspan=1>672,000</td><td rowspan=1 colspan=1>1500</td><td rowspan=1 colspan=1>1000</td></tr></table>

2) Comparison of results: The results obtained in the case of two knapsacks by applying distance metric are presented in Table V.

Table V shows that the solution obtained by $\varepsilon$ -MOKA are closer from the Pareto front than the solutions obtained by NSGA II, SPEA2 and PESA. The situation is very similar for NSGA II, SPEA2 and PESA even if we increase the number of generations.

# TABLE VII

THE RESULTS OBTAINED FOR THREE KNAPSACKS BY $\varepsilon$ -MOKA, NSGA II, SPEA2 AND PESA CONSIDERING 288,000 FUNCTIONS EVALUATIONS. RESULTS ARE AVERAGED OVER 30 RUNS.

<table><tr><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>ε-MOKA</td><td rowspan=1 colspan=1>NSGA II</td><td rowspan=1 colspan=1>SPEA 2</td><td rowspan=1 colspan=1>PESA</td></tr><tr><td rowspan=1 colspan=1>ε-MOKA</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>0.787402</td><td rowspan=1 colspan=1>0.910033</td><td rowspan=1 colspan=1>0.985815</td></tr><tr><td rowspan=1 colspan=1>NSGA II</td><td rowspan=1 colspan=1>0</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>0.996314</td><td rowspan=1 colspan=1>0.990203</td></tr><tr><td rowspan=1 colspan=1>SPEA 2</td><td rowspan=1 colspan=1>0</td><td rowspan=1 colspan=1>0.853698</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>0.985883</td></tr><tr><td rowspan=1 colspan=1>PESA</td><td rowspan=1 colspan=1>0</td><td rowspan=1 colspan=1>0.850779</td><td rowspan=1 colspan=1>0.93234</td><td rowspan=1 colspan=1></td></tr></table>

The solutions obtained in the final population by $\varepsilon$ -MOKA are not dominated by solutions obtained in the final populations by NSGA II, SPEA 2 and PESA even increasing the number of generations. A small improvement occurs for NSGA II, PAES and SPEA 2 in the sense that the number of solutions, obtained in the final population by $\varepsilon$ -MOKA which dominates solutions obtained in the final population by the other three algorithms, is smaller.

The results obtained in the case of three knapsacks by applying $C$ metric for 576,000 functions evaluations are presented in Table VIII.

TABLE VIII THE RESULTS OBTAINED FOR THREE KNAPSACKS BY $\varepsilon$ -MOKA, NSGA II, SPEA2 AND PESA CONSIDERING 576,000 FUNCTIONS EVALUATIONS. RESULTS ARE AVERAGED OVER 30 RUNS.   

<table><tr><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>ε-MOKA</td><td rowspan=1 colspan=1>NSGA II</td><td rowspan=1 colspan=1>SPEA 2</td><td rowspan=1 colspan=1>PESA</td></tr><tr><td rowspan=1 colspan=1>ε-MOKA</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>0.999851</td><td rowspan=1 colspan=1>1</td><td rowspan=1 colspan=1>1</td></tr><tr><td rowspan=1 colspan=1>NSGA II</td><td rowspan=1 colspan=1>0.34914</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>0.99623</td><td rowspan=1 colspan=1>0.99170</td></tr><tr><td rowspan=1 colspan=1>SPEA 2</td><td rowspan=1 colspan=1>0.128210</td><td rowspan=1 colspan=1>0.832425</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>0.96905</td></tr><tr><td rowspan=1 colspan=1>PESA</td><td rowspan=1 colspan=1>0.128210</td><td rowspan=1 colspan=1>0.809001</td><td rowspan=1 colspan=1>0.939329</td><td rowspan=1 colspan=1></td></tr></table>

A small number of solution obtained by $\varepsilon$ -MOKA are dominated by solutions obtained by NSGA II, SPEA 2 and PESA even for 576,000 functions evaluation. That means $\varepsilon$ - MOKA has a very good convergence.

The results obtained in the case of four knapsacks by applying $C$ metric for 175,000 functions evaluations are presented in Table IX.

TABLE IX THE RESULTS OBTAINED FOR FOUR KNAPSACKS BY $\varepsilon$ -MOKA, NSGA II, SPEA2 AND PESA CONSIDERING 175,000 FUNCTIONS EVALUATIONS.   

<table><tr><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>ε-MOKA</td><td rowspan=1 colspan=1>NSGA II</td><td rowspan=1 colspan=1>SPEA 2</td><td rowspan=1 colspan=1>PESA</td></tr><tr><td rowspan=1 colspan=1>ε-MOKA</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>0.991756</td><td rowspan=1 colspan=1>0.999857</td><td rowspan=1 colspan=1>1</td></tr><tr><td rowspan=1 colspan=1>NSGA II</td><td rowspan=1 colspan=1>0.394445</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>0.996448</td><td rowspan=1 colspan=1>1</td></tr><tr><td rowspan=1 colspan=1>SPEA 2</td><td rowspan=1 colspan=1>0.178535</td><td rowspan=1 colspan=1>0.825909</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>0.999951</td></tr><tr><td rowspan=1 colspan=1>PESA</td><td rowspan=1 colspan=1>0.049242</td><td rowspan=1 colspan=1>0.571111</td><td rowspan=1 colspan=1>0.813379</td><td rowspan=1 colspan=1></td></tr></table>

Table IX shows that the number of solutions obtained in the final population by applying $\varepsilon$ -MOKA which are dominated by solutions obtained in the final population by NSGA II, PAES and SPEA 2 (first column) is very small compared to the number of solutions obtained by NSGA II, PAES and SPEA 2 which dominate solutions obtained by $\varepsilon$ -MOKA (first line on the table).

The results obtained in the case of four knapsacks by applying $C$ metric for 336,000 functions evaluations are presented in Table X.

TABLE X THE RESULTS OBTAINED FOR FOUR KNAPSACKS BY $\varepsilon$ -MOKA, NSGA II, SPEA2 AND PESA CONSIDERING 336,000 FUNCTIONS EVALUATIONS.   

<table><tr><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>ε-MOKA</td><td rowspan=1 colspan=1>NSGA II</td><td rowspan=1 colspan=1>SPEA 2</td><td rowspan=1 colspan=1>PESA</td></tr><tr><td rowspan=1 colspan=1>ε-MOKA</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>0.86266</td><td rowspan=1 colspan=1>0.95565</td><td rowspan=1 colspan=1>0.995708</td></tr><tr><td rowspan=1 colspan=1>NSGA II</td><td rowspan=1 colspan=1>0.73848</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>0.996423</td><td rowspan=1 colspan=1>0.998426</td></tr><tr><td rowspan=1 colspan=1>SPEA 2</td><td rowspan=1 colspan=1>0.65741</td><td rowspan=1 colspan=1>0.81182</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>0.988937</td></tr><tr><td rowspan=1 colspan=1>PESA</td><td rowspan=1 colspan=1>0.63986</td><td rowspan=1 colspan=1>0.73114</td><td rowspan=1 colspan=1>0.966238</td><td rowspan=1 colspan=1></td></tr></table>

Increasing the number of generations from 175,000 to 336,000 increase the number of solutions obtained by NSGA II, SPEA 2 and PESA which are not dominated by solutions obtained by $\varepsilon - M O K A$ .

The results obtained in the case of four knapsacks by applying $C$ metric for 672,000 functions evaluations are presented in Table XI.

TABLE XI THE RESULTS OBTAINED FOR FOUR KNAPSACKS BY $\varepsilon$ -MOKA, NSGA II, SPEA2 AND PESA CONSIDERING 672,000 FUNCTIONS EVALUATIONS.   

<table><tr><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>ε-MOKA</td><td rowspan=1 colspan=1>NSGA II</td><td rowspan=1 colspan=1>SPEA 2</td><td rowspan=1 colspan=1>PESA</td></tr><tr><td rowspan=1 colspan=1>ε-MOKA</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>0.641452</td><td rowspan=1 colspan=1>0.58422</td><td rowspan=1 colspan=1>0.655</td></tr><tr><td rowspan=1 colspan=1>NSGA II</td><td rowspan=1 colspan=1>0.54112</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>0.998076</td><td rowspan=1 colspan=1>0.999851</td></tr><tr><td rowspan=1 colspan=1>SPEA 2</td><td rowspan=1 colspan=1>0.52985</td><td rowspan=1 colspan=1>0.793005</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>0.992359</td></tr><tr><td rowspan=1 colspan=1>PESA</td><td rowspan=1 colspan=1>0.512298</td><td rowspan=1 colspan=1>0.687386</td><td rowspan=1 colspan=1>0.95535</td><td rowspan=1 colspan=1></td></tr></table>

After 672,000 functions evaluations the number of solutions from the final population obtained by NSGA II, SPEA 2 and PESA which are dominate by solutions obtained by $\varepsilon$ -MOKA easy decreases compared with previous case - 336,000 (the number from the first column of the Table XI are smaller). The number of solutions obtained by $\varepsilon$ -MOKA which are dominated by solutions obtained by NSGA II, SPEA 2 and PESA easy increases (the number from the first column of the Table XI are greater).

Analyzing these tables we can see the effectiveness of applying $\varepsilon$ -MOKA to the multicriterion knapsack problem. By using the $\varepsilon$ dominance technique at the beginning of search process many solutions (which otherwise could be eliminated from the evolution stage) have the opportunity to be improved. However, by decreasing the value of $\varepsilon$ the standard Pareto dominance is obtained at the end of the search process.

# V. CONCLUSIONS

In this paper a new evolutionary algorithm for solving $_ { 0 / 1 }$ multiobjective knapsack problem has been proposed. The algorithm uses the ε – dominance concept which is a generalization of the Pareto dominance. The value of $\varepsilon$ is not fixed. Larger values are considered for $\varepsilon$ at the beginning of the search process. These values are decreased as the number of generations increase. This procedure proved to be very useful.

Several numerical experiments have been performed using several well-known instances of the knapsack problem. For these experiments two knapsacks and 100 items are considered. A comparison with SPEA, PESA and NSGA II is also performed. Experimental results have shown that the proposed algorithm significantly outperforms the compared algorithms in all experiments.

# Список литературы

[1] E. Balas, E. Zemel, ”An algorithms for large zero-one knapsack problems”, in Operations Research, Vol 28, pp. 1130-1154, 1980.   
[2] V. Chvatal, ”Hard knapsack problems”, Operations Research, Vol 28, pp. 1402-1411, 1980.   
[3] D.W. Corne, J.D. Knowles, ”The Pareto-Envelope based Selection Algorithm for Multiobjective Optimization”, in Proceedings of the Sixth International Conference on Parallel Problem Solving from Nature, Springer-Verlag, Berlin, 2000, pp. 839-848.   
[4] K. Deb, S. Agrawal, A. Pratap, T. Meyarivan, ”A fast elitist nondominated sorting genetic algorithm for multi-objective optimization: NSGA II”, in M. S. et al. Eds, Parallel Problem Solving From Nature – PPSN VI, Springer-Verlag, Berlin, 2000, pp. 849 - 858.   
[5] B. Gavish, H. Pirkul, ”Efficient algorithms for solving multiconstraint zero-one knapsack problem to optimality”, Mathematical Programming Vol. 31, pp. 78-105, 1985.   
[6] C. Grosan, M. Oltean, D. Dumitrescu, ”Performance Metrics for Multiobjective Optimization Evolutionary Algorithms”, in Proceedings of Conference on Applied and Industrial Mathematics, Oradea, Romania, 2003.   
[7] C. Grosan, ”How to compare the multiobjective evolutionary algorithms performances?” in Zilele Academice Clujene, Cluj-Napoca, Romania, 2003.   
[8] G. P. Ingargiola, J. F. Korsh, ”A reduction algorithm for zero-one single knapsack problems”, in Management Science Vol. 20, pp. 460-463, 1975.   
[9] A. Jaszkiewicz, ”On the performance of Multiple Objective Local Search on the $_ { 0 / 1 }$ Knapsack problem – A Comparative Experiment”, IEEE Transaction on Evolutionary Computation, Vol 6, pp. 402-412, 2002.   
[10] I. Ko, ”Using AI techniques and learning to solve multi-level knapsack problems”. PhD thesis, University of Colorado at Boulder, Boulder, CO, 1993.   
[11] W. Loots, T.H.C. Smith, ”A parallel algorithm for the zero-one knapsack problem”, International Journal Parallel Program, Vol. 21, pp. 313-348, 1992.   
[12] S. Martello, and P. Toth, Knapsack problems: Algorithms and computer implementation, Willey and Sons, Chichester, 1990.   
[13] S. Martello, P. Toth, ”An upper bound for the zero-one knapsack problem and a branch and bound algorithm”, European Journal of Operational Research, Vol. 1, pp. 169-175, 1977.   
[14] M. Penn, D. Hasson, M. Avriel, ”Solving the 0/1 proportional Knapsack problem by sampling”, J. Optim. Theory Appl pp. 261-272, 1994.   
[15] S. Sahni, ”Approximate algorithms for the 0/1 knapsack problem”, Journal of ACM, Vol. 22, pp. 115-124, 1975.   
[16] M. Vasquez, J.K. Hao, ”A hybrid approach for the 0/1 multidimensional knapsack problem”, in Proceedings of the $I 3 ^ { t h }$ International Joint Conference on Artificial Intelligence pp. 328-333, 2001.   
[17] E. Zitzler, L. Thiele, ”Multiobjective optimization using evolutionary algorithms-a comparative case study”. in Fifth International Conference on Parallel Problem Solving from Nature, A. E. Eiben, T. Back, M. Schoenauer and H. P. Schwefel Eds., Springer, Berlin, Germany, 1998, pp. 292-301.   
[18] E. Zitzler, L. Thiele, ”Multiobjective Evolutionary Algorithms: A comparative case study and the Strength Pareto Approach”, IEEE Transaction on Evolutionary Computation, Vol 3, pp. 257-271, 1999.   
[19] E. Zitzler, ”Evolutionary algorithms for multiobjective optimization: Methods and Applications”, Ph. D. thesis, Swiss Federal Institute of Technology (ETH) Zurich, Switzerland.   
[20] E. Zitzler, M. Laumanns and L. Thiele, ”SPEA 2: Improving the Strength Pareto Evolutionary Algorithm”, TIK Report 103, Computer Engineering and Networks Laboratory (TIK), Departament of Electrical Engineering Swiss federal Institute of Technology (ETH) Zurich, 2001.   
[21] http://www.tik.ee.ethz.ch/ zitzler/testdata.html