# Algorithms for Maximum Independent Sets

J. M. ROBSON

Department of Computer Science, Australian National University, GPO Box 4, Canberra, ACT 2600, Australia

Received February 5, 1985

An algorithm is presented which finds (the size of) a maximum independent set of an n vertex graph in time $O ( 2 ^ { 0 . 2 7 6 n } )$ improving on a previous bound of $O ( 2 ^ { n / 3 } )$ . The improvement comes principally from three sources: first, a modified recursive algorithm based on a more detailed study of the possible subgraphs around a chosen vertex; second, an improvement, not in the algorithm but in the time bound proved, by an argument about connected regular graphs; third, a time-space trade-off which can speed up recursive algorithms from a fairly wide class. $\circledast$ 1986 Academic Press, Inc.

# 1. IntroduCtION

Finding a maximum independent set (m.i.s.) of a graph is a well-known NP-hard problem, equivalent to finding a maximum clique of the complementary graph [3]. Several algorithms [1, 2] have been published intended to give reasonable average behaviour on instances of these problems with some input distribution. One algorithm [5] is specially designed to achieve a good worst case; it runs in time $O ( 2 ^ { c n } )$ for $c < 1 / 3$ where $\pmb { n }$ is the order of the graph and returns the size of a m.i.s.; it is easy to modify it if required to return one independent set of this maximum size.

This paper gives two versions of a new but similar algorithm which u $c$ reduced significantly below $\textstyle { \frac { 1 } { 3 } }$ . The first version runs in polynomial space in time $O ( 2 ^ { c n } )$ for $c < 0 . 2 9 6$ The second version, which uses exponential space, reduces the value of the constant to about 0.276. The way in which use of exponential space can speed up an exponential time recursive algorithm is simple and of wider applicability. For instance a naive algorithm to decide satisfiability of a CNF expression $\pmb { \cal E }$ of $\pmb { n }$ clauses over variables $x _ { 1 } , \ldots x _ { n }$ (or to decide the QBF expression $\forall x _ { 1 } \exists x _ { 2 } \dots x _ { n } ( E ) )$ would take time $O ( 2 ^ { n } )$ ; this can be reduced to $O ( 2 ^ { 0 . 7 7 3 n } )$ by the same technique.

Section 2 of the paper introduces the terminology, notation, and ideas which are common to the two versions of the algorithm. Sections 3 and 4 give the code and analysis of the polynomial space version of the algorithm which depends on an auxiliary function, presented separately in Section 5. Section 6 discusses the acceleration of this and other algorithms by use of exponential space and Section 7 draws some conclusions and suggests directions for further work.

# 2. BAsic COncEPtS

# 2.1. Notation and Terminology

Given a graph $\pmb { G }$ or $( V , E )$ , if $v \in V ,$ , the degree of $v$ in $G$ will be written $d ( v : G )$ or simply as $\pmb { d } ( \pmb { v } )$ where no ambiguity is likely. $N ( v )$ denotes the set of neighbours of $V$ in $\pmb { G }$ and $N ^ { 2 } ( v )$ denotes the set of neighbours in $G$ of vertices in $N ( v )$ excluding $v$ itself; $\overrightharpoon { N } ( v ) = v + N ( v )$ If $\pmb { \mathscr { u } } \in \mathscr { V }$ or $U \subset V ,$ we write $G - u$ or ${ \bf { \vec { G } } } - { \bf { \vec { U } } }$ for the graph induced on $V - \mathrm { ~ } \{ u \}$ or $\ b { V } - \ b { U }$ by $\pmb { G }$ and in general we write "subgraph" where strictly we mean induced subgraph.

In the program we write $e d g e ( v , w )$ for the predicate that $( v , w ) \in E$ and we adhere to Pascal-like conventions on bracketing, using $\left\{ \begin{array} { r l } \end{array} \right\}$ strictly for comments and [ ] for set constructors.

# 2.2. The Basic Recursive Structure

The algorithm is presented as a recursive function ms such that $m s ( G ) =$ m.i.s. of $G \}$ Most of the ideas in ms are very simple. The most fundamental idea is that given a vertex of $\pmb { G }$ (called $\pmb { B }$ in the program), any maximal independent set either contains $\pmb { B }$ (and therefore no neighbour of $\pmb { B }$ )or does not contain $\pmb { B } .$ This gives the simple recurrence

$$
m s \bigl ( G \bigr ) = m a x \bigl ( 1 + m s \bigl ( G - \overline { { { N } } } \bigl ( B \bigr ) \bigr ) , m s \bigl ( G - B \bigr ) \bigr ) .
$$

If $d ( B )$ is large $( \ge 8 )$ , the subproblem $G - \overline { { N } } ( B )$ is so much smaller than the original that the time bound of $k 2 ^ { c n }$ for $\pmb { G }$ follows inductively from the same bound for $( G - B )$ and $G - \overline { { N } } ( B )$ and the inequality $2 ^ { - 9 c } \overset { \cdot } { + } 2 ^ { - c } < 1 .$ If the algorithm does not find a vertex with high degree, it must consider the neighbourhood of some vertex in more detail.

# 2.3. The Auxiliary Function ms2

In the neighbourhood of a vertex (called $\pmb { A }$ )of low degree, another idea is useful. If the function is going to consider independent sets containing $\pmb { A }$ then it may ignore those that contain exactly one element of $N ( A )$ since such a set has the same size as one containing $\pmb { A }$ instead; even more so it may ignore an independent set containing no element of $\overline { { N } } ( A )$ Thus we have another recurrence

$$
m s \bigl ( G \bigr ) = m a x \bigl ( 1 + m s \bigl ( G - \overline { { { N } } } \bigl ( A \bigr ) \bigr ) , m s ^ { 2 } \bigl ( G - A , N \bigl ( A \bigr ) \bigr ) \bigr ) .
$$

Here $m s ^ { 2 } ( G , S )$ is the maximum size of an independent set of $\pmb { G }$ containing at least two elements of $\pmb { S } .$ (In fact the $m s ^ { 2 }$ we use is not exactly as defined. It sometimes "ignores" the extra information $s$ and returns the size of some independent set of $\pmb { G }$ which is at least as large as every independent set containing two or more elements of S. That change does not invalidate Eq. (2)).

If $d ( A )$ is small, then $m s ^ { 2 } ( G - A , N ( A ) )$ may be much faster to compute than $m s ( G - A )$ This suggests the algorithm's overall approach: two adjacent vertices are chosen with $d ( A )$ small and $d ( B )$ large; if $d ( A )$ is small enough for Eq. (2) to ensure fast computation then it is used; otherwise Eq. (1) is used and in the larger subproblem $( G - B )$ , the degree of $\pmb { A }$ has been reduced producing an approach to a graph where (2) will be useful.

# 2.4. Regular Graphs

The approach described above will be least effective in a regular graph (one where all vertices have the same degree), because then it is not even possible to choose $\pmb { A }$ and $\pmb { B }$ such that $d ( B ) > d ( A )$ For this reason, in the algorithm of [5], regular graphs required the most intricate analysis and produced the worst behaviour. In this paper we circumvent this problem by showing that regular graphs are rare enough to be irrelevant even to the worst case behaviour of the algorithm. Since disconnected graphs are easily dealt with and a connected regular graph of degree $\pmb { d }$ has no proper subgraph which is regular with degree $\pmb { d } _ { : }$ , any chain of recursive calls can include only one regular degree $\pmb { d }$ graph. As shown in Section 4, this implies that ignoring regular graphs of degree $< 8$ affects only the constant hidden in the $O ( 2 ^ { c n } )$ notation.

# 2.5. Dominance

One last idea is occasionally useful. A vertex $\pmb { A }$ is said to "dominate" $\pmb { B }$ if $\overline { { { N } } } ( A ) \subset \overline { { { N } } } ( B )$ If this is so, any independent set containing $\pmb { B }$ has the same size as another containing $\pmb { A }$ instead of $\pmb { B }$ ; this gives the recurrence

$$
m s ( G ) = m s ( G - B ) .
$$

This is a very restricted form of the notion of dominance discussed in [5]. In Section 5 we will also need a slightly more general case where an independent subset $\pmb { A }$ of $V$ "dominates" another subset $\pmb { B }$ in that $\cup _ { A } { \overline { { N } } } ( A )$ $\mathsf { \Lambda } \subset \mathsf { U } _ { B } \overline { { N } } ( B )$ and $| A | \geq | B | ;$ in this case by similar reasoning there is some m.i.s. which does not contain all of $\pmb { B }$ .

# 3. The Function ms

This is the polynomial space version of ms. Since the time bound to be shown is $O ( { \mathrm { p o l y n o m i a l } } ( n ) 2 ^ { c n } )$ for graphs of order $\pmb { n }$ , we can omit details which merely affect the polynomial. Thus we give the function in a Pascal-like language with many graph operations described in a loose mixture of English, Pascal, and mathematics on the understanding that they can be coded into Pascal procedures which will run in time polynomial in the order of the graph. The syntax of Pascal has also been modified to use return statements as the method of returning a result from a function and to include conditional expressions.

function ms(G: graph): integer;   
begin   
if not connected $( G )$ then begin $c : =$ smallest connected component of $G$ ; return $m s ( G - C ) + ( { \mathfrak { i } } { \mathfrak { f } } | C | \leq 2$ then 1 else $m s ( C ) )$ end;   
if $| G | \leq 1$ then return $| G |$ .   
choose $\pmb { A }$ , $\pmb { B }$ vertices of $\pmb { G }$ such that   
(i) $d ( A )$ is minimal and   
(ii) $( A , B )$ is an edge of $\pmb { G }$ and $d ( B )$ is maximal over all neighbours of   
vertices with degree $d ( A )$ ;   
if $d ( A ) = 1$ then return $\ddot { 1 } + m s ( G - \overrightarrow { N } ( A ) )$   
if $d ( A ) = 2$ then begin $B ^ { \prime } : = N ( A ) - B$ {the other neighbour of $\pmb { A }$ } if $e d g e ( B , B ^ { \prime } )$ then return $1 + \bar { m } s ( G - \overline { { N } } ( \tilde { A } ) )$ ; return $m a x ( 2 + m s ( G - \overline { { { N } } } ( B ) - \widetilde { N } ( B ^ { \prime } ) ) , 1 + m s ^ { 2 } ( G - \overline { { { N } } } ( A ) , N ^ { 2 } ( A ) ) )$ end;   
if $d ( A ) = 3$ then return $m a x ( m s ^ { 2 } ( G - A , N ( A ) ) , 1 + m s ( G - \widetilde { N } ( A ) ) )$   
if $\pmb { A }$ dominates $\pmb { B }$ then return $m s ( G - B )$   
return $m a x ( m s ( G - B ) , 1 + m s ( G - \overline { { { N } } } ( B ) ) )$   
end;

Only the case $d ( A ) = 2$ should need any further explanation. If $( B , B ^ { \prime } )$ is an edge then clearly there is some m.i.s. containing $\pmb { A }$ Otherwise the function considers independent sets containing either ( $\pmb { B }$ and $B ^ { \prime }$ ) or ( $\pmb { A }$ and at least two elements of $N ^ { 2 } ( A ) )$ ; there must be some m.i.s. of one of these forms since one containing $\pmb { A }$ and at most one element of $N ^ { 2 } ( A )$ could be modified to include $\pmb { B }$ and $\pmb { B } ^ { \prime }$ instead, without decreasing its size.

# 4. ANALYsIS of ms

# 4.1. Irregular Graphs

In this section a time bound of O(polynomial $( n ) 2 ^ { c n } )$ is proved for the running time of ms with $c < 0 . 2 9 6$ This bound depends for the moment on an oracle which returns the value of ms on regular graphs of order 4 to 7 and on assumptions about the speed of the auxiliary function $m s ^ { 2 }$ Section 4.2 shows that the dependence on the oracle can be removed with only a multiplication of the time bound by a constant. Section 5 gives the function $m s ^ { 2 }$ and justifies the assumptions used here.

The central fact to be proved is that a call of ms on a graph of order $\pmb { n }$ produces at most $k 2 ^ { c n }$ "trivial" calls of ms, that is, calls which return a result with no recursion. Since a nontrivial call involves a polynomial bounded amount of work plus one or more calls on smaller graphs, this implies the stated time bound of O(polynomial $( n ) 2 ^ { c n } )$ . $k$ is chosen so that the result is true for all small graphs and the result is then proved by induction on $\pmb { n }$ . In the interests of brevity we use a somewhat loose terminology and refer to the number of trivial calls arising from a call of ms or $m s ^ { 2 }$ as the " time" taken by that call.

In order to complete the inductive step of the proof, we need to strengthen the bound claimed for certain classes of graphs. To be precise we prove the following theorem.

Theorem 1. For $c \geq 0 . 2 9 6$ there exists $\pmb { k }$ such that the time taken by ms on a graph $\pmb { G }$ is at most $t ( G , \left| G \right| )$ provided calls on regular connected graphs $\pmb { G }$ of degree 4 to 7 are replaced by calls on an oracle which uses time $t ( G , | G | )$ where

$t ( G , n ) = \mathbf { i f } ~ G$ has a vertex of degree 1 then $k 2 ^ { c ( n - 2 ) }$ else if $\pmb { G }$ has a vertex of degree 2 then $k 2 ^ { c ( n - 1 \frac { 1 } { 2 } ) }$ else if $\pmb { G }$ has a vertex of degree 3 then $c _ { 3 } k 2 ^ { c n }$ else if $\pmb { G }$ is not connected then $k 2 ^ { c ( n - 1 ) }$ else if $\pmb { G }$ has a vertex of degree 4 then $c _ { 4 } k 2 ^ { c n }$

else if $G$ has a vertex of degree 5 then $c _ { 5 } k 2 ^ { c n }$ else $k 2 ^ { c n }$ and $\begin{array} { l } { c _ { 3 } = 2 ^ { - 4 c } + 2 ^ { - 3 c } < 0 . 7 9 9 } \\ { c _ { 4 } = c _ { 3 } 2 ^ { - c } / ( 1 - 2 ^ { - 6 c } ) < 0 . 9 1 9 } \\ { c _ { 5 } = c _ { 4 } 2 ^ { - c } / ( 1 - 2 ^ { - 7 c } ) < 0 . 9 8 2 , } \end{array}$ on the assumption that the function $m s ^ { 2 }$ on graphs $G , s$ takes time $t ^ { 2 } ( G , | G | , S , | \dot { S | } )$ where $t ^ { 2 } ( G , n , S , m ) =$ if $m \geq 5$ then $t ( G , n )$ else if $m = 4$ then $k 2 ^ { c ( n - 1 ) }$ else if $m = 3$ or $m = 2$ then if $s$ has a vertex of degree 0 (in $G$ ) then $k 2 ^ { c ( n - 2 ) }$ else if $s$ has a vertex of degree 1 (in $G$ ) then $k 2 ^ { c ( n - 3 ) }$ else $k 2 ^ { c ( n - 4 ) }$ else 1.

Proof. The proof is by induction on $n , k$ is chosen $> 1$ and such that the result holds for all graphs of order $< 1 1$ .Next we assume the result proved for all ${ \pmb n } ^ { \prime } < { \pmb n }$ and prove it for $\pmb { n }$ .

The structure of the inductive step follows that of the function. We write t(n; condition) for the maximum of $t ( G , | G | )$ over graphs $\pmb { G }$ such that $| G | = n$ and condition holds; $t ( n )$ is an abbreviation for $t ( n , t r u e )$ , that is, $\pmb { k } 2 ^ { c n }$ Similarly we write $t ^ { 2 } ( n , m$ condition) for the maximum of $\scriptstyle t ^ { 2 } ( G , | G | , S , | S | )$ over graphs $\pmb { G }$ and $\pmb { S }$ such that $| G | = n , | S | = m$ and condition holds; $t ^ { 2 } ( n , m )$ is an abbreviation for $t ^ { 2 } ( n , m ; t r u e ) .$

i) If $G$ is not connected and $| C | = i ,$ time $\leq t ( i ) + t ( n - i )$ which is maximised by minimising $i$ but $i = 1$ and $i = 2$ are special cases, giving time $\leq m a x ( t ( n - 1 ) , t ( 3 ) + t ( n - 3 ) )$ $= t ( n - 1 )$ . Moreover if $\pmb { G }$ has a vertex of degree 1, 2, or 3, then either (i > this degree and C has the low degree vertex) or $( G - C$ has the low degree vertex). In each case this establishes the stronger bound; for instance, for degree 1, time $\leq m a x ( t ( n - 1 ; G$ has a vertex with degree 1), $t ( 3 ) + t ( n - 3 ; G$ has a vertex with degree 1), t(3; G has a vertex with degree 1) + t(n - 3)) $\leq m a x ( t ( n - 3 ) , t ( 1 ) + t ( n - 3 ) )$ $< t ( n - 2 )$ .   
ii) if $d ( A ) = 1$ , there is one recursive call $m s ( G - { \widehat { N } } ( A ) )$ giving time $\leq t ( n - 2 )$ as required.

iii) If $d ( A ) = 2$ , there are two recursive calls (except in the case edge $( B , B ^ { \prime } )$ which is trivial), $m s ( G - \overline { { N } } ( B ) - \overline { { N } } ( B ^ { \prime } ) )$ and $m s ^ { 2 } ( G - \widehat { N } ( A ) , \widehat { N } ^ { 2 } ( A ) ) ;$ let $x = \{ N ^ { 2 } ( A ) \} .$ .

(iia) If $x \leq 1$ , the $m s ^ { 2 }$ call is trivial giving time $\leq 1 + t ( n - 3 ) < t ( n - 2 ) ;$ .   
(iiib) if $x = 2$ , time $\leq t ( n - 5 ) + t ^ { 2 } ( n - 3 , 2 )$ $\leq 2 t ( n - 5 ) < k 2 ^ { c ( n - 1 { \frac { 1 } { 2 } } ) }$ .   
iiic If $x = 3$ , time $\leq t ( n - 6 ) + t ^ { 2 } ( n - 3 , 3 )$ ≤ t(n- 6)+t(n− 5)<k2c(n-1 \);   
(iiid) if $x = 4$ , time $\leq t ( n - 7 ) + t ^ { 2 } ( n - 3 , 4 )$ ≤ t(n − 7)+t(n − 4)<k2c(n-12);   
(ii) if $x \ge 5$ , time $\leq t ( n - 8 ) + t ( n - 3 ) < k 2 ^ { c ( n - 1 { \frac { 1 } { 2 } } ) }$ as required.

v) If $d ( A ) = 3$ , there are two recursive calls $m s ^ { 2 } ( G - A , N ( A ) )$ and $m s ( G - { \overline { { N } } } ( A ) )$ taking time

$$
\leq t ( n - 5 ) + t ( n - 4 ) = c _ { 3 } k 2 ^ { c n } .
$$

v If $\pmb { G }$ is not connected but has no vertices of degree $\leq 3$ $m s ( C )$ is called for each $c$ a connected component of $\pmb { G }$ Each component must have order at least 5 giving

$$
\begin{array} { r l } & { \check { \leq } t ( 5 ) + t ( n - 5 ) \mathrm { ~ w i t h ~ } n \geq 1 0 } \\ & { \leq k ( 3 + 2 ^ { c ( n - 1 ) } 2 ^ { - 4 c } ) } \\ & { \leq k ( 3 + 2 ^ { c ( n - 1 ) - 1 } ) } \\ & { < k 2 ^ { c ( n - 1 ) } \mathrm { ~ s i n c e ~ } 2 ^ { 9 c } > 6 . } \end{array}
$$

(vi) Otherwise, unless $\pmb { A }$ dominates $\pmb { B }$ there are two recursive calls $m s ( G - B )$ and $m s ( G - \overline { { N } } ( B ) )$ .

(via) If $d ( A ) \geq 7$ $d ( B ) \geq 8$ since $\pmb { G }$ cannot be regular with degree 7; hence

vic)if $d ( A ) = 4$ or 5, $d ( B ) \geq d ( A ) + 1$ , and if

$d ( B ) = d ( A ) + 1$ then there is another vertex $B ^ { \prime } \in N ( A )$ such that $d ( B ^ { \prime } ) = d ( A )$ or $d ( A ) + 1$ and $( B , B ^ { \prime } )$ is not an edge (from the choice of $\pmb { A }$ and $\pmb { B }$ and the fact that $\pmb { A }$ does not dominate $\pmb { B }$ ).

Hence either $| G - { \overline { { N } } } ( B ) | < n - d ( A ) - 2$ or $| G - { \overline { { N } } } ( B ) | = n - d ( A ) - 2$ and $G - { \overrightarrow { N } } ( B )$ has a vertex of degree $\leq d ( A : G )$ thus $t ( G , n ) \leq c _ { d ( A ) - 1 } k 2 ^ { c ( n - 1 ) }$ $+ \ m a x ( k 2 ^ { \overleftarrow { c } ( n - } d ( A ) - 3 ) , c _ { d ( A ) } k 2 ^ { c ( n - d ( A ) - 2 ) } )$ and the second term of the max is larger in each case since $c _ { 4 } , c _ { 5 } > 2 ^ { - c }$ .

Thus finally $t ( G , n ) \leq c _ { d ( A ) - 1 } k 2 ^ { c ( n - 1 ) } + k 2 ^ { c ( n - d ( A ) - 2 ) } c _ { d ( A ) }$ $= c _ { d ( A ) } k 2 ^ { c n }$ as required by the definitions of $c _ { 4 }$ and $c _ { 5 }$ .

# 4.2. Regular Graphs

We now justify the claim that reliance on the oracle for regular connected graphs of degree 4 to 7 only affects the constant $k$ in the time bound. If we drop the oracle for degree 4 graphs we have an algorithm which does work in time $\leq t ( n )$ for any graph which has no subgraph which is regular with degree 4; hence it works in time $\leq t ( n )$ for any graph which is a proper subgraph of a connected regular degree 4 graph. Now looking at the time taken by ms on a regular degree 4 connected graph, we see that the two recursive calls $m s ( G - B )$ and $m s ( G - \overline { { N } } ( B ) )$ take time $\leq t ( n - 1 ) + t ( n$ $- \ S ) \leq k ^ { \prime } 2 ^ { c n }$ for $k ^ { \prime } \approx 1 . 1 7 k$ . Thus by the same inductive argument as before, we prove that the new algorithm, using the oracle only for degree 5 to 7, runs in time $\leq k ^ { \prime } 2 ^ { c n }$ for all graphs.

Repeating the same argument three more times gives eventually an algorithm which uses no oracle at all and runs in time $\leq k ^ { \prime \prime } 2 ^ { c n }$ for $k ^ { \prime \prime } \approx 1 . 3 8 k$ on all graphs.

# 5. The AuXiliaRY FUnction ms2

Next we present the auxiliary function $m s ^ { 2 } ( G , S )$ and justify the assumptions about its running time used in Section 4.1. The discussion of timing is simple and will be included as comment in the program text. After a few trivial but tedious special cases have been disposed of, the logic is very straightforward: if $\pmb { \mathscr { s } }$ is an element of $\pmb { S } _ { : }$ , a m.i.s. must either contain $\pmb { \mathscr { s } }$ and one other element of $s$ or contain not $\pmb { \mathscr { s } }$ but two other elements of $s$ . Another function $m s ^ { 1 }$ is sometimes used to handle the first of these; in the second we use the same idea as in ms and consider only independent sets containing two or more neighbours of $\pmb { S }$ .

function $m s ^ { 2 } ( G )$ graph; $s$ vertexset): integer; {first comes the declaration of $m s ^ { 1 }$ which is defined similarly to $m s ^ { 2 }$ but concerns sets $\pmb { S }$ of which one element is to be in the independent set}   
function $m s ^ { 1 } ( G ;$ graph; S: vertexset): integer; {This is only called with $\pmb { S }$ a two element subset of the vertices of $G$ It returns the size of an independent set of $\pmb { G }$ at least as large as the largest such set which contains an element of $\pmb { S }$ . The elements of $\pmb { S }$ are $s _ { 1 }$ and $\pmb { s } _ { 2 }$ with $d ( s _ { 1 } ) \leq d ( s _ { 2 } )$ .

The time to compute $m s ^ { 1 } ( G , S )$ $\leq t ( n - 1 )$ if $( s _ { 1 } , s _ { 2 } )$ is an edge of $\pmb { G }$ or $d ( s _ { 1 } ) \leq 1$ $\leq t ( n - 2 )$ otherwise.

$t ^ { 1 }$ is defined analogously to $t ^ { 2 }$ }   
begin   
if $d ( s _ { 1 } ) \leq 1$ then return $m s ( G )$ ; $\{ { \mathrm { t i m e } } \leq t ( n - 1 ) \}$   
if edge $( s _ { 1 } , s _ { 2 } )$ then if $d ( s _ { 1 } ) \leq 3$ then return ms(G) $\{ { \mathrm { t i m e } } \leq t ( n - 1 ) \}$ else return max( $m s ( G - \overline { { N } } ( s _ { 1 } ) )$ , ms(G − N(s2))) + 1; $\{ \mathrm { t i m e } \le 2 t ( n - 5 ) < t ( n - 1 ) \}$   
if $N ( s _ { 1 } ) \cap N ( s _ { 2 } ) \langle \rangle \phi$ then return $m s ^ { 1 } ( G - N ( s _ { 1 } ) \cap N ( s _ { 2 } ) , S ) ;$ {time $\leq t ^ { 1 } ( n - 1 ) \leq t ( n - 2 ) \}$   
if $d ( s _ { 2 } ) = 2$ then begin $\pmb { { \cal E } }$ , ${ \pmb F } : =$ the elements of $N ( s _ { 1 } )$ ; {independent sets to be considered contain $s _ { 1 }$ or $( s _ { 2 } , E$ and F)} if edge $( E , F )$ then return $1 + m s ( G - \widetilde { N } ( s _ { 1 } ) )$ : {time $\leq t ( n - 3 ) \}$ if $N ( E ) + N ( F ) - s _ { 1 } \subset N ( s _ { 2 } )$ then return $3 + m s ( G - \overline { { N } } ( s _ { 1 } ) - \overline { { N } } ( s _ { 2 } ) )$ $\{ \overline { { N } } ( s _ { 1 } ) + \overline { { N } } ( s _ { 2 } )$ has no 4 element independent set containing $\pmb { s _ { 1 } }$ or $\pmb { s } _ { 2 }$ and $\{ E , F , s _ { 2 } \}$ dominates every other 3 element independent set $\begin{array} { r l } & { \mathrm { t r m e } \leq \iota ( n - 0 ) \} } \\ & { \mathrm { ~ r e t u r n } \quad m a x ( 1 + m s ( G - \widetilde { N } ( s _ { 1 } ) ) , 3 + m s ( G - \overline { { N } } ( E ) - \overline { { N } } ( F ) - } \\ & { \overline { { N } } ( s _ { 2 } ) ) ) } \\ & { \{ \mathrm { t i m e } \leq \iota ( n - 3 ; G \mathrm { ~ h a s ~ a ~ v e r t e x ~ o f ~ d e g r e e } 2 ) + \iota ( n - 7 ) } \\ & { \qquad \leq \iota ( n - 4 \frac { 1 } { 2 } ) + \iota ( n - 7 ) } \\ & { \qquad < \iota ( n - 2 ) \} } \end{array}$ time $\leq t ( n - 6 ) \}$ end;   
return $m a x ( m s ( G - \overrightarrow { N } ( s _ { 2 } ) ) , m s ^ { 2 } ( G - \overrightarrow { N } ( s _ { 1 } ) - s _ { 2 } , N ( s _ { 2 } ) ) ) + 1$ {independent set contains $\pmb { s _ { 2 } }$ or $( s _ { 1 }$ and two elements of $N ( s _ { 2 } ) )$ if $d ( s _ { 1 } ; G ) = 2$ then also $d ( \widetilde { s } _ { 1 } ; G \widetilde { - } \widetilde { N } ( s _ { 2 } ) ) = 2$ , giving if $d ( s _ { 2 } ) = 3$ time $\leq t ( n - 5 \frac { 1 } { 2 } ) + t ^ { 2 } ( n - 4 , 3 ) < t ( n - 2 )$ if $d ( s _ { 2 } ) = 4$ time $\leq t ( n - 6 \frac { 1 } { 2 } ) + t ^ { 2 } ( n - 4 , 4 ) < t ( n - 2 )$ if $d ( s _ { 2 } ) \geq 5$ time ≤ $( n - 7 _ { 2 } ^ { 1 } ) + t ( n - 4 ) < t ( n - 2 )$ if $d ( s _ { 1 } ; G ) = \ o ^ { , } { 3 }$ then also $d ( s _ { 1 } ; G - \bar { N } ( s _ { 2 } ) ) = 3$ , giving if $d ( s _ { 2 } ) = 3$ time $\leq t ( n - 5 ) + t ^ { 2 } ( n - 5 , 3 ) < t ( n - 2 )$ if $d ( s _ { 2 } ) > 3$ time $\leq t ( n - 6 ) + t ( n - 5 ) < t ( n - 2 )$ if $d ( s _ { 1 } ) \geq 4$ then time $\leq t ( n - 5 ) + t ( n - 6 ) < t ( n - 2 ) \}$   
end $\{ \mathsf { o f } \ m s ^ { 1 } \}$ ;   
bbegin $\{ m s ^ { 2 }$ The elements of $\pmb { S }$ are $s _ { 1 } , s _ { 2 } , \ldots$ with $d ( s _ { i } ) \leq d ( s _ { i + 1 } ) \}$   
if $\vert s \vert \le 1$ then return 0;   
if $| S | = 2$ then if edge $( s _ { 1 } , s _ { 2 } )$ then return 0 else return $2 + m s ( G - \widetilde { N } ( s _ { 1 } ) - \overline { { N } } ( s _ { 2 } ) )$

$\{ { \mathrm { t i m e } } \leq t ( n - 2 - d ( s _ { 1 } ) ) \}$ $| { \pmb S } | = 3$ then {This is the only complicated case and is the crucial one arising from ms with $d ( A ) = 3 .$ begin if $d ( s _ { 1 } ) = 0$ then return $1 + m s ^ { 1 } ( G - s _ { 1 } , S - s _ { 1 } ) ;$ $\{ \mathrm { t i m e } \leq t ^ { 1 } ( n - 1 ) \leq t ( n - 2 ) \}$ if $e d g e ( s _ { 1 } , s _ { 2 } )$ and $e d g e ( s _ { 2 } , s _ { 3 } )$ and $e d g e ( s _ { 3 } , s _ { 1 } )$ then return 0; if $e d g e ( s _ { i } , s _ { j } )$ and edge $( s _ { i } , s _ { k } ) ( j \langle \rangle k )$ then return $2 ^ { ' } + m s ( G - \widetilde { N } ( s _ { j } ) - \overline { { N } } ( s _ { k } ) )$ {time $\leq t ( n - 2 - d ( s _ { j } ) ) \}$ if $e d g e ( s _ { i } , s _ { j } )$ then return $1 { } ^ { \prime \prime \prime } + m s ^ { 1 } ( G - \overline { { N } } ( s _ { k } ) , [ s _ { i } , s _ { j } ] ) ( i \langle \rangle k \langle \rangle j ) ;$ {independent set cannot contain $s _ { i }$ and $s _ { j }$ and so contains one of them and $s _ { k }$ . time $\leq t ^ { 1 } ( n - 1 - d ( s _ { k } ) ) \leq t ( n - 2 - d ( s _ { k } ) ) \}$ if vertex $v \in N ( s _ { i } ) \cap N ( s _ { j } ) ( i \langle \rangle j )$ then return $m s ^ { 2 } ( G - v , S ) ;$ . {independent set contains $s _ { i }$ or $s _ { j }$ and so not $v$ . time $\leq t ^ { 2 } ( n - 1 , | S | ;$ degrees reduced by at most 1)} if $d ( s _ { 1 } ) = 1$ then return $1 \dot { + } m s ^ { 1 } ( G - \overline { { N } } ( s _ { 1 } ) , S - s _ { 1 } )$ time $\leq t ^ { 1 } ( n - 2 ) \leq t ( n - 3 ) \}$ return $m a x ( 1 + m s ^ { 1 } ( G - \overline { { { N } } } ( s _ { 1 } ) , S - s _ { 1 } ) , m s ^ { 2 } ( G - \overline { { { N } } } ( s _ { 2 } ) - \overline { { { N } } } ( s _ { 3 } ) -$ $s _ { 1 } , N ( s _ { 1 } ) ) \}$ $\begin{array} { r l } & { \overset { , } { ! } , \overset { , } { \operatorname { a r } } ( s _ { 1 } ) \overset { , } { \operatorname { a r } } \overset { } { \operatorname { a r } } \overset { } { \operatorname { a r } } = 2 \mathrm { ~ t i m e } \leq t ( n - 5 ) + t ^ { 2 } ( n - 7 , 2 ) < t ( n - 5 ) + t ( n - 9 ) } \\ & { \overset { , } { \operatorname { c } } t ( n - 3 ) } \\ & { \overset { } { \operatorname { f } } } & { d ( s _ { 1 } ) = 3 \mathrm { ~ t i m e } \leq t ( n - 6 ) + t ^ { 2 } ( n - 9 , 3 ) \leq t ( n - 6 ) + t ( n - 1 1 ) } \\ & { < t ( n - 4 ) } \\ & { \overset { } { \operatorname { f } } } & { d ( s _ { 1 } ) \geq 4 \mathrm { ~ t i m e } \leq t ( n - 7 ) + t ( n - 1 1 ) < t ( n - 4 ) } \end{array}$ since, in all three cases, the call of $m s ^ { 1 }$ has its second parameter S a set of two vertices of degree $\geq 2$ with no edge between them} end $\{ | S | = 3 \}$ ; $| S | = 4$ then if $G$ has a vertex of degree $\leq 3$ then return $m s ( G )$ . $\{ { \mathrm { t i m e } } \leq t ( n - 1 ) \}$ else return max $( 1 + m s ( G - \overline { { { N } } } ( s _ { 1 } ) ) , m s ^ { 2 } ( G - s _ { 1 } , \dot { S } - s _ { 1 } ) )$ $\{ { \mathrm { t i m e } } \leq t ( n - 5 ) + t ^ { 2 } ( n - 1 , 3$ members of $s$ have degree $\geq 3$ $\leq 2 t ( n - 5 )$ . $< t ( n - 1 ) \}$ . turn $m s ( G ) \{ | S | \geq 5 \colon { \mathrm { t i m e } } \leq t ( n ) \}$ nd;

{In each case the time has been shown to be bounded as assumed in Theorem 1. Strictly the proof of Theorem 1 and the bounds on $m s ^ { 1 }$ and $m s ^ { 2 }$ are a triple simultaneous induction.}

# 6. A Time-SPace Trade-ofF

# 6.1. Accelerating Exponential Recursive Algorithms

It is a commonplace observation that functions on integer arguments may be most simply expressed recursively but be grossly inefficient in their recursive form because of a tendency to repeat some subcomputations very many times. This tendency can be removed, either by a dynamic programming approach or by what we call the "memory" method, that is, by retaining the recursive structure while storing all values of the function which have already been computed and never reevaluating such a stored value. The same technique can be used with functions on combinatorial arguments such as graphs and enables us to reduce the constant $c$ in our time bound for ms to about 0.276.

In the case of integer arguments an array is probably suitable for storing the already computed values. For combinatorial arguments, if the algorithm is to run on a random access machine, it will generally be effective to store (argument, value) pairs in a balanced tree structure using the argument as key; this depends on having an easily computable ordering of the argument type. In the case of graphs, it is probable that no easily computable ordering exists, so we regard the arguments as subsets of the vertices $V$ of the original graph and order them by the natural ordering of $2 ^ { V }$ .

If the algorithm is required to run on a Turing Machine, a slightly more complex approach achieves the same result. This will be discussed in Section 6.4.

First we use a simple argument to show that ms modified in this way runs in time $O ( 2 ^ { c n } )$ for $c \approx 0 . 2 8 2$ .Section 6.2 uses a rather more complex argument on a slightly different ms to reduce the bound still further.

The time taken by the modified ms on a graph of order $\pmb { n }$ is divided into two parts, that on small graphs (graphs of order $\leq \alpha n$ where $\pmb { \alpha }$ is a constant to be decided later) and that on large graphs (we have now dropped the definition of time as the number of trivial calls arising).

The time taken on small graphs is bounded by the observation that the number of such graphs is $\begin{array} { r } { \sum _ { i = 0 } ^ { \bullet } { \binom { n } { i } } } \end{array}$ giving $( n ) { \binom { n } { \alpha n } }$ .

The extra time taken on any large graph (order $n ^ { \prime } > \alpha n \dot { }$ ) is seen to be bounded by $k 2 ^ { c ( n ^ { \prime } - \alpha n ) }$ by the same inductive argument used in Section 4.

Hence

$$
{ \mathrm { t o t a l ~ t i m e } } \leq { \mathrm { p o l y n o m i a l } } ( n ) \left( 2 ^ { c ( 1 - \alpha ) n } + { \frac { 1 } { \left( \alpha ^ { \alpha } ( 1 - \alpha ) ^ { ( 1 - \alpha ) } \right) ^ { n } } } \right)
$$

and choosing $\pmb { \alpha } \approx 0 . 0 4 8$ to balance the two terms gives the bound of $O ( 2 ^ { 0 . 2 8 2 n } )$ b

# 6.2. Connected Subgraphs

The argument of Section 6.1 can be slightly strengthened by the observation that the time spent on small graphs is determined essentially by the number of connected small graphs. Any small graph simply causes at most $\alpha n / 3$ evaluations of ms on connected small graphs. For the moment we limit the discussion to graphs of degree $\leq 8$ and show, for small ${ \pmb { \alpha } } .$ ,an upper bound on the number of connected subgraphs which is much less than $\left( { \underset { \alpha n } { n } } \right)$

LEMMA. If $G = ( V , E )$ is $\pmb { a }$ graph of order n and degree $\leq 8$ , the number of connected induced subgraphs of $\pmb { G }$ order ${ n ^ { \prime } = O \ell }$ polynomial $( n ) ( 7 ^ { 7 } 6 ^ { - 6 } ) ^ { n ^ { \prime } } )$ .

Proof. We show a simple 1-many mapping from connected induced subgraphs of order $\pmb { n } ^ { \prime }$ (other than connected components of $G$ ) to triples $( v , e , t )$ where $v \in V , e \in E$ and $t$ is a 7-ary tree of order $n ^ { \prime }$ The conclusion follows by the enumeration of the 7-ary trees of order $\pmb { n } ^ { \prime }$ [4] and Stirling's approximation.

Choose an arbitrary ordering of the edges $\pmb { { \cal E } }$ and let $C$ be a connected induced subgraph of $\pmb { G }$ (not a component). Let $v$ be a vertex of $c$ such that $d ( v : C ) \leq 7 ;$ if $d ( v : G ) = 8 _ { \mathrm { { ; } } }$ ,choose $e$ an edge in $\pmb { \cal E }$ which is incident on $v$ and is not an edge of $c$ otherwise choose $\pmb { e }$ arbitrarily in $\pmb { { \cal E } }$ Choose $_ T$ a spanning tree of $c$ with root $v$

$\pmb { T }$ has out degree $\leq 7$ at each vertex and, given the ordering of $E$ gives the 7-ary tree $t$ in an obvious way; the seven subtrees at a node are ordered according to the ordering of the edges and an edge which is not in $\pmb { T }$ gives an empty subtree in $t$

It is clear that, given $v , \ e ,$ and $t .$ , it is possible to reconstruct $T$ and thereby $C _ { i }$ , establishing that the mapping is indeed 1-many and completing the proof of the lemma.

TheORe 2. If ms is modifed in the folloing two ways its running tie is $O ( 2 ^ { 0 . 2 7 6 n } )$ :

(i) use of memory to avoid repeated computation on the same subgraph; ii) whenever $\pmb { G }$ has a vertex $V$ of degree $> 8 ,$ , returning max $\textstyle ( m s ( G -$ $V ) , \dot { 1 } + m s ( G - \overline { { { N } } } ( V ) )$ .

Proof. We prove the result first for graphs of degree $\leq 8 .$ By the lemma the time spent on graphs of order $\leq \alpha n$ is polynomial $( n ) ( 7 ^ { 7 } 6 ^ { - 6 } ) ^ { \alpha n }$ By the usual inductive argument, the extra time spent on large graphs resulting from a graph of order $\pmb { n } ^ { \prime }$ is $O ( 2 ^ { c ( n ^ { \prime } - \alpha n ) } )$ Choosing ${ \pmb { \alpha } } = { \bf 0 . 0 6 6 7 }$ gives a total time of $O ( 2 ^ { 0 . 2 7 6 n } )$ .

The general result is proved inductively where the induction is based on the degree $\leq 8$ case. $\pmb { G }$ either has degree $\leq 8$ or is dealt with by modification (ii) in time $\leq 2 ^ { 0 . 2 7 6 ( n - 1 ) } + \bar { 2 } ^ { 0 . 2 7 6 ( n - 1 0 ) } < 2 ^ { 0 . 2 7 6 n }$ since $2 ^ { - 0 . 2 7 6 }$ $+ \ 2 ^ { - 2 . 7 6 } < 1$ .

# 6.3. An Application to Some Logical Problems

The same approach of using memory to avoid recomputation can also achieve a substantial speedup in solving QBF (Quantified Boolean Formula) problems over a fairly wide set of expressions including as a small subset formulae in CNF with a number of clauses equal to the number of variables. The special case where all the quantifiers are existential gives the same result for SAT over the same set of expressions. The expressions in question are most easily characterised in terms of boolean circuits rather than syntactically. They can be computed from $_ { 2 n }$ inputs $a _ { 1 } , \ldots , a _ { n } ,$ $\neg a _ { 1 } , \dotsc , \dotsc a _ { n }$ by circuits of a number (linear in $\pmb { n }$ and less than about $1 . 2 9 n )$ of and and or gates of unbounded fan-in and fan-out subject to the restriction, for each $_ i$ independently, that either no input $a _ { i }$ or $\neg a _ { i }$ goes directly into any and gate or no input ${ \pmb a } _ { i }$ or $\neg a _ { i }$ goes directly into any or gate. For simplicity we consider only the case where the number of gates is the same as $\pmb { n }$ the number of variables.

A simple approach to solving such a problem would recursively solve the two subproblems obtained by setting ${ \pmb { a } } _ { \sf o u t e r }$ (the variable of the outermost quantification) to true and to false and combine the two results appropriately. A slightly more sophisticated algorithm would first simplify the circuit after each assignment by removing gates whose output was "obvious" (a gate's output is "obvious" if it is directly implied by those inputs which are either the obvious outputs of other gates or already assigned literals) and second notice cases where the function computed by the current circuit was obviously monotonic in $a _ { \mathrm { o u t e r } }$ (because either $\pmb { a } _ { \mathsf { o u t e r } }$ or $\neg a _ { \mathrm { o u t e r } }$ was not connected to any gate) and solve only one subproblem in these cases; for instance if the circuit is monotonic increasing in $a _ { \mathrm { o u t e r } }$ , this variable will be set to true if existentially quantified or to false if universally quantified. This algorithm will still take time $O ( 2 ^ { n } )$ but its "memorising" version will run in time $O ( 2 ^ { 0 . 7 7 3 n } )$ . The reason is simply that whenever two assignments to a variable are possible, each of them reduces the number of gates by at least one and that a nontrivial subproblem can be specified by the number of assignments made and which gates remain.

Now after $\pmb { n } ^ { \prime }$ variables have been assigned a value which was not dictated by the "monotonic" rule, the number of possible subproblems is bounded in two ways; first it is at most $2 ^ { n ^ { \prime } }$ since $\pmb { n } ^ { \prime }$ choices have been made; second it is at most $( n - n ^ { \prime } + 1 ) \Sigma _ { i = 0 } ^ { n - n ^ { \prime } } { \binom { n } { i } }$ is in the range $[ n , n ^ { \prime } ]$ and at most $( n - n ^ { \prime } )$ gates remain.

Thus choosing ${ \pmb n } ^ { \prime } \approx 0 . 7 7 3 n$ so that $2 ^ { n ^ { \prime } } \approx \left( \begin{array} { c } { { n } } \\ { { n ^ { \prime } } } \end{array} \right)$ ensures that the time spent on problems with at most $\pmb { n } ^ { \prime }$ such assignments and the time spent on those with more than $\pmb { n } ^ { \prime }$ are both $O ( { \mathrm { p o l y n o m i a l } } ( n ) 2 ^ { 0 . 7 7 3 n } )$ .

If we remove the restriction on the gates into which inputs may go, we still obtain a slight improvement over time $O ( 2 ^ { n } )$ by a slightly more complex argument. It can be shown that the time in this case is

$$
O \left( \left( \begin{array} { c } { { n } } \\ { { n } } \\ { { \overline { { { 3 } } } } } \end{array} \right) \right) \approx 2 ^ { 0 . 9 1 2 n } .
$$

# 6.4. Achieving the Time-Space Trade-off with a Turing Machine

Since the "memorising" algorithms have space complexity almost as great as their time complexity, simulating them by a Turing Machine might almost square their time bound producing an algorithm much slower than the polynomial space version. This can be avoided by a more careful Turing Machine version of the algorithm which can still obtain exactly the same reduction in the exponent of the time bound.

The significant fact is that the later part of the sequence of recursive calls produced from a given call does not depend on the results of earlier calls. This means that, instead of making the recursive calls in sequence, we could make them in parallel or interleave them. Now a large number of references to the memory can be batched together and such a batch of references can, by sorting them, be made much more efficiently than if they had to be done sequentially.

In order to make it clear that the method being described applies to both the ms function and to QBF, we give some fairly general conditions for it to be applicable instead of describing it in terms of a particular function.

THeOReM 3. If f is a function with domain $\pmb { D }$ and range $\pmb R$ such that

(i) 3 functions $f _ { 1 } , f _ { 2 } , f _ { 3 }$ such that (ia) $f _ { 1 } ( d ) = ( d _ { 1 } , d _ { 2 } , \dots , d _ { f _ { 2 } ( d ) } )$ , (an element of $D ^ { * }$ (ib) $f ( d ) = f _ { 3 } ( d , f ( d _ { 1 } ) , \dots , f ( d _ { f _ { 2 } ( d ) } ) )$ (the recursive definition off (ic) $f _ { 1 } , f _ { 2 }$ and $f _ { 3 }$ are in Ptime,   
ii) if $T ( d )$ is the computation tree formed by adding to d instances of the trees $T ( d _ { i } )$ of the elements of $\dot { f } _ { 1 } ( d )$ then (iia) the depth of $\pmb { T } ( \pmb { d } )$ is bounded by a polynomial in |d| (iib) any element t of $T ( d )$ has $| t |$ bounded by a polynomial in $| d | ,$   
(ii) 3 a total ordering $\leq$ on $\pmb { D }$ computable in Ptime, then $f ( d )$ is computable by $^ { a }$ multitape Turing Machine in time bounded by polynomial $\langle | d \boldsymbol { \mathfrak { p } } \times $ (# distinct elements of $_ D$ in $T ( d ) )$ .

Proof. Before proceeding to describe the Turing Machine computation, we note that conditions (ic) and (ib) ensure that the degree of elements of $T ( d )$ is bounded by polynomial( $| d |$ and so (iia) ensures that log(# elements in $T ( d ) ) = O ( { \tt p o l y n o m i a l } ( \vert d \vert ) )$ so that elements of $T ( d )$ can be sorted in $O ( { \mathfrak { p o l y n o m i a l } } ( | d | ) )$ passes.

The Turing Machine computation proceeds in two phases. The first phase constructs top-down the representation of the directed acyclic graph $G ( d )$ formed from $T ( d )$ by identifying nodes with the same element of $\pmb { D }$ and directing edges upwards; duplicated representations of nodes of $\pmb { G }$ are avoided by regular sorting which brings duplicates together so that they can be dealt with. The second phase evaluates $f$ at leaves and then propagates results back up through the graph evaluating $f$ at each node when the results of its recursive calls are available; again sorting is used, this time to move results from where they are computed to where they are needed.

The representation of the graph $G ( d )$ is as follows: if $( A \to B )$ is an edge of the graph, there are two records of it, $( A , \cdot \to \ ' , B )$ and $( B , \ l ^ { * }  \ l ^ { * } , A )$ ; the whole graph is represented by the records of its edges sorted lexicographically (so that for each vertex $\pmb { A }$ there is a contiguous sequence of records corresponding to all the edges into and out of $\pmb { A }$ ).

This representation of $G ( d )$ is easily computed in an order corresponding to a breadth first scan of the tree. Initially the records $( d _ { i } , \cdot \to \ ' , d )$ are placed on tape 1 (for $d _ { i }$ the elements of $f _ { 1 } ( d ) )$ and are " unmarked"; then in successive stages tape 1 is scanned for all unmarked records of the form $( X , \cdot \to \ ' , \ Y )$ , these records are "marked" and records $( X _ { i } , \cdot \to \ ^ { \circ } , \ X )$ and $( X , \ \cdot  \ , \ X _ { i } )$ are added to tape 2 for $X _ { i }$ the elements of $f _ { 1 } ( X )$ with the $^ { \bullet }  ^ { \bullet }$ records unmarked; then the records on tape 2 are sorted and merged into tape 1; finally, if tape 1 contains repeated sequences of records $( V ,$ $\mathbf { \Phi } \cdot \mathbf { \Phi } \to \mathbf { \Phi } , W )$ for the same $V ,$ , then if one is already marked the rest are now marked and if all are unmarked all but one are now marked. The number of these stages required is bounded by the depth of $T ( d )$ so that the total time for this first phase is bounded by polynomial $( | d | ) \times | G ( d ) |$ as required.

The second phase now gradually overwrites all the records of the form $( A , \cdot  \cdot , A _ { i } )$ meaning that $f ( A )$ depends on $f ( A _ { i } )$ with records $( A ,  )$ $A _ { i } , f ( A _ { i } ) )$ ; when this has happened for all $A _ { i } , f ( A )$ can be computed and passed up to all those $\pmb { B }$ such that a $( A , \mathrel { \mathop  } \mathrm { ~ , ~ } B )$ record exists. Eventually we are left only with the records $( d , \cdot  , d _ { i } , f ( d _ { i } ) )$ needed to compute the value $f ( d )$ .

In more detail, this phase also consists of a number of stages. At each stage, for every vertex $\pmb { A }$ such that each $( A , \ \cdot  \ , \ A _ { i } )$ record has been replaced by $( A , \cdot  \cdot , A _ { i } , f ( A _ { i } ) ) , f ( A )$ is computed and then for every $( A ,$ $\cdot \stackrel { , } {  } \stackrel { , } { , } B )$ record, a new record $( B , \cdot  \cdot , A , f ( A ) )$ is written on tape 2 (and all records of the form $( A , \ldots )$ are cleared from tape 1); then tape 2 is sorted and finally merged into tape 1 with records of the form $( \bar { X , } ^ { \cdot  } \dot { : }$

$Y , f ( Y ) )$ with $X \neq d$ replacing the original record $( X , \lor  \lor Y )$ Again this process terminates after a number of stages bounded by the depth of $T ( d )$ and the whole computation is now completed in a total time of polynomial $( | d | ) \times | G ( d ) | .$

# 7. CONcLuSIOnS

The bound of $O ( 2 ^ { n / 3 } )$ in [5] on the time to find a maximum independent set has been reduced to $O ( 2 ^ { 0 . 2 7 6 n } )$ by three main methods. First, a deeper study of the neighbourhood of a chosen vertex in the graph has been made but without a more complex case structure in the program; this was made possible by the auxiliary functions $m s ^ { 2 }$ and $m s ^ { 1 }$ which by being mutually recursive hide some indefinitely complex case analysis. Second, the argument that low degree regular graphs can be discounted removed a lot of awkward cases. Third, if one is willing to use exponential space, an essentially trivial way of utilising the store achieves a nontrivial reduction in the exponent. Although the reduction of about 0.05 in the exponent by these three methods may sound modest, it looks better if thought of as a reduction of $9 9 . 9 \%$ in the time to compute ms for a 200 vertex graph.

Quite apart from the large probability that another algorithm can improve on this bound, it is quite possible that the algorithm given here can be proved to obey a lower bound. First, a more careful analysis of the possible graph structure around the edge $( A , B )$ may show more about the possible sequences of recursive calls, thereby giving a better bound for the polynomial space version, and second, a more accurate enumeration of the small subgraphs which can arise may reveal more about the effectiveness of the " memory" modification.

# ACKNOWLEDGMENTS

Much of the work reported here was done while I was at the University of Warwick. I am grateful to Professor Mike Paterson for his many helpful comments and to the SERC for funding my stay at Warwick.

# Список литературы

1. C. BRON AND J. KErBosCH, Algorithm 457: Finding all cliques of an undirected graph, Comm. ACM 16 (1973), 575577.   
2. J. C. JohnsTon, Cliques of a graph: Variations on the Bron-Kerbosch algorithm, Internat. J. Comput. Inform. Sci., 5 (1976), 209238.   
3. R. KARp, Reducibility among combinatorial problems, in "Complexity of Computer computations" (R. E. Miller and J. W. Thatcher, Eds.), Plenum, New York, 1972.   
4.D. E. KnUTH, "Fundamental Algorithms," p. 584, Addison-Wesley, Reading, Mass., 1968.   
5. R. E. TARJAN AND A. E. TROJANOwsKI, Finding a maximum independent set, SIAM J. Comput. 6 (1977), 537546.