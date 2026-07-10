# A Cutting Plane Based Algorithm for the Ferreira A. Martin R. Weism

C.E. Ferreira\* A. Martin R. Weismantel

Konrad-Zuse-Zentrum für Informationstechnik Berlin, Germany

# layout of

nce. This includes a discussion and evaluation of separation algorithms, an LP-based primal heuristic and some implementation details. The paper is based on the polyhedral theory for the multiple knapsack polytope developed in our companion paper [FMW93] and meant to turn this theory into an algorithmic tool for the solution of practical problems. an LP-based primal heuristic and some implementation details. The paper is based on the polyhedral theory for the multiple knapsack polytope developed in our companion paper [FMW93] and meant to turn this theory Introduction

# is associated a weight fi >

set of items $N$ the set of knapsac $M$ that yields minimum cost. Thi $i \in N$ lem is called the weighted m $f _ { i } > 0$ knapsack problem. $k \in M$ has a capacity $F _ { k } > 0$ Moreover, an objective function $c _ { i k } \in \mathbb { R }$ $i \in N , k \in M$ is given, which reflects the cost if item $i$ is assigned to knapsack $k$ . The task is to assign a subset of the kna sack roblem and the eneralized assi nment roblem. The sin le 0 1 kna - sack roblem is the s ecial case of the multi le

Closely related to the (weighted) multiple knapsack problem are the single $0 / 1$ knapsack problem and the generalized assignment problem. The single $0 / 1$ knapsack problem is the special case of the multiple knapsack problem where $| M | = 1$ problem is a gen $\mathcal { N P }$ zation of the multiple knapsack problem where every item i may have a particular weight fik for each knapsack k. The corresponding polyhedron was investigated in [GR90]. (see, for instance, [B75], [HJP75], [P75], [W75]). The generalized assignment problem is a generalization of the multiple knapsack problem where every item $i$ may have a particular weight $f _ { i k }$ for each knapsack $k$ . The corresponding polyhedron was investigated in [GR90].

Our motivation for studying the multiple knapsack problem came from two applications, namely, the design of processors for main frame computers and the layout of electronic circuits. We will briefly describe both applications now.

chip modules or other devices. Each of these devices is dened by several technical properties that we do not intend to describe here. Two properties of devices are important for us. Every device k has a capacity Fk, representing its \area" or the weight it can hold and a cut capacity Sk, describing the number of wires that can be connected to this device. The electronic components have certain contact points, called pins, from which wires can extend to pins of other components. In the logical design phase it is dete $k$ mined which pin $F _ { k }$ f which components have to be connected by a wire to ensure certain $S _ { k }$ nctional properties. It is customary to call a collection of pins that have to be connected a net. points, called pins, from which wires can extend to pins of other components. In The task is to assign the electronic components to the devices in such a way that a certain objective function is minimized and a number of technical side constraints is satised. Among them are two essential requ

The task is to assign the electronic components to the devices in such a way  For each device k the sum of the areas of the electronic components that are assigned to this device must not exceed the capacity Fk.

capacity Sk. $k$ the sum of the areas of the electronic components that are assigned to this device must not exceed the capacity $F _ { k }$ e mathematical problem that arises by thoroughly $k$ odelling all (or at least ost impo $S _ { k }$ n

combinatorial relaxations of the complete model. A rst relaxation of the general the most important) aspects of this question is a rather complicated integer program. The full model appears to be hopelessly difficult  at least for the present state of integer programming technology. Thus, we investigated a hierarchy of combinatorial relaxations of the complete model. A first relaxation of the general determined heuristically. For more details we refer the reader to [FGKKMW93]. and concentrate on the packing aspect of the problem. In knapsack terminology, The second application we have in mind arises in the la out of electronic circuits. H r n m r r l m h - ll l m n r l m i i n of lo ical units cells to locations on a iven rectan le silicon sub ect to certain particular weight representing its area. Due to the inherent complexity of the placement problem and its large scale, it is further decomposed in practice. In a rst step, the given rectangle is subdivided and it is determined which cells are assigned to which of the subareas such that the total weight of the cells that are assigned to the same subarea does not exceed the corresponding area capacity. This process of iteratively subdividing areas and assigning cells to subareas is continued until every subarea contains at most one cell. If we interpret cells as items and subareas as knapsacks, we can associate with every problem arising in this decomposition scheme a multiple knapsack problem. In fact, the multiple knapsack problem does not reect the whole situation, since { besides the area requirements { there are many additional side constraints which are to be taken into account and a complicated objective function must be minimized which strongly depends on the underlying fabrication technology. Nevertheless, solving the corresponding multiple knapsack problems seems to be a reasonable starting point to attack the much more complicated placement problems. into account and a complicated objective function must be minimized which strongly depends on the underlying fabrication technology. Nevertheless, solving the corresponding multiple knapsack problems seems to be a reasonable starting point to attack the much more complicated placement problems.

xik = 1, if item i is assigned to knapsack k, and xik = 0, otherwise. The multiple knapsack po $( N , M , f , F )$ N -M; f; F) is dened as the convex hull of all feasible $N$ lutions to the m $M$ iple knapsack problem. It is ea $f = ( f _ { i } ) _ { i \in N }$ at the following relatio $F = ( F _ { k } ) _ { k \in M }$ . We introduce variables $x _ { i k } \in \mathbb { R } ^ { N \times M }$ with the interpretation $x _ { i k } = 1$ , if item $i$ is assigned to knapsack $k$ , and $x _ { i k } = 0$ , otherwise. The multiple MK(N-M $M K ( N \times M , f , F )$ is defined as the convex hull of all feasible i2N fixik  Fk; for all k 2 M; (1) relation holds.

$$
\begin{array} { r l } { M K ( N \times M , f , F ) = \operatorname { c o n v } \{ x \in \mathbb { R } ^ { N \times M } \mid } & { } \\ { \sum _ { i \in N } f _ { i } x _ { i k } \leq F _ { k } , } & { \mathrm { f o r ~ a l l ~ } k \in M ; \quad ( 1 ) } \\ { \sum _ { k \in M } x _ { i k } \leq 1 , } & { \mathrm { f o r ~ a l l ~ } i \in N ; \quad ( 2 ) } \\ { x _ { i k } \in \{ 0 , 1 \} , } & { \mathrm { f o r ~ a l l ~ } i \in N , k \in M \} . } \end{array}
$$

The constraints (1) are called knapsack constraints and the constraints (2) SOS (Special Ordered Set) constraints. The weighted multiple knapsack problem can

be solved  in principle  via the following linear program:

$$
\begin{array} { r l } { \operatorname* { m i n } } & { \sum _ { i \in N } \sum _ { k \in M } c _ { i k } x _ { i k } } \\ & { x \in M K ( N \times M , f , F ) . } \end{array}
$$

idea is the following. polytope $M K ( N \times M , f , F )$ by means of inequalities. This issue was addressed in Start with a small set of valid ine ualities for exam le the SOS and kna sack ine ualities. These ine ualities dene a ol hedron P0 that contains MK N - M F . O timize t

multiple knapsack problem. If y is also feasible, y is an optimal solution for the weighted multiple knapsack problem. Otherwise, th $P ^ { \prime }$ exists a valid $M K ( N \times$ $M , f , F )$ (N -M; f; F) that is violated by y. Thus, w $P ^ { \prime }$ ust solv $y$ the separation problem which is to $y$ nd a valid inequality that is violated by y. If such an inequality is found, we add it $y$ o the linear pro $y$ ram and solve it again. The procedure of iteratively solving linear programs and adding violated constraints is c $M K ( N \times M , f , F )$ cutting plane algorit $y$ . Thus, we must solve the separation problem which is to find a valid inequality that is violated by $y$ . If such an inequality is found, we add it to the linear program and solve it again. The lower bound for the wei hted multi le kna sack roblem. The latter case is not avoidable in eneral since we do not know a c

classes of facet-dening inequalities. If we intend to nd an optimal solution of the problem we must embed the procedure into an enumeration scheme. avoidable in general, since we do not know a complete description of the multiple knapsack polytope, and exact separation routines are not available for all known classes of facet-defining inequalities. If we intend to find an optimal solution of the problem we must embed the procedure into an enumeration scheme.

ration problem for these classes of inequalities. We investigate the computational complexity of the separation problem for one class and present several heuristic procedures to nd violated inequalities. This issue includes lifting and complementing of inequalities. In Section 4 we deal with implementational details. In particular, a primal heuristic to nd a good feasible solution for the multiple knapsack problem is presented. We have tested our cutting plane based algorithm on instances arising in the applications mentioned above. The computational results we have obtained are shown in Section 5. particular, a primal heuristic to find a good feasible solution for the multiple knapsack problem is presented. We have tested our cutting plane based algorithm on instances arising in the applications mentioned above. The computational results we have obtained are shown in Section 5.

# role in our cutting plane algorithm. For many of these classe

suppose throughout this chapter that an instance (N; M; f; F) of the multiple knapsack problem is given. In case jMj = 1, the quadruple (N; M; f; F) denes an instance of the single knapsack problem. We will frequently abbreviate this instance by the triple (N; f; Fk) where M = fkg. First of all, let us x some notation. $( N , M , f , F )$ of the multiple knapsack problem is given. In case $| M | = 1$ , the quadruple $( N , M , f , F )$ defines It will turn out that we often refer to subinstances of the multi le kna sack roblem where certain $( N , f , F _ { k } )$ not feas $M = \{ k \}$ rtain kna sacks. Thus we will notation.

It will turn out that we often refer to subinstances of the multiple knapsack MK(T; f; F) := convfx 2 IR j Pi:(i;k)2T fixik  Fk; k 2 Sl=1 Bl; Pk:(i;k)2T xik  1 $A _ { i } \subseteq N$ 2 Sj= $B _ { i } \subseteq M$ for $i = 1 , \ldots , t$ are given, and let $T : = \cup _ { i = 1 } ^ { t } A _ { i } \times B _ { i }$ 0; 1g; (i; k) 2

$$
\begin{array} { r l r } { M K ( T , f , F ) : = \mathrm { c o n v } \{ x \in \mathbb { R } ^ { T } \mid } & { \sum _ { i : ( i , k ) \in T } f _ { i } x _ { i k } \leq F _ { k } , } & { k \in \bigcup _ { l = 1 } ^ { t } B _ { l } , } \\ & { \sum _ { k : ( i , k ) \in T } x _ { i k } \leq 1 , } & { i \in \bigcup _ { j = 1 } ^ { t } A _ { j } , } \\ & { x _ { i k } \in \{ 0 , 1 \} , } & { ( i , k ) \in T \} . } \end{array}
$$

MK(T; f; F) equals jTj = Pti=1 jAijjBij if and only if fi  Fk for all (i; k) 2 T. For the remainder of this paper we assu $M K ( N \times M , f , F )$ r all i 2 N; k 2 M. abbreviate by $M K$ . It is easy to see that $M K$ is full dimensional if and only A $f _ { i } \ \leq \ F _ { k }$ N is a $i \in N$ with $k \in M$ to some kna sack k 2 M if P > F . $M K ( T , f , F )$ minima $\begin{array} { r } { | T | = \sum _ { i = 1 } ^ { t } \left| A _ { i } \right| \left| B _ { i } \right| } \end{array}$ if P $f _ { i } \leq F _ { k }$ or all s $( i , k ) \in T$ t d 1 be some inte er. We sa that a subset of $f _ { i } \leq F _ { k }$ S N $i \in N$ - $k \in M$ i jDj = $S \subseteq N$ satises f(D)  Fk and f(D [ fsg) > Fk $k \in M$ 2 $\textstyle \sum _ { i \in S } f _ { i } > F _ { k }$ this notation a minimal cover is a 1-c $k$ ver. $\sum _ { i \in S \backslash \{ s \} } f _ { i } \leq F _ { k }$ with N $s \in \ S$ and $d \geq 1$ n N0 is called a (1,d)-conguration with respect $S \subseteq N$ kna $d$ sack k 2 M respect to some knapsack $k \in M$ , if $S$ is a cover and every subset $D \subseteq S$ with $| D | = | S | - d$ satisfies $f ( D ) \leq F _ { k }$ and $f ( D \cup \{ s \} ) > F _ { k }$ for all $s \in S \setminus D$ . Using this notation a minimal cover is a 1-cover. A set $N ^ { \prime } \cup \{ z \}$ with $N ^ { \prime } \subseteq N$ and $z \in N \setminus N ^ { \prime }$ 0 fj  Fk; $( 1 , d )$ -configuration with respect to some knapsack $k \in M$ if

$\begin{array} { r } { \sum _ { j \in N ^ { \prime } } f _ { j } \le F _ { k } } \end{array}$

2. $K \cup \{ z \}$ is a minimal cover with respect to knapsack $k$ , for all $K \subset N ^ { \prime }$ with $| K | = d$

For $I \subseteq N$ and a vector $\boldsymbol { x } \in \mathbb { R } ^ { N }$ we set $\textstyle x ( I ) : = \sum _ { i \in I } x _ { i }$

i 2 N; k 2 M. In case m  2, the SOS constraints dene facets of MK.   
multiple knapsack polyhedron.

the M knapsack constraints we can associa $x _ { i k } \geq 0$ ingle knapsack p $M K$ edron $i \in N , k \in M$ . In case $m \geq 2$ , the SOS constraints define facets of $M K$

Let $( N , M , f , F )$ be an instance of the multiple knapsack problem. With each of Obv $| M |$ l for ever k M the relation MK N-M F SK N F hold

$$
S K ( N , f , F _ { k } ) : = \operatorname { c o n v } \{ x \in \mathbb { R } ^ { N } \ | \ \sum _ { i \in N } f _ { i } x _ { i } \leq F _ { k } , x _ { i } \in \{ 0 , 1 \} , i \in N \} .
$$

subsequent lemma s $k \in M$ at all nontri $M K ( N \times M , f , F ) \subseteq S K ( N , f , F _ { k } )$ ciated with the single knapsack polytopes are inherited by MK (cf. [GR90]). these single knapsack polyhedra can be used to describe the corresponding multiple knapsack polytope. Indeed, the answer to this question is yes, since the Lemma 2.1 Let V  N and k 2 M be given. Suppose a x   is a nontrivial facet-dening inequality of SK(V; f; Fk). Then, $M K$   denes

Lemma 2.1 Let $V \subseteq N$ and $k \in M$ i; if l = k; $a ^ { T } x \leq \alpha$ is a nontrivial facet-defining inequality of $S K ( V , f , F _ { k } )$ erwise. $\overline { { a } } ^ { T } x \leq \alpha$ defines a facet of $M K ( V \times M , f , F )$ , where $\overline { { a } } \in \mathbb { R } ^ { V \times M }$ and

$$
\overline { { { a } } } _ { i l } : = \left\{ \begin{array} { c l } { { a _ { i } , } } & { { i f l = k ; } } \\ { { 0 , } } & { { o t h e r w i s e . } } \end{array} \right.
$$

valid for MK(N-M; f; F) is called individual $M K ( N \times M , f , F )$ s for the polytope MK(N-M; f; F) that cannot be obtained by applying Lemma 2.1 $a ^ { T } x \leq \alpha$ lled joint. Examples of individual inequaliti $S K ( N , f , F _ { k } )$ nimal co $\overline { { a } } _ { i l } \ : = \ : a _ { i }$ alit $l = k$ the $\overline { { a } } _ { i l } = 0$ nguration i $( i \in V , l \in M )$ we want to present now $\overline { { a } } ^ { T } x \leq \alpha$ which is valid for $M K ( N { \times } M , f , F )$ is called individual. Valid inequalities for the polytope $M K ( N \times M , f , F )$ N is a minimal cover with res ect to some kna sack k 2 M. The ine u alit the $( 1 , d )$ X x  jS j   1

Suppose that $S \subseteq N$ is a minimal cover with respect to some knapsack $k \in M$ The inequality

$$
\sum _ { i \in S } x _ { i k } \leq | S | - 1
$$

Another well known class of individual inequalities c $S$ nsist $k$ of the (1,d)-conguration inequalities. Suppose that N0 [fzg  N is a (1,d)-conguration with r $S$ pect $k$ o some knapsack k $S K ( S , f , F _ { k } )$ nequality $M K ( S \times M , f , F ) )$

X xik + (jN j   d + 1)xzk  jN j $( 1 , d )$ -configuration inequalities. Suppose that $N ^ { \prime } \cup \{ z \} \subseteq N$ is a $( 1 , d )$ -configuration with respect to some knapsack $k \in M$ . The inequality

$$
\sum _ { i \in N ^ { \prime } } x _ { i k } + ( | N ^ { \prime } | - d + 1 ) x _ { z k } \leq | N ^ { \prime } |
$$

is called $( 1 , d )$ -configuration inequality corresponding to $N ^ { \prime } \cup \{ z \}$ and $k$ . In [P80] it was shown that the $( 1 , d )$ -configuration inequality corresponding to $N ^ { \prime } \cup \{ z \}$ and $k$ defines a facet of $S K ( N ^ { \prime } \cup \{ z \} , f , F _ { k } )$ (and, therefore, of $M K ( ( N ^ { \prime } \cup \{ z \} ) { \times } M , f , F ) )$

this section we will briey re $( 1 , d )$ some of the results from our companion paper. joint inequalities that are valid for the multiple knapsack polytope (cf. [W90], In [FMW93] a theorem is presented which allows to extend certain classes of facetdening inequalities of the multiple knapsack polytope. Here, we will restrict the discussions just to the special case where a minimal cover inequality is to be

In [FMW93] a theorem is presented which allows to extend certain classes of facetLet S  N be a minimal cover with respect to some knapsack k 2 M and let M0  M be a subset of knapsacks with k 2 M0. Let us choose a positive integer r  minfjN n Sj; jM n M0jg, sets T1; : : : ; Tr that are mutually

Let $S \subseteq N$ be a minimal cover with respect to some knapsack $k \in M$ and let $M ^ { \prime } \subseteq M$ X X X $k \in M ^ { \prime }$ . Let us choose a positive integer $r \leq \operatorname* { m i n } \{ | N \setminus S | , | M \setminus M ^ { \prime } | \}$ v=1 i2 $T _ { 1 } , \dots , T _ { r }$ that are mutually disjoint subsets of $N \backslash S$ and a subset $\{ k _ { 1 } , \ldots , k _ { r } \}$ of $M \backslash M ^ { \prime }$ . We call the inequality

$$
\sum _ { i \in S } x _ { i k } + \sum _ { v = 1 } ^ { r } \sum _ { i \in S \cup T _ { v } } x _ { i k _ { v } } \leq | S | - 1 + \sum _ { v = 1 } ^ { r } | T _ { v } |
$$

the extended cover inequality corresponding to $S$ $T _ { 1 } , \dots , T _ { r } , \ k , k _ { 1 } , \dots , k _ { r }$ . It is Finally, $M K$ s introduce t $T _ { v } \cup \{ i \}$ of multiple cover inequa $k _ { v }$ es whi $i \in S$ n be $v = 1 , \ldots , r$ generalization of minimal cover inequalities to several knapsacks. These inequalities were introd

Finally, let us introduce the class of multiple cover inequalities which can be viewed as a generalization of minimal cover inequalities to several knapsacks. These inequalities were introduced in [W90], and in [FMW93] some conditions were derived when they define facets.

i2S j 2J $( N , M , f , F )$ be given. Suppose, $S \subseteq N$ d mu $J \subseteq M$ ver inequa $\begin{array} { r } { \sum _ { i \in S } f _ { i } > \sum _ { k \in J } F _ { k } } \end{array}$ the polytope MK(N-M; f; F). inequality

$$
\sum _ { i \in S } \sum _ { j \in J } x _ { i j } \leq | S | - 1
$$

practical problems. $M K ( N \times M , f , F )$

For the rest of this paper we will deal with the task how to integrate these inequalities in a cutting plane algorithm and we will discuss their use in solving 3 The Sep

# presented in [FMW93]. Formally, the separa

In this section we deal with the separation problems for the classes of inequalities Given an instance (N; M; f; F) of the multiple knapsack problem, a vector y 2 [0; 1] and a c

Given an instance $( N , M , f , F )$ of the multiple knapsack problem, a vector $y \in [ 0 , 1 ] ^ { N \times M }$ and a class of valid inequalities for $M K ( N \times$ $M , f , F )$ of inequalities sh $y$ wn in the previous section include the co over. So, it seems natural to look at the separ $y$ tion prob

single knapsack problem. This fact indicates that the separation problem for the minimal cover inequalities is also NP-hard. We have not found an explicit proof of this result in the literature. Therefore, we give a short proof here. to some weighting of the items) cover is $\mathcal { N P }$ -hard, because it reduces to the Though this result does not prove that all the other separation problems are NPhard as well we con ecture that $\mathcal { N P }$ e roblems are not solvable in ol nomial time. Thus we ut our em hasis on develo in se aration heuristic

ideas of lifting and complementing inequalities. $\mathcal { N P }$ - hard as well, we conjecture that these problems are not solvable in polynomial time. Thus, we put our emphasis on developing separation heuristics, which we will discuss in the following. We conclude this section by describing the main ideas of lifting and complementing inequalities.

# 3.1 Separation of Minimal Cover Inequalities

Theorem 3.1 The separation problem for the minimal cover inequalities is N Phard.

# Proof.

(SMC) Given an instance (V; a; b) of the single knapsack problemV $( S M C )$ vector x 2 [0; 1] . Does there exist a subset S  V suc $\mathcal { N P }$ at i2S ai

(SMC) Given an instance $( V , a , b )$ of the single knapsack problem and a vector h $x \in [ 0 , 1 ] ^ { V }$ e decision problem associate $S \subseteq V$ he knapsac $\textstyle \sum _ { i \in S } a _ { i } \geq b + 1$ , $\Sigma _ { i \in S \backslash \{ j \} } a _ { i } \leq b$ e NP-c $j \in S$ te [K $\begin{array} { r } { \sum _ { i \in S } x _ { i } > | S | - 1 ; } \end{array}$ ed

(KP) Given an instance (R; w; k) of the single knapsack problem, an obR $( K P )$ e function vector $\mathcal { N P }$ IN and a positive integer number f $( S M C )$

(KP) Given an instance $( R , w , k )$ of the single knapsack problem, an objective of all, note tha $c \in \mathbb { N } ^ { R }$ ) belongs to NP, since it can $f \in \mathbb { N }$ ed in linear whether a give $S ^ { \prime } \subseteq R$  V is a $\sum _ { i \in S ^ { \prime } } c _ { i } \geq f$ (SM $\begin{array} { r } { \sum _ { i \in S ^ { \prime } } w _ { i } \le k \sharp } \end{array}$ w

Let an instance IKP o $( S M C )$ be given, i. $\mathcal { N P }$ an instance (R; w; k) of the single knapsack problem, a weig $S \subseteq V$ or c 2 INR and a $( S M C )$ integer number f 2 IN. $( K P )$ ene an instance IS $( S M C )$ SMC) by setting

Let an instance $\mathcal { T } _ { K P }$ of $( K P )$ be given, i. e., an instance $( R , w , k )$ of the single xi := 1   $c \in \mathbb { N } ^ { R }$ for all i 2 V; $f \in \mathbb { N }$ We define an instance $\mathcal { T } _ { S M C }$ := $( S M C )$ by setting

$$
\begin{array} { r l } { V } & { : = R ; } \\ { x _ { i } } & { : = 1 - \frac { w _ { i } } { k } + \epsilon , ~ \mathrm { f o r ~ a l l } ~ i \in V ; } \\ { a } & { : = c ; } \\ { b } & { : = f - 1 ; } \end{array}
$$

Let S be a solutio

Now we show that $\mathcal { T } _ { K P }$ has a solution if and only if $\mathcal { T } _ { S M C }$ has one.

Let $S$ be a solution of $\mathcal { T } _ { S M C }$ . Then, $\begin{array} { r } { \sum _ { i \in S } a _ { i } \ \geq \ b + 1 } \end{array}$ and $\textstyle \sum _ { i \in S } x _ { i } > | S | - 1$ By substitution, we obtain $\textstyle \sum _ { i \in S } c _ { i } \geq f$ and $\begin{array} { r } { \sum _ { i \in S } ( 1 - \frac { w _ { i } } { k } + \epsilon ) > | S | - 1 } \end{array}$ .Thus, $\begin{array} { r } { | S | ( 1 + \epsilon ) - \frac { 1 } { k } \sum _ { i \in S } w _ { i } > | S | - 1 } \end{array}$ y proper subset $\begin{array} { r } { \frac { 1 } { k } \sum _ { i \in S } w _ { i } < 1 + \epsilon | S | } \end{array}$ of IKP $\begin{array} { r } { \epsilon < \frac { 1 } { k | V | } } \end{array}$ Pi2 $w _ { i } \in \mathbb { N }$ f and Pi2S0 w $\textstyle \sum _ { i \in S } w _ { i } \leq k$ stitut $S$ g c and f, we $\mathcal { T } _ { K P }$ i

Pi2S0 wi  k b $S ^ { \prime }$  k and adding j $\mathcal { T } _ { K P }$ o both sides, we obtain jS0j   1 Pi2S0 wi  jS0j $S ^ { \prime }$ 1; which is equivalent to Pi2S0(1   wi ) $S ^ { \prime }$ jS0j   1: Since  > $\mathcal { T } _ { K P }$ we get $\begin{array} { r } { \sum _ { i \in S ^ { \prime } } c _ { i } \geq f } \end{array}$ + ) > $\textstyle \sum _ { i \in S ^ { \prime } } w _ { i } \ \leq \ k$ hence, Pi2S0 xi $c$ > jS0j $f$ 1: Thus, S0 i $\sum _ { i \in S ^ { \prime } } a _ { i } \geq$ $b + 1$ MC . $S ^ { \prime }$ is minimal, we have that $\Sigma _ { i \in S ^ { \prime } \backslash \{ j \} } a _ { i } \leq b$ for all $j \in S$ . Dividing $\Sigma _ { i \in S ^ { \prime } } w _ { i } \le k$ by $- k$ and adding $| S ^ { \prime } |$ to both sides, we obtain $\begin{array} { r } { | S ^ { \prime } | - \frac { 1 } { k } \sum _ { i \in S ^ { \prime } } w _ { i } \geq } \end{array}$ $| S ^ { \prime } | - 1$ 1] a pseudopolynomial al $\begin{array} { r } { \sum _ { i \in S ^ { \prime } } \bigl ( 1 - \frac { w _ { i } } { k } \bigr ) \ge \bigl | S ^ { \prime } \bigr | - 1 } \end{array}$ t solves $\epsilon > 0$ paration $\begin{array} { r } { \sum _ { i \in S ^ { \prime } } ( 1 - \frac { w _ { i } } { k } + \epsilon ) > | S ^ { \prime } | - 1 } \end{array}$ inequalities. $\begin{array} { r } { \sum _ { i \in S ^ { \prime } } x _ { i } > \vert S ^ { \prime } \vert - 1 } \end{array}$ ased o $S ^ { \prime }$ transformatio $\mathcal { T } _ { S M C }$ h er solved with a pseudopolynomial time and space complexity. problem for minimal cover inequalities. The algorithm is based on a transformaIn our code we have integrated a heuristic to separate minimal cover inequalities that was introduced in [CJP83]. This procedure can be described as follows. solved with a pseudopolynomial time and space complexity.

Separation heuristic for minimal cover inequalities Input: An instance of the single knapsack problem (N; f; C) and a

# Separation heuristic for minimal cover inequalities

Solve the following linear program $( N , f , C )$ and a vector $x ^ { \prime } \in [ 0 , 1 ] ^ { N }$

min Pi2N (1   xi)\~si

0  s\~i 

$$
\begin{array} { r l } { \operatorname* { m i n } } & { \sum _ { i \in N } ( 1 - x _ { i } ^ { \prime } ) \tilde { s } _ { i } } \\ { s . t . } & { \sum _ { i \in N } f _ { i } \tilde { s } _ { i } \geq C + 1 , } \\ & { 0 \leq \tilde { s } _ { i } \leq 1 \ \mathrm { f o r ~ a l l } \ i \in N . } \end{array}
$$

ineq $S : = \{ i \in N \mid \tilde { s } _ { i } > 0 \}$

Reduce $S$ to a minimal cover.   
Lift the corresponding inequality to a facet of $S K ( N , f , C )$   
tore all minimal covers we obtain by applying this procedure in a c ture, called \

We store all minimal covers we obtain by applying this procedure in a certain structure, called "pool". We use these minimal covers as substructures for some other separation routines (see next subsection). Note that the minimal cover $S$ found by the heuristic defines a facet for the polytope $S K ( S , f , C )$ , but not

The linear prog $S K ( N , f , C )$ heuristic can be solved eciently by using Dantzig's $S K ( N , f , C )$ For ease of exp $M K ( N \times M , f , F ) )$ r the moment that N = f1; : : : ; ng and that (1 x1)  : : :  (1 xn) . Set c := min i 2 1; : : : ; n Pi

The linear program in the heuristic can be solved efficiently by using Dantzig's >> 1; 1  i  c   1; $N = \{ 1 , \ldots , n \}$ ad that $\begin{array} { r } { \frac { ( 1 - x _ { 1 } ) } { f _ { 1 } } \leq . . . \leq \frac { ( 1 - x _ { n } ) } { f _ { n } } } \end{array}$ c  $c : = \operatorname* { m i n } \{ i \in \{ 1 , \ldots , n \} \mid \Sigma _ { j = 1 } ^ { i } f _ { j } > C \}$ >: C+ j=1 fj ; i = c: $s ^ { * } = ( s _ { i } ^ { * } ) _ { i \in N }$ , where

$$
s _ { i } ^ { * } = \left\{ \begin{array} { l l } { 1 , } & { 1 \leq i \leq c - 1 ; } \\ { 0 , } & { c + 1 \leq i \leq n ; } \\ { \frac { C + 1 - \sum _ { j = 1 } ^ { c - 1 } f _ { j } } { f _ { c } } , } & { i = c . } \end{array} \right.
$$

# violated inequalities for the multiple knapsack

to b e cut o. violated inequalities for the multiple knapsack polytope. For the exposition of Separation of (1; d)-Conguration Inequalities $( N , M , f , F )$ of the multiple knapsack problem is given and that $x ^ { \prime } \in [ 0 , 1 ] ^ { N \times M }$ is the fractional point In order to n

# can be describe $( 1 , d )$ ollows.

In order to find violated $( 1 , d )$ -configuration inequalities we have been implementing and evaluating two heuristics. One of these was introduced in [CJP83] and can be described as follows.

# For every ite

if P 2N0[ i fj  C a $S$ d if for all K  N0 [ fig with jK $k$ = d,

Let $z \in S$ t K [ fzg is a cover with respect t   
Set $N ^ { \prime } : = S \setminus \{ z \}$ N0 [ $d : = | N ^ { \prime } |$   
lift the $i \in N \backslash S$ ding (1,d)- $\begin{array} { r } { \sum _ { j \in N ^ { \prime } \cup \{ i \} } f _ { j } \le F _ { k } } \end{array}$ q if $\begin{array} { r } { \sum _ { j \in N ^ { \prime } \cup \{ i \} } f _ { j } \le C } \end{array}$ it is violated. $K \subseteq N ^ { \prime } \cup \{ i \}$ with $| K | = d$ the set $K \cup \{ z \}$ is a cover with respect to $k$ set $N ^ { \prime } : = N ^ { \prime } \cup \{ i \}$ ond algorithm for ndi $( 1 , d )$ ; d)-conguration inequalities ter t and partitions the set

The second algorithm for finding $( 1 , d )$ -configuration inequalities uses a threshold parameter $t$ and partitions the set of items $N$ into two sets $L$ and $S$ . For the be descr $S$ ed as follows. $t$ and the items in $L$ have weight greater than $t$ . The special element of the $( 1 , d )$ -configuration is now chosen among the items in $L$ and the other elements in the $( 1 , d )$ -configuration Heuristi $S$ by solving a linear program. More precisely, the algorithm can Set L := fi 2 N j

# Solve the foll

Set $L : = \{ i \in N \mid f _ { i } > t \}$ and $S : = \{ i \in N \mid f _ { i } \leq t \}$ Choose a knapsack $k \in M$ Let $z \in L$ s:t: Pi2S f $x _ { z } ^ { \prime } = \operatorname* { m a x } \{ x _ { i } ^ { \prime } \mid i \in L \}$ 0  t i 

$$
\begin{array} { r l } { \operatorname* { m a x } } & { \sum _ { i \in S } x _ { i } ^ { \prime } t _ { i } } \\ { s . t . } & { \sum _ { i \in S } f _ { i } t _ { i } \leq F _ { k } , } \\ & { 0 \leq t _ { i } \leq 1 , \mathrm { ~ f o r ~ a l l ~ } i \in S . } \end{array}
$$

Set $N ^ { \prime } : = \{ i \in S \mid t _ { i } = 1 \}$   
If $N ^ { \prime } \cup \left\{ z \right\}$ is a $( 1 , d )$ -configuration,   
Problem Heuristic 1 Heuristic 2

f violated inequalities found by the rst $d$ rocedure is given. Accord   

<table><tr><td rowspan=1 colspan=1>Problem</td><td rowspan=1 colspan=1>Heuristic 1</td><td rowspan=1 colspan=1>Heuristic 2</td></tr><tr><td rowspan=1 colspan=1>c|2 0% red.</td><td rowspan=1 colspan=1>3</td><td rowspan=1 colspan=1>106</td></tr><tr><td rowspan=1 colspan=1>c|21%red.</td><td rowspan=1 colspan=1>4</td><td rowspan=1 colspan=1>162</td></tr><tr><td rowspan=1 colspan=1>c|22% red.</td><td rowspan=1 colspan=1>1</td><td rowspan=1 colspan=1>91</td></tr><tr><td rowspan=1 colspan=1>cl23% red.</td><td rowspan=1 colspan=1>1</td><td rowspan=1 colspan=1>124</td></tr><tr><td rowspan=1 colspan=1>cl2 4% red.</td><td rowspan=1 colspan=1>1</td><td rowspan=1 colspan=1>143</td></tr><tr><td rowspan=1 colspan=1>dm1 36.75% red.</td><td rowspan=1 colspan=1>1</td><td rowspan=1 colspan=1>9</td></tr><tr><td rowspan=1 colspan=1>dm136.8%red.</td><td rowspan=1 colspan=1>1</td><td rowspan=1 colspan=1>9</td></tr><tr><td rowspan=1 colspan=1>dm2 27 %red.</td><td rowspan=1 colspan=1>1</td><td rowspan=1 colspan=1>4</td></tr><tr><td rowspan=1 colspan=1>dm2 28%red.</td><td rowspan=1 colspan=1>0</td><td rowspan=1 colspan=1>9</td></tr><tr><td rowspan=1 colspan=1>dm2 29%red.</td><td rowspan=1 colspan=1>1</td><td rowspan=1 colspan=1>6</td></tr><tr><td rowspan=1 colspan=1>dm2 30 % red.</td><td rowspan=1 colspan=1>0</td><td rowspan=1 colspan=1>16</td></tr></table>

conguration inequalities that were obtained by applying Heuristic 2. On all (see Section 5 for more details on these instances). In column 2 the total number of violated inequalities found by the first procedure is given. Accordingly, the numbers shown in column 3 correspond to the number of violated $( 1 , d )$ configuration inequalities that were obtained by applying Heuristic 2. On all

Hence, choosing one item from the cover as the special element of the conguration and adding some other items that do not belong to the cover may not give rise to a violated inequality. In contrast, the performance of Heuristic 2 only depends on the fractional point x0 and on the parameter t. In our implementation we sort the items in increasing order according to their weights, w.l.o.g. N = f1; : : : ; ng, f1  f2  : : :  fjNj, and run the heuristic with all possible sets L and S such that S = f1; : : : ; ig, L = fi + 1; : : : ; jNjg and fi < fi+1. depends on the fractional point $x ^ { \prime }$ and on the parameter $t$ . In our implemenSeparation of Multiple Cover Inequalities $N = \{ 1 , \ldots , n \}$ $f _ { 1 } \leq f _ { 2 } \leq . . . \leq f _ { | N | }$ , and run the heuristic with all possible sets $L$ iven $S$ set J  $S = \{ 1 , \dots , i \}$ s. $L = \{ i + 1 , \dots , | N | \}$ with $f _ { i } < f _ { i + 1 }$ o

# to nd violated multiple cover inequalities, is

we then try $J \subseteq M$ mine a set of items that denes a multiple cover. $J$ he latter problem $S \subseteq N$ , in princip $f ( S ) \ > \ F ( J )$ the minimal cover separation routines to the \aggregated" knapsack with capacity F(M0). More precisely, suppose, x0 2 IRN-M is t $\mathcal { M }$ current fractional $M ^ { \prime } \subseteq M$ d M0  M is the set of k $M ^ { \prime } \in \mathcal { M }$ for which we want to nd a multiple cover. We dene the instance (N; f; C) of the single knapsack problem by setting C := F(M0). Moreover we dene a new fractional point, y 2 IRN say, where yi := Pk $F ( M ^ { \prime } )$ for all i 2 N. With input $\boldsymbol { x } ^ { \prime } \in \mathbb { R } ^ { N \times M }$ d y, the routines for nding minim $M ^ { \prime } \subseteq M$ nequalities are called. If these calls yield a violated minimal cover inequality, it is transformed $( N , f , C )$ he original space and, hence, corresponds t $C : = F ( M ^ { \prime } )$ multiple cover inequality. fractional point, $y \in \mathbb { R } ^ { N }$ say, where $\begin{array} { r } { y _ { i } : = \sum _ { k \in M ^ { \prime } } x _ { i k } ^ { \prime } } \end{array}$ for all $i \in N$ . With input $( N , f , C )$ ately $y$ there are 2jMj   (jMj + 2) dierent sets of knapsacks for which we could perform the algorithm just described. This would, even for small jMj, result in an immense running time. Therefore, we generate a set M of candida

item i 2 N we determine $2 ^ { | M | } - \left( | M | + 2 \right)$ x0ik > 0g, where x0 is the current LP solution. If 2  jBij  jMj   1, we consider Bi as one candidate set for w $| M |$ we try to nd a multiple cover as described before. In case Bi $\mathcal { M }$ M, we simply $M ^ { \prime } \subseteq M$ ubsets of M of cardinality jMj   1 to the set M of candidate sets. The idea $i \in N$ s (heuristic) se $B _ { i } : = \{ k \in M \mid x _ { i k } ^ { \prime } > 0 \}$ ets is t $x ^ { \prime }$ t Bi is a subset of knapsacks w $2 \leq | B _ { i } | \leq | M | - 1$ one item is in $B _ { i }$ ict with its \correct position". Thus, additional inequalities are needed that provide further $B _ { i } = M$ tion how to handle this conic $M$ of cardinality $| M | - 1$ to the set $\mathcal { M }$ of candidate sets. The idea for this (heuristic) selection of the candidate sets is that $B _ { i }$ is a subset of Proceeding in this way, the number of dierent candidate sets that are generated Thus, additional inequalities are needed that provide further information how to handle this conflict.

Proceeding in this way, the number of different candidate sets that are generated

Let S be a cover with respect $| N | + | M | - 1$ s

# X(xik + xil) + X xil  jSj

is t $S$ extended cover inequality corresponding $k$ o S, $l \in M \backslash \{ k \}$ l. A $T \subseteq N \backslash S$ [FMW93], it is

$$
\sum _ { i \in S } ( x _ { i k } + x _ { i l } ) + \sum _ { i \in T } x _ { i l } \leq | S | + | T | - 1
$$

is the extended cover inequality corresponding to $S$ $T$ $k$ and $l$ . As shown in [FMW93], it is valid for the polytope $M K$ if and only if $T \cup \{ i \}$ is a cover with The rst r $l$ outine $i \in S$ es a cover S (with respect to some knapsack k) that is stored in the pool. For every l 2 M n f $S$ we proceed $T$ s follows. Initialize T by setti

a cover with respect to k where sm $S$ 2 S is an element in S mith mini $k$ al weight fs . In case this is true, we $l \in M \setminus \{ k \}$ nded cover inequality correspondi $T$ to S, T, k $T : = N \backslash S$ check for a possible violatio $T$ the item $i$ with minimal value $\frac { x _ { i l } } { f _ { i } }$ until the condition $f ( T ) \leq F _ { l }$ holds. Finally, we check whether $T \cup \{ s _ { m i n } \}$ defines At this point, let us no $k$ e that $s _ { m i n } \in S$ ion how to delet $S$ items from the initial $f _ { s _ { m i n } }$ is of very heuristic nature. The idea is that an item i with heigh weight and $S , T$ l $k$ alue $l$ il is very unlikely contained in the s

antees that the resulting inequality is valid, since f(T[fsg)  f(T[fsming) > Fk for $T$ l s 2 S. One property of this algorithm is that the re $i$ ult it produces strongly depends on $x _ { i l }$ e covers stored in the pool. Anothe $T$ way to generated extended cover inequalities is to start from the scratch a $[ [ T \cup \{ s _ { m i n } \} ]$ p a cover S and a set TnS based on the information given by the fracti $f ( T \cup \{ s \} ) \geq f ( T \cup \{ s _ { m i n } \} ) > F _ { k }$ speaki $s \in S$ e outline of the subsequent algorithm. depends on the covers stored in the pool. Another way to generated extended cover inequalities is to start from the scratch and build up a cover $S$ and a set $T \backslash S$ Extended Cover Heuristic 2 $x ^ { \prime }$ . This is, roughly Choose two knapsacks k; l 2 M, k 6= l and so

# 0  si  1 for all i 2 N:

Set S := fi 2 N j si > $k , l \in M$ $k \neq l$ and solve the linear program:

Reduc $\begin{array} { r } { \sum _ { i \in N } \bigl ( 1 . 0 - x _ { i k } ^ { \prime } - x _ { i l } ^ { \prime } \bigr ) s _ { i } } \end{array}$ $s . t$ sm $\Sigma _ { i \in N } f _ { i } s _ { i } > F _ { k }$ n $0 \leq s _ { i } \leq 1$ rogram $i \in N$

Set $S : = \{ i \in N \mid s _ { i } > 0 \}$

Reduce $S$ to a minimal cover.

Let $s _ { m i n }$ be an item in $S$ with minimum weight.

Solve the linear program:

Lift th $s . t$ $\begin{array} { r l r l } & { \sum _ { i \in N \backslash S } ( 1 . 0 - x _ { i l } ^ { \prime } ) t _ { i } } & & { } \\ & { \sum _ { i \in N \backslash S } f _ { i } t _ { i } > F _ { l } - f _ { s _ { m i n } } , } & & { \mathrm { S e t } \ T : = \{ i \in N \ \backslash \ S \ | \ t _ { i } > 0 \} . } \end{array}$ $0 \leq t _ { i } \leq 1$ for all $i \in N \backslash S$

Reduce $T$ so that $T \cup \{ s _ { m i n } \}$ is a minimal cover

Lift the extended cover inequality corresponding to $S , T$ $k$ and $l$

We have performed several experiments to evaluate both algorithms. It turned Separation of Heterogeneous Two-Cover Inequalities does the first one. Nevertheless, we included both routines in our cutting plane Before sketching the ideas how to nd violated heterogeneous two-cover ine

# M; k 6= l are given. Moreover, assume that S  N is a cove

Before sketching the ideas how to find violated heterogeneous two-cover inequalxik + (jSj   1)xil  jSj(jSj   1) $k , l \in$ $M , k \neq l$ are given. Moreover, assume that $S \subseteq N$ is a cover with respect to $\mathrm { k }$ is ca $G \subseteq N \setminus S$ geneous two-cover inequality correspo

$$
\sum _ { i \in S } x _ { i k } + \sum _ { i \in S \cup G } ( | S | - 1 ) x _ { i l } \leq | S | ( | S | - 1 )
$$

of inequalities proceeds in a two stage process. First a cove $S , G ,$ i $k$ res $l$ ect to knapsack k is generated by solving the sa $M K$ near program as in t ${ \tilde { G } } \subseteq G$ nded $\tilde { S } \subseteq S , | \tilde { G } | = | \tilde { S } | \geq 1$ ereafter, $S \setminus \tilde { S } \cup \tilde { G }$ N n S is generated by successively $l$ dding elements of N n S to G as long as the following condition is satised. The condition requires that every subset T  S [ G, jTj = jSj an $S$ T \ G 6= ; is a cover wit $k$ respect to l. This test can be performed eciently by maintaining a set Tmin with the jSj   1 smallest $G \subseteq N \setminus S$ S [ G and updating this set Tmin for each new $N \backslash S$ ad $G$ d to G. Moreover, the condition guarantees that the resulting inequality is valid for $T \subseteq S \cup G$ e $| T | = | S |$ e suc $T \cap G \neq \emptyset$ ding a violated heterogeneo $l$ us two-cover inequality, a lifting step is performed. This issue $T _ { m i n }$ cussed in $| S | - 1$ t subsection. $S \cup G$ and updating this set $T _ { m i n }$ for each new item added to $G$ . Moreover, the condition guarantees that the resulting inequality is valid for $M K$ . If the procedure succeeds in finding a violated heterogeneous two-cover inequality, a lifting step is performed. This issue is discussed in the next subsection.

# in solving practical problem instances via a polyhedral based a

The concept of lifting and complementing inequalities is a very important issue in solving practical problem instances via a polyhedral based approach. The idea coecients of those variables that are xed to zero in the subproblem. If some variable was xed to one, we refer to the operation of calculating this coecient as complementing. In the following we will discuss both operations in more detail. inequality must be determined. We call lifting the operation of calculating the Lifting Inequalities variable was fixed to one, we refer to the operation of calculating this coefficient Given an index set N, a subset S  N and a polytope P  [0; 1]N with 0/1

# P \ fx 2 IRN j xi = 0

coecients ak (k 2 $N$ n S) are cal $S \subseteq N$ g coecients. In $P \subseteq [ 0 , 1 ] ^ { N }$ fting s $0 / 1$ inequality can be solved via the f $a ^ { T } x \leq \alpha$ rocedure ([P75]). $P \cap \{ x \in \mathbb { R } ^ { N } \mid x _ { i } = 0 $ for all $i \in N \setminus S \}$ . We say that an inequality $\overline { { a } } ^ { T } x \leq \overline { { \alpha } }$ is a lifting of $a ^ { T } x \leq \alpha$ if $\overline { { a } } _ { i } = a _ { i }$ for all $i \in S$ $\overline { { \alpha } } = \alpha$ and $\overline { { a } } ^ { T } x \leq \overline { { \alpha } }$ is valid for $P$ . The Initia $\overline { { a } } _ { k }$ e $( k \in N \setminus S )$ all i 2 S . Choose a sequence of the variables in N n S (w.l.o.g.

Initialize $\overline { { a } } _ { i } = a _ { i }$ for all $i \in S$   
k := max a x $N \backslash S$ (w.l.o.g. we assume that   
s:t: x 2 P \ fx 2 IR $\{ 1 , \ldots , | N \setminus S | \} )$   
For $k = 1 , \ldots , | N \setminus S |$ ; 1g; for a

$$
\begin{array} { r l } { \gamma _ { k } : = } & { \operatorname* { m a x } \overline { { a } } ^ { T } x } \\ & { s . t . \quad x \in P \cap \{ x \in \mathbb { R } ^ { N } \mid x _ { k } = 1 , x _ { i } = 0 \mathrm { ~ i f ~ } | N \setminus S | \geq i > k \} } \\ & { \qquad x _ { i } \in \{ 0 , 1 \} , \mathrm { ~ f o r ~ a l l ~ } i \in S \cup \{ 1 , \ldots , k - 1 \} . } \\ { \overline { { a } } _ { k } : = \alpha - \gamma _ { k } . } \end{array}
$$

However, if P is the single knapsack polytope, Zemel showed that the coecients k (and hence ak) can be computed in polyno $N \backslash S$ me ([Z86]). His idea is to $a ^ { T } x \ \leq \ \alpha$ the problem, slightly modify it and solve this modied program by applying dynamic programming techniques. Due t $\gamma _ { k }$ he $\mathcal { N P }$ cular structure of the resultin $P$ optimization problem the running time of the dynamic program is $\gamma _ { k }$ unded by a $\overline { { a } } _ { k }$ ynomial in the size of the input data. "dualize" the problem, slightly modify it and solve this modified program by We have been implementing this idea and applied it to the classes of minimal cover and (1; d)-conguration inequalities. bounded by a polynomial in the size of the input data.

We have been implementing this idea and applied it to the classes of minimal cover and $( 1 , d )$ -configuration inequalities.

For the joint inequalities we cannot calculate the exact lifting coefficients effiprogram given in the procedure above and dene u $u _ { k }$ as the objective f $\gamma _ { k }$ ction value rounded down. In order to lift multiple cover ineq $\overline { { a } } _ { k } : = \alpha - u _ { k }$ oceed in a slightly dierent way. Roughly speaking, lifting of multiple cover inequalities is heuristically performed by lifting a cover inequality. Suppose, S  N is a multiple cover with respect to M0  M. With the multiple c $u _ { k }$ r inequality corresponding to S and M0 we associate a cover inequality Pi2S yi  jSj   1 which is valid for the single knapsack polytope SK(N; f; F(M0)). The latter inequality is now lifted by using Zemel's procedure. Let bTy  jSj   1 denote t $S \subseteq N$ ed inequality and dene aik := bi $M ^ { \prime } \subseteq M$ 2 M0 and i 2 N. Then, it is easy to see that the ine $S$ uality $M ^ { \prime }$ x  jSj   1 is a lifted multiple co $\begin{array} { r } { \sum _ { i \in S } y _ { i } \ \leq \ | S | - 1 } \end{array}$ esponding to S and M0 which is valid for the mu $S K ( N , f , F ( M ^ { \prime } ) )$ olytope MK. lifted by using Zemel's procedure. Let $b ^ { T } y \leq | S | - 1$ denote this lifted inequality Complem $\overline { { { a } } } _ { i k } : = \ : b _ { i }$ nequal $k \in M ^ { \prime }$ and $i \in N$ . Then, it is easy to see that the inequality $\overline { { a } } ^ { T } x \leq | S | - 1$ is a lifted multiple cover inequality corresponding to $S$ To $M ^ { \prime }$ knowledge the idea of complementing inequalitie $M K$ ft

# discuss the algorithms we design

To our knowledge the idea of complementing inequalities (lifting the compleGiven an index set N, a subset S  N and a polytope P  [0; 1]N with 0/1 vertices. Moreover, suppose that aTx   is a valid inequality for the polytope P \ fx 2 IRN j x = 1 for all i 2

is valid for P. $N$ e coecien $S \subseteq N$ k 2 N n S) are $P \subseteq [ 0 , 1 ] ^ { N }$ lemen $0 / 1$ coecients. Similarly to the pre $a ^ { T } x \leq \alpha$ bsection, a general procedure can be $P \cap \{ x \in \mathbb { R } ^ { N } \mid x _ { i } = 1 \mid$ menting $i \in N \backslash S \}$ equality aTx   which is val $\overline { { a } } ^ { T } x \le \overline { { \alpha } }$ polytope P \ fx 2 IRN $a ^ { T } x \ \leq \ \alpha$ r a $\overline { { a } } _ { i } ~ = ~ a _ { i }$ n Sg. $i \in S$ $\overline { { \alpha } } \geq \alpha$ and $\overline { { a } } ^ { T } x \le$ $\overline { \alpha }$ is valid for $P$ . The coefficients $\overline { { a } } _ { k }$ $( k \in \textit { N } \backslash \textit { S } )$ are called complementing coefficients. Similarly to the previous subsection, a general procedure can be Initialize ai = ai for all i 2 S and set  := . $a ^ { T } x \leq \alpha$ which is valid for the Choose a $P \cap \{ x \in \mathbb { R } ^ { N } \mid x _ { i } = 1 \qquad $ cients i $i \in N \setminus S \}$ .

k := $\overline { { a } } _ { i } = a _ { i }$ aTx $i \in S$ and set $\overline { { \alpha } } : = \alpha$ s:t: x 2 P \ fx 2 IRN j xk $N \backslash S$ i = 1 for all jN n Sj  i > xi 2 f0; 1g; $\{ 1 , . . . , | N \setminus S | \} )$ 1

ak : $k = 1 , \ldots , | N \rangle S |$ calculate   
$\mu _ { k } : = \mathrm { ~ \ m a x ~ }$ $\overline { { a } } ^ { T } x$ s.t. $x \in P \cap \{ x \in \mathbb { R } ^ { N } \mid x _ { k } = 0 , x _ { i } = 1$ for all $| N \setminus S | \geq i > k \}$ ; $x _ { i } \in \{ 0 , 1 \}$ , for all $i \in S \cup \{ 1 , . . . , k - 1 \}$   
$\begin{array} { r l } { \overline { { a } } _ { k } : = } & { { } \mu _ { k } - \overline { { \alpha } } } \end{array}$   
$\overline { { \alpha } } : = \mu _ { k }$

Let k 2 f1; : : : ; jN n Sjg be given and suppose that aTx   dene $P$ a facet of the polytope SK(S [ f1; : : : ; k   1g; f; F   PjNnSj fi). In order to obtain a fac $d$ t-denin ine ualit of the ol to e SK S [ 1 : : : k F   Pj

 k Let $k \in \{ 1 , \ldots , | N \setminus S | \}$ $\textstyle S K ( S \cup \{ 1 , \dotsc , k - 1 \} , f , F - \sum _ { i = k } ^ { | N \backslash S | } f _ { i } )$ be given and suppose that $\overline { { a } } ^ { T } x \le \overline { { \alpha } }$ . In order to obtain a defines a facet s:t: Pj2S[f1;:::;k 1g $S K ( S \cup \{ 1 , \dots , k \} , f , F - \textstyle \sum _ { i = k + 1 } ^ { | N \backslash S | } f _ { i } )$ the value $\mu _ { k }$ must be determined.

$$
\begin{array} { r l } { \mu _ { k } = } & { \operatorname* { m a x } \overline { { a } } ^ { T } x } \\ & { s . t . \quad \sum _ { j \in S \cup \{ 1 , \ldots , k - 1 \} } f _ { j } x _ { j } \leq F - \sum _ { i = k + 1 } ^ { | N \backslash S | } f _ { i } , } \\ & { x _ { j } \in \{ 0 , 1 \} , \mathrm { ~ f o r ~ a l l ~ } j \in S \cup \{ 1 , \ldots , k - 1 \} . } \end{array}
$$

s:t: aT x   $\mu \in \mathbb { N }$ , the following minimization problem (cf. [Z86]).

$$
\begin{array} { r l } { d ( \mu ) = } & { \operatorname* { m i n } \quad \sum _ { j \in S \cup \{ 1 , \dots , k - 1 \} } f _ { j } x _ { j } } \\ { s . t . } & { \overline { { a ^ { T } } } x \geq \mu } \\ & { x _ { j } \in \{ 0 , 1 \} , \mathrm { ~ f o r ~ a l l ~ } j \in S \cup \{ 1 , \dots , k - 1 \} . } \end{array}
$$

an upper bound for k that is polynin polynomial time. A trivial upper $\mu _ { k }$ mputed $\mu _ { k } = \operatorname* { m a x } \{ \mu \mid d ( \mu ) \stackrel { \cdot } { \leq } F - \textstyle \sum _ { i = k + 1 } ^ { | N \backslash S | } \bar { f } _ { i } \}$ dynamic programming techniques the problem of computing $\operatorname* { m a x } \{ \mu ~ | ~ d ( \mu ) ~ \leq$ $\begin{array} { r } { F - \sum _ { i = k + 1 } ^ { | N \setminus S | } f _ { i } \} } \end{array}$ k  X ai + a1 + : : : + $O ( | N | \mu _ { k } )$ Hence, if there exists an upper bound for $\mu _ { k }$ that is polynomial in $| N |$ , then $\mu _ { k }$ itself can be computed in polynomial time. A trivial upper bound for $\mu _ { k }$ is given by

$$
\mu _ { k } \leq \sum _ { i \in S } { \overline { { a } } } _ { i } + { \overline { { a } } } _ { 1 } + . . . + { \overline { { a } } } _ { k - 1 } .
$$

Solvin $\overline { { a } } _ { i } = \mu _ { i } - \mu _ { i - 1 }$ n formu $i = 1 , \ldots , k - 1$ Pi2S ai $\mu _ { 0 } = \overline { { \alpha } }$ Moreo $\overline { { a } } _ { i } = a _ { i }$ he case $i \in S$ nimal cover

$$
\mu _ { k } \leq \sum _ { i \in S } { \overline { { a } } } _ { i } + \mu _ { k - 1 } - { \overline { { \alpha } } } .
$$

Solving this recursion formula yields $\mu _ { k } \leq k ( \sum _ { i \in S } { \overline { { a } } } _ { i } - { \overline { { \alpha } } } )$ . Moreover, in the case In order to complemen $( 1 , d )$ nt inequalities, this type of a $\textstyle \sum _ { i \in S } { \overline { { a _ { i } } } } - { \overline { { \alpha } } }$ es not work any $| N |$ re. Hence, $k$ we determine ap $| N |$ ximate complement $| N | ^ { 2 }$ oecients by applying $\mu _ { k }$ e same techniques as in the case of lifting (see previous subsection). B

cover inequalities. This issue is discussed next. For the ease of exposition let more. Hence, we determine approximate complementing coefficients by applying the same techniques as in the case of lifting (see previous subsection). Besides this we have been implementing an additional complementing procedure for extended cover inequalities. This issue is discussed next. For the ease of exposition let on r we distinguish the following c $x _ { j r }$ is fixed to one. Moreover, assume that $\begin{array} { r } { \sum _ { i \in S } x _ { i k } + \sum _ { i \in S \cup T } x _ { i l } \le | S | + | T | - 1 } \end{array}$ is an extended cover inequality which is valid for $M K \cap \{ x _ { j r } = 1 \}$ . This implies, in particular, that $S$ is a cover with  r 6= $k$ r 6= l: Th $T \cup \{ i \}$ complementing coecient $l$ corresp $i \in S$ g to variable on $r$ we distinguish the following cases:

 $r \neq k , r \neq l$ is case the relation i2S fi > Fk  fj holds and hence, S [fjg is $x _ { j r }$ over with respect to k. If, in addition, $\begin{array} { r } { \sum _ { i \in S } x _ { i k } + \sum _ { i \in S \cup T } x _ { i l } \le | S | + | T | - 1 } \end{array}$ add j to S, $M K$   
• $r = k$ ponding to variable xjk is $\sum _ { i \in S } f _ { i } > F _ { k } - f _ { j }$ coecient corresp $S \cup \{ j \}$ to variable xjl is set to 0. $k$ his yields the in $T \cup \{ j \}$ Pi2S[ j xik +Pi2S[T $l$ il  jSj $j$ jT $S$   1 w $S : = S \cup \{ j \}$ for MK, but no longer an exte $\textstyle \sum _ { i \in S } x _ { i k } +$ $\textstyle \sum _ { i \in S \cup T } x _ { i l } \ \leq \ | S | + | T | - 1$ is valid for $M K$ . Otherwise, the coefficient corresponding to variable $x _ { j k }$ is set to 1 and the coefficient corresponding to r = l: T $x _ { j l }$ conditions above imply that T [ fig $\begin{array} { r } { \sum _ { i \in S \cup \{ j \} } x _ { i k } + \sum _ { i \in S \cup T } x _ { i l } \leq } \end{array}$ $\vert S \vert + \vert T \vert - 1$ .e., f(T) + fi > Fl   $M K$ herefore, we can append j to the set T, i.e., T :   
• $r = l$ K, as one can easily convince one $T \cup \{ i \}$ is a cover with respect to $l$ for all $i \in S$ , i.e., $f ( T ) + f _ { i } > F _ { l } - f _ { j }$ . Therefore, we can append $j$ to the set $T$ $T : = T \cup \{ j \}$ and the inequality $\begin{array} { r } { \sum _ { i \in S } x _ { i k } + \sum _ { i \in S \cup T } x _ { i l } \le \left| S \right| + \left| T \right| - 1 } \end{array}$ ct, this complementing procedure for extended c $S , T$ i $k$ equal $l$ ties can be aliz $M K$ the case when more than one varia

In fact, this complementing procedure for extended cover inequalities can be generalized to the case when more than one variable is fixed to one.

More precisely, there is a threshold parameter, t say, and a variable x is xed if 0 r 0 1  h l . Ini i ll i . . T $\boldsymbol { x } ^ { \prime } \in \mathbb { R } ^ { N \times M }$ h iz f the original problem instance drastically. Thereafter, the separation routines are called in order to nd violated inequalities for the subpolytope P := MK \fxik = 0; if x0 < t; xik = 1; if x0 > 1   tg. If the $t$ eparation algorithm $x _ { i k }$ ucceed in $x _ { i k } ^ { \prime } < t$ vi $x _ { i k } ^ { \prime } > 1 - t$ qualities for P, $t$ the appropriate complementing and lifting procedures are applied. Table 2 shows the number of violated inequalities that are obtained by xing variables to one (as described above), ca $P : = M K \cap \{ x _ { i k } =$ routi $x _ { i k } ^ { \prime } < t , x _ { i k } = 1$ ing $x _ { i k } ^ { \prime } > 1 - t \}$ enting the corresponding inequalities. For more details on the problem inst $P$ ces we refer to section 5. procedures are applied. Table 2 shows the number of violated inequalities that are obtained by fixing variables to one (as described above), calling the separation routines, applying lifting and complementing the corresponding inequalities. For more details on the problem instances we refer to section 5.

Table 2: Separation in subproblems using complementing procedure.   

<table><tr><td rowspan=1 colspan=1>Problem</td><td rowspan=1 colspan=1># viol. ineq.</td></tr><tr><td rowspan=1 colspan=1>c|2 0% red.</td><td rowspan=1 colspan=1>60</td></tr><tr><td rowspan=1 colspan=1>c|2 1%red.</td><td rowspan=1 colspan=1>127</td></tr><tr><td rowspan=1 colspan=1>c|2 2%red.</td><td rowspan=1 colspan=1>109</td></tr><tr><td rowspan=1 colspan=1>c|2 3%red.</td><td rowspan=1 colspan=1>123</td></tr><tr><td rowspan=1 colspan=1>cl2 4% red.</td><td rowspan=1 colspan=1>157</td></tr><tr><td rowspan=1 colspan=1>dm136.75%red.</td><td rowspan=1 colspan=1>14</td></tr><tr><td rowspan=1 colspan=1>dm136.8%red.</td><td rowspan=1 colspan=1>14</td></tr><tr><td rowspan=1 colspan=1>dm227 %red.</td><td rowspan=1 colspan=1>42</td></tr><tr><td rowspan=1 colspan=1>dm228%red.</td><td rowspan=1 colspan=1>47</td></tr><tr><td rowspan=1 colspan=1>dm2 29%red.</td><td rowspan=1 colspan=1>50</td></tr><tr><td rowspan=1 colspan=1>dm2 30 % red.</td><td rowspan=1 colspan=1>15</td></tr></table>

# cutting plane based algorithm. In order to make such an a

on some of these issues. cutting plane based algorithm. In order to make such an algorithm effective and For solvin the linear ro rams we use the CPLEX Callable Librar CPLEX92 a ver fast and robust LP solver written and su orted b R. E. Bixb . The initial linear ro ram in

For the practical applications we have in mind all items must be assigned to the knapsacks, i. e., the SOS constraints must be satised with equality. Thus, instead of using the SOS constraints we factually add the corresponding equalities Pk2M xik = 1 (i 2 N) to the initial linear prog $0 \leq x _ { i k } \leq 1$ now on, $i \in N$ i $k \in M$ a solution feasible for the multiple knapsack problem only if all items are assigned to the knapsacks, i. e., if all SOS constraints are satised with equality. instead of using the SOS constraints we factually add the corresponding equalities $\begin{array} { r } { \sum _ { k \in M } x _ { i k } = 1 } \end{array}$ $( i \in N )$ e desi n of a cuttin lane al orithm is to kee the actual linear ro ram of moderate size. To this end we eliminate ine ualities from the LP that are not ti ht at the current linear pro rammin solution x0.

we control the number of violated inequalities added to the LP by a parameter. linear program of moderate size. To this end, we eliminate inequalities from the LP that are not tight at the current linear programming solution $x ^ { \prime }$ . In each iteration we call all separation algorithms discussed in the previous section, but we control the number of violated inequalities added to the LP by a parameter.

If we find more violated inequalities than specified by this parameter, we take the An im ortant issue in our al orithm is the xin $a ^ { T } x \leq \alpha$ bles b reduc $\boldsymbol { a } ^ { T } \boldsymbol { x } ^ { \prime } - \boldsymbol { \alpha }$ is smallest. Of course, we make sure that no redundant inequalities are added to bound on the value

variable xik with x0 = 0 and z   z0  dik can be xed to zero. Similarly, each non $z ^ { \prime }$ asic variable xik with x0ik = 1 and z   z0   dik can b $z ^ { * }$ xed to one. Moreover, further variables can be xed by l $x ^ { \prime } = ( x _ { i k } ^ { \prime } )$ lications, for example, if som $d \ = \ ( d _ { i k } )$ xik is xed to one by the reduced cost criterion, then all variables xil; l 2 $x _ { i k }$ fkg; $x _ { i k } ^ { \prime } = 0$ xed $z ^ { * } - z ^ { \prime } \leq d _ { i k }$ e 3 shows for some problem instances the number of varia $x _ { i k }$ s (in p $x _ { i k } ^ { \prime } = 1$ es) t $z ^ { * } - z ^ { \prime } \leq - d _ { i k }$ this procedure. Moreover, further variables can be fixed by logical implications, for example, if some variable $x _ { i k }$ is fixed to one by the reduced cost criterion, then all variables $x _ { i l }$ $l \in M \setminus \{ k \}$ Problem Variables xed cl2 0% red. 2433 (22.32%)

since a complete description of the multiple   

<table><tr><td rowspan=1 colspan=1>Problem</td><td rowspan=1 colspan=1>Variables fixed</td></tr><tr><td rowspan=1 colspan=1>c|2 0% red.</td><td rowspan=1 colspan=1>2433  (22.32%)</td></tr><tr><td rowspan=1 colspan=1>c|2 1%red.</td><td rowspan=1 colspan=1>3039 (27.89%)</td></tr><tr><td rowspan=1 colspan=1>c|2 2%red.</td><td rowspan=1 colspan=1>2184  (20.04%)</td></tr><tr><td rowspan=1 colspan=1>cl2 3%red.</td><td rowspan=1 colspan=1>2933  (26.91%)</td></tr><tr><td rowspan=1 colspan=1>cl2 4% red.</td><td rowspan=1 colspan=1>3293  (30.22%)</td></tr><tr><td rowspan=1 colspan=1>dm136.75% red.</td><td rowspan=1 colspan=1>89   (8.79%)</td></tr><tr><td rowspan=1 colspan=1>dm136.8% red.</td><td rowspan=1 colspan=1>89   (8.79%)</td></tr><tr><td rowspan=1 colspan=1>dm2 27 % red.</td><td rowspan=1 colspan=1>1544  (33.33%)</td></tr><tr><td rowspan=1 colspan=1>dm2 28%red.</td><td rowspan=1 colspan=1>1538  (33.20%)</td></tr><tr><td rowspan=1 colspan=1>dm2 29%red.</td><td rowspan=1 colspan=1>3384  (73.05%)</td></tr><tr><td rowspan=1 colspan=1>dm2 30 % red.</td><td rowspan=1 colspan=1>1346  (29.05%)</td></tr></table>

heuristics in order to obtain good upper bounds on the value of the optimal solution. These heuristics are based on rounding the current linear programming is not known and exact separation algorithms for the known classes of inequalities are not at hand. Due to this fact, we have also implemented several LP-based In the rst heuristic we proceed as follows. We set F0 := Fk for all k 2 M and solution. These heuristics are based on rounding the current linear programming solution $x ^ { \prime }$

In the first heuristic we proceed as follows. We set $F _ { k } ^ { \prime } : = F _ { k }$ for all $k \in M$ and no further item can $i$ be assigned. $\{ x _ { i k } ^ { \prime } \mid k \in M$ and $f _ { i } \leq F _ { k } ^ { \prime } \}$ is maximum. Let $i ^ { * }$ be the "maximum" item and $k ^ { * }$ the corresponding knapsack. We assign $i ^ { * }$ he second he $k ^ { * }$ stic diers from the r $F _ { k ^ { * } } ^ { \prime }$ one by sele $F _ { k ^ { * } } ^ { \prime } : = F _ { k ^ { * } } ^ { \prime } - f _ { i ^ { * } }$ hat is assigned next, randomly. More precisely, we determine a random sequence of the items, and, according to thi

we assign item i to a knapsack k where the maximum value is attained, update F0 accordingly and continue. the items, and, according to this sequence, we compute $\operatorname* { m a x } \{ x _ { i k } ^ { \prime } \mid k \in M$ and $f _ { i } \leq F _ { k } ^ { \prime } \}$ hird heuristic, we interpret each vector (x0ik)k2M, $i$ r i 2 N, as a probability distribu $i$ ion, i. e., we to $k ^ { * }$ a dial that assigns item i to knapsack k with $F _ { k ^ { * } } ^ { \prime }$ bability x0ik. The sequence

a parameter that is a multiple of the number of $( x _ { i k } ^ { \prime } ) _ { k \in M }$ l var $i \in N$ , as a probability distribution, i. e., we toss a dial that assigns item $i$ to knapsack $k$ with It turns ou $\boldsymbol { x } _ { i k } ^ { \prime }$ hat none of these heuristics is superior to the others. In most exam les the rst two rocedures are more successful at the ver be innin whereas the third one erforms better in the se uel.

Moreover we have im lemented an im rovement heuristic that is based on the ideas of FM82 . The rocedure a lied to our roblem is described in the folwhereas the third one performs better in the sequel.

Moreover, we have implemented an improvement heuristic that is based on the Improvement heuristic. Initializ

# Set F0 := Fk   Pi N fi

All it $z ^ { \prime }$ ms are $z$ uppose $z \in \{ 0 , 1 \} ^ { N \times M }$ ked".

For $p : = 1$ fi 2 N j i unlocked, De $z ^ { p }$ rmine $z ^ { \prime }$ n Set $\begin{array} { r } { F _ { k } ^ { \prime } : = F _ { k } - \sum _ { i \in N } f _ { i } z _ { i k } ^ { p } } \end{array}$ infcik $k \in M$ l Move item i to knapsack k. While $\{ i \in N \mid i$ p and F0. $z _ { i k } ^ { p } = 0$ and $f _ { i } \leq F _ { k } ^ { \prime }$ for some $k \in M \} \neq \emptyset$ Lock item i (in order to avo $i ^ { * }$ cycling). $k ^ { * }$ with $z _ { i ^ { * } k ^ { * } } ^ { p } = 0$ be the be $c _ { i ^ { * } k ^ { * } } = \operatorname* { m i n } \{ c _ { i k } \ | \ i$ during this p $z _ { i k } ^ { p } = 0$ and $f _ { i } \leq F _ { k } ^ { \prime } \}$ < cTz0, set $i ^ { * }$ 0 := z. $k ^ { * }$ turn z0 $z ^ { p }$ d ST $F ^ { \prime }$ . Lock item $i ^ { * }$ (in order to avoid cycling). Let $z ^ { * }$ be the best solution found during this pass. If $c ^ { T } z ^ { * } < c ^ { T } z ^ { \prime }$ , set $z ^ { \prime } : = z ^ { * }$ Else return $z ^ { \prime }$ and STOP.

Return $z ^ { \prime }$

Finally, let us note that we have embedded our cutting plane algorithms in an enumeration scheme. Here, if we nd no further violated inequality and the current linear pro

to zero, and one where this variable is set to one. The resulting branching tree is worked out in depth rst search manner. current linear programming solution is not integer, we select a variable that is closest to 0.5 and create two subproblems, one where the selected variable is set to zero, and one where this variable is set to one. The resulting branching tree 5 Computational Results

# ba algorithm. We have tested the algori

In this section we report on computational experiences with our cutting plane based algorithm. We have tested the algorithm on multiple knapsack problem com uters. Table 4 summarizes the data. Instances comin from this a lication r r i

items and the total sum of the capacities are shown. computers. Table 4 summarizes the data. (Instances coming from this application are abbreviated by dm in the tables.) Column 2 and 3 give the number of items Problem jNj jMj i2N fi k2M Fk dm1 257 4 83827

hich was already found by the primal he   

<table><tr><td rowspan=1 colspan=1>Problem</td><td rowspan=1 colspan=1>N </td><td rowspan=1 colspan=1>M</td><td rowspan=1 colspan=1>∑iN fi</td><td rowspan=1 colspan=1>∑kM Fk</td></tr><tr><td rowspan=1 colspan=1>dm1</td><td rowspan=1 colspan=1>257</td><td rowspan=1 colspan=1>4</td><td rowspan=1 colspan=1>83827</td><td rowspan=1 colspan=1>132704</td></tr><tr><td rowspan=1 colspan=1>dm2</td><td rowspan=1 colspan=1>772</td><td rowspan=1 colspan=1>6</td><td rowspan=1 colspan=1>284608</td><td rowspan=1 colspan=1>423972</td></tr></table>

Table 5 presents the solutions obtained by our algorithm. Neither individual nor The fact that both problem instances are trivial is not surprising, since the total sum of the knapsack capacities is much bigger than the sum of the weights of the iteration. The CPU Times are in seconds obtained on a Sun Sparc IPX.

The fact that both problem instances are trivial is not surprising, since the total sum of the knapsack capacities is much bigger than the sum of the weights of the usual procedure in practice is to start with some initial capacities of the devices and try to nd a solution that assigns the modules to the devices and connects the nets by wires. If this succeeds, the capacities of the devices are reduced, the whole problem is solved again, and it is continued in this way until no further area reduction is possible. In fact, one of the main goals in the design of main frame computers is to reduce the available amount of space as far as possible. So, from a practical point of view a very interesting question is how far the capacities of the devices can be reduced at most. We followed this question and iteratively reduced the total amount of the knapsack capacities. frame computers is to reduce the available amount of space as far as possible. So, from a practical point of view a very interesting question is how far the capacities Problem Red. Opt. Sol. Ind. ineq. Joint ineq. CPU dm1 36.75% 236250 18

Table 5: Computational results for examples dm.   

<table><tr><td rowspan=1 colspan=1>Problem</td><td rowspan=1 colspan=1>Opt. Sol.</td><td rowspan=1 colspan=1>Ind. Ineq.</td><td rowspan=1 colspan=1>Joint Ineq.</td><td rowspan=1 colspan=1>CPUTime</td></tr><tr><td rowspan=1 colspan=1>dm1</td><td rowspan=1 colspan=1>236250</td><td rowspan=1 colspan=1>0</td><td rowspan=1 colspan=1>0</td><td rowspan=1 colspan=1>1.97</td></tr><tr><td rowspan=1 colspan=1>dm2</td><td rowspan=1 colspan=1>81120</td><td rowspan=1 colspan=1>0</td><td rowspan=1 colspan=1>0</td><td rowspan=1 colspan=1>6.50</td></tr></table>

of 33% in example dm2 leads to infeasibility, since the tota   

<table><tr><td rowspan=1 colspan=1>Problem</td><td rowspan=1 colspan=1>Red.</td><td rowspan=1 colspan=1>Opt. Sol.</td><td rowspan=1 colspan=1>Ind. ineq.</td><td rowspan=1 colspan=1>Joint ineq.</td><td rowspan=1 colspan=1>CPU</td></tr><tr><td rowspan=1 colspan=1>dm1</td><td rowspan=1 colspan=1>36.75%</td><td rowspan=1 colspan=1>236250</td><td rowspan=1 colspan=1>18</td><td rowspan=1 colspan=1>15</td><td rowspan=1 colspan=1>9.72</td></tr><tr><td rowspan=1 colspan=1>dm1</td><td rowspan=1 colspan=1>36.8%</td><td rowspan=1 colspan=1>236250</td><td rowspan=1 colspan=1>18</td><td rowspan=1 colspan=1>15</td><td rowspan=1 colspan=1>9.42</td></tr><tr><td rowspan=1 colspan=1>dm2</td><td rowspan=1 colspan=1>27%</td><td rowspan=1 colspan=1>81134</td><td rowspan=1 colspan=1>23</td><td rowspan=1 colspan=1>40</td><td rowspan=1 colspan=1>10:20.80</td></tr><tr><td rowspan=1 colspan=1>dm2</td><td rowspan=1 colspan=1>28%</td><td rowspan=1 colspan=1>81176</td><td rowspan=1 colspan=1>27</td><td rowspan=1 colspan=1>55</td><td rowspan=1 colspan=1>14:36.73</td></tr><tr><td rowspan=1 colspan=1>dm2</td><td rowspan=1 colspan=1>29%</td><td rowspan=1 colspan=1>81204</td><td rowspan=1 colspan=1>25</td><td rowspan=1 colspan=1>58</td><td rowspan=1 colspan=1>17:21.80</td></tr><tr><td rowspan=1 colspan=1>dm2</td><td rowspan=1 colspan=1>30%</td><td rowspan=1 colspan=1>81302</td><td rowspan=1 colspan=1>33</td><td rowspan=1 colspan=1>15</td><td rowspan=1 colspan=1>41:13.93</td></tr></table>

solution, the number of individual and joint inequ $3 6 . 8 5 \%$ ound by our separation algorithms a $3 3 \%$ he total CPU Time (min:sec). All problem instances in Table 6 are solved to optimality without branching. shows the amount of reduction, columns 3 to 6 present the value of the optimal solution, the number of individual and joint inequalities found by our separation algorithms and the total CPU Time (min:sec). All problem instances in Table 6 are solved to optimality without branching.

Two problems could not be solved to optimality by our algorithm even when branching was applied. Table 7 shows the results for these two examples. The Problem Red. Lower bound Upper bound Gap (%) dm2 31% 81482 81498 0.0196

(Here, the instances are abbre   

<table><tr><td rowspan=1 colspan=1>Problem</td><td rowspan=1 colspan=1>Red.</td><td rowspan=1 colspan=1>Lowerbound</td><td rowspan=1 colspan=1>Upper bound</td><td rowspan=1 colspan=1>Gap (%)</td></tr><tr><td rowspan=1 colspan=1>dm2</td><td rowspan=1 colspan=1>31%</td><td rowspan=1 colspan=1>81482</td><td rowspan=1 colspan=1>81498</td><td rowspan=1 colspan=1>0.0196</td></tr><tr><td rowspan=1 colspan=1>dm2</td><td rowspan=1 colspan=1>32%</td><td rowspan=1 colspan=1>81728</td><td rowspan=1 colspan=1>81736</td><td rowspan=1 colspan=1>0.0097</td></tr></table>

instances in Table 4. One might expect that these instances are more dicult than the examples dm with 0% area reduction. in the tables.) The ratio between the total weight of the items and the total available knapsack capacity is much closer to one than it is the case for the Problem jNj jMj Pi2N fi Pk2M Fk cl1 2292 16 95

hese examples the weights of the items   

<table><tr><td rowspan=1 colspan=1>Problem</td><td rowspan=1 colspan=1>| N |</td><td rowspan=1 colspan=1>| M |</td><td rowspan=1 colspan=1>∑iN fi</td><td rowspan=1 colspan=1>∑kM Fk</td></tr><tr><td rowspan=1 colspan=1>c|1</td><td rowspan=1 colspan=1>2292</td><td rowspan=1 colspan=1>16</td><td rowspan=1 colspan=1>9522</td><td rowspan=1 colspan=1>10000</td></tr><tr><td rowspan=1 colspan=1>cl2</td><td rowspan=1 colspan=1>681</td><td rowspan=1 colspan=1>16</td><td rowspan=1 colspan=1>2571</td><td rowspan=1 colspan=1>2704</td></tr><tr><td rowspan=1 colspan=1>cl3</td><td rowspan=1 colspan=1>2669</td><td rowspan=1 colspan=1>16</td><td rowspan=1 colspan=1>6762</td><td rowspan=1 colspan=1>7104</td></tr><tr><td rowspan=1 colspan=1>cl4</td><td rowspan=1 colspan=1>1021</td><td rowspan=1 colspan=1>16</td><td rowspan=1 colspan=1>4031</td><td rowspan=1 colspan=1>4240</td></tr><tr><td rowspan=1 colspan=1>cl5</td><td rowspan=1 colspan=1>68</td><td rowspan=1 colspan=1>16</td><td rowspan=1 colspan=1>260</td><td rowspan=1 colspan=1>288</td></tr><tr><td rowspan=1 colspan=1>cl6</td><td rowspan=1 colspan=1>6112</td><td rowspan=1 colspan=1>16</td><td rowspan=1 colspan=1>25392</td><td rowspan=1 colspan=1>26672</td></tr></table>

all knapsacks. In all cases for which the value of the rst LP is already equal to the value of the optimal solution our primal heuristics nd an optimal solution in the rst iteration of the algorithm. The only nontrivial example is cl2, where indeed individual and joint inequalities were necessary to nd the optimal solution. In Table 9 we show the value of an optimal solution, the number of individual and joint inequalities found by our separation algorithms and the total CPU Time first iteration of the algorithm. The only nontrivial example is cl2, where indeed individual and joint inequalities were necessary to find the optimal solution. In Table 9 we show the value of an optimal solution, the number of individual and joint inequalities found by our separation algorithms and the total CPU Time (min:sec).

Table 9: Solutions of the examples cl.   

<table><tr><td rowspan=1 colspan=1>Problem</td><td rowspan=1 colspan=1>Opt. Solution</td><td rowspan=1 colspan=1>Ind. ineq.</td><td rowspan=1 colspan=1>Joint ineq.</td><td rowspan=1 colspan=1>CPU Time</td></tr><tr><td rowspan=1 colspan=1>cl1</td><td rowspan=1 colspan=1>2292</td><td rowspan=1 colspan=1>0</td><td rowspan=1 colspan=1>0</td><td rowspan=1 colspan=1>3:56.30</td></tr><tr><td rowspan=1 colspan=1>cl2</td><td rowspan=1 colspan=1>939.99</td><td rowspan=1 colspan=1>145</td><td rowspan=1 colspan=1>60</td><td rowspan=1 colspan=1>23:52.40</td></tr><tr><td rowspan=1 colspan=1>cl3</td><td rowspan=1 colspan=1>2669</td><td rowspan=1 colspan=1>0</td><td rowspan=1 colspan=1>0</td><td rowspan=1 colspan=1>3:25.18</td></tr><tr><td rowspan=1 colspan=1>cl4</td><td rowspan=1 colspan=1>1021</td><td rowspan=1 colspan=1>0</td><td rowspan=1 colspan=1>0</td><td rowspan=1 colspan=1>4:16.65</td></tr><tr><td rowspan=1 colspan=1>cl5</td><td rowspan=1 colspan=1>472</td><td rowspan=1 colspan=1>0</td><td rowspan=1 colspan=1>0</td><td rowspan=1 colspan=1>1.80</td></tr><tr><td rowspan=1 colspan=1>cl6</td><td rowspan=1 colspan=1>6112</td><td rowspan=1 colspan=1>0</td><td rowspan=1 colspan=1>0</td><td rowspan=1 colspan=1>27:03.75</td></tr></table>

available knapsack capacity. Even here, we solve all reduced examples, except the reduced instances of cl2, in the rst iteration, a very astonishing fact. The reduced instances of cl2 are much more dicult. In all but one example the rst lower bound does not give the optimal objective function value. To solve these problems to optimality not only individual inequalities but also joint inequalities were necessary. Table 10 presents the results. (Note that a reduction of 5 % leads to infeasibility, since in this case the total sum of the knapsack capacities is less than the total weight of the items.) problems to optimality not only individual inequalities but also joint inequalities were necessary. Table 10 presents the results. (Note that a reduction of $5 \%$ leads Problem Red. Opt. Sol. Ind. ineq. Joint ineq. CPU Time cl2 1% 946.99

close to the value of the optimal solution. The re   

<table><tr><td rowspan=1 colspan=1>Problem</td><td rowspan=1 colspan=1>Red.</td><td rowspan=1 colspan=1>Opt. Sol.</td><td rowspan=1 colspan=1>Ind. ineq.</td><td rowspan=1 colspan=1>Joint ineq.</td><td rowspan=1 colspan=1>CPU Time</td></tr><tr><td rowspan=1 colspan=1>cl2</td><td rowspan=1 colspan=1>1%</td><td rowspan=1 colspan=1>946.99</td><td rowspan=1 colspan=1>318</td><td rowspan=1 colspan=1>143</td><td rowspan=1 colspan=1>21:12.10</td></tr><tr><td rowspan=1 colspan=1>c|2</td><td rowspan=1 colspan=1>2%</td><td rowspan=1 colspan=1>946.99</td><td rowspan=1 colspan=1>126</td><td rowspan=1 colspan=1>135</td><td rowspan=1 colspan=1>22:12.25</td></tr><tr><td rowspan=1 colspan=1>c|2</td><td rowspan=1 colspan=1>3%</td><td rowspan=1 colspan=1>960.99</td><td rowspan=1 colspan=1>162</td><td rowspan=1 colspan=1>146</td><td rowspan=1 colspan=1>22:56.90</td></tr><tr><td rowspan=1 colspan=1>cl2</td><td rowspan=1 colspan=1>4%</td><td rowspan=1 colspan=1>967.99</td><td rowspan=1 colspan=1>196</td><td rowspan=1 colspan=1>185</td><td rowspan=1 colspan=1>16:06.03</td></tr></table>

after the rst iteration is larger by far. Only when individual and especially when joint inequalities are added the linear programming solution provides structural information such that $i \in N$ rimal heuristics nd good upper bo $c _ { i k }$ ds $k \in M$ n an similar. However, the gap between the first lower bound and the upper bound after the first iteration is larger by far. Only when individual and especially when joint inequalities are added the linear programming solution provides structural information such that the primal heuristics find good upper bounds or even an after rst LP after ind. ineq. after joint ineq.

and the number of knapsacks.   

<table><tr><td rowspan=1 colspan=1>|N|</td><td rowspan=1 colspan=1>| M |</td><td rowspan=1 colspan=1>Average gapafter first LP</td><td rowspan=1 colspan=1>Average gapafter ind. ineq.</td><td rowspan=1 colspan=1>Average gapafter joint ineq.</td></tr><tr><td rowspan=1 colspan=1>50</td><td rowspan=1 colspan=1>4</td><td rowspan=1 colspan=1>561.0</td><td rowspan=1 colspan=1>231.4 (41.2%)</td><td rowspan=1 colspan=1>36.6   (6.5%)</td></tr><tr><td rowspan=1 colspan=1>100</td><td rowspan=1 colspan=1>4</td><td rowspan=1 colspan=1>265.4</td><td rowspan=1 colspan=1>164.0  (61.8%)</td><td rowspan=1 colspan=1>78.6  (29.6%)</td></tr><tr><td rowspan=1 colspan=1>150</td><td rowspan=1 colspan=1>4</td><td rowspan=1 colspan=1>355.2</td><td rowspan=1 colspan=1>149.2  (42.0%)</td><td rowspan=1 colspan=1>114.2  (32.3%)</td></tr><tr><td rowspan=1 colspan=1>200</td><td rowspan=1 colspan=1>4</td><td rowspan=1 colspan=1>335.4</td><td rowspan=1 colspan=1>117.0  (34.9%)</td><td rowspan=1 colspan=1>75.2  (22.4%)</td></tr><tr><td rowspan=1 colspan=1>300</td><td rowspan=1 colspan=1>4</td><td rowspan=1 colspan=1>332.0</td><td rowspan=1 colspan=1>112.4  (33.9%)</td><td rowspan=1 colspan=1>100.6  (30.3%)</td></tr><tr><td rowspan=1 colspan=1>400</td><td rowspan=1 colspan=1>4</td><td rowspan=1 colspan=1>210.5</td><td rowspan=1 colspan=1>154.8  (73.5%)</td><td rowspan=1 colspan=1>90.0  (42.8%)</td></tr><tr><td rowspan=1 colspan=1>500</td><td rowspan=1 colspan=1>4</td><td rowspan=1 colspan=1>171.0</td><td rowspan=1 colspan=1>41.5  (24.3%)</td><td rowspan=1 colspan=1>38.2  (22.4%)</td></tr></table>

domly computed such that Pk M Fk   Pi N fi, where  is a random number chosen from [1:05; 1:3]. We have created four dierent problems with the same number of knapsacks and items. The numbers in column 3 to 5 show the average over the absolute values of the gaps between the upper bounds and the lower bounds after the rst itera $\begin{array} { r } { \sum _ { k \in M } F _ { k } \le \alpha \sum _ { i \in N } f _ { i } } \end{array}$ violated $\alpha$ ndividual inequalities were found, and after no further violated joint inequalities were found. The number in brackets give the percentual improvement of the gap. Although we cannot solve most of these random examples to optimality without branching, the results conrm that the gap between the lower and an upper bound is substantially decreased by using individual and joint inequalities. ber in brackets give the percentual improvement of the gap. Although we cannot solve most of these random examples to optimality without branching, the results confirm that the gap between the lower and an upper bound is substantially 6 Conclusions

# kn sack problem. In pa

layout of electronic circuits. Almost all practical examples are solved to optimality without branching. These results conrm the practical use of the inequalities presented in [FMW93] and indicate that the separation procedures perform quite on problem instances arising in the design of main frame computers and in the layout of electronic circuits. Almost all practical examples are solved to optimality without branching. These results confirm the practical use of the inequalities presented in [FMW93] and indicate that the separation procedures perform quite well. This impression is also supported by applying our cutting plane algorithm References

# References

[B75] act Knapsack Separation", Networks 22, 503 - 514 (1992). ming 8, 146 - 164 (1975).   
[B091] brary, CPLEX Optimization (1992). act Knapsack Separation", Networks 22, 503 - 514 (1992).   
Zero-One Linear Programming Problems", Operations Research 31, 803 - 844 (1983).   
[FGKK W93] C. E. Ferreira, M. Grotschel, S. Kie, C. Krispenz, A. Martin and R. Weismantel, \Some Integer Programs Arising in the Design of Main Frame Com   
[FM82] C. M. Fiduccia, R. M. Mattheyses, \A Linear-Time Heuristic for Improving Network Partitions", Proc. 19th. DAC, 175 - 181 (1982). Main Frame Computers", appears in ZOR 37 (1993).   
[FM82] Knapsack Polytope", Konrad-Zuse-Zentrum fur Informationstechnik Berlin Preprint SC 93-04 (1993).   
[GR90] E. S. Gottlieb e M. R. Rao, \The Generalized Assignment Problem: Valid Inequalities and Facets", Mathematical Programming 46, 31 - 52 (1990).   
[HJP75] P. L. Hammer, E. L. Johnson and U. N. Peled, \Facets of Regular 0-1 Polytopes", Mathematical Programming 8, 179 - 206 (1975). (1990).   
[HJP75] Knapsack and Sum of Subset Problems", Journal of ACM 22, 463 - 468 (1975).   
[K72] R. M. Karp, \Reducibility among Combinatorial Problems", in R. E. Miller and J. W. Thatcher (eds.), Complexity of Computer computations, Plenu   
[K72] R. M. Karp, "Reducibility among Combinatorial Problems", in R. E. Miller and J. W. Thatcher (eds.), Complexity of Computer computations, Plenum Press, New York, 85 - 103 (1972).   
[MT91] 23, 833 - 837 (1975). puter Implementations, John Wiley and Sons, New York (1991).   
[P75] lems", Mathematical Programming 18, 94 - 99 (1980). 23, 833 - 837 (1975).   
[P80] matical Programming 8, 165 - 178 (1975). lems", Mathematical Programming 18, 94 - 99 (1980).   
[W75] Generalised Upper Bound Constraints", Discrete Applied Mathematics 29, 251 - 261 (1990).   
[Z86] E. Zemel, \On the Computational Complexity of Facets for the Knapsack Problem", Working Paper 713, The Center for Mathematical Studies in Economic   
[Z86] E. Zemel, "On the Computational Complexity of Facets for the Knapsack Problem", Working Paper 713, The Center for Mathematical Studies in Economics and Management Sciences, Northwestern University (1986).