# The Longest Path Problem is Polynomial on Interval Graphs

Kyriaki Ioannidou $^ { 1 \star }$ , George B. Mertzios $2 { \star } { \star }$ , and Stavros D. Nikolopoulos $^ { 1 \star }$

$^ { 1 }$ Department of Computer Science, University of Ioannina, Greece {kioannid, stavros}@cs.uoi.gr $^ 2$ Department of Computer Science, RWTH Aachen University, Germany mertzios@cs.rwth-aachen.de

Abstract. The longest path problem is the problem of finding a path of maximum length in a graph. Polynomial solutions for this problem are known only for small classes of graphs, while it is NP-hard on general graphs, as it is a generalization of the Hamiltonian path problem. Motivated by the work of Uehara and Uno in [20], where they left the longest path problem open for the class of interval graphs, in this paper we show that the problem can be solved in polynomial time on interval graphs. The proposed algorithm runs in $O ( n ^ { 4 } )$ time, where $n$ is the number of vertices of the input graph, and bases on a dynamic programming approach.

Keywords: Longest path problem, interval graphs, polynomial algorithm, complexity, dynamic programming.

# 1 Introduction

A well studied problem in graph theory with numerous applications is the Hamiltonian path problem, i.e., the problem of determining whether a graph is Hamiltonian; a graph is said to be Hamiltonian if it contains a Hamiltonian path, that is, a simple path in which every vertex of the graph appears exactly once. Even if a graph is not Hamiltonian, it makes sense in several applications to search for a longest path, or equivalently, to find a maximum induced subgraph of the graph which is Hamiltonian. However, finding a longest path seems to be more difficult than deciding whether or not a graph admits a Hamiltonian path. Indeed, it has been proved that even if a graph has a Hamiltonian path, the problem of finding a path of length $n - n ^ { \varepsilon }$ for any $\varepsilon < 1$ is NP-hard, where $n$ is the number of vertices of the graph [15]. Moreover, there is no polynomial-time constant-factor approximation algorithm for the longest path problem unless P=NP [15]. For related results see also [7–9, 22, 23].

It is clear that the longest path problem is NP-hard on every class of graphs on which the Hamiltonian path problem is NP-complete. The Hamiltonian path problem is known to be NP-complete in general graphs [10, 11], and remains NP-complete even when restricted to some small classes of graphs such as split graphs [13], chordal bipartite graphs, split strongly chordal graphs [17], circle graphs [5], planar graphs [11], and grid graphs [14]. However, it makes sense to investigate the tractability of the longest path problem on the classes of graphs for which the Hamiltonian path problem admits polynomial time solutions. Such classes include interval graphs [16], circular-arc graphs [6], convex bipartite graphs [17], and co-comparability graphs [4]. Note that the problem of finding a longest path on proper interval graphs is easy, since all connected proper interval graphs have a Hamiltonian path which can be computed in linear time [2]. On the contrary, not all interval graphs are Hamiltonian; in the case where an interval graph has a Hamiltonian path, it can be computed in linear time [16]. However, in the case where an interval graph is not Hamiltonian, there is no known algorithm for finding a longest path on it.

In contrast to the Hamiltonian path problem, there are few known polynomial time solutions for the longest path problem, and these restrict to trees and some small graph classes. Specifically, a linear time algorithm for finding a longest path in a tree was proposed by Dijkstra around 1960, a formal proof of which can be found in [3]. Later, through a generalization of Dijkstra’s algorithm for trees, Uehara and Uno [20] solved the longest path problem for weighted trees and block graphs in linear time and space, and for cacti in $O ( n ^ { 2 } )$ time and space, where $n$ and $m$ denote the number of vertices and edges of the input graph, respectively. More recently, polynomial algorithms have been proposed that solve the longest path problem on bipartite permutation graphs in $O ( n )$ time and space [21], and on ptolemaic graphs in $O ( n ^ { 5 } )$ time and $O ( n ^ { 2 } )$ space [19].

Furthermore, Uehara and Uno in [20] introduced a subclass of interval graphs, namely interval biconvex graphs, which is a superclass of proper interval and threshold graphs, and solved the longest path problem on this class in $O ( n ^ { 3 } ( m + n \log n ) )$ time. As a corollary, they showed that a longest path of a threshold graph can be found in $O ( n + m )$ time and space. They left open the complexity of the longest path problem on interval graphs.

In this paper, we resolve the open problem posed in [20] by showing that the longest path problem admits a polynomial time solution on interval graphs. Interval graphs form an important and well-known class of perfect graphs [13]; a graph $G$ is an interval graph if its vertices can be put in a one-to-one correspondence with a family of intervals on the real line, such that two vertices are adjacent in $G$ if and only if their corresponding intervals intersect. In particular, we propose an algorithm for solving the longest path problem on interval graphs which runs in $O ( n ^ { 4 } )$ time using a dynamic programming approach. Thus, not only we answer the question left open by Uehara and Uno in [20], but also improve the known time complexity of the problem on interval biconvex graphs, a subclass of interval graphs [20].

Interval graphs form a well-studied class of perfect graphs, have important properties, and admit polynomial time solutions for several problems that are NP-complete on general graphs (see e.g. [1, 13, 16]). Moreover, interval graphs have received a lot of attention due to their applicability to DNA physical mapping problems [12], and find many applications in several fields and disciplines such as genetics, molecular biology, scheduling, VLSI circuit design, archaeology and psychology [13].

# 2 Theoretical Framework

We consider finite undirected graphs with no loops or multiple edges. For a graph $G$ , we denote its vertex and edge set by $V ( G )$ and $E ( G )$ , respectively. An undirected edge is a pair of distinct vertices $u , v \in V ( G )$ , and is denoted by $u v$ . We say that the vertex $u$ is adjacent to the vertex $v$ or, equivalently, the vertex $u$ sees the vertex $v$ , if there is an edge $u v$ in $G$ . Let $S$ be a set of vertices of a graph $G$ . Then, the cardinality of the set $S$ is denoted by $| S |$ and the subgraph of $G$ induced by $S$ is denoted by $G [ S ]$ . The set $N ( v ) = \{ u \in V ( G ) : u v \in E ( G ) \}$ is called the neighborhood of the vertex $v \in V ( G )$ in $G$ , sometimes denoted by $N _ { G } ( v )$ for clarity reasons. The set $N [ v ] = N ( v ) \cup \{ v \}$ is called the closed neighborhood of the vertex $v \in V ( G )$ .

A simple path of a graph $G$ is a sequence of distinct vertices $v _ { 1 } , v _ { 2 } , \ldots , v _ { k }$ such that $v _ { i } v _ { i + 1 } \in E ( G )$ , for each i, $1 \leq i \leq k - 1$ , and is denoted by $( v _ { 1 } , v _ { 2 } , \ldots , v _ { k } )$ ; throughout the paper all paths considered are simple. We denote by $V ( P )$ the set of vertices in the path $P$ , and define the length of the path $P$ to be the number of vertices in $P$ , i.e., $| P | = | V ( P ) |$ . We call right endpoint of a path $P = ( v _ { 1 } , v _ { 2 } , \ldots , v _ { k } )$ the last vertex $v _ { k }$ of $P$ . Moreover, let $P = ( v _ { 1 } , v _ { 2 } , \ldots , v _ { i - 1 } , v _ { i } , v _ { i + 1 } , \ldots , v _ { j } , v _ { j + 1 } , v _ { j + 2 } , \ldots , v _ { k } )$ and $P _ { 0 } = ( v _ { i } , v _ { i + 1 } , \dots , v _ { j } )$ be two paths of a graph. Sometimes, we shall denote the path $P$ by $P = ( v _ { 1 } , v _ { 2 } , \ldots , v _ { i - 1 } , P _ { 0 } , v _ { j + 1 } , v _ { j + 2 } , \ldots , v _ { k } )$ .

# 2.1 Structural Properties of Interval Graphs

A graph $G$ is an interval graph if its vertices can be put in a one-to-one correspondence with a family $F ^ { \dagger }$ of intervals on the real line such that two vertices are adjacent in $G$ if and only if the corresponding intervals intersect; $F$ is called an intersection model for $G$ [1]. The class of interval graphs is hereditary, that is, every induced subgraph of an interval graph $G$ is also an interval graph. Ramalingam and Rangan [18] proposed a numbering of the vertices of an interval graph; they stated the following lemma.

Lemma 1. (Ramalingam and Rangan [18]): The vertices of any interval graph $G$ can be numbered with integers $1 , 2 , \ldots , | V ( G ) |$ such that if $i < j < k$ and $i k \in E ( G )$ , then $j k \in E ( G )$ .

As shown in [18], the proposed numbering, which results after sorting the intervals of the intersection model of a graph $G$ on their right ends [1], can be obtained in $O ( | V ( G ) | + | E ( G ) | )$ time. An ordering of the vertices according to this numbering is found to be quite useful in solving some graph-theoretic problems on interval graphs [1, 18]. Throughout the paper, such an ordering is called a right-end ordering of $G$ . Let $u$ and $v$ be two vertices of $G$ ; if $\pi$ is a right-end ordering of $G$ , denote $u < _ { \pi } v$ if $u$ appears before $v$ in $\pi$ . In particular, if $\pi = ( u _ { 1 } , u _ { 2 } , \ldots , u _ { | V ( G ) | } )$ is a right-end ordering of $G$ , then $u _ { i } ~ < _ { \pi } ~ u _ { j }$ if and only if $i < j$ .

Lemma 2. Let $G$ be an interval graph, and let $\pi$ be a right-end ordering of $G$ . Let $P = ( v _ { 1 } , v _ { 2 } , \ldots , v _ { k } )$ be a path of $G$ , and let $v _ { \ell } \notin V ( P )$ be a vertex of $G$ such that $v _ { 1 } < _ { \pi } v _ { \ell } < _ { \pi } v _ { k }$ and $v _ { \ell } v _ { k } \notin E ( G )$ . Then, there exist two consecutive vertices $v _ { i - 1 }$ and $v _ { i }$ in $P$ , $2 \leq i \leq k$ , such that $v _ { i - 1 } v _ { \ell } \in E ( G )$ and $v _ { \ell } < _ { \pi } v _ { i }$ .

# 2.2 Normal Paths

Our algorithm for constructing a longest path of an interval graph $G$ uses a specific type of paths, namely normal paths.

Definition 1. Let $G$ be an interval graph, and let $\pi$ be a right-end ordering of $G$ . The path $P = ( v _ { 1 } , v _ { 2 } , \ldots , v _ { k } )$ of $G$ is called $a$ normal path, if $v _ { 1 }$ is the leftmost vertex of $V ( P )$ in $\pi$ , and for every $i$ , $2 \leq i \leq k$ , the vertex $v _ { i }$ is the leftmost vertex of $N ( v _ { i - 1 } ) \cap \{ v _ { i } , v _ { i + 1 } , . . . , v _ { k } \}$ in $\pi$ .

The notion of a normal path of an interval graph $G$ is a generalization of the notion of a typical path of $G$ ; the path $P = ( v _ { 1 } , v _ { 2 } , \ldots , v _ { k } )$ of an interval graph $G$ is called a typical path, if $v _ { 1 }$ is the leftmost vertex of $V ( P )$ in $\pi$ . The notion of a typical path was introduced by Arikati and Rangan [1], in order to solve the path cover problem on interval graphs; they proved the following result.

Lemma 3. (Arikati and Rangan $[ { 1 } / { } ]$ : Let $P$ be a path of an interval graph $G$ Then, there exists a typical path $P ^ { \prime }$ in $G$ such that $V ( P ^ { \prime } ) = V ( P )$ .

The following lemma is the basis of our algorithm for solving the longest path problem on interval graphs.

Lemma 4. Let $P$ be a path of an interval graph $G$ . Then, there exists a normal path $P ^ { \prime }$ of $G$ , such that $V ( P ^ { \prime } ) = V ( P )$ .

# 3 Interval Graphs and the Longest Path Problem

In this section we present our algorithm, which we call Algorithm LP Interval, for solving the longest path problem on interval graphs; it consists of three phases and works as follows:

Phase 1: it takes an interval graph $G$ and constructs the auxiliary interval graph $H$ ; Phase 2: it computes a longest path $P$ on $H$ using Algorithm LP on $\_ H$ ; Phase 3: it computes a longest path $\hat { P }$ on $G$ from the path $P$ ;

The proposed algorithm computes a longest path $P$ of the graph $H$ using dynamic programming techniques and, then, computes a longest path $\widehat { P }$ of $G$ from the path $P$ b. We next describe in detail the three phases of our algorithm and prove properties of the constructed graph $H$ which will be used for proving the correctness of the algorithm.

# 3.1 The interval graph $\pmb { H }$

In this section we present Phase 1 of the algorithm: given an interval graph $G$ and a right-end ordering $\pi$ of $G$ , we construct the interval graph $H$ and a right-end ordering $\sigma$ of $H$ .

I Construction of $H$ and $\sigma$ : Let $G$ be an interval graph and let $\pi = ( v _ { 1 } , v _ { 2 } , \ldots , v _ { | V ( G ) | } )$ be a right-end ordering of $G$ . Initially, set $V ( H ) = V ( G )$ , $\sigma = \pi$ , and $A = \emptyset$ . Traverse the vertices of $\pi$ from left to right and do the following: for every vertex $v _ { i }$ add two vertices $a _ { i , 1 }$ and ${ a } _ { i , 2 }$ to $V ( H )$ and make both these vertices to be adjacent to every vertex in $N _ { G } [ v _ { i } ] \cap \{ v _ { i } , v _ { i + 1 } , . . . , v _ { | V ( G ) | } \}$ ; add and to $A$ . Update $a _ { i , 1 }$ ${ a } _ { i , 2 }$ $\sigma$ such that $a _ { 1 , 1 } < _ { \sigma } a _ { 1 , 2 } < _ { \sigma } v _ { 1 }$ , and $v _ { i - 1 } < _ { \sigma } a _ { i , 1 } < _ { \sigma } a _ { i , 2 } < _ { \sigma } v _ { i }$ for every $i$ , $2 \leq i \leq | V ( G ) |$ .

We call the constructed graph $H$ the stable-connection graph of the graph $G$ . Hereafter, we will denote by $n$ the number $| V ( H ) |$ of vertices of the graph $H$ and by $\sigma = ( u _ { 1 } , u _ { 2 } , \ldots , u _ { n } )$ the constructed ordering of $H$ . By construction, the vertex set of the graph $H$ consists of the vertices of the set $C = V ( G )$ and the vertices of the set $A$ . We will refer to $C$ as the set of the connector vertices $c$ of the graph $H$ and to $A$ as the set of stable vertices $a$ of the graph $H$ ; we denote these sets by $C ( H )$ and $A ( H )$ , respectively. Note that $| A ( H ) | = 2 | V ( G ) |$ .

By the construction of the stable-connection graph $H$ , all neighbors of a stable vertex $a \in A ( H )$ are connector vertices $c \in C ( H )$ , such that $\textit { a } < _ { \sigma } \textit { c }$ . Moreover, observe that all neighbors of a stable vertex form a clique in $G$ and, thus, also in $H$ . For every connector vertex $u _ { i } \in C ( H )$ , we denote by $\boldsymbol { u } _ { f ( u _ { i } ) }$ and $u _ { h ( u _ { i } ) }$ the leftmost and rightmost neighbor of $u _ { i }$ in $\sigma$ , respectively, which appear before $u _ { i }$ in $\sigma$ , i.e., $u _ { f ( u _ { i } ) } < _ { \sigma } u _ { h ( u _ { i } ) } < _ { \sigma } u _ { i }$ . Note that $\boldsymbol { u } _ { f ( u _ { i } ) }$ and $u _ { h ( u _ { i } ) }$ are distinct stable vertices, for every connector vertex $u _ { i }$ .

Lemma 5. Let $G$ be an interval graph. The stable-connection graph $H$ of $G$ is an interval graph, and the vertex ordering $\sigma$ is a right-end ordering of $H$ .

Definition 2. Let $H$ be the stable-connection graph of an interval graph $G$ , and let $\sigma = ( u _ { 1 } , u _ { 2 } , \ldots , u _ { n } )$ be the right-end ordering of $H$ . For every pair of indices $i , j$ , $1 \leq i \leq j \leq n$ , we define the graph $H ( i , j )$ to be the subgraph $H [ S ]$ of $H$ , induced by the the set $S = \{ u _ { i } , u _ { i + 1 } , \dotsc , u _ { j } \} \setminus \{ u _ { k } \in C ( H ) : u _ { f ( u _ { k } ) } < _ { \sigma } u _ { i } \}$ .

The following properties hold for every induced subgraph $H ( i , j )$ , $1 \leq i \leq$ $j \le n$ , and they are used for proving the correctness of Algorithm LP on $\boldsymbol { \mathcal { H } }$ .

Observation 1 Let $u _ { k }$ be a connector vertex of $H ( i , j )$ , i.e., $u _ { k } \in C ( H ( i , j ) )$ . Then, for every vertex $u _ { \ell } ~ \in ~ V ( H ( i , j ) )$ , such that $u _ { k } \ < _ { \sigma } \ u _ { \ell }$ and $u _ { k } u _ { \ell } \in$ $E ( H ( i , j ) )$ , $u _ { \ell }$ is also a connector vertex of $H ( i , j )$ .

Observation 2 No two stable vertices of $H ( i , j )$ are adjacent.

Lemma 6. Let $P = ( v _ { 1 } , v _ { 2 } , \ldots , v _ { k } )$ be a normal path of $H ( i , j )$ . Then:

# Algorithm LP on H

Input: a stable-connection graph $H$ , a right-end ordering $\sigma = ( u _ { 1 } , u _ { 2 } , \ldots , u _ { n } )$ of $H$ .   
Output: a longest binormal path of $H$ .

for $j = 1$ to $_ n$ for $i = j$ downto 1 if $i = j$ and $u _ { i } \in A ( H )$ then $\ell ( u _ { i } ; i , i ) \gets 1 ; P ( u _ { i } ; i , i ) = ( u _ { i } )$ ; if $i \neq j$ then for every stable vertex $u _ { k } \in A ( H )$ , $i \le k \le j - 1$ $\ell ( u _ { k } ; i , j ) \gets \ell ( u _ { k } ; i , j - 1 )$ ; $P ( u _ { k } ; i , j ) = P ( u _ { k } ; i , j - 1 )$ ; {initialization} if $u _ { j }$ is a stable vertex of $H ( i , j )$ , i.e., $u _ { j } \in A ( H )$ then $\ell ( u _ { j } ; i , j ) \gets 1 ; P ( u _ { j } ; i , j ) = ( u _ { j } )$ ; if $u _ { j }$ is a connector vertex of $H ( i , j )$ , i.e., $u _ { j } \in C ( H )$ and $i \leq f ( u _ { j } )$ then execute process $( H ( i , j ) )$ ;

compute the $m a x \{ \ell ( u _ { k } ; 1 , n ) : u _ { k } \in A ( H ) \}$ and the corresponding path $P ( u _ { k } ; 1 , n )$ ;

where the procedure process() is as follows:

$$
\mathtt { p r o c e s s } ( H ( i , j ) )
$$

for $y = f ( u _ { j } ) + 1$ to $j - 1$ for $x = f ( u _ { j } )$ to $y - 1$ $\{ u _ { x }$ and $u _ { y }$ are adjacent to $u _ { j } \}$ if $u _ { x } , u _ { y } \in A ( H )$ then $w _ { 1 } \gets \ell ( u _ { x } ; i , j - 1 )$ ; $P _ { 1 } ^ { \prime } = P ( u _ { x } ; i , j - 1 )$ ; $w _ { 2 }  \ell ( u _ { y } ; x + 1 , j - 1 ) ; P _ { 2 } ^ { \prime } = P ( u _ { y } ; x + 1 , j - 1 ) ;$ if $w _ { 1 } + w _ { 2 } + 1 > \ell ( u _ { y } ; i , j )$ then $\ell ( u _ { y } ; i , j ) \gets w _ { 1 } + w _ { 2 } + 1$ ; $P ( u _ { y } ; i , j ) = ( P _ { 1 } ^ { \prime } , u _ { j } , P _ { 2 } ^ { \prime } )$ ;   
return the value $\ell ( u _ { k } ; i , j )$ and the path $P ( u _ { k } ; i , j )$ , $\forall ~ u _ { k } \in A ( H ( f ( u _ { j } ) + 1 , j - 1 ) )$ ;   
(a) For any two stable vertices $v _ { r }$ and $v _ { \ell }$ in $P$ , $v _ { r }$ appears before ${ v } _ { \ell }$ in $P$ if and only if $v _ { r } < _ { \sigma } v _ { \ell }$ .   
(b) For any two connector vertices $v _ { r }$ and v\` in $P$ , if v\` appears before $v _ { r }$ in $P$ and $v _ { r } < _ { \sigma } v _ { \ell }$ , then $v _ { r }$ does not see the previous vertex $v _ { \ell - 1 }$ of ${ v } _ { \ell }$ in $P$ .

# 3.2 Finding a longest path on $\pmb { H }$

In this section we present Phase 2 of Algorithm LP Interval. Let $G$ be an interval graph and let $H$ be the stable-connection graph of $G$ constructed in Phase 1. We next present Algorithm LP on $\_ H$ , which computes a longest path of the graph $H$ . Let us first give some definitions and notations necessary for the description of the algorithm.

Definition 3. Let $H$ be a stable-connection graph, and let $P$ be a path of $H ( i , j )$ , $1 \leq i \leq j \leq n$ . The path $P$ is called binormal if $P$ is a normal path of $H ( i , j )$ , both endpoints of $P$ are stable vertices, and no two connector vertices are consecutive in $P$ .

Input: an interval graph $G$ and a right-end ordering $\pi$ of $G$ .   
Output: a longest path $\hat { P }$ of $G$ .   
1. Construct the stable-connection graph $H$ of $G$ and the right-end ordering $\sigma$ of $H$ ; let $V ( H ) = C \cup A$ , where $C = V ( G )$ and $A$ are the sets of the connector and stable vertices of $H$ , respectively;   
2. Compute a longest binormal path $P$ of $H$ , using Algorithm LP on $_ { - } H$ ; let $P = ( v _ { 1 } , v _ { 2 } , \ldots , v _ { 2 k } , v _ { 2 k + 1 } )$ , where $v _ { 2 i } \in C$ , $1 \leq i \leq k$ , and $v _ { 2 i + 1 } \in A$ , $0 \leq i \leq k$ ;   
3. Compute a longest path $\boldsymbol { \hat { P } } = ( v _ { 2 } , v _ { 4 } , \dots , v _ { 2 k } )$ of $G$ , by deleting all stable vertices $\{ v _ { 1 } , v _ { 3 } , \ldots , v _ { 2 k + 1 } \}$ bfrom the longest binormal path $P$ of $H$ ;

Notation 1 Let $H$ be a stable-connection graph, and let $\sigma = ( u _ { 1 } , u _ { 2 } , \ldots , u _ { n } )$ be the right-end ordering of $H$ . For every stable vertex $u _ { k } \in A ( H ( i , j ) )$ , we denote by $P ( u _ { k } ; i , j )$ a longest binormal path of $H ( i , j )$ with $u _ { k }$ as its right endpoint, and by $\ell ( u _ { k } ; i , j )$ the length of $P ( u _ { k } ; i , j )$ .

Since any binormal path is a normal path, Lemma 6 also holds for binormal paths. Moreover, since $P ( u _ { k } ; i , j )$ is a binormal path, it follows that its right endpoint $u _ { k }$ is also the rightmost stable vertex of $P$ in $\sigma$ , due to Lemma 6(a).

Algorithm LP on $\boldsymbol { \mathcal { H } }$ , which is presented in Figure 1, computes for every induced subgraph $H ( i , j )$ and for every stable vertex $u _ { k } \in A ( H ( i , j ) )$ , the length $\ell ( u _ { k } ; i , j )$ and the corresponding path $P ( u _ { k } ; i , j )$ . Since $H ( 1 , n ) = H$ , it follows that the maximum among the values $\ell ( u _ { k } ; 1 , n )$ , where $u _ { k } \in A ( H )$ , is the length of a longest binormal path $P ( u _ { k } ; 1 , n )$ of $H$ . In Section 4.2 we prove that the length of a longest path of $H$ equals to the length of a longest binormal path of $H$ . Thus, the binormal path $P ( u _ { k } ; 1 , n )$ computed by Algorithm LP on $\_ H$ is also a longest path of $H$ .

# 3.3 Finding a longest path on $\pmb { G }$

During Phase 3 of our Algorithm LP Interval, we compute a path $\widehat { P }$ from the longest binormal path $P$ of $H$ , computed by Algorithm LP on $\boldsymbol { \mathcal { H } }$ b, by simply deleting all the stable vertices of $P$ . In Section 4.2 we prove that the resulting path $\widehat { P }$ is a longest path of the interval graph $G$ .

bIn Figure 2, we present our Algorithm LP Interval for solving the longest path problem on an interval graph $G$ ; note that Steps 1, 2, and 3 of the algorithm correspond to the presented Phases 1, 2, and 3, respectively.

# 4 Correctness and Time Complexity

In this section we prove the correctness of our algorithm and compute its time complexity. More specifically, in Section 4.1 we show that Algorithm LP on $_ { - H }$ computes a longest binormal path $P$ of the graph $H$ (in Lemma 13 we prove that this path is also a longest path of $H$ ), while in Section 4.2 we show that the length of a longest binormal path $P$ of $H$ is equal to $2 k + 1$ , where $k$ is the length of a longest path of $G$ . Finally, we show that the path $\hat { P }$ constructed at Step 3 of Algorithm LP Interval is a longest path of $G$ .

# 4.1 Correctness of Algorithm LP on H

We next prove that Algorithm LP on $\mathbf { \nabla } _ { H }$ correctly computes a longest binormal path of the graph $H$ . The following lemmas appear useful in the proof of the algorithm’s correctness.

Lemma 7. Let $H$ be a stable-connection graph, and let $\sigma = ( u _ { 1 } , u _ { 2 } , \ldots , u _ { n } )$ be the right-end ordering of $H$ . Let $P$ be a longest binormal path of $H ( i , j )$ with $u _ { y }$ as its right endpoint, let $u _ { k }$ be the rightmost connector vertex of $H ( i , j )$ in $\sigma$ , and let $u _ { f ( u _ { k } ) + 1 } \le _ { \sigma } u _ { y } \le _ { \sigma } u _ { h ( u _ { k } ) }$ . Then, there exists a longest binormal path $P ^ { \prime }$ of $H ( i , j )$ with $u _ { y }$ as its right endpoint, which contains the connector vertex $u _ { k }$ .

Lemma 8. Let $H$ be a stable-connection graph, and let $\sigma$ be the right-end ordering of $H$ . Let $P = ( P _ { 1 } , v _ { \ell } , P _ { 2 } )$ be a binormal path of $H ( i , j )$ , and let $v _ { \ell }$ be $a$ connector vertex of $H ( i , j )$ . Then, $P _ { 1 }$ and $P _ { 2 }$ are binormal paths of $H ( i , j )$ .

Lemma 9. Let $H$ be a stable-connection graph, and let $\sigma = ( u _ { 1 } , u _ { 2 } , \ldots , u _ { n } )$ be the right-end ordering of $H$ . Let $P _ { 1 }$ be a binormal path of $H ( i , j - 1 )$ with $u _ { x }$ as its right endpoint, and let $P _ { 2 }$ be a binormal path of $H ( x + 1 , j - 1 )$ with $u _ { y }$ as its right endpoint, such that $V ( P _ { 1 } ) \cap V ( P _ { 2 } ) = \emptyset$ . Suppose that $u _ { j }$ is a connector vertex of $H$ and that $u _ { i } \le _ { \sigma } u _ { f ( u _ { j } ) } \le _ { \sigma } u _ { x }$ . Then, $P = ( P _ { 1 } , u _ { j } , P _ { 2 } )$ is a binormal path of $H ( i , j )$ with $u _ { y }$ as its right endpoint.

Lemma 10. Let $H$ be a stable-connection graph, and let $\sigma$ be the right-end ordering of $H$ . For every induced subgraph $H ( i , j )$ of $H$ , $1 \leq i \leq j \leq n$ , and for every stable vertex $u _ { y } \in A ( H ( i , j ) )$ , Algorithm $L P _ { - } o n _ { - } H$ computes the length $\ell ( u _ { y } ; i , j )$ of a longest binormal path of $H ( i , j )$ which has $u _ { y }$ as its right endpoint and, also, the corresponding path $P ( u _ { y } ; i , j )$ .

Proof (sketch). Let $P$ be a longest binormal path of the stable-connection graph $H ( i , j )$ , which has a vertex $u _ { y } \in A ( H ( i , j ) )$ as its right endpoint. Consider first the case where $C ( H ( i , j ) ) = \emptyset$ ; the graph $H ( i , j )$ is consisted of a set of stable vertices $A ( H ( i , j ) )$ , which is an independent set, due to Observation 2. Therefore, in this case Algorithm LP on $\_ H$ sets $\ell ( u _ { y } ; i , j ) = 1$ for every vertex $u _ { y } \in A ( H ( i , j ) )$ , which is indeed the length of the longest binormal path $P ( u _ { y } ; i , j ) = ( u _ { y } )$ o f $H ( i , j )$ which has $u _ { y }$ as its right endpoint. Therefore, the lemma holds for every induced subgraph $H ( i , j )$ , for which $C ( H ( i , j ) ) = \emptyset$ .

We examine next the case where $C ( H ( i , j ) ) \neq \emptyset$ . Let $C ( H ) = \{ c _ { 1 } , c _ { 2 } , \ldots , c _ { k } , \ldots , c _ { t } \}$ be the set of connector vertices of $H$ , where $c _ { 1 } < _ { \sigma } c _ { 2 } < _ { \sigma } . . . < _ { \sigma } c _ { k } < _ { \sigma } . . . < _ { \sigma } c _ { t }$ . Let $\sigma ~ = ~ ( u _ { 1 } , u _ { 2 } , \ldots , u _ { n } )$ be the vertex ordering of $H$ constructed in Phase 1. Recall that, by the construction of $H$ , $n = 3 t$ , and $A ( H ) = V ( H ) \setminus C ( H )$ is the set of stable vertices of $H$ .

Let $H ( i , j )$ be an induced subgraph of $H$ , and let $c _ { k }$ be the rightmost connector vertex of $H ( i , j )$ in $\sigma$ . The proof of the lemma is done by induction on the index $k$ of the rightmost connector vertex $c _ { k }$ of $H ( i , j )$ . More specifically, given a connector vertex $c _ { k }$ of $H$ , we prove that the lemma holds for every induced subgraph $H ( i , j )$ of $H$ , which has $c _ { k }$ as its rightmost connector vertex in $\sigma$ . To this end, in both the induction basis and the induction step, we distinguish three cases on the position of the stable vertex $u _ { y }$ in the ordering $\sigma$ : $u _ { i } \le _ { \sigma } u _ { y } \le _ { \sigma } u _ { f ( c _ { k } ) }$ , $u _ { h ( c _ { k } ) } < _ { \sigma } u _ { y } \le _ { \sigma } u _ { j }$ , and $u _ { f ( c _ { k } ) + 1 } \le _ { \sigma } u _ { y } \le _ { \sigma } u _ { h ( c _ { k } ) }$ . In each of these three cases, we examine first the length of a longest binormal path of $H ( i , j )$ with $u _ { y }$ as its right endpoint and, then, we compare this value to the length of the path computed by Algorithm LP on $\_ H$ . Moreover, we prove that the path computed by Algorithm LP on $\boldsymbol { \mathcal { H } }$ is indeed a binormal path with $u _ { y }$ as its right endpoint. $\boxed { \begin{array} { r l } \end{array} }$

Due to Lemma 10, and since the output of Algorithm LP on $\boldsymbol { \mathcal { H } }$ is the maximum among the lengths $\ell ( u _ { y } ; 1 , n )$ , $u _ { y } \in A ( H ( 1 , n ) )$ , along with the corresponding path, it follows that Algorithm LP on $\_ H$ computes a longest binormal path of $H ( 1 , n )$ with right endpoint a vertex $u _ { y } \in A ( H ( 1 , n ) )$ . Thus, since $H ( 1 , n ) = H$ , we obtain the following result.

Lemma 11. Let $G$ be an interval graph. Algorithm $L P$ on H computes a longest binormal path of the stable-connection graph $H$ of the graph $G$ .

# 4.2 Correctness of Algorithm LP Interval

We next show that Algorithm LP Interval correctly computes a longest path of an interval graph $G$ . The correctness proof is based on the following property: for any longest path $P$ of $G$ there exists a longest binormal path $P ^ { \prime }$ of $H$ , such that $| P ^ { \prime } | = 2 | P | + 1$ and vice versa (this property is proved in Lemma 12). Therefore, we obtain that the length of a longest binormal path $P$ of $H$ computed by Algorithm LP on $\_ H$ is equal to $2 k + 1$ , where $k$ is the length of a longest path $\widehat { P }$ of $G$ . Next, we show that the length of a longest binormal path of $H$ bequals to the length of a longest path of $H$ . Finally, we show that the path $\widehat { P }$ computed at Step 3 of Algorithm LP Interval is indeed a longest path of $G$ .

Lemma 12. Let $H$ be the stable-connection graph of an interval graph $G$ . Then, for any longest path $P$ of $G$ there exists a longest binormal path $P ^ { \prime }$ of $H$ , such that $| P ^ { \prime } | = 2 | P | + 1$ and vice versa.

Proof. Let $\sigma$ be the right-end ordering of the graph $H$ constructed in Phase 1.

( $\Longrightarrow$ ) Let $P = ( v _ { 1 } , v _ { 2 } , \ldots , v _ { k } )$ be a longest path of $G$ , i.e., $| P | = k$ . We will   
show that there exists a binormal path $P ^ { \prime }$ of $H$ such that $| P ^ { \prime } | = 2 k + 1$ . Since $G$ is   
an induced subgraph of $H$ , the path $P$ of $G$ is a path of $H$ as well. We construct   
a path $\widehat { P }$ of $H$ from $P$ , by adding to $P$ the appropriate stable vertices, using the   
bfollowing procedure. Initially, set ${ \hat { P } } = P$ and for every subpath $( v _ { i } , v _ { i + 1 } )$ of the   
path $\widehat { P }$ , $1 \leq i \leq k - 1$ b, do the following: consider first the case where $v _ { i } < _ { \sigma } v _ { i + 1 }$ ;   
bthen, by the construction of $H$ , is adjacent to both stable vertices and $v _ { i + 1 }$ $a _ { i , 1 }$

${ a } _ { i , 2 }$ associated with the connector vertex $v _ { i }$ . If $a _ { i , 1 }$ has not already been added to $\widehat { P }$ , then replace the subpath $( v _ { i } , v _ { i + 1 } )$ by the path $\left( v _ { i } , a _ { i , 1 } , v _ { i + 1 } \right)$ ; otherwise, breplace the subpath $( v _ { i } , v _ { i + 1 } )$ by the path $\left( v _ { i } , a _ { i , 2 } , v _ { i + 1 } \right)$ . Similarly, in the case where $v _ { i + 1 } < _ { \sigma } v _ { i }$ , replace the subpath $( v _ { i } , v _ { i + 1 } )$ by the path $( v _ { i } , a _ { i + 1 , 1 } , v _ { i + 1 } )$ or $( v _ { i } , a _ { i + 1 , 2 } , v _ { i + 1 } )$ , respectively. Finally, consider the endpoint $v _ { 1 }$ (resp. $v _ { k }$ ) of $\widehat { P }$ . If $_ { a _ { 1 , 1 } }$ (resp. ${ a } _ { k , 1 }$ ) has not already been added to $\widehat { P }$ , then add $_ { a _ { 1 , 1 } }$ (resp. ${ \boldsymbol { a } } _ { k , 1 }$ ) as the first (resp. last) vertex of $\widehat { P }$ b; otherwise, add $_ { a _ { 1 , 2 } }$ (resp. ${ a } _ { k , 2 }$ ) as the first (resp. last) vertex of $\widehat { P }$ .

bBy the construction of $\widehat { P }$ it is easy to see that for every connector vertex $v$ of $P$ bwe add two stable vertices as neighbors of $v$ in $\widehat { P }$ , and since in $H$ there are bexactly two stable vertices associated with every connector vertex $v$ , it follows that every stable vertex of $H$ appears at most once in $\widehat { P }$ . Furthermore, since we add in total $k + 1$ stable vertices to $P$ , where $| P | = k$ b, it follows that $| \widehat { P } | = 2 k + 1$ . Denote now by $P ^ { \prime }$ a normal path of $H$ such that $V ( P ^ { \prime } ) = V ( \widehat { P } )$ b. Such a path exists, due to Lemma 4. Due to the above construction, the path $\widehat { P }$ is consisted of $k + 1$ stable vertices and $k$ bconnector vertices. Thus, since no two stable vertices are adjacent in $H$ due to Observation 2, and since $P ^ { \prime }$ is a normal path of $H$ , it follows that $P ^ { \prime }$ is a binormal path of $H$ . Thus, for any longest path $P$ of $G$ there exists a binormal path $P ^ { \prime }$ of $H$ , such that $| P ^ { \prime } | = 2 | P | + 1$ .

( $\Longleftarrow$ ) Consider now a longest binormal path $P ^ { \prime } = ( v _ { 1 } , v _ { 2 } , \ldots , v _ { \ell } )$ of $H$ . Since $P ^ { \prime }$ is binormal, it follows that $\ell = 2 k + 1$ , and that $P ^ { \prime }$ has $k$ connector vertices and $k + 1$ stable vertices, for some $k \geq 1$ . We construct a path $P$ by deleting all stable vertices from the path $P ^ { \prime }$ of $H$ . By the construction of $H$ , all neighbors of a stable vertex $a$ are connector vertices and form a clique in $G$ ; thus, for every subpath $( v , a , v ^ { \prime } )$ of $P ^ { \prime }$ , $v$ is adjacent to $v ^ { \prime }$ in $G$ . It follows that $P$ is a path of $G$ . Since we removed all the $k + 1$ stable vertices of $P ^ { \prime }$ , it follows that $| P | = k$ , i.e., $| P ^ { \prime } | = 2 | P | + 1$ .

Summarizing, we have constructed a binormal path $P ^ { \prime }$ of $H$ from a longest path $P$ of $G$ such that $| P ^ { \prime } | = 2 | P | + 1$ , and a path $P$ of $G$ from a longest binormal path $P ^ { \prime }$ of $H$ such that $| P ^ { \prime } | = 2 | P | + 1$ . This completes the proof.

Lemma 13. For any longest path $P$ and any longest binormal path $P ^ { \prime }$ of $H$ , it holds $| P ^ { \prime } | = | P |$ .

Let $P$ be the longest binormal path of $H$ computed in Step 2 of Algorithm LP Interval, using Algorithm LP on $\_ H$ . Then, in Step 3 Algorithm LP Interval computes the path $\widehat { P }$ by deleting all stable vertices from $P$ . By the construction of $H$ b, all neighbors of a stable vertex $a$ are connector vertices and form a clique in $G$ ; thus, for every subpath $( \boldsymbol { v } , \boldsymbol { a } , \boldsymbol { v ^ { \prime } } )$ of $P$ , $v$ is adjacent to $v ^ { \prime }$ in $G$ . It follows that $\hat { P }$ is a path of $G$ . Moreover, since $P$ is binormal, it has $k$ connector vertices and $k + 1$ stable vertices, i.e., $| P | = 2 k + 1$ , where $k \geq 1$ . Thus, since we have removed all $k + 1$ stable vertices of $P$ , it follows that $| \widehat { P } | = k$ and, thus, $\widehat { P }$ is a longest path of $G$ b b due to Lemma 12. Thus, we have proved the following result.

Theorem 1. Algorithm LP Interval computes a longest path of an interval graph $G$ .

# 4.3 Time Complexity

Let $G$ be an interval graph on $| V ( G ) | = n$ vertices and $| E ( G ) | = m$ edges. It has been shown that we can obtain the right-end ordering $\pi$ of $G$ , which results from numbering the intervals after sorting them on their right ends, in $O ( n + m )$ time [1, 18].

First, we show that Step 1 of Algorithm LP Interval, which constructs the stable-connection graph $H$ of the graph $G$ , takes $O ( n ^ { 2 } )$ time. Indeed, for every connector vertex $u _ { i }$ , $1 \leq i \leq n$ , we can add two stable vertices in $V ( H )$ in $O ( 1 )$ time and we can compute the specific neighborhood of $u _ { i }$ in $O ( n )$ time.

Step 2 of Algorithm LP Interval includes the execution of Algorithm LP on $\boldsymbol { \mathcal { H } }$ . The subroutine process() takes $O ( n ^ { 2 } )$ time, due to the $O ( n ^ { 2 } )$ pairs of the neighbors $u _ { x }$ and $u _ { y }$ of the connector vertex $u _ { j }$ in the graph $H ( i , j )$ . Additionally, the subroutine process() is executed at most once for each subgraph $H ( i , j )$ of $H$ , $1 \leq i \leq j \leq n$ , i.e., it is executed $O ( n ^ { 2 } )$ times. Thus, Algorithm LP on $\boldsymbol { \mathcal { H } }$ takes $O ( n ^ { 4 } )$ time.

Step 3 of Algorithm LP Interval can be executed in $O ( n )$ time since we simply traverse the vertices of the path $P$ , constructed by Algorithm LP on $\_ H$ , and delete every stable vertex.

Theorem 2. A longest path of an interval graph can be computed in $O ( n ^ { 4 } )$ time.

# 5 Concluding Remarks

In this paper we presented a polynomial-time algorithm for solving the longest path problem on interval graphs, which runs in $O ( n ^ { 4 } )$ time and, thus, provided a solution to the open problem stated by Uehara and Uno in [20] asking for the complexity status of the longest path problem on interval graphs. It would be interesting to see whether the ideas presented in this paper can be applied to find a polynomial solution to the longest path problem on convex and biconvex graphs, the complexities of which still remain open [20].

# Список литературы

1. S.R. Arikati and C. Pandu Rangan, Linear algorithm for optimal path cover problem on interval graphs, Inform. Proc. Lett. 35 (1990) 149–153.   
2. A.A. Bertossi, Finding Hamiltonian circuits in proper interval graphs, Inform. Proc. Lett. 17 (1983) 97–101.   
3. R. Bulterman, F. van der Sommen, G. Zwaan, T. Verhoeff, A. van Gasteren, and W. Feijen, On computing a longest path in a tree, Inform. Proc. Lett. 81 (2002) 93–96.   
4. P. Damaschke, J.S. Deogun, D. Kratsch, and G. Steiner, Finding Hamiltonian paths in cocomparability graphs using the bump number algorithm, Order 8 (1992) 383– 391.   
5. P. Damaschke, The Hamiltonian circuit problem for circle graphs is NP-complete, Inform. Proc. Lett. 32 (1989) 1–2.   
6. P. Damaschke, Paths in interval graphs and circular arc graphs. Discrete Math. 112 (1993) 49–64.   
7. T. Feder and R. Motwani, Finding large cycles in Hamiltonian graphs, Proc. 16th annual ACM-SIAM Symp. on Discrete Algorithms (SODA), ACM (2005) 166–175.   
8. H.N. Gabow, Finding paths and cycles of superpolylogarithmic length, Proc. 36th annual ACM Symp. on Theory of Computing (STOC), ACM (2004) 407–416.   
9. H.N. Gabow and S. Nie, Finding long paths, cycles and circuits, 19th annual International Symp. on Algorithms and Computation (ISAAC), LNCS 5369 (2008) 752–763.   
10. M.R. Garey and D.S. Johnson, Computers and Intractability: A Guide to the Theory of NP-completeness, W.H. Freeman, San Francisco, 1979.   
11. M.R. Garey, D.S. Johnson, and R.E. Tarjan, The planar Hamiltonian circuit problem is NP-complete, SIAM J. Computing 5 (1976) 704–714.   
12. P.W. Goldberg, M.C. Golumbic, H. Kaplan, and R. Shamir, Four strikes against physical mapping of DNA, Journal of Computational Biology 2 (1995) 139–152.   
13. M.C. Golumbic, Algorithmic Graph Theory and Perfect Graphs (Annals of Discrete Mathematics, Vol. 57), North-Holland Publishing Co., Amsterdam, The Netherlands, 2004.   
14. A. Itai, C.H. Papadimitriou, and J.L. Szwarcfiter, Hamiltonian paths in grid graphs, SIAM J. Computing 11 (1982) 676–686.   
15. D. Karger, R. Motwani, and G.D.S. Ramkumar, On approximating the longest path in a graph, Algorithmica 18 (1997) 82–98.   
16. J.M. Keil, Finding Hamiltonian circuits in interval graphs, Inform. Proc. Lett. 20 (1985) 201–206.   
17. H. Muller, Hamiltonian circuits in chordal bipartite graphs, ¨ Discrete Math. 156 (1996) 291–298.   
18. G. Ramalingam and C. Pandu Rangan, A unified approach to domination problems on interval graphs, Inform. Proc. Lett. 27 (1988) 271–274.   
19. Y. Takahara, S. Teramoto, and R. Uehara, Longest path problems on ptolemaic graphs, IEICE Trans. Inf. and Syst. 91-D (2008) 170–177.   
20. R. Uehara and Y. Uno, Efficient algorithms for the longest path problem, 15th annual International Symp. on Algorithms and Computation (ISAAC), LNCS 3341 (2004) 871–883.   
21. R. Uehara and G. Valiente, Linear structure of bipartite permutation graphs and the longest path problem, Inform. Proc. Lett. 103 (2007) 71–77.   
22. S. Vishwanathan, An approximation algorithm for finding a long path in Hamiltonian graphs, Proc. 11th annual ACM-SIAM Symp. on Discrete Algorithms (SODA), ACM (2000) 680–685.   
23. Z. Zhang, and H. Li, Algorithms for long paths in graphs, Theoret. Comput. Sci. 377 (2007) 25–34.