# Overview of the Algorithms for Solving the Multidimensional Knapsack Problems

# M. Jalali Varnamkhasti

Department of Mathematics, Dolatabad Branch Islamic Azad University, Isfahan, Iran Jalali.m.v@gmail.com

# Abstract

The multidimensional knapsack problem is defined as an optimization problem that is NP-hard combinatorial. The multidimensional knapsack problems have large applications, which include many applicable problems from different area, like cargo loading, cutting stock, bin-packing, financial and other management, etc. This paper reviews some researches published in the literature. The concentrate is on the different proposed algorithms as well as exact algorithms, and heuristic or metaheuristic algorithms.

Keyword: Multidimensional knapsack problem; exact algorithms; heuristic

# 1. Introduction

The goal of a Multidimensional Knapsack Problem (MKP) is to boost the sum of values of the items to be chosen from some specified set by means of taking multiple-resource restraints into consideration. This problem has been widely studied over many decades due to both theoretical interests and its broad applications in several engineering fields, operations research, and the management and computer sciences. Basically, the MKP can be formulated as follows [1]:

$$
\operatorname* { m a x } _ { \mathbf { \Phi } } \ f ( x _ { 1 } , x _ { 2 } , . . . , x _ { n } ) = \sum _ { j = 1 } ^ { n } p _ { j } x _ { j }
$$

$$
x _ { j } \in \{ 0 , 1 \} \quad j = 1 , . . . , n
$$

where $n =$ number of objects; $m =$ number of knapsacks; $w _ { i j } =$ consumption of resource i for object j; $c _ { i } =$ capacity of the ith knapsack; ${ p _ { j } } ^ { = }$ profit associated with object $j$ ; and $x _ { j } =$ decision variable with object $j$ .

Many different kinds of knapsack problems are found in the literature, including multi-objective, multi-dimensional, multiple-choice, and bounded problems, to mention some. The classical knapsack problem attempts to choose subset from an infinite set of items which boosts a linear function of the selected items contingent upon one inequality restraint. The 0-1 knapsack problem, wherein variables are confined to binary ones, is a special MKP case where $m = 1$ and it can be resolved by pseudo-polynomial time function. The MKP expands the classical knapsack problem to m restraints. For example, if $\scriptstyle { m = 2 }$ , the MKP becomes a bi-dimensional problem. On the other hand, the multiple-choice 0-1 knapsack problem partitions the item set into subsets and the solution must then encircle one item exactly in each subset. The bounded multiple-choice 0-1 knapsack problem however imposes further limitations so as to limit the number of items which can be chosen from any subset.

The MKP is one of the most famous optimization problems due to that many sophisticated optimization problems can be resolved or converted via a succession of knapsack-type sub-problems by means of a number of relaxation methods. For instance, the binary knapsack problem is employed as a sub-problem to resolve the generalized assignment and the vehicle routing problems. As an additional example, the set-covering problems which are broadly practiced in scheduling crew and flights can be restructured as MKP by techniques of variable complementing. Accordingly, the knapsack problem is drawing a lot of theoretical interests and is usually utilized as benchmark problem for the purpose of comparing or validating solution methods in the area of combinatorial optimization. Elaborate literature on the MKP and its relations to different problems are published elsewhere ([2], Martello and Troth [3], Pisinger [4], Chu and Beasley [5], [6]).

# 2. Solution Algorithms to the Knapsack Problem

From a computational perspective, many approaches have been suggested to solve the MKPs and the different proposed algorithms can be broadly grouped into two classes; (i) exact algorithms, and $( i i )$ heuristic or metaheuristic algorithms.

# 2.1 Exact Algorithms

Exact techniques for approaching the MKP evolved many decades earlier and encompassed the Lagrangian methods and surrogate relaxation techniques, special enumeration techniques and reduction schemes, and the branch-and-bound method.

The surrogate strategy presented by Glover [7] substituted the original restraints by one surrogate restraint. Greenberg and Pierskalla [8] posited the first principal handling of surrogate restraints in the setting of general mathematical programming and his research was succeeded by the works of Glover [9, 10] and Dyer [11]. Martello and Toth [12] reported that experiments using algorithm-solving approach unwire non-correlated and that weakly associated instances amounted to more than 100,000 variables. Freville [13] argued that albeit further effort is needed to compute the bounds, the methods of surrogate relaxation more beneficial in resolving the MKP than the methods which use the Lagrangean relaxation due to that the latter framework is not suitable for handling the homogeneous and simple MKP structure.

Balas [14] and Geoffrion [15] built implicit enumeration techniques to resolve the 0–1 linear programs, and Lemke and Spielberg [16] and Breu and Burdet [17] examined the computational potency of different optimizing 0–1 encodes on the basis of these methods. Capability of these implicit, enumeration-based, branch-and-bound techniques in resolving MKP instances persisted somewhat limited. Furthermore, these techniques did not compete with other, more important approaches.

Shih [18, 19] presented the first linear programming-based, branch-andbound technique by use of the particular MKP structure and found a top bound through resolving m single-restrained knapsack problems. He documented computational experiments of a group of 30 uncorrelated and randomly-generated problems having up to five knapsack restraints and ninety parameters. He illustrated that the time needed to solve the enhanced Balas [14] algorithm can be lowered in this manner. Gavish and Pirkul [2] reached to the conclusion that the major imperfections of Shih’s method [19] included its extreme space requirements as well as its inability to resolve problems of tight resource restraints. They proposed a branch-andbound routine for MKP enclosing new rough algorithms for gaining surrogate rules and bounds for decreasing the size of the problem. Furthermore, they demonstrated that their approach was significantly faster than Shih’s [19] through examining with problems having sizes up to seven constraints and 80 variables. Employing LP relaxation of surrogate dual to escape solving 0–1 knapsack problems and to lower solution time, they achieved competent results without enhancing the LP bound.

Freville and Plateau [20] investigated utilization of integer surrogate relaxation to solve the bi-dimensional case by formulating an competent pre-processing stage which can be ended with an enumerative stage if due. Computational experiments with correlated and randomly generated

instances amounting to 750 variables showed that the method is as good as that of Gavish and Pirkul [2] and that it is capable of furnishing a competitive replacement for the LP-based strategies.

Several other particular approaches have attempted to solve the particular/distinctive structures of the MKP. For example, Sahni [21] suggested approximation algorithms for the 0-1 knapsack problem. Plateau and Roucairol [22] utilized parallelization of tree search algorithm which encircled a search for initial achievable solution, a reduction of size on the basis of the additivity of the decreased costs, and use of a terminal branchand-bound technique. Freville and Plateau [23] formulated distinct methods for the bi-dimensional 0–1 knapsack problem and these methods proved to be capable of finding the optimum dual solution within an infinite number of iterations, independent of the variable numbers practically.

Many other methods handled the case of highly associated instances which continued to be very difficult to resolve, and proved to be able to solve, effectively, big problems of such types and of other hard classes. Prominent examples of these methods encompass upper bounds gained through addition of valid inequalities to the cardinality of optimum solution restraint [24]).

Schilling [25] offered asymptotic investigation of MK, and calculated the value of the asymptotic objective function where the capacity of the knapsack was equivalent to one and the profit and resource parameters were distributed in a uniform manner over the unit interval. Szkatula [26] generalized the research by not confining the knapsack capacities to one. Fontanari [27] ran a statistical examination of the MKP and explored reliance of the objective function on the number of capacity restraints and on knapsack capacities.

Albeit different algorithms were formulated to furnish good upper and lower bounds; because of NP perfection, the exact approaches are based mostly on a type of branch and bound and commercial solvers like CPLEX, XPRESS, LINDO, and OSL only can resolve instances of medium and small sizes optimally. Therefore, for solving MKPs instances of large size, several metaheuristic and heuristics techniques have been developed like rough algorithm, multi-stage algorithms, tabu search, simulated annealing, scatter search, and GAs.

# 2.2 Heuristic Algorithms

Senju and Toyoda [28] suggested a twofold heuristic for the MKPs starting with appointing ones to each and every variable and assigning zero to one to the values of these variables simultaneously in accordance with growing ratios till the requirements of feasibility are fulfilled. On the contrary, Kochenberger et al. [29], Toyoda [30], Loulou and Michaelides [31] developed a number of methods for the MKP starting from the origin and assigning ones to the values of the parameters in accordance with declining ratios until the point when addition of additional variables will violate the constraints.

Hillier [32] presented multi-stage algorithms and internal routes for the MKP which concentrated on the simplex made up of the optimum solution of the LP and its nearby farthest points as a starting point of line search. The first stage identifies a route which leads from the optimum solution of LP to other adjacent solution pertaining to the integer viable region. Afterwards, the algorithm traverses this route to determine a better possible integer solution in the second stage. And in the eventual step, local search is carried out in an attempt to enhance the present possible solution by modifying one variable or more at the same time.

By utilizing MKPs moderate size instances, Zanakis [33] demonstrated that Hillier’s [32] algorithm was more precise than the fundamental primal/dual greedy algorithms. A procedure of the most widely-known LPbased ones for identifying rough solutions to the popular linear 0–1 problems is the so-called “Pivot and Complement” method which was originally established by Balas and Martin [34]. They recommended a rough algorithm for the MKP to solve the core problem, which is a knapsack problem determined on a small sub-set of existing items, so that there will be a high possibility of discovering a global optimum in the core, demonstrating that the probability for the heuristic to discover the optimum solution grows with instance size. The protocol starts with resolving the LP relaxation using a standard bounded variable simplex method and proceeds by implementing a series of pivots intending to put the bounded parameters to the basis at the minimum cost. A complementing stage tries next to enhance the 0–1 solution gained in pivoting. Moreover, favourable results have too been achieved for pure 0–1 linear programs using combinations of tabu search and a pivot-and-complement heuristic.

Freville and Plateau [6] suggested an effective pre-MKP processing algorithm assigning sharp low and high limits to the optimal value by lowering the continuous possible set and by removing variables and constraints. Magazine and Oguz (1984) integrated the Senju and Toyoda’s binary algorithm using a Lagrangean relaxation approach allowing for fixing the values of parameters to their values allotted in the whole optimum solutions. Later, their research was expanded by Volgenant and Zoon (1990). Freville and Plateau [35] concentrated on Lagrangean and surrogate relaxations. They suggested three approaches to solutions using accelerated fixing (many variables fixed simultaneously), noising method and strongly determined variables, and surrogate constraints.

Pirkul (1987) built a more plain general technique for solving the MKP containing a descent method for determining the surrogate restraints. They then evidenced that this greedy method was in general more rapid than the pivot-and-complement heuristic and that it produced solutions were that had been comparable, in terms of the quality of the achieved solution, to instances amounting to 20 constraints and 200 variables.

Lee and Guignard [36] suggested a multi-stage technique for solving the MKP tuned with few variables that rule the trade-off between time of computation and quality of solution, whose values were user-defined. They documented that time enhancements to time of computation and quality of solution by numerical outcomes for 48 test problems having 6-500 parameters and 5–20 constraints.

Hanafi and Freville [37] developed a simple multi-stage algorithm for the MKP incorporating several heuristic principles like noising, threshold accepting, simulated annealing, and greedy in a flexible way. Beginning with a group of random possible solutions, the first phase conducted many local search operations and then an extra phase, founded on reiterated greedy steps attempted to enhance the present possible solution. Balas et al. [38] introduced a complex local search in the neighbourhood of the integer of fractional LP-solution intended to resolve pure 0–1 problems.

Martello and Toth [39] established an efficient algorithm for problems of large sizes on the basis of the using a greedy algorithm to solve large knapsack problems. It is capable of solving the core problem and achieving an optimal solution by branch-and-bound, hence gaining an appreciably good low bound.

Plateau et al. [40] tested a multi-stage procedure by use of metaheuristics and interior point techniques where the first stage embraces a hybrid search that employs an interior point technique to produce fractional germ points, a local search to retrieve feasibility, and a cut generator to population diversify of the starting possible solutions. On the other hand, the second stage performs a constant number of route re-linking trials between groups of solution pairs chosen from the starting population. They were able to solve MKP and compared their findings with those of the Chu and Beasley [5] genetic algorithm. In conclusion, the results of the former study exhibited encouraging prospects for the application of interior point techniques as guides to fostered/improved route re-linking, and scattered or local search operations approaches.

Balev et al. [41] suggested a heuristic using dynamic programming in a relevant manner to obtain a possible solution by progressive enhancements to the LP-rounding solution, and examined its performance on all standard sets found in the literature. Their heuristic was found to be remarkably fast and powerful in comparison with the best tabu search methods.

Frieze and Clarke [42] recommended a polynomial approximation method on the foundations of using a dual simplex algorithm for linear programming and tested the asymptotic characteristics of a specific random model. [43] offered a group algorithms of the generalized greedy type wherein items are selected on the basis of their profit declining ratios and weighted sums of their resource coefficients.

Fox and Scudder [44] suggested a heuristic founded on a start setting all variable values to zero (one) and progressively selecting variables to be set to one (zero). They presented the computational outputs for randomly produced MKP test problems comprising up to 100 constraints and variables.

# 2.3 Metaheuristic Algorithms

The most common metaheuristics so far are the, Genetic Algorithm (GA), Greedy Randomized Adaptive Search Procedure (GRASP), Neural Networks (NN), Threshold Accepting Algorithms (TAA), and the Simulated Annealing (SA), and Tabu Search (TS).

Drexel [45] established a SA technique and suggested a particular twoexchange random move which preserves the viability of all the solutions produced in the process. Dueck and Scheuer [46] argued that the deterministic version of SA, known as threshold accepting, produced a bit better results than those produced by the 1988 approach of Drexel [45] for the MKPs.

Dammeyer and Voss [47] presented a TS to solve the MKPs by using a dynamic release of TS known as the Reverse Elimination Method wherein feasibility is preserved during the process by means of a multivariate DROP/ADD move. Battiti and Tecchiolli [48] tested a tabu list dynamic management, known as Reactive Tabu Search, and obtained performance satisfactory well enough with the MKPs.

Lokketangen and Glover [49] founded a straightforward method by letting TS depend on a standard bounded parameter simplex technique as subroutine. They investigated employment of the tunnelling effect and introduced strategic oscillation method which interchanges between destructive and constructive stages of TS and directs the search to parameter depths at both sides of the boundary of the feasible solution. By doing so, they were able to achieve computational outcomes of high quality over many large MKPs problems amounting to 25 constraints and 500 variables. Hanafi and Freville [50] developed a TS method that integrates generalized greedy algorithms with strategic oscillation lead by surrogate information restraints and the condition of the search. They obtained outputs rival with the ones formerly obtained by Glover and Kochenberger [51].

In terms of sizes of the solved problems, Vasquez and Vimont [52] gained the solutions of the best quality for benchmark problems drawn from the related literature. Yet, the time spent in computations was quite high as far as resolving very big instances is concerned. Dammeyer and Voss [47] suggested a TS heuristic on the foundations of inverse elimination and reported results of computations for 57 standard MKP test problems derived from the literature and they were able to find the optimum solutions for 41 out of these.

Lokketangen and Glover [53] recommended a TS heuristic intended for solving universal zero-one, mixed-integer programming problems. They examined tested the proposed technique on some standard MKP problems found in the literature and gained optimum solutions for $9 4 . 7 4 \%$ of them.

Evolutionary algorithms comprise one of the important streamlets of metaheuristics. Michalewicz [54] suggested a GA which adapts the penalty function method to the knapsack problem. Chu and Beasley [5] furnished the most comprehensive covering of GAs for MKPs. They recommended the earliest successful application of GA’s by confining the GA to only

searching the possible search sphere. They furnished an overview and account of the GA, the MKP, and a group of 270 test problems which had been afterwards made available through the internet. Their algorithm encircles heuristic operator that affirms attainment of feasible offspring solutions. They held comparisons between the performances of branch-andbound algorithm and GA and discovered that the performance of GA was somewhat appreciable. Using huge set of problems randomly produced, they reported that the GA heuristic was able to achieve solutions of high-quality for problems of varying features within short calculation time.

Raidl [55] established an enhanced GA by presenting a heuristic repair operator founded on initial variable values of the relaxed LP solution; a local enhancement operator founded on the LP-relaxed MKP solution, and a pre-optimized starting population. They examined the performance of the enhanced GA and compared it with the test set of the Chu and Beasley [5]. Eventually they reached to the conclusion that, in the larger part of time, the former operator converged remarkably faster to somewhat better solutions.

Jalali and Lee [56] proposed a fuzzy genetic algorithm with new crossover operators and probability selection technique based on the population diversity for solving MKPs. Jalali [57] introduced GA based on some new mutation operators for solving 0/1 knapsack problems. In another study, Jalali [58] introduced a new technique for controlling the mutation rate based on diversity of the population and fuzzy tools in GA and used this technique for solving MKPs.

# 4. Conclusion

In this paper we have given a comprehensive survey of the most popular algorithms that they have been used for solving multidimensional knapsack problems. The exact algorithm, heuristic and metaheuristic algorithms are presented as main category discussion and details of each algorithm are given.

# Список литературы

[1] F. Djannaty and S. Doostar. A Hybrid Genetic Algorithm for the Multidimensional Knapsack Problem. International Journal Contemporary Mathematical Sciences. (9) 3 (2008), 443-456.   
[2] B. Gavish and H. Pirkul. Efficient algorithms for solving multiconstraint zero-one knapsack problems to optimality. Mathematical Programming. 31 (1985), 78–105.   
[3] S. Martello and P. Toth. Knapsack problems: Algorithms and Computer Implementations. John Wiley & Sons Ltd., Chichester. (1990).   
[4] D. Pisinger. An expanding-core algorithm for the exact 0–1 knapsack problem. European Journal of Operational Research. 87 (1995), 175–187.   
[5] P. C. Chu and J. E. Beasley. A genetic algorithm for the multidimensional knapsack problem. Journal of Heuristics. 4 (1998), 63-86.   
[6] A. Freville and G. Plateau. An efficient preprocessing procedure for the multidimensional 0-1 knapsack problem. Discrete Applied Mathematics. 49 (1994), 189–212.   
[7] F. Glover. A multiphase-dual algorithm for the zero-one integer programming problem. Operation Research,. 13 (1965), 879–919.   
[8] H. Greenberg and W. Pierskalla. Surrogate mathematical programs. Operations Research. 18 (1970), 924–939.   
[9] F. Golver. Surrogate constraints duality in mathematical programming. Operations Research. 23 (1975), 434-451.   
[10] F. Golver. Surrogate constraints. Operations Research. 16 (1968), 741–749.   
[11] H. E. Dyer. Calculating surrogate constraints. Mathematical Programming. 19 (1980), 255–278.   
[12] S. Martello and P. Troth. Knapsack problems: Algorithms and computer implementations. New York: Wiley. (1990).   
[13] A. Freville. The multidimensional 0–1 knapsack problem: an overview. European Journal of Operations Research. (1) 155 (2004), 1-21.   
[14] E. Balas. An additive algorithm for solving linear programs with zero–one variables. Operations Research. 13 (1965), 517–546.   
[15] A. M. Geoffrion. An improved implicit enumeration approach for integer programming. Operations Research. 17 (1969), 437–454.   
[16] C. E. Lemke and K. Spielberg. Direct search algorithms for zero–one and mixed-integer programming. Operations Research. 15 (1967), 892–914.   
[17] R. Breu and C. A. Burdet. Branch and Bound experiments in zero–one programming. Mathematical Programming Study. 2 (1974), 1-50.   
[18] W. Shih. A branch and bound method for the multiconstraint zero-one knapsack problem. Journal of the Operational Research Society,. 30 (1979), 369–378.   
[19] W. Shih. A branch and bound method for the multiconstraint zero-one knapsack problem. Journal of the Operational Research Society. 30 (1979), 369–378.   
[20] A. Freville and G. Plateau. The 0–1 bidimensional knapsack problem: Towards an efficient high-level primitive tool. Journal of Heuristics. 2 (1997), 147-167.   
[21] S. K. Sahni. Approximate algorithms for the 0-1 knapsack problem. Journal of the ACM. (1) 22 (1975), 115-124.   
[22] G. Plateau and C. Roucairol. A Supercomputer Algorithm for the 0-1 Multiknapsack Problem. In R. Sharda, B. Golden, E. Wasil, O. Balei and W. Stewart, (eds.), Impacts of Recent Computer Advances on Operations Research, Operations Research Series. (1989), 144–157.   
[23] A. Freville and G. Plateau. An exact search for the solution of the surrogate dual of the 0–1 bidimensional knapsack problem. European Journal of Operational Research. 68 (1993), 413–421.   
[24] S. Martello and P. Toth. Upper bounds and algorithms for hard 0–1 knapsack problems. Operations Research. 45 (1997), 768–778.   
[25] K. E. Schilling. The Growth of m-Constraint Random Knapsacks. European Journal of Operational Research. 46 (1990), 109-112.   
[26] K. Szkatula. The Growth of Multi-constraint Random Knapsacks with Various Right-hand Sides of the Constraints. European Journal of Operational Research. 73 (1994), 199-204.   
[27] J. F. Fontanari. A Statistical Analysis of the Knapsack Problem. Journal of Physics A: Mathematical and General. 28 (1995), 4751–4759.   
[28] S. Senju and Y. Toyada. An approach to linear programming problems with 0–1 variables. Management Science. 15 (1968), 196–207.   
[29] G. Kochenberger, G. McCarl and F. Wymann. A heuristic for general integer programming. Decision Sciences,. 5 (1974), 36-44.   
[30] Y. Toyoda. A simplified algorithm for obtaining approximate solutions to zero-one programming problems. Management Science. 21 (1975), 1417– 1427.   
[31] R. Loulou and E. Michaelides. New greedy-like heuristics for the multidimensional 0–1 knapsack problem. Operations Research. 27 (1979), 1101-1114.   
[32] F. S. Hillier. Efficient heuristic procedures for integer linear programming with an interior. Operations Research. 17 (1969), 600–637.   
[33] S. H. Zanakis. Heuristic 0–1 linear programming: An experimental comparison of three methods. Management Science. 24 (1977), 91–104.   
[34] E. Balas and C. H. Martin. Pivot and complement – A heuristic for 0–1 programming. Management Science. 26 (1980), 86-96.   
[35] A. Freville and G. Plateau. Heuristics and reduction methods for multiple constraints 0–1 linear programming problems. European Journal of Operational Research. 24 (1986), 206–215.   
[36] J. S. Lee and M. Guignard. An approximate algorithm for multidimensional zero–one knapsack problems. A parametric approach. Management Science. 34 (1988), 402– 410.   
[37] S. Hanafi and A. Freville. An efficient tabu search approach for the 0–1 multidimensional knapsack problem. European Journal of Operational Research. 106 (1998), 659–675.   
[38] E. Balas, S. Ceria, M. Dawande, F. Margot and G. Pataki. A new heuristic for pure 0–1 programs Operations Research, OCTANE. 49 (2001), 207–225.   
[39] S. Martello and P. Toth. A new algorithm for the 0-1 knapsack problem. Management Science. 34 (1988), 633-644.   
[40] A. Plateau, D. Tachat and P. Tolla. A hybrid search combining interior point methods and metaheuristics for 0–1 programming. International Transactions in Operational Research. 9 (2002), 731–746.   
[41] S. Balev, A. Freville, N. Yanev and R. Andonov. A dynamic programming based reduction procedure for the multidimensional 0–1 knapsack problem. European Journal of Operations Research,. (1) 186 (2008), 63-76.   
[42] A. M. Frieze and M. R. B. Clarke. Approximation Algorithms for the mDimensional 0-1 Knapsack Problem: Worst-Case and Probabilistic Analysis. European Journal of Operational Research. 15 (1984), 100-109.   
[43] A. H. G. Rinnooy Kan, L. Stougie and C. Vercellis. A Class of Generalized Greedy Algorithms for the Multi-knapsack Problem. Discrete Applied Mathematics. 42 (1993), 279–290.   
[44] G. E. Fox and G. D. Scudder. A Heuristic with Tie Breaking for Certain 0-1 Integer Programming Models. Naval Research Logistics Quarterly. 32 (1985), 613–623.   
[45] A. Drexel. A simulated annealing approach to the multiconstraint zero-one knapsack problem. Computing. 40 (1988), 1-8.   
[46] G. Dueck and T. Scherer. Threshold accepting: a general purpose optimization algorithm. Journal of Computational Physics. 90 (1990), 161- 175.   
[47] F. Dammeyer and S. Voss. Dynamic tabu list management using the reverse elimination method. Annals of Operations Research. 41 (1993), 31-46.   
[48] R. Battiti and G. Tecchiolli. The reactive tabu search. ORSA Journal on Computing. 6 (1994), 126–140.   
[49] A. Lokketangen and F. Glover. Probabilistic move selection in tabu search for zero–one mixed integer programming problems. Meta-Heuristics: Theory and Applications, Kluwer Academic Publishers. (1996), 467–487.   
[50] S. Hanafi and A. Freville. Extension of reverse elimination method through a dynamic management of the tabu list. RAIRO Operations Research. 35 (2001), 251–267.   
[51] F. Glover and G. Kochenberger. Critical event tabu search for multidimentional knapsack problems. Meta-heuristics: Theory and applications, Dordecht: Kluwer Academics Publishers. (407-427) (1996).   
[52] M. Vasquez and Y. Vimont. Improved results on the 0–1 multidimensional knapsack problem. European Journal of Operational Research. 165 (2005), 70–81.   
[53] A. Lokketangen and F. Glover. Solving zero-one mixed integer programming problems using tabu search. European Journal of Operations Research. 106 (1998), 624–658.   
[54] Z. Michalewicz. Genetic Algorithm $^ +$ Data Structures $=$ Evolution Programs. (3rd revised and extended edition. Springer-Verlag, 1996).   
[55] G. R. Raidl. An Improved Genetic Algorithm for the Multiconstrained 0-1 Knapsack Problem. In Proceeding of the 5th IEEE International Conference on Evolutionary Computation. (1998), Anchorage, Alaska, 207–211.   
[56] M. Jalali Varnamkhasti and L. L.S..A Genetic Algorithm with Fuzzy Crossover Operator and Probability. Advance Operation Research, (2011). (to appear).   
[57] M. Jalali Varnamkhasti. A genetic algorithm based on new mutation methods for solving $_ { 0 / 1 }$ knapsack problem. Far East Journal of Mathematical Sciences, (2011). (to appear).   
[58] M. Jalali Varnamkhasti. Controlling the mutation rate based on diversity of the population and fuzzy tools in genetic algorithm. Advanced Studies in Biology Journal, (2011). (to appear).