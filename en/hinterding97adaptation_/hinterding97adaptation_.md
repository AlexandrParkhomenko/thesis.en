# Adaptation in Evolutionary Computation: A Survey

Robert Hinterding, Zbigniew Michalewicz, and A.E. Eiben

Abstract— Adaptation of parameters and operators is one of the most important and promising areas of research in evolutionary computation; it tunes the algorithm to the problem while solving the problem. In this paper we develop a classification of adaptation on the basis of the mechanisms used, and the level at which adaptation operates within the evolutionary algorithm. The classification covers all forms of adaptation in evolutionary computation and suggests that further research.

# I. InTROduCtiON

As evolutionary algorithms (EAs) implement the idea of evolution, and as evolution itself must have evolved to reach its current state of sophistication, it is natural to expect adaptation to be used not only for finding solutions to a problem, but also for tuning the algorithm to the particular problem.

In EAs, we not only need to choose the algorithm, representation, and operators for the problem, but we also need to choose parameter values and operator probabilities for the evolutionary algorithm so that it will find the solution and, what is also important, find it efficiently. This process of finding appropriate parameter values and operator probabilities is a time-consuming task and considerable effort has gone into automating this process.

Researchers have used various ways of finding gooc values for the strategy parameters as these can both affect the performance of the algorithm in a significant way. Many researchers experimented with various problems from a particular domain, tuning the strategy parameters on the basis of such experimentation (tuning "by hand"). Later, they reported their results of applying a particular EA to a particular problem, stating:

For these experiments, we have used the following parameters: population size $=$ 80, probability of crossover $= 0 . 7$ , etc.

without much justification of the choice made. Other researchers tried to modify the values of strategy parameters 1 during the run of the algorithm; it is possible to do this by using some (possibly heuristic) rule, by taking feedback from the current state of the search, or by employing some self-adaptive mechanism. Note that these changes may affect a single component of a chromosome, the whole chromosome (individual), or even the whole population. Clearly, by changing these values while the algorithm is searching for the solution of the problem, further efficiencies can be gained.

Self-adaptation, based on the evolution of evolution, was developed in Evolution Strategies to adapt mutation parameters to suit the problem during the run. The method was very successful in improving efficiency of the algorithm for some problems. This technique has been extended to other areas of evolutionary computation, but fixed representations, operators, and control parameters are still the norm.

Other research areas based on the inclusion of adapting mechanisms are:

•representation of individuals (as proposed by Shaefer (1987); the Dynamic Parameter Encoding technique, Schraudolph & Belew (1992) and messy genetic algorithms, Goldberg et al. (1991) also fall into this category). operators. It is clear that different operators play different roles at different stages of the evolutionary process. The operators should adapt (e.g., adaptive crossover, Schaffer $\&$ Morishima (1987), Spears (1995)). This is true especially for time-varying fitness landscapes. control parameters. There have been various experiments aimed at adaptive probabilities of operators (Davis, 1989; Julstrom, 1995; Srinivas & Patnaik, 1994). However, much more remains to be done.

In this paper we develop a comprehensive classification of adaptation and give examples of their use. The classification is based on the mechanism of adaptation and level (in the EA) it occurs. Such a classification might be of some importance to the evolutionary computation community, since many researchers use the terms "adaptation" or "self-adapt: in arbitrary ways; in a few instances some authors (including ourselves!) used the term "self-adaptation' where there was a simple (deterministic and heuristic) rule for changing some parameter of the process!

The paper is organised as follows: the next section we develop classification of adaptation in Evolutionary Algorithms (EAs). Section III looks at types of adaptation, whereas Section IV — at the levels of adaptation. Section V discusses the combination of types and levels of adaptation and Section VI presents the discussion and conclusion.

# II. Classification of Adaption

The action of determining the variables and parameters of an EA to suit the problem has been termed adapting the algorithm to the problem, and in EAs this can be done while the algorithm is finding the problem solution.

We give classifications of adaptation in Table 1; this classification is based on the mechanism of adaptation (adaptation type) and on which level inside the EA adaptation occurs (adaptation level). These classifications are orthogonal and encompass all form: of adaptation within EAs. Angeline's classification (1995) is from a different perspective and forms a subset of our classifications.

The Type of parameters' change consists of two main categories: static (no change) and dynamic, with the latter one divided further into deterministic (D), adaptive (A), and self-adaptive (SA) mechanisms. In the following section we discuss these types of adaptation.

The Level of parameters' change consists of four categories: environment (E), population (P), individual (I), and component (C). These categories indicate the scope of the changed parameter; we discuss these types of adaptation in Section IV.

Whether examples are discussed in Section III or in Section IV is completely arbitrary. An example of adaptive individual level adaptation (I-A) could have been discussed in Section III as an example of adaptive dynamic adaptation or in Section IV as an example of individual level of adaptation.

# III. Types of ADaption

The classification of the type of adaptation is made on the basis of the mechanism of adaptation used in the process; in particular, attention is paid to the issue of whether ot not a feedback from the EA is used.

# A. Static

Static adaptation is where the strategy parameters have a constant value throughout the run of the EA. a person or a program) is needed to tune the desired strategy parameters and choose the most appropriate values. This method is commonly used for most of the strategy parameters.

De Jong (1975) put considerable into finding parameter values which were good for a number of numeric test problems using a traditional GA. He determined experimentally recommended values for the probability of using single-point crossover and bit mutation. Grefenstette (1986) used a GA as a meta-algorithm to optimize values for some parameter values.

# B. Dynamic

Dynamic adaptation happens if there is some mechanism which modifies a strategy parameter without external control. The class of EAs that use dynamic adaptation can be sub-divided further into three classes where the mechanism of adaptation is the criterion.

# B.1. Deterministic

Deterministic dynamic adaptation takes place if the value of a strategy parameter is altered by some deterministic rule; this rule modifies the strategy parameter deterministically without using any feedback from the EA. Usually, the rule will be used when a set number of generations have elapsed since the last time the rule was activated.

This method of adaptation can be used to alter the probability of mutation so that the probability of mutation changes with the number of generations. For example:

$$
m u t \% = 0 . 5 + 0 . 3 \cdot \frac { g } { G } ,
$$

where $g$ is the generation number from $1 \ldots G$ . Here the mutation probability $m u t \%$ will increase from 0.5 to 0.8 as the number of generations increases to $G$ .

This method of adaptation was used also in defining a mutation operator for floating-point representations (Michalewicz, 1996): non-uniform mutation. For a parent $\vec { x }$ , if the element $x _ { k }$ is selected for this mutation, the result is $\vec { x } ^ { \prime } = \left( x _ { 1 } , \ldots , x _ { k } ^ { \prime } , \ldots , x _ { n } \right)$ , where

Table 1: Classification of adaptation in EAs   

<table><tr><td rowspan="2">Type Level</td><td rowspan="2">Static</td><td colspan="3">Dynamic</td></tr><tr><td>Deterministic</td><td>Adaptive</td><td>Self-adaptive</td></tr><tr><td>Environment</td><td>S</td><td>E-D</td><td>E-A</td><td>E-SA</td></tr><tr><td>Population</td><td>S</td><td>P-D</td><td>P-A</td><td>P-SA</td></tr><tr><td>Individual</td><td>S</td><td>I-D</td><td>I-A</td><td>I-SA</td></tr><tr><td>Component</td><td>S</td><td>C-D</td><td>C-A</td><td>C-SA</td></tr></table>

$$
\begin{array} { r } { x _ { k } ^ { \prime } = \left\{ \begin{array} { l l } { x _ { k } + \triangle \big ( t , r i g h t ( k ) - x _ { k } \big ) } \\ { \qquad \mathrm { i f ~ a ~ r a n d o m ~ b i n a r y ~ d i g i t ~ i s ~ 0 ~ } } \\ { x _ { k } - \triangle \big ( t , x _ { k } - l e f t ( k ) \big ) } \\ { \qquad \mathrm { i f ~ a ~ r a n d o m ~ b i n a r y ~ d i g i t ~ i s ~ 1 } . } \end{array} \right. } \end{array}
$$

The function $\triangle ( t , y )$ returns a value in the range $[ 0 , y ]$ such that the probability of $\triangle ( t , y )$ being close to 0 increases as $t$ increases( $t$ is the generation number). This property causes this operator to search the space uniformly initially (when $t$ is small), and very locally at later stages.

Deterministic dynamic adaptation was also used for changing the objective function of the problem; the point was to increase the penalties for violated constraints with evolution time (Joines $\&$ Houck, 1994; Michalewicz $\&$ Attia, 1994). Joines $\&$ Houck used the following formula:

$$
\begin{array} { r } { F ( \vec { x } ) = f ( \vec { x } ) + ( C \times t ) ^ { \alpha } \sum _ { j = 1 } ^ { m } f _ { j } ^ { \beta } ( \vec { x } ) , } \end{array}
$$

whereas Michalewicz and Attia experimented with

$$
\begin{array} { r } { F ( \vec { x } , \tau ) = f ( \vec { x } ) + \frac { 1 } { 2 \tau } \sum _ { j = 1 } ^ { m } f _ { j } ^ { 2 } \left( \vec { x } \right) . } \end{array}
$$

In both cases, functions $f _ { j }$ measure the violation of the $j$ -th constraint.

Eiben $\&$ Ruttkay (1996) described an implementation of an evolutionary algorithm for constraint satisfaction problems, where the penalty coefficients were increased after a specified number of generations.

# B.2. Adaptive

Adaptive dynamic adaptation takes place if there is some form of feedback from the EA that is used to determine the direction and/or magnitude of the change to the strategy parameter. The assignment of the value of the strategy parameter may involve credit assignment, and the action of the EA may determine whether or not the new value persists or propagates throughout the population.

Early examples of this type of adaptation include Rechenberg's $^ { \circ } 1 / 5$ success rule', which was used to vary the step size of mutation (Rechenberg, 1973). This rule states that the ratio of successful mutations to all mutations should be $1 / 5$ , hence if the ratio is greater than $1 / 5$ then increase the step size, and if the ration is less than $1 / 5$ then decrease the step size. Another example is Davis's 'adaptive operator fitness', which used feedback from the performance of reproduction operators to adjust their probability of being used (Davis, 1991).

Adaption was also used to change the objective function by increasing or decreasing penalty coefficients for violated constraints. For example, Bean & Hadj-Alouane (1992) designed a penalty function where its one component takes a feedback from the search process. Each individual is evaluated by the formula:

$$
\begin{array} { r } { F ( \vec { x } ) = f ( \vec { x } ) + \lambda ( t ) \sum _ { j = 1 } ^ { m } f _ { j } ^ { 2 } ( \vec { x } ) , } \end{array}
$$

where $\lambda ( t )$ is updated every generation $t$ in the following way:

$$
\lambda ( t + 1 ) = \left\{ \begin{array} { l l } { ( 1 / \beta _ { 1 } ) \cdot \lambda ( t ) , } \\ { \quad \mathrm { i f } \overrightarrow { b } ( i ) \in \mathcal { F } \mathrm { f o r ~ a l l } } \\ { \quad \quad t - k + 1 \leq i \leq t } \\ { \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad } \\ { \quad \quad \mathrm { i f } \overrightarrow { b } ( i ) \in \mathcal { S } - \mathcal { F } \mathrm { f o r ~ a l l } } \\ { \quad \quad \quad \quad \quad t - k + 1 \leq i \leq t } \\ { \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \lambda ( t ) , } \end{array} \right.
$$

where $\vec { b } ( i )$ denotes the best individual, in terms of function eval, in generation $i$ , $\beta _ { 1 } , \beta _ { 2 } > 1$ and $\beta _ { 1 } \neq$ $\beta _ { 2 }$ (to avoid cycling). In other words, the method (1) decreases the penalty component $\lambda ( t + 1 )$ for the generation $t + 1$ , if all best individuals in the last $k$ generations were feasible, and (2) increases penalties, if all best individuals in the last $k$ generations were infeasible. If there are some feasible and infeasible individuals as best individuals in the last $k$ generations, $\lambda ( t + 1 )$ remains without change.

Other examples include adaptation of probabilities of eight operators for adaptive planner/navigator (Xiao et al. , 1996), where the feedback from the evolutionary process includes, through the operator performance index, effectiveness of operators in improving the fitness of a path, their operation time, and their side effect to future generations.

# B.3. Self-adaptive

The idea of the evolution of evolution can be used to implement the self-adaptation of parameters. Here the parameters to be adapted are encoded onto the chromosome(s) of the individual and undergo mutation and recombination. These encoded parameters do not affect the fitness of individuals directly, but "better" values will lead to "better" individuals and these individuals will be more likely to survive and product offspring and hence propagate these "better" parameter values.

Schwefel (1977; 1995) developed this method to self-adapt the mutation step size and the mutation rotation angles in Evolution Strategies. Self-adaptati was extended to EP by Fogel et al. (1991) and to GAs by Bäck (1992) and Hinterding (1995).

The parameters to self adapt can be parameter values or probabilities of using alternative processes, and as these are numeric quantities this type of self-adaptation has been used mainly for the optimisation of numeric functions. This has been the case when single chromosome representations are used (which is the overwhelming case), as otherwise numerical and non-numerical representations would need to be combined on the same chromosome. Examples of self-adaptation for non-numerical problems are Fogel et al. (1995) where they self-adapted the relative probabilities of five mutation operators for the components of a finite state machine. The other example is Hinterding (1997), where a multichromosome GA is used to implement the self-adapta in the Cutting Stock Problem with contiguity. Here self-adaptation is used to adapt the probability of using one of the two available mutation operators, and the strength of the group mutation operator.

# IV. LEvELS Of ADaPtiON

We can also define at what level within the EA and the solution representation adaptation takes place. We define four levels: environment, population, individual, and component. These levels of adaptation can be used with each of the types of adaptation, and a mixture of levels and types of adaptation can be used within an EA.

# A. Environment Level Adaption

Environment level adaptation is where the response of the environment to the individual is changed. This covers cases such as when the penalties in the fitness function change, where weights within the fitness function change and the fitness of an individual changes in response to niching considerations (some of these were discussed in the previous section, in the context of types of adaptation).

Darwen & Yao (1996), explore both deterministic environmental adaptation and adaptive environmental adaptation in their paper comparing fitness sharing methods.

# B. Population Level Adaption

In EAs some (or all in simple EAs) of the parameters are global, modifying these parameters when they apply to all members of the population is population level adaptation.

Dynamic adaptation of these parameters is in most cases deterministic or adaptive. No cases of population level self-adaptation have been seen yet. The example of deterministic modification of the mutation rate given above is deterministic population level adaptation, and Rechenberg's $^ { \circ } 1 / 5$ success rule' is an example of adaptive population level adaptation.

Population level adaptation also covers cases where a number of populations are used in a parallel EA or otherwise, Lis (1996) uses feedback from a number of parallel populations to dynamically adapt the mutation rate. The feedback from populations with different mutation probabilities was used to adjust the mutation probabilities of all the populations up or down. Schlierkamp-Voosen & Mühlenbein (1996) use competition between sup-populations to determine which populations will lose or gain individuals. Hinterding it et al. (1996) use feedback from three sub-populations with different population sizes to adaptively change some or all of the sub-population sizes.

# C. Individual Level Adaption

Individual-level adaptation adjusts strategy parameters held within individuals and whose value affects only that individual. Examples are: the adaptation of the mutation step size in ESs, EP, and GAs; the adaptation of crossover points in GAs (Schaffer $\&$ Morishima, 1987).

Arabas it et al.(1994) describe a method for adapting population size by defining age of individuals; the size of the population after single iteration is

$$
\begin{array} { r } { P o p S i z e ( t { + } 1 ) = P o p S i z e ( t ) { + } N ( t ) { - } D ( t ) , } \end{array}
$$

where $D ( t )$ is the number of chromosomes which die off during generation $t$ and $N ( t )$ is the number of offspring produced during the generation $t$ (for details, see Michalewicz (1996)). The number of produced offspring $N ( t )$ is proportional to the size of the population at given generation $t$ , whereas the number of individuals "to die" $D ( t )$ depends on age of individual chromosomes. There are several heuristics one can use for the age allocation for individuals (Arabas et al. , 1994); all of them require a feedback from the current state of the search.

# D. Component Level Adaption

Component-level adaptation adjusts strategy parameters local to some component or gene of an individual in the population. The best known example of component level adaptation is the self-adaptation of component level mutation step sizes and rotation angles in ESs.

Additionally, in Fogel et al. (1995) the mechanism of adapting probabilities of mutation for each component of a finite states machine is discussed.

# V. COMBINING FORMS OF ADAPTATION

The classic example of combining forms of adaptation is in ESs, where the algorithm can be configured for individual level adaptation (one mutation step size per individual), component level adaptation (one mutation step size per component) or with two types of component level adaptation where both the mutation step size and rotation angle is selfadapted for individual components (Schwefel, 1977).

Hinterding it et al. (1996) combine global-level adaptation of the population size with individual level self-adaptation of the mutation step size for optimising numeric functions.

Combining forms of adaptation has not been used much as the interactions are complex, hence deterministic or adaptive rules will be difficult to work out. But self-adaptation where we use evolution to determine the beneficial interactions (as in finding solutions to problems) would seem to be the best approach.

# VI. Discussion

The effectiveness of evolutionary computations depend on the interaction of representation used for the problem solutions, the reproduction operators used, and the configuration of the evolutionary algorithm used.

Adaption provides the opportunity to customise the evolutionary algorithm to the problem and to modify the configuration and the strategy parameters used while the problem solution is sought. This enables us to not only incorporate domain information and multiple reproduction operators into the EA more easily, but can allow the algorithm itself to select those values and operators which give better results. Also these values can be modified during the run of the EA to suit the situation during that part of the run.

Information about which of the operators available are most suitable to a particular problem is not easily determined, adaptation can be used here to provide feedback or to determine when they should be used.

More research on the combination of the types and levels of adaptation needs to be done as this could lead to significant improvements to finding good solutions and the speed of finding them.

#

REfEreNceS   
Angeline, P.J. 1995. Adaptive and Self-Adaptive Evolutionary Computation. In: Palaniswami, M., Attikiouzel, Y., Marks, R.J.II, Fogel, D., & Fukuda, T. (eds), Computational Intelligence, A Dynamic System Perspective. IEEE Press. pp.152161.   
Arabas, J., Michalewicz, Z., & Mulawka, J. 1994. GAVaPS — a Genetic Algorithm with Varying Population Size. In: Proceedings of the First IEEE Conference on Evolutionary Computation. IEEE Press. pp. 7378.   
Bäck, T. 1992. Self-adaption in Genetic Algorithms. In: Proceedings of the First European Conference on Artificial Life. Cambridge: MIT Press. pp. 263271.   
Bean, J.C., & Hadj-Alouane, A.B. 1992. A Dual Genetic Algorithm for Bounded Integer Programs. TR 92-53. Department of Industrial and Operations Engineering, The University of Michigan.   
Darwen, P, & Yao, X. 1996. Every Niching Mehtod has its Niche: Fitness sharing and Implicit Sharing Compared. In: Voigt, H-M., Ebeling, W., Rechenberg, I., & Schwefel, H-P. (eds), Parellel Problem Solving from Nature - PPSV IV. Lecture Notes in Computer Science, vol. 1141. Berlin: Springer. pp. 398-407.   
Davis, L. 1989. Adapting Operator Probabilities in Genetic Algorithms. In: Proceedings of the 3rd International Conference on Genetic Algorithms. Morgan Kaufmann.   
Davis, L. (ed). 1991. Handbook of Genetic Algorithms. Van Nostrand Reinhold.   
De Jong, K. A. 1975. An Analysis of the Behaviour of a Class of Genetic Adaptive System. Doctoral dissertation, University of Michigan. Dissertation Abstract International, 36(10), 5140B. (University Microfilms No 76-9381).   
Eiben, A.E., & Ruttkay, Zs. 1996. Self-adaptivity for Constraint Satisfaction: Learning Penalty Functions. In: Proceedings of the 3rd IEEE International Conference on Evolutionary Computation. IEEE Press. pp. 258261.   
Fogel, D.B., Fogel, L.J., & Atmar, J.W. 1991. Meta-Evolutionary Programming. In: Chen, R.R. (ed), Proc. of the 25th Asilomar Conf. on Signals, Systems, and Computers. San Jose: Maple Press. pp. 540545.   
Fogel, L.J., Angeline, P.J., & Fogel, D.B. 1995. An Evolutionary Programming Approach to SelfAdaption on Finite State Machines. In: McDonnell, J.R., Reynolds, R.G., & Fogel, D.B. (eds), Proceedings of the Forth Annual Conference on Evolutionary Programming. Massachusetts: MIT Press. pp. 355365.   
Goldberg, D.E., Deb, K., & Korb, B. 1991. Do not Worry, Be Messy. In: Proceedings of the 4th International Conference on Genetic Algorithms. Morgan Kaufmann. pp. 2430.   
Grefenstette, J.J. 1986. Optimization of Control Parameters for Genetic Algorithms. IEEE Transactions on Systems, Man, and Cybernetics, vol. 16(1), pp. 122128.   
Hinterding, R. 1995. Gaussian Mutation and Selfadaption in Numeric Genetic Algorithms. In: IEEE International Conference on Evolutionary Computation. IEEE Press. pp 384-389.   
Hinterding, R. 1997. Self-adaptation using Multichromosomes. In: Proceedings of the 4th IEEE International Conference on Evolutionary Computation. IEEE Press.   
Hinterding, R., Michalewicz, Z., & Peachey, T.C. 1996. Self-Adaptive Genetic Algorithm for Numeric Functions. In: Voigt, H-M., Ebeling, W., Rechenberg, I., & Schwefel, H-P. (eds), Parellel Problem Solving from Nature - PPSV IV. Lecture Notes in Computer Science, vol. 1141. Berlin: Springer. pp. 420-429.   
Joines, J.A., & Houck, C.R. 1994. On the Use of Non-Stationary Penalty Functions to Solve Nonlinear Constrained Optimization Problems With GAs. In: Proceedings of the First IEEE Conference on Evolutionary Computation. IEEE Press. pp. 579584.   
Julstrom, B.A. 1995. What Have You Done for Me Lately? Adapting Operator Probabilities in a Steady-State Genetic Algorithm. In: Proceedings of the Sixth International Conference on Genetic Algorithms. Morgan Kaufmann. pp. 8187.   
Lis, J. 1996. Parallel Genetic Algorithm with Dynamic Control Parameter. In: Proceedings of the 1996 IEEE Conference on Evolutionary Computation. Piscataway,NY:IEEE Press. pp. 324329.   
Michalewicz, Z. 1996. Genetic Algorithms $+$ Data Structures $=$ Evolution Programs. 3rd edn. New York: Springer - Verlag.   
Michalewicz, Z., & Attia, N. 1994. Evolutionary Optimization of Constrained Problems. In: Sebald, A.V., & Fogel, L.J. (eds), Proceedings of the Third Annual Conference on Evolutionary Programming. World Scientific. pp. 98108.   
Rechenberg, R. 1973. Evolutionsstrategie: Optimierung technischer Syseme nach Prinzipien der biologischen Evolution. Stuttgart: Frommann-Holzboog.   
Schaffer, J.D., & Morishima, A. 1987. An Adaptive Crossover Distribution Mechanism for Genetic Algorithms. In: Proceedings of the 2nd International Conference on Genetic Algorithms. Lawrence Erlbaum Associates. pp. 3640.   
Schlierkamp-Voosen, D., & Mühlenbein. 1996. Adaption of Population Sizes by Competing Subpopulations. In: Proceedings of the 1996 IEEE Conference on Evolutionary Computation. Piscataway,NY: IEEE Press. pp. 330-335.   
Schraudolph, N., & Belew, R. 1992. Dynamic Parameter Encoding for Genetic Algorithms. Machine Learning, vol. 9(1), pp. 921.   
Schwefel, H-P. 1977. Numerische Optimierung von Computer-Modellen mittels der Evolutionsstrategie. Interdisciplinary systems research, vol. 26. Basel: Birhäuser.   
Schwefel, H-P. 1995. Evolution and Optimum Seeking. Sixth-Generation Computer Technology Series. Wiley.   
Shaefer, C.G. 1987. The ARGOT Strategy: Adaptive Representation Genetic Optimizer Technique. In: Proceedings of the 2nd International Conference on Genetic Algorithms. Lawrence Erlbaum Associates. pp. 5055.   
Spears, W.M. 1995. Adapting Crossover in Evolutionary Algorithms. In: McDonnell, J.R., Reynolds, R.G., & Fogel, D.B. (eds), Proceedings of the Fourth Annual Conference on Evolutionary Programming. The MIT Press. pp. 367384.   
Srinivas, M., & Patnaik, L.M. 1994. Adaptive Probabilities of Crossover and Mutation in Genetic Algorithms. IEEE Transactions on Systems, Man, and Cybernetics, vol. 24(4), pp. 1726.   
Xiao, J., Michalewicz, Z., & Zhang, L. 1996. Evolutionary Planner/Navigator: Operator Performance and Self-Tuning. In: Proceedings of the 3rd IEEE International Conference on Evolutionary Computation. IEEE Press. pp. 366 371.