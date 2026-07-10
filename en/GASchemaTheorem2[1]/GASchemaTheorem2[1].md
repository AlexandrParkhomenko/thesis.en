# Holland’s GA Schema Theorem

v Objective – provide a formal model for the effectiveness of the GA search process.   
v In the following we will first approach the problem through the framework formalized by Holland [1] and popularized by Goldberg [2].   
v This concentrates on providing a model for the expectation of schema survival, where this naturally represents a limitation in itself.   
v We will then move on to consider further drawbacks of the original ‘Schema Theorem’ and some of the recent attempts to provide more representative Schema Theorems.

v Consider the case of a canonical GA,

ÿ Binary alphabet;   
ÿ Fixed length individuals of equal length, $l$ ;   
ÿ Fitness Proportional Selection;   
ÿ Single Point Crossover;   
ÿ Gene wise mutation.

v Definition 1 – Schema, $H$ .

A schema is a subset of the space of all possible individuals for which all the genes match the template for schema $H$ .

If A denotes the alphabet of gene alleles then $A \prod ^ { * }$ is the schema alphabet, where \* is the ‘wild card’ symbol matching any allele value.

E.g. for the binary alphabet $A \supseteq \{ 0 , 1 , ^ { * } \} \mathrm { w h e r e } ^ { * } \iint \{ 0 , 1 \}$

# Example

v For a binary individual with the gene sequence $\{ 0 \ 1 \ 1 \ 1 \ 0 \ 0 \ 0 \}$ , then it follows that one (of many) matching schema might have the form, $\mathrm { H } = [ ^ { * } \mathrm { ~ 1 ~ 1 ~ } ^ { * } \mathrm { ~ 0 ~ } ^ { * } \mathrm { ~ } ^ { * } ]$

v The schema $\mathrm { H } = [ 0 \ 1 ^ { * } \ 1 \ ^ { * } ]$ identifies the chromosome set,

$$
\begin{array} { c c c c c } { { 0 } } & { { 1 } } & { { 0 } } & { { 1 } } & { { 0 } } \\ { { } } & { { } } & { { } } & { { } } & { { } } \\ { { 0 } } & { { 1 } } & { { 0 } } & { { 1 } } & { { 1 } } \\ { { } } & { { } } & { { } } & { { } } & { { } } \\ { { 0 } } & { { 1 } } & { { 1 } } & { { 1 } } & { { 0 } } \\ { { } } & { { } } & { { } } & { { } } & { { } } \\ { { 0 } } & { { 1 } } & { { 1 } } & { { 1 } } & { { 1 } } \end{array}
$$

v Needless to say, not all schema are created equal, thus, $1 * * * * * *$ does not tell us as much as $0 ~ 1 ^ { * * } 1 ~ 1 ~ 0$ .

Moreover, schema $1 * * * * * 0$ spans the entire length of an individual whereas $1 * 1 * * * *$ does not.

v Definition 2 – Schema Order, $o ( H )$ .

Schema order, $o ( \cdot )$ , is the number of non ‘\*’ genes in schema $H$ . Example,   
ß $o ( ^ { * * * } { } ^ { * } 0 ^ { * * * } { } ^ { * } ) = 1$

v Definition 3 – Schema Defining Length, $\textstyle \prod H$ .

Schema Defining Length, $\mathbb { U } H )$ , is the distance between first and last non ‘\*’ gene in schema H.   
Example,   
ß $\prod ( ^ { * } * * * 0 * * * ) = 4 - 4 = 0$

v Note

For cardinality, $k$ , there are $( k + 1 ) ^ { l }$ schema in string of length $\mathbf { \epsilon } ^ { 6 } l ^ { 5 }$ .

We are now in a position to incrementally introduce the effect of the various selection and search operators associated with the above definition for the special case of a canonical GA with binary genes.

# Selection Operators – Fitness Proportional Selection

Essentially all that we are attempting to model is the probability that individual, $h$ , samples schema, $H .$ , or

$$
\mathrm { P } ( h \bigsqcup H )
$$

v There are several ways of modeling this.

Consider the following two part model,

ß Probability of selection number of instances of schema $H$ in the population; ß Probability of selection average fitness of schema $H$ relative to the average fitness of all individuals in the population.

Thus,

(Number of individuals matching (Mean fitness of individuals matching ${ \mathrm { P } } ( h \bigsqcup H ) =$ schema $H$ at generation t) schema H)

$$
\mathrm { o r , } \qquad \mathrm { P } ( h \sqcap H ) = \frac { m ( H , t ) f ( H , t ) } { M \bar { f } ( t ) }
$$

where $m ( H , t )$ is the number of instances of schema $H$ at generation $t$

v Lemma 1 – Under fitness proportional selection the expected number of instances of schema $H$ at time $t$ is,

$$
\operatorname { E } [ m ( H , t + 1 ) ] = M \prod \operatorname { P } ( h \prod H ) = { \frac { m ( H , t ) f ( H , t ) } { { \bar { f } } ( t ) } }
$$

v Implication,

Schemas with fitness greater (lower) than the average population fitness are likely to account for proportionally more (less) of the population at the next generation. Strictly speaking for accurate estimates of expectation and probability the population size should be infinite.

# Search Operators – Single point crossover

Reproduction does nothing to improve the fitness of individuals in a population. (Single point) Crossover was the first of two search operators introduced to modify the distribution of schema in the population. In his original work, Holland concentrated on modeling the lower bound alone [1].

v Consider the following individual, $h$ , two matching schema, $H _ { I }$ , $H _ { 2 }$ and crossover point between $3 ^ { \mathrm { r d } }$ and $4 ^ { \mathrm { t h } }$ gene, or,

<table><tr><td>h = 1</td><td>0</td><td>1</td><td>1 1</td><td>0</td><td>0</td></tr><tr><td>H1 =</td><td>* 0</td><td>1</td><td>* *</td><td>*</td><td>0</td></tr><tr><td>H2 =</td><td></td><td>1</td><td>*</td><td>*</td><td>*</td></tr><tr><td></td><td>* 0</td><td></td><td>*</td><td></td><td></td></tr></table>

v Observations,

Schema $H _ { I }$ will naturally be broken by the location of the crossover operator unless the second parent is able to ‘repair’ the disrupted gene.   
Schema $H _ { 2 }$ emerges unaffected and is therefore independent of the second parent.   
Schema with long defining length are more likely to be disrupted by single point crossover than schema using short defining lengths.

v Lemma 2 – Under single point crossover, the (lower bound) probability of schema $H$ surviving at generation $t$ is,

$$
\mathrm { P } ( H { \mathrm { ~ s u r v i v e s } } ) = 1 - \mathrm { P } \left( H { \mathrm { ~ d o e s ~ n o t ~ s u r v i v e } } \right)
$$

$$
\mathrm { o r } , \qquad 1 \bigtriangledown \frac { \widehat { \mathcal { \textbf { l } } } H ) } { l \bigtriangledown 1 } P _ { \mathit { d i f f } } ( H , t )
$$

Where $P _ { \mathit { d i f f } } ( H , t )$ is the probability that the second parent does not match schema $H$ ; and $p _ { c }$ is the a priori selected threshold of applying crossover.

v Comment,

In the special case of the worst case lower bound $P _ { \mathit { d i f f } } ( H , t ) = 1$ .

# Search Operators – Gene wise Mutation

v Mutation is applied gene by gene.

v In order for schema $H$ to survive, all non \* genes in the schema much remain unchanged.

v Probability of not changing a gene is,

$$
( 1 - p _ { m } )
$$

v Require that all $o ( H )$ non \* genes survive, or

$$
( 1 - p _ { m } ) ^ { o ( H ) }
$$

Typically the probability of applying the mutation operator, $p _ { m } , < < 1$ , thus

$$
( 1 - p _ { m } ) ^ { o ( H ) } \bigcup 1 - o ( H ) p _ { m }
$$

Lemma 3 – Under gene wise mutation, the (lower bound) probability of an order $o ( H )$ schema $H$ surviving at generation $t$ is,

$$
1 - o ( H ) p _ { m }
$$

v Theorem 1 – The Schema Theorem [1, 2]

The expected number of schema $H$ at generation $t + 1$ when using a canonical GA with proportional selection, single point crossover and gene wise mutation (where the latter are applied at rates $p _ { c }$ and $p _ { m } ^ { \phantom { \dagger } } ,$ ) is,

$$
\mathrm { E } [ m ( H , t + 1 ) ] \geq \frac { m ( H , t ) f ( H , t ) } { \bar { f } ( t ) } \boxed { \triangleleft { 1 } \boxed { 1 } } p _ { c } \frac { \iiint } { 1 \boxed { 1 } } p _ { d i f f } ( H , t ) \bigtriangledown o ( H ) p _ { m } \boxed { \begin{array} { l } { \boxed { 1 } } \\ { \boxed { 2 } } \end{array} }
$$

v Comments,

The theorem is described in terms of expectation, thus strictly speaking is only true for the case of a population with an infinite number of members. In the case of finite population sizes the significance of population drift plays an increasingly important role [3].

The above form is naturally specific to the selection and search operators under which it was derived. A more generic form for the Schema Theorem might take the form,

$$
\operatorname { E } [ m ( H , t + 1 ) ] \geq m ( H , t ) \bigcup ( \mathrm { H } , t ) \left\{ 1 - \bigcup ( \mathrm { H } , t ) \right\}
$$

ß Where $\textstyle \prod ( \mathrm { H } , t )$ is the ‘selection coefficient’ and $\textstyle \prod ( \mathrm { H } , t )$ is the ‘transcription error’ [4]. ß This makes the various contributions more explicit. Specifically for schema $H$ to survive then,

$$
\bigstar \bigstar ( H , t ) \models \{ 1 - \bigstar ( H , t ) \}
$$

$$
\mathrm { o r } , \frac { f ( H , t ) } { \bar { f } ( t ) } \ge \boxed { 1 } \boxed { \prod p _ { c } \frac { \iiint H ) } { 1 \big \prod l } p _ { d i f f } ( H , t ) \big \prod o ( H ) p _ { m } } \boxed { 1 }
$$

ß This is the basis for the observation that short (defining length), low order schema of above average population fitness will be favored by canonical GAs, or the Building Block Hypothesis [1, 2].

# Problems

v The Schema Theorem as defined by Holland represented a mile stone in the development of Genetic Algorithms in particular and latter in the development of corresponding theorems for Genetic Programming. However, it has also several significant shortcomings which have lead to more modern approaches to theorems for Genetic Algorithms. Consider the following,

Only the worst-case scenario is considered. No positive effects of the search operators are considered. This has lead to the development of Exact Schema Theorems [5]; The theorem concentrates on the number of schema surviving not which schema survive. Such considerations have been addressed by the utilization of Markov chains to provide models of behavior associated with specific individuals in the population [6]. Claims of “exponential increases” in fit schema i.e., if the expectation operator of Theorem 1 is ignored and the effects of crossover and mutation discounted, the following result was popularized by Goldberg [2], $\operatorname { m } ( H , t + 1 ) \geq ( 1 + \operatorname { c } ) \operatorname { m } ( H , t )$ , where c is the constant by which fit schema are always fitter than the population average. Unfortunately, this is rather misleading as the average population fitness will tend to increase with $t$ , thus population and fitness of remaining schema will tend to converge with increasing ‘time’.

# Список литературы

[1] J.H. Holland, (1998) Adaptation in Natural and Artificial Systems: An Introductory Analysis with Applications to biology, control and artificial intelligence. MIT Press, ISBN 0-262-58111- 6. (NB original printing 1975).

[2] D.E., Goldberg, (1989) Genetic Algorithms in Search, Optimization and Machine Learning. Addison Wesley, ISBN 0-201-15767-5.   
[3] Rodgers A., Prugel-Bennett A. (1999) Genetic Drift in GA Selection Schemes, IEEE Transactions on Evolutionary Computation. 3(4), pp 298-303.   
[4] C.R. Reeves, J.E. Rowe (2003) Genetic Algorithms – Principles and Perspectives. Kluwer Academic Pub. ISBN 1-4020-7240-6.   
[5] C. Stephens, H. Waelbroeck (1998) “Effective Degrees of Freedom in Genetic Algorithms,” Physical review: E, 57(3), pp 3251-3264.   
[6] Vose M.D., Nix A. (1992) “Modeling Genetic Algorithms with Markov Chains,” Annals of Mathematics and Artificial Intelligence, 5, pp 79-98.