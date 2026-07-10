# Hyperbolic Fixed Points are Typical in the Space of Mixing Operators for the Infinite Population Genetic Algorithm

Christina Hayes Department of Mathematical Sciences Montana State University Bozeman, Montana 59717-2400 hayes@math.montana.edu

Toma´sˇ Gedeon∗   
Department of Mathematical Sciences Montana State University Bozeman, Montana 59717-2400   
gedeon@math.montana.edu

# ABSTRACT

We study an infinite population model for the genetic algorithm, where the iteration of the algorithm corresponds to an iteration of a map $G$ . The map $G$ is a composition of a selection operator and a mixing operator, where the latter models effects of both mutation and crossover. We examine the hyperbolicity of fixed points of this model. We show that for a typical mixing operator all the fixed points are hyperbolic.

# Categories and Subject Descriptors

I.2.8 [Artificial Intelligence]: Problem Solving, Control Methods, And Search - Genetic Algorithms

# General Terms

Algorithms, Artificial Intelligence

# Keywords

Genetic algorithm, mixing, generic, typical, hyperbolic fixed point.

# 1. INTRODUCTION

In this paper we consider a dynamical systems model of the genetic algorithm (GA). This model was introduced by Vose (see [10]) by replacing finite population by population densities modelling an infinite population. The model is further extended in [3], [6], [7], and [9]. Although the precise correspondence between behavior of such infinite population Genetic Algorithm and the behavior of the GA for finite population has not been established in detail, the infinite population model has the advantage of being a well defined dynamical system. Therefore, the techniques of dynamical systems theory can be used to formulate and hopefully answer some fundamental questions about the GA. One such question is the question of convergence. For plausible crossover, mutation and selection 1, does the algorithm always converge to a unique solution for all initial states? In the infinite population model, the iterations of the GA are represented as iterations of a fixed map $G$ on a space of admissible population densities $p$ . Thus, the question of convergence can be reformulated in this setting as existence of a globally attracting stable fixed point, that is, a population $p _ { 0 }$ such that $G ( p _ { 0 } ) = p _ { 0 }$ .

The fixed points, $p _ { 0 }$ such that $G ( p _ { 0 } ) = p _ { 0 }$ , are fundamental objects of interest in our study. The behavior of the map $G$ in the neighborhood of $p _ { 0 }$ is determined by the eigenvalues of the linearization $D G ( p _ { 0 } )$ . If all the eigenvalues have absolute value less than one, then all iterates starting near $p _ { 0 }$ converge to $p _ { 0 }$ . If there is at least one eigenvalue with absolute value greater than one, then almost all iterates will diverge from $p _ { 0 }$ [4]. Such classification is, however, possible only if no eigenvalues lie on the unit circle in the complex plain. Fixed points $p _ { 0 }$ , for which $D G ( p _ { 0 } )$ has this property, are called hyperbolic. If at least one eigenvalue of $D G ( p _ { 0 } )$ has modulus 1, the fixed point is non-hyperbolic.

It is easy to see that hyperbolicity is an open condition, i.e. if a fixed point is hyperbolic, then all small perturbations of the map $G$ will still admit a fixed point with eigenvalues off the unit circle. It follows that for sufficiently large finite population, the GA will also admit a fixed point. Thus, hyperbolic fixed points under $G$ predict behavior for finite population GA.

On the other hand, non-hyperbolic fixed points can disappear under arbitrarily small perturbations. If the infinite population model wants to be a viable model of the behavior of the finite population GA, non-hyperbolic fixed points should be rare. It is clear that they must be present for some admissible maps $G$ , since they occur when a fixed point bifurcates. Vose and Eberlein [6] considered a class of mappings $G$ that were a composition of a mutation and crossover operator, with proportional selection scheme. The set of fitness functions was parameterized by the positive orthant. They have shown that for an open and dense set of such fitness functions, the corresponding operator, $G$ , has

hyperbolic fixed points.

In this contribution we consider a class of mappings $G =$ $M \circ F$ where $F ^ { \prime }$ is arbitrary, but fixed, selection operator and $M$ is a mixing operator from a class described in section 2. The class of mixing operators we consider include all mixing operators that are a composition of the mutation a selection operators as described in Reeves and Rowe [3] and Vose [6]. We show that for an open and dense set of mixing operators, the corresponding operator $G$ has hyperbolic fixed points.

Due to length limitations we will not provide complete proofs. Instead, we give outlines of proofs to introduce the reader to the main structure of the arguments involved. For more details please see [1]. We start with a preliminary section introducing notation and the specifics of the map $G$ .

# 2. PRELIMINARIES

The dynamical systems model of the genetic algorithm provides an attractive mathematical framework for investigating the properties of GAs. In this paper we study the model introduced by Vose [6].

The genetic algorithm searches for solutions in the search space $\Omega = \{ 1 , 2 , \dots n \}$ ; each element of $\Omega$ can be thought of as a ”species.” We consider a total population of size $r$ with $r \ > > \ n$ . We represent such a population as an incidence vector:

$$
v = ( v _ { 1 } , v _ { 2 } , . . . , v _ { n } )
$$

where $v _ { i }$ is the number of times the species $i$ appears in the population. It follows that $\textstyle \sum _ { i } v _ { i } = r$ . We associate each Ppopulation with a probability distribution over $\Omega$ . That is, a population is identified with the population incidence vector

$$
p = ( p _ { 1 } , p _ { 2 } , . . . , p _ { n } )
$$

where $\begin{array} { r } { p _ { i } = \frac { v _ { i } } { r } } \end{array}$ is the proportion of the $_ i$ -th species in the population. In this representation, the iterations of the genetic algorithm yield a sequence of vectors $p \in \Lambda$ where

$$
\Lambda = \{ ( x _ { 1 } , x _ { 2 } , . . . , x _ { n } ) \in \mathbb { R } ^ { n } | \sum x _ { i } = 1
$$

and $x _ { i } \geq 0$ for all $i = 1 , \ldots , n \}$ .

Note that $\Lambda \subset \mathbb { R } ^ { n }$ is the unit simplex in $\mathbb { R } ^ { n }$ . Not every point $x \in \Lambda$ corresponds to a population incidence vector $p$ , since these have non-negative rational entries with denominator $r$ . However, as the population size $r$ gets arbitrarily large, population incidence vectors become dense in the simplex. Thus $\Lambda$ may be viewed as a set of admissible states for infinite populations.

Let $G ( \boldsymbol { p } )$ represent the action of the genetic algorithm on $p \in \Lambda$ , where $G : \Lambda \mapsto \Lambda$ is a differentiable map ([6]). The map $G$ is a composition of three operators: selection, mutation, and crossover. We will now describe each of these in turn.

We let $F \colon \Lambda \mapsto \Lambda$ represent the selection operator. There are many possible models for the selection operator and our results do not depend on this choice of selection operator. Possible choices include proportional, tournament, or rank selection (see [6]). The $_ i$ -th component, $F _ { i } ( p )$ represents the probability that an individual of type $i$ will result if selection is applied to $p \in \Lambda$ . We extend the domain of definition of $F ^ { \prime }$ to the positive orthant in $\mathbb { R } ^ { n }$ , $\mathbb { R } ^ { n + }$ and define $F : \mathbb { R } ^ { n + } \mapsto \Lambda$ by

$$
F ( x ) : = \frac { F ( x ) } { \sum _ { i } F _ { i } ( x ) } .
$$

We let $U : \Lambda \mapsto \Lambda$ represent mutation with a positive mutation rate. Here $U$ is a matrix with $U _ { i j } ~ > ~ 0$ for all $i , j$ , where $U _ { i j }$ represents the probability that item $j \in \Omega$ mutates into $i \in \Omega$ . That is, $U _ { k } ( p )$ is the probability an individual of type $k$ will result after applying mutation to population $p$ .

Let crossover, $C : \Lambda \mapsto \Lambda$ , be defined by

$$
\boldsymbol { C } ( \boldsymbol { p } ) = ( \boldsymbol { p } ^ { T } \boldsymbol { C } _ { 1 } \boldsymbol { p } , \dots , \boldsymbol { p } ^ { T } \boldsymbol { C } _ { n } \boldsymbol { p } )
$$

for $p \in \Lambda$ , where $C _ { 1 } , \ldots , C _ { n }$ is a sequence of symmetric non-negative matrices. Here $C _ { k } ( p )$ represents the probability that an individual $k$ is created by applying crossover to population $p$ . Recall that an operator $A : \mathbb { R } ^ { n } \mapsto \mathbb { R } ^ { n }$ is quadratic if there exist matrices $A _ { 1 } , A _ { 2 } , \ldots , A _ { n }$ such that $A ( x ) = ( x ^ { T } A _ { 1 } x , \ldots , x ^ { T } A _ { n } x )$ . We denote a quadratic operator with its corresponding matrices as $A = \left( A _ { 1 } , \ldots , A _ { n } \right)$ . Thus $C = ( C _ { 1 } , \ldots , C _ { n } )$ is a quadratic operator ([5]).

We combine mutation and crossover to obtain the mixing operator $M = C \circ U$ . Thus the $k$ -th component of the mixing operator

$$
M _ { k } ( p ) = p ^ { T } ( U ^ { T } C _ { k } U ) p
$$

represents the probability that an individual of type $k$ will result after applying mutation and crossover to population $p$ . Observe that mixing is also a quadratic operator from $\Lambda$ to $\Lambda$ ([5]). This motivates the definition of a mixing operator. Let $\mathcal { A } ^ { n \times n }$ represent the set of $n \times n$ matrices with real valued entries. We call a quadratic operator, $M = ( M _ { 1 } , \ldots , M _ { n } )$ , a mixing operator if the following properties hold:

Let $\mathcal { M }$ be the set of quadratic operators $M$ satisfying (1)- (3). Observe that $M \in \mathcal { M }$ maps $\Lambda$ to $\Lambda$ . This is easily seen since, for $x \in \Lambda$ , $M ( x ) = ( x ^ { T } M _ { 1 } x , \ldots , x ^ { T } M _ { n } x )$ , and

$$
\begin{array} { l } { \displaystyle \sum _ { k } [ M ( x ) ] _ { k } = { x ^ { T } } \left( \sum _ { k } M _ { k } \right) x = { x ^ { T } } \cdot \left( \sum x _ { i } , \sum x _ { i } , . . . , \sum x _ { i } \right) } \\ { \displaystyle = { x ^ { T } } \cdot ( 1 , . . . , 1 ) = 1 . } \end{array}
$$

Finally, we define

$$
G = M \circ F , { \mathrm { ~ f o r ~ } } M \in { \mathcal { M } }
$$

to be the complete operator for the genetic algorithm, or a GA map.

In addition to the above model, the following notation and terminology will be used. For an $n \times n$ matrix $A$ , let $d e t ( A )$ denote the determinant of the matrix $A$ . The characteristic polynomial for the matrix $A$ is denoted $d e t ( A - \lambda I )$ , where $I$ is the $n \times n$ identity matrix. The eigenvalues of a matrix are the roots of $d e t ( A - \lambda I )$ . We call an eigenvalue simple if it is a root of $d e t ( A - \lambda I )$ with multiplicity one. Let $s p e c ( A )$ denote the set of eigenvalues of $A$ . A matrix $A$ is symmetric if $A _ { i j } = A _ { j i }$ for all $i , j$ . The transpose of a matrix $A$ is denoted $A ^ { T }$ . We use the notation $A > 0$ to indicate that $A _ { i j } ~ > ~ 0$ for all $_ { i j }$ . For a matrix $A$ , $r a n k ( A )$ denotes the dimension of the range of $A$ , or the number of linearly independent columns of the matrix. Let $\| A \|$ denote the norm of the matrix $A$ . Let $S ^ { 1 }$ denote the unit circle in $\mathbb { C }$ .

# 3. MAIN RESULTS

Before we present the main result, we introduce key definitions.

Definition 1. If $f ( p ) = p$ , a point $p$ is called a fixed point of $f$ .

Definition 2. A fixed point p for $f : \mathbb { R } ^ { n } \mapsto \mathbb { R } ^ { n }$ is called hyperbolic if the Jacobian $D f ( p )$ has no eigenvalues on the unit circle. A fixed point $p$ is non-hyperbolic if spe $: ( D f ( p ) ) \cap$ $S ^ { 1 } \neq \emptyset$ .

Definition 3. A map $G$ is hyperbolic if all fixed points are hyperbolic.

Definition 4. A property is typical, or generic, if it holds for an open and dense set of parameter values.

We now present our main result.

Theorem 1. Let $G = M \circ F$ be a GA map (1). For $a$ typical mixing operator, $G$ is hyperbolic.

To prove the above theorem, we will need the following two propositions.

Proposition 1. Let $G = M \circ F ^ { \prime }$ be a GA map (1). The set of mixing operators $M$ , for which the fixed points of $G$ are hyperbolic, forms an open set in $\mathcal { M }$ .

The proof of this proposition is based on the fact that

$$
d e t ( D G ( p ) - \lambda I ) = d e t ( [ D M \circ F ( p ) ] D F ( p ) - \lambda I )
$$

is a continuous function of $M$ and, therefore, if $\lambda _ { i } ~ \notin ~ S ^ { 1 }$ , then small perturbations do not change this fact. The proof of proposition 1 is relatively easy. The proof of the following proposition, 2, is considerably more difficult.

Proposition 2. Let $G = M \circ F ^ { \prime }$ be a GA map (1). The set of mixing operators for which the fixed points of $G$ are hyperbolic, forms a dense set in $\mathcal { M }$ .

To prove this proposition, we will assume we have a fixed point $p$ of $G$ with one or more eigenvalues on $S ^ { 1 }$ . We first characterize perturbations, $M _ { \epsilon } \in \mathcal { M }$ , that preserve the fixed point.

We construct ${ \mathcal { P } } ( { \boldsymbol { p } } )$ to simplify the characterization of the perturbations of $M$ with the fixed point preserving characteristic. Let $\mathcal { P } ( \boldsymbol { p } )$ represent quadratic operators

$$
P = ( P _ { 1 } , \ldots , P _ { n } )
$$

for which the following properties hold:

1. $P _ { i } \in \mathcal { A } ^ { n \times n }$ is symmetric for all $i = 1 , \ldots , n$ ;

2. $M _ { i } \pm P _ { i } > 0$ ;

3. $\textstyle \sum _ { i } P _ { i } = \mathbf { 0 }$

4. $[ F ( p ) ] ^ { T } P _ { i } F ( p ) = 0$ where $p$ is the fixed point.

It is easy to see that $\mathcal { P } ( p ) \neq \emptyset$ .

For $P \in { \mathcal { P } } ( p )$ , let $M _ { \epsilon } : = M + \epsilon P$ . In Lemma 1 we show that $M _ { \epsilon }$ is a quadratic operator on $\Lambda$ and $M _ { \epsilon } \in \mathcal { M }$ . Therefore, $G _ { \epsilon } = M _ { \epsilon } \circ F$ is a $G A$ map.

Lemma 1. Let $G = M \circ F$ be a GA map (1). Assume $p \in \Lambda$ has $G ( p ) = p$ . If $P \in { \mathcal { P } } ( p )$ , then for sufficiently small $\epsilon > 0$ , $M _ { \epsilon } = M + \epsilon P$ satisfies

1. $M _ { \epsilon } \in \mathcal { M }$

2. $G _ { \epsilon } ( p ) = M _ { \epsilon } \circ F ( p ) = p$ .

That is, $G ( p ) = p = G _ { \epsilon } ( p )$ .

We observe that

$$
\begin{array} { r c l } { } & { } & { G _ { \epsilon } = M _ { \epsilon } \circ F } \\ { } & { } & { = ( M + \epsilon P ) \circ F } \\ { } & { } & { = ( M \circ F ) + \epsilon ( P \circ F ) } \\ { } & { } & { = G + \epsilon ( P \circ F ) . } \end{array}
$$

Thus,

$$
\begin{array} { c } { { D G _ { \epsilon } ( p ) = D [ G + ( \epsilon P \circ F ) ] ( p ) } } \\ { { \mathrm { } } } \\ { { \mathrm { } = D G ( p ) + H } } \end{array}
$$

where $H \in { \mathcal { A } } ^ { n \times n }$ . In order to trace the effects of perturbations of $M$ on the derivative $D G _ { \epsilon }$ , we define

$$
\mathcal H = \{ H \in \mathcal A ^ { n \times n } | H = D ( P \circ F ) ( p ) \mathrm { ~ f o r ~ } P \in \mathcal P ( p ) \}
$$

Observe that conditions (3) and (4) for defining the class ${ \mathcal { P } } ( p )$ restrict the admissible set of perturbations $P$ . It can be shown that this restriction implies that each $H \in { \mathcal { H } }$ has rank at most $n - 1$ . Therefore, we can only perturb $s p e c ( D G ( p ) )$ in $n - 1$ directions. This makes the proof of density non-trivial.

Lemma 2. Let $G = M \circ F$ be a $G A$ map (1). Assume $G ( p ) = p$ for $p \in \Lambda$ , and that $D G ( p )$ has at most one simple eigenvalue $\lambda _ { 0 }$ of norm one. Then, there exists $M _ { \epsilon } \in \mathcal { M }$ such that $G _ { \epsilon } ( p ) = p$ and spec $\because [ D G _ { \epsilon } ( p ) ] \cap { \mathcal { S } } ^ { 1 } = \emptyset$ .

To find this perturbation, we consider $D G ( p )$ in the Jordan normal form, denoted $[ D G ( p ) ] _ { J }$ . The class of matrices $\mathcal { H }$ becomes the class $\mathcal { H } _ { J }$ in the new basis. We find $H _ { J } \in \mathcal { H } _ { J }$ , such that $s p e c ( D G ( p ) J + H J ) \cap { \mathcal { S } } ^ { \perp } = \emptyset$ . Since $s p e c ( D G ( p ) \ j + H \ j ) = s p e c ( D G ( p ) + H )$ , we then calculate $H$ corresponding to $H _ { J }$ to determine the appropriate $M _ { \epsilon } \in \mathcal { M }$ .

For repeated eigenvalues, the argument showing $H _ { J }$ exists becomes very complicated. In this case we address collections of eigenvalues on $S ^ { 1 }$ of multiplicity greater than one through use of the lemmas below.

Lemma 3. Let $G = M \circ F$ be a $G A$ map (1) with fixed point $p$ . If $D G ( p )$ has eigenvalue $\lambda _ { 0 } \in \mathcal { S } ^ { 1 }$ and multiplicity $k > 1$ , then there exists $P \in { \mathcal { P } } ( p )$ such that $D G _ { \epsilon } ( p )$ has eigenvalue $\lambda _ { 0 } \in S ^ { 1 }$ with multiplicity at most 1.

The rank of the perturbation matrix $H$ plays a critical role in the proof of Lemma 3.

Lemma 4. Let $G \ : = \ : M \circ F$ be a $G A$ map (1). There exists a perturbation $M _ { \epsilon } \in \mathcal { M }$ of $M$ with $G _ { \epsilon } = M _ { \epsilon } \circ F$ and $D G _ { \epsilon } ( p ) = D G ( p ) + H$ such that $H$ is of rank $n - 1$ .

That such an $H$ exists can be shown by explicitly forming an operator $P \in \mathcal { P }$ so that the corresponding $H \in \mathcal { H }$ has $r a n k ( H ) = n - 1$ .

Lemma 5. Let $G = M \circ F$ be a GA map (1). For each $H \in \mathcal { H }$ there exists an interval $[ 0 , \delta _ { H } ]$ , $\delta _ { H } > 0$ , such that for all $\delta \in [ 0 , \delta _ { H } ]$ , $\delta H \in \mathcal H$ .

We finally prove Lemma 3 using the analytic function $g ( c ) = d e t ( D G ( p ) - \lambda _ { 0 } I + c H )$ in combination with the results of Lemma 5.

Recall that $\lambda _ { 0 } ~ \in ~ { \mathcal { S } } ^ { 1 }$ is the eigenvalue of $D G ( p )$ with multiplicity $k \ > \ 1$ . Since the polynomial $g : \mathbb { R } \mapsto \mathbb { C }$ , $g ( c ) = d e t ( D G ( p ) - \lambda _ { 0 } I + c H )$ , defines an analytic function in $c$ , either

2. $g ( c )$ has isolated zeros ([2]).

By Lemma 4, we can choose $H$ to have rank $n - 1$ . Thus 0 is a simple eigenvalue of $H$ . For large values of $c$ , we have $0 \in s p e c ( c H )$ but for $\mu \in [ s p e c ( c H ) \backslash \{ 0 \} ]$ , $| \mu | > K$ for some large $K$ . If $\| D G ( p ) \| < < K$ , then we can view $D G ( p )$ as a small perturbation of $c H$ . Two possibilities arise:

(a) There exists $c \in \mathbb R$ such that $g ( c ) = d e t ( c H + D G ( p ) -$ $\lambda _ { 0 } I ) \neq 0$ . (b) ${ \mathrm { ~ \ G r ~ a l l ~ } } c \in \mathbb { R } , g ( c ) = d e t ( c H + D G ( p ) - \lambda _ { 0 } I ) = 0 .$

Case (a) implies (2), i.e. $g$ has isolated zeros. Since $g ( 0 ) = 0$ , there is $\delta$ arbitrarily close to 0 such that $g ( \delta ) \neq 0$ . The proof now follows from Lemma 5. In case (b), we note that since $H$ had the simple eigenvalue $_ 0$ , $\lambda _ { 0 }$ must be a simple eigenvalue of $( c H + D G ( p ) )$ for large $c$ . This proves Lemma 3 in case (b).

# 4. CONCLUSIONS

This paper investigates the hyperbolicity of fixed points for the infinite population genetic algorithm as represented by the GA map(1). We show that for an open and dense set of mixing operators in $\mathcal { M }$ , the fixed points of the GA map are hyperbolic. This implies that for most mixing operators the behavior of the infinite population model in the neighborhood of fixed points is a good predictor of the behavior of finite, but large, population models. In particular, for most mixing operators these fixed points perturb into fixed points of the finite population model, and furthermore, the stability properties of the fixed points in infinite and finite population models are the same.

With the exceptional set of those mixing operators for which these statements are not true is nowhere dense. This means, in particular, that an arbitrarily small perturbation of such exceptional mixing operators leads to a regular operator.

Since the local dynamics around fixed points perturbs from infinite population model to a finite population model, we conclude that the GA map can serve as a good approximation of the finite population model.

# 5. REFERENCES

[1] C. Hayes and T. Gedeon. Hyperbolic fixed points are typical in the space of mixing operators for the infinite population genetic algorithm. Technical Report, http://www.math.montana.edu/∼gedeon/gen alg.html.   
[2] S. Lang. Complex Analysis. Springer, 4th edition, 1999.   
[3] C. R. Reeves and J. E. Rowe. Genetic Algorithms - Principles and Perspectives: A Guide to GA Theory. Kluwer Academic Publishers, 2003.   
[4] C. Robinson. Dynamical Systems: Stability, Symbolic Dynamics and Chaos. CRC Press, 1995.   
[5] J. E. Rowe, M. D. Vose, and A. H. Wright. Group properties of crossover and mutation. Evolutionary Computation, 10(2):151–184, 2002.   
[6] M. D. Vose. The Simple Genetic Algorithm: Foundations and Theory. The MIT Press, 1999.   
[7] M. D. Vose and A. H. Wright. Simple genetic algorithms with linear fitness. Evolutionary Computation, 2(4):347–368, 1994.   
[8] A. H. Wright and G. Bidwell. A search for counterexamples to two conjectures on the simple genetic algorithm. Foundations of Genetic Algorithms 4, Morgan Kaufman Publishers, 1997.   
[9] A. H. Wright and J. E. Rowe. Continuous dynamical systems models of steady-state genetic algorithms. Foundations of Genetic Algorithms, 6, Morgan Kaufmann, 2001.   
[10] A. H. Wright and M. D. Vose. Stability of vertex fixed points and applications. Foundations of Genetic Algorithms 3, Morgan Kaufman Publishers, 1995.