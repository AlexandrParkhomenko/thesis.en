# quadratic assignment problem. We focus our attention on recent developand Recent Developments

1. Introduction dratic assignment problem (QAP) can be stated as follows: diverse areas such as operations research, parallel and distributed computing, and combinatorial data analysis. In this paper we survey some of p2N j p( )p(j) p( ) quadratic assignment problem. We focus our attention on recent developis t

# 1. Introduction

2, 67, 137]. $\mathcal { N } = \{ 1 , 2 , \dots , n \}$ tane $n \times n$ assigning $\begin{array} { r } { F = \left( f _ { i j } \right) } \end{array}$ o loca $D = \left( d _ { k l } \right)$ d facility j to location l is fijdkl. The objective is to nd an assig

$$
\operatorname* { m i n } _ { p \in \Pi _ { N } } \sum _ { i = 1 } ^ { n } \sum _ { j = 1 } ^ { n } f _ { i j } d _ { p ( i ) p ( j ) } + \sum _ { i = 1 } ^ { n } c _ { i p ( i ) } ,
$$

In a $\Pi _ { \mathcal { N } }$ tion to its application in facility l $\mathcal { N }$ ation problems, the QAP has been found useful in such applications as scheduling [8 $\begin{array} { r } { F = \left( f _ { i j } \right) } \end{array}$ kboard wiring problem $f _ { i j }$ electronics [240], parallel and distrib $_ i$ ed compu $j$ g [24 $D = \left( d _ { k l } \right)$ tistical data analysis [118]. O $d _ { k l }$ r applications may be found in [77, 13 $k$ , 159]. $l$ The term "quadratic" comes from the reformulation of $_ i$ he problem $k$ s an optimiz $j$ tion problem $l$ wit $f _ { i j } d _ { k l }$ uadratic objective function. There is a one-toone correspondence between N and the $p \in \Pi _ { \mathcal { N } } .$ - n permutation matrices the assignment is minimized. Throughout this paper we often refer to the QAP orion.uwaterloo.ca in the director ub henr

1991 Mathematics Subject Classication. Primary 90B80, 90C20, 90C35, 90C27; Secondary found useful in such applications as scheduling [88], the backboard wiring probartitionin surve exact al orithms heuristics al orithms test roblems biblio ra h . data analysis [118]. Other applications may be found in [77, 138, 159].

c 0000 American Mathematical Society0000-0000/00 \$1.00 + \$.25 per page optimization problem with a quadratic objective function. There is a one-toone correspondence between $\Pi _ { \mathcal { N } }$ and the set of $n \times n$ permutation matrices $\boldsymbol { X } = \left( \boldsymbol { x } _ { i j } \right) _ { n \times n }$ x 2 f0; 1g; i = 1; : : : ; n; j = 1; : : : ; n;

$$
\sum _ { j = 1 } ^ { n } x _ { i j } = 1 , \ i = 1 , \dots , n ,
$$

$$
\sum _ { i = 1 } ^ { n } x _ { i j } = 1 , \ j = 1 , \ldots , n ,
$$

$$
x _ { i j } \in \{ 0 , 1 \} , \ i = 1 , \dots , n , \ j = 1 , \dots , n ,
$$

$$
\begin{array} { r } { x _ { i j } = \left\{ \begin{array} { l l } { 1 } & { \mathrm { i f ~ f a c i l i t y ~ } i \mathrm { ~ i s ~ a s s i g n e d ~ t o ~ l o ~ l o c a t i o n ~ } j } \\ { 0 } & { \mathrm { o t h e r w i s e } . } \end{array} \right. } \end{array}
$$

With the above constraints on $\pmb { x }$ , we have the following equivalent formulation for the quadratic assignment problem, working on the space of permutation matrices,

$$
\operatorname* { m i n } \ \sum _ { i = 1 } ^ { n } \sum _ { j = 1 } ^ { n } \sum _ { k = 1 } ^ { n } \sum _ { l = 1 } ^ { n } a _ { i j } b _ { k l } x _ { i k } x _ { j l } + \sum _ { i , j = 1 } ^ { n } c _ { i j } x _ { i j } .
$$

timal permutation is discussed in Section 6. Concluding remarks are made in cal tools and techniques that have proven to be useful for QAP. This includes various formulations of the problem and representations of the feasible set. The 2. Mathematics of QAP tractable relaxations. We include optimality conditions and representations of derivatives for QAP and its relaxations. In Section 3, we present several applications of QAP, both theoretical and practical. We also include generalizations. 2.1. Formulations. Several formulations have been used in the literature to study the QAP. We outline several of these formulations now. (Please see [100] for more details and more formulations.) Section 7.

# 2. Mathematics of QAP

tivities to a set of locations. useful and interesting for QAP.

2.1. Formulations. Several formulations have been used in the literature to study the QAP. We outline several of these formulations now. (Please see [100] for more details and more formulations.)

2.1.1. Koopmans-Beckmann. The QAP was introduced in 1957 by Koopmans and Beckmann [137] using the formulation presented above in equations (1.1) to (1.4). This model was formulated to study the assignment of a set of economic activities to a set of locations.

Several elementary properties of the trace can be exploited. For example:

ct satis

$$
\begin{array} { r } { \operatorname* { m i n } _ { X \in \Pi } f ( X ) = \mathfrak { t } r a c e \left( A X B + C \right) X ^ { t } , } \end{array}
$$

where .t denotes transpose, $\Pi$ is the set of permutation matrices, and trace hM; Ni = trace M N; $A$ and $B$ to be real symmetric $n \times n$ matrices and $C \in \mathfrak { R } ^ { n \times n }$ . This formulation was introduced in where  stands for complex conjugate. 2.1.3. Kron $\pmb { n }$ ker Product. The trace formulation

compact form of representing the quadratic form with the matrix X as the variable. The Hessian of this uadratic form is the tensor roduct or Kronecker product $M N = \mathrm { t } r a c e N M = \mathrm { t } r a c e N ^ { t } M ^ { t }$ . Moreover, the trace provides a valid inner product on the space of real (or complex) $m \times n$ matrices

$$
\langle M , N \rangle = \mathrm { t } r a c e M ^ { * } N ,
$$

where ·\* stands for complex conjugate.

2.1.3. Kronecker Product. The trace formulation of the objective function is f(X) = vec (X) (A 
 B)vec (X) + vec (C) vec (X): $X$ as the variable. The Hessian of this quadratic form is the tensor product or Kronecker product

$$
A \otimes B = ( a _ { i j } b _ { k l } ) = ( a _ { i j } B ) ,
$$

using the Kronecker product hides the structure of the problem and $A$ ncrea $B$ s the complexity in that we do $\mathsf { v e c } \left( X \right) \in \mathfrak { N } ^ { n ^ { 2 } }$ ntage of the hidden fact that we are really working on an $X$ dimensional problem. For that reason, the K

$$
f ( X ) = \mathsf { v e c } ( X ) ^ { t } ( A \otimes B ) \mathsf { v e c } ( X ) + \mathsf { v e c } ( C ) ^ { t } \mathsf { v e c } ( X ) .
$$

Derivatives and algebraic manipulations can all be done via the Kronecker product. For example, the eigenvalues of the Kronecker product are the $n ^ { 2 }$ eigenvalp , , p p f g p y pn2 $A$ ( $B$ . However, ( ij ) ( ) ( )) the complexity in that we do not take advantage of the hidden fact that we are really working on an $\pmb { n }$ dimensional problem. For that reason, the Kronecker product is rarely used and we do not study it further. (See [96] for details on manipulations and calculus involving Kronecker products.)

2.2. The Feasible Set and Perturbations. The feasible set for QAP consists of all the possible assignments of $\pmb { n }$ objects to $\pmb { n }$ locations. The extreme points, or vertices, of the bipartite perfect matching polytope (as defined by the nonnegative vectors $x = ( x _ { i j } ) \in \Re ^ { n ^ { 2 } }$ satisfying the constraints (1.1) and (1.2)) are the incidence vectors of all possible assignments. Alternatively, in the trace formulation, the feasible set consists of all the permutation matrices. It is well the permutation matrices is the set of doubl

$$
\begin{array} { r l r } { \Pi } & { = } & { \mathcal { O } \cap \mathcal { E } \cap \mathcal { N } , } \\ & { = } & { \mathcal { S } \cap \mathcal { E } \cap \mathcal { N } , } \end{array}
$$

function $\mathcal { O } \ = \ \{ X \ : \ X ^ { t } X \ = \ I \}$ ptimal solution of the original prob ${ \mathcal { S } } \ = \ \{ X \ :$ pertu $X ^ { t } X ~ = ~ n \}$ chang $\mathcal { E } = \{ X : X u = X ^ { t } u = u \}$ and so are important in improving bounding techniques. Two standard p $\mathcal { N } = \{ X : X \ge 0 \}$ nt row and column perturbations and diago $\mathcal { D } = \mathcal { E } \cap \mathcal { N }$ tions, are known to have this property. Specically, suppose that e; f; r; s 2 <n and dene the permutation matrices is the set of doubly stochastic matrices, conv $\Pi = \mathcal { D }$ Thus the set of doubly stochastic matrices corresponds to the bipartite perfect B(f; s) = B + fut + uft + diag (s);

The properties of the feasible set allow for perturbations of the objective function without changing the optimal solution of the original problem. These perturbations do change relaxations for the problem and so are important in where diag changes a vector to a diagonal matrix and, conversely, it changes a column perturbations and diagonal perturbations, are known to have this proptrace AXB + C Xt = trac $e , f , r , s \in \Re ^ { n }$ f; s + C e;

$$
A ( e , r ) = A + e u ^ { t } + u e ^ { t } + \mathrm { d } i a g \left( r \right) ,
$$

$$
B ( f , s ) = B + f u ^ { t } + u f ^ { t } + \mathrm { d } i a g \left( s \right) ,
$$

$$
\begin{array} { r c l } { { C ( e , f , r , s ) } } & { { = } } & { { C + 2 A u f ^ { t } + 2 e u ^ { t } B - 2 n e f ^ { t } - 2 \sum _ { k } e _ { k } u f ^ { t } } } \\ { { } } & { { } } & { { + \mathrm { d } i a g ( A ) s ^ { t } + r \mathrm { d } i a g ( B ) ^ { t } - 2 e s ^ { t } - 2 r f ^ { t } - r s ^ { t } , } } \end{array}
$$

is discussed in [198].) matrix to a vector formed from the diagonal elements. Then

$$
\bigl ( A X B + C \bigr ) X ^ { t } = \operatorname { t } r a c e \big ( A \bigl ( e , r \bigr ) X B \bigl ( f , s \bigr ) + C \bigl ( e , f , r , s \bigr ) \bigr ) X ^ { t } , \ \forall X \in  { \mathbb { I } } .
$$

(Note that symmetry is preserved by these transformations.)

If we keep the constraint $X \in \mathcal { E }$ , i.e. $X$ has row and column sums equal to 1, then the constant row and column perturbations are redundant and can be ignored, i.e. only the diagonal perturbations need be used. (See e.g. [102] for details. The question of which perturbations are needed, under which relaxations, is discussed in [198].)

2.3. Relaxations. Since QAP is an NP-hard problem, the equivalent expression of the constraints in (2.1) are very useful. We immediately get representations for relaxations. These relaxations remove the combinatorial nature of the problem and allow for solutions using continuous optimization techniques. The strategy is to relax the objective function and/or the constraints, in order to get a tractable problem. These problems do not provide useful approximations in general. But, we can then find the best relaxation of a family of these problems over the above mentioned perturbations. (More details are provided when we discuss lower bounds in Section 5.2.)

2.3.1. Linearization. If the quadratic term of QAP vanishes, then we have an ordinary linear assignment problem which can be solved very efficiently. In general, the QAP can be relaxed to a (0,1)-linear integer program. This can be done by introducing new binary variables $y _ { i j k l } = x _ { i j } x _ { k l }$ . These new variables replace the occurrence of quadratic terms in the objective function. New constraints are added to ensure consistency with the original problem. Typically, the convex hull of the constraint set is used in order to obtain an ordinary linear programming problem. See e.g. [143, 155, 154, 132, 8, 18, 55, 34, 81, 2, 100].

an of the feasible set, i.e. on the span of the doubly stochastic matrices, or equivalently, on the span of matrices with row and column sums equal to 1. However, this relaxation does not fully exploit the structure of the problem, since it treats the objective function as a quadratic form over <n : $A$ and $B$ in order to make the Hessian of the objective function convex. We can then take the convex hull of the feasible set, i.e. we relax the feasible set to the doubly stochastic matrices $\mathcal { D }$ . This results in a standard quadratic programming problem that can be solved by well known methods. In fact, we do not need to make the Hessian positive semidefinite on all matrices $X$ , but rather only on the span of the feasible set, i.e. on the span of the doubly stochastic matrices, or equivalently, on the span of matrices with row and column sums equal to 1.

2.3.4. Parametrization of Permutation and Orthogonal Groups. The vector e of ones is both a right and left eigenvector corresponding to an eig

2.3.3. Trust Region Subproblems. If we use the second representation in (2.1) and relax the constraint set to $X \in \mathcal { S } \cap \mathcal { E }$ , then we do not have to worry about convexity of the objective function, i.e. we obtain a tractable problem called a trust region subproblem. (In [241] it is shown that these problems are really Vte = 0; V tV = I : problems.) However, these problems still do not exploit the structure of QAP.

2.3.4. Parametrization of Permutation and Orthogonal Groups. The vector e of ones is both a right and left eigenvector corresponding to an eigenvalue of 1, v := e ; P = [v . V] 2 O: set of QAP onto the span of the doubly stochastic matrices while not losing the special trace structure of the objective function.

rametriz $\pmb { n } \times \left( \pmb { n } - 1 \right)$ permut $V$ on matrices f

$$
V ^ { t } e = 0 ; V ^ { t } V = I _ { n - 1 } .
$$

The columns of $V$ therefore constitute an orthonormal basis of $\{ e \} ^ { - }$ . Further, let

$$
v : = \frac { e } { \lVert e \rVert } ; P = [ v : V ] \in \mathcal { O } .
$$

Thus $Q : = V V ^ { t } = I - v v ^ { t }$ describes the orthogonal projection on $\{ e \} ^ { - }$ . The parametrization of the permutation matrices follows. (See [102].)

PROPOSITION 2.1. Let $X$ 2 N $n \times n$ VY $Y$ t  $( n - 1 ) \times ( n - 1 )$ . Suppose that X and Y satisfy

$$
\boldsymbol { X } = \boldsymbol { P } \left[ \begin{array} { l l } { 1 } & { 0 } \\ { 0 } & { \boldsymbol { Y } } \end{array} \right] \boldsymbol { P ^ { t } } .
$$

Then

$$
X \in { \mathcal { E } } ,
$$

$$
X \in \mathcal { N } \iff V Y V ^ { t } \geq - v v ^ { t } ,
$$

$$
X \in \mathcal { O } _ { n } \iff Y \in \mathcal { O } _ { n - 1 } .
$$

matrix S, see $X \in { \mathcal { E } }$ 72, 60]. This re $Y$ ts in an unconstrained

Relaxing the constraints to $X \in \mathcal { O }$ or to $X \in \mathcal { O } \cap \mathcal { E }$ removes the combinatorial nature of the problem. The resulting problem can be split into an eigenvalue problem for the quadratic part of the objective function and a standard linear programming problem for the linear part. (This is discussed in detail in the 2.4. Derivatives and Optima

m. It is therefore not surprising that verifying optimality is $X \in \mathcal { O }$ n NP-hard problem. In fact, even checking local optima $X = \exp ^ { S }$ rd problem. See Section 4.2.) H $S$ wever there are tractable optimality conditions for the relaxations. space of skew symmetric matrices.

2.3.5. Semidefinite Programming. The orthogonal constraint can be relaxed to $X X ^ { t } \preceq I$ , i.e. $X X ^ { t }$ is negative semidefinite. This relaxation is discussed in k(X) = XBXt; g(X) = XtX   I; f(X) = trace

2.4. Derivatives and Optimality Conditions. QAP is an NP-hard problem. It is therefore not surprising that verifying optimality is also an NP-hard dk X h = X B h t hB X t 4.2.) However there are tractable optimality conditions for the relaxations.

df(X; h) = trace A(dk(X; h)) = trace A(XBht + hBXt): in QAP. Let

$$
k ( X ) = X B X ^ { t } , g ( X ) = X ^ { t } X - I , f ( X ) = \mathfrak { t r a c e } A X B X ^ { t } .
$$

Then the corresponding differentials in the (matrix) direction $h$ are

$$
\begin{array} { r c l } { d k \big ( X ; h \big ) } & { = } & { X B h ^ { t } + h B X ^ { t } ; } \\ { d g \big ( X ; h \big ) } & { = } & { X h ^ { t } + h ^ { t } X ; } \\ { d f \big ( X ; h \big ) } & { = } & { \mathsf { t r a c e \ } A \big ( d k \big ( X ; h \big ) \big ) = \mathsf { t r a c e \ } A \big ( X B h ^ { t } + h B X ^ { t } \big ) . } \end{array}
$$

a ran ian usin the above dierentials. If we set the derivative to 0 we et the $C = 0$ on that AXB XS = 0 or XtAXB =  S: We conclude from S = St that XtAX and B commute and

$$
\operatorname* { m i n } f ( X ) { \mathrm { ~ s u b j e c t ~ t o ~ } } g ( X ) = 0 .
$$

the span of the doubly stochastic

$$
f ( X ) + { \mathfrak { t } } r a c e S g ( X ) ,
$$

where the Lagrange multiplier $S$ is a symmetric matrix. We can differentiate the Lagrangian using the above differentials. If we set the derivative to 0, we get the condition that $A X B + X S = 0$ or $X ^ { t } A X B = - S$ . We conclude from $S = S ^ { t }$ , that $X ^ { t } A X$ and $B$ commute and so are mutually diagonalizable. This yields the minimum scalar product of the eigenvalues used in the bounds in Theorem 5.1. An improved bound can be obtained by projecting the feasible set onto min max trace -(AXB + C)Xt + t (Xe   e) + t (Xt(2.3) e   e); permutation matrices, see 2.3.4. (More details can be found in [210, 102, 129].)

hile the dual is the max-min problem max min trace -(AXB + C)Xt + t (Xe   e) + t (Xt(2.4) e   e $\mathcal { D }$ while perturbing the objective function to make it convex on the span of $\mathcal { D }$ , then the The above relaxation provides lower bounds for QAP. Thus, for each perturbation dened in Section 2.2, with the above convexity assumption on the span of D, the dual problem provides lower bounds for QAP because we can eectiv

$$
\operatorname* { m i n } _ { X \in \mathcal { N } } \operatorname* { m a x } _ { \lambda _ { 1 } , \lambda _ { 2 } \in \mathfrak { R } ^ { n } } { \mathfrak { t } } r a c e \ \big [ ( A X B + C ) X ^ { t } \big ] + \lambda _ { 1 } ^ { t } \big ( X e - e \big ) + \lambda _ { 2 } ^ { t } \big ( X ^ { t } e - e \big ) ,
$$

while the dual is the max-min problem

$$
\operatorname* { m a x } _ { \lambda _ { 1 } , \lambda _ { 2 } \in \mathfrak { R } ^ { n } } \operatorname* { m i n } _ { X \in \mathcal { N } } \mathfrak { t r a c e } \ \big [ ( A X B + C ) X ^ { t } \big ] + \lambda _ { 1 } ^ { t } \big ( X e - e \big ) + \lambda _ { 2 } ^ { t } \big ( X ^ { t } e - e \big ) .
$$

The above relaxation provides lower bounds for $\mathrm { Q A P }$ . Thus, for each perturbation defined in Section 2.2, with the above convexity assumption on the span of $\mathcal { D }$ , the dual problem provides lower bounds for QAP because we can effectively characterize global optimality for it. This is no longer true if we do not make the convexity assumptions on the objective function.

Statements about global optimality for nonconvex problems, such as QAP itself, are much harder to make. A characterization for general problems can be found in [114].

2.4.4. Local Optimality. For the general quadratic programming relaxation, even in the nonconvex case, i.e. for a general objective function constrained to D, we still get necessary and sufficient local optimality conditions. This is due to the quadratic nature of the problem, i.e. the second order optimality conditions are necessary and sufficient. However, this is not the case for problems with nonnegativity constraints. It has been shown in [191] that the problem of checking local optimality (and the problem of checking if a local minimum is strict) in quadratic programming with linear constraints is NP-hard. Pardalos and Vavasis [192] have also shown that quadratic programming with one negative eigenvalue (all others zero) remains an NP-hard problem.

3. Applications, Generalizations and special cases ric matrices $A , B$ . If one of $A$ or $B$ is symmetric, then we can still get an equivalent symmetric $\mathrm { Q A P }$ by symmetrizing the other, e.g. replace $B$ by $\left( B + B ^ { t } \right) / 2$ If both $A$ and $B$ are not symmetric, then we can still symmetrize the quadratic form by using the Kronecker product, but we then lose the trace structure of the problem.

However, even if both $A$ and $B$ are not symmetric, we can still obtain mean3.1. The 3-index Assignment Problem. The three-index (or 3-dime

# 3. Applications, Generalizations and special cases

Applications for QAP are many and varied. Several are mentioned in the introduction above. We also point out that [33] summarizes recently published applications of quadratic assignment problem.

We will describe now first some generalizations of the quadratic assignment problem, and then discuss some interesting special cases.

3.1. The 3-index Assignment Problem. The three-index (or 3-dimensional) assignment problem of order $\pmb { n }$ can be stated as a (0,1)-programming problem of the following form:

$$
\begin{array} { r l r } { \operatorname* { m i n } } & { \textstyle \sum \{ c _ { i j k } x _ { i j k } : i \in I , j \in J , k \in K \} , } & \\ { \mathrm { s . } t . } & { \textstyle \sum \{ x _ { i j k } : j \in J , k \in K \} = 1 , \ \forall i \in I , } & \\ & { \textstyle \sum \{ x _ { i j k } : i \in I , k \in K \} = 1 , \ \forall j \in J , } & \\ & { \textstyle \sum \{ x _ { i j k } : i \in I , j \in J \} = 1 , \ \forall k \in K , } & \\ & { \textstyle \qquad x _ { i j k } \in \{ 0 , 1 \} , \ \forall i , j , k , } & \end{array}
$$

by Fro $I , ~ J$ [83] $K$ nd discussed by Burkard and $| I | = | J | = | K | = n$ see Burkard and Rudolf [42]. More recently, Balas and Saltzman [11] developed a bran $\pmb { n }$ an $n ^ { 3 }$ b

shion with subgradient optimization. assignment problem is NP-hard [131]. Most ot the proposed algorithms for this problem are implicit enumeration methods. Some of the proposed algorithms include those of Vlach [247], Pierskalla [196, 197] and Leue [145]; a primaldual algorithm described by Hansen and Kaufman [106]; a branch and bound algorithm using a Lagrangian dual and subgradient optimization implemented by Fröhlich [83] and discussed by Burkard and Fröhlich [38]. Also see Burkard and Rudolf [42]. More recently, Balas and Saltzman [11] developed a branch and bound algorithm that also uses facet-defining inequalities in a Lagrangian fashion with subgradient optimization.

Let $A$ P = conv x 0 1 n3 : x P $R =$ $I \cup J \cup K$ is the row index set of $A$ . Let $S$ be the column index set of $A$ . Let $G _ { A }$ be the intersection graph of $A$ , i.e., the graph that has a vertex for every column of $A$ and an edge for every pair of non-orthogonal columns. Let

$$
P = \{ x \in R ^ { n ^ { 3 } } : A x = e , x \geq 0 \} ,
$$

for a f $e = ( 1 , . . . , 1 ) ^ { t } \in R ^ { 3 n }$ inear-ti

$$
P _ { I } = { \mathsf { c o n v } } \{ { \pmb x } \in \{ 0 , 1 \} ^ { n ^ { 3 } } : x \in P \}
$$

Other papers on the three-index assignment p $\pmb { n }$ o

Balas and Saltzman [10] started to study the facial structure of $P _ { I }$ . They gave an $O ( n ^ { 4 } )$ procedure to detect whether there is a clique facet of $P _ { I }$ , violated by a given noninteger point $\pmb { x }$ . In [1], Balas and Qi gave an $O ( n ^ { 3 } )$ procedure to do signment problem (QSA) unies some inter $n ^ { 3 }$ ing $O ( n ^ { 3 } )$ natorial optimization for a facet class of $P _ { I }$ is linear-time and its complexity is best possible. Balas and Qi [9], Gwan and Qi [99] also gave linear-time separation algorithms for other two facet classes of $P _ { I }$ k=1 i=1 j=1 cijxikxjk (3.2)

xjk 2 f0; 1g; 8j; k; and [219].

ion problem, and the m-coloring problem on graphs [234], [235]. Given n objects and an n - n dissimilarity matrix C = (cij), the \clustering problem" is to nd a partition of the object

$$
\begin{array} { r l } { \operatorname* { m i n } } & { \sum _ { k = 1 } ^ { m } \sum _ { i = 1 } ^ { n } \sum _ { j = 1 } ^ { n } c _ { i j } x _ { i k } x _ { j k } } \\ { \mathrm { s . } t . } & { \sum _ { k = 1 } ^ { m } x _ { j k } = 1 , \ j = 1 , . . . , n } \\ & { \quad { x _ { j k } } \in \{ 0 , 1 \} , \quad \forall j , k , } \end{array}
$$

semiassignment problem with cij = wiwj for all i and j. The \m-coloring problem" is also a special case of the (QSA) pro

graph $\pmb { n }$ (V; A), the grap $n \times n$ mits a coloration of $C = \left( c _ { i j } \right)$ s with m colors problem" is to find a partition of the objects into $_ m$ classes (clusters) which minimizes the sum of the dissimilarities between objects belonging to the same class.

The "equipartition problem" is the following: Given $\pmb { n }$ objects with weights ${ \boldsymbol { w } } _ { i }$ $i = 1 , \ldots , n$ , find a partition of the objects into $_ m$ classes so as to minimize the variance of the class weights. This problem can be formulated as a quadratic semiassignment problem with $c _ { i j } = { w _ { i } w _ { j } }$ for all $_ i$ and $j$ -

The $^ { 6 6 } \mathrm { m }$ -coloring problem" is also a special case of the (QSA) problem. Given a graph $G ( V , A )$ , the graph admits a coloration of its vertices with $_ m$ colors ization of the quadratic assignment problem. Let A = (ai;j;k;l) and B = (bm;p

$$
\begin{array} { c c } { \operatorname* { m i n } } & { \quad \sum _ { k = 1 } ^ { m } \sum _ { ( i , j ) \in A } x _ { i k } x _ { j k } } \\ & { \quad \sum _ { k = 1 } ^ { m } x _ { j k } = 1 , j = 1 , \ldots , n } \\ { \mathrm { s . t . } } & { \quad x _ { j k } \in \{ 0 , 1 \} , \quad \forall j , k , } \end{array}
$$

over all permutation matrices X

3.3. The Biquadratic Assignment Problem. Recently Burkard, Cela and Klinz [35] (see the paper in this volume) introduced a fourth order generalization of the quadratic assignment problem. Let $A = \left( a _ { i , j , k , l } \right)$ and $B = \left( b _ { m , p , s , t } \right)$ be two arrays of $n ^ { 4 }$ elements. Then the biquadratic assignment problem asks to minimize

$$
\sum _ { i , j , k , l , m , p , s , t } a _ { i , j , k , l } b _ { m , p , s , t } x _ { i m } x _ { j p } x _ { k s } x _ { l t }
$$

of the problem. $X$ . This problem arises in the field of VLSI synthesis. In [35] various formulations of this problem are described. Also, lower bounds and some methods to construct instances with known optimal solution are presented. There are still many open problems related to this generalized model of the quadratic assignment problem. In particular it would be interesting to explore eigenvalue related techniques to this problem.

After having described some relatives of the quadratic assignment problem, which typically are at least as hard or harder to solve we will now focus on specially structured quadratic assignment problems which lead to simplifications of the problem.

3.4. Special Cases. The quadratic assignment problem can be formulated very naturally in a graph theoretical context. This formulation was investigated first by Christofides and Gerrard [54], and later by Bokhari [23] and Rendl [208]. We review this formulation and present several applications to other optimization M G G0 = H : H sub ra h of G0 H  G :

Let $G = ( V , E )$ and $G ^ { \prime } = ( V ^ { \prime } , E ^ { \prime } )$ be graphs. $G$ is isomorphic to $G ^ { \prime }$ $\mathbf { \Omega } ^ { \prime } G \approx G ^ { \prime }$ The graph theoretic formulation of quadratic assignme $p : V \mapsto V ^ { \prime }$ was

$$
i j \in E \iff p ( i ) p ( j ) \in E ^ { \prime } .
$$

We denote by $\Pi ( G , G ^ { \prime } )$ the set of adjacency preserving mappings between $G$ and $G ^ { \prime }$ . Furthermore we denote by $M ( G , G ^ { \prime } )$ the set of all subgraphs $H$ of $G ^ { \prime }$ , which are isomorphic to $G , \mathsf { i . e }$ -

$$
M ( G , G ^ { \prime } ) = \{ H : H { \mathrm { ~ } } { \mathrm { s u b g r a p h ~ o f ~ } } G ^ { \prime } , H \approx G \} .
$$

The graph theoretic formulation of quadratic assignment problem was proposed by Christofides and Gerrards as follows.

Let $G$ and $G ^ { \prime }$ be graphs with edge weights $a : E \mapsto \mathfrak { R } , \ b : E ^ { \prime } \longmapsto \mathfrak { R }$

$$
\operatorname* { m i n } _ { H \in M \left( G , G ^ { \prime } \right) } \operatorname* { m i n } _ { \pi \in \Pi \left( G , H \right) } \sum _ { i j \in E } a _ { i j } b _ { \pi \left( i \right) \pi \left( j \right) } .
$$

It is well known that the traveling salesma $\vert V \vert ~ \le ~ \vert V ^ { \prime } \vert ~ . )$ the matching prob$G$ m can $G ^ { \prime }$ e formulated as a special quadratic assign $K _ { n }$ nt prob $M ( G , G ^ { \prime } ) = \{ G ^ { \prime } \}$ haps $\Pi ( G , G ^ { \prime } )$ own are the connections of t $\pmb { n }$ quadratic assignment problem to the bandwidth problem in grap

ndwidth problem (we refer to [201] for a survey on the topic): Let G be an undirected (and unweighted) graph on n nodes. A permutation  of n elements is called a labeling of the nodes of G. The bandwidth of a labeling  is dened as problem.

It is well known that the traveling salesman problem and the matching probThe bandwidth  of G is the minimum of this number over all labelings. In terms of matrices, the bandwidth problem asks for a simultaneous permutation of the rows and columns of the adjacency matrix of G such that all nonzero entries are as close as possible to the main diagonal.

Sup $G$ se the bandwidth of a given graph G is at $\pmb { n }$ ost k. Let us denote b $\pi$ Pn $\pmb { n }$ the graph on n vertices with edges ij when $G$ er ji   jj  k. Then clearly G $\pi$ ust be isomor

$$
\operatorname* { m a x } _ { i j \in E } | \pi ( i ) - \pi ( j ) | .
$$

Pn;k by B, then $\sigma$ we $G$ is the minimum of this number over all labelings. In terms The bandwidth of G is at most k if and only if max2 Pij aijb(i)(j) = 2jEj: Therefore if some upper bound on this qu $G$ ratic assignment problem has a value less than 2jEj for a xed value of

ndwidth is larger than k. This idea was u $G$ in [110] to $k$ derive lower bounds $P _ { n , k }$ he bandwidth $\pmb { n }$ f graphs. In particu $i j$ the follow $| i - j | \le k$ lower bound $G$ the bandwidth is proved. $P _ { n , k }$ . Conversely, if the bandwidth of $G$ is larger than $k$ , then there cannot exist a subgraph of $P _ { n , k }$ which is isomorphic to $G$ (G)  n2(L)= $G$ (L) $A$ and the adjacency matrix of $P _ { n , k }$ by $B$ , then we conclude:

The bandwidth of $G$ is at most $k$ if and only if $\begin{array} { r } { \operatorname* { m a x } _ { \pi \in \Pi } \sum _ { i j } a _ { i j } b _ { \pi ( i ) \pi ( j ) } = 2 | E | } \end{array}$ Therefore if some upper bound on this quadratic assignment problem has a value less than $2 | E |$ for a fixed value of $k$ , one immediately concludes that the bandwidth is larger than $k$ . This idea was used in [110] to derive lower bounds on the bandwidth of graphs. In particular the following simple lower bound on the bandwidth is proved.

$$
\sigma ( G ) \geq n \lambda _ { 2 } ( L ) / \lambda _ { n } ( L ) \ - \ 1
$$

Here $L$ denotes the Laplacian matrix of the graph, which is related to $A$ by $L = D i a g ( A e ) - A$ . (Recall that $A e$ is the vector of row sums of $A$ .)

[ , ] p g g p p p $g r a p h$ , which is the same as the bandwidth except that one minimizes

$$
\sum _ { i j \in E } | \pi ( i ) - \pi ( j ) | .
$$

4. Comp $\pi$ exity Issues and Asymptotic Behavior separator of some given size $k$ exists in a graph can be modeled as a quadratic assignment problem. We refer to further details in [110].

In [166, 209] it is pointed out that the general graph partition problem can be modeled as a quadratic assignment problem. (See Section 4.3 for details.) It turns out however, that exploiting the special structure of the partition problem leads to more powerful results than treating this problem as a quadratic assignment problem.

# AP is NP-complete, which implies that nding a poly

From the computational point of view the QAP is one of the most difficult problems to solve. In this section several aspects regarding the complexity of the QAP are discussed. Although computational complexity characterizes worst case instances, it also plays an important role in developing new algorithms for p ( ), g p p g p ( ), q p and revealing surprising connections among problems and their solutions.

4.1. Computational Complexity. In 1976, Sahni and Gonzalez showed that the QAP is $N P$ -complete, which implies that finding a polynomial-time algorithm to solve it is unlikely [221]. In addition, they have also shown that QAP belongs even to the hardest core of this complexity class, in the sense that the problem of finding an e-approximate solution of QAP remains $N P$ -complete.

Many well known $N P$ -Complete problems, such as the traveling salesman problem (TSP), the graph partitioning problem (GP), the maximum clique problem (MCP), can be easily formulated as special cases of the QAP:

adjacency matrix of the graph for the MCP, a ow matrix corresponds to the adjacency matrix of a clique of size k. The maximum clique can be found by solving a set of n QAPs, $\pmb { n }$ n   
The graph partitioning problem (GP): The distance matrix corresponds to the adjacency matrix of the GP, the flow matrix corresponds to the adjacency matrix of two disjoint complete graphs of size $n / 2$ (assuming $\pmb { n }$ is even).   
The maximum clique problem (MCP): To identify the existence of a clique of size $k$ , one constructs a distance matrix corresponding to the adjacency matrix of the graph for the MCP, a flow matrix corresponds to the adjacency matrix of a clique of size $k$ . The maximum clique can be found by solving a set of $\pmb { n }$ QAPs, one for each $k , 1 \leq k \leq n$

ighted adjacency matrix of a tree, while the other one represents the distance matrix of a grid graph G = (V; E), where the distances between nodes i and j is dened as follows $A$ and $B$ are weighted adjacency matrices of a tree, the problem can be solved in a dynamic programming fashion, in polynomial time. But if only 1 of the 2 matrices is a weighted adjacency matrix of a tree, the problem remains to be $N P$ -complete since the TSP Other polynomial-time solv

atrix is the weighted adjacency matrix $O ( n \log n )$ e star (see Christodes and Gerrard [53]). When both distance and ow matrices are weighted adjacency matrices of series-parallel graphs containing no bipartite graph K2;2, then again the corresponding QA $G = ( V , E )$ in polynomial time [208]. $_ i$ and $j$ is defined as follows

$$
b _ { i j } = \left\{ \begin{array} { l l } { 1 , \mathrm { ~ i f ~ } ( i , j ) \in E , } \\ { \mathrm { l e n g t h ~ o f ~ t h e ~ s l ~ } } \end{array} \right.
$$

Other polynomial-time solvable cases include the case in which one of the matrix is the weighted adjacency matrix of a double star (see Christofides and Gerrard [53]). When both distance and flow matrices are weighted adjacency matrices of series-parallel graphs containing no bipartite graph $K _ { 2 , 2 }$ , then again the corresponding QAP is solved in polynomial time [208].

rdest problems in PLS. For certain NP-complete problems, the corresponding PLS problems have already been shown to be PLS-complete [126, 223]. I

ard to the complexity of local search, see also [181] and [191]. moves to neighboring solutions until no further improvement is possible. To characterize the complexity of solving combinatorial optimization problems such as the QAP with local search algorithms, a Polynomial-time Local Search (PLS) class has been defined [126] that captures the structure of NP problems at the level of their feasible solutions and neighborhoods. Similar to NP-completeness, the concept of PLS-completeness has been defined to capture the class of the hardest problems in PLS. For certain NP-complete problems, the corresponding PLS problems have already been shown to be PLS-complete [126, 223]. In regard to the complexity of local search, see also [181] and [191].

th the lowest cost in the sequence (the algorithm stops if the sequence is empty search algorithm for the QAP and establish the connection between the new algorithm and the Kernighan-Lin heuristic algorithm for the (GP).

The local search algorithm for the QAP starts with a random permutation as a current permutation. For a current permutation $p _ { 0 }$ , a sequence of permutations, $p _ { 1 } , \ldots , p _ { l }$ , is constructed in a greedy sense. Each of the permutations in the sequence is obtained from the previous one by swapping (interchanging) two assignments and has cost lower than the current permutation. A local search is performed in the sequence, replacing the current permutation by the permutation with the lowest cost in the sequence (the algorithm stops if the sequence is empty for the current permutation). In the description of the local search algorithm (i) Set p0 = p and calculate $C ( \boldsymbol { p } _ { k } )$ st C(p0). Set i = 0 $p _ { k }$ = 0, and G(i) = 0, where gi and G(i) are the step gain and the cu $p _ { 0 }$ lative gain, respectively. ( $G ( k )$ = 1. Initially, selec $p _ { k }$ pair of $G ( k ) = C ( p _ { 0 } ) - C ( p _ { k } )$ y exchanging their locations, a positive step gain is obtained, i.e., g1 =

Algorithm 1: A Local Search Algorithm for the QAP

Input: $\pmb { n }$ $n \times n$ matrices $F , D$ , and a permutation $p$ of size $\pmb { n }$

Output: A local optimal permutation $p$ for the QAP.

(iv) Co $p _ { 0 } = p$ he cumulative gain, G $C ( p _ { 0 } )$ Pk= $i = 0$ , $g _ { i } = 0$ > 0; t $G ( i ) = 0$ o 3. $g _ { i }$ and $G ( i )$ are the step gain and the cumulative gain, respectively. (v) $i = 1$ t k, such that G(k) is maximum for 0  k  i. If k > 0 then set p0 = pk and go to 2. $g _ { 1 } = C ( p _ { 0 } ) - C ( p _ { 1 } ) > 0$ We have reached a local optimum for the QAP. $G ( 1 ) = g _ { 1 }$   
(iii) $i = i + 1$ . For each pair of facilities not already selected, evaluate the step gain by exchanging their locations. Then, select the pair with maximum gain $g _ { i } = C ( p _ { i - 1 } ) - C ( p _ { i } )$ . If all facilities have been selected then set   
aph Gence $i = i - 1$ ( )ssuming jVj = 2n) win of the set V alwa $\begin{array} { r } { G ( i ) = \sum _ { k = 1 } ^ { k = i } g _ { k } } \end{array}$ w(eion $G ( i ) > 0$ For conve-sets A B h jAj = jB $k$ = jVj=2 i $G ( k )$ rest of the pap $0 \leq k \leq i$   
nd a $k > 0$ on (A; B) $p _ { 0 } = p _ { k }$ set V with t   
den ed to be the sum of the weights of all edges betw $p = p _ { 0 }$ and B. As t $p$ e mo $C ( \boldsymbol { p } )$ c

nse. Each partition (Ak; Bk); 1  k  l, in the sequence is obtained from the previo $G ( V , E )$ (Ak 1; Bk 1 $| V | = 2 n$ ping one vertex in $w ( e )$ $e \in E$ ne vertex in Bk 1 and has cost lower than $V$ e current partition. A local search is per $( A , B )$ in th $| A | = | B | = | V | / 2$ f this sequence, replacing the current partition by the partition with the l $( A , B )$ ost in the s $V$ uence (the algorithm stop $C ( A , B )$ equence is empty for the current partition). Similar to the description $A$ Algor $B$ hm 1, we use the cumulative gain G(k) for a partition pk. heuristic starts with a random partition of the set $V$ . A sequence of partitions, ${ ( A _ { 1 } , B _ { 1 } ) , \ldots , ( A _ { l } , B _ { l } ) }$ , is constructed for a current partition $\left( A _ { 0 } , B _ { 0 } \right)$ in a greedy sense. Each partition $\left( A _ { k } , B _ { k } \right)$ , $1 \leq k \leq l$ , in the sequence is obtained from the previous one $\left( A _ { k - 1 } , B _ { k - 1 } \right)$ by swapping one vertex in $A _ { k - 1 }$ with one vertex in $B _ { k - 1 }$ and has cost lower than the current partition. A local search is performed in the set of partitions of this sequence, replacing the current partition by the partition with the lowest cost in the sequence (the algorithm stops if the sequence is empty for the current partition). Similar to the description of Algorithm 1, we use the cumulative gain $G ( k )$ for a partition $p _ { k }$

Algorithm 2: Kernighan-Lin heuristic for the GP   
Input: $n , G = ( V , E )$ with $\vert V \vert = 2 n , W = \left( w _ { i j } \right)$ , and a partition $( A , B )$ of $V$   
Output: A locally optimal partition $( A , B )$ of $V$ gain $A _ { 0 } = A$ (Ai 1 $B _ { 0 } = B$ C(Ai; Bi). If all $C ( A _ { 0 } , B _ { 0 } )$ s have $i = 0 , g _ { i } = 0$ then $G ( i ) = 0$   1 and $g _ { i }$ to 5. $G ( i )$ are step gain and cumulative gain, Compute th (ii) $\mathrm { i } = 1$ .Initially, select a pair of vertices $a _ { 1 } \in A _ { 0 }$ and $b _ { 1 } \in \mathcal { B } _ { 0 }$ such that, Choose k, such that G(k) is maximum for $\left( A _ { 1 } , B _ { 1 } \right)$ produces a positive If k > 0 t $g _ { 1 }$ n set $g _ { 1 } = C ( A _ { 0 } , B _ { 0 } ) - C ( A _ { 1 } , B _ { 1 } ) > 0$ . If such a pair does We have reached a local optimum fo $G ( 1 ) = g _ { 1 }$ s   
(iii) $i = i + 1$ A; B and C(A; B). $a _ { i } \in A _ { i - 1 }$ and $b _ { i } \in B _ { i - 1 }$ and swap them to obtain $A _ { i }$ and $B _ { i }$ with maximum step gain $g _ { i } = C ( A _ { i - 1 } , B _ { i - 1 } )  – C ( A _ { i } , B _ { i } )$ . If all the vertices have been selected   
ne can easily see the similarity between them. Instead of working with partitions QAP in the $k$ ext section $G ( k )$ ls why the adapta $0 \leq k \leq i$   
P can $k > 0$ ective. F $A _ { 0 } = A _ { k }$ re, e $B _ { 0 } = B _ { k }$ computationa dica te that the proposed local search algorithm (Algori $A = A _ { 0 }$ perfo $B = B _ { 0 }$ y Output $A , B$ and $C ( A , B )$

n problems, local search gives rise to some of the most successful heuristics. A classical exam le in this re ard is the Linear Pro rammin Problem for which in the GP, we work with permutations in the QAP. The reduction from the GP to the QAP in the next section reveals why the adaptation of (KL) algorithm to the QAP can be effective. Furthermore, extensive computational results in section examples can be constructed that force the Simplex method to take exponential well.

In order to characterize the complexity of such local search algorithms, a new complexity class, the Polynomial-time Local Search class, was introduced and A classical example in this regard is the Linear Programming Problem for which the Simplex method can be viewed as a local search algorithm, in which a local search step is to go from the current basis to an adjacent basis which differs from the current one by one column vector. Based on the pivoting rule, worst-case examples can be constructed that force the Simplex method to take exponential time. Whether there can be a pivoting rule under which the Simplex method takes only polynomial time is a major open question.

In order to characterize the complexity of such local search algorithms, a new complexity class, the Polynomial-time Local Search class, was introduced and

More formally, a local sear $P$ problem P in PLS is dened as $x \in I$ s: Given an input x, nd a locally optimal solution s 2 F( $F ( x )$ or the problem P, the following three $s \in F ( x )$ al time algorithm $\pmb { s }$ should also e $x \in I$ , we can produce a feasible solution $s \in F ( x )$ in polynomial time. Next, given $x \in I$ and $s \in F ( x )$ we can compute the cost $C ( \boldsymbol { s } , \boldsymbol { x } )$ of s in polynomial time. In addition, every solution $s \in F ( x )$ has a set of neighboring solutions $N ( s , x )$ . Finally, given $x \in I$ and $s \in F ( x )$ , we can test in polynomial time whether $\pmb { s }$ is locally optimal, and if not, produce a solution belonging to $N ( s , x )$ with a better cost value (A solution $\pmb { s }$ is locally optimal if it does not have a strictly better neighbor).

A problem P 2 PLS is PLS-reducible $P$ another problem Q 2 PLS, if there are polyn $\pmb { x }$ mial time computable functions f $s \in F ( x )$ ch that f maps an i $P$ ance x of P to an instance f(x) of Q and for any locally optimal s

(i) Algorithm A, on input $x \in I$ , computes an initial feasible solution ${ \pmb s } _ { 0 } ~ \in$ $F ( x )$   
(ii) Algorithm B, on input $x \in I$ and $s \in F ( x )$ computes $C ( \boldsymbol { s } , \boldsymbol { x } )$   
(ii) Algorithm C, on input $x \in I$ and $s \in F ( x )$ , either determines that $\pmb { s }$ is locally optimal or finds a better solution in $N ( s , x )$

obtained fr $P \in \mathrm { { P L S } }$ ) by swapping one element of A with $Q \in \mathrm { { P L S } }$ ent of B. (A ; B ) is a greedy swap if C(A; B)   C( $f$ ; B ) $g$ s maximiz $f$ over all swaps of $\pmb { x }$ A; $P$ . If in fact (A ; $f ( x )$ s t $Q$ lexicographically smallest over all gre $\pmb { s }$ dy s $f ( x )$ , $g { \big ( } s , x { \big ) }$ that (A ; B ) is the lexicographic greed $\pmb { x }$ wap of (A; B). $P$ Let (Ai; Bi) be a sequence of partitions, each of which is a swap of the one pr $P$ e

m (A0; B0). We call it monotonic, if the dierences of Ai   A0 and Bi   B0 are monotonically increasing (that is, no vertex is switched back to its original set (A0; B0)). Finally, we say that a partition (A ; B ) is a neig $( A , B )$ f (A; B) if it occ $( A ^ { ' } , B ^ { ' } )$ e unique $A$ axim $A ^ { ' }$ monotonic sequence of lexicographicall $( A ^ { ' } , B ^ { ' } )$ swaps starting w $( A , B )$ B). Note that such a sequenc $A$ will consist of jVj=2 $B$ 1 $( A ^ { ' } , B ^ { ' } )$ ns, with the last on $C ( A , B ) - C ( A ^ { ' } , B ^ { ' } )$ Thus, each partition has jVj=2 $( A , B )$ ors. The $( A ^ { ' } , B ^ { ' } )$ m performs local search over this neighborhood structure, replaci $( A ^ { ' } , B ^ { ' } )$ urrent partition by the partition w $( A , B )$ lowe $\left( A _ { i } , B _ { i } \right)$ n the neig hb o rho o d. In $\left( A _ { 0 } , B _ { 0 } \right)$ aining part of this section, we show that the $A _ { i } - A _ { 0 }$ ith t $B _ { i } - B _ { 0 }$ borhood structure dened in Algorithm 1 is PLS-complete by reduction from set $\left( A _ { 0 } , B _ { 0 } \right) )$ . Finally, we say that a partition $( A ^ { ' } , B ^ { ' } )$ is a neighbor of $( A , B )$ if it occurs in the unique maximal monotonic sequence of lexicographically greedy swaps starting with $( A , B )$ . Note that such a sequence will consist of $| V | / 2 + 1$ partitions, with the last one equal to $( B , A )$ . Thus, each partition has $| V | / 2$ neighbors. The algorithm performs local search over this neighborhood structure, replacing the current partition by the partition with the lowest cost in the neighborhood.

In the remaining part of this section, we show that the QAP with the neighborhood structure defined in Algorithm 1 is PLS-complete by reduction from this neighborhood structure, nding a local optimum for the QAP is in PLS. To prove PLS-completeness, we show that the GP is PLS-reducible to the QAP. Given an instance of the GP of size 2n, we can create an instance of the QAP with the same size in polynomial time. Furthermore, for each local optimal permutation of the QAP, there is a natural local optimal partition for the corresponding GP. More specically, suppose for the GP, the graph G = (V; E) has edge weights w(e) and vertex set V with jV $\lfloor n / 2 \rfloor$ n. We construct, in polynomial time, an instance of the QAP with 2n - 2n matrices F = (fij) and D = (dkl) dened below: $\lfloor n / 2 \rfloor$ neighboring permutations. Hence, with this neighborhood structure, finding a local optimum for the QAP is in PLS.

To prove PLS-completeness, we show that the GP is PLS-reducible to the fij ( ; j) ( ; j) ; $2 n$ , we can create an instance of the QAP with the same size in polynomial time. Furthermore, for each local optimal dkl = 0 if k; l 2 A or k; l 2 B; otherwise dlk = 1; responding GP. More specifically, suppose for the GP, the graph $G = ( V , E )$ has edge weights $w ( e )$ and vertex set $V$ with $| V | = 2 n$ . We construct, in polynomial time, an instance of the QAP with $2 n \times 2 n$ matrices $\boldsymbol { F } = \left( f _ { i j } \right)$ and $D = \left( d _ { k l } \right)$ This reduction

$$
f _ { i j } = w ( i , j ) { \mathrm { ~ i f ~ } } ( i , j ) \in E ; { \mathrm { ~ o t h e r w i s e ~ } } f _ { i j } = 0 ,
$$

$$
A = \{ 1 , 2 , \ldots , n \} , B = \{ n + 1 , n + 2 , \ldots , 2 n \} .
$$

and can be recovered in polynomial time. By denition, the local search pr $p _ { k }$ em for the QAP with the ne $\left( A _ { k } , B _ { k } \right)$ od structure de $V$ d in Algorithm 1 is PLScomplete. $\pmb { n }$ in $p _ { k }$ constitutes the set $A _ { k }$ We should also mention that, at pre $n + 1$ th $2 n$ ar $p _ { k }$ o known local crit $B _ { k }$ a in deciding $p _ { k }$ w good $\mathrm { Q A P }$ al optimal solution is, in relation to the $\left( A _ { k } , B _ { k } \right)$ ptimum. From the complexity point of view, it can be shown $p _ { 0 }$ at, i $\left( A _ { 0 } , B _ { 0 } \right)$ xists a polynomial tim $p _ { k }$ algorithm for checking whether a $p _ { 0 }$ ven permutation $\left( A _ { k } , B _ { k } \right)$ lly optimal, then P = NP [177 $\left( A _ { 0 } , B _ { 0 } \right)$ . Hence, for any local optimal permutation of the $\mathrm { Q A P }$ , the corresponding partition is a local optimal partition for the GP and can be recovered in polynomial time. By definition, the local search problem for the QAP with the neighborhood structure defined in Algorithm 1 is PLScomplete.

We should also mention that, at present, there are no known local criteria in deciding how good a local optimal solution is, in relation to the global optimum. From the complexity point of view, it can be shown that, if there exists a polynomial time algorithm for checking whether a given permutation is globally optimal, then $\mathrm { P } = \mathrm { N P }$ [177].

4.4. Asymptotic Behavior. A nice feature of the $\mathrm { Q A P }$ is that the relative xed permutation p 2 , let cip(i)jp(j) be independently distributed. For given  > 0 and 0 < 0   and 0 < (E + 0)=(E   0)  1 + , and Finke discovered this behavior for the QAP in the plane, i.e., the distance matrix $B$ P(   < 1 + )  1   2n!e ; that this behavior holds also for the QAP in general in 1985. The result can be where 0 = 2((0)=(0 + 22))2;

THEOREM 4.1. For $i , j , k , l \in \{ 1 , \cdots n \}$ , let $c _ { i j k l }$ be identically distributed random variables in $[ 0 , 1 ]$ with expected value $E$ and variance $\sigma ^ { 2 } > 0$ . For every Several other re $p \in \Pi$ rs, i $c _ { i p \left( i \right) j p \left( j \right) }$ Frenk, van Houweninge, and Rinnooy Kan $\epsilon > 0$ and $0 < \epsilon _ { 0 } \le \sigma ^ { 2 }$ 212] $0 < ( E + \epsilon _ { 0 } ) / ( E - \epsilon _ { 0 } ) \le 1 + \epsilon ,$ e

$$
P ( \frac { F _ { c } ^ { + } } { F _ { c } ^ { - } } < 1 + \epsilon ) \ge 1 - 2 n ! e ^ { - \lambda _ { 0 } n ^ { 2 } } ,
$$

5.1 $\lambda _ { 0 } = 2 { \left( \left( \epsilon _ { 0 } \sigma \right) \right)} / { \left( \epsilon _ { 0 } + 2 \sigma ^ { 2 } \right) }  ^ { 2 }$ $\begin{array} { r } { \operatorname* { l i m } _ { n \to \infty } n ! e ^ { - \lambda } 0 ^ { n ^ { 2 } } = 0 } \end{array}$ be di $F _ { c } ^ { + }$ nt m $F _ { C } ^ { - }$ ds used to nd an optimal solution of QAP. The methods include d $Q A P$ ic programming, $C$ t

Several other researchers, including Frenk, van Houweninge, and Rinnooy Kan enerall dicult to solve. This is due to the inherent dicult of the AP the convergence holds almost everywhere.

# 5. Methods of Solution

Cutting plane methods for the QAP were introduced by Bazaraa and Sherali [19]. Although the computational experience was not satisfactory, such methods can be used to nd good suboptimal solutions, s

4]. In Bazaraa and Sherali [20], cutting plane procedures were investigated for solving the concave quadratic minimization formulation of the QAP. Several heuristics derived from the cutting plane procedures produce good quality solutions in early stage of the search procedure. Christodes and Benavent [52] used a special dynamic programming approach for the special case of the QAP in w

atrix of a tree. Problems of sizes up to 30 were solved. [19]. Although the computational experience was not satisfactory, such methods can be used to find good suboptimal solutions, see e.g., Burkard and Bönniger [34]. In Bazaraa and Sherali [20], cutting plane procedures were investigated for solving the concave quadratic minimization formulation of the QAP. Several heuristics derived from the cutting plane procedures produce good quality solutions in early stage of the search procedure.

Christofides and Benavent [52] used a special dynamic programming approach for the special case of the QAP in which the fow matrix is the weighted adjacency matrix of a tree. Problems of sizes up to 30 were solved.

ee. Some of the earliest branch and bound algorithms for solving QAPs are described in [36], [66], [180] and [218]. Pair assignment algorithms were developed by Gavett and Plyter [86], Land [141], and Nugent et al. [171], etc. At each node of the branch-and-bound search tree, a xed pair of facilities is allocated to a pair of locations. The last algorithm, the relative positioning algorithm, was developed by Mirchandani and Obata [160]. In their approach, the levels of the branch-and-bound search tree do not correspond to the assignments of facilities to locations. The partial permutations at each level are determined in terms of distances between facilities, i.e., their relative positions. Numerical experiences indicate that

gorithms the single assignment algorithms are the best. The pair assignment algorithms were shown to be not computationally ecient. The authors of the relative positioning algorithm claimed favorable behavior of the algorithm for problems with sparse matrices. and Obata [160]. In their approach, the levels of the branch-and-bound search tree do not correspond to the assignments of facilities to locations. The partial permutations at each level are determined in terms of distances between facilities, i.e., their relative positions.

Numerical experiences indicate that among the 3 types of branch-and-bound algorithms the single assignment algorithms are the best. The pair assignment algorithms were shown to be not computationally efficient. The authors of the relative positioning algorithm claimed favorable behavior of the algorithm for problems with sparse matrices.

pensive to compute. In the following, a brief discussion of the 3 categories of lower bounds is given. should be sharp and should be fast to compute. For the QAP, there are roughly 3 categories of lower bounds. The first category includes the classical GilmoreLawler bound (GLB) and related bounds [89, 143]. The second category includes the eigenvalue based bounds [74, 102, 101, 210, 103]. The rest of the hx; yi  = minhx; Pyi; hx; yi+ = maxhx; Pyi; solving a number of linear assignment problems [5, 47, 54, 82]. It is generally where the set  denotes the set of all permutations of N and x; y 2 R . In fact, hx; yi  can be computed as the inner product of x and y , where x is lower bounds is given.

5.2.1. Gilmore-Lawler Bound (GLB) and Related Bounds. The GLB is computed by using the minimal vector product and the maximal vector product, denoted $\left. x , y \right. _ { - }$ and $\left. { \pmb x } , { \pmb y } \right. _ { + }$ , defined below

$$
\langle x , y \rangle _ { - } = \operatorname* { m i n } _ { P \in \Pi } \langle x , P y \rangle , \ : \langle x , y \rangle _ { + } = \operatorname* { m a x } _ { P \in \Pi } \langle x , P y \rangle ,
$$

where the set $\Pi$ denotes the set of all permutations of $N$ and $x , y \in R ^ { n }$ . In fact, $\left. x , y \right. _ { - }$ can be computed as the inner product of $x ^ { + }$ and $y ^ { - }$ , where $x ^ { + }$ is linear assignment problem (LAP) with co $\pmb { x }$ matrix L, i.e. $y ^ { - }$ is obtained by ordering the components of $_ y$ descendingly. $\left. x , y \right. _ { + }$ can be computed similarly.

Let $a _ { i } , b _ { i }$ $i = 1 , . . . , n$ GLB(A; B) = min X lip(i): $A , B$ , respectively. Let $\hat { a } _ { i }$ be the vector consisting of the $\left( n - 1 \right)$ i=1 $a _ { i }$ , not including $a _ { i i }$ 5 $\hat { b } _ { i }$ .2. Eigenvalue Based Bounds. $\left( n - 1 \right)$ based on eigenv $b _ { i }$ ues of the ow $b _ { i i }$ d distance matric $L = \left( l _ { i j } \right)$ B have be

$$
l _ { i j } = a _ { i i } b _ { j j } + \langle \hat { a } _ { i } , \hat { b } _ { j } \rangle _ { - } , \ i , j = 1 , . . . , n .
$$

(2.1.2). $\mathbf { Q } \operatorname { A P } ( \mathbf { A } , \mathbf { B } )$ , is defined to be the solution to the A lower bound for the quadratic part of QAP, b $L$ ed on

$$
G L B ( A , B ) = \operatorname* { m i n } _ { p \in \Pi } \sum _ { i = 1 } ^ { n } l _ { i p ( i ) } .
$$

5.2.2. Eigenvalue $B$ ased Bounds. Bounds based on eigenvalues of the flow and distance matrices $A$ and $B$ have been proposed in a series of papers by Finke et al. [74], Hadley et al. [102, 101], and Rendl and Wolkowicz [210]. These bounds, denoted by $\mathrm { E V B }$  i+1  X X aijbp(i)p(j)  X ii: (2.1.2).

The linear part of QAP is bounded exactly by solving a linear sum assig $A$ ment $B$ oblem, denoted LSAP(C). We get the following bound for QAP $\mathcal { O }$ . This results in the following theorem (see [70, 74]).

EVBfA; B $B$ = in i+1 + LSAP(C): $\lambda _ { 1 } \leq \lambda _ { 2 } \ldots \leq \lambda _ { n }$ be the eigenvalues of $A$ , and $\mu _ { 1 } ~ \leq ~ \mu _ { 2 } \ldots \leq ~ \mu _ { n }$ be the eigenvalues of $B$ . For any $p \in \Pi$ i

$$
\sum _ { i = 1 } ^ { n } \lambda _ { i } \mu _ { n - i + 1 } \leq \sum _ { i = 1 } ^ { n } \sum _ { j = 1 } ^ { n } a _ { i j } b _ { p ( i ) p ( j ) } \leq \sum _ { i = 1 } ^ { n } \lambda _ { i } \mu _ { i } .
$$

The strengthened relaxation of the constraint set of permutation matrices to O \ E was done in [101]. This relaxation proved to be particularl

$$
E V B \{ A , B \} = \sum _ { i = 1 } ^ { n } \lambda _ { i } \mu _ { n - i + 1 } + L S A P ( C ) .
$$

obtained iteratively, with each iteration taking O(n3) running time. This latter technique attempted to combine the bounds for the linear and quadratic parts. or constant row and column, perturbations of the matrices. Several such lower bounds, EVB1, EVB2, EVB3, and IVB, were developed in [74, 101].

The strengthened relaxation of the constraint set of permutation matrices to $\mathcal { O } \cap \mathcal { E }$ was done in [101]. This relaxation proved to be particularly efficient and made the constant row and column reductions redundant. Rendl and Wolkowicz [210] recently proposed a new lower bound (MEVB) based on eigenvalue decomposition in conjunction with a steepest ascent algorithm. The bound is obtained iteratively, with each iteration taking $O ( n ^ { 3 } )$ running time. This latter technique attempted to combine the bounds for the linear and quadratic parts.

(A further attempt to avoid taking the sum of two minima obtained by treating the quadratic and linear parts separately is given in the paper by Karisch, Rendl, and Wolkowicz in these proceedings.)

he bounds are denoted by FY1 and FY2 respectively. Finally, Carraresi and Malucelli [47] proposed $\mathtt { X u }$ w lower bound (CM) for the QAP through an iterative process. In each iteration, at most O(n2) linear assignment problems related with an e $n ^ { 2 } + 1$ t reformulation of the QAP a $\pmb { n }$ solved. Hence the procedure has a time complexity of O(kn5) w $O ( k n ^ { 5 } )$ the nu $k$ ber of iterations used. Christofides and Gerrard [54] proposed a lower bound (CG) by solving $O ( n ^ { 4 } )$ linear assignment problems corresponding to pairs of assignments, resulting in a $O ( n ^ { 7 } )$ procedure. Frieze and Yadegar [82] obtained 2 lower bounds by solving the Lagrangian relaxation of a related linear integer formulation of the QAP. 1 ( ij ) 2 ( ij ) 1 21 2 B into two matrices B1 = (bij ) and B2 = (bij ) such that B = B1 + B2. For each pair (i; j); i; j = 1; :::; n, consider $O ( n ^ { 2 } )$ llowing minimization problem with an equivalent reformulation of the $\mathrm { Q A P }$ are solved. Hence the procedure min aik bj(5.1) $O ( k n ^ { 5 } )$ aki b $k$ (k)j + akibp(k)j   aki bp(k)j

wher e 2  and i = : mal reduction schemes for the QAP was proposed in Li, Pardalos, Ramakrishnan Dene a n - n matrix L = (lij) where lij is the optimal objective fun $A$ ion value of (5.1). $A _ { 1 } = \big ( a _ { i j } ^ { ( \bar { 1 } ) } \big )$ ng th $\overset { \mathbf { \bar { A _ { 2 } } } } { = } ( a _ { i j } ^ { ( 2 ) } )$ es a new lo $A = A _ { 1 } + A _ { 2 }$ 49, Theorem 4.1]. $B$ Theorem 5.2. Le $B _ { 1 } = ( b _ { i j } ^ { ( 1 ) } )$ x L $B _ { 2 } = ( b _ { i j } ^ { ( 2 ) } )$ s above. T $B = B _ { 1 } + B _ { 2 }$ on o the linear $( i , j ) , \ i , j = 1 , . . . , n .$ with cost matrix L is a lower bound or the c

$$
\quad \mathrm { m i n } \qquad \sum _ { k = 1 } ^ { n } a _ { i k } ^ { ( 1 ) } b _ { j p ( k ) } ^ { ( 1 ) } + \sum _ { k = 1 } ^ { n } a _ { k i } ^ { ( 2 ) } b _ { p ( k ) j } + \sum _ { k = 1 } ^ { n } a _ { k i } b _ { p ( k ) j } ^ { ( 2 ) } - \sum _ { k = 1 } ^ { n } a _ { k i } ^ { ( 2 ) } b _ { p ( k ) j } ^ { ( 2 ) }
$$

reductio $n \times n$ ni ues $L = \left( l _ { i j } \right)$ the lite $l _ { i j }$ ture choose A and B with constant column sums which we call constant columns . We refer to such techni ues as

nstant column reductions. $L$ be defined as above. Then the solution of Let M = (mij) be a matrix in R . We t $L$ at a row vector mi; 1  i  n, of M as $Q A P$ n

The classical Gilmore-Lawler bound is a special case in which both matrices $A$ and $B$ are not partitioned. Different ways of partitioning the matrices $A$ and $B$ (we also refer to this as reduction) yield different lower bounds. The common reduction techniques used in the literature choose $A _ { 2 }$ and $B _ { 2 }$ with constant column sums (which we call constant columns). We refer to such techniques as constant column reductions.

Let $M = \left( m _ { i j } \right)$ be a matrix in $R ^ { n \times n }$ . We treat a row vector $m _ { i }$ $1 \leq i \leq n$ of $M$ as a $1 \times n$ matrix and a column vector $m _ { j } ^ { t }$ $1 \leq j \leq n$ as a $n \times 1$ matrix.

two variances, (a) average row variance, (b) variance of the entire matrix $\gamma ( M )$ variance $V ( M )$ , and total variance $T ( M , \lambda )$ of $M$

$$
\gamma ( M ) = \frac { 1 } { n ^ { 2 } } \sum _ { i = 1 } ^ { n } \sum _ { j = 1 } ^ { n } m _ { i j } , V ( M ) = \frac { 1 } { n ^ { 2 } } \sum _ { i = 1 } ^ { n } \sum _ { j = 1 } ^ { n } \left( \gamma ( M ) - m _ { i j } \right) ^ { 2 } ,
$$

$$
T ( M , \lambda ) = \lambda \sum _ { i = 1 } ^ { m } V ( a _ { i } ) + ( 1 - \lambda ) V ( M ) , { \mathrm { ~ f o r ~ } } 0 \leq \lambda \leq 1 .
$$

Note that the statistical total variance used here is the convex combination of In our reductio $\left( a \right)$ cheme, we considered $\left( b \right)$ partition A = A1 + A2, where A1

$$
\begin{array} { r c l } { \overline { T } } & { = } & { \displaystyle \frac { \lambda } { n } \sum _ { i = 1 } ^ { n } V ( m _ { i } ) + ( 1 - \lambda ) V ( M ) } \\ & & { = } & { \displaystyle \frac { \lambda } { n } \sum _ { i = 1 } ^ { n } ( \gamma ( m _ { i } ) - m _ { i j } ) ^ { 2 } + \frac { \lambda } { n ^ { 2 } } \sum _ { i = 1 } ^ { n } \sum _ { j = 1 } ^ { n } ( \gamma ( M ) - m _ { i j } ) ^ { 2 } } \\ & { = } & { \displaystyle \frac { 1 } { n ^ { 2 } } T ( M , \lambda ) . } \end{array}
$$

of A and B are the ti hter the GLB is the followin $A = A _ { 1 } + A _ { 2 }$ schemes $A _ { 1 } =$ $A + \Delta$ and $A _ { 2 } = - \Delta$ , such that the variances of $A _ { 1 }$ and $A _ { 2 }$ , the sum of variances of the rows of $A _ { 1 }$ , and the sum of variances of the rows of $A _ { 2 }$ are minimized. R-1) aij = aij   (ann   aij) and aij = (ann   aij); i;

$$
\begin{array} { r l } { \operatorname* { m i n } \quad } & { { } \theta T ( A + \Delta , \lambda ) + ( 1 - \theta ) T ( - \Delta ^ { t } , \lambda ) } \\ { \mathrm { ~ s u c h ~ t h a t ~ } \quad } & { { } \Delta \in \boldsymbol { R } ^ { n \times n } } \end{array}
$$

we pro $0 \leq \theta \leq 1$ o

B2(). Both new lower bounds are dependent on the parameter . Note that, LB $A$ (0.0) $B$ GLB(A; B) and LB1(1.0) = GLB(At; Bt). For LB1(), we found in our computational experiments

atrix  to partition matrices A and B takes only O(n2) time. By presort $\mathcal { R }$ g the rows of the ow and distance m $\operatorname { L B 1 } ( \theta )$ A and B, one can compute lij; i; j = we propose is to use the reduction scheme $\mathcal { R } { - } 2$ . This lower bound is denoted $\operatorname { L B 2 } ( \theta )$ . Both new lower bounds are dependent on the parameter $\theta$ . Note that, $\operatorname { L B } 1 ( 0 . 0 ) = G L B ( A , B )$ and $\operatorname { L B } 1 ( 1 . 0 ) = G L B ( A ^ { t } , B ^ { t } )$

For $\operatorname { L B 1 } ( \theta )$ , we found in our computational experiments that $\theta = 0 . 5$ is a good choice. For $\operatorname { L B 2 } ( \theta )$ , we used $\theta = 1 . 0$ . The latter was expected since the column variance of the matrix $\Delta$ is already zero when computing $\operatorname { L B 2 } ( \theta )$

The new lower bounds can be computed quite efficiently. Computing the matrix $\Delta$ to partition matrices $A$ and $B$ takes only $O ( n ^ { 2 } )$ time. By presorting the rows of the flow and distance matrices $A$ and $B$ , one can compute $l _ { i j } , i , j =$

$1 , . . . , n$ e t $O ( n ^ { 3 } )$  ! 1, this partitioning scheme app $O ( n ^ { 3 } )$ s the constant column reduction partitioning. Experimentally, we have observed that th

duction partitioning scheme is more eective and is easier to implement. For an ecient implementation of

$$
\begin{array} { r c l } { { \delta _ { i j } } } & { { = } } & { { \theta \lambda \displaystyle \frac { 1 - \theta } { 1 - \theta \lambda } \gamma ( a _ { i } ) + \displaystyle \frac { \theta ( 1 - \lambda ) + \theta \lambda ^ { 2 } ( 1 - \theta ) - \theta ^ { 2 } \lambda ^ { 2 } ( 1 - \theta ) } { ( 1 - \theta \lambda ) ( 1 - \lambda + \theta \lambda ) } \gamma ( A ) } } \\ { { } } & { { } } & { { - \displaystyle \frac { \lambda \theta ( 1 - \theta ) } { 1 - \lambda + \theta \lambda } \gamma ( a _ { j } ^ { t } ) - \theta a _ { i j } . } } \end{array}
$$

Note that, as $\theta  1$ , this partitioning scheme approaches the constant column reduction partitioning. Experimentally, we have observed that the column reduction partitioning scheme is more effective and is easier to implement. For an efficient implementation of the lower bound and computational results of a branch and bound algorithm that uses the new bound see [148].

art from a permutation p and try to get an improved permutation by using some techniques, sim $\mathrm { Q A P }$ n approaches an $\epsilon$ genetic algorithms which belong to stochast $N P$ arch techniques. and solution quality are highly desirable. Research in this direction abounds in literature. Basically, there are 5 types of heuristics including construction methods which start from an empty permutation $p$ and expand $p$ to a suboptimal permutation according to certain criteria, limited enumeration methods which perform partial enumeration with the expectation that good solutions are generally found in early stages of enumeration, improvement methods which 6 ( ) $p$ and try to get an improved permutation by using some techniques, simulation approaches and genetic algorithms which belong to stochastic search techniques.

One of the oldest heuristics used is the CRAFT (Computerized Relative Allocation of Facilities Technique) [4, 231, 30]. This is a well-known heuristic for designing the layout of facilities that has been in use for over 25 years. Given a set of departments, locations, a matrix of $p$ ows between departme $p$ s, and a matrix of costs to transport one item between tw $( i , j )$ partments $i \notin M$ dis$j \not \in p ( M )$ AFT iteratively improves an initial, u $M$ -supplied, layout by a series of departmen $p$ exchanges. At each step CRAFT considers either all po $p ( M )$ 2- the set $\{ p ( i ) ~ | ~ i \in M \}$ . This process is repeated until $p$ becomes a complete permutation.

One of the oldest heuristics used is the CRAFT (Computerized Relative Allocation of Facilities Technique) [4, 231, 30]. This is a well-known heuristic for designing the layout of facilities that has been in use for over 25 years. Given a set of departments, locations, a matrix of fows between departments, and a matrix of costs to transport one item between two departments a unit distance, CRAFT iteratively improves an initial, user-supplied, layout by a series of department exchanges. At each step CRAFT considers either all possible 2- way, 3-way, or both 2-way and 3-way exchanges. It chooses the exchange that provides the most improvement in minimizing total cost, and then repeats the process until no improving exchange can be found.

n stops when a predetermined time limit is reached or there is no improvement within a certain time limit. Another way is to decrease the requirements for optimality. For example, whenever an improvement is not obtained after a given time period, the upper bound is decreased by a certain specied percentage, resulting $\pmb { n }$ n deeper cuts in the enumeration tree. Although it is possible that the optimal solution may be cut o, the enumeration process is speeded up. Furthermore

e by not more than some specied percentage. tions. One simple way is to put a time limit on the search procedure. Enumeration stops when a predetermined time limit is reached or there is no improvement within a certain time limit. Another way is to decrease the requirements for optimality. For example, whenever an improvement is not obtained after a given time period, the upper bound is decreased by a certain specified percentage, resulting in deeper cuts in the enumeration tree. Although it is possible that the optimal solution may be cut off, the enumeration process is speeded up. Furthermore, one can estimate that the optimal value differs from the suboptimal one by not more than some specified percentage.

5.3.3. Improvement Methods. The majority of the heuristic solution methods Tabu search was introduced by Glover [90, 91] as a technique to overcome local optimality in combinatorial search. The underlying idea is to limit the search directions for each search step to obtain good quality solutions in an eective way. This approach has been applied successfully to a number of combinatorial optimization problems including the TSP. Adaptations of tabu search to the QAP have been studied by Skorin-Kapov [238] and Taillard [242]. The basic idea is as follows. To improve a given initial permutation tabu search seeks, among the set of permuta

e best heuristic evaluation. In the simplest case, such an evaluation dictates the choice of a permutation which give the best objective function value. Every choice of a neighboring permutation represents an exchange of a pair of facilities. way. This approach has been applied successfully to a number of combinatorial optimization problems including the TSP. Adaptations of tabu search to the QAP have been studied by Skorin-Kapov [238] and Taillard [242]. The basic idea is as follows.

To improve a given initial permutation tabu search seeks, among the set of permutations obtained by a pair exchange of assignments, a permutation with the best heuristic evaluation. In the simplest case, such an evaluation dictates the choice of a permutation which give the best objective function value. Every choice of a neighboring permutation represents an exchange of a pair of facilities.

has proven useful in solving some traditional optimization problems, such as computer design, partitioning, component placement, wiring, and the traveling salesman problem. The analogy has resulted in a methodology, termed simulated annealing, which is used to overcome local optimality (see Kirkpatrick, Gelatti, and Vecchi [135]). The term \annealing" refers to the process

annealing schedule. The process is continued until the vicinity of the solidi- cation temperature is reached, where the system is allowed to reach the \ground state" (the lowest energy state of the system). Simulated annealing is a Monte Carlo approach to simulate the behavior of this system to achieve thermal equilibrium at a given temperature in a given annealing schedule. This analogy has been applied in solving combinatorial optimization problems. According to the above authors:

Iterative improvement, commonly applied to such problems, is much like the microscopic rearrangement process modeled by statistical mechanics, with the cost function playing the role of energy. However, accepting only rearrangements that lower the cost function of the system is like extremely rapid quenching high temperatures to T = 0. So, it should not be surprising that resulting solutions are usually metastable. The Metropolis procedure from statistical mechanics provides a generalization of iterative improvement in which controlled uphill steps can also be incorporated in the search for a better solution. Simulated A

Iterative improvement, commonly applied to such problems, is much like the microscopic rearrangement process modeled by statistical mechanics, with the cost function playing the role of energy. However, accepting only rearrangements that lower the cost function of the system is like extremely rapid quenching high temperatures to $T = 0$ . So, it should not be surprising that resulting solutions are usually metastable. The Metropolis procedure from statistical mechanics provides a generalization of iterative improvement in which controlled uphill steps can also be incorporated in the search for a better solution.

Simulated Annealing is applied to the QAP [253] as follows:

For example ti = 10 - (0:9)(i 1). The system remains at stage i until a predetermined number of pair evaluate the consequent change $\left( \delta f \right)$ in the total cost $( f )$ Repeat the above step as long as $\delta f ~ < ~ 0$ . Otherwise, select a random variable $\pmb { x }$ from a uniform distribution $U ( 0 , 1 )$ . If $~ x ~ < ~ P ( \delta f ) ~ =$ $E X P ( - \delta f / t _ { i } )$ (where $\mathrm { P }$ represents the probability obtained from the exponential distribution (EXP)), then accept the pair exchange and repeat the process. Here $t _ { i }$ represents the annealing schedule temperature at stage $_ i$ where $t _ { 1 } > t _ { 2 } > . . . > t _ { r }$ represents the annealing schedule. For example $t _ { i } = 1 0 \times ( 0 . 9 ) ^ { ( i - 1 ) }$ The system remains at stage $_ i$ until a predetermined number of pair

exchanges have been considered before going to the next stage. If all the temperatures in the annealing schedule have been used, i.e. if $i > r$ , then stop.

e procedure. Essential to the success of the adaptation of simulated annealing to the QAP is the annealing schedule as discussed in their work [41, 253]. In the paper [183], computational results with four heuristics, the CRAFT, simulating annealing, tabu search, and a local search based on graph partitioning permutation is counter to the normal steepest descent strategy. However, it is argued in the analogy that by taking such controlled ascent steps, the optimization 5.3.5. Genetic Algorithms. Genetic algorithms

other type of stochastic search technique. While simulated annealing is based on thermodynamic process, genetic algorithms are based on the mechanics of natural selection and natural adaptation. A genetic algorithm maintains a population consisting of a subset of individuals (solutions). Through means of biased selection and genetic operations, the algorithm replaces a population with a new population of individuals with better tness values on the average. Genetic al

uence at that time. With the advent of parallel computers, there has been increasing interest in genetic algorithms since they are inherently parallel. A number of researchers have tried to apply genetic algorithms to solve combinatorial optimization problems, such as the the graph partitioning problem and the traveling salesman problem [161]. selection and genetic operations, the algorithm replaces a population with a new 5.4. Greedy Randomized Adaptive Search Procedures

RASP is an iterative randomized sampling technique in which each iteration provides an approximate solution to the problem at hand. The incumbent solution over all GRASP iterations is kept as the nal result. There are two phases within each GRASP iteration: the rst constructs an initial solution via an adaptive randomized greedy function; the second applies a local search technique to the constructed solution in hope of nding an improvement. A comprehensive survey of GRASP can be found in [73

odels the positioning of intermodal highway trailers on railcars. The GRASP is GRASP is an iterative randomized sampling technique in which each iteration provides an approximate solution to the problem at hand. The incumbent solution over all GRASP iterations is kept as the final result. There are two phases within each GRASP iteration: the first constructs an initial solution via an adaptive randomized greedy function; the second applies a local search technique to the constructed solution in hope of finding an improvement. A comprehensive survey of GRASP can be found in [73].

In [71] GRASP has been applied to a quadratic assignment problem that models the positioning of intermodal highway trailers on railcars. The GRASP is incorporated within a branch and bound algorithm to compute optimal solutions. In Li, Pardalos et al (see the paper in this volume), the GRASP has been applied to solve the general QAP. The GRASP was tested on 88 instances of QAPs (most QFD(p) = X X fijdp(i)p(j): instances, and improved on the best known solution in a few cases.

# 6. Test Problem Generation

iteria including the accuracy of the solution, the speed of t $\mathrm { Q A P s }$ orithm, and the eectiveness of the algorithm with respect to dierent problem classes. Ho $N =$ $\{ 1 , 2 , \ldots , n \}$ cult pro $( n \times n )$ existing th $\boldsymbol { F } = \left( f _ { i j } \right)$ ot it $D = \left( d _ { k l } \right)$ e measurement for the $p$ criteria. $\mathrm { N }$ nce, empirical co

$$
Q _ { F D } ( p ) = \sum _ { i } \sum _ { j } f _ { i j } d _ { p ( i ) p ( j ) } .
$$

ferences on this subject, see e.g., Pardalos [178, 179], Pardalos and Rosen [190], and Floudas and Pardalos [76]. criteria including the accuracy of the solution, the speed of the algorithm, and the effectiveness of the algorithm with respect to different problem classes. However, for many difficult problems, existing theory cannot itself provide measurement for these criteria. Hence, empirical computational experimentation is necessary. Evaluation and test of an algorithm can be done by using test problems with a known optimal solution. Test problems also provide a standard platform on which different algorithms for the same problem can be compared. For general references on this subject, see e.g., Pardalos [178, 179], Pardalos and Rosen [190], and Floudas and Pardalos [76].

6.1. Palubetskis' Generator for QAPs with a Known Solution. Next, we discuss the generation of test problems for the quadratic assignment problem. One of the first methods for constructing test problems with a known optimal permutation was proposed by Palubetskis [175]. Assume that the distance matrix is taken from a grid graph.

Input: $\pmb { w }$ , a value to initialize the $F$ matrix, and $z < w$ , to obtain random values between $[ 0 , z ]$

Output: Matrices $F$ and $D$ and an optimal permutation $p ^ { * }$

(i) Construct the matrix $D = \left( d _ { i j } \right)$ , of which the elements are the distances between the knots of the two dimensional grid $r \times s$ , where $r s = n$ , using rectilinear distances. If $( i , j )$ are neighboring knots, then $d _ { i j } = 1$   
ii Set $\begin{array} { r } { F = \left( f _ { i j } \right) } \end{array}$ where $f _ { i j } ~ = ~ w$ (an input parameter to the algorithm). Compute $g _ { i j } = 2 - d _ { i j }$   
(ii)  While for any i $j = 1 , \dotsc , n$ such that $g _ { i j } \leq 0$   
(iv) Choose the pair $l , m$ , such that $d _ { l m } = \operatorname* { m a x } \{ d _ { i j } \}$ where the max is taken over every $( i , j )$ for which $g _ { i j } \leq 0$ . If no such pair exists, then go to 8.

(ix) Output F, D and p and opti $k$ al cost w(P P dij). $l$ to $_ m$ , such that, $\mid d _ { l k } - d _ { m k } \mid \leq 1$ . Then, choose randomly, $\Delta \in [ 0 , z < w ]$ where $\pmb { w }$ and $z$ are the input parameters to the algorithm. Next, we $f _ { l m } : = \Delta , f _ { l k } : = f _ { l k } + \left( w - \Delta \right) , f _ { m k } : = f _ { m k } + \left( w - \Delta \right)$ [16 $g _ { l m } : =$ $g _ { l k } : = g _ { m k } : = 1$ , r the QAP with = w( dij). $p ^ { * } = p ^ { * } ( i ) , i = 1 , 2 , . . . , n ,$ where $P ^ { * }$ will be the optimal permutation. Form the matrix $\boldsymbol { F } = \left( c _ { i j } \right)$ proof is b $f _ { i j } = f _ { u v }$ on on t $\boldsymbol { i } = \boldsymbol { p } ^ { * } \left( \boldsymbol { u } \right)$ r of i $j = p ^ { * } ( v )$ (ix) Output $F$ $D$ and $p ^ { * }$ and optimal cost $w ( \sum \sum d _ { i j } )$

Next, we provide the proof of correctness of the above algorithm [165]. Before applying Step $\# 8$ , the identity permutation is an optimal permutation for the QAP with input data, the matrices $F$ and $D$ and the optimal cost, $C = w ( \sum \sum d _ { i j } )$

e identity permutation is optimal and the correspondi

Base: To start with, let $F ^ { ( 0 ) } = ( f _ { i j } = w )$ be the flow matrix. Obviously, for D $F ^ { ( 0 ) }$ g the (i + 1)-th iteration, let dlm = maxfdijg over all i; j $C$ u

th between l and m, i.e. dlk + $_ i$ dmk = dlm (Comment: k need n $F ^ { ( i ) }$ atisfy the condition j dlk   dmk j  1 as stated in the algorithm. $C$ t

To prove: at the end of the $( i + 1 )$ -th iteration, for the flow matrix $F ^ { ( i + 1 ) }$ the identity permutation is optimal and the corresponding cost is the same as where F^ = ( ^fi $_ i .$ -th iteration i.e., $C$

During the $( i + 1 )$ -th iteration, let $d _ { l m } = \bf { m a x } \{ { d _ { i j } } \}$ over all $i , j$ such that $g _ { i j } ~ \leq ~ 0$ ^fij = < $k$ be selected such that $k$ is on the shortest path between $l$ and $_ m$ >> $d _ { l k } + d _ { m k } = d _ { l m }$ (Comment: $k$ need not satisfy the condition $| \ d _ { l k } \ - \ d _ { m k } \ | \ \leq \ 1$ as stated in the algorithm. It is sufficient if $d _ { l k } + d _ { m k } = d _ { l m } )$ hat

$$
F ^ { ( i + 1 ) } = F ^ { ( i ) } + \hat { F } 
$$

where $\hat { F } = ( \hat { f _ { i j } } )$ and

$$
\hat { f _ { i j } } = \left\{ \begin{array} { l l } { { \pmb w } - \Delta } & { \mathrm { i f ~ } i = l \ \mathrm { a n d ~ } j = k , } \\ { { \pmb w } - \Delta } & { \mathrm { i f ~ } i = m \ \mathrm { a n d ~ } j = k , } \\ { \Delta - { \pmb w } } & { \mathrm { i f ~ } i = l \ \mathrm { a n d ~ } j = m , } \\ { 0 } & { \mathrm { o t h e r w i s e } . } \end{array} \right.
$$

It is obvious that

$$
o p t ( F ^ { ( i + 1 ) } ) \ge o p t \big ( F ^ { ( i ) } \big ) + o p t \big ( \hat { F } \big ) .
$$

Next, we provide tw $o p t { \left( { F ^ { \left( i \right) } } \right) } = C$ s constructed using the above ge $o p t ( { \hat { F } } ) =$ 0. Hence,

$$
o p t ( F ^ { ( i + 1 ) } ) \geq C .
$$

lso, the input parameters to the generator are: w = 9 and z = 3. The gener $F ^ { ( i ) }$ matrices F and D are as follows: $\hat { F }$ . Hence, the 9 3 2 1 16 $F ^ { ( i + 1 ) }$ 9 0 32 the same as at the end of the $_ i .$ 0 16 18 2 $C$

66 1 1 0 9 15 9 33 1 17 25 77

Example 1: Here, $n = 1 0$ and the grid dimensions are: $r = 5$ and $s \mathit { \Theta } = 2$ Also, the input parameters to the generator are: $w = 9$ and $z = 3$ . The generated matrices $F$ and $D$ are as follows:

For this problem, the known optimal cost is 1890 and the optimal permutation of the facilities in relation to the locations is $\left( 8 \ 2 \ 1 \ 1 0 \ 5 \ 9 \ 7 \ 4 \ 3 \ 6 \right)$ . The results obtained by our algorithm are: cost due to our algorithm is 1890, which is

66 5 13 9 15 3 2 16 24 18 2 77 (7 10 1 4 5 2 3 9 6 8).

Example 2: The grid for this example is $r = 2$ $s = 5$ and $n = 1 0$ . The input parameters to the generator are: $w = 9$ and $z = 5$ . The generated flow matrix $F$ is given below.

Optimal cost for this example is also 1890. Our algorithm cost is the same as the optimal cost and the corresponding permutation in both the cases is the identity 6.3. QAP

6.2. Li & Pardalos Generator for QAPs with a Known Solution. Li and Pardalos [150] have generalized the results of Palubetskis and constructed test problems for more general types of QAPs. Their generator includes Palubetskis' procedure [175] as a special case, in which the distance matrix is taken from a grid graph. The fortran generator described in [150] is available by e-mail from the authors (the fortran code can also be obtained by sending an e-mail message to "coap@math.ufl.edu", and in the body of the message put "send 92006").

6.3. QAP-LIB. Finally we point out that a collection of more than 130 instances of quadratic assignment problems is contained in a library called the "QAP-LIB", [39]. This library consists of two parts. The data part contains various instances given by the input matrices A, $B$ and $C$ , if $C \neq 0$ . Then there is a documentation, corresponding to [39]. This documentation is updated regularly, the last update being from February 1994. The documentation contains the following information on each of the instances: the best known feasible solution value is given, along with some information on who found it and by which method. Secondly the best currently available lower bounds on the objective function is provided. The two parts are available via anonymous ftp from ftp.tu-graz.ac.at in the directory /pub/papers/qaplib.

6.4. OR-Library. QAP instances can be also obtained from the OR-Library (o.rlibrary@ic.ac.uk) - see the file qapinfo. For details see [123]. Information about test problems for quadratic assignment problems as well as other combinatorial problems can be obtained by sending email to o.rlibrary@ic.ac.uk with the email message being the file name for the problem areas you are interested in.

# 7. Concluding Remarks

In this paper we gave a survey regarding the most recent results and applications on QAP. In addition, an up-to-date bibliography is included which includes papers on QAP and realted problems as well as applications in diverse areas.

# Appendix A. Notations

$\pmb { n }$ A permutation yielding the maxim   
$e$ The Eigenvalue bound for   
$A$ The inner produ   
$B$ ; The maximum perm   
$Q A P ( A , B )$ The minimum permuted inner product of $A$ ctors x and y $B$   
$\Pi _ { m }$ The vector obtained by   
$f ( \boldsymbol p )$ The vector obtained by reorder $Q A P ( A , B )$ ponents of x desce $p$   
$f _ { A , B } ^ { \prime }$ The transpose of the matrix A $Q A P ( A , B )$   
$f _ { A , B } ^ { * }$ e The trace of the matrix A $Q A P ( A , B )$   
$G L B ( A , B )$ The vector formed from the diagonal elements of A $Q A P ( A , B )$ $E V B ( A , B )$ The diagonal matrix formed fr $Q A P ( A , B )$   
$\langle x , y \rangle$ The set of permutation matr $\pmb { x }$ es $_ y$   
$\left. x , y \right. _ { + }$ The set of positive semidenite symmetric matric $\pmb { x }$ and $_ y$   
$\left. x , y \right. _ { - }$ The set of doubly stochastic matrices $\pmb { x }$ and $_ y$   
$x ^ { + }$ The set of orthogonal matrices $\pmb { x }$ ascendingly   
$\boldsymbol { \mathscr { x } } ^ { - }$ The set of nonnegative (elementwise) matrices $\pmb { x }$ descendingly $A ^ { t }$ The set of matrices with row $A$   
trace $A$ The set of matrices with $A$   
diag $( A )$ The vector formed from the diagonal elements of $A$   
$\mathrm { d } i a g \left( \boldsymbol { v } \right)$ References $v$   
$\Pi$ The set of permutation matrices   
$\mathcal { P }$ r natorial optimization and neural computing, John Wiley and   
$\mathcal { D }$ nd H.D. Sherali, A tight linearization and   
$\mathcal { O }$ u amming problems, Management Scien   
$\mathcal { N }$ 3 (1991), no. 2, 175{219.   
$\mathcal { E }$ nd E.S. Bua, Heuristic algorithm and simulation appro   
$\mathcal { S }$ ities, Management Science 9 (1963), 294{309.

# alysis of some

7. G. Avondo-Bodeno, Economic applications of the theory of graphs, Gordon and Breach Science Publishers, 1962.   
8. E. Balas and J.B. Mazzola, Quadratic 0-1 programming by a new linearization, Proceedings of the TIMS/ORSA (Washington D.c.), TIMS/ORSA, May 1980.   
3. R.K. Ahuja, T.L. Magnanti, and J.B. Orlin, Some recent advances in network flows, SIAM Review 33 (1991), no. 2, 175-219.   
4. G.C. Armour and E.S. Buffa, Heuristic algorithm and simulation approach to relative location of facilities, Management Science 9 (1963), 294-309.   
5. A.A. Assad and W. Xu, On lower bounds for a class of quadratic $\{ 0 , 1 \}$ programs, Operations Research Letters 4 (1985), 175-180.   
6. J.G. Augustin and J. Minker, Analysis of some graph theoretical cluster techniques, J. ACM 17 (1970), 571588.   
7. G. Avondo-Bodeno, Economic applications of the theory of graphs, Gordon and Breach Science Publishers, 1962.   
8. E. Balas and J.B. Mazzola, Quadratic O-1 programming by a new linearization, Proceedings of the TIMS/ORSA (Washington D.c.), TIMS/ORSA, May 1980.   
agement Science 35 (1989), 249{255. J.F. Bard and T.A. Feo, An algorithm for the manufact   
IIE Transactions 23 (1991), 83{92. M.S. Bazaraa and A.N. Elshafei, An ex   
11. ent problem, Naval Research Logistics Quarterly 26 (1979), 109{121. M.S. Bazaraa an   
signment problem, Naval Research Logistics Quarterly 30 (1983), 287{304. M.S. Bazaraa and H.D. Sherali, Ne   
problem, Operations Research Verfahren 32 (1979), 29{46. , Bender's partitioning scheme applied to a new formulation of the quadratic assignment proble   
20. , On the use of exact and heuristic cutting plane methods for the quadratic assignment problem, Journal of Operati   
21. G. Birko, Tres observaciones sobre el algebra lineal, Univ. Nac. Tucuman Rev. Ser. A (1946), 147{151.   
22. J. B. Blanks, Near optimal quadratic-based placement for a class of ic layout problems, IEEE Circuits and Devices (1985), 31{373.   
23. S.H. Bokhari, On the mapping problem, IEEE Transactions on Computers C-30 (1981), no. 3, 207{214.   
24. , Assignment problems in parallel and distributed computing, Kluwer Academic Publishers, Boston, 1987.   
25. eph Bowman and Fred Glover, A note on zero-one integer and concave programming, Operations Research 21 (1973), 182{183.   
26. oyd, The subtour polytope of the travelling salesman problem, Ph.D. thesis, University of Waterloo, 1986.   
27. E. Donald Brown, L. Christopher Huntley, and R. Andrew Spillance, A parallel genetic heuristic for the   
4 06-4 15, 1989. R.A. Brualdi and H.J. Ryser, Combinatoria   
New York , 19 91. P.A. Bruijs, On   
24. , European Journal of Operational Research 17 (1984), 21{30. E.S. Bua, G.C. Armour,   
Business Review 42 (1962), 136{158. R.E. Burkard, Die storungsmethode zur losung q   
ations Research Verfahren 16 (1973), 84{108. , Some recent advan   
ming, Elsevier Publishers B.V. North-Holland, 1984, pp. 53{68. R.E. Burkard, Locations with spatial interactions: the quadratic assignment problem, Discrete Locat   
34. R.E. Burkard and T. Bonniger, A heuristic for quadratic boolean programs with applications to quadrati   
(1983), 374{ 386. problem, European Journal of Operational Research 17 (1984), 21-30.   
30. E.S. Buffa, G.C. Armour, and T.E. Vollmann, Allocating facilities with CRAFT, Harvard Business Review 42 (1962), 136158.   
31. R.E. Burkard, Die störungsmethode zur lösung quadratischer zuordnungsprobleme, Operations Research Verfahren 16 (1973), 84-108.   
32. ,Some recent advances in quadratic assignment problems, Mathematical Programming, Elsevier Publishers B.V. North-Holland, 1984, pp. 53-68.   
33. R.E. Burkard, Locations with spatial interactions: the quadratic assignment problem, Discrete Location Theory (P.B. Mirchandani and R.L. Francis, eds.), John Wiley, 1991.   
34. R.E. Burkard and T. Bonniger, A heuristic for quadratic boolean programs with applications to quadratic assignment problems, European Journal of Operational Research 13 (1983), 374386.   
40. R.E. Burkard and J. Oermann, Entwurf von schreibmaschinentastaturen mittels quadratischer zuordnungsprobleme, Z. Operations Res. 21 (1977), B121{B1   
41. R.E. Burkard and F. Rendl, A thermodynamically motivated simulation procedure for combinatorial optimization problems, European Journal of Operations Research 17 (1984), 169{174.   
42. R.E. Burkard and R. Rudolf, Computational investigations on 3-dimensional axial assignment problems, Tech. report, Technische Universitat G   
in: Belgian Journal of Operations Research. R.E. Burkard, R. Rudolf, and G. Woeg   
lems with decomposable cost-coecients, Tech. Report Report 238, Technische Universitat Graz, Austria, 1992. R.E. Burkar   
salesman problems, Discrete Applied Mathematics 32 (1991), 61{76. R.E. Burkard and K.-H. Stratmann, Numerical investigations on quadratic a   
problems, Naval Research Logistics Quaterly 25 (1978), 129{148. P. Camion, Characterization of totally unimodular matrices, Proc. Amer. Math. Soc. 16 (1965), 1068{73.   
47. P. Carraresi and F. Malucelli, A new lower bound for the quadratic assignment problem, Operations Research 40 (1992), no. Supplement 1, S22{S27. P. Carraresi and F. Malucelli, A reformulat   
assignment problem, Tech. Report TR-34/92, Universita di Pisa, 1992. J. Chakrapani and J. Skorin-Kapov, A connectionist approaches to the quadratic assignment problem, Comp   
50. , A constructive method to improve lower bounds for the quadratic assignment problem, Working paper, State University of New York at Stony Bro   
51. , Massively parallel tabu search for the quadratic assignment problem, Annals of Operations Research forthcoming (1992).   
52. N. Christodes and E. Benavent, An exact algorithm for the quadrtic assignment problem, Operations Rese   
53. N. Christodes and M. Gerrard, Special cases of the quadratic assignment problem, Management Science Research Report 391, Carnegie Mellon Univ   
54. , A graph theoretic analysis of bounds for the quadratic assignment problem, Studies on graphs and discrete programming P. Hansen, ed. , North-Holland   
55. N. Christodes, A. Mingozzi, and P. Toth, Contributions to the quadratic assignment problem, European Journal of Operations Research 4 (1980), 243{247.   
56. ger C.N. Fiechter and D. de Werra, Basic ideas of tabu search with an application to traveling salesman and quadratic assignment, Ricerca Operativa 62 (1992),   
57. nnolly, An improved annealing scheme fro the qap, Journal of Operational Research 46 (1990), 93{100.   
58. K. Conrad, Das quadratische zuweisungsproblem und zwei seiner spezialfalle, MohrSiebeck, Tubingen (1971).   
59. Y. Crama and F.C.R. Spieksma, Approximation algorithms for three-dimensional assignment problems with triangle inequalities, European Journal of Operational Res   
54. _, A graph theoretic analysis of bounds for the quadratic assignment problem, Studies on graphs and discrete programming (P. Hansen, ed.), North-Holland, 1981, pp. 61-68.   
55. N. Christofides, A. Mingozzi, and P. Toth, Contributions to the quadratic assignment problem, European Journal of Operations Research 4 (1980), 243-247.   
56. A. Rogger C.N. Fiechter and D. de Werra, Basic ideas of tabu search with an application to traveling salesman and quadratic assignment, Ricerca Operativa 62 (1992), 5-28.   
57. D.T. Connolly, An improved annealing scheme fro the qap, Journal of Operational Research 46 (1990), 93100.   
58. K. Conrad, Das quadratische zuweisungsproblem und zwei seiner spezialfalle, MohrSiebeck, Tubingen (1971).   
59. Y. Crama and F.C.R. Spieksma, Approximation algorithms for three-dimensional assignment problems with triangle inequalities, European Journal of Operational Research 60 problem, Mathem   
67. A.N. Elshafei, Hospital layout as a quadratic assignment problem, O   
Quarterly 28 (1977), 167{179. R. Euler,   
Applicationes Mathematicae (Zastosowania Matematyki) XIX (1987), 375{386. B.H. Faaland and F.S. Hillier,   
procedures, Operations Research 27 (1979), 1069{1087. K. Fan, Maximum properties and inequalities for the   
operators, Proc. Nat. Acad. Sci. U.S.A. 35 (1951), 1951.   
71. T.A. Feo and J. Gonzalez-Velarde, The intermodal trailer assignment problem, Tech. report, Operations Research Group, The University of Texas at Austin, Austin,   
66. -, A branch and bound algorithm for the Koopmans-Beckman quadratic assignment T.A. Feo and M.G.C. Resende, A probabilistic heuristic for a   
set covering problem, Operations Research Letters 8 (1989), 67{71. T.A. Feo and M.G.C. Resend   
report, AT&T Bell Laboratories, Murray Hill, NJ 07974-2070, 1994. G. Finke, R.E. Burkard, and F. Rendl, Quadratic assignment problems, Annals of   
Mathematics 31 (1987), 61{82. G. Finke and E.B. Medova-Dempster, Approximation   
mization problems, Tech. report, Technical University of Nova Scotia, 1987. C.A. Floudas and P.M. Pardalos, A collection of test   
optimization algorithms, Springer-Verlag, Lecture Notes in Computer Science, No. 455, report, Operations Research Group, The University of Texas at Austin, Austin, TX R.L. Francis and J.   
N.J., 19 74. J.C.B. Frenk, M. van Houweninge, and A.H.G. Rinnoony Kan, Asy   
assignment problems, Tech. report, Erasmus University, Rotterdam, 1982. C. Friden, A. Hertz, and D. de Werra, STABULUS: A technique fo   
in large graphs with tabu search, Computing 42 (1989), 35{44. A.M. Frieze, Complexity of a   
Operations Research 13 (1983), 161{164. A.M. Frieze and J. Yadegar, an algorithm for solving 3-dimensional assign   
with application to scheduling a teaching practice, Operations Research 32 (1981), 989{ optimization algorithms, Springer-Verlag, Lecture Notes in Computer Science, No. 455, 1990.   
77. R.L. Francis and J.A. White, Facility layout and location, Prentice-Hall, Englewood Cliffs, K. Frohlich,   
sitat Koln, 1979, Masters Thesis. W. Gander, G. Golub, and U. von Matt, A constrained eigenvalue problem   
bra and its Applications 114/115 (1989), 815{839. M.R. Garey and D.S. Johnson, Computers and intractability -   
NP-completeness, W.H. Freeman and Company, 1979. J.W. Gavett and N.V. Plyter, The optima   
81. A.M. Frieze and J. Yadegar, an algorithm for solving 3-dimensional assignment problem with application to scheduling a teaching practice, Operations Research 32 (1981), 989- 995.   
82. On the quadratic assignment problem, Discrete Applied Mathematics 5 (1983), 8998.   
83. K. Fröhlich, Dreidimensionale zuordnungsprobleme, Ph.D. thesis, Math. Institut, Universität Köln, 1979, Masters Thesis.   
WGan G.Golub,anU.voMaAcora igen roble Linbra and its Applications 114/115 (1989), 815-839.   
85. M.R. Garey and D.S. Johnson, Computers and intractability - A guide to the theory of NP-completeness, W.H. Freeman and Company, 1979.   
8 J.W. Gavett and N.V. Plyter, The optimal assignment of facilities to locations by branch E. David Goldburg, Genetic algorithms in search, o Addison-Wesley Publishing Company, Inc., 1989. B. Gollan, Eigenvalue perturbations and n cal Programming Study 30 (1987), 67{81. S. Goto and E.S. Kuh, An approach to the two-dimensional placement problem in circuit layout, IEEE Transactions   
96. A. Graham, Kronecker products and matrix calculus: with applications, Halsted Press, Toronto, 1981.   
97. G.W. Graves and A.B. Whinston, An algorithm for the quadratic assignment problem,   
91. ement Science 17 (1970), 453{471.   
98. V.P. Gulati, S.K. Gupta, and A.K. Mittal, Unconstrained bivalent programming problem, European Journal of Operations Research 15 (1984), 121{1   
99. G. Gwan and L. Qi, On facet of the three index assignment polytope, Australasian Journal of Combinatorics 6 (1992), 67{87.   
100. S.W. Hadley, Continuous optimization approaches for the quadratic assignment problem, Ph.D. thesis, University of Waterloo, 1989.   
101. S.W. Hadley, F. Rendl, and H. Wolkowicz, Bounds for the quadratic assignment problem using continuous optimization techniques, Integer Programming and Com Optimization, University of Waterloo Press, 1990, pp. 237{248. , A new ematics of Operations Research 17 (1992), no. 3, 727{739. S.W. Hadley, F. Rendl, and H. Wolkowicz, and the Homan-Wielandt inequality, Linear Algebra and its Applications 58 (1992),   
1 09{1 24.   
104. M. Hall Jr., Combinatorial theory, Blaisdell Company, Waltham, MA, 1967. M. Hanan and J.M. Kurtzberg, problem, SIAM Review 14 (1972), 324{342. P. Hansen and L. Kaufman, A primal-dual a problem, Cahiers Centre Etudess Rec h. Oper 15 (1973), 327{336. J.P. Hart and A.W. Shogan, Semi-greedy heuristics: An empirical study, Operations Research Letters 6 (1987), 107{114.   
108. eey, Assigning runners to a relay team, Optimal Strategies in Sports (Amsterdam) (S.P. Ladany and R.E. Machol, eds.), North-Hollan   
103. S.W. Hadley, F. Rendl, and H. Wolkowicz, Nonsymmetric quadratic assignment problems C.H. Heider, A computationally simplied pair exchange algorithm for the quadratic assignment   
110. C. Helmberg, B. Mohar, S. Poljak, and F. Rendl, A spectral approach t and separator problems in graphs, Tech. Report CDLDO 32, Institute of Mathematics, University of Technology Graz, 1993.   
111. P.S. Hiller and M.M. Connors, Quadratic assignment algorithms and the location of indivisible facilities, Management Science 13 (1966), 42{57.   
112. F.S. Hillier, Ecient heuristic procedures for integer linear programming with an interior, Operations Research 17 (1969), 600{   
108. D.R. Heffley, Assigning runners to a relay team, Optimal Strategies in Sports (Amsterdam) (S.P. Ladany and R.E. Machol, eds.), North-Holland, Amsterdam, 1977, pp. 169-   
171.   
109. C.H. Heider, A computationally simplified pair exchange algorithm for the quadratic assignment problem, Paper 101, Center for Naval Analysis, Arlington (Va), 1972.   
110. C. Helmberg, B. Mohar, S. Poljak, and F. Rendl, A spectral approach to bandwidth and separator problems in graphs, Tech. Report CDLDO 32, Institute of Mathematics, University of Technology Graz, 1993.   
111. P.S. Hiller and M.M. Connors, Quadratic assignment algorithms and the location of indivisible facilities, Management Science 13 (1966), 42-57.   
112. F.S. Hillier, Efficient heuristic procedures for integer linear programming with an interior, Operations Research 17 (1969), 600-637.   
113. rk, NY 10016, 1987. T. Ibaraki, Theoretical comparisons of search strategies in branch-and-bound algorithms, International Journal of Computer   
120. T. Ibaraki, T. Ohashi, and F. Mine, A heuristic algorithm for mixed-integer programming problems, Mathematical Programming Study 2 (1974), 115{136. I.Gilar and M.A. Pollatschek, Layout simulation for keyboard, Behavio   
Technology 5 (1986), 273{281. B. Jansen, A note on \Lower bound   
Technology, Mathematics and Computer Science, December 1993. J.E.Beasley, Obtaining test problems using e-mail, Journal of glo   
117. R. Horn and C. Johnson, Matrix analysis, Cambridge University Press, New York, 1985.   
124. Prashnna Jog, Jung Y. Suh, and Dirk Van Gucht, Parallel genetic algorithms applied to the traveling salesman probl   
125. D.S. Johnson, C.A. Aragon, L.A. McGeoch, and C. Schevon, Optimization by simulated annealing: An experimental evaluation; Part II, Graph coloring and number partitionin   
Operations Research 39 (1991), 378{406. D.S. Johnson, C.H. Papadimitriou, and M. Yannakakis, How easy   
of Computer and System Sciences 37 (1988), 79{100. B. K. Kaku and G. L. Thompso   
problem, European Journal of Operational Res $Q A P ^ { \prime }$ 23 (1986), 382{390. B.K. Kaku, T.E. Morton, and G.L. Thompson, A heuristic algor   
layout problem, Tech. report, Carnegie Mellon University, Pittsburgh, Pa., 1989. S. E. Kari   
problem, Research Report CORR 93-15, DIMACS, Rutgers University, New Brunswick, NJ, 1993, To appear in the Proceedings of the Workshop on the Quadratic Progr   
Problem, DIMACS, 1993. N. Karmarkar, An interior-point approach to NP-complete problems { extended abstract, Contemporary Mathematics 114 (1990),   
131. R. Karp, Reducibility among combinatorial problems, Proc. Complexity of Computer Computations (R.E. Miller and J.W. Thatcher, eds.),   
132. L. Kaufman and F. Broeckx, An algorithm for the quadratic assignment problem using benders' decomposition, European Journal of Operational Research 2 (19   
133. B. Kernighan and S. Lin, An ecient heuristic procedure for partitioning graphs, Bell Systems Journal 49 (1972), 291{307.   
134. G.A.P. Kindervater and J.K. Lenstra, An introduction to parallelism in combinatorial optimization, Discrete Applied Mathematics 14 (1986), 135{156. S. Kirpatrick, C.D. Gelatti, and M.P. Vecchi, Optimization by simulated annealing, Science 220 (1983), 671{680.   
136. G.A. Kochenberger, B.A. McCarl, and F.P. Wyman, A heuristic for general integer programming, Decision Sci. 5 (1974), 36{44.   
137. T.C. Koopmans and M.J. Beckmann, Assignment problems and the location of economic activities, Econometrica 25 (1957), 53{76.   
138. J. Krarup and P.M. Pruzan, Computer-aided layout design, Mathematical Programming ben ders' decomposition, European Journal of Operational Research 2 (1978), 204-211.   
133. B. Kernighan and S. Lin, An effcient heuristic procedure for partitioning graphs, Bell Systems Journal 49 (1972), 291-307.   
134. G.A.P. Kindervater and J.K. Lenstra, An introduction to parallelism in combinatorial optimization, Discrete Applied Mathematics 14 (1986), 135-156.   
135. S. Kirpatrick, C.D. Gelatti, and M.P. Vecchi, Optimization by simulated annealing, Science 220 (1983), 671680.   
136. G.A. Kochenberger, B.A. McCarl, and F.P. Wyman, A heuristic for general integer programming, Decision Sci. 5 (1974), 3644.   
137. T.C. Koopmans and M.J. Beckmann, Assignment problems and the location of economic activities, Econometrica 25 (1957), 5376.   
138. J. Krarup and P.M. Pruzan, Computer-aided layout design, Mathematical Programming O. Leue, Methoden zur   
(1972), 154{162. Tao Li, Parallel imprecise iterative deepening   
tional J. of High Speed Computing 3 (1991), no. 1, 63{76. Y. Li, Heuristic and exact algorithms for the quadratic assignment problem,   
The Pennsylvania State University, 1992. Y. Li, P.M. Pardalos, K.   
algorithm for the quadratic assignment problem, Tech. report, AT&T Bell Laboratories, Murray Hill, NJ 07974-2070, December 1992.   
149. , Lower bounds for the quadratic assignment problem, Tech. report, AT&T Bell   
Laboratories, Murray Hill, NJ 07974-2070, April 1992, To appear in Annals of Operations man problem: A guided tour of combinatorial optimization, John Wiley & Sons, 1985.   
150. Yong Li and Panos M. Pardalos, Generating quadratic assignment test problems with known optimal p   
no. 2, 163{184. , Parallel algorithms for the quadratic assignment p   
Optimization and Parallel Computing, 177{189, Elsevier, Amsterdam, 1992, pp. 177{189. S. Lin and B. Kernighan, An eective h   
problem, Operations Research 21 (1973), 498{516. L. Lovasz, On the ratio of optimal integral and fractional covers, Discrete Mathematics 13 (1975), 391{398.   
154. ve and J. Y. Wong, On solving a one-dimensional space allocation problem with integer programming, INFOR 14 (1976), 139{143. , S   
programming, Naval Research Logistics Quarterly 23 (1976), 623{627. Robert F. Love, James G. Morris, and George O. Wesolowsky, Facilities location: Models and methods, N   
157. otschel and L. Lovasz and A. Schrijver, Geometric algorithms and combinatorial optimization, Springer-Verlag, 1988.   
158. W.L. Maxwell, The scheduling of economic lot sizes, Naval Research Logistics Quaterly 11 (1964), 89{124.   
159. E.J. McCormik, Human factors engineering, McGraw-Hill, New York, 1970. P.B. Mirchandani a   
ities: the quadratic assignment problem a review, Working Paper Ps-79-1, Rensselaer Polytechnic Institute, Troy, New York, May 1979.   
161. hlenbein, Parallel genetic algorithms, population genetics and combinatorial optimization, Proc. 3rd Conf. on Genetic Algorithms, 416-421, 1989.   
162. , Parallel genetic algorithms in optimization, to appear in informatik fachbenchle, Springer-Verlag, 1992.   
163. H. Muhlenbein, M. Gorges-Schleuter, and O. Kramer, Evolution algorithms in combinatorial optimization, Parallel Comput   
164. H. Muller-Merbach, Optimale reihenlorgen, Springer, Berlin, 1970. K.A. Murthy and   
159. E.J. McCormik, Human factors engineering, McGraw-Hill, New York, 1970.   
160. P.B. Mirchandani and T. Obata, Locational decisions with interactions between facilities: the quadratic assignment problem a review, Working Paper Ps-79-1, Rensselaer Polytechnic Institute, Troy, New York, May 1979.   
161. H. Muhlenbein, Parallel genetic algorithms, population genetics and combinatorial optimization, Proc. 3rd Conf. on Genetic Algorithms, 416-421, 1989.   
162. , Parallel genetic algorithms in optimization, to appear in informatik fachbenchle, Springer-Verlag, 1992.   
163. H. Muhlenbein, M. Gorges-Schleuter, and O. Kramer, Evolution algorithms in combinatorial optimization, Parallel Computing 7 (1988), 65-85.   
164. H. Muller-Merbach, Optim ale reihenlorgen, Springer, Berlin, 1970.   
165. K.A. Murthy and P.M. Pardalos, A polynomial-time approximation algorithm for the C.E. Nugent, T   
for the assignment of facilities to locations, Journal of Operations Research 16 (1969), signment problem, Informatica 3 (1992), no. 4, 524538.   
172. M.L. Overton, Large-scale optimization of eigenvalues, SIAM J. Optimization 2 (1992), set, Journal of Optimization and Applications 70 (1991), no. 2, 377-384.   
173. M. Padberg, On the facial structure of the set packing polyhedra, Mathematical Programming 5 (1973), 199{216.   
174. G. Palubetskis, Quadratic 0-1 optimization, Informatica 1 (1990), 89{106. G.S. Palubetskis, Generatio   
solutions (in Russian), Zh. Vychisl. Mat. Mat. Fiz. 28 (1988), no. 11, 1740{1743. C.H Papadimitriou and K. Steiglitz, Combinatorial optimization: algorithms and complexity, Prentice-Hall, Inc., Englewood Clis, NJ 07632, USA, 1982.   
177. C.H. Papadimitriou and D. Wolfe, The complexity of facets resolved, Proceedings of the Foundations Of Computer Science, 1985, pp. 74{78. P.M. Pard   
test problems, ACM Transactions on Mathematical Software 13 (1987), no. 2, 133{137. 88-120.   
actions on Mathematical Software 17 (1991), no. 1, 74{87. P.M. Pardalos and J. Cro   
Proceedin s of the Su ercom utin 1989 Conference ACM Press 1989   
181. P.M. Pardalos and S. Jha, Complexity of uniqueness and local search in quadratic 0-1 programming, Operations Research Letters (1992), 119{123.   
182. P.M. Pardalos and X. Li, Parallel branch and bound algorithms for combinatorial optimization, Supercomputer 39 (1990), 23{30.   
183. P.M. Pardalos, K.A. Murthy, and T.P. Harrison, A computational comparison of local search heuristics for solving quadratic assignment pr   
178. P.M. Pardalos, Generation of large-scale quadratic programs for use as global optimization P.M. Pardalos, K.A. Murthy, and Y. Li, Computational experience with parallel algo  
179. for solving the quadratic assignment problem, to appear in Computer Science and Operations Research: New developments in their interface   
CSTS, January 1992. P.M. Pardalos, A. Phillips, and J.B. Rosen, Topics in parallel computing in mathemati   
programming, Science Press, 1993. P.M. Pardalos and G.P. Rodgers, Parallel branch and bo   
strained quadratic 0-1 programming, Impact of Recent Advances on Operations Research ((R. Sharda et al.), ed.), North-Holland Pre   
187. , Computational aspects of a branch and bound algorithm for quadratic zero-one programming, Computing 45 (1990), 131{144. , A   
Oper. Research 19 (1992), no. 5, 363{375. P.M. Pardalos and J.B. Rosen, Methods for global concave minimization: A bibliographic survey, Siam Review 28 (1986), 367{379. CSTS, January 1992.   
185. P.M. Pardalos, A. Phillips, and J.B. Rosen, Topics in parallel computing in mathematical programming, Science Press, 1993.   
186. P.M. Pardalos and G.P. Rodgers, Parallel branch and bound algorithms for unconstrain ed quadratic O-1 programming, Impact of Recent Advances on Operations Research ((R. Sharda et al.), ed.), North-Holland Press, 1989, pp. 131-143.   
187. Computational aspects of a branch and bound algorithm for quadratic zero-one programming, Computing 45 (1990), 131-144.   
188. , A branch and bound algorithm for the maximum clique problem, Comp. and Oper. Research 19 (1992), no. 5, 363375.   
189. P.M. Pardalos and J.B. Rosen, Methods for global concave minimization: A bibliographic survey, Siam Review 28 (1986), 367-379.   
196. erskalla, The tri-substitution method for the three-multidimensional assignment problem, CORS J. 5 (1967), 71{81.   
197. , The multidimensional assignment problem, Operations Research 16 (1968), 422{ gramming is np-hard, Operations Research Letters 7 (1988), 33-35.   
198. S. Poljak, F. Rendl, and H. Wolkowicz, General relaxations and concave extensions for (0,1)-quadratic programming, Tech. report, University of   
199. M.A. Pollatschek, N. Gershoni, and Y.T. Radday, Optimization of the typewritter keyboard by computer simulation, Angewandte Informatik 10 (1976), 438{439.   
200. W.R. Pulleyblank, Mathematical Programming The State of the Art, 312{345, SpringerVerlag, 1982, pp. 312{345.   
201. A.K. Dewdney P.Z. Chinn, J. Chvatalova and N.E. Gibbs, The bandwidth problem for graphs and matrices: a survey, Journal of Graph Theory   
202. L. Qi, E. Balas, and G. Gwan, A new facet class and a polyhedral method for the threeindex assignment problem, Advance   
197. , The multidimensional assignment problem, Operations Research 16 (1968), 422- M.J.   
and-bound algorithms, McGraw-Hill, New York, 1987. $( \theta , \iota )$ aghavachari, On connections between zero-one integer programming and conca   
programming under linear constraints, Operations Research 17 (1969), 680{684. G. Reinelt, The linear ordering problem: algorithms and applications, Rese   
position in Mathematics, vol. 8, Heldermann Verlag Berlin, Berlin, 1985. S. Reiter and D.B. Rice, D   
ear integer programming problems, Management Science 12 (1966), 829{850. F. Rendl, Ranking scalar products to improve bounds for the quadratic assig   
lem, European Journal of Operations Research 20 (1985), 363{372. F. Rendl, Quadratic assignment problems on series-parallel digraphs, Zeitschrift fur Operations Research A   
209. F. Rendl and H. Wolkowicz, A projection technique for partitioning the nodes of a graph, Annals of Operations Research (1990), no. CORR 90-   
of APMOD93 conference Budapest 1993. F. Rendl and H. Wolkowicz, Applications of parametric programming and eigenval   
imization to the quadratic assignment problem, Mathematical Programming 53 (1992), position in Mathematics, vol. 8, Heldermann Verlag Berlin, Berlin, 1985.   
211. W.T. Rhee, A note on asymptotic properties of teh quadratic assigment problem, Operations Research Letters (1989), 197{200.   
212. , Stochastic analysis of the quadratic assignment problem, Manuscript, Ohio State University, Columbus, Ohio 43210, 1990.   
213. R.H. Roth, An approach to solving linear discrete optimization problems, J. Assoc. Comut. Mach. 17 1970 300{313.   
214. C. Roucairol, Aection quadratique, Ph.D. thesis, Universite Pierre et Marie Curie, Paris Annals of Operations Research (1990), no. CORR 90-20, To appear in the special issue , A reduction method for quadrat   
Verfahren 32 (1979), 183{187. imization to the quadratic assignment problem, Mathematical Programming 53 (1992), 6378.   
2. W.T.Rhee, A note on asymptotic properties of teh quadratic assigment problem, Operations Research Letters (1989), 197-200.   
212. •, Stochastic analysis of the quadratic assignment problem, Manuscript, Ohio State University, Columbus, Ohio 43210, 1990.   
2. R.H. Roth, An approach to solving linear discrete optimizatin problems, J. Assoc.Comput. Mach. 17 (1970), 300-313.   
214. C. Roucairol, Affection quadratique, Ph.D. thesis, Universite Pierre et Marie Curie, Paris VI, 1976.   
215. -, A reduction method for quadratic assignment problems, Operations Research Verfahren 32 (1979), 183187.   
222. age and M.G. Wloka, Parallelism in graph-partitioning, Journal of Parallel and Distributed Com   
223. haer and M. Yannakakis, Simple local search problems that are hard to solve, Tech. report, AT&T Bell Laboratories, 1989.   
224. age, A more portable fortran random number generator, ACM Transactions on Mathematical Software 5 (1979), 132{138.   
225. Alexander Schrijver, Theory of linear and integer programming, John Wiley and Sons, versität Graz, Austria, 1991, Masters Thesis.   
226. M. Scriabin and R.C. Vergin, Comparison of computer algorithms and visual based methods f   
227. R. Sedgewick, Permutation generation methods, Computing Surveys 9 (1977), no. 2, 137{164.   
228. S. Senju and Y. Toyoda, An approach to linear programming with 0-1 variables, Management Science 15 (1968), B196{B207.   
229. S.I. Sergeyev, A new lower bound for the quadratic assignment problem, Zh. Vychisl. Mat. Mat. Fiz. 27 (1987), no. 12, 1802{1811.   
230. C.E. Shannon, The zero-error capacity of a noisy channel, I.R.E. Transactions 3 (1956). SHARE, Computerized relative allocation o   
1 965, SDA3391 . H.D.   
thesis, Georgia Institute of Technology, Atlanta, June 1979. H.D. Sherali and P. Rajgopal, A exible polynomial time const   
heuristic for the quadratic assignment problem, Computers & Operations Research 13 (1986), n   
234. B. Simeone, An asymptotically exact polynomial time algorithm for equipartition problems, Discrete Applied Math. 14 (19   
235. , Combinatorial optimization, Lecture Notes in Mathematics, vol. 1403, SpringerVerlag, 1986.   
236. C.C. Skiscim and B.L. Golden, Optimization by simulated annealing: A preliminary   
computational study for the tsp, Proceedings of the 1983 Winter Simulation Conference, 1983.   
237. J. Skorin-Kapov, Extensions of tabu search adaptation to the quadratic assignment problem, Computers and Operations Research forthcoming.   
238. , Tabu search applied to the quadratic assignment problem, ORSA Journal on Computing 2 (1990), no. 1, 33{45. T.H.C. Smith, A comp   
and a pair exchange algorithm for the quadratic assignment problem, Man. Sci. Res. Rep. 383, Carnegie Mellon University, Pittsburgh, Pa.,   
240. berg, The backboard wiring problem: A placement algorithm, SIAM Review 3 (1961), 37{50   
241. R.J. Stern and H. Wolkowicz, Indenite trust region subproblems and nonsymmetric eigenvalue perturbations, Tech. Report CORR 92-38, University of Waterloo, Waterloo, Cana   
27. J. Skorin-Kapov, Extensions of tabu search adaptation to the quadraticassignment problem, Computers and Operations Research forthcoming.   
238. Tabu search applied to the quadratic assignment problem, ORSA Journal on Computing 2 (1990), no. 1, 3345.   
239. T.H.C. Smith, A computational comparision of an improved pair assignment algorithm and a pair exchange algorithm for the quadratic assignment problem, Man. Sci. Res. Rep. 383, Carnegie Mellon University, Pittsburgh, Pa., November 1975.   
240. L. Steinberg, The backboard wiring problem: A placement algorithm, SIAM Review 3 (1961), 3750.   
241. R.J. Stern and H. Wolkowicz, Indefinite trust region subproblems and nonsymmetric eigenvalue perturbations, Tech. Report CORR 92-38, University of Waterloo, Waterloo, Canada, 1992, to appear in SIOPT.   
Matematicky Obzor (1967), 181{191. T. E. Vollman and   
Science 12 (1966), 450{468. M. Werman, The relationship between integer and real so   
programming, Mathematical Programming 51 (1991), 133{135. D.H. West, Algor   
ACM Transactions on Mathematical Software 9 (1983), 461{466. D.J. White, A parametric-based heuristic program for the quadratic assignme   
Naval Research Logistics Quaterly 40 (1993), no. 4, 553{568. B. Whitehead and M. Z. Elders, An approach to the optimum layout of single-story buildings, Architect's Journal 139 (1964), 13   
253. M.R. Wilhelm and T.L. Ward, Solving quadratic assignment problems by simulated annealing, IEEE Transactions 19 1987   
254. W.S. Wong and R.J.T. Morris, A new appraoch to choosing initial points in local search, Information Processing Lett   
249. M. Werman, The relationship between integer and real solutions of constrained convex P.M. Pardalos Department of Industrial and Systems Engi   
Florida Gainesville FL 32611 USA and Technical University of Crete Greece ACM Transactions on Mathematical Software 9 (1983), 461-466.   
251. D.J. White, A parametric-based heuristic program for the quadratic assignment problem, Naval Research Logistics Quaterly 40 (1993), no. 4, 553-568.   
(F. Rendl) Technische Universitat Graz, Institut fur Mathematik, Kopernikusbuildings, Architect's Journal 139 (1964), 1373-1380.   
253. M.R. Wilhelm and T.L. Ward, Solving quadratic assignment problems by simulated annealing, IEEE Transactions 19 (1987), no. 1, 107-119.   
(H. Wolkowicz) University of Waterloo, Department of Combinatorics and Optition, Waterloo, Ontario, Canada (P.M. Pardalos) DepArtmeNt oF IndustRiaL And SystEMs EngineERIng, University OF   
FLoridA, GainesviLle, FL 32611 USA And TechnicAL University Of CretE, Greece E-mail address, P.M. Pardalos: pardalos@math.ufl.edu (F. Rendl) TEchNische Universitat GRAz, Institut fuR MatheMatik, KopErnikus  
GASSA 24, A-8010 GRAZ, AuSTRIA E-mail address, F. Rendl: rendl@ftug.dnet.tu-graz.ac.at (H. Wolkowicz) University oF WaterLoo, Department of ComBinatorics And OptI  
MIZaTION, WaTERLOO, ONTARiO, CanaDa E-mail address, H. Wolkowicz: hwolkowicz@orion.uwaterloo.ca