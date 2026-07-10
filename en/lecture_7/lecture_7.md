In the previous lecture we discussed the Knapsack problem. In this lecture we discuss other packing and independent set problems.

# 1 Maximum Independent Set Problem

A basic graph optimization problem with many applications is the maximum (weighted) independent set problem (MIS) in graphs.

Definition 1 Given an undirected graph $G = ( V , E )$ a subset of nodes $S \subseteq V$ is an independent set (stable set) iff there is no edge in $E$ between any two nodes in $S$ . A subset of nodes $S$ is $a$ clique if every pair of nodes in $S$ have an edge between them in $G$ .

The MIS problem is the following: given a graph $G = ( V , E )$ find an independent set in $G$ of maximum cardinality. In the weighted case, each node $v \in V$ has an associated non-negative weight $w ( v )$ and the goal is to find a maximum weight independent set. This problem is NP-Hard and it is natural to ask for approximation algorithms. Unfortunately, as the famous theorem below shows, the problem is extremely hard to approximate.

Theorem 1 (H˚astad [1]) Unless $P = N P$ there is no 1n1− -approximation for MIS for any fixed $\epsilon > 0$ where $n$ is the number of nodes in the given graph.

Remark: The maximum clique problem is to find the maximum cardinality clique in a given graph.   
It is approximation-equivalent to the MIS problem; simple complement the graph.

The theorem basically says the following: there are a class of graphs in which the maximum independent set size is either less than $n ^ { \delta }$ or greater than $n ^ { 1 - \delta }$ and it is NP-Complete to decide whether a given graph falls into the former category or the latter.

The lower bound result suggests that one should focus on special cases, and several interesting positive results are known. First, we consider a simple greedy algorithm for the unweighted problem.

<table><tr><td>GREEDy(G):</td></tr><tr><td>S ← While G is not empty do</td></tr><tr><td>Let v be a node of minimum degree in G S ← SU{v}</td></tr><tr><td>Remove v and its neighbors from G</td></tr><tr><td>end while Output S</td></tr></table>

Theorem 2 Greedy outputs an independent set $S$ such that $| S | \ge n / ( \Delta + 1 )$ where $\Delta$ is the maximum degree of any node in the graph.

Proof: We upper bound the number of nodes in $V \setminus S$ as follows. A node $u$ is in $V \setminus S$ because it is removed as a neighbor of some node $v \in S$ when Greedy added $v$ to $S$ . Charge $u$ to $v$ . A node $v \in S$ can be charged at most $\Delta$ times since it has at most $\Delta$ neighbors. Hence we have that $| V \setminus S | \leq \Delta | S |$ . Since every node is either in $S$ or $V \setminus S$ we have $| S | + | V \setminus S | = n$ and therefore $( \Delta + 1 ) | S | \geq n$ which implies that $| S | \ge n / ( \Delta + 1 )$ . ✷

Since the maximum independent set size in a graph is $n$ we obtain the following.

Corollary 3 Greedy gives $a \ \frac { 1 } { \Delta + 1 }$ -approximation for (unweighted) MIS in graphs of degree at most $\Delta$ .

Exercise: Show that Greedy outputs an independent set of size at least $\frac { n } { 2 ( d + 1 ) }$ where $d$ is the average degree of $G$ .

Remark: The well-known Turan’s theorem shows via a clever argument that there is always an independent set of size n(d+1) where $d$ is the average degree of $G$ .

Remark: For the case of unweighted graphs one can obtain an approximation ratio of Ω( log dd log log d ) where $d$ is the average degree. Surprisingly, under a complexity theory conjecture called the UniqueGames conjecture it is known to be NP-Hard to approximate MIS to within a factor of O( log2 ∆∆ ) in graphs with maximum degree $\Delta$ when $\Delta$ is sufficiently large.

Exercise: Consider the weigthed MIS problem on graphs of maximum degree $\Delta$ . Alter Greedy to sort the nodes in non-increasing order of the weight and show that it gives a $\frac { 1 } { \Delta + 1 }$ -approximation. Can one obtain an $\Omega ( 1 / d )$ -approximation for the weighted case where $d$ is the average degree?

LP Relaxation: One can formulate a simple linear-programming relaxation for the (weighted) MIS problem where we have a variable $x ( v )$ for each node $v \in V$ indicating whether $v$ is chosen in the independent set or not. We have constraints which state that for each edge $( u , v )$ only one of $u$ or $v$ can be chosen.

$$
{ \begin{array} { l } { { \mathrm { m a x i m i z e ~ } } \displaystyle \sum _ { v \in V } w ( v ) x ( v ) } \\ { { \mathrm { s u b j e c t ~ t o ~ } } x ( u ) + x ( v ) \leq 1 \qquad ( u , v ) \in E } \\ { \qquad x ( v ) \in [ 0 , 1 ] \qquad v \in V } \end{array} }
$$

Although the above is a valid integer programming relaxation of MIS when the variabels are constrained to be in $\{ 0 , 1 \}$ , it is not a particularly useful formulation for the following simple reason.

Claim 4 For any graph the optimum value of the above $L P$ relaxation is at least $w ( V ) / 2$ . In particular, for the unweighted case it is at least $n / 2$ .

Simply set each $x ( v )$ to $1 / 2$ !

One can obtain a strengthened formulation below by observing that if $S$ is clique in $G$ then any independent set can pick at most one node from $S$ .

$$
\begin{array} { c } { \mathrm { m a x i m i z e ~ } \displaystyle \sum _ { v \in V } w ( v ) x ( v ) } \\ { \mathrm { s u b j e c t ~ t o ~ } \displaystyle \sum _ { v \in S } x ( v ) \leq 1 \qquad \displaystyle S \mathrm { ~ i s ~ a ~ c l i q } } \\ { x ( v ) \in [ 0 , 1 ] \qquad v \in V } \end{array}
$$

The above linear program has an exponential number of variables and it cannot be solved in polynomial time in general but for some special cases of interest the above linear program can indeed be solved (or approximately solved) in polynomial time and leads to either exact algorithms or good approximation bounds.

Approximability of Vertex Cover and MIS: The following is a basic fact and is easy to prove.

Proposition 5 In any graph $G = ( V , E )$ , $S$ is a vertex cover in $G$ if and only if $V \setminus S$ is an independent set in $G$ . Thus $\alpha ( G ) + \beta ( G ) = | V |$ where $\alpha ( G )$ is the size of a maximum independent set in $G$ and $\beta ( G )$ is the size of a minimum vertex cover in $G$ .

The above shows that if one of Vertex Cover or MIS is NP-Hard then the other is as well. We have seen that Vertex Cover admits a 2-approximation while MIS admits no constant factor approximation. It is useful to see why a 2-approximation for Vertex Cover does not give any useful information for MIS even though $\alpha ( G ) + \beta ( G ) = | V |$ . Suppose $S ^ { * }$ is an optimal vertex cover and has size $\geq | V | / 2$ . Then a 2-approximation algorithm is only guaranteed to give a vertex cover of size $| V |$ ! Hence one does not obtain a non-trivial independent set by complementing the approximate vertex cover.

Some special cases of MIS: We mention some special cases of MIS that have been considered in the literature, this is by no means an exhaustive list.

• Interval graphs; these are intersection graphs of intervals on a line. An exact algorithm can be obtained via dynamic programming and one can solve more general versions via linear programming methods.   
• Note that a maximum (weight) matching in a graph $G$ can be viewed as a maximum (weight) independent set in the line-graph of $G$ and can be solved exactly in polynomial time. This has been extended to what are known as claw-free graphs.   
Planar graphs and generalizations to bounded-genus graphs, and graphs that exclude a fixed minor. For such graphs one can obtain a PTAS due to ideas originally from Brenda Baker.   
• Geometric intersection graphs. For example, given $n$ disks on the plane find a maximum number of disks that do not overlap. One could consider other (convex) shapes such as axis parallel rectangles, line segments, pseudo-disks etc. A number of results are known. For example a PTAS is known for disks in the plane. An $\Omega ( \textstyle { \frac { 1 } { \log n } } )$ -approximation for axis-parallel rectangles in the plane when the rectangles are weighted and an $\Omega ( \frac { 1 } { \log \log n } )$ -approximation for the unweighted case.

# 2 Packing Integer Programs (PIPs)

We can express the Knapsack problem as the following integer program. We scaled the knapsack capacity to 1 without loss of generality.

$$
\begin{array} { l } { \displaystyle \mathrm { m a x i m i z e } \sum _ { i = 1 } ^ { n } p _ { i } x _ { i } } \\ { \mathrm { s u b j e c t ~ t o } \sum _ { i } s _ { i } x _ { i } \leq 1 } \\ { x _ { i } \in \{ 0 , 1 \} \qquad 1 \leq i \leq n } \end{array}
$$

More generally if have multiple linear constraints on the “items” we obtain the following integer program.

Definition 2 A packing integer program (PIP) is an integer program of the form $\operatorname* { m a x } \{ w x \mid A x \leq$ $1 , x \in \{ 0 , 1 \} ^ { n } \}$ where w is a $1 \times n$ non-negative vector and $A$ is a $m \times n$ matrix with entries in $[ 0 , 1 ]$ . We call it a $\{ 0 , 1 \}$ -PIP if all entries are in $\{ 0 , 1 \}$ .

In some cases it is useful/natural to define the problem as $\operatorname* { m a x } \{ w x \mid A x \leq b , x \in \{ 0 , 1 \} ^ { n } \}$ where entries in $A$ and $b$ are required to rational/integer valued. We can convert it into the above form by dividing each row of $A$ by $b _ { i }$ .

When $m$ the number of rows of $A$ (equivalently the constraints) is small the problem is tractable. It is some times called the $m$ -dimensional knapsack (recall the problem in HW 1) and one can obtain a PTAS for any fixed constant $m$ . However, when $m$ is large we observe that MIS can be cast as a special case of $\{ 0 , 1 \}$ -PIP. It corresponds exactly to the simple integer/linear program that we saw in the previous section. Therefore the problem is at least as hard to approximate as MIS. Here we show via a clever LP-rounding idea that one can generalize the notion of bounded-degree to column-sparsity in PIPs and obtain a related approximation. We will then introduce the notion of width of the constraints and show how it allows for improved bounds.

Definition 3 A PIP is $k$ -column-sparse if the number of non-zero entries in each column of $A$ is at most $k$ . A PIP has width $W$ if $\operatorname* { m a x } _ { i , j } A _ { i j } / b _ { i } \leq 1 / W$ .

# 2.1 Randomized Rounding with Alteration for PIPs

We saw that randomized rounding gave an $O ( \log n )$ approximation algorithm for the Set Cover problem which is a canonical covering problem. Here we will consider the use of randomized rounding for packing problems. Let $x$ be an optimum fractional solution to the natural LP relaxation of a PIP where we replace the constraint $x \in \{ 0 , 1 \} ^ { n }$ by $x \in \lfloor 0 , 1 \rfloor ^ { n }$ . Suppose we apply independent randomized rounding where we set $x _ { i } ^ { \prime }$ to 1 with probability $x _ { i }$ . Let $x ^ { \prime }$ be the resulting integer solution. The expected weight of this solution is exactly $\sum _ { i } w _ { i } x _ { i }$ which is the LP solution value. However, $x ^ { \prime }$ may not satisfy the constraints given by $A x \leq b$ . A natural strategy to try to satisfy the constraints is to set $x _ { 1 } ^ { \prime }$ to 1 with probability $c x _ { i }$ where $c < 1$ is some scaling constant. This may help in satisfying the constraints because the scaling creates some room in the constraints; we now have that the expected solution value is $c \sum _ { i } w _ { i } x _ { i }$ , a loss of a factor of $c$ . Scaling by itself does not allow us to claim that all constraints are satisfied with good probability. A very useful technique in this context is the technique of alteration; we judiciously fix/alter the rounded solution $x ^ { \prime }$ to force it to satisfy the constraints by setting some of the variables that are 1 in $x ^ { \prime }$ to $0$ . The trick is to do this in such a way as to have a handle on the final probability that a variable is set to 1. We will illustrate this for the Knapsack problem and then generalize the idea to $k$ -sparse PIPs. The algorithms we present are from [2].

Rounding for Knapsack: Consider the Knapsack problem. It is convenient to think of this in the context of PIPs. So we have $a x \leq 1$ where $a _ { i }$ now represents the size of item $i$ and the knapsack capacity is $1$ ; $w _ { i }$ is the weight of item. Suppose $x$ is a fractional solution. Call an item $i$ “big” if $a _ { i } > 1 / 2$ and otherwise it is “small”. Let $S$ be the indices of small items and $B$ the indices of the big items. Consider the following rounding algorithm.

<table><tr><td>ROuNDING-WITH-ALTERATION FOR KNAPSAcK:</td></tr><tr><td>Let x be an optimum fractional solution Round each i to 1 independently with probability xi/4. Let x&#x27; be rounded solution.</td></tr><tr><td>x′ = x′ If (x′ = 1 for exactly one big item i)</td></tr><tr><td>For each j = i set x′f = 0</td></tr><tr><td>Else If (∑is six′ &gt; 1 or two or more big items are chosen in x′)</td></tr><tr><td>For each j set x′ = 0</td></tr><tr><td></td></tr><tr><td>End If Output feasible solution x&quot;</td></tr></table>

In words, the algorithm alters the rounded solution $x ^ { \prime }$ as follows. If exactly one big item is chosen in $x ^ { \prime }$ then the algorithm retains that item and rejects all the other small items. Otherwise, the algorithm rejects all items if two or more big items are chosen in $x ^ { \prime }$ or if the total size of all small items chosen in $x ^ { \prime }$ exceeds the capacity.

The following claim is easy to verify.

Claim 6 The integer solution $x ^ { \prime \prime }$ is feasible.

Now let us analyze the probability of an item $i$ being present in the final solution. Let $\mathcal { E } _ { 1 }$ be the event that $\textstyle \sum _ { i \in S } a _ { i } x _ { i } ^ { \prime } > 1$ , that is the sum of the sizes of the small items chose in $x ^ { \prime }$ exceeds the capacity. Let $\mathcal { E } _ { 2 }$ be the event that at least one big item is chosen in $x ^ { \prime }$ .

Claim 7 $\mathrm { P r } [ \mathcal { E } _ { 1 } ] \leq 1 / 4$ .

Proof: Let $\begin{array} { r } { X _ { s } = \sum _ { i \in S } a _ { i } x _ { i } ^ { \prime } } \end{array}$ be the random variable that measures the sum of the sizes of the small items chosen. We have, by linearity of expectation, that

$$
\mathbb { E } [ X _ { s } ] = \sum _ { i \in S } a _ { i } \mathbb { E } [ x _ { i } ^ { \prime } ] = \sum _ { i \in S } a _ { i } x _ { i } / 4 \leq 1 / 4 .
$$

By Markov’s inequality, $\operatorname* { P r } [ X _ { s } > 1 ] \le \mathbb { E } [ X _ { s } ] / 1 \le 1 / 4$ .

Claim 8 $\operatorname* { P r } [ \mathcal { E } _ { 2 } ] \leq 1 / 2$ .

Proof: Since the size of each big item in $B$ is at least $1 / 2$ , we have $\begin{array} { r } { 1 \geq \sum _ { i \in B } a _ { i } x _ { i } \geq \sum _ { i \in B } x _ { i } / 2 } \end{array}$ . Therefore $\textstyle \sum _ { i \in B } x _ { i } / 4 \leq 1 / 2$ . Event $\mathcal { E } _ { 2 }$ happens if some item $i \in B$ is chosen in the random selection. Since $i$ is chosen with probability $x _ { i } / 4$ , by the union bound, $\begin{array} { r } { \operatorname* { P r } [ \mathcal { E } _ { 2 } ] \leq \sum _ { i \in B } x _ { i } / 4 \leq 1 / 2 } \end{array}$ . ✷

Lemma 9 Let $Z _ { i }$ be the indicator random variable that is 1 if $x _ { i } ^ { \prime \prime } = 1$ and 0 otherwise. Then $\mathbb { E } [ Z _ { i } ] = { \mathrm { P r } } [ Z _ { i } = 1 ] \geq x _ { i } / 1 6$ .

Proof: We consider the binary random variable $X _ { i }$ which is $1$ if $x _ { i } ^ { \prime } = 1$ . We have ${ \mathbb E } [ X _ { i } ] = \operatorname* { P r } [ X _ { i } =$ $1 ] = x _ { i } / 4$ . We write

$$
\operatorname* { P r } [ Z _ { i } = 1 ] = \operatorname* { P r } [ X _ { i } = 1 ] \cdot \operatorname* { P r } [ Z _ { i } = 1 \mid X _ { i } = 1 ] = { \frac { x _ { i } } { 4 } } \operatorname* { P r } [ Z _ { i } = 1 \mid X _ { i } = 1 ] .
$$

To lower bound $\operatorname* { P r } [ Z _ { i } = 1 \mid X _ { i } = 1 ]$ we upper bound the probability $\mathrm { P r } [ Z _ { i } = 0 | X _ { i } = 1 ]$ , that is, the probability that we reject $i$ conditioned on the fact that it is chosen in the random solution $x ^ { \prime }$ .

First consider a big item $i$ that is chosen in $x ^ { \prime }$ . Then $i$ is rejected iff if another big item is chosen in $x ^ { \prime }$ ; the probability of this can be upper bounded by $\mathrm { P r } [ \mathcal { E } _ { 1 } ]$ . If item $i$ is small then it is rejected if and only if $\mathcal { E } _ { 2 }$ happens or if a big item is chosen which happens with $\mathrm { P r } [ \mathcal { E } _ { 1 } ]$ . In either case

$$
\operatorname* { P r } [ Z _ { i } = 0 | X _ { i } = 1 ] \leq \operatorname* { P r } [ \mathcal { E } _ { 1 } ] + \operatorname* { P r } [ \mathcal { E } _ { 2 } ] \leq 1 / 4 + 1 / 2 = 3 / 4 .
$$

Thus,

$$
\operatorname* { P r } [ Z _ { i } = 1 ] = \operatorname* { P r } [ X _ { i } = 1 ] \cdot \operatorname* { P r } [ Z _ { i } = 1 \mid X _ { i } = 1 ] = { \frac { x _ { i } } { 4 } } ( 1 - \operatorname* { P r } [ Z _ { i } = 0 \mid X _ { i } = 1 ] ) \geq { \frac { x _ { i } } { 1 6 } } .
$$

One can improve the above analysis to show that $\operatorname* { P r } [ Z _ { i } = 1 ] \geq x _ { i } / 8$ .

Theorem 10 The randomized algorithm outputs a feasible solution of expected weight at least Pni=1 wixi/16.

Proof: The expected weight of the output is

$$
\mathbb { E } [ \sum _ { i } w _ { i } x _ { i } ^ { \prime \prime } ] = \sum _ { i } w _ { i } \mathbb { E } [ Z _ { i } ] \ge \sum _ { i } w _ { i } x _ { i } / 1 6
$$

where we used the previous lemma to lower bound $\mathbb { E } [ Z _ { i } ]$ .

Rounding for $k$ -sparse PIPs: We now extend the rounding algorithm and analysis above to $k$ -sparse PIPs. Let $x$ be a feasible fractional solution to $\operatorname* { m a x } \{ w x \mid A x \leq 1 , x \in [ 0 , 1 ] ^ { n } \}$ . For a column index $i$ we let $N ( i ) = \{ j \mid A _ { j , i } > 0 \}$ be the indices of the rows in which $i$ has a non-zero entry. Since $A$ is $k$ -column-sparse we have that $| N ( i ) | \le k$ for $1 \leq i \leq n$ . When we have more than one constraint we cannot classify an item/index $i$ as big or small since it may be big for some constraints and small for others. We say that $i$ is small for constraint $j \in N ( i )$ if $A _ { j , i } \leq 1 / 2$ otherwise $i$ is big for constraint $j$ . Let $S _ { j } = \{ i \mid j \in N ( i )$ , and $i$ small for $j \}$ be the set of all small columns for $j$ and $B _ { j } = \{ i \mid j \in N ( i )$ , and $i$ small for $j \}$ be the set of all big columns for $j$ . Note that $S _ { j } \cap B _ { j }$ is the set of all $i$ with $A _ { j , i } > 0$ .

Rounding-with-Alteration for $k$ -sparse PIPs:   
Let $x$ be an optimum fractional solution   
Round each $i$ to 1 independently with probability $x _ { i } / ( 4 k )$ . Let $x ^ { \prime }$ be rounded solution.   
$x ^ { \prime \prime } = x ^ { \prime }$   
For $j = 1$ to $m$ do If ( $x _ { i } ^ { \prime } = 1$ for exactly one $i \in B _ { j }$ ) For each $h \in S _ { j } \cup B _ { j }$ and $h \neq i$ set $x _ { h } ^ { \prime \prime } = 0$ Else If $\begin{array} { r } { ( \sum _ { i \in S _ { j } } A _ { j , i } x _ { i } ^ { \prime } > 1 } \end{array}$ or two or more items from $B _ { j }$ are chosen in $x ^ { \prime }$ ) For each $h \in S _ { j } \cup B _ { j }$ set $x _ { h } ^ { \prime \prime } = 0$ End If   
End For   
Output feasible solution $x ^ { \prime \prime }$

The algorithm, after picking the random solution $x ^ { \prime }$ , alters it as follows: it applies the previous algorithm’s strategy to each constraint $j$ separately. Thus an element $i$ can be rejected at different constraints $j \in N ( i )$ . We need to bound the total probability of rejection. As before, the following claim is easy to verify.

Claim 11 The integer solution $x ^ { \prime \prime }$ is feasible.

Now let us analyze the probability of an item $i$ being present in the final solution. Let $\mathcal { E } _ { 1 } ( j )$ be the event that $\textstyle \sum _ { i \in S _ { j } } A _ { j , i } x _ { i } ^ { \prime } > 1$ , that is the sum of the sizes of the items that are small for $j$ in $x ^ { \prime }$ exceed the capacity. Let $\mathcal { E } _ { 2 } ( j )$ be the event that at least one big item for $j$ is chosen in $x ^ { \prime }$ . The following claims follow from the same reasoning as the ones before with the only change being the scaling factor.

Claim 12 $\mathrm { P r } [ \mathcal { E } _ { 1 } ( j ) ] \leq 1 / ( 4 k )$ .

Claim 13 $\mathrm { P r } [ \mathcal { E } _ { 2 } ( j ) ] \leq 1 / ( 2 k )$ .

Lemma 14 Let $Z _ { i }$ be the indicator random variable that is 1 if $x _ { i } ^ { \prime \prime } = 1$ and 0 otherwise. Then $\mathbb { E } [ Z _ { i } ] = \mathrm { { P r } } [ Z _ { i } = 1 ] \geq x _ { i } / ( 1 6 k )$ .

Proof: We consider the binary random variable $X _ { i }$ which is 1 if $x _ { i } ^ { \prime } = 1$ after the randomized rounding. We have $\mathbb { E } [ X _ { i } ] = \operatorname* { P r } [ X _ { i } = 1 ] = x _ { i } / ( 4 k )$ . We write

$$
\operatorname* { P r } [ Z _ { i } = 1 ] = \operatorname* { P r } [ X _ { i } = 1 ] \cdot \operatorname* { P r } [ Z _ { i } = 1 \mid X _ { i } = 1 ] = { \frac { x _ { i } } { 4 k } } \operatorname* { P r } [ Z _ { i } = 1 \mid X _ { i } = 1 ] .
$$

We upper bound the probability $\mathrm { P r } [ Z _ { i } = 0 | X _ { i } = 1 ]$ , that is, the probability that we reject $i$ conditioned on the fact that it is chosen in the random solution $x ^ { \prime }$ . We observe that

$$
\operatorname* { P r } [ Z _ { i } = 0 | X _ { i } = 1 ] \le \sum _ { j \in N ( i ) } \left( \operatorname* { P r } [ \mathcal { E } _ { 1 } ( j ) ] + \operatorname* { P r } [ \mathcal { E } _ { 2 } ( j ) ] \le k ( 1 / ( 4 k ) + 1 / ( 2 k ) ) \le 3 / 4 . \right.
$$

We used the fact that $N ( i ) \leq k$ and the claims above. Therefore,

$$
\operatorname { r } [ Z _ { i } = 1 ] = \operatorname* { P r } [ X _ { i } = 1 ] \cdot \operatorname* { P r } [ Z _ { i } = 1 \mid X _ { i } = 1 ] = { \frac { x _ { i } } { 4 k } } ( 1 - \operatorname* { P r } [ Z _ { i } = 0 \mid X _ { i } = 1 ] ) \geq { \frac { x _ { i } } { 1 6 k } } .
$$

The theorem below follows by using the above lemma and linearity of expectation to compare the expected weight of the output of the randomized algorithm with that of the fractional solution.

Theorem 15 The randomized algorithm outputs a feasible solution of expected weight at least $\scriptstyle \sum _ { i = 1 } ^ { n } w _ { i } x _ { i } / ( 1 6 k )$ . There is $1 / ( 1 6 k )$ -approximation for $k$ -sparse $P I P s$ .

Larger width helps: We saw during the discussion on the Knapsack problem that if all items are small with respect to the capacity constraint then one can obtain better approximations. For PIPs we defined the width of a given instance as $W$ if $\operatorname* { m a x } _ { i , j } A _ { i j } / b _ { i } \leq 1 / W$ ; in other words no single item is more than $1 / W$ times the capacity of any constraint. One can show using a very similar algorithm and anaylisis as above that the approximation bound improves to $\Omega ( 1 / k ^ { | W | } )$ for instance with with $W$ . Thus if $W = 2$ we get a $\Omega ( 1 / { \sqrt { k } } )$ approximation instead of $\Omega ( 1 / k )$ - approximation. More generally when $W \geq c \log k / \epsilon$ for some sufficiently large constant $c$ we can get a $( 1 - \epsilon )$ -approximation.

# Список литературы

[1] J. H˚astad. Clique is Hard to Approximate within $n ^ { 1 - \epsilon }$ . Acta Mathematica, 182:105–142, 1999.   
[2] N. Bansal, N. Korula, V. Nagarajan, A. Srinivasan. On $k$ -Column Sparse Packing Programs. Proc. of IPCO, 2010. Available at http://arxiv.org/abs/0908.2256.