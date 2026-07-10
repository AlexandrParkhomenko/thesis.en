# Parallel Genetic Algorithms for Optimization and Application to NP-Complete Problem Solving Submitted to Colloque CoMBINaToIRE ET InFORMATIQUE, Brest, 1995

D. Duvivier\* Ph. Preux† E-G. Talbi‡

Keywords: Meta-heuristic, parallel computing, combinatorial optimization, hybrid search method

# Introduction

Geneic algorithms (GAs) are stochastic research methods introduced by J. Holland in the 70's and inspired by the biological evolution o living beings. In the past, GAs have been succesully pplied in the felds o artificial intelligence and combinatorialoptimization. However, theirexecution cost is a majordrawback to their widespread use. Apart from enhancing the algorithm, the growing availability of parallel computers opens new horizons. Several parallel execution models of GAs have been proposed and applied to solve various problems. Three approaches to parallel genetic algorithms may be considered [Tal95]:

the standard parallel approach: in this approach, the evaluation, the selection and the reproduction steps are performed in parallel [Rob87]. Both mating and selection are performed over the whole population.   
the decomposition approach: this approach consists in dividing the population into equally sized subpopulations. Each processor runs the genetic algorithm on one subpopulation, periodically selecting good individuals to send to its neighbors [Tan87].   
the local selection approach: it is a fine grained model, where the population is mapped on a connected graph of processor, one individual per processor [TB91]. The selection is done locally in the neighborhood of each individual.

The design of these parallel models have mainly been driven by the architecture on which they were intended to run (SIMD, MIMD with loosely, or tightly coupled processors). We have experimented the decomposition approach and the local selection approach to solve data fusion problems, graph partitioning, robot trajectory design, as wel s a few military applications. We have implemented parallel execution models on various target architectures (massively parallel Maspar computer, 16 processors farm, 128 transputers networks).

In the rest of this paper, we present very briefy the basic ideas grounding our work and our current works. We focus our attention on the study o various hybrid GAs, the co-evolution in parallel model, and we introduce a new parallel approach, namely the heterogenous approach.

# From ideas ...

Our research group aims at studying GAs to solve combinatorial optimization problems. Though grounded on the GA scheme of execution, we do not restrict ourselves to the study of pure GAs. Problems are well-known that lead to the definition of alternatives to the standard GA. It is now considered as granted that genetic algorithms used as optimizers should use non binary representation of solutions with associated genetic operators (see for instance [De 93]). (Operators are the very heart of genetic search techniques, mechanically manipulating current solutions to engender new ones. A selection mechanism stochastically retains individuals amongst the parents and the offsprings favoring the best ones.)

An other path of research is the use of parallel execution models. Our point is not restricted here to the useof the brute forceo parallel computers.Rather, we think thata rel cooperationo several sarch methods will lead to better solutions (see for instance [KMD95]), either by the way of a co-evolution of partial solutions, or of different search methods, or a combination of both.

Finally, yet an other track is the hybridization, that is the composition of the standard GA with other search methods, such as simulated annealing, hil-climbing, TABU search, branch-and-bound, .algorithms. We think that this last track is a very promising one and we are concentrating most of our effrts on it.

# ... to works

Hence, one issue is to assess the use of GAs to solve combinatorial optimization problems and shed some ln heoll pointswhat kin  proems stan  proem, can be olv efntyh GA techniques?We are currently ackling three problems in the fieldof combinatorialoptimization, namely the quadratic asignment problem, the job-shop scheduling problem, and the graph partitioning problem.

Comparisons between GA search, stochastic hill-climbing (seen as a simple and cheap method) and TABU search (seen as a very efficient method) have been performed to assess the efficiency of GAs [TMS94]. Encouraging results have been obtained. Comparisons with simulated annealing are planned.

The second issue is to propose new variants of the basic algorithm. We are currently working on the hybridization of GAs with other search methods such as the TABU search. This kind of search methods may be seen at three distinct levels.

Either, it may be seen as a GA operator (kind of mutation directed towards better fitting individuals, while the mutation in the standard GA is direction-less). In this case, say the TABU search is applied on some individuals, considering them as the originof the search. Its result gives an individual which replaces the original one in the population of the GA.

Or, it may also be used after the GA to exploit the result of the previous exploration of the search space by the GA. It is widely known that the GA is efficient at the beginning of the search (the research space is quickly restricted to a sub-space) as long as the population has not uniformed too much. Once the research space is largely restricted, it is then much more ecient touse an other search method, such as the TABU search. Then, we use the prototypical individual of the GA population as the origin of the new search algorithm. These two schemes of hybridation have been experimented with success on the graph partitioning problem [TMS94].

Or, the GA and the TABU may run concurrently, exchanging individuals from time to time. One keypoint is here the way the GA and the TABU communicate (when?, which individuals?, how is a new individual handled by the other algorithm?). We are currently experimenting this point on a parallel heterogeneous environment (the heterogeneous approach). The GA is running in a local selection manner on a SIMD computer, and several TABUs are running in parallel on a processor farm.

# Conclusion

We have briely presented the key ideas of our work focusing on the adequacy of using algorithms based on the genetic, or evolutionary, paradigm as robust combinatorial optimizers. We think, and our first results confrm i, that acareful hybridization of non binary GAs with other search methods will provide us with vey efficint heuristics. Furthermore, the co-evolutionof partial solutions orovarious searc method appers to be a very fruitful research path. The heterogeneous approach should efficiently meet the challenge of the implementation of these search methods on current heteregeneous parallel environments.

# Список литературы

[De 93] Kenneth A. De Jong. Genetic algorithms are NOT function optimizers. In [Whi93], pages 5-17, 1993.

[M95 Su Wndm cDvrOtTl report, Santa Fe Institute, April 1995. nealing, L.Davis ed., Morgan Kaufmann Pub., pages 129-140, 1987.   
T applications irrégulières, edition Hermes, Cauterets, France, Fev 1995.   
T , Cambridge, pages 177-183, July 1987.   
puting, Cologne, Germany, June 1991.   
Artificielle EA94, Toulouse, France, Sep 1994.