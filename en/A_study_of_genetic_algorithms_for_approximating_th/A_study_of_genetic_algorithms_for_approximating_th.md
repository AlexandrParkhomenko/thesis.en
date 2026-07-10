# A study of genetic algorithms for approximating the longest path in generic graphs

Conference Paper $\cdot$ October 2010

READS 111

3 authors, including:

![](images/e3a1c56688698e3353ae0f5fb34789a7098f612e69f8f468dfa24b9e8909c5d7.jpg)

Carlos Henggeler Antunes University of Coimbra and INESC Coimbra

243 PUBLICATIONS 2,811 CITATIONS

![](images/cab675febee05f495bb244dbcc1eb9c53b7e9eb3e5bcbc4f323c7080d219e32b.jpg)

Rui P. Rocha

University of Coimbra

96 PUBLICATIONS 809 CITATIONS

Some of the authors of this publication are also working on these related projects:

![](images/2e9fe7e818058758f130ada290c6cc1bb2d6ce307a4d7a690d58fa8a5d43b3a4.jpg)

M.Sc. Thesis on Real-Time Motion Controller for Differential Mobile Robots View project

Ren4EEnIEQ – Comprehensive BIM add-on tool for the improvement of energy efficiency and indoor environment quality in renovation of buildings View project

# A Study of Genetic Algorithms for Approximating the Longest Path in Generic Graphs

# David Bina Siassipour Portugal

A report presented for the subject of Advanced Topics on Operational Research

February, 2010

# Abstract

Finding the longest simple path in a generic undirected graph is a challenging issue that belongs to the NP-Complete class of problems. Four approaches based on genetic algorithms to solve this question are presented in this report. The first three algorithms proposed use crossover mechanisms between pairs of solutions based on their intersecting regions and the fourth one uses a mutation mechanism on individual solutions, in which the perturbation applied depends on the state of the system. Simulation results validate the distinct approaches, reveal their good performance and provide hints for their application in robotics, package networks and other fields.

Key Words: Genetic Algorithms, Graph Theory, Longest Path Problem

# Contents

Abstract iii

Contents iv

List of Figures vi

List of Tables vii

# 1 Introduction 1

1.1 The Longest Path Problem (LPP) . .   
1.2 Genetic Algorithms (GAs) 2   
1.3 Outline of the document . . . 4

# 2 Defining The Problem 5

# 3 The Algorithms 7

3.1 Generating initial solutions . 7   
3.2 Algorithm 1: GA using non-intersecting paths (GANP) 8   
3.3 Algorithm 2: GA using intersecting paths (GAIP) 9   
3.4 Algorithm 3: GA using both pairs of paths (GABPP) . . . . 10   
3.5 Algorithm 4: GA using a mutation mechanism (GAMM) . . 11

# 4 Results and Discussion 13

4.1 Simulation Results 13   
4.2 Discussion 19

5 Conclusions 21

5.1 Overview . . 21   
5.2 Future Work . 22

# Bibliography

23

# List of Figures

3.1 An illustrative example of two disconnected paths. . . . . . 8   
3.2 An illustrative example of two paths which intersect. 9   
3.3 An illustrative example of a mutated path. . 11   
4.1 First graph used to colect results. It has 134 vertices, 134 edges and around 2250 distinct paths. . . . . . . 14   
4.2 Second graph used to colect results. It has 74 vertices, 73 edges and around 700 distinct paths. 16   
4.3 Third graph used to colect results. It has 12 vertices, 11 edges and 21 distinct paths. . . . . . . . 17

# List of Tables

4.1 Results for the First Algorithm (GANP) using the graph on figure 4.1. . . 14   
4.2 Results for the Second Algorithm (GAIP) using the graph on figure 4.1. . . 15   
4.3 Results for the Third Algorithm (GABPP) using the graph on figure 4.1. . 15   
4.4 Results for the Fourth Algorithm (GAMM) using the graph on figure 4.1. . 15   
4.5 Results for the First Algorithm (GANP) using the graph on figure 4.2. . . 16   
4.6 Results for the Second Algorithm (GAIP) using the graph on figure 4.2. . . 16   
4.7 Results for the Third Algorithm (GABPP) using the graph on figure 4.2. . 17   
4.8 Results for the Fourth Algorithm (GAMM) using the graph on figure 4.2. . 17   
4.9 Results for the First Algorithm (GANP) using the graph on figure 4.3. . . 18   
4.10 Results for the Second Algorithm (GAIP) using the graph on figure 4.3. . . 18   
4.11 Results for the Third Algorithm (GABPP) using the graph on figure 4.3. . 18   
4.12 Results for the Fourth Algorithm (GAMM) using the graph on figure 4.3. . 19

# Chapter 1

# Introduction

# 1.1 The Longest Path Problem (LPP)

In this report, we address the problem of finding the longest path in a generic undirected graph G=(V, E). V is the set of $\boldsymbol { n }$ vertices and $\mathrm { E }$ is the set of $m$ edges. The goal is to find for all u, v ≤ V, the longest path from u to v, using weighted edges. We consider simple paths, which do not have any repeated edges or vertices. This problem belongs to the NP-Complete class of problems, as it is a generalization of the Hamiltonian path problem and cannot be solved in polynomial time unless P = NP. For this reason, proposed solutions are normally based on heuristics. The main objective of this work is to analyze and validate distinct approaches to solve this problem using genetic algorithms. A vast work in graph theory is already presented in the literature. In this paragraph, in particular, work concerning the longest path problem (LPP) and related issues is reviewed. Karger et al. [Karger et al., 1997] presented several polynomial-time approximation algorithms for the LPP in unweighted undirected graphs, with limited performance. Hardness results are provided to justify the difficulty of obtaining better performance guarantees for the longest path approximations and, in general, for NPcomplete problems. Additionally, a polynomial time approximation algorithm for the LPP is presented in [Gabow, 2004]. The method finds paths that have greater than polylogarithmic length. The main idea of the algorithm is to add edges $\boldsymbol { v } \boldsymbol { x }$ and vy to a 2 degree vertex v. By letting x and y vary; one can approximate the longest path and similarly the longest cycle in an undirected graph. More recently, an approximate and simplified search algorithm for the longest path in a graph was described in [Portugal and Rocha, 2010]. This was used for planning robot’s patrolling trajectories based on a topological graph-like representation. The algorithm is fast and always returns, at least, a sub-optimal solution. Monien [Monien, 1985] worked on finding arbitrary long paths with fixed length $k$ , which is a closely related issue to the LPP, and proved that they can be found in $O ( k ! n m )$ time, if they exist. Also, [Bodlaender, 1989] described a construction algorithm for cycles or paths with length≤ $k$ , that uses $O ( n )$ time, based on a depth first search approach, improving Monien’s bounds. Furthermore, a randomized method for finding paths of a specified length $k$ in generic graphs, which improved the worst-case bound of Bodlaender [Bodlaender, 1989] in undirected graphs, was described in [Alon et al., 1995]. The method was called color-coding. It detects, in polynomial time, if a path of length log(n) exists. Despite the NP nature of the general problem, conclusions have already been drawn from studying particular cases; moreover, polynomial solutions are known for specific classes of graphs. For example for directed acyclic graphs (DAGs) the problem is solvable in linear time by negating the edge weights and running a shortest-path algorithm like Bellman-Ford. Other different algorithms for DAGs have also been presented in [Ando et al., 2009] and [Wagner, 2004], the latter one being applied for studies with gene pairs in large genetic networks. On the other hand, [Uehara and Uno, 2004] showed that the LPP can be solved in polynomial time for (vertex/edge) weighted treelike graphs and discussed the complexity of the problem for other types of graphs. Following this work, an algorithm in [Ioannidou et al., 2009] that solves the LPP in polynomial time for interval graphs was presented. Finally, a different work that studies longest paths in combinational circuits which contain cycles was reported in [Hsu et al, 1998].

# 1.2 Genetic Algorithms (GAs)

In recent years, genetic algorithms (GAs) have become very popular for solving complex optimization and search problems. They are an evolutionary computing approach, inspired in Darwin’s theory about evolution and survival of the fittest. GAs are adaptive global search heuristic methods designed to find exact or approximate solutions by using inheritance, mutation, crossover and selection mechanisms with individuals, in order to form new and enhanced generations and converge to optimal solution(s).

Genetic approaches have been studied in many scientific fields and are commonly recognized for their performance. As a consequence, applications on graph theory problems have emerged in recent years. Wong et al. [Wong et al., 2005] described the GAroute, a query routing function in a Peer-to-Peer Network, which returns a list of routing paths that cover as many relevant peers as possible. This is equivalent to the LPP in a directed graph and the authors use GAs to obtain approximate solutions in polynomial time. Also working with network datasets, [Prager and Spears, 2009] uses an evolutionary approach together with graph-based computation to discover routes with specific functional characteristics in a network. Furthermore, [Nair and Skooda, 2009] deals with path selection from a known sender to the receiver aiming to maximize bandwidth along the forward channels while minimizing the route length. The authors compare a GA with a simulated annealing approach and conclude that the first one shows better convergence. Also, [Gelenbe et al., 2006] uses GAs for path discovery in cognitive packet networks, by combining paths that were previously discovered to create new valid paths, which are selected based on their fitness. In [Kumar et al., 2009], the problem of vehicle route selection to a given destination on an actual map under a static and constrained environment is addressed and a customized solution based on a GA is proposed. In the area of robotics, Solano and Jones [Solano and Jones, 1993] studied the generation of minimum distance paths for a mobile robot in an environment with a set of obstacles. The optimization of these paths is done by means of a genetic approach, which considers obstacle avoidance. In a similar work, [Davies and Jnifene, 2008] applies a GA path planner that optimizes and reduces the time for task completion of a set of three mobile robots that visit user-defined waypoints while not colliding to obstacles. Finally, another application on a classic graph theory problem is proposed in [Talbi and Bessi\`ere, 2004], which studies a genetic approach for partitioning graphs.

# 1.3 Outline of the document

This document is organized in different sections. The first chapter introduces some important issues, reviews the most relevant research work previously carried out concerning the LPP and GAs and describes how the report is organized.

The next section states the problem that is addressed and the subsequent section describes the proposed algorithms. Later on, the results are presented and discussed. The report ends with conclusions and future work and the referenced works in this document are presented in a separate bibliography section.

# Chapter 2

# Defining The Problem

It is not the objective of this report to describe a method to improve the bounds of the current existing algorithms for the LPP and demonstrate theoretical concepts to guarantee the detection of the optimal solution. Instead, the interest is focused on validating, by simulation, practical and reasonable fast approaches that offer high quality solutions and can be used in applications, which may admit sporadically sub-optimal solutions and where computational time is important. The initial motivation for developing this work was the same as in [Portugal and Rocha, 2010]: finding long paths in topological graphlike maps, which usually do not contain Euler or Hamilton paths, to use as a reference for patrolling an environment with multiple robots. The longest path does not typically visit all vertices of the graph. However, a post-processing phase can be done to compute detours for visiting unattended places to solve the patrolling problem. As seen on the previous section, other applications beyond multi-robot path planning may benefit from tackling the LPP and related problems, like routing in package networks, route planning for vehicles using GPS, measuring circuit’s performance and others.

As it was stated before, we will be using weighted edges which typically represent the distance/length between two vertices in the context of topological maps. Nevertheless, the proposed approaches may also be used with unweighted edges, by imposing the same cost for all edges. In that particular case of the problem, the longest path(s) will be the one(s) with the greater number of hops in the graph.

Genetic approaches have the ability to collect and apprehend important knowledge about the search space during its process and adapt future iterations according to previously obtained information through random optimization techniques. Taking the inherent knowledge within the search space into account, it is more likely to obtain the global optimal solution using a GA instead of a traditional search algorithm. The first three approaches used are based on crossover mechanisms, in which two parents create a set of offspring that share their genetic material. The last approach is based on mutations, in which each individual creates two offspring by perturbation on their genetic material in places specified according to the overall state of the system.

There are a number of common features in all algorithms. Each generated path is a legitimate solution and is represented as an ordered array of vertices with variable length. The choice of individuals for the next generation is done by means of a roulette wheel selection between parents and offspring based on a path cost fitness function. Also, explicit elitism is performed by choosing a small fraction of the best solutions to automatically carry on for the next generation. The stop condition for the algorithms relies on the stagnancy of the fittest solutions found during the search process. In the next section, the generation of the initial solution space is explained and the algorithms are presented.

# Chapter 3

# The Algorithms

All the proposed algorithms accept, as input, the population size (n) and the elitism fraction, and the output is (are) the best solution(s) obtained.

# 3.1 Generating initial solutions

One can achieve better results and earlier convergence by choosing an efficient method for generating initial solutions, in the context of the LPP using GAs. Since most of the algorithms herein analyzed strongly rely on the genetic material of the initial solution space, it is important to guarantee initial solutions with good quality; in this case, this corresponds to long and diverse initial paths. Initially, a random method was considered. It started by selecting a random vertex of the graph and compute paths by choosing neighbors of the current vertex at random, as long as they were not already included in the path. It finished computing the path when there were no available neighbors left. This proved to be an inefficient method, seeing as most of the paths computed would be very short, mostly because degree one vertices, i.e. vertices with only one neighbor, would be selected rather rapidly. To overcome this fact, a new method was proposed. The first vertex is still selected at random. However, the following vertices are selected with a probability according to their degree. For example, if two neighbors of a given vertex have degrees 3 and 1, the first one would be selected with a probability of 0.75 and the second one with 0.25. In addition, if we have reached a vertex with unavailable neighbors, instead of stopping the method, we analyze whether the degree of the first vertex is greater than one and keep computing the path to the opposite direction until reaching a finishing point for the method. This technique presented much better results in terms of initial generated paths than the first one and was used for producing the initial solution space, with size n, throughout the rest of the work. Since we are dealing with undirected graphs, we consider the path A-B-C, equivalent to C-B-A and we ensure that no equal solutions coexist in the solution space.

![](images/303679bce694dcd38dfc4d35df1b58f7e418406e0ec688ebbf1a220c06642a04.jpg)  
Figure 3.1: An illustrative example of two disconnected paths.

# 3.2 Algorithm 1: GA using non-intersecting paths (GANP)

The first algorithm generates new offspring based on parents with no common vertices. Assuming that we have the initial solutions space, a search takes place to find pairs of nonintersecting paths (that do not have common vertices). When a pair of disconnected paths is found, we search for an edge that connects both paths, by running through a path’s vertices and checking if any of them connects to the other path’s vertices using a single edge not included in any of the paths. Constraining to a single edge connection between both paths, not only drastically decreases the computational time, but it also proves to be efficient, as it will be seen in the results section. Figure 3.1 illustrates an example of two disconnected paths: [1 2 6 11 9] and [3 5 8 10]. The edge (6, 8) will connect both paths and four offspring are generated: [1 2 6 8 10], [1 2 6 8 5 3], [3 5 8 6 11 9] and [10 8 6 11 9]. Note that all offspring contain genetic material from both parents. After generating all offspring, it is necessary to select which solutions will carry on to the next generation. The elitist fraction of the previous generation is automatically saved and the rest of the solutions are picked using a roulette wheel selection between parents and offspring. This is done firstly by gathering all parents and descendants, then removing identical solutions in order to have only unique ones, computing their path cost (fitness function), and finally selecting them with a probability according to their cost. The higher the cost, the more likely it is that a given solution is chosen. After this step, the new generation with size n is created and the process can start again. As the process goes on, it is expected to run slower in the beginning and faster along time, due to the detection of longer paths over time, which reduces the probability of having disconnected pairs of solutions and less crossovers are made. After a few runs, the algorithm converges to a final solution. A stagnancy variable is responsible to monitor the changes of the best values obtained and after a pre-defined number of runs without improving, the algorithm stops.

![](images/afb2b9ac073debc83c8cf6a78901ea6c9d9bb4bbd980d51beaf165cfd386463f.jpg)  
Figure 3.2: An illustrative example of two paths which intersect.

# 3.3 Algorithm 2: GA using intersecting paths (GAIP)

The second algorithm generates new offspring based on parents which intersect. Assuming that we have the initial solutions space, a search takes place to find pairs of paths that intersect once (which have a common vertex, a common edge or a common set of edges). When a pair of intersecting paths is found, their intersection must be analyzed, since two different cases may occur:

∙ A crossroad, if they only have a common vertex, which means that this vertex has at least degree 4, and four offspring can be generated.

A junction, if they have a common edge or set of edges, which is the most usual case. They can generate only two descendants.

Figure 3.2 illustrates an example of the second case, two intersecting paths: [1 2 6 8 5 7] and [3 5 8 10] with (5, 8) as their common edge. Two offspring, which also incorporate the junction, can be generated: [1 2 6 8 5 3] and [10 8 5 7]. Note that all offspring contain genetic material from both parents. It is worth mentioning that if the junction occurs in the beginning (or end) of one or both paths, no offspring is generated, because it is not possible to create a descendant that contains the junction and the parents’ genetic material. Not doing anything in this case will benefit the computational time of this approach. Also, paths that contain two or more intersections are not considered. This case would imply the presence of cycles in the graph. Our algorithms can deal with cycles but, generally speaking, the existence of several cycles in a graph is not usual, hence there was no need to create an algorithm based on these cases. After generating all offspring, both the selection of paths to carry on to the next generation and the stopping condition are the same as in the previous algorithm. In this case, as the process goes on, it is expected to run faster in the beginning and slower along time, due to the detection of longer paths over time, which increases the probability of having intersecting paths and consequently more crossovers are required.

# 3.4 Algorithm 3: GA using both pairs of paths (GABPP)

The third algorithm basically incorporates both previous approaches. Assuming that we have the initial solutions space, a search takes place to find pairs of paths that intersect once and pairs of disconnected paths. Offspring are generated using the methods seen before, for each particular case. After generating all offspring, the selection of paths to carry on to the next generation and the stopping condition are the same as in the previous algorithms.

![](images/d477cc473eac0cf0536f11c785d455cf371b88a342243b1012d67c0cb298ee5c.jpg)  
Figure 3.3: An illustrative example of a mutated path.

# 3.5 Algorithm 4: GA using a mutation mechanism (GAMM)

Unlike the previous approaches, this algorithm does not rely on crossover mechanisms. Instead, it uses a mutation technique to generate descendants. A variable is initialized to measure the perturbation pressure. Assuming that we have the initial solution space, the mutation operator works as follows: it starts by going through all the paths, the perturbation pressure is evaluated and according to its scalar value a perturbation is applied close to the end of the path (low perturbation measures) or near the middle of the path (high perturbation measures). For each successful run, two offspring are generated per path consisting in two mutated solutions that result from the perturbation applied in the original path and in a flipped version of the original path, as seen on figure 3.3. The perturbation starts in a vertex that must have at least degree 3, since it cannot go backwards or to the next vertex of the original path. Therefore, a third vertex must be selected as an alternative to apply the mutation. From this point on, all following vertices are chosen, applying the same principle as in the generation of the initial solutions. Vertices with higher degree have higher probabilities of being picked, keeping in mind that no vertex already included in the path can be chosen again. As it was mentioned before, the starting point to compute the mutation depends on the perturbation pressure value. This value varies during the process, in order to adapt to the needs of the problem. If in a generation, there is no improvement of the solution obtained, the perturbation measure is incremented and in the next generation the perturbation pressure on the solutions is higher. This is aimed at bringing new genetic material into the population and therefore diversify the search into new regions of the search space in order to attempt escaping from local optima. To avoid the overgrowing of this value, we control the number of successful mutations. If in a given generation, no mutation was successful, it means that the perturbation value is too high (higher than half of the hops on all paths) and no mutation can be applied. In this case, we re-initialize the perturbation pressure. After generating all offspring, the selection of paths to carry on to the next generation and the stopping condition are the same as in the previous algorithms. The results show the great efficiency of this algorithm.

# Chapter 4

# Results and Discussion

After developing and testing the four algorithms it is time to analyze their performance.   
In this chapter, the simulation results are presented and discussed.

# 4.1 Simulation Results

All algorithms described were implemented in Matlab R2007b and simulation results were collected using an Intel Pentium Core 2 Quad 2.66GHz Desktop with 4 GB RAM. In Tables 4.1 to 4.4, we present the results for the four approaches using a graph with 134 vertices, shown in figure 4.1. In Tables 4.5 to 4.8, we present the results using a graph with 74 vertices, shown in figure 4.2 and in Tables 4.9 to 4.12, we present the results with a much simpler graph with 12 vertices, show in figure 4.3.   
Each row represents a sample of 10 runs of the corresponding algorithm with the parameters presented.

![](images/e016bcaa4dde9af6bba983ca0e49cc6911dcb1e1c499c3c6047cfc4d75a1a582.jpg)  
Figure 4.1: First graph used to colect results. It has 134 vertices, 134 edges and around 2250 distinct paths.

Table 4.1: Results for the First Algorithm (GANP) using the graph on figure 4.1.   

<table><tr><td rowspan=1 colspan=1>b</td><td rowspan=1 colspan=1>Elite (%)</td><td rowspan=1 colspan=1>Success</td><td rowspan=1 colspan=1>σw(%)</td><td rowspan=1 colspan=1>Avg. Time (s)</td><td rowspan=1 colspan=1>Avg. It.</td><td rowspan=1 colspan=1>Score (%)</td></tr><tr><td rowspan=1 colspan=1>200</td><td rowspan=1 colspan=1>10%</td><td rowspan=1 colspan=1>5/10</td><td rowspan=1 colspan=1>5.33%</td><td rowspan=1 colspan=1>249.46</td><td rowspan=1 colspan=1>4.4</td><td rowspan=1 colspan=1>98.74%</td></tr><tr><td rowspan=1 colspan=1>200</td><td rowspan=1 colspan=1>5%</td><td rowspan=1 colspan=1>7/10</td><td rowspan=1 colspan=1>1.67%</td><td rowspan=1 colspan=1>242.40</td><td rowspan=1 colspan=1>3.7</td><td rowspan=1 colspan=1>99.50%</td></tr><tr><td rowspan=1 colspan=1>200</td><td rowspan=1 colspan=1>1%</td><td rowspan=1 colspan=1>7/10</td><td rowspan=1 colspan=1>7.58%</td><td rowspan=1 colspan=1>241.70</td><td rowspan=1 colspan=1>3.3</td><td rowspan=1 colspan=1>98.62%</td></tr><tr><td rowspan=1 colspan=1>100</td><td rowspan=1 colspan=1>10%</td><td rowspan=1 colspan=1>1/10</td><td rowspan=1 colspan=1>9.13%</td><td rowspan=1 colspan=1>40.92</td><td rowspan=1 colspan=1>4.0</td><td rowspan=1 colspan=1>96.21%</td></tr><tr><td rowspan=1 colspan=1>100</td><td rowspan=1 colspan=1>5%</td><td rowspan=1 colspan=1>2/10</td><td rowspan=1 colspan=1>8.61%</td><td rowspan=1 colspan=1>39.89</td><td rowspan=1 colspan=1>3.7</td><td rowspan=1 colspan=1>96.54%</td></tr><tr><td rowspan=1 colspan=1>100</td><td rowspan=1 colspan=1>1%</td><td rowspan=1 colspan=1>4/10</td><td rowspan=1 colspan=1>3.92%</td><td rowspan=1 colspan=1>40.03</td><td rowspan=1 colspan=1>3.7</td><td rowspan=1 colspan=1>98.43%</td></tr><tr><td rowspan=1 colspan=1>50</td><td rowspan=1 colspan=1>10%</td><td rowspan=1 colspan=1>2/10</td><td rowspan=1 colspan=1>28.53%</td><td rowspan=1 colspan=1>8.40</td><td rowspan=1 colspan=1>4.1</td><td rowspan=1 colspan=1>87.43%</td></tr><tr><td rowspan=1 colspan=1>50</td><td rowspan=1 colspan=1>5%</td><td rowspan=1 colspan=1>1/10</td><td rowspan=1 colspan=1>18.19%</td><td rowspan=1 colspan=1>8.44</td><td rowspan=1 colspan=1>3.6</td><td rowspan=1 colspan=1>91.36%</td></tr><tr><td rowspan=1 colspan=1>50</td><td rowspan=1 colspan=1>2%</td><td rowspan=1 colspan=1>0/10</td><td rowspan=1 colspan=1>24.23%</td><td rowspan=1 colspan=1>7.80</td><td rowspan=1 colspan=1>3.5</td><td rowspan=1 colspan=1>86.48%</td></tr></table>

Table 4.2: Results for the Second Algorithm (GAIP) using the graph on figure 4.1.   

<table><tr><td rowspan=1 colspan=1>b</td><td rowspan=1 colspan=1>Elite (%)</td><td rowspan=1 colspan=1>Success</td><td rowspan=1 colspan=1>σw(%)</td><td rowspan=1 colspan=1>Avg. Time (s)</td><td rowspan=1 colspan=1>Avg. It.</td><td rowspan=1 colspan=1>Score (%)</td></tr><tr><td rowspan=1 colspan=1>200</td><td rowspan=1 colspan=1>10%</td><td rowspan=1 colspan=1>5/10</td><td rowspan=1 colspan=1>7.58%</td><td rowspan=1 colspan=1>482.95</td><td rowspan=1 colspan=1>5.4</td><td rowspan=1 colspan=1>98.00%</td></tr><tr><td rowspan=1 colspan=1>200</td><td rowspan=1 colspan=1>5%</td><td rowspan=1 colspan=1>1/10</td><td rowspan=1 colspan=1>17.87%</td><td rowspan=1 colspan=1>298.17</td><td rowspan=1 colspan=1>4.1</td><td rowspan=1 colspan=1>92.58%</td></tr><tr><td rowspan=1 colspan=1>200</td><td rowspan=1 colspan=1>1%</td><td rowspan=1 colspan=1>2/10</td><td rowspan=1 colspan=1>7.90%</td><td rowspan=1 colspan=1>372.54</td><td rowspan=1 colspan=1>4.6</td><td rowspan=1 colspan=1>96.80%</td></tr><tr><td rowspan=1 colspan=1>100</td><td rowspan=1 colspan=1>10%</td><td rowspan=1 colspan=1>0/10</td><td rowspan=1 colspan=1>26.29%</td><td rowspan=1 colspan=1>92.76</td><td rowspan=1 colspan=1>4.2</td><td rowspan=1 colspan=1>87.62%</td></tr><tr><td rowspan=1 colspan=1>100</td><td rowspan=1 colspan=1>5%</td><td rowspan=1 colspan=1>1/10</td><td rowspan=1 colspan=1>25.90%</td><td rowspan=1 colspan=1>176.24</td><td rowspan=1 colspan=1>5.6</td><td rowspan=1 colspan=1>87.87%</td></tr><tr><td rowspan=1 colspan=1>100</td><td rowspan=1 colspan=1>1%</td><td rowspan=1 colspan=1>0/10</td><td rowspan=1 colspan=1>12.02%</td><td rowspan=1 colspan=1>88.98</td><td rowspan=1 colspan=1>4.1</td><td rowspan=1 colspan=1>94.05%</td></tr><tr><td rowspan=1 colspan=1>50</td><td rowspan=1 colspan=1>10%</td><td rowspan=1 colspan=1>1/10</td><td rowspan=1 colspan=1>47.69%</td><td rowspan=1 colspan=1>12.13</td><td rowspan=1 colspan=1>3.6</td><td rowspan=1 colspan=1>76.79%</td></tr><tr><td rowspan=1 colspan=1>50</td><td rowspan=1 colspan=1>5%</td><td rowspan=1 colspan=1>0/10</td><td rowspan=1 colspan=1>38.75%</td><td rowspan=1 colspan=1>8.93</td><td rowspan=1 colspan=1>3.3</td><td rowspan=1 colspan=1>73.26%</td></tr><tr><td rowspan=1 colspan=1>50</td><td rowspan=1 colspan=1>2%</td><td rowspan=1 colspan=1>1/10</td><td rowspan=1 colspan=1>31.49%</td><td rowspan=1 colspan=1>10.78</td><td rowspan=1 colspan=1>3.2</td><td rowspan=1 colspan=1>83.49%</td></tr></table>

Table 4.3: Results for the Third Algorithm (GABPP) using the graph on figure 4.1.   

<table><tr><td rowspan=1 colspan=1>b</td><td rowspan=1 colspan=1>Elite (%)</td><td rowspan=1 colspan=1>Success</td><td rowspan=1 colspan=1>σw(%)</td><td rowspan=1 colspan=1>Avg. Time (s)</td><td rowspan=1 colspan=1>Avg. It.</td><td rowspan=1 colspan=1>Score (%)</td></tr><tr><td rowspan=1 colspan=1>200</td><td rowspan=1 colspan=1>10%</td><td rowspan=1 colspan=1>7/10</td><td rowspan=1 colspan=1>5.33%</td><td rowspan=1 colspan=1>581.54</td><td rowspan=1 colspan=1>4.8</td><td rowspan=1 colspan=1>99.07%</td></tr><tr><td rowspan=1 colspan=1>200</td><td rowspan=1 colspan=1>5%</td><td rowspan=1 colspan=1>3/10</td><td rowspan=1 colspan=1>10.80%</td><td rowspan=1 colspan=1>542.59</td><td rowspan=1 colspan=1>4.7</td><td rowspan=1 colspan=1>97.12%</td></tr><tr><td rowspan=1 colspan=1>200</td><td rowspan=1 colspan=1>1%</td><td rowspan=1 colspan=1>5/10</td><td rowspan=1 colspan=1>3.92%</td><td rowspan=1 colspan=1>775.86</td><td rowspan=1 colspan=1>5.0</td><td rowspan=1 colspan=1>98.54%</td></tr><tr><td rowspan=1 colspan=1>100</td><td rowspan=1 colspan=1>10%</td><td rowspan=1 colspan=1>5/10</td><td rowspan=1 colspan=1>7.58%</td><td rowspan=1 colspan=1>347.61</td><td rowspan=1 colspan=1>4.3</td><td rowspan=1 colspan=1>97.80%</td></tr><tr><td rowspan=1 colspan=1>100</td><td rowspan=1 colspan=1>5%</td><td rowspan=1 colspan=1>3/10</td><td rowspan=1 colspan=1>12.02%</td><td rowspan=1 colspan=1>510.01</td><td rowspan=1 colspan=1>6.5</td><td rowspan=1 colspan=1>97.06%</td></tr><tr><td rowspan=1 colspan=1>100</td><td rowspan=1 colspan=1>1%</td><td rowspan=1 colspan=1>5/10</td><td rowspan=1 colspan=1>5.46%</td><td rowspan=1 colspan=1>380.20</td><td rowspan=1 colspan=1>4.5</td><td rowspan=1 colspan=1>98.36%</td></tr><tr><td rowspan=1 colspan=1>50</td><td rowspan=1 colspan=1>10%</td><td rowspan=1 colspan=1>0/10</td><td rowspan=1 colspan=1>27.12%</td><td rowspan=1 colspan=1>141.18</td><td rowspan=1 colspan=1>4.3</td><td rowspan=1 colspan=1>87.08%</td></tr><tr><td rowspan=1 colspan=1>50</td><td rowspan=1 colspan=1>5%</td><td rowspan=1 colspan=1>1/10</td><td rowspan=1 colspan=1>24.10%</td><td rowspan=1 colspan=1>136.97</td><td rowspan=1 colspan=1>4.0</td><td rowspan=1 colspan=1>89.02%</td></tr><tr><td rowspan=1 colspan=1>50</td><td rowspan=1 colspan=1>2%</td><td rowspan=1 colspan=1>0/10</td><td rowspan=1 colspan=1>24.61%</td><td rowspan=1 colspan=1>162.70</td><td rowspan=1 colspan=1>4.9</td><td rowspan=1 colspan=1>87.19%</td></tr></table>

Table 4.4: Results for the Fourth Algorithm (GAMM) using the graph on figure 4.1.   

<table><tr><td rowspan=1 colspan=1>b</td><td rowspan=1 colspan=1>Elite (%)</td><td rowspan=1 colspan=1>Success</td><td rowspan=1 colspan=1>σw(%)</td><td rowspan=1 colspan=1>Avg. Time (s)</td><td rowspan=1 colspan=1>Avg. It.</td><td rowspan=1 colspan=1>Score (%)</td></tr><tr><td rowspan=1 colspan=1>400</td><td rowspan=1 colspan=1>10%</td><td rowspan=1 colspan=1>8/10</td><td rowspan=1 colspan=1>7.71%</td><td rowspan=1 colspan=1>41.11</td><td rowspan=1 colspan=1>6.2</td><td rowspan=1 colspan=1>98.84%</td></tr><tr><td rowspan=1 colspan=1>400</td><td rowspan=1 colspan=1>5%</td><td rowspan=1 colspan=1>5/10</td><td rowspan=1 colspan=1>6.36%</td><td rowspan=1 colspan=1>44.69</td><td rowspan=1 colspan=1>7.1</td><td rowspan=1 colspan=1>98.03%</td></tr><tr><td rowspan=1 colspan=1>400</td><td rowspan=1 colspan=1>1%</td><td rowspan=1 colspan=1>5/10</td><td rowspan=1 colspan=1>2.25%</td><td rowspan=1 colspan=1>41.38</td><td rowspan=1 colspan=1>6.5</td><td rowspan=1 colspan=1>98.99%</td></tr><tr><td rowspan=1 colspan=1>300</td><td rowspan=1 colspan=1>10%</td><td rowspan=1 colspan=1>7/10</td><td rowspan=1 colspan=1>5.33%</td><td rowspan=1 colspan=1>29.91</td><td rowspan=1 colspan=1>8.0</td><td rowspan=1 colspan=1>99.13%</td></tr><tr><td rowspan=1 colspan=1>300</td><td rowspan=1 colspan=1>5%</td><td rowspan=1 colspan=1>5/10</td><td rowspan=1 colspan=1>17.99%</td><td rowspan=1 colspan=1>22.24</td><td rowspan=1 colspan=1>6.2</td><td rowspan=1 colspan=1>96.29%</td></tr><tr><td rowspan=1 colspan=1>300</td><td rowspan=1 colspan=1>1%</td><td rowspan=1 colspan=1>6/10</td><td rowspan=1 colspan=1>7.71%</td><td rowspan=1 colspan=1>27.14</td><td rowspan=1 colspan=1>7.4</td><td rowspan=1 colspan=1>98.67%</td></tr><tr><td rowspan=1 colspan=1>200</td><td rowspan=1 colspan=1>10%</td><td rowspan=1 colspan=1>4/10</td><td rowspan=1 colspan=1>18.57%</td><td rowspan=1 colspan=1>11.32</td><td rowspan=1 colspan=1>5.8</td><td rowspan=1 colspan=1>95.46%</td></tr><tr><td rowspan=1 colspan=1>200</td><td rowspan=1 colspan=1>5%</td><td rowspan=1 colspan=1>4/10</td><td rowspan=1 colspan=1>24.10%</td><td rowspan=1 colspan=1>11.75</td><td rowspan=1 colspan=1>6.0</td><td rowspan=1 colspan=1>96.48%</td></tr><tr><td rowspan=1 colspan=1>200</td><td rowspan=1 colspan=1>1%</td><td rowspan=1 colspan=1>3/10</td><td rowspan=1 colspan=1>23.01%</td><td rowspan=1 colspan=1>11.00</td><td rowspan=1 colspan=1>5.7</td><td rowspan=1 colspan=1>93.37%</td></tr><tr><td rowspan=1 colspan=1>100</td><td rowspan=1 colspan=1>10%</td><td rowspan=1 colspan=1>4/10</td><td rowspan=1 colspan=1>24.04%</td><td rowspan=1 colspan=1>5.03</td><td rowspan=1 colspan=1>8.0</td><td rowspan=1 colspan=1>95.55%</td></tr><tr><td rowspan=1 colspan=1>100</td><td rowspan=1 colspan=1>5%</td><td rowspan=1 colspan=1>1/10</td><td rowspan=1 colspan=1>28.57%</td><td rowspan=1 colspan=1>3.92</td><td rowspan=1 colspan=1>6.3</td><td rowspan=1 colspan=1>94.01%</td></tr><tr><td rowspan=1 colspan=1>100</td><td rowspan=1 colspan=1>1%</td><td rowspan=1 colspan=1>2/10</td><td rowspan=1 colspan=1>20.24%</td><td rowspan=1 colspan=1>3.99</td><td rowspan=1 colspan=1>6.4</td><td rowspan=1 colspan=1>92.29%</td></tr></table>

![](images/4cef7048995667174d1f8c4db103c03915f923a420bf9b2d6fa4a6510dc71e58.jpg)  
Figure 4.2: Second graph used to colect results. It has 74 vertices, 73 edges and around 700 distinct paths.

Table 4.5: Results for the First Algorithm (GANP) using the graph on figure 4.2.   

<table><tr><td rowspan=1 colspan=1>b</td><td rowspan=1 colspan=1>Elite (%)</td><td rowspan=1 colspan=1>Success</td><td rowspan=1 colspan=1>σw(%)</td><td rowspan=1 colspan=1>Avg. Time (s)</td><td rowspan=1 colspan=1>Avg. It.</td><td rowspan=1 colspan=1>Score (%)</td></tr><tr><td rowspan=1 colspan=1>150</td><td rowspan=1 colspan=1>10%</td><td rowspan=1 colspan=1>9/10</td><td rowspan=1 colspan=1>0.28%</td><td rowspan=1 colspan=1>56.12</td><td rowspan=1 colspan=1>1.5</td><td rowspan=1 colspan=1>99.97%</td></tr><tr><td rowspan=1 colspan=1>150</td><td rowspan=1 colspan=1>5%</td><td rowspan=1 colspan=1>10/10</td><td rowspan=1 colspan=1>0%</td><td rowspan=1 colspan=1>70.29</td><td rowspan=1 colspan=1>2.3</td><td rowspan=1 colspan=1>100%</td></tr><tr><td rowspan=1 colspan=1>150</td><td rowspan=1 colspan=1>1%</td><td rowspan=1 colspan=1>10/10</td><td rowspan=1 colspan=1>0%</td><td rowspan=1 colspan=1>73.75</td><td rowspan=1 colspan=1>2.6</td><td rowspan=1 colspan=1>100%</td></tr><tr><td rowspan=1 colspan=1>75</td><td rowspan=1 colspan=1>10%</td><td rowspan=1 colspan=1>6/10</td><td rowspan=1 colspan=1>0.85%</td><td rowspan=1 colspan=1>12.25</td><td rowspan=1 colspan=1>2.8</td><td rowspan=1 colspan=1>99.83%</td></tr><tr><td rowspan=1 colspan=1>75</td><td rowspan=1 colspan=1>5%</td><td rowspan=1 colspan=1>4/10</td><td rowspan=1 colspan=1>2.36%</td><td rowspan=1 colspan=1>13.52</td><td rowspan=1 colspan=1>3.0</td><td rowspan=1 colspan=1>99.45%</td></tr><tr><td rowspan=1 colspan=1>75</td><td rowspan=1 colspan=1>1%</td><td rowspan=1 colspan=1>4/10</td><td rowspan=1 colspan=1>0.28%</td><td rowspan=1 colspan=1>11.48</td><td rowspan=1 colspan=1>2.3</td><td rowspan=1 colspan=1>99.83%</td></tr><tr><td rowspan=1 colspan=1>40</td><td rowspan=1 colspan=1>10%</td><td rowspan=1 colspan=1>1/10</td><td rowspan=1 colspan=1>6.98%</td><td rowspan=1 colspan=1>2.90</td><td rowspan=1 colspan=1>2.8</td><td rowspan=1 colspan=1>96.34%</td></tr><tr><td rowspan=1 colspan=1>40</td><td rowspan=1 colspan=1>5%</td><td rowspan=1 colspan=1>1/10</td><td rowspan=1 colspan=1>3.21%</td><td rowspan=1 colspan=1>3.11</td><td rowspan=1 colspan=1>3.1</td><td rowspan=1 colspan=1>98.07%</td></tr><tr><td rowspan=1 colspan=1>40</td><td rowspan=1 colspan=1>2%</td><td rowspan=1 colspan=1>3/10</td><td rowspan=1 colspan=1>6.89%</td><td rowspan=1 colspan=1>2.95</td><td rowspan=1 colspan=1>2.8</td><td rowspan=1 colspan=1>98.18%</td></tr></table>

Table 4.6: Results for the Second Algorithm (GAIP) using the graph on figure 4.2.   

<table><tr><td rowspan=1 colspan=1>b</td><td rowspan=1 colspan=1>Elite (%)</td><td rowspan=1 colspan=1>Success</td><td rowspan=1 colspan=1>σw(%)</td><td rowspan=1 colspan=1>Avg. Time (s)</td><td rowspan=1 colspan=1>Avg. It.</td><td rowspan=1 colspan=1>Score (%)</td></tr><tr><td rowspan=1 colspan=1>75</td><td rowspan=1 colspan=1>10%</td><td rowspan=1 colspan=1>6/10</td><td rowspan=1 colspan=1>2.36%</td><td rowspan=1 colspan=1>79.80</td><td rowspan=1 colspan=1>4.5</td><td rowspan=1 colspan=1>99.68%</td></tr><tr><td rowspan=1 colspan=1>75</td><td rowspan=1 colspan=1>5%</td><td rowspan=1 colspan=1>9/10</td><td rowspan=1 colspan=1>0.28%</td><td rowspan=1 colspan=1>68.44</td><td rowspan=1 colspan=1>4.1</td><td rowspan=1 colspan=1>99.97%</td></tr><tr><td rowspan=1 colspan=1>75</td><td rowspan=1 colspan=1>1%</td><td rowspan=1 colspan=1>9/10</td><td rowspan=1 colspan=1>2.64%</td><td rowspan=1 colspan=1>69.95</td><td rowspan=1 colspan=1>4.1</td><td rowspan=1 colspan=1>99.74%</td></tr><tr><td rowspan=1 colspan=1>50</td><td rowspan=1 colspan=1>10%</td><td rowspan=1 colspan=1>5/10</td><td rowspan=1 colspan=1>7.08%</td><td rowspan=1 colspan=1>14.62</td><td rowspan=1 colspan=1>4.3</td><td rowspan=1 colspan=1>98.56%</td></tr><tr><td rowspan=1 colspan=1>50</td><td rowspan=1 colspan=1>5%</td><td rowspan=1 colspan=1>2/10</td><td rowspan=1 colspan=1>7.36%</td><td rowspan=1 colspan=1>15.98</td><td rowspan=1 colspan=1>4.7</td><td rowspan=1 colspan=1>97.19%</td></tr><tr><td rowspan=1 colspan=1>50</td><td rowspan=1 colspan=1>2%</td><td rowspan=1 colspan=1>5/10</td><td rowspan=1 colspan=1>19.91%</td><td rowspan=1 colspan=1>17.57</td><td rowspan=1 colspan=1>5.1</td><td rowspan=1 colspan=1>97.24%</td></tr><tr><td rowspan=1 colspan=1>25</td><td rowspan=1 colspan=1>10%</td><td rowspan=1 colspan=1>1/10</td><td rowspan=1 colspan=1>46.23%</td><td rowspan=1 colspan=1>1.12</td><td rowspan=1 colspan=1>3.6</td><td rowspan=1 colspan=1>87.25%</td></tr><tr><td rowspan=1 colspan=1>25</td><td rowspan=1 colspan=1>4%</td><td rowspan=1 colspan=1>1/10</td><td rowspan=1 colspan=1>27.83%</td><td rowspan=1 colspan=1>0.89</td><td rowspan=1 colspan=1>2.4</td><td rowspan=1 colspan=1>87.19%</td></tr></table>

Table 4.7: Results for the Third Algorithm (GABPP) using the graph on figure 4.2.   

<table><tr><td rowspan=1 colspan=1>b</td><td rowspan=1 colspan=1>Elite (%)</td><td rowspan=1 colspan=1>Success</td><td rowspan=1 colspan=1>σw(%)</td><td rowspan=1 colspan=1>Avg. Time (s)</td><td rowspan=1 colspan=1>Avg. It.</td><td rowspan=1 colspan=1>Score (%)</td></tr><tr><td rowspan=1 colspan=1>75</td><td rowspan=1 colspan=1>10%</td><td rowspan=1 colspan=1>9/10</td><td rowspan=1 colspan=1>0.28%</td><td rowspan=1 colspan=1>276.26</td><td rowspan=1 colspan=1>5.6</td><td rowspan=1 colspan=1>99.97%</td></tr><tr><td rowspan=1 colspan=1>75</td><td rowspan=1 colspan=1>5%</td><td rowspan=1 colspan=1>8/10</td><td rowspan=1 colspan=1>2.36%</td><td rowspan=1 colspan=1>209.40</td><td rowspan=1 colspan=1>4.1</td><td rowspan=1 colspan=1>99.74%</td></tr><tr><td rowspan=1 colspan=1>75</td><td rowspan=1 colspan=1>1%</td><td rowspan=1 colspan=1>10/10</td><td rowspan=1 colspan=1>0%</td><td rowspan=1 colspan=1>201.35</td><td rowspan=1 colspan=1>3.9</td><td rowspan=1 colspan=1>100%</td></tr><tr><td rowspan=1 colspan=1>50</td><td rowspan=1 colspan=1>10%</td><td rowspan=1 colspan=1>7/10</td><td rowspan=1 colspan=1>2.36%</td><td rowspan=1 colspan=1>117.18</td><td rowspan=1 colspan=1>5.5</td><td rowspan=1 colspan=1>99.71%</td></tr><tr><td rowspan=1 colspan=1>50</td><td rowspan=1 colspan=1>5%</td><td rowspan=1 colspan=1>5/10</td><td rowspan=1 colspan=1>2.36%</td><td rowspan=1 colspan=1>94.63</td><td rowspan=1 colspan=1>4.2</td><td rowspan=1 colspan=1>99.44%</td></tr><tr><td rowspan=1 colspan=1>50</td><td rowspan=1 colspan=1>2%</td><td rowspan=1 colspan=1>6/10</td><td rowspan=1 colspan=1>0.85%</td><td rowspan=1 colspan=1>82.09</td><td rowspan=1 colspan=1>4.2</td><td rowspan=1 colspan=1>99.83%</td></tr><tr><td rowspan=1 colspan=1>25</td><td rowspan=1 colspan=1>10%</td><td rowspan=1 colspan=1>2/10</td><td rowspan=1 colspan=1>43.30%</td><td rowspan=1 colspan=1>17.06</td><td rowspan=1 colspan=1>4.1</td><td rowspan=1 colspan=1>92.40%</td></tr><tr><td rowspan=1 colspan=1>25</td><td rowspan=1 colspan=1>4%</td><td rowspan=1 colspan=1>1/10</td><td rowspan=1 colspan=1>7.92%</td><td rowspan=1 colspan=1>15.08</td><td rowspan=1 colspan=1>3.5</td><td rowspan=1 colspan=1>97.50%</td></tr></table>

Table 4.8: Results for the Fourth Algorithm (GAMM) using the graph on figure 4.2.   

<table><tr><td rowspan=1 colspan=1>b</td><td rowspan=1 colspan=1>Elite (%)</td><td rowspan=1 colspan=1>Success</td><td rowspan=1 colspan=1>σw(%)</td><td rowspan=1 colspan=1>Avg. Time (s)</td><td rowspan=1 colspan=1>Avg. It.</td><td rowspan=1 colspan=1>Score (%)</td></tr><tr><td rowspan=1 colspan=1>300</td><td rowspan=1 colspan=1>10%</td><td rowspan=1 colspan=1>9/10</td><td rowspan=1 colspan=1>0.28%</td><td rowspan=1 colspan=1>11.38</td><td rowspan=1 colspan=1>2.9</td><td rowspan=1 colspan=1>99.97%</td></tr><tr><td rowspan=1 colspan=1>300</td><td rowspan=1 colspan=1>5%</td><td rowspan=1 colspan=1>9/10</td><td rowspan=1 colspan=1>0.28%</td><td rowspan=1 colspan=1>13.84</td><td rowspan=1 colspan=1>3.8</td><td rowspan=1 colspan=1>99.97%</td></tr><tr><td rowspan=1 colspan=1>300</td><td rowspan=1 colspan=1>1%</td><td rowspan=1 colspan=1>7/10</td><td rowspan=1 colspan=1>0.28%</td><td rowspan=1 colspan=1>10.27</td><td rowspan=1 colspan=1>2.6</td><td rowspan=1 colspan=1>99.92%</td></tr><tr><td rowspan=1 colspan=1>200</td><td rowspan=1 colspan=1>10%</td><td rowspan=1 colspan=1>7/10</td><td rowspan=1 colspan=1>0.85%</td><td rowspan=1 colspan=1>6.00</td><td rowspan=1 colspan=1>3.2</td><td rowspan=1 colspan=1>99.86%</td></tr><tr><td rowspan=1 colspan=1>200</td><td rowspan=1 colspan=1>5%</td><td rowspan=1 colspan=1>7/10</td><td rowspan=1 colspan=1>3.21%</td><td rowspan=1 colspan=1>6.02</td><td rowspan=1 colspan=1>3.4</td><td rowspan=1 colspan=1>99.57%</td></tr><tr><td rowspan=1 colspan=1>200</td><td rowspan=1 colspan=1>1%</td><td rowspan=1 colspan=1>8/10</td><td rowspan=1 colspan=1>0.85%</td><td rowspan=1 colspan=1>6.10</td><td rowspan=1 colspan=1>3.4</td><td rowspan=1 colspan=1>99.89%</td></tr><tr><td rowspan=1 colspan=1>100</td><td rowspan=1 colspan=1>10%</td><td rowspan=1 colspan=1>7/10</td><td rowspan=1 colspan=1>2.64%</td><td rowspan=1 colspan=1>3.01</td><td rowspan=1 colspan=1>5.1</td><td rowspan=1 colspan=1>99.68%</td></tr><tr><td rowspan=1 colspan=1>100</td><td rowspan=1 colspan=1>5%</td><td rowspan=1 colspan=1>8/10</td><td rowspan=1 colspan=1>0.85%</td><td rowspan=1 colspan=1>2.78</td><td rowspan=1 colspan=1>4.8</td><td rowspan=1 colspan=1>99.89%</td></tr><tr><td rowspan=1 colspan=1>100</td><td rowspan=1 colspan=1>1%</td><td rowspan=1 colspan=1>4/10</td><td rowspan=1 colspan=1>0.85%</td><td rowspan=1 colspan=1>2.66</td><td rowspan=1 colspan=1>4.6</td><td rowspan=1 colspan=1>99.72%</td></tr><tr><td rowspan=1 colspan=1>50</td><td rowspan=1 colspan=1>10%</td><td rowspan=1 colspan=1>2/10</td><td rowspan=1 colspan=1>13.11%</td><td rowspan=1 colspan=1>1.07</td><td rowspan=1 colspan=1>4.6</td><td rowspan=1 colspan=1>95.54%</td></tr><tr><td rowspan=1 colspan=1>50</td><td rowspan=1 colspan=1>5%</td><td rowspan=1 colspan=1>4/10</td><td rowspan=1 colspan=1>4.62%</td><td rowspan=1 colspan=1>1.32</td><td rowspan=1 colspan=1>5.9</td><td rowspan=1 colspan=1>98.87%</td></tr><tr><td rowspan=1 colspan=1>50</td><td rowspan=1 colspan=1>2%</td><td rowspan=1 colspan=1>1/10</td><td rowspan=1 colspan=1>8.58%</td><td rowspan=1 colspan=1>1.23</td><td rowspan=1 colspan=1>5.0</td><td rowspan=1 colspan=1>97.08%</td></tr></table>

![](images/2513666b3499c3c84e04ef91b409bba0d87dd38b19ab785a12798dee03b53938.jpg)  
Figure 4.3: Third graph used to colect results. It has 12 vertices, 11 edges and 21 distinct paths.

Table 4.9: Results for the First Algorithm (GANP) using the graph on figure 4.3.   

<table><tr><td rowspan=1 colspan=1>b</td><td rowspan=1 colspan=1>Elite (%)</td><td rowspan=1 colspan=1>Success</td><td rowspan=1 colspan=1>σw(%)</td><td rowspan=1 colspan=1>Avg. Time (s)</td><td rowspan=1 colspan=1>Avg. It.</td><td rowspan=1 colspan=1>Score (%)</td></tr><tr><td rowspan=1 colspan=1>15</td><td rowspan=1 colspan=1>14%</td><td rowspan=1 colspan=1>10/10</td><td rowspan=1 colspan=1>0%</td><td rowspan=1 colspan=1>0.19</td><td rowspan=1 colspan=1>1.1</td><td rowspan=1 colspan=1>100%</td></tr><tr><td rowspan=1 colspan=1>15</td><td rowspan=1 colspan=1>7%</td><td rowspan=1 colspan=1>10/10</td><td rowspan=1 colspan=1>0%</td><td rowspan=1 colspan=1>0.20</td><td rowspan=1 colspan=1>1.2</td><td rowspan=1 colspan=1>100%</td></tr><tr><td rowspan=1 colspan=1>10</td><td rowspan=1 colspan=1>20%</td><td rowspan=1 colspan=1>9/10</td><td rowspan=1 colspan=1>1.13%</td><td rowspan=1 colspan=1>0.16</td><td rowspan=1 colspan=1>1.2</td><td rowspan=1 colspan=1>99.89%</td></tr><tr><td rowspan=1 colspan=1>10</td><td rowspan=1 colspan=1>10%</td><td rowspan=1 colspan=1>9/10</td><td rowspan=1 colspan=1>1.13%</td><td rowspan=1 colspan=1>0.16</td><td rowspan=1 colspan=1>1.1</td><td rowspan=1 colspan=1>99.89%</td></tr><tr><td rowspan=1 colspan=1>5</td><td rowspan=1 colspan=1>40%</td><td rowspan=1 colspan=1>4/10</td><td rowspan=1 colspan=1>21.90%</td><td rowspan=1 colspan=1>0.13</td><td rowspan=1 colspan=1>1.1</td><td rowspan=1 colspan=1>95.60%</td></tr><tr><td rowspan=1 colspan=1>5</td><td rowspan=1 colspan=1>20%</td><td rowspan=1 colspan=1>1/10</td><td rowspan=1 colspan=1>21.90%</td><td rowspan=1 colspan=1>0.14</td><td rowspan=1 colspan=1>1.0</td><td rowspan=1 colspan=1>93.63%</td></tr></table>

Table 4.10: Results for the Second Algorithm (GAIP) using the graph on figure 4.3.   

<table><tr><td rowspan=1 colspan=1>b</td><td rowspan=1 colspan=1>Elite (%)</td><td rowspan=1 colspan=1>Success</td><td rowspan=1 colspan=1>σw(%)</td><td rowspan=1 colspan=1>Avg. Time (s)</td><td rowspan=1 colspan=1>Avg. It.</td><td rowspan=1 colspan=1>Score (%)</td></tr><tr><td rowspan=1 colspan=1>15</td><td rowspan=1 colspan=1>14%</td><td rowspan=1 colspan=1>10/10</td><td rowspan=1 colspan=1>0%</td><td rowspan=1 colspan=1>0.20</td><td rowspan=1 colspan=1>1.1</td><td rowspan=1 colspan=1>100%</td></tr><tr><td rowspan=1 colspan=1>15</td><td rowspan=1 colspan=1>7%</td><td rowspan=1 colspan=1>10/10</td><td rowspan=1 colspan=1>0%</td><td rowspan=1 colspan=1>0.21</td><td rowspan=1 colspan=1>1.0</td><td rowspan=1 colspan=1>100%</td></tr><tr><td rowspan=1 colspan=1>10</td><td rowspan=1 colspan=1>20%</td><td rowspan=1 colspan=1>8/10</td><td rowspan=1 colspan=1>1.13%</td><td rowspan=1 colspan=1>0.17</td><td rowspan=1 colspan=1>1.4</td><td rowspan=1 colspan=1>99.77%</td></tr><tr><td rowspan=1 colspan=1>10</td><td rowspan=1 colspan=1>10%</td><td rowspan=1 colspan=1>8/10</td><td rowspan=1 colspan=1>9.48%</td><td rowspan=1 colspan=1>0.16</td><td rowspan=1 colspan=1>1.3</td><td rowspan=1 colspan=1>98.94%</td></tr><tr><td rowspan=1 colspan=1>5</td><td rowspan=1 colspan=1>40%</td><td rowspan=1 colspan=1>3/10</td><td rowspan=1 colspan=1>9.93%</td><td rowspan=1 colspan=1>0.13</td><td rowspan=1 colspan=1>2.2</td><td rowspan=1 colspan=1>98.53%</td></tr><tr><td rowspan=1 colspan=1>5</td><td rowspan=1 colspan=1>20%</td><td rowspan=1 colspan=1>2/10</td><td rowspan=1 colspan=1>21.44%</td><td rowspan=1 colspan=1>0.13</td><td rowspan=1 colspan=1>1.3</td><td rowspan=1 colspan=1>97.20%</td></tr></table>

Table 4.11: Results for the Third Algorithm (GABPP) using the graph on figure 4.3.   

<table><tr><td rowspan=1 colspan=1>b</td><td rowspan=1 colspan=1>Elite (%)</td><td rowspan=1 colspan=1>Success</td><td rowspan=1 colspan=1>σw(%)</td><td rowspan=1 colspan=1>Avg. Time (s)</td><td rowspan=1 colspan=1>Avg. It.</td><td rowspan=1 colspan=1>Score (%)</td></tr><tr><td rowspan=1 colspan=1>15</td><td rowspan=1 colspan=1>14%</td><td rowspan=1 colspan=1>10/10</td><td rowspan=1 colspan=1>0%</td><td rowspan=1 colspan=1>0.50</td><td rowspan=1 colspan=1>1.1</td><td rowspan=1 colspan=1>100%</td></tr><tr><td rowspan=1 colspan=1>15</td><td rowspan=1 colspan=1>7%</td><td rowspan=1 colspan=1>10/10</td><td rowspan=1 colspan=1>0%</td><td rowspan=1 colspan=1>0.47</td><td rowspan=1 colspan=1>1.0</td><td rowspan=1 colspan=1>100%</td></tr><tr><td rowspan=1 colspan=1>10</td><td rowspan=1 colspan=1>20%</td><td rowspan=1 colspan=1>10/10</td><td rowspan=1 colspan=1>0%</td><td rowspan=1 colspan=1>0.32</td><td rowspan=1 colspan=1>1.0</td><td rowspan=1 colspan=1>100%</td></tr><tr><td rowspan=1 colspan=1>10</td><td rowspan=1 colspan=1>10%</td><td rowspan=1 colspan=1>10/10</td><td rowspan=1 colspan=1>0%</td><td rowspan=1 colspan=1>0.34</td><td rowspan=1 colspan=1>1.1</td><td rowspan=1 colspan=1>100%</td></tr><tr><td rowspan=1 colspan=1>5</td><td rowspan=1 colspan=1>40%</td><td rowspan=1 colspan=1>5/10</td><td rowspan=1 colspan=1>1.13%</td><td rowspan=1 colspan=1>0.19</td><td rowspan=1 colspan=1>1.5</td><td rowspan=1 colspan=1>99.50%</td></tr><tr><td rowspan=1 colspan=1>5</td><td rowspan=1 colspan=1>20%</td><td rowspan=1 colspan=1>9/10</td><td rowspan=1 colspan=1>1.13%</td><td rowspan=1 colspan=1>0.20</td><td rowspan=1 colspan=1>1.4</td><td rowspan=1 colspan=1>99.89%</td></tr></table>

Table 4.12: Results for the Fourth Algorithm (GAMM) using the graph on figure 4.3.   

<table><tr><td rowspan=1 colspan=1>b</td><td rowspan=1 colspan=1>Elite (%)</td><td rowspan=1 colspan=1>Success</td><td rowspan=1 colspan=1>σw(%)</td><td rowspan=1 colspan=1>Avg. Time (s)</td><td rowspan=1 colspan=1>Avg. It.</td><td rowspan=1 colspan=1>Score (%)</td></tr><tr><td rowspan=1 colspan=1>15</td><td rowspan=1 colspan=1>14%</td><td rowspan=1 colspan=1>10/10</td><td rowspan=1 colspan=1>0%</td><td rowspan=1 colspan=1>0.24</td><td rowspan=1 colspan=1>1.1</td><td rowspan=1 colspan=1>100%</td></tr><tr><td rowspan=1 colspan=1>15</td><td rowspan=1 colspan=1>7%</td><td rowspan=1 colspan=1>9/10</td><td rowspan=1 colspan=1>0.45%</td><td rowspan=1 colspan=1>0.24</td><td rowspan=1 colspan=1>1.0</td><td rowspan=1 colspan=1>99.95%</td></tr><tr><td rowspan=1 colspan=1>10</td><td rowspan=1 colspan=1>20%</td><td rowspan=1 colspan=1>8/10</td><td rowspan=1 colspan=1>1.13%</td><td rowspan=1 colspan=1>0.22</td><td rowspan=1 colspan=1>1.5</td><td rowspan=1 colspan=1>99.84%</td></tr><tr><td rowspan=1 colspan=1>10</td><td rowspan=1 colspan=1>10%</td><td rowspan=1 colspan=1>9/10</td><td rowspan=1 colspan=1>1.13%</td><td rowspan=1 colspan=1>0.22</td><td rowspan=1 colspan=1>1.8</td><td rowspan=1 colspan=1>99.89%</td></tr><tr><td rowspan=1 colspan=1>5</td><td rowspan=1 colspan=1>40%</td><td rowspan=1 colspan=1>6/10</td><td rowspan=1 colspan=1>9.48%</td><td rowspan=1 colspan=1>0.20</td><td rowspan=1 colspan=1>1.9</td><td rowspan=1 colspan=1>98.78%</td></tr><tr><td rowspan=1 colspan=1>5</td><td rowspan=1 colspan=1>20%</td><td rowspan=1 colspan=1>7/10</td><td rowspan=1 colspan=1>9.48%</td><td rowspan=1 colspan=1>0.19</td><td rowspan=1 colspan=1>1.9</td><td rowspan=1 colspan=1>98.96%</td></tr></table>

n - Population Size. Elite ( $\%$ ) - Elite Fraction. Success - Number of successful times to achieve the Longest Path. $\sigma _ { \mathrm { w } }$ - Worst Deviation Obtained. Avg.Time - Average Time to Converge. Avg.It. - Average Iteration to Converge. Score - Overall Score (measures the quality of the solutions obtained).

# 4.2 Discussion

The first approach (GANP) scored the best overall results. For example, the longest path was found 7 times out of 10 for a population of 200 individuals with elite size of 5% and $1 \%$ using the first graph. In the first case, the 3 results that did not achieve the global optimum converged to the second longest path, hence the overall score of 99,5%. Also, GANP presents good results with population of medium sizes in reasonable computational time and becomes much slower with large populations. Apparently, the improvement of the overall scores does not justify the extra computational time; however the probability of finding the longest path increases significantly.

The second algorithm (GAIP) scored the worst results. The algorithm is slower, because much more operations are made during one run, when compared to the first algorithm. Results suggest that the algorithm’s design could be improved in a way to filter out most of the operations which may be considered unnecessary (i.e., that provide worse paths than their ancestors) in order to reduce the computational time.

The third algorithm (GABPP) got much better results than the previous (GAIP) and similar results to the first one (GANP). Despite this, the approach is even slower and is not appropriate for fast applications. With lower population sizes, for the same parameters, when compared to the first algorithm it had a slightly worse score probably because the second approach generates more solutions than the first (when run together) and the paths that resulted from the first approach, which may be overly better, have less probability to be chosen.

Although not scoring the best results, GAMM algorithm is the most appropriate for applications in which time is critical. This approach has the best compromise between quality and computational time. Since there is no crossover, the algorithm does not need an inner loop like the others. Hence, it is around 10 times faster than GANP for a population of 100 individuals and around 100 times faster than the GAIP for the same case. Every offspring is generated from a single parent and the results obtained are very good. Even tests with large population sizes run very quickly. Note that in the case of a population size of 400, with a $1 0 \%$ elite group using the first graph, the longest path was reached 8 times out of 10. Another interesting aspect of this approach is that it normally needs a higher number of iterations to converge when compared to the other approaches and when the same population sizes are used. As seen before, the longest path of the graphs were known ahead. This was only possible by running a brute-force search and confirming it through visual inspection.

It is not clear which is the appropriate elite fraction to use for each approach. Results denote an apparent pattern where 1-5% groups perform better for smaller population sizes and 5-10% fractions are favourable otherwise. The choice of this value is important to avoid imposing too much selective pressure and a premature convergence to a local optimum.

# Chapter 5

# Conclusions

In this last chapter, a global and self-critical overview of the proposed approaches takes place in order to sum up the work. Also, possible related future work directions are discussed.

# 5.1 Overview

Genetic algorithms resemble aspects of biological evolution, through an adaptive search procedure that applies the process of natural selection and the principle of survival of the fittest. In each generation, solutions compete for selection and the procedure favours fitter solutions over poorer ones. When the successful candidates are chosen, the recombination and mutation operators take place and the procedure is repeated for a convenient number of generations, producing higher-quality solutions, which are focused in regions of the search space where good solutions have already been found. In this report, four different approaches based on Genetic Algorithms were proposed to solve the Longest Path Problem. Three of them rely on crossover mechanisms involving pairs of solutions and the final one relies on a mutation mechanism involving one single parent. Generally, all the approaches guarantee high quality results when using appropriate parameters. Results obtained also showed, in terms of score, that the first algorithm has the best performance in reasonable computational time bounds. Both the second and third algorithms, although obtaining good results, require long time to compute a final solution. Finally, the fourth algorithm is the fastest, the one with better score/complexity ratio and the more appropriate for applications where time is critical.

# 5.2 Future Work

The inferior results that were obtained, namely in the time complexity of the second and third approach, could be strengthened in future work by filtering out a great deal of unnecessary operations that occur during these processes. Also, it would be interesting to test these approaches using a more optimized programming language, e.g. C/C++, to verify the speed of computation.

# Bibliography

[Karger et al., 1997] D. Karger, R. Montwani and G. Ramkumar, On approximating the longest path in a graph, Journal Algorithmica, Springer New York, ISSN 0178-4617, Vol. 18, No. 1, pp. 92-98, May, 1997.   
[Gabow, 2004] H. Gabow, Finding paths and cycles of superplylogarithmic length, In Proceedings of the 36th annual ACM symposium on Theory of computing (STOC’04), ISBN 1-58113-852-0, pp. 407-416, Chicago, Illinois, U.S.A., 2004.   
[Portugal and Rocha, 2010] D. Portugal and R. Rocha, MSP Algorithm: Multi-Robot Patrolling based on Territory Allocation using Balanced Graph Partitioning, In Proceedings of 25th ACM Symposium on Applied Computing (SAC’2010), Special Track on Intelligent Robotic Systems (ROBOT), Sierre, Switzerland, March 22-26, 2010.   
[Monien, 1985] B. Monien, How to find long paths efficiently, Annals of Discrete Mathematics, Elsevier Science Publishers B.V., Vol. 25, pp. 239-254, 1985.   
[Bodlaender, 1989] H. Bodlaender, On linear time minor tests and depth first search, In Proceedings of Workshop on Algorithms and Data Structures (WADS’89), pp. 577-590, Springer-Verlag, Lecture Notes in Computer Science, Vol. 382, Ottawa, Canada, August 17-19, 1989.

[Alon et al., 1995]

N. Alon, R. Yuster and U. Zwick, Color-coding, Journal of the ACM (JACM), ISSN 0004-5411, Vol. 42, Issue 4, pp. 844-856, July, 1995.

[Ando et al., 2009]

E. Ando, T. Nakata, and M. Yamashita, Approximating the Longest Path Length of a Stochastic DAG by a Normal Distribution in Linear Time, Journal of Discrete Algorithms, ISSN 1570-8667, Vol. 7, No. 4, pp. 420-438, December, 2009.

[Wagner, 2004]

A. Wagner, Reconstructing pathways in large genetic networks from genetic perturbations, Journal of Computational Biology, Vol. 11, No.1, pp. 53-60, 2004.

[Uehara and Uno, 2004]

R. Uehara and Y. Uno, Efficient algorithms for the longest path problem, Lecture Notes in Computer Science, ISSN 0302-9743, Vol. 3341, Springer-Verlag, pp. 871-883, 2004.

[Ioannidou et al., 2009]

K. Ioannidou, G. Mertzios and S. Nikolopoulos, The Longest Path Problem Is Polynomial on Interval Graphs, In Proceedings of the 34th International Symposium on Mathematical Foundations of Computer Science (MFCS’09), SpringerVerlag, ISBN 978-3-642-03815-0, pp. 403-414, Novy Smokovec, High Tatras, Slovakia, 2009.

[Hsu et al, 1998]

1Y. Hsu, S. Sun and D. Du, Finding The Longest Simple Path in Cyclic Combinational Circuits, IEEE International Conference on Computer Design (ICCD’98), IEEE Computer Society, ISBN 0-8186-9099-2, pp.530, Austin, Texas, U.S.A., 1998.

[Wong et al., 2005]

W. Wong, T. Lau and I. King, Information retrieval in P2P networks using genetic algorithm. In Proceedings of the 14th International World Wide Web Conference, Special interest tracks and posters, pp. 922-923, Chiba, Japan, May 10-14, 2005.

[Prager and Spears, 2009] S. Prager, and W. Spears, A hybrid evolutionary-graph approach for finding functional network paths, In Proceedings of the 17th ACM GIS International Conference on Advances in Geographic Information Systems (ACM-GIS 2009), ACM, ISBN 978-1-60558-649-6, pp. 306-315, Seattle, Washington, U.S.A., November 4-6, 2009.

[Nair and Skooda, 2009] T. Nair, K. Sooda, Comparison of Genetic Algorithm and Simulated Annealing Technique for Optimal Path Selection in Network Routing, In Proceedings of the National Conference on VLSI and Networks (NCVN-09), pp. 47-53, Chennai, Tamil Nadu, India, 2009.

[Gelenbe et al., 2006] E. Gelenbe, P. Liu and J. Lain´e, Genetic algorithms for route discovery, IEEE Transaction on Systems, Man and Cybernetics (SMC 2006), Vol. 36, No. 6, pp. 1247-1254, Taipei, Taiwan, October 8-11, 2006.

[Kumar et al., 2009]

A. Kumar, J. Arunadevi and V. Mohan, Intelligent Transport Route Planning Using Genetic Algorithms in Path Computation Algorithms, European Journal of Scientific Research, EuroJournals Publishing, ISSN 1450-216X, Vol. 25, No. 3, pp. 463-468, 2009.

[Solano and Jones, 1993] J. Solano and D. Jones, Generation of collision-free paths, a genetic approach, In Proceedings of the IEEE Colloquium on Genetic Algorithms for Control and Systems Engineering, pp. 5/1-5/6, London, 1993.

[Davies and Jnifene, 2008] T. Davies and A. Jnifene, Path Planning and Trajectory Control of Collaborative Mobile Robots Using Hybrid Control Architecture, Journal of Systemics, Cybernetics and Informatics (JSCI), Vol. 6, No. 4, pp. 42-48, 2008.

[Talbi and Bessi\`ere, 2004]

E. Talbi and P. Bessi\`ere, A Parallel Genetic Algorithm for the Graph Partitioning Problem, In Proceedings of the 5th ACM International Conference on Supercomputing (ICS91), ISBN 0-89791-434, pp. 312-320, Cologne, Germany, 1991.