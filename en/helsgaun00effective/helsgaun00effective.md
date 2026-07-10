# An Effective Implementation of the Lin-Kernighan Traveling Salesman Heuristic

Keld HelsgaunE-mail: keld@ruc.dk

Department of Computer Science Roskilde University DK-4000 Roskilde, Denmark

# Abstract

This report describes an implementation of the Lin-Kernighan heuristic, one of the most successful methods for generating optimal or nearoptimal solutions for the symmetric traveling salesman problem. Computational tests show that the implementation is highly effective. It has found optimal solutions for all solved problem instances we have been able to obtain, including a 7397-city problem (the largest nontrivial problem instance solved to optimality today). Furthermore, the algorithm has improved the best known solutions for a series of large-scale problems with unknown optima, among these an 85900-city problem.

# 1. Introduction

The Lin-Kernighan heuristic [1] is generally considered to be one of the most effective methods for generating optimal or near-optimal solutions for the symmetric traveling salesman problem. However, the design and implementation of an algorithm based on this heuristic is not trivial. There are many design and implementation decisions to be made, and most decisions have a great influence on performance.

This report describes the implementation of a new modified version of the Lin-Kernighan algorithm. Computational experiments have shown that the implementation is highly effective.

The new algorithm differs in many details from the original one. The most notable difference is found in the search strategy. The new algorithm uses larger (and more complex) search steps than the original one. Also new is the use of sensitivity analysis to direct and restrict the search.

Run times of both algorithms increase approximately as $\mathtt { n } ^ { 2 . 2 }$ . However, the new algorithm is much more effective. The new algorithm makes it possible to find optimal solutions to large-scale problems, in reasonable running times.

For a typical 100-city problem the optimal solution is found in less than a second, and for a typical 1000-city problem optimum is found in less than a minute (on a 300 MHz G3 Power Macintosh).

Even though the algorithm is approximate, optimal solutions are produced with an impressively high frequency. It has produced optimal solutions for all solved problems we have been able to obtain, including a 7397-city problem (at the time of writing, the largest nontrivial problem solved to optimality).

The rest of this report is organized as follows. Section 2 defines the traveling salesman problem and gives an overview of solution algorithms. Section 3 describes the original algorithm of Lin and Kernighan (including their own refinements of the algorithm). Sections 4 and 5 present the new modified algorithm and its implementation. The effectiveness of the implementation is reported in Section 6.

# 2. The traveling salesman problem

# 2.1 Formulation

A salesman is required to visit each of n given cities once and only once, starting from any city and returning to the original place of departure. What tour should he choose in order to minimize his total travel distance?

The distances between any pair of cities are assumed to be known by the salesman. Distance can be replaced by another notion, such as time or money. In the following the term ’cost’ is used to represent any such notion.

This problem, the traveling salesman problem (TSP), is one of the most widely studied problems in combinatorial optimization [2]. The problem is easy to state, but hard to solve. Mathematically, the problem may be stated as follows:

Given a ‘cost matrix’ $\mathrm { C } = \mathrm { ( c _ { i j } ) }$ , where $\mathrm { c _ { i j } }$ represents the cost of going from city i to city j, $( \mathrm { i } , \mathrm { j } = 1 , . . . , \tilde { \mathrm { n } } )$ , find a permutation $( \mathrm { i } _ { 1 } , \mathrm { i } _ { 2 } ^ { - } , \mathrm { i } _ { 3 } , . . . , \mathrm { i } _ { \mathrm { n } } ^ { - } )$ of the integers from 1 through n that minimizes the quantity

$$
\mathrm { c _ { i _ { 1 } i _ { 2 } } + c _ { i _ { 2 } i _ { 3 } } + \ldots + c _ { i _ { n } i _ { 1 } } }
$$

Properties of the cost matrix C are used to classify problems.

If ${ \bf c _ { \mathrm { i j } } } = { \bf c _ { \mathrm { j i } } }$ for all i and j, the problem is said to be symmetric; otherwise, it is asymmetric.   
If the triangle inequality holds $( \mathrm { c _ { i k } \leq c _ { i j } + c _ { j k } }$ for all i, j and $\mathrm { k }$ ), the problem is said to be metric. If $\mathrm { c _ { i j } }$ are Euclidean distances between points in the plane, the problem is said to be Euclidean. A Euclidean problem is, of course, both symmetric and metric.

# 2.2 Motivation

The importance of the TSP stems not from a massive need from salesmen wishing to minimize their travel distance. The importance comes from a wealth of other applications, many of which seemingly have nothing to do with traveling routes.

For example, consider the following process planning problem. A number of jobs have to be processed on a single machine. The machine can only process one job at a time. Before a job can be processed the machine must be prepared (cleaned, adjusted, or whatever). Given the processing time of each job and the switch-over time between each pair of jobs, the task is to find an execution sequence of the jobs making the total processing time as short as possible.

It is easy to see that this problem is an instance of TSP. Here cij represents the time to complete job j after job i (switch-over time plus time to perform job j). A pseudo job with processing time 0 marks the beginning and ending state for the machine.

Many real-world problems can be formulated as instances of the TSP. Its versatility is illustrated in the following examples of application areas:

• Computer wiring   
• Vehicle routing   
• Crystallography   
• Robot control   
• Drilling of printed circuit boards • Chronological sequencing.

TSP is a typical problem of its genre: combinatorial optimization. This means that theoretical and practical insight achieved in the study of TSP can often be useful in the solution of other problems in this area. In fact, much progress in combinatorial optimization can be traced back to research on TSP. The now well-known computing method, branch and bound, was first used in the context of TSP [3, 4]. It is also worth mentioning that research on TSP was an important driving force in the development of the computational complexity theory in the beginning of the 1970s [5].

However, the interest in TSP not only stems from its practical and theoretical importance. The intellectual challenge of solving the problem also plays a role. Despite its simple formulation, TSP is hard to solve. The difficulty becomes apparent when one considers the number of possible tours - an astronomical figure even for a relatively small number of cities. For a symmetric problem with n cities there are (n-1)!/2 possible tours. If n is 20, there are more than 1018 tours. The 7397-city problem, which is successfully solved by the algorithm described in this report, contains more than 1025,000 possible tours. In comparison it may be noted that the number of elementary particles in the universe has been estimated to be ‘only’ $1 0 ^ { 8 7 }$ .

# 2.3 Solution algorithms

It has been proven that TSP is a member of the set of NP-complete problems. This is a class of difficult problems whose time complexity is probably exponential. The members of the class are related so that if a polynomial time were found for one problem, polynomial time algorithms would exist for all of them. However, it is commonly believed that no such polynomial algorithm exists. Therefore, any attempt to construct a general algorithm for finding optimal solutions for the TSP in polynomial time must (probably) fail.

That is, for any such algorithm it is possible to construct problem instances for which the execution time grows at least exponentially with the size of the input. Note, however, that time complexity here refers to any algorithm’s behavior in worst cases. It can not be excluded that there exist algorithms whose average running time is polynomial. The existence of such algorithms is still an open question.

Algorithms for solving the TSP may be divided into two classes:

• Exact algorithms;   
• Approximate (or heuristic) algorithms.

# 2.3.1 Exact algorithms

The exact algorithms are guaranteed to find the optimal solution in a bounded number of steps. Today one can find exact solutions to symmetric problems with a few hundred cities, although there have been reports on the solution of problems with thousands of cities.

The most effective exact algorithms are cutting-plane or facet-finding algorithms [6, 7, 8]. These algorithms are quite complex, with codes on the order of 10,000 lines. In addition, the algorithms are very demanding of computer power. For example, the exact solution of a symmetric problem with 2392 cities was determined over a period of more than 27 hours on a powerful super computer [7]. It took roughly 3-4 years of CPU time on a large network of computers to determine the exact solution of the previously mentioned 7397-city problem [8].

Symmetric problems are usually more difficult to solve than asymmetric problems [9]. Today the 7397-city problem is the largest (nontrivial) symmetric problem that has been solved. In comparison, the optimal solution of a 500,000-city asymmetric problem has been reported [10].

# 2.3.2 Approximate algorithms

In contrast, the approximate algorithms obtain good solutions but do not guarantee that optimal solutions will be found. These algorithms are usually very simple and have (relative) short running times. Some of the algorithms give solutions that in average differs only by a few percent from the optimal solution. Therefore, if a small deviation from optimum can be accepted, it may be appropriate to use an approximate algorithm.

The class of approximate algorithms may be subdivided into the following three classes:

• Tour construction algorithms • Tour improvement algorithms • Composite algorithms.

The tour construction algorithms gradually build a tour by adding a new city at each step. The tour improvement algorithms improve upon a tour by performing various exchanges. The composite algorithms combine these two features.

A simple example of a tour construction algorithm is the so-called nearestneighbor algorithm [11]: Start in an arbitrary city. As long as there are cities, that have not yet been visited, visit the nearest city that still has not appeared in the tour. Finally, return to the first city.

This approach is simple, but often too greedy. The first distances in the construction process are reasonable short, whereas the distances at the end of the process usually will be rather long. A lot of other construction algorithms have been developed to remedy this problem (see for example [2], [12] and [13]).

The tour improvement algorithms, however, have achieved the greatest success. A simple example of this type of algorithm is the so-called 2-opt algorithm: Start with a given tour. Replace 2 links of the tour with 2 other links in such a way that the new tour length is shorter. Continue in this way until no more improvements are possible.

Figure 2.1 illustrates a 2-opt exchange of links, a so-called 2-opt move. Note that a 2-opt move keeps the tour feasible and corresponds to a reversal of a subsequence of the cities.

![](images/0b42ed563a2781cb308d9f10bb8e8aa120df02b23255dc1c34d46550ce23ac49.jpg)  
Figure 2.1 A 2-opt move

A generalization of this simple principle forms the basis for one the most effective approximate algorithms for solving the symmetric TSP, the Lin-Kernighan algorithm [1]. The original algorithm, as implemented by Lin and Kernighan in 1971, had an average running time of order $\mathtt { n } ^ { 2 . 2 }$ and was able to find the optimal solutions for most problems with fewer than 100 cities.

However, the Lin-Kernighan algorithm is not simple to implement. In a survey paper from 1989 [14] the authors wrote that no other implementation of the algorithm at that time had shown as good efficiency as was obtained by Lin and Kernighan.

# 3. The Lin-Kernighan algorithm

# 3.1 The basic algorithm

The 2-opt algorithm is a special case of the $\gimel$ -opt algorithm [15], where in each step $\lambda$ links of the current tour are replaced by $\lambda$ links in such a way that a shorter tour is achieved. In other words, in each step a shorter tour is obtained by deleting $\lambda$ links and putting the resulting paths together in a new way, possibly reversing one ore more of them.

The $\lambda$ -opt algorithm is based on the concept $\gimel$ -optimality:

A tour is said to be $\lambda$ -optimal (or simply $\lambda$ -opt) if it is impossible to obtain a shorter tour by replacing any $\lambda$ of its links by any other set of links.

From this definition it is obvious that any $\lambda$ -optimal tour is also $\aleph ^ { \prime }$ -optimal for $1 \leq \lambda ^ { \prime } \leq \lambda$ . It is also easy to see that a tour containing n cities is optimal if and only if it is n-optimal.

In general, the larger the value of $\lambda$ , the more likely it is that the final tour is optimal. For fairly large $\lambda$ it appears, at least intuitively, that a $\lambda$ -optimal tour should be optimal.

Unfortunately, the number of operations to test all $\lambda$ -exchanges increases rapidly as the number of cities increases. In a naive implementation the testing of a $\bar { \lambda }$ -exchange has a time complexity of $\mathrm { O } ( \mathrm { n } ^ { \lambda } )$ . Furthermore, there is no nontrivial upper bound of the number of $\lambda$ –exchanges. As a result, the values $\lambda = 2$ and $\lambda \overset { \cdot } { = } 3$ are the most commonly used. In one study the values $\lambda = 4$ and $\lambda = 5$ were used [16].

However, it is a drawback that $\lambda$ must be specified in advance. It is difficult to know what $\lambda$ to use to achieve the best compromise between running time and quality of solution.

Lin and Kernighan removed this drawback by introducing a powerful variable $\lambda$ -opt algorithm. The algorithm changes the value of $\lambda$ during its execution, deciding at each iteration what the value of $\lambda$ should be. At each iteration step the algorithm examines, for ascending values of $\lambda$ , whether an interchange of $\lambda$ links may result in a shorter tour. Given that the exchange of r links is being considered, a series of tests is performed to determine whether $\mathrm { r } { + } 1$ link exchanges should be considered. This continues until some stopping conditions are satisfied.

At each step the algorithm considers a growing set of potential exchanges (starting with $\mathrm { r } = 2$ ). These exchanges are chosen in such a way that a feasible tour may be formed at any stage of the process. If the exploration succeeds in finding a new shorter tour, then the actual tour is replaced with the new tour.

The Lin-Kernighan algorithm belongs to the class of so-called local optimization algorithms [17, 18]. The algorithm is specified in terms of exchanges (or moves) that can convert one tour into another. Given a feasible tour, the algorithm repeatedly performs exchanges that reduce the length of the current tour, until a tour is reached for which no exchange yields an improvement. This process may be repeated many times from initial tours generated in some randomized way. The algorithm is described below in more detail.

Let T be the current tour. At each iteration step the algorithm attempts to find two sets of links, $\mathrm { X } = \{ \mathrm { x } _ { 1 } , . . . , \mathrm { x } _ { \mathrm { r } } \}$ and $\mathrm { Y } = \mathrm { \hat { \{ y } _ { 1 } , ~ . . . , ~ y _ { r } \} }$ , such that, if the links of $\mathrm { X }$ are deleted from $\mathrm { T }$ and replaced by the links of Y, the result is a better tour. This interchange of links is called a $r$ -opt move. Figure 3.1 illustrates a 3-opt move.

![](images/9f702e86b2ad1ff2a19a82522f54e5f223b00edba3ee2ac893a3cab74963f648.jpg)  
Figure 3.1 A 3-opt move

The two sets $\mathrm { X }$ and $\mathrm { Y }$ are constructed element by element. Initially $\mathrm { X }$ and Y are empty. In step i a pair of links, $\mathbf { X } _ { \mathrm { i } }$ and ${ \mathrm { y } } _ { \mathrm { i } } ,$ are added to $\mathrm { X }$ and $\dot { \mathrm { ~ Y ~ } }$ , respectively.

In order to achieve a sufficient efficient algorithm, only links that fulfill the following criteria may enter X and Y.

# (1) The sequential exchange criterion

$\mathbf { X _ { i } }$ and $\mathrm { y _ { i } }$ must share an endpoint, and so must $\mathrm { y _ { i } }$ and $\mathbf { X } _ { \mathrm { i } + 1 }$ . $\mathrm { I f t } _ { 1 }$ denotes one of the two endpoints of $\mathbf { X } _ { 1 }$ , we have in general: $\mathbf { x } _ { \mathrm { i } } = ( \mathbf { t } _ { 2 \mathrm { i } - 1 } , \mathbf { t } _ { 2 \mathrm { i } } )$ , $\mathsf { y } _ { \mathrm { i } } = \left( \mathrm { t } _ { 2 \mathrm { i } } , \mathrm { t } _ { 2 \mathrm { i } + 1 } \right)$ and $\mathbf { \Delta x _ { i + 1 } } = ( \mathrm { t } _ { 2 \mathrm { i + 1 } } , \mathrm { t } _ { 2 \mathrm { i + 2 } } )$ for $\mathrm { i } \geq 1$ . See Figure 3.2.

![](images/12391ac05fa584189cd1541db688bc805e2e152c0d71278d69cbc154dded63d4.jpg)  
Figure 3.2. Restricting the choice of $\dot { \boldsymbol { x } } _ { i }$ yi, $x _ { i + l } ,$ and $y _ { i + l } .$

As seen, the sequence $( \mathrm { x } _ { 1 } , \mathrm { y } _ { 1 } , \mathrm { x } _ { 2 } , \mathrm { y } _ { 2 } , \mathrm { x } _ { 3 } , . . . , \mathrm { x } _ { \mathrm { r } } , \mathrm { y }$ constitutes a chain of adjoining links.

A necessary (but not sufficient) condition that the exchange of links X with links Y results in a tour is that the chain is closed, i.e., $\mathbf { y } _ { \mathrm { r } } \equiv ( \mathbf { t } _ { 2 \mathrm { r } } , \mathbf { t } _ { 1 } )$ . Such an exchange is called sequential.

Generally, an improvement of a tour may be achieved as a sequential exchange by a suitable numbering of the affected links. However, this is not always the case. Figure 3.3 shows an example where a sequential exchange is not possible.

![](images/0cf74dbfe5ffb106ed3a963c847c6d07c1fc1175fd24667c3b4de48afb695e76.jpg)  
Figure 3.3 Nonsequential exchange $( r = 4 )$ .

# (2) The feasibility criterion

It is required that $\mathbf { \boldsymbol { x } } _ { \mathrm { i } } = ( \mathbf { \boldsymbol { t } } _ { 2 \mathrm { i } - 1 } , \mathbf { \boldsymbol { t } } _ { 2 \mathrm { i } } )$ is chosen so that, if $\mathrm { t } _ { 2 \mathrm { i } }$ is joined to $\mathfrak { t } _ { 1 }$ , the resulting configuration is a tour. This feasibility criterion is used for $\mathrm { i } \geq 3$ and guarantees that it is possible to close up to a tour. This criterion was included in the algorithm both to reduce running time and to simplify the coding.

# (3) The positive gain criterion

It is required that $\mathrm { y _ { i } }$ is always chosen so that the gain, $\mathrm { G _ { i } } ,$ from the proposed set of exchanges is positive. Suppose $\mathbf { g } _ { \mathrm { i } } = \mathbf { c } ( \mathbf { x } _ { \mathrm { i } } ) - \mathbf { c } ( \mathbf { y } _ { \mathrm { i } } )$ is the gain from exchanging $\mathbf { X _ { i } }$ with yi. Then $\mathrm { G _ { i } }$ is the sum $\mathbf { g } _ { 1 } + \mathbf { g } _ { 2 } + \ldots + \mathbf { g } _ { \mathrm { i } }$ .

This stop criterion plays a great role in the efficiency of the algorithm. The demand that every partial sum, $\mathrm { G } _ { \mathrm { i } } ,$ must be positive seems immediately to be too restrictive. That this, however, is not the case, follows from the following simple fact: If a sequence of numbers has a positive sum, there is a cyclic permutation of these numbers such that every partial sum is positive. The proof is simple and can be found in [1].

# (4) The disjunctivity criterion

Finally, it is required that the sets X and Y are disjoint. This simplifies coding, reduces running time and gives an effective stop criterion.

Below is given an outline of the basic algorithm (a simplified version of the original algorithm).

1. Generate a random initial tour T. 2. Let $\dot { 1 } = 1$ . Choose $\mathfrak { t } _ { 1 }$ . 3. Choose $\mathbf { x } _ { 1 } = ( \mathbf { t } _ { 1 } , \mathbf { t } _ { 2 } )$ T. 4. Choose ${ \bf y } _ { 1 } = ( { \bf t } _ { 2 } , { \bf t } _ { 3 } )$ T such that $\mathrm { G } _ { 1 } > 0$ . If this is not possible, go to Step 12. 5. Let $\mathrm { i } = \mathrm { i } + 1$ . 6. Choose $\mathbf { x } _ { \mathrm { i } } = ( \mathbf { t } _ { 2 \mathrm { i } - 1 } , \mathbf { t } _ { 2 \mathrm { i } } )$ T such that (a) if $\mathfrak { t } _ { \mathrm { i } }$ is joined to $\mathfrak { t } _ { 1 }$ , the resulting configuration is a tour, $\mathrm { T } ^ { \varsigma }$ , and (b) $\mathbf { \boldsymbol { x } } _ { \mathrm { { i } } } \neq \mathbf { \boldsymbol { y } } _ { \mathrm { { s } } }$ for all $\mathrm { s } < \mathrm { i }$ . If $\mathrm { T } ^ { \varsigma }$ is a better tour than $\mathrm { T }$ , let $\mathrm { T } = \mathrm { T } ^ { \mathrm { } }$ and go to Step 2. 7. Choose ${ \bf y } _ { \mathrm { i } } = ( \mathbf { t } _ { 2 \mathrm { i } } , \mathbf { t } _ { 2 \mathrm { i } + 1 } )$ T such that (a) $\mathrm { G } _ { \mathrm { i } } > 0$ , (b) $\mathrm { y } _ { \mathrm { i } } \neq \mathrm { x } _ { \mathrm { s } }$ for all $\mathrm { { s } } \leq \mathrm { { i } }$ , and (c) $\mathbf { X } _ { \mathrm { i + 1 } }$ exists. If such $\mathrm { y _ { i } }$ exists, go to Step 5. 8. If there is an untried alternative for ${ \mathrm { y } } _ { 2 }$ , let $\mathrm { i } = 2$ and go to Step 7. 9. If there is an untried alternative for $\mathbf { X } _ { 2 }$ , let $\mathrm { i } = 2$ and go to Step 6. 10. If there is an untried alternative for ${ \bf y } _ { 1 }$ , let $\dot { 1 } = 1$ and go to Step 4. 11. If there is an untried alternative for $\mathbf { X } _ { 1 }$ , let $\dot { 1 } = 1$ and go to Step 3. 12. If there is an untried alternative for $\mathfrak { t } _ { 1 }$ , then go to Step 2. 13. Stop (or go to Step 1).

Comments on the algorithm:

Step 1. A random tour is chosen as the starting point for the explorations.

Step 3. Choose a link $\mathbf { x } _ { 1 } = ( \mathbf { t } _ { 1 } , \mathbf { t } _ { 2 } )$ on the tour. When $\mathfrak { t } _ { 1 }$ has been chosen, there are two choices for $\mathbf { X } _ { 1 }$ . Here the verb ‘choose’ means ‘select an untried alternative’. However, each time an improvement of the tour has been found (in Step 6), all alternatives are considered untried.

Step 6. There are two choices of $\mathbf { X _ { i } }$ . However, for given $\mathrm { y } _ { \mathrm { i - 1 } }$ $( \mathrm { i } \geq 2 )$ only one of these makes it possible to ‘close’ the tour (by the addition of yi). The other choice results in two disconnected subtours. In only one case, however, such an unfeasible choice is allowed, namely for $\dot { 1 } = \dot { 2 }$ . Figure 3.5 shows this situation.

![](images/924c802f93f6f73885c15ccec4575610ccde933fa0af228a7c65744b4d86d5e4.jpg)  
Figure 3.5 No close up at $x _ { 2 }$

If $\mathrm { y } _ { 2 }$ is chosen so that $\mathrm { t } _ { 5 }$ lies between $\mathbf { t } _ { 2 }$ and $\mathrm { t } _ { 3 }$ , then the tour can be closed in the next step. But then $\mathrm { t } _ { 6 }$ may be on either side of $\mathrm { t } _ { 5 }$ (see Figure 3.6); the original algorithm investigated both alternatives.

![](images/7159483601b697ac0b70204834f7e78f67c21fe466223fbb4d635a3b3a6ec595.jpg)  
Figure 3.6 Two choices for $x _ { 3 }$

On the other hand, if ${ \tt y } _ { 2 }$ is chosen so that $\mathrm { t } _ { 5 }$ lies between $\mathrm { t } _ { 4 }$ and $\mathrm { t } _ { 1 }$ , there is only one choice for $\mathrm { t } _ { 6 }$ (it must lie between $\mathrm { t } _ { 4 }$ and $\mathrm { t } _ { 5 }$ ), and $\mathrm { t } _ { 7 }$ must lie between $\mathfrak { t } _ { 2 }$ and $\mathrm { t } _ { 3 }$ . But then $\mathfrak { t } _ { 8 }$ can be on either side of $\mathrm { t } _ { 7 }$ (see Figure 3.7); the original algorithm investigated the alternative for which $\mathbf { c ( t _ { 7 } , t _ { 8 } ) }$ is maximum.

![](images/b0fda5bdd54e5164beebda7e18a8c66e3aba5c0ecc5fe86a9de11470ee7848c3.jpg)  
Figure 3.7 Unique choice for $x _ { 3 }$ . Limited choice of y3. Two choices for $x _ { 4 } .$

Condition (b) in Step 6 and Step 7 ensures that the sets $\mathrm { X }$ and $\mathrm { Y }$ are disjoint: $\mathrm { y _ { i } }$ must not be a previously broken link, and $\mathbf { X _ { i } }$ must not be a link previously added.

Steps 8-12. These steps cause backtracking. Note that backtracking is allowed only if no improvement has been found, and only at levels 1 and 2.

Step 13. The algorithm terminates with a solution tour when all values of $\mathfrak { t } _ { 1 }$ have been examined without improvement. If required, a new random initial tour may be considered at Step 1.

The algorithm described above differs from the original one by its reaction on tour improvements. In the algorithm given above, a tour T is replaced by a shorter tour $\mathrm { T } ^ { \varsigma }$ as soon as an improvement is found (in Step 6). In contrast, the original algorithm continues its steps by adding potential exchanges in order to find an even shorter tour. When no more exchanges are possible, or when $\mathrm { G } _ { \mathrm { i } } \leq \mathrm { G } ^ { * }$ , where $\mathrm { G ^ { * } }$ is the best improvement of T recorded so far, the search stops and the current tour T is replaced by the most advantageous tour. In their paper [1] Lin and Kernighan did not state their reasons for introducing this method. It complicates the coding and results neither in better solutions nor in shorter running times.

# 3.2 Lin and Kernighan’s refinements

A bottleneck of the algorithm is the search for links to enter the sets X and Y. In order to increase efficiency, special care therefore should be taken to limit this search. Only exchanges that have a reasonable chance of leading to a reduction of tour length should be considered.

The basic algorithm as presented in the preceding section limits its search by using the following four rules:

(1) Only sequential exchanges are allowed.   
(2) The provisional gain must be positive.   
(3) The tour can be ‘closed’ (with one exception, $\mathrm { i } = 2$ ).   
(4) A previously broken link must not be added, and a previously added link must not be broken.

To limit the search even more Lin and Kernighan refined the algorithm by introducing the following rules:

(5) The search for a link to enter the tour, $\mathrm { y } _ { \mathrm { i } } = ( \mathrm { t } _ { 2 \mathrm { i } } , \mathrm { t } _ { 2 \mathrm { i } + 1 } )$ , is limited to the five nearest neighbors to $\mathbf { t } _ { 2 \mathrm { i } }$ .   
(6) For $\mathrm { i } \geq 4$ , no link, $\mathbf { X } _ { \mathrm { i } } ,$ on the tour must be broken if it is a common link of a small number (2-5) of solution tours.   
(7) The search for improvements is stopped if the current tour is the same as a previous solution tour.

Rules 5 and 6 are heuristic rules. They are based on expectations of which links are likely to belong to an optimal tour. They save running time, but sometimes at the expense of not achieving the best possible solutions.

Rule 7 also saves running time, but has no influence on the quality of solutions being found. If a tour is the same as a previous solution tour, there is no point in attempting to improve it further. The time needed to check that no more improvements are possible (the checkout time) may therefore be saved. According to Lin and Kernighan the time saved in this way it typically 30 to 50 percent of running time.

In addition to these refinements, whose purpose is primarily to limit the search, Lin and Kernighan added some refinements whose purpose is primarily to direct the search. Where the algorithm has a choice of alternatives, heuristic rules are used to give priorities to these alternatives. In cases where only one of the alternatives must be chosen, the one with the highest priority is chosen. In cases where several alternatives must be tried, the alternatives are tried in descending priority order (using backtracking). To be more specific, the following rules are used:

(8) When link $\mathrm { y } _ { \mathrm { i } }$ $( \mathrm { i } \geq 2 )$ is to be chosen, each possible choice is given the priority ${ \mathsf { c } } ( { \mathsf { x } } _ { 1 + 1 } ) - { \mathsf { c } } ( { \mathsf { y } } _ { \mathrm { i } } )$ .   
(9) If there are two alternatives for $\mathbf { X } _ { 4 }$ , the one where $\mathsf { c } ( \mathbf { x } _ { 4 } )$ is highest is chosen.

Rule 8 is a heuristic rule for ranking the links to be added to Y. The priority for $\mathrm { y _ { i } }$ is the length of the next (unique) link to be broken, $\mathbf { X } _ { \mathrm { i ^ { + } l } }$ , if ${ \mathrm { y } } _ { \mathrm { i } }$ is included in the tour, minus the length of $\mathrm { y _ { i } }$ . In this way, the algorithm is provided with some look-ahead. By maximizing the quantity ${ \mathfrak { c } } ( { \mathfrak { x } } _ { \mathrm { i + 1 } } ) - { \mathfrak { c } } ( { \mathfrak { y } } _ { \mathrm { i } } ) .$ , the algorithm aims at breaking a long link and including a short link.

Rule 9 deals with the special situation in Figure 3.7 where there are two choices for $\mathbf { X } _ { 4 }$ . The rule gives preference to the longest link in this case. In three other cases, namely for $\mathbf { X } _ { 1 }$ , $\mathbf { X } _ { 2 } .$ , and sometimes $\mathbf { X } _ { 3 }$ (see Figure 3.6) there are two alternatives available. In these situations the algorithm examines both choices using backtracking (unless an improved tour was found). In their paper Lin and Kernighan do not specify the sequence in which the alternatives are examined.

As a last refinement, Lin and Kernighan included a limited defense against the situations where only nonsequential exchanges may lead to a better solution. After a local optimum has been found, the algorithm tests, among the links allowed to be broken, whether it is possible to make a further improvement by a nonsequential 4-opt change (as shown in Figure 3.3). Lin and Kernighan pointed out that the effect of this post optimization procedure varies substantially from problem to problem. However, the time used for the test is small relative to the total running time, so it is a cheap insurance.

# 4. The modified Lin-Kernighan algorithm

Lin and Kernighan’s original algorithm was reasonably effective. For problems with up to 50 cities, the probability of obtaining optimal solutions in a single trial was close to 100 percent. For problems with 100 cities the probability dropped to between 20 and 30 percent. However, by running a few trials, each time starting with a new random tour, the optimum for these problems could be found with nearly 100 percent assurance.

The algorithm was evaluated on a spectrum of problems, among these a drilling problem with 318 points. Due to computer-storage limitations, the problem was split into three smaller problems. A solution tour was obtained by solving the subproblems separately, and finally joining the three tours. At the time when Lin and Kernighan wrote their paper (1971), the optimum for this problem was unknown. Now that the optimum is known, it may be noted that their solution was 1.3 percent above optimum.

In the following, a modified and extended version of their algorithm is presented. The new algorithm is a considerable improvement of the original algorithm. For example, for the mentioned 318-city problem the optimal solution is now found in a few trials (approximately 2), and in a very short time (about one second on a 300 MHz G3 Power Macintosh). In general, the quality of solutions achieved by the algorithm is very impressive. The algorithm has been able to find optimal solutions for all problem instances we have been able to obtain, including a 7397-city problem (the largest nontrivial problem instance solved to optimality today).

The increase in efficiency is primarily achieved by a revision of Lin and Kernighan’s heuristic rules for restricting and directing the search. Even if their heuristic rules seem natural, a critical analysis shows that they suffer from considerable defects.

# 4.1 Candidate sets

A central rule in the original algorithm is the heuristic rule that restricts the inclusion of links in the tour to the five nearest neighbors to a given city (Rule 5 in Section 3.2). This rule directs the search against short tours and reduces the search effort substantially. However, there is a certain risk that the application of this rule may prevent the optimal solution from being found. If an optimal solution contains one link, which is not connected to the five nearest neighbors of its two end cities, then the algorithm will have difficulties in obtaining the optimum.

The inadequacy of this rule manifests itself particularly clearly in large problems. For example, for a 532-city problem [19] one of the links in the optimal solution is the 22nd nearest neighbor city for one of its end points. So in order to find the optimal solution to this problem, the number of nearest neighbors to be considered ought to be at least 22. Unfortunately, this enlargement of the set of candidates results in a substantial increase in running time.

The rule builds on the assumption that the shorter a link is, the greater is the probability that it belongs to an optimal tour. This seems reasonable, but used too restrictively it may result in poor tours.

In the following, a measure of nearness is described that better reflects the chances of a given link being a member of an optimal tour. This measure, called $\alpha$ -nearness, is based on sensitivity analysis using minimum spanning trees.

First, some well-known graph theoretical terminology is reviewed.

Let $\mathrm { G } = ( \mathrm { N } , \mathrm { E } )$ be a undirected weighted graph where $\mathrm { N } = \{ 1 , 2 , . . . , \mathrm { n } \}$ is the set of nodes and $\mathrm { E = \{ ( i , j ) | \ i \mathrm { ~  ~ { ~ \cal ~ N ~ } , j ~ } ~ \Delta ~ N \} }$ is the set of edges. Each edge (i,j) has associated a weight c(i,j).

A path is a set of edges $\{ ( \mathrm { i } _ { 1 } , \mathrm { i } _ { 2 } ) , ( \mathrm { i } _ { 2 } , \mathrm { i } _ { 3 } ) , . . . , ( \mathrm { i } _ { \mathrm { k } - 1 } , \mathrm { i } _ { \mathrm { k } } ) \}$ with $\mathrm { i } _ { \mathrm { p } } \ne \mathrm { i } _ { \mathrm { q } }$ for all ${ \mathfrak { p } } \neq { \mathfrak { q } }$

A cycle is a set of edges $\{ ( \mathrm { i } _ { 1 } , \mathrm { i } _ { 2 } ) , ( \mathrm { i } _ { 2 } , \mathrm { i } _ { 3 } ) , . . . , ( \mathrm { i } _ { \mathrm { k } } , \mathrm { i } _ { 1 } ) \}$ with $\mathrm { i } _ { \mathrm { p } } \ne \mathrm { i } _ { \mathrm { q } }$ for ${ \mathfrak { p } } \neq { \mathfrak { q } }$

A tour is a cycle where ${ \boldsymbol { \mathrm { k } } } = { \boldsymbol { \mathrm { n } } }$ .

For any subset S E the length of S, L(S), is given by $\begin{array} { r } { \mathrm { L } ( \mathrm { S } ) = \sum _ { \mathrm { ( i , j ) } } \mathrm { ~ s ~ } \mathsf { c } ( \mathrm { i , j } ) } \end{array}$

An optimal tour is a tour of minimum length. Thus, the symmetric TSP can simply be formulated as: “Given a weighted graph G, determine an optimal tour of $\mathbf { G } ^ { \mathfrak { s } }$ .

A graph G is said to be connected if it contains for any pair of nodes a path connecting them.

A tree is a connected graph without cycles. A spanning tree of a graph G with n nodes is a tree with n-1 edges from G. A minimum spanning tree is a spanning tree of minimum length.

Now the important concept of a $I$ -tree may be defined.

A 1-tree for a graph $\mathrm { G } = ( \mathrm { N } , \mathrm { E } )$ is a spanning tree on the node set $\mathrm { N } \backslash \{ 1 \}$ combined with two edges from E incident to node 1.

The choice of node 1 as a special node is arbitrary. Note that a 1-tree is not a tree since it contains a cycle (containing node 1; see Figure 4.1).

![](images/855572c2e43746e952799f5fd5f27d77e3591a47afc5bebf7a3556e597dad2cc.jpg)  
Figure 4.1 A 1-tree.

A minimum $I$ -tree is a 1-tree of minimum length.

The degree of a node is the number of edges incident to the node.

It is easy to see [20, 21] that

(1) an optimal tour is a minimum 1-tree where every node has degree 2;

(2) if a minimum 1-tree is a tour, then the tour is optimal.

Thus, an alternative formulation of the symmetric TSP is: “Find a minimum 1-tree all whose nodes have degree $2 ^ { \circ }$ .

Usually a minimum spanning tree contains many edges in common with an optimal tour. An optimal tour normally contains between 70 and 80 percent of the edges of a minimum 1-tree. Therefore, minimum 1-trees seem to be well suited as a heuristic measure of ‘nearness’. Edges that belong, or ‘nearly belong', to a minimum 1-tree, stand a good chance of also belonging to an optimal tour. Conversely, edges that are ‘far from’ belonging to a minimum 1- tree have a low probability of also belonging to an optimal tour. In the LinKernighan algorithm these ‘far’ edges may be excluded as candidates to enter a tour. It is expected that this exclusion does not cause the optimal tour to be missed.

More formally, this measure of nearness is defined as follows:

<table><tr><td>Let T be a minimum 1-tree of length L(T) and let T+(i,j) denote a minimum 1-tree required to contain the edge (i,j). Then the αnearness of an edge (i,j) is defined as the quantity</td></tr><tr><td>α(i,j) = L(T+(i,j)) - L(T).</td></tr></table>

That is, given the length of (any) minimum 1-tree, the $\mathfrak { a }$ −nearness of an edge is the increase of length when a minimum 1-tree is required to contain this edge.

It is easy to verify the following two simple properties of :

(1) ${ \mathfrak { a } } ( { \mathrm { i } } , { \mathrm { j } } ) \geq 0 .$ (2) If (i,j) belongs to some minimum 1-tree, then $\mathfrak { a } ( \mathrm { i } , \mathrm { j } ) = 0$ .

The $\mathtt { a }$ -measure can be used to systematically identify those edges that could conceivably be included in an optimal tour, and disregard the remainder. These 'promising edges', called the candidate set, may, for example, consist of the k -nearest edges incident to each node, and/or those edges having an $\mathtt { a }$ -nearness below a specified upper bound.

In general, using the -measure for specifying the candidate set is much better than using nearest neighbors. Usually, the candidate set may be smaller, without degradation of the solution quality.

The use of -nearness in the construction of the candidate set implies computations of -values. The efficiency, both in time of space, of these computations is therefore important. The method is not of much practical value, if the computations are too expensive. In the following an algorithm is presented that computes all $\mathfrak { a }$ -values. The algorithm has time complexity $\dot { \mathrm { O } ( \mathrm { n } ^ { 2 } ) }$ and uses space O(n).

Let $\mathrm { G } = \left( \mathrm { N } , \mathrm { E } \right)$ be a complete graph, that is, a graph where for all nodes i and j in $_ \mathrm { N }$ there is an edge $( \mathrm { \bar { i } } , \mathrm { \bar { j } } )$ in E. The algorithm first finds a minimum 1-tree for G. This can be done by determination of a minimum spanning tree that contains the nodes $\{ 2 , 3 , . . . , \mathrm { n } \}$ , followed by the addition of the two shortest edges incident to node 1. The minimum spanning tree may, for example, be determined using Prim’s algorithm [22], which has a run time complexity of ${ \mathrm { O } } ( { \mathfrak { n } } ^ { 2 } )$ . The additional two edges may be determined in time O(n). Thus, the complexity of this first part is ${ \mathrm { O } } ( { \mathfrak { n } } ^ { 2 } )$ .

Next, the nearness $\mathfrak { a } ( \mathrm { i } , \mathrm { j } )$ is determined for all edges (i,j). Let T be a minimum 1-tree. From the definition of a minimum spanning tree, it is easy to see that a minimum spanning tree $\mathrm { T } ^ { + } ( \mathrm { i } , \mathrm { j } )$ containing the edge (i,j) may be determined from T using the following action rules:

(a) If (i,j) belongs to T, then $\mathrm { T } ^ { + } ( \mathrm { i } , \mathrm { j } )$ is equal to T.   
(b) Otherwise, if (i,j) has 1 as end node $( \mathrm { i } = 1 \quad \mathrm { j } = 1 )$ , then $\mathrm { T } ^ { + } ( \mathrm { i } , \mathrm { j } )$ is obtained from T by replacing the longest of the two edges of T incident to node 1 with (i,j).   
(c) Otherwise, insert (i,j) in T. This creates a cycle containing (i,j) in the spanning tree part of T. Then $\mathrm { T } ^ { + } ( \mathrm { i } , \mathrm { j } )$ is obtained by removing the longest of the other edges on this cycle.

Cases a and b are simple. With a suitable representation of 1-trees they can both be treated in constant time.

Case c is more difficult to treat efficiently. The number of edges in the produced cycles is O(n). Therefore, with a suitable representation it is possible to treat each edge with time complexity O(n). Since ${ \hat { \mathrm { O } } } ( { \mathrm { n } } ^ { 2 } )$ edges must be treated this way, the total time complexity becomes $\mathrm { O } ( \mathrm { n } ^ { 3 } )$ , which is unsatisfactory.

However, it is possible to obtain a total complexity of $\mathrm { O } ( \mathrm { n } ^ { 2 } )$ by exploiting a simple relation between the $\mathtt { a }$ -values [23, 24].

Let $\beta ( \mathrm { i } , \mathrm { j } )$ denote the length of the edge to be removed from the spanning tree when edge (i,j) is added. Thus $\mathfrak { a } ( \mathrm { i } , \mathrm { j } ) \doteq \mathfrak { c } ( \mathrm { i } , \mathrm { j } ) - \mathsf { \beta } ( \mathrm { i } , \mathrm { j } )$ . Then the following fact may be exploited (see Figure 4.2). If $( \mathrm { j } _ { 1 } , \mathrm { j } _ { 2 } )$ is an edge of the minimum spanning tree, i is one of the remaining nodes and ${ \bf j } _ { 1 }$ is on that cycle that arises by adding the edge $( \mathrm { i } , \mathrm { j } _ { 2 } )$ to the tree, then $\beta ( \mathrm { i } , \mathrm { j } _ { 2 } )$ may be computed as the maximum of $\beta ( \mathrm { i } , \mathrm { j } _ { 1 } )$ and $\mathsf { c } ( \mathrm { j } _ { 1 } , \mathrm { j } _ { 2 } )$ .

![](images/e05fb1767f297b05d21a86f3e69d3b1ba71644d131827404ccf9e5ca4441ad77.jpg)  
Figure $4 . 2 \beta ( i , j _ { 2 } )$ may be computed from $\beta ( i , j _ { l } )$ .

Thus, for a given node i all the values $\mathsf { \beta } ( \mathrm { i , j } ) , \mathrm { j } = 1 , 2 , . . . , \mathrm { n }$ , can be computed with a time complexity of O(n), if only the remaining nodes are traversed in a suitable sequence. It can be seen that such a sequence is produced as a byproduct of Prim’s algorithm for constructing minimum spanning trees, namely a topological order, in which every node's descendants in the tree are placed after the node. The total complexity now becomes ${ \mathrm { O } } ( { \mathfrak { n } } ^ { 2 } )$ .

Figure 4.3 sketches in C-style notation an algorithm for computing $\beta ( \mathrm { i } , \mathrm { j } )$ for $\mathrm { i } \neq 1 , \mathrm { j } \neq 1 , \mathrm { i } \neq \mathrm { j }$ . The algorithm assumes that the father of each node j in the tree, dad[j], precedes the node (i.e., $\mathrm { d a d [ j ] = i \hbar \hbar \Gamma _ { 1 } < j ) }$ .

![](images/c8fc3101c1224c8045c51e6c995d5af693479732b59edb154254fb1034850361.jpg)  
Figure 4.3 Computation of $\{ \beta ( i , j )$ for i 1, j 1, i j.

Unfortunately this algorithm needs space ${ \mathrm { O } } ( { \mathfrak { n } } ^ { 2 } )$ for storing $\beta$ -values. Some space may be saved by storing the $\mathrm { c } \mathrm { - }$ and $\beta$ -values in one quadratic matrix, so that, for example, the c-values are stored in the lower triangular matrix, while the $\beta .$ -values are stored in the upper triangular matrix. For large values of n, however, storage limitations may make this approach impractical.

Half of the space may be saved if the c-values are not stored, but computed when needed (for example as Euclidean distances). The question is whether it is also possible to save the space needed for the $\beta$ -values At first sight it would seem that the $\beta$ -values must be stored in order to achieve ${ \mathrm { O } } ( { \mathrm { n } } ^ { 2 } )$ time complexity for their computation. That this is not the case will now be demonstrated.

The algorithm, given in Figure 4.4, uses two one-dimensional auxiliary arrays, b and mark. Array b corresponds to the $\beta$ -matrix but only contains $\beta .$ - values for a given node $\dot { \beth }$ , i.e., $\mathrm { ~ b ~ } [ \mathrm { ~ j ~ } ] \ = \ \beta ( \mathrm { i } , \mathrm { j } )$ . Array mark is used to indicate that b[j] has been computed for node i.

The determination of b[j] is done in two phases. First, b[j] is computed for all nodes $\dot { ] }$ on the path from node i to the root of the tree (node 2). These nodes are marked with i. Next, a forward pass is used to compute the remaining $\mathtt { b }$ -values. The $\mathtt { a }$ -values are available in the inner loop.

![](images/b4e194af2243e64664e4383e06e4c17cb46b5f5e904c0b43e615b178703a6349.jpg)  
Figure 4.4 Space efficient computation of .

It is easy to see that this algorithm has time complexity $\mathrm { O } ( \mathrm { n } ^ { 2 } )$ and uses space O(n).

The $\mathtt { a }$ -values provide a good estimate of the edges’ chances of belonging to an optimal tour. The smaller is for an edge, the more promising is this edge. Using -nearness it is often possible to limit the search to relative few of the -nearest neighbors of a node, and still obtain an optimal tour. Computational tests have shown that the $\mathtt { a }$ -measure provides a better estimate of the likelihood of an edge being optimal than the usual c-measure. For example, for the 532-city problem the worst case is an optimal edge being the 22nd c-nearest edge for a node, whereas the worst case when using the -measure is an optimal edge being the 14th $\mathtt { a }$ -nearest. The average rank of the optimal edges among the candidate edges is reduced from 2.4 to 2.1.

This seems to be quite satisfactory. However, the $\mathfrak { a }$ -measure can be improved substantially by making a simple transformation of the original cost matrix. The transformation is based on the following observations [21]:

(1) Every tour is a 1-tree. Therefore the length of a minimum 1-tree is a lower bound on the length of an optimal tour.   
(2) If the length of all edges incident to a node are changed with the same amount, , any optimal tour remains optimal. Thus, if the cost matrix $\mathrm { C = ( c _ { i j } ) }$ is transformed to $\mathrm { D } = ( \mathrm { d } _ { \mathrm { i j } } ^ { \cdot } )$ , where $\mathrm { d _ { i j } = c _ { i j } + \pi _ { i } + \pi _ { j } , }$ then an optimal tour for the $\mathrm { D }$ is also an optimal tour for C. The length of every tour is increased by $2 \hat { \Sigma } \hat { \Pi } _ { \mathrm { i } }$ . The transformation leaves the TSP invariant, but usually changes the minimum 1-tree.   
(3) If $\mathrm { T } _ { \pi }$ is a minimum 1-tree with respect to D, then its length, $\mathrm { L ( T _ { \pi } ) }$ , is a lower bound on the length of an optimal tour for D. Therefore $\mathrm { w } ( \pi ) = \mathrm { L } ( \mathrm { T } _ { \pi } ) - 2 \bar { \Sigma } \pi _ { \mathrm { i } }$ is lower bound on the length of an optimal tour for C.

The aim is now to find a transformation, $\mathrm { ~ C ~ }  \mathrm { ~ D ~ }$ , given by the vector $\Pi { = } \left( \Pi _ { 1 } , \Pi _ { 2 } , . . . , \Pi _ { \mathrm { h } } \right)$ , that maximizes the lower bound $\mathrm { w } ( \bar { \pi } ) = \mathrm { L } ( \mathrm { T } _ { \pi } ) \cdot 2 \bar { \pi } _ { \mathrm { ~ i ~ } }$ .

If $\mathrm { T } _ { \pi }$ becomes a tour, then the exact optimum has been found. Otherwise, it appears, at least intuitively, that if $\mathrm { w } ( \pi ) > \mathrm { w } ( 0 )$ , then $\mathtt { a }$ -values computed from D are better estimates of edges being optimal than $\mathfrak { a }$ -values computed from C.

Usually, the maximum of $\mathrm { w } ( \pi )$ is close to the length of an optimal tour. Computational experience has shown that this maximum typically is less than 1 percent below optimum. However, finding maximum for $\mathrm { w } ( \pi )$ is not a trivial task. The function is piece-wise linear and concave, and therefore not differentiable everywhere.

A suitable method for maximizing $\mathrm { w } ( \pi )$ is subgradient optimization [21] (a subgradient is a generalization of the gradient concept). It is an iterative method in which the maximum is approximated by stepwise changes of .

At each step is changed in the direction of the subgradient, i.e., $\pmb { \mathrm { n } } ^ { \mathrm { k + 1 } } = \pmb { \mathrm { n } } +$ tkvk, where ${ \bf v ^ { k } }$ is a subgradient vector, and tk is a positive scalar, called the step size.

For the actual maximization problem it can be shown that ${ \bf v ^ { \bf k } } = \mathrm { d ^ { k } } - 2$ is a subgradient vector, where $\mathrm { d ^ { k } }$ is a vector having as its elements the degrees of the nodes in the current minimum 1-tree. This subgradient makes the algorithm strive towards obtaining minimum 1-trees with node degrees equal to 2, i.e., minimum 1-trees that are tours. Edges incident to a node with degree 1 are made shorter. Edges incident to a node with degree greater than 2 are made longer. Edges incident to a node with degree 2 are not changed.

The -values are often called penalties. The determination of a (good) set of penalties is called an ascent.

Figure 4.5 shows a subgradient algorithm for computing an approximation W for the maximum of $\mathrm { w } ( \pi )$ .

![](images/dad8c66915d56420c7110a25f5abb0acfb16d92259c3c4d2b87a86f54718e554.jpg)  
Figure 4.5 Subgradient optimization algorithm.

It has been proven [26] that W will always converge to the maximum of $\mathrm { w } ( \pi )$ , if tk $ 0$ for $\mathrm { \bf ~ k } \to \infty$ and $\sum \mathrm { t k } = \infty$ . These conditions are satisfied, for example, if tk is $\mathrm { t ^ { 0 } / k }$ , where $\mathrm { t } ^ { 0 }$ is some arbitrary initial step size. But even if convergence is guaranteed, it is very slow.

The choice of step size is a very crucial decision from the viewpoint of algorithmic efficiency or even adequacy. Whether convergence is guaranteed is often not important, as long as good approximations can be obtained in a short time.

No general methods to determine an optimum strategy for the choice of step size are known. However, many strategies have been suggested that are quite effective in practice [25, 27, 28, 29, 30, 31]. These strategies are heuristics, and different variations have different effects on different problems. In the present implementation of the modified Lin-Kernighan algorithm the following strategy was chosen (inspired by [27] and [31]):

The step size is constant for a fixed number of iterations, called a period. When a period is finished, both the length of the period and the step size are halved.   
The length of the first period is set to $\mathrm { n } / 2$ , where n is the number of cities. The initial step size, $\mathrm { t } ^ { 0 }$ , is set to 1, but is doubled in the beginning of the first period until W does not increase, i.e., $\mathrm { w } ( \pi ^ { \mathrm { k } } ) \leq \mathrm { w } ( \pi ^ { \mathrm { k } - 1 } )$ . When this happens, the step size remains constant for the rest of the period. If the last iteration of a period leads to an increment of $\mathrm { W }$ , then the period is doubled. The algorithm terminates when either the step size, the length of the period or $\mathbf { v ^ { k } }$ becomes zero.

Furthermore, the basic subgradient algorithm has been changed on two points (inspired by [13]):

• The updating of , i.e., $\boldsymbol { \Pi } ^ { \mathrm { k } + 1 } = \boldsymbol { \Pi } ^ { \mathrm { k } } + \mathbf { t } ^ { \mathrm { k } } \mathbf { v } ^ { \mathrm { k } }$ , is replaced by

$$
\pmb { \mathrm { \pi } } ^ { \pmb { \mathrm { k } } + 1 } = \pmb { \mathrm { \pi } } ^ { \pmb { \mathrm { k } } } + \mathbf { \mathrm { t } } ^ { \mathrm { k } } ( 0 . 7 \pmb { \mathrm { v } } ^ { \mathrm { k } } + 0 . 3 \mathbf { \mathrm { v } } ^ { \mathrm { k } - 1 } ) , \mathbf { w } \mathbf { h } \mathbf { \mathrm { e } } \mathbf { \mathrm { v } } ^ { - 1 } = \mathbf { v } ^ { 0 } .
$$

The special node for the 1-tree computations is not fixed. A minimum 1-tree is determined by computing a minimum spanning tree and then adding an edge corresponding to the second nearest neighbor of one of the leaves of the tree. The leaf chosen is the one that has the longest second nearest neighbor distance.

Practical experiments have shown that these changes lead to better bounds.

Having found a penalty vector , that maximizes $\mathbf { w } ( \pi )$ , the transformation given by $\pi$ of the original cost matrix C will often improve the $\mathtt { a }$ -measure substantially. For example, for the 532-city problem every edge of the optimal tour is among the $5 \ \mathsf { \bar { a } }$ -nearest neighbors for at least one of its endpoints. The improvement of the -measure reduces the average rank of the optimal edges among the candidate edges from 2.1 to 1.7. This is close to the ideal value of 1.5 (when every optimal edge has rank 1 or 2).

Table 4.1 shows the percent of optimal edges having a given rank among the nearest neighbors with respect to the c-measure, the $\mathfrak { a }$ -measure, and the improved $\mathtt { a }$ -measure, respectively.   
Table 4.1. The percentage of optimal edges among candidate edges for the 532-city problem.   

<table><tr><td rowspan=1 colspan=1>rank</td><td rowspan=1 colspan=1>c</td><td rowspan=1 colspan=1>α(π= 0)|</td><td rowspan=1 colspan=1>Improved α</td></tr><tr><td rowspan=5 colspan=1></td><td rowspan=2 colspan=1>43.7</td><td rowspan=1 colspan=1>43.7</td><td rowspan=1 colspan=1>47.0</td></tr><tr><td rowspan=1 colspan=1>31.2</td><td rowspan=1 colspan=1></td></tr><tr><td rowspan=1 colspan=1>3.3</td><td rowspan=1 colspan=1></td></tr><tr><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1></td></tr><tr><td rowspan=1 colspan=1>0.7</td><td rowspan=1 colspan=1>0.7</td></tr><tr><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1></td></tr><tr><td rowspan=1 colspan=1>10</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1></td></tr><tr><td rowspan=1 colspan=1>11</td><td rowspan=1 colspan=1>0.2</td><td rowspan=1 colspan=1>0.3</td></tr><tr><td rowspan=5 colspan=1></td><td rowspan=1 colspan=1>0.2</td><td rowspan=1 colspan=1></td></tr><tr><td rowspan=1 colspan=1></td><td rowspan=4 colspan=1>0.1</td></tr><tr><td rowspan=1 colspan=1>0.2</td></tr><tr><td rowspan=1 colspan=1></td></tr><tr><td rowspan=1 colspan=1>0.10.1</td></tr><tr><td rowspan=1 colspan=1>rankavg</td><td rowspan=1 colspan=1>2.4</td><td rowspan=1 colspan=1>2.1</td><td rowspan=1 colspan=1>1.7</td></tr></table>

It appears from the table that the transformation of the cost matrix has the effect that optimal edges come ‘nearer’, when measured by their $\mathtt { a }$ -values. The transformation of the cost matrix ‘conditions’ the problem, so to speak. Therefore, the transformed matrix is also used during the Lin-Kernighan search process. Most often the quality of the solutions is improved by this means.

The greatest advantage of the $\mathtt { a }$ -measure, however, is its usefulness for the construction of the candidate set. By using the $\mathtt { a }$ -measure the cardinality of the candidate set may generally be small without reducing the algorithm’s ability to find short tours. Thus, in all test problems the algorithm was able to find optimal tours using as candidate edges only edges the ${ \boldsymbol { 5 } } { \mathrm { ~ ‰ ~ } }$ -nearest edges incident to each node. Most of the problems could even be solved when search was restricted to only the $4 { \mathfrak { a } }$ -nearest edges.

The candidate edges of each node are sorted in ascending order of their $\mathfrak { a }$ -values. If two edges have the same -value, the one with the smallest cost, $\mathrm { c _ { i j } } ,$ comes first. This ordering has the effect that candidate edges are considered for inclusion in a tour according to their ‘promise’ of belonging to an optimal tour. Thus, the -measure is not only used to limit the search, but also to focus the search on the most promising areas.

To speed up the search even more, the algorithm uses a dynamic ordering of the candidates. Each time a shorter tour is found, all edges shared by this new tour and the previous shortest tour become the first two candidate edges for their end nodes.

This method of selecting candidates was inspired by Stewart [32], who demonstrated how minimum spanning trees could be used to accelerate 3-opt heuristics. Even when subgradient optimization is not used, candidate sets based on minimum spanning trees usually produce better results than nearest neighbor candidate sets of the same size.

Johnson [17] in an alternative implementation of the Lin-Kernighan algorithm used precomputed candidate sets that usually contained more than 20 (ordinary) nearest neighbors of each node. The problem with this type of candidate set is that the candidate subgraph need not be connected even when a large fraction of all edges is included. This is, for example, the case for geometrical problems in which the point sets exhibit clusters. In contrast, a minimum spanning tree is (by definition) always connected.

Other candidate sets may be considered. An interesting candidate set can be obtained by exploiting the Delaunay graph [13, 33]. The Delaunay graph is connected and may be computed in linear time, on the average. A disadvantage of this approach, however, is that candidate sets can only be computed for geometric problem instances. In contrast, the $\mathtt { a }$ -measure is applicable in general.

# 4.2 Breaking of tour edges

A candidate set is used to prune the search for edges, Y, to be included in a tour. Correspondingly, the search of edges, X, to be excluded from a tour may be restricted. In the actual implementation the following simple, yet very effective, pruning rules are used:

(1) The first edge to be broken, $\mathbf { X } _ { 1 }$ , must not belong to the currently best solution tour. When no solution tour is known, that is, during the determination of the very first solution tour, $\mathbf { X } _ { 1 }$ must not belong to the minimum 1-tree.   
(2) The last edge to be excluded in a basic move must not previously have been included in the current chain of basic moves.

The first rule prunes the search already at level 1 of the algorithm, whereas the original algorithm of Lin and Kernighan prunes at level 4 and higher, and only if an edge to be broken is a common edge of a number (2-5) of solution tours. Experiments have shown that the new pruning rule is more effective. In addition, it is easier to implement.

The second rule prevents an infinite chain of moves. The rule is a relaxation of Rule 4 in Section 3.2.

# 4.3 Basic moves

Central in the Lin-Kernighan algorithm is the specification of allowable moves, that is, which subset of r-opt moves to consider in the attempt to transform a tour into a shorter tour.

The original algorithm considers only r-opt moves that can be decomposed into a $2 \bar { . }$ or 3-opt move followed by a (possibly empty) sequence of 2-opt moves. Furthermore, the r-opt move must be sequential and feasible, that is, it must be a connected chain of edges where edges removed alternate with edges added, and the move must result in a feasible tour. Two minor deviations from this general scheme are allowed. Both have to do with 4-opt moves. First, in one special case the first move of a sequence may be a sequential 4-opt move (see Figure 3.7); the following moves must still be 2-opt moves. Second, nonsequential 4-opt moves are tried when the tour can no longer be improved by sequential moves (see Figure 3.3).

The new modified Lin-Kernighan algorithm revises this basic search structure on several points.

First and foremost, the basic move is now a sequential 5-opt move. Thus, the moves considered by the algorithm are sequences of one or more 5-opt moves. However, the construction of a move is stopped immediately if it is discovered that a close up of the tour results in a tour improvement. In this way the algorithm attempts to ensure 2-, 3-, 4- as well as 5-optimality.

Using a 5-opt move as the basic move broadens the search and increases the algorithm’s ability to find good tours, at the expense of an increase of running times. However, due to the use of small candidate sets, run times are only increased by a small factor. Furthermore, computational experiments have shown that backtracking is no longer necessary in the algorithm (except, of course, for the first edge to be excluded, ${ \bf X } _ { 1 } \mathrm { ~ . ~ }$ ). The removal of backtracking reduces runtime and does not degrade the algorithm’s performance significantly. In addition, the implementation of the algorithm is greatly simplified.

The new algorithm’s improved performance compared with the original algorithm is in accordance with observations made by Christofides and Eilon [16]. They observed that 5-optimality should be expected to yield a relatively superior improvement over 4-optimality compared with the improvement of 4-optimality over 3-optimality.

Another deviation from the original algorithm is found in the examination of nonsequential exchanges. In order to provide a better defense against possible improvements consisting of nonsequential exchanges, the simple nonsequential 4-opt move of the original algorithm has been replaced by a more powerful set of nonsequential moves.

This set consists of

• any nonfeasible 2-opt move (producing two cycles) followed by any 2- or 3-opt move, which produces a feasible tour (by joining the two cycles); • any nonfeasible 3-opt move (producing two cycles) followed by any 2-opt move, which produces a feasible tour (by joining the two cycles).

As seen, the simple nonsequential 4-opt move of the original algorithm belongs to this extended set of nonsequential moves. However, by using this set of moves, the chances of finding optimal tours are improved. By using candidate sets and the “positive gain criterion” the time for the search for such nonsequential improvements of the tour is small relative to the total running time.

Unlike the original algorithm the search for nonsequential improvements is not only seen as a post optimization maneuver. That is, if an improvement is found, further attempts are made to improve the tour by ordinary sequential as well as nonsequential exchanges.

# 4.4 Initial tours

The Lin-Kernighan algorithm applies edge exchanges several times to the same problem using different initial tours.

In the original algorithm the initial tours are chosen at random. Lin and Kernighan concluded that the use of a construction heuristic only wastes time. Besides, construction heuristics are usually deterministic, so it may not be possible to get more than one solution.

However, the question of whether or not to use a construction heuristic is not that simple to answer. Adrabinsky and Syslo [34], for instance, found that the farthest insertion construction heuristic was capable of producing good initial tours for the Lin-Kernighan algorithm. Perttunen [35] found that the

Clarke and Wright savings heuristic [36] in general improved the performance of the algorithm. Reinelt [13] also found that is better not to start with a random tour. He proposed using locally good tours containing some major errors, for example the heuristics of Christofides [37]. However, he also observed that the difference in performance decreases with more elaborate versions of the Lin-Kernighan algorithm.

Experiments with various implementations of the new modified Lin-Kernighan algorithm have shown that the quality of the final solutions does not depend strongly on the initial tours. However, significant reduction in run time may be achieved by choosing initial tours that are close to being optimal.

In the present implementation the following simple construction heuristic is used:

1. Choose a random node i.   
2. Choose a node j, not chosen before, as follows: If possible, choose j such that (a) (i,j) is a candidate edge, (b) $\alpha ( \mathrm { i } , \mathrm { j } ) = 0$ , and (c) $( \mathrm { i } , \mathrm { j } )$ belongs to the current best tour. Otherwise, if possible, choose j such that (i,j) is a candidate edge. Otherwise, choose j among those nodes not already chosen.   
3. Let $\mathrm { i } = \mathrm { j }$ . If not all nodes have been chosen, then go to Step 2.

If more than one node may be chosen at Step 2, the node is chosen at random among the alternatives. The sequence of chosen nodes constitutes the initial tour.

This construction procedure is fast, and the diversity of initial solutions is large enough for the edge exchange heuristics to find good final solutions.

# 4.5 Specification of the modified algorithm

This section presents an overview of the modified Lin-Kernighan algorithm.   
The algorithm is described top-down using the C programming language.

Below is given a sketch of the main program.

![](images/4a241d5c5aa6beff4260126b7740da01aead1a51a692bb2e94b506a8accd7cf7.jpg)

First, the program reads the specification of the problem to be solved and creates the candidate set. Then a specified number (Runs) of local optimal tours is found using the modified Lin-Kernighan heuristics. The best of these tours is printed before the program terminates.

The creation of the candidate set is based on $\mathfrak { a }$ -nearness.

![](images/702a6293655e1001bf0a678b7b02ccc34372700944c0368b7a5f03590a59703a.jpg)

First, the function Ascent determines a lower bound on the optimal tour length using subgradient optimization. The function also transforms the original problem into a problem in which $\mathfrak { a }$ -values reflect the likelihood of edges being optimal. Next, the function GenerateCandidates computes the $\mathfrak { a }$ -values and associates to each node a set of incident candidate edges. The edges are ranked according to their -values. The parameter MaxCandidates specifies the maximum number of candidate edges allowed for each node, and MaxAlpha puts an upper limit on their -values. The value of MaxAlpha is set to some fraction, Excess, of the lower bound.

The pseudo code of the function Ascent shown below should be reasonable self-explanatory. It follows the description given in Section 4.1. The V-value of a node is its degree minus 2. Therefore, Norm being the sum of squares of all V-values, is a measure of a minimum 1-tree’s discrepancy from a tour. If Norm is zero, then the 1-tree constitutes a tour, and an optimal tour has been found. In order to speed up the computations the algorithm uses candidate sets in the computations of minimum 1-trees.

double Ascent() { Node \*N; double BestW, W; int Period $=$ InitialPeriod, P, InitialPhase $\ c = ~ 1$ ; $\begin{array} { r l } { \mathbb { W } } & { { } = } \end{array}$ Minimum1TreeCost(); if $( \mathrm { N o r m } = 0 $ ) return W; GenerateCandidates(AscentCandidates, LONG_MAX); BestW $\qquad = \quad \boldsymbol { \ W }$ ; ForAllNodes(N) { $\mathrm { { N - > L a s t V } \ = \Delta N { - } > V } ; $ $\tt N \mathrm { \to \tt B e s t P i } = N \mathrm { \to \tt B i }$ ; } for ( $\begin{array} { r l } { \mathrm { T } } & { { } = } \end{array}$ InitialStepSize; $\mathrm { ~ \tt ~ T ~ } > \mathrm { ~ \tt ~ O ~ }$ ; Period $\mathbf { \Omega } / = \mathbf { \Omega } 2$ , $\mathrm { ~ T ~ \ / = ~ \ 2 ~ }$ ) { for ( $\textsuperscript { . p } =  { 1 }$ ; $\mathrm { ~ \tt ~ T ~ } > \mathrm { ~ \tt ~ O ~ }$ && P $< =$ Period; $\mathbb { P } { \mathrel { + { + } } }$ ) { ForAllNodes(N) { if $( \mathrm { N - } > \mathrm { V } \quad ! = \mathrm { ~ 0 ~ }$ ) $\mathrm { N \mathrm { - > } P i } \mathrm { \Lambda } + = \mathrm { \Large ~ T ^ { \star } ~ } ( 7 \mathrm { { } } ^ { \star } \mathrm { N \mathrm { - > } V } + 3 ^ { \star } \mathrm { N \mathrm { - > } L a s t { v } } ) / 1 0$ ; N->LastV $=$ N->V; } $\begin{array} { r l } { \mathbb { W } } & { { } = } \end{array}$ Minimum1TreeCost(); if $( \mathrm { N o r m } = 0 ) \ .$ ) return W; if ( $. W >$ BestW) { BestW $\qquad = \quad \boldsymbol { \ W }$ ; ForAllNodes(N) $\tt N \mathrm { \to B e s t P i } = N \mathrm { \to B i } _ { \mathrm { \Lambda } }$ ; if (InitialPhase) T $\star = ~ 2$ ; if ( $\begin{array} { r l } { \operatorname { \mathbb { P } } } & { { } = = } \end{array}$ Period) Period $\star = ~ 2$ ; } else if (InitialPhase && P $>$ InitalPeriod/2) { InitialPhase $\qquad = \quad 0$ ; $\mathrm { ~ \tt ~ { ~ P ~ } ~ } = \mathrm { ~ \tt ~ { ~ O ~ } ~ }$ ; $\mathrm { ~ T ~ } = \ 3 ^ { \star } \mathrm { T } / 4$ ; } } ForAllNodes(N) $\tt N { \mathrm { \mathrm { - > P i } } } \ = \ \tt N { \mathrm { - > B e s t P i } } .$ ; return Minimum1TreeCost();

Below is shown the pseudo code of the function GenerateCandidates. For each node at most MaxCandidates candidate edges are determined. This upper limit, however, may be exceeded if a “symmetric” neighborhood is desired (SymmetricCandidates $\ ! = 0 ^ { \cdot }$ ) in which case the candidate set is complemented such that every candidate edge is associated to both its two end nodes.

<table><tr><td>void GenerateCandidates(long MaxCandidates, long MaxAlpha) { Node *From, *To; long Alpha;</td></tr><tr><td>Candidate *Edge;</td></tr><tr><td>ForAllNodes(From)</td></tr><tr><td></td></tr><tr><td>From-&gt;Mark = 0;</td></tr><tr><td></td></tr><tr><td>ForAllNodes(From) {</td></tr><tr><td>if (From != FirstNode) { From-&gt;Beta = LONG_MIN;</td></tr><tr><td>for (To = From; To-&gt;Dad != O; To = To-&gt;Dad) {</td></tr><tr><td>To-&gt;Dad-&gt;Beta = max(To-&gt;Beta, To-&gt;Cost); To-&gt;Dad-&gt;Mark = From;</td></tr><tr><td>}</td></tr><tr><td>} ForAllNodes(To, To != From) {</td></tr><tr><td>if (From == FirstNode)</td></tr><tr><td></td></tr><tr><td>Alpha = To == From-&gt;Father ? 0 :</td></tr><tr><td>C(From,To) - From-&gt;NextCost;</td></tr><tr><td>else if (To == FirstNode)</td></tr><tr><td>Alpha = From == To-&gt;Father ? O:</td></tr><tr><td>C(From,To) - To-&gt;NextCost;</td></tr><tr><td>else {</td></tr><tr><td>if (To-&gt;Mark != From)</td></tr><tr><td>To-&gt;Beta = max(To-&gt;Dad-&gt;Beta, To-&gt;Cost);</td></tr><tr><td>Alpha = C(From,To) - To-&gt;Beta;</td></tr><tr><td>}</td></tr><tr><td>if (Alpha &lt;= MaxAlpha)</td></tr><tr><td>InsertCandidate(To, From-&gt;CandidateSet);</td></tr><tr><td>}</td></tr><tr><td></td></tr><tr><td>if (SymmetricCandidates)</td></tr><tr><td>ForAllNodes(From)</td></tr><tr><td></td></tr><tr><td>ForAllCandidates(To, From-&gt;CandidateSet)</td></tr><tr><td>if (!IsMember(From, To-&gt;CandidateSet))</td></tr><tr><td>InsertCandidate(From, To-&gt;CandidateSet);</td></tr></table>

After the candidate set has been created the function FindTour is called a predetermined number of times (Runs). FindTour performs a number of trials where in each trial it attempts to improve a chosen initial tour using the modified Lin-Kernighan edge exchange heuristics. Each time a better tour is found, the tour is recorded, and the candidates are reordered with the function AdjustCandidateSet. Precedence is given to edges that are common to the two currently best tours. The candidate set is extended with those tour edges that are not present in the current set. The original candidate set is re-established at exit from FindTour.

![](images/4798d705a181472b0859d2dbe8a419291105699a50f2ff0c84b5006c794414f1.jpg)

The following function, LinKernighan, seeks to improve a tour by sequential and nonsequential edge exchanges.

<table><tr><td>double LinKernighan() { Node *t1, *t2; int X2, Failures; long G, Gain; double Cost = 0; ForAllNodes(t1)</td></tr><tr><td>Cost += C(t1,SUC(t1)); do { Failures = 0;</td></tr><tr><td></td></tr><tr><td>ForallNodes(tl, Failures &lt; Dimension) {</td></tr><tr><td>for (X2 = 1; X2 &lt;= 2; X2++) {</td></tr><tr><td></td></tr><tr><td>t2 = X2 == 1 ? PRED(t1) : SUC(t1);</td></tr><tr><td>if (InBetterTour(tl,t2))</td></tr><tr><td>continue; G = C(t1,t2);</td></tr><tr><td>while (t2 = BestMove(tl, t2, &amp;G, &amp;Gain)) {</td></tr><tr><td>if (Gain &gt; 0) {</td></tr><tr><td>Cost -= Gain;</td></tr><tr><td>StoreTour();</td></tr><tr><td>Failures = 0;</td></tr><tr><td>goto Next_t1;</td></tr><tr><td></td></tr><tr><td>}</td></tr><tr><td>}</td></tr><tr><td>Failures++;</td></tr><tr><td>RestoreTour();</td></tr><tr><td></td></tr><tr><td></td></tr><tr><td></td></tr><tr><td>Next_t1: ;</td></tr><tr><td>}</td></tr><tr><td></td></tr><tr><td>if ((Gain = Gain23()) &gt; 0) {</td></tr><tr><td>Cost -= Gain;</td></tr><tr><td></td></tr><tr><td></td></tr><tr><td></td></tr><tr><td>StoreTour();</td></tr><tr><td></td></tr><tr><td></td></tr><tr><td>}</td></tr></table>

First, the function computes the cost of the initial tour. Then, as long as improvements may be achieved, attempts are made to find improvements using sequential 5-opt moves (with BestMove), or when not possible, using nonsequential moves (with Gain23). For each sequential exchange, a basis edge $( \ t _ { } 1 , \ t _ { } 2 )$ is found by selecting t1 from the set of nodes and then selecting $\pm 2$ as one of t1’s two neighboring nodes in the tour. If $( \ t 1 , \ t 2 )$ is an edge of the trial’s best tour (BetterTour), then it is not used as a basis edge.

The function BestMove is sketched below. The function BestMove makes sequential edge exchanges. If possible, it makes an r-opt move $( \mathrm { r } \leq 5 )$ that improves the tour. Otherwise, it makes the most promising 5-opt move that fulfils the positive gain criterion.

Node \*BestMove(Node \*t1, Node \*t2, long \*G0, long \*Gain) { Node \*t3, \*t4, \*t5, \*t6, \*t7, \*t8, \*t9, \*t10; Node \*T3, \*T4, \*T5, \*T6, \*T7, \*T8, \*T9, $^ { \star } \mathbb { T } 1 0 \ = \ 0 ,$ ; long G1, G2, G3, G4, G5, G6, G7, G8, BestG8 $=$ LONG_MIN; int X4, X6, X8, X10; ${ } ^ { \star } \mathsf { G a i n } ~ = ~ 0 ; ~ \mathsf { R e v e r s e d } ~ = ~ \mathsf { S U C } ~ ( \mathsf { t } 1 ) ~ : = ~ \mathsf { t } 2 ;$ ForAllCandidates(t3, $\pm 2 - >$ CandidateSet) { if ( $\begin{array} { l l } { \pm 3 } & { = = } \end{array}$ PRED(t2) || $\begin{array} { l l } { \pm 3 } & { = = } \end{array}$ SUC(t2) || $( \mathsf { G } \mathbb { 1 } ) \subset \star \mathsf { G } 0 - \mathsf { C } ( \mathsf { t } 2 , \mathsf { t } 3 ) \big ) \subset = \mathsf { 0 } )$ continue; for ( $\mathrm { ~ \ : ~ } \mathrm { ~ \ : ~ } \mathrm { ~ \ : ~ } \mathrm { ~ \ : ~ } \mathrm { ~ \ : ~ } \mathrm { ~ \ : ~ } .$ ; $\mathrm { ~ \ X 4 ~ } ~ < = ~ 2$ ; $\mathrm { ~ X 4 + + }$ ) { $\ t 4 ~ = ~ \mathrm {  ~ X ~ 4 ~ } = = ~ 1$ ? PRED(t3) : SUC(t3); ${ \mathsf { G } } 2 ~ = ~ { \mathsf { G } } 1 ~ + ~ { \mathsf { C } } ( { \mathsf { t } } 3 , { \mathsf { t } } 4 )$ ; if ( $\mathrm { ~ \ X 4 ~ } ~ = = ~ 1$ && (\*Gain = G2 - C(t4,t1)) > 0) { Make2OptMove(t1, t2, t3, t4); return t4; } ForAllCandidates(t5, t4->CandidateSet) { if ( $\pm 5 \quad = =$ PRED(t4) || $\pm 5 \quad = =$ SUC(t4) || $( \mathsf { G 3 } \ = \ \mathsf { G 2 } - \mathsf { C } ( \mathsf { t 4 } , \mathsf { t 5 } ) \ ) < = \ 0$ continue; for ( $\mathrm { ~ \normalfont ~ { ~ X ~ 6 ~ } ~ } = \mathrm { ~ \normalfont ~ { ~ 1 ~ } ~ }$ ; $\mathrm { ~ \ X 6 ~ } ~ < = ~ 2$ ; ${ \mathrm { X 6 + + } }$ ) { Determine (T3,T4,T5,T6,T7,T8,T9,T10) = (t3,t4,t5,t6,t7,t8,t9,t10) such that $\begin{array} { r c c c l } { { \sf G 8 } } & { { = } } & { { \star _ { \sf G } { 0 } } } & { { - } } & { { \sf C \left( \pm 2 , \sf T 3 \right) } } & { { + } } & { { \sf C \left( \mathbb { T } 3 , \mathbb { T } 4 \right) } } \\ { { } } & { { - } } & { { \sf C \left( \mathbb { T } 4 , \mathbb { T } 5 \right) } } & { { + } } & { { \sf C \left( \mathbb { T } 5 , \mathbb { T } 6 \right) } } \\ { { } } & { { - } } & { { \sf C \left( \mathbb { T } 6 , \mathbb { T } 7 \right) } } & { { + } } & { { \sf C \left( \mathbb { T } 7 , \mathbb { T } 8 \right) } } \\ { { } } & { { - } } & { { \sf C \left( \mathbb { T } 8 , \mathbb { T } 9 \right) } } & { { + } } & { { \sf C \left( \mathbb { T } 9 , \mathbb { T } 1 0 \right) } } \end{array}$ is maximum ( $=$ BestG8), and (T9,T10) has not previously been included; if during this process a legal move with \*Gain > 0 is found, then make the move and exit from BestMove immediately; } } } } $\star _ { \sf G a i n } ~ = ~ 0$ ; if ( $\mathrm { ~ T 1 0 ~ \Omega = ~ 0 ~ }$ ) return 0; Make5OptMove(t1,t2,T3,T4,T5,T6,T7,T8,T9,T10); \*G0 = BestG8; return T10;   
}

Only the first part of the function (the 2-opt part) is given in some detail. The rest of the function follows the same pattern. The tour is as a circular list. The flag Reversed is used to indicate the reversal of a tour.

To prevent an infinite chain of moves the last edge to be deleted in a 5-opt move, (T9,T10), must not previously have been included in the chain.

A more detailed description of data structures and other implementation issues may be found in the following section.

# 5. Implementation

The modified Lin-Kernighan algorithm has been implemented in the programming language C. The software, approximately 4000 lines of code, is entirely written in ANSI C and portable across a number of computer platforms and C compilers. The following subsections describe the user interface and the most central techniques employed in the implementation.

# 5.1 User interface

The software includes code both for reading problem instances and for printing solutions.

Input is given in two separate files:

(1) the problem file and (2) the parameter file.

The problem file contains a specification of the problem instance to be solved. The file format is the same as used in TSPLIB [38], a publicly available library of problem instances of the TSP.

The current version of the software allows specification of symmetric, asymmetric, as well as Hamiltonian tour problems.

Distances (costs, weights) may be given either explicitly in matrix form (in a full or triangular matrix), or implicitly by associating a 2- or 3-dimensional coordinate with each node. In the latter case distances may be computed by either a Euclidean, Manhattan, maximum, geographical or pseudo-Euclidean distance function. See [38] for details. At present, all distances must be integral.

Problems may be specified on a complete or sparse graph, and there is an option to require that certain edges must appear in the solution of the problem.

The parameter file contains control parameters for the solution process. The solution process is typically carried out using default values for the parameters. The default values have proven to be adequate in many applications. Actually, almost all computational tests reported in this paper have been made using these default settings. The only information that cannot be left out is the name of the problem file.

The format is as follows:

PROBLEM_ $\mathrm { { ^ { * } I L E } } = { < s t r i n g > }$ Specifies the name of the problem file.

Additional control information may be supplied in the following format:

$\mathrm { R U N S } = < i n t e g e r >$ The total number of runs. Default: 10.

$\mathrm { M A X \_ T R I A L S } = < i n t e g e r >$ The maximum number of trials in each run. Default: number of nodes (DIMENSION, given in the problem file).

TOUR_ $\mathrm { F I L E } = < s t r i n g >$ Specifies the name of a file to which the best tour is to be written.

OPTIMUM $=$ <real>   
Known optimal tour length. A run will be terminated as soon as a tour length less than or equal to optimum is achieved.   
Default: DBL_MAX.

MAX_CANDIDATES $=$ <integer> { SYMMETRIC }

The maximum number of candidate edges to be associated with each node. The integer may be followed by the keyword SYMMETRIC, signifying that the candidate set is to be complemented such that every candidate edge is associated with both its two end nodes.   
Default: 5.

ASCENT_CANDIDATES $=$ <integer>

The number of candidate edges to be associated with each node during the ascent. The candidate set is complemented such that every candidate edge is associated with both its two end nodes.   
Default: 50. $\mathrm { E X C E S S } = < i n t e g e r >$   
The maximum -value allowed for any candidate edge is set to EXCESS times the absolute value of the lower bound of a solution tour (determined by the ascent). Default: 1.0/DIMENSION.

INITIAL_PERIOD $=$ <integer> The length of the first period in the ascent. Default: DIMENSION/2 (but at least 100).

INITIAL_STEP_ $\mathrm { S I Z E } = < i n t e g e r >$ The initial step size used in the ascent. Default: 1.

$\mathrm { P I } \_ { \mathrm { F I L E } } = < s t r i n g >$

Specifies the name of a file to which penalties ( -values determined by the ascent) is to be written. If the file already exits, the penalties are read from the file, and the ascent is skipped.

PRECISI $\mathrm { O N } = < i n t e g e r >$ The internal precision in the representation of transformed distances: $\mathrm { d _ { i j } = P R E C I S I O N * } \mathrm { c _ { i j } + \mathrm { \Pi \Pi _ { i } + \Pi \mathrm { f _ { j } } } } ,$ where ${ \mathrm { d } } _ { \mathrm { i j } } , { \mathrm { c } } _ { \mathrm { i j } } ,$ i and $\Pi _ { \mathrm { j } }$ are all integral. Default: 100 (which corresponds to 2 decimal places).

SEED $=$ <integer>   
Specifies the initial seed for random number generation. Default: 1.

SUBGRADIENT: [ YES | NO ]

Specifies whether the -values should be determined by subgradient optimization.   
Default: YES.

$\mathrm { \Delta T R A C E \_ L E V E L } = < i n t e g e r >$

Specifies the level of detail of the output given during the solution process. The value 0 signifies a minimum amount of output. The higher the value is the more information is given.   
Default: 1.

During the solution process information about the progress being made is written to standard output. The user may control the level of detail of this information (by the value of the TRACE_LEVEL parameter).

Before the program terminates, a summary of key statistics is written to standard output, and, if specified by the TOUR_FILE parameter, the best tour found is written to a file (in TSPLIB format).

The user interface is somewhat primitive, but it is convenient for many applications. It is simple and requires no programming in C by the user. However, the current implementation is modular, and an alternative user interface may be implemented by rewriting a few modules. A new user interface might, for example, enable graphical animation of the solution process.

# 5.2 Representation of tours and moves

The representation of tours is a central implementation issue. The data structure chosen may have great impact on the run time efficiency. It is obvious that the major bottleneck of the algorithm is the search for possible moves (edge exchanges) and the execution of such moves on a tour. Therefore, special care should be taken to choose a data structure that allows fast execution of these operations.

The data structure should support the following primitive operations:

(1) find the predecessor of a node in the tour with respect to a chosen orientation (PRED);   
(2) find the successor of a node in the tour with respect to a chosen orientation (SUC);   
(3) determine whether a given node is between two other nodes in the tour with respect to a chosen orientation (BETWEEN);   
(4) make a move;   
(5) undo a sequence of tentative moves.

The necessity of the first three operations stems from the need to determine whether it is possible to 'close' the tour (see Figures 3.5-3.7). The last two operations are necessary for keeping the tour up to date.

In the modified Lin-Kernighan algorithm a move consists of a sequence of basic moves, where each basic move is a 5-opt move (k-opt moves with $\mathrm { k } \leq 4$ are made in case an improvement of the tour is possible).

In order simplify tour updating, the following fact may be used: Any r-opt move $( \mathrm { r } \geq 2 )$ is equivalent to a finite sequence of 2-opt moves [16, 39]. In the case of 5-opt moves it can be shown that any 5-opt move is equivalent to a sequence of at most five 2-opt moves. Any 4-opt move as well as any 3-opt move is equivalent to a sequence of at most three 2-opt moves.

This is exploited as follows. Any move is executed as a sequence of one or more 2-opt moves. During move execution, all 2-opt moves are recorded in a stack. A bad move is undone by unstacking the 2-opt moves and making the inverse 2-opt moves in this reversed sequence.

Thus, efficient execution of 2-opt moves is needed. A 2-opt move, also called a swap, consists of moving two edges from the current tour and reconnecting the resulting two paths in the best possible way (see Figure 2.1). This operation is seen to reverse one of the two paths. If the tour is represented as an array of nodes, or as a doubly linked list of nodes, the reversal of the path takes time O(n).

It turns out that data structures exist that allow logarithmic time complexity to be achieved [13, 40, 41, 42, 43]. These data structures, however, should not be selected without further notice. The time overhead of the corresponding update algorithms is usually large, and, unless the problem is large, typically more than 1000 nodes, update algorithms based on these data structures are outperformed by update algorithms based on the array and list structures. In addition, they are not simple to implement.

In the current implementation of the modified Lin-Kernighan algorithm a tour may be represented in two ways, either by a doubly linked list, or by a twolevel tree [43]. The user can select one of these two representations. The doubly linked list is recommended for problems with fewer than 1000 nodes. For larger problems the two-level tree should be chosen.

When the doubly link list representation is used, each node of the problem is represented by a C structure as outlined below.

![](images/ca40553d611a8b10eae319837697f1347d83a506d1ff39159311ed394bc5b477.jpg)

The variable Id is the identification number of the node $\bigl ( 1 \leq \ I \mathrm { d } \leq \mathrm { n } \bigr )$ ) .

Rank gives the ordinal number of the node in the tour. It is used to quickly determine whether a given node is between two other nodes in the tour.

Pred and Suc point to the predecessor node and the successor node of the tour, respectively.

A 2-opt move is made by swapping Pred and Suc of each node of one of the two segments, and then reconnecting the segments by suitable settings of Pred and Suc of the segments’ four end nodes. In addition, Rank is updated for nodes in the reversed segment.

The following small code fragment shows the implementation of a 2-opt move. Edges (t1,t2) and $( \in 3 , \pm 4 )$ are exchanged with edges (t2,t3) and $( \ t 1 , \ t 4 )$ (see Figure 3.1).

Any of the two segments defined by the 2-opt move may be reversed. The segment with the fewest number of nodes is therefore reversed in order to speed up computations. The number of nodes in a segment can be found in constant time from the Rank-values of its end nodes. In this way much run time can be spared. For an example problem with 1000 nodes the average number of nodes touched during reversal was about 50, whereas a random reversal would have touched 500 nodes, on the average. For random Euclidean instances, the length of the shorter segment seems to grow roughly as $\mathtt { n } ^ { 0 . 7 }$ [44].

However, the worst-case time cost of a 2-opt move is still O(n), and the costs of tour manipulation grow to dominate overall running time as n increases.

A worst-case cost of ${ \mathrm { O } } ( { \sqrt { \mathrm { n } } } )$ per 2-opt move may be achieved using a two-level tree representation. This is currently the fastest and most robust representation on large instances that might arise in practice. The idea is to divide the tour into roughly n segments. Each segment is maintained as a doubly linked list of nodes (using pointers labeled Pred and Suc).

Each node is represented by a C structure as outlined below.

![](images/1ebe464c1161405cd9dae717d27b95f890e93ae356d423ed41f53e586c661501.jpg)

Rank gives the position of the node within the segment, so as to facilitate BETWEEN queries. Parent is a pointer the segment containing the node.

Each segment is represented by the following C structure.

![](images/53d1315ee03c3e7270721c74621d5158496494807bc1c13116a9f28f1d283071.jpg)

The segments are connected in a doubly linked list (using pointers labeled Pred and Suc), and each segment contains a sequence number, Rank, that represents its position in the list.

First and Last are pointers to the segment's two end nodes. Reversed is a reversal bit indicating whether the segment should be traversed in forward or reverse direction. Just switching this bit reverses the orientation of a segment.

All the query operations (PRED, SUC and BETWEEN) are performed in constant time (as in the list representation, albeit with slightly larger constants), whereas the move operations have a worst-case cost of ${ \mathrm { O } } { \overline { { ( } } } { \sqrt { \mathrm { n } } } )$ per move.

The implementation of the operations closely follows the suggestions given in [43]. See [43, pp. 444-446] for details.

# 5.3 Distance computations

A bottleneck in many applications is the computing of distances. For example, if Euclidean distances are used, a substantial part of run time may be spent in computing square roots.

If sufficient space is available, all distances may be computed once and stored in a matrix. However, for large problems, say more than 5000 nodes, this approach is usually not possible.

In the present implementation, distances are computed once and stored in a matrix, only if the problem is smaller than a specified maximum dimension. For larger problems, the following techniques are used to reduce run time.

(1) Each candidate edge including its length is associated to the node from which it emanates. A large fraction of edges considered during the solution process are candidate edges. Therefore, in many cases the length of an edge may be found by a simple search among the candidate edges associated with its end nodes.

(2) Computational cheap functions are used in calculating lower bounds for distances. For example, a lower bound for an Euclidean distance $\surd ( \mathrm { ~ d x } ^ { 2 } + \mathrm { d y } ^ { 2 } )$ may be quickly computed as the maximum of $\left| \operatorname { d x } \right|$ and |dy|. Often a reasonable lower bound for a distance is sufficient for deciding that there is no point in computing the true distance. This may, for example, be used for quickly deciding that a tentative move cannot possibly lead to a tour improvement. If the current gain, plus a lower bound for the distance of a closing edge, is not positive, then the tour will not be improved by this move.

(3) The number of distance computations is reduced by the caching technique described in [45]. When a distance between two nodes has been computed the distance is stored in a hash table. The hash index is computed from the identification numbers of the two nodes. Next time the distance between the same two nodes is to be computed, the table is consulted to see whether the distance is still available. See [45] for details. The effect of using the caching technique was measured in the solution of a 2392-node problem. Here optimum was found with about 70 times fewer ordinary distance calculations than without the technique, and the running time was more than halved.

# 5.4 Reduction of checkout time

When the algorithm has found a local optimum, time is spent to check that no further progress is possible. This time, called the checkout time, can be avoided if the same local optimum has been found before. There is no point in attempting to find further improvements - the situation has been previously been 'checked out'. The checkout time often constitutes a substantial part of the running time. Lin and Kernighan report checkout times that are typically 30 to 50 per cent of running time.

The modified algorithm reduces checkout time by using the following techniques.

(1) Moves in which the first edge $\displaystyle ( \mathfrak { t } _ { 1 } , \mathfrak { t } _ { 2 } )$ to be broken belongs to the currently best solution tour are not investigated.

(2) A hashing technique is used. A hash function maps tours to locations in a hash table. Each time a tour improvement has been found, the hash table is consulted to see whether the new tour happens to be local optimum found earlier. If this is the case, fruitless checkout time is avoided. This technique is described in detail in [46].

(3) The concept of the don’t look bit, introduced by Bentley [44], is used. If for a given choice of $\mathrm { t } _ { 1 }$ the algorithm previously failed to find an improvement, and if $\mathrm { t } _ { 1 } \mathrm { ' s }$ tour neighbors have not changed since that time, then it is unlikely that an improving move can made if the algorithm again looks at $\mathfrak { t } _ { 1 }$ . This is exploited as follows. Each node has a don’t look bit, which initially is 0. The bit for node $\mathrm { t } _ { 1 }$ is set to 1 whenever a search for an improving move with $\mathrm { t } _ { 1 }$ fails, and it is set to 0 whenever an improving move is made in which it is an end node of one of the its edges. In considering candidates for $\mathfrak { t } _ { 1 }$ all nodes whose don’t look bit is 1 are ignored. This is done in maintaining a queue of nodes whose bits are zero.

# 5.5 Speeding up the ascent

Subgradient optimization is used to determine a lower bound for the optimum. At each step a minimum 1-tree is computed. Since the number of steps may be large, it is important to speed up the computation of minimum 1-trees. For this purpose, the trees are computed in sparse graphs.

The first tree is computed in a complete graph. All remaining trees but the last are computed in a sparse subgraph determined by the $\mathtt { a }$ -measure. The subgraph consists of a specified number of -nearest neighbor edges incident to each node.

Prim's algorithm [22] is used for computing minimum spanning trees. Therefore, to achieve a speed-up it is necessary to quickly find the shortest edge from a number of edges. In the current implementation a binary heap is used for this purpose.

The combination of these methods results in fast computation of minimum spanning trees, at least when the number of candidate edges allowed for each node is not too large. On the other hand, this number should not be so small that the lower bound computed by the ascent is not valid. In the present implementation, the number is 50 by default.

# 6. Computational results

The performance of an approximate algorithm such as the Lin-Kernighan algorithm can be evaluated in three ways:

(1) by worst-case analysis   
(2) by probabilistic (or average-case) analysis   
(3) by empirical analysis

The goal of worst-case analysis is to derive upper bounds for possible deviations from optimum; that is, to provide quality guarantees for results produced by the algorithm.

All known approximate algorithms for the TSP have rather poor worst-case behavior. Assume, for example, that the problems to be solved are metric (the triangle inequality holds). Then the approximate algorithm known to have the best worst-case behavior is the algorithm of Christofides [37]. This algorithm guarantees a tour length no more than $50 \%$ longer than optimum. For any ropt algorithm, where $\bar { \boldsymbol { \mathrm { r } } } \leq \boldsymbol { \mathrm { n } } / 4$ (n being the number of cities), problems may be constructed such that the error is almost $100 \%$ [11]. For non-metric problems it can proven that it is impossible to construct an algorithm of polynomial complexity which find tours whose length is bound by a constant multiple of the optimal tour length [47].

The purpose of the second method, probabilistic analysis, is to evaluate average behavior of the algorithms. For example, for an approximate TSP algorithm probability analysis can used be to estimate the expected error for large problem sizes.

The worst-case as well as the probability approach, however, have their drawbacks. The mathematics involved may be very complex and results achieved by these methods may often be of little use when solving practical instances of TSP. Statements concerning problems that almost certainly do not occur in practice (‘pathological’ problems, or problems with an ‘infinite’ number of cities) will often be irrelevant in connection with practical problem solving.

In this respect the third method, empirical analysis, seems more appropriate. Here the algorithm is executed on a number of test problems, and the results are evaluated, often in relation to optimal solutions. The test problems may be generated at random, or they may be constructed in a special way. If the test problems are representative for those problems the algorithm is supposed to solve, the computations are useful for evaluating the appropriateness of the algorithm.

The following section documents computational results of the modified LinKernighan algorithm. The results include the qualitative performance and the run time efficiency of the current implementation. Run times are measured in seconds on a 300 MHz G3 Power Macintosh.

The performance of the implementation has been evaluated on the following spectrum of problems:

(1) Symmetric problems (2) Asymmetric problems (3) Hamiltonian cycle problems (4) Pathological problems

Each problem has been solved by a number of independent runs. Each run consist of a series of trials, where in each trial a tour is determined by the modified Lin-Kernighan algorithm. The trials of a run are not independent, since edges belonging to the best tour of the current run are used to prune the search.

In the experiments the number of runs varies. In problems with less than 1000 cities the number of runs is 100. In larger problems the number of runs is 10.

The number of trials in each run is equal to the dimension of the problem (the number of cities). However, for problems where optimum is known, the current series of trials is stopped if the algorithm finds optimum.

# 6.1 Symmetric problems

TSPLIB [38] is a library, which is meant to provide researchers with a set of sample instances for the TSP (and related problems). TSPLIB is publicly available via FTP from softlib.rice.edu and contains problems from various sources and with various properties.

At present, instances of the following problem classes are available: symmetric traveling salesman problems, asymmetric traveling salesman problems, Hamiltonian cycle problems, sequential ordering problems, and capacitated vehicle routing problems. Information on the length of optimal tours, or lower and upper bounds for this length, is provided (if available).

More than 100 symmetric traveling salesman problems are included in the library, the largest being a problem with 85900 cities. The performance evaluation that follows is based on those problems for which the optimum is known. Today there are 100 problems of this type in the library, ranging from a problem with 14 cities to a problem with 7397 cities. The test results are reported in Table 6.1 and 6.2.

Table 6.1 displays the results from the subgradient optimization phase. The table gives the problem names along with the number of cities, the problem type, the optimal tour length, the lower bound, the gap between optimum and lower bound as a percentage of optimum, and the time in seconds used for subgradient optimization.

The problem type specifies how the distances are given. The entry MATRIX indicates that distances are given explicitly in matrix form (as full or triangular matrix). The other entry names refer to functions for computing the distances from city coordinates. The entries EUC_2D and CEIL_2D both indicates that distances are the 2-dimensional Euclidean distances (they differ in their rounding method). GEO indicates geographical distances on the Earth’s surface, and ATT indicates a special ‘pseudo-Euclidean’ distance function. All distances are integer numbers. See [38] for details.

Table 6.1 Determination of lower bounds (Part I)   

<table><tr><td></td><td></td><td>Type</td><td>Optimum</td><td>Lower bound</td><td>Gap</td><td>Time</td></tr><tr><td>Name</td><td>Cities</td><td></td><td></td><td>2565.8</td><td></td><td>0.7</td></tr><tr><td>a280</td><td>280</td><td>EUC_2D</td><td>2579 202310</td><td>201196.2</td><td>0.5 0.6</td><td>4.0</td></tr><tr><td>ali535</td><td>535</td><td>GEO ATT</td><td></td><td>10602.1</td><td>0.2</td><td>0.1</td></tr><tr><td>att48</td><td>48 532</td><td>ATT</td><td>10628 27686</td><td>27415.7</td><td>1.0</td><td>2.9</td></tr><tr><td>att532</td><td></td><td></td><td></td><td></td><td></td><td>0.0</td></tr><tr><td>bayg29</td><td>29</td><td>GEO</td><td>1610</td><td>1608.0 2013.3</td><td>0.1</td><td>0.0</td></tr><tr><td>bays29 berlin52</td><td>29 52</td><td>GEO EUC_2D</td><td>2020 7542</td><td>7542.0</td><td>0.3</td><td>0.1</td></tr><tr><td>bier127</td><td></td><td></td><td></td><td>117430.6</td><td>*0.0</td><td></td></tr><tr><td>brazil58</td><td>127 58</td><td>EUC_2D MATRIX</td><td>118282</td><td>25354.2</td><td>0.7</td><td>0.3</td></tr><tr><td></td><td></td><td></td><td>25395</td><td></td><td>0.2</td><td>0.1</td></tr><tr><td>brg180</td><td>180</td><td>MATRIX</td><td>1950</td><td>1949.3</td><td>0.0</td><td>0.3</td></tr><tr><td>burma14 ch130</td><td>14</td><td>GEO</td><td>3323</td><td>3223.0</td><td>*0.0</td><td>0.0</td></tr><tr><td></td><td>130</td><td>EUC_2D</td><td>6110</td><td>6074.6</td><td>0.6</td><td>0.2</td></tr><tr><td>ch150</td><td>150</td><td>EUC_2D</td><td>6528</td><td>6486.6 145672.9</td><td>0.6</td><td>0.3</td></tr><tr><td>d198</td><td>198</td><td>EUC_2D EUC_2D</td><td>15780</td><td></td><td>7.6</td><td>0.4</td></tr><tr><td>d493 d657</td><td>493 657</td><td>EUC_2D</td><td>35002</td><td>34822.4</td><td>0.5</td><td>2.5</td></tr><tr><td>d1291</td><td>1291</td><td></td><td>48912</td><td>48447.6</td><td>0.9</td><td>5.1</td></tr><tr><td>d1655</td><td>1655</td><td>EUC_2D</td><td>50801</td><td>50196.8</td><td>1.2</td><td>19.0</td></tr><tr><td></td><td>42</td><td>EUC_2D</td><td>62128</td><td>61453.3</td><td>1.1</td><td>47.0</td></tr><tr><td>dantzig42</td><td>1000</td><td>MATRIX</td><td>699</td><td>697.0 18339778.9</td><td>0.3</td><td>0.0</td></tr><tr><td>dsj1000</td><td>51</td><td>CEIL_2D EUC_2D</td><td>18659688</td><td></td><td>1.7</td><td>12.3</td></tr><tr><td>eil51 eil76</td><td>76</td><td>EUC_2D</td><td>426</td><td>422.4</td><td>0.8</td><td>0.1</td></tr><tr><td>eil101</td><td>101</td><td></td><td>538</td><td>536.9</td><td>0.2</td><td>0.1</td></tr><tr><td>fl417</td><td></td><td>EUC_2D</td><td>629</td><td>627.3</td><td>0.3</td><td>0.2</td></tr><tr><td>fl1400</td><td>417</td><td>EUC_2D</td><td>11861</td><td>11287.3</td><td>4.8</td><td>2.0</td></tr><tr><td></td><td>1400</td><td>EUC_2D</td><td>20127</td><td>19531.9</td><td>3.0</td><td>36.5</td></tr><tr><td>fl1577 fnl4461</td><td>1577</td><td>EUC_2D</td><td>22249</td><td>21459.3</td><td>3.5</td><td>45.2</td></tr><tr><td>fri26</td><td>4461</td><td>EUC 2D</td><td>182566</td><td>181566.1</td><td>0.5</td><td>332.7</td></tr><tr><td>gil262</td><td>26</td><td>MATRIX</td><td>937</td><td>937.0</td><td>*0.0</td><td>0.0</td></tr><tr><td>gr17</td><td>262</td><td>EUC_2D MATRIX</td><td>2378</td><td>2354.4</td><td>1.0</td><td>0.6</td></tr><tr><td>gr21</td><td>17 21</td><td>MATRIX</td><td>2085</td><td>2085.0</td><td>*0.0</td><td>0.0</td></tr><tr><td>gr24</td><td>24</td><td>MATRIX</td><td>2707</td><td>2707.0 1272.0</td><td>*0.0</td><td>0.0</td></tr><tr><td>gr48</td><td>48</td><td></td><td>1272</td><td></td><td>*0.0</td><td>0.0</td></tr><tr><td>gr96</td><td>96</td><td>MATRIX GEO</td><td>5046</td><td>4959.0 54569.5</td><td>1.7</td><td>0.1</td></tr><tr><td>gr120</td><td>120</td><td>MATRIX</td><td>55209</td><td></td><td>1.2</td><td>0.2</td></tr><tr><td>gr137</td><td>137</td><td></td><td>6942</td><td>6909.9 69113.1</td><td>0.5</td><td>0.2 0.4</td></tr><tr><td>gr202</td><td>202</td><td>GEO GEO</td><td>69853</td><td>40054.9</td><td>1.1</td><td></td></tr><tr><td>gr229</td><td>229</td><td>GEO</td><td>40160</td><td>133294.7</td><td>0.3</td><td>0.4 0.7</td></tr><tr><td>gr431</td><td>431</td><td></td><td>134602</td><td>170225.9</td><td>1.0</td><td></td></tr><tr><td>gr666</td><td></td><td>GEO</td><td>171414</td><td></td><td>0.7</td><td>2.0</td></tr><tr><td></td><td>666</td><td>GEO</td><td>294358</td><td>292479.3</td><td>0.6</td><td>4.8</td></tr><tr><td>hk48</td><td>48</td><td>MATRIX</td><td>11461</td><td>11444.0</td><td>0.1</td><td>0.0</td></tr><tr><td>kroA100</td><td>100</td><td>EUC_2D</td><td>21282</td><td>20936.5</td><td>1.6</td><td>0.1</td></tr><tr><td>kroB100</td><td>100</td><td>EUC_2D</td><td>22141</td><td>21831.7</td><td>1.4</td><td>0.1</td></tr><tr><td>kroC100</td><td>100</td><td>EUC_2D</td><td>20749</td><td>20472.5</td><td>1.3</td><td>0.2</td></tr><tr><td>kroD100</td><td>100</td><td>EUC_2D</td><td>21294</td><td>21141.5</td><td>0.7</td><td>0.2</td></tr><tr><td>kroE100</td><td>100</td><td>EUC_2D</td><td>22068</td><td>21799.4</td><td>1.2</td><td>0.2</td></tr><tr><td>kroA150</td><td>150</td><td>EUC2D</td><td>26524</td><td>26293.2</td><td>0.9</td><td>0.3</td></tr><tr><td>Name</td><td>Cities</td><td>Type</td><td>Optimum</td><td>Lower bound</td><td>Gap</td><td>Time</td></tr><tr><td>kroB150</td><td>150</td><td>EUC_2D</td><td>26130</td><td>25732.4</td><td>1.5</td><td>0.3</td></tr><tr><td>kroA200</td><td>200</td><td>EUC_2D</td><td>29368</td><td>29056.8</td><td>1.1</td><td>0.7</td></tr><tr><td>kroB200</td><td>200</td><td>EUC_2D</td><td>29437</td><td>29163.8</td><td>0.9</td><td>0.4</td></tr><tr><td>lin105</td><td>105</td><td>EUC_2D</td><td>14379</td><td>14370.5</td><td>0.1</td><td>0.2</td></tr><tr><td></td><td>318</td><td>EUC_2D</td><td>42029</td><td>41881.1</td><td>0.4</td><td>1.5</td></tr><tr><td>lin318 linhp318</td><td>318</td><td>EUC_2D</td><td>41345</td><td>41224.3</td><td>0.3</td><td>1.2</td></tr><tr><td>nrw1379</td><td>1379</td><td>EUC_2D</td><td>56638</td><td>56393.2</td><td>0.4</td><td>23.3</td></tr><tr><td>p654</td><td>654</td><td>EUC_2D</td><td>34643</td><td>33218.1</td><td>4.1</td><td>4.5</td></tr><tr><td>pa561</td><td>561</td><td>MATRIX</td><td>2763</td><td>2738.4</td><td>0.9</td><td>3.2</td></tr><tr><td>pcb442</td><td>442</td><td>EUC_2D</td><td>50778</td><td>50465.0</td><td>0.6</td><td>2.0</td></tr><tr><td>pcb1173</td><td>1173</td><td>EUC_2D</td><td>56892</td><td>56349.7</td><td>1.0</td><td>15.7</td></tr><tr><td>pcb3038</td><td>3038</td><td>EUC_2D</td><td>137694</td><td>136582.0</td><td></td><td>139.8</td></tr><tr><td>pla7397</td><td>7397</td><td>CEIL_2D</td><td>23260728</td><td>23113655.4</td><td>0.8 0.6</td><td>1065.6</td></tr><tr><td>pr76</td><td>76</td><td>EUC_2D</td><td>108159</td><td>105050.6</td><td>2.9</td><td>0.1</td></tr><tr><td>pr107</td><td>107</td><td>EUC_2D</td><td>44303</td><td>39991.5</td><td>9.7</td><td>0.2</td></tr><tr><td>pr124</td><td>124</td><td>EUC_ 2D</td><td>59030</td><td>58060.6</td><td>1.6</td><td>0.2</td></tr><tr><td>pr136</td><td>136</td><td>EUC_ 2D</td><td>96772</td><td>95859.2</td><td>0.9</td><td>0.3</td></tr><tr><td>pr144</td><td>144</td><td>EUC_ 2D</td><td>58537</td><td>57875.7</td><td>1.1</td><td>0.3</td></tr><tr><td>pr152</td><td>152</td><td>EUC_2D</td><td>73682</td><td>72166.3</td><td>2.1</td><td>0.5</td></tr><tr><td>pr226</td><td>226</td><td>EUC_ 2D</td><td>80369</td><td>79447.8</td><td>1.1</td><td>0.6</td></tr><tr><td>pr264</td><td>264</td><td>EUC_2D</td><td>49135</td><td>46756.3</td><td>4.8</td><td>0.6</td></tr><tr><td>pr299</td><td>299</td><td>EUC_2D</td><td>48191</td><td>47378.5</td><td>1.7</td><td>0.9</td></tr><tr><td>pr439</td><td>439</td><td>EUC 2D</td><td>107217</td><td>105816.3</td><td></td><td>2.0</td></tr><tr><td>pr1002</td><td>1002</td><td>EUC_2D</td><td>259045</td><td>256726.9</td><td>1.3</td><td>15.6</td></tr><tr><td>pr2392</td><td>2392</td><td>EUC_2D</td><td>378032</td><td>373488.5</td><td>0.9</td><td>84.6</td></tr><tr><td>rat99</td><td>99</td><td>EUC_2D</td><td></td><td>1206.0</td><td>1.2</td><td>0.2</td></tr><tr><td>rat195</td><td>195</td><td>EUC_ 2D</td><td>1211</td><td>2292.0</td><td>0.4</td><td>0.3</td></tr><tr><td>rat575</td><td>575</td><td>EUC_2D</td><td>2323</td><td>6723.4</td><td>1.3</td><td>3.2</td></tr><tr><td>rat783</td><td>783</td><td>EUC_2D</td><td>6773</td><td>8772.1</td><td>0.7</td><td>6.5</td></tr><tr><td>rd100</td><td>100</td><td>EUC_2D</td><td>8806</td><td>7897.1</td><td>0.4</td><td>0.1</td></tr><tr><td>rd400</td><td>400</td><td>EUC_2D</td><td>7910</td><td>15155.9</td><td>0.2</td><td>1.7</td></tr><tr><td>rl1304</td><td>1304</td><td>EUC_2D</td><td>15281</td><td>249079.2</td><td>0.8</td><td>19.9</td></tr><tr><td>rl1323</td><td>1323</td><td>EUC_2D</td><td>252948</td><td>265810.4</td><td>1.5</td><td>20.8</td></tr><tr><td>rl1889</td><td>1889</td><td>EUC_2D</td><td>270199</td><td>311305.0</td><td>1.6</td><td>49.6</td></tr><tr><td>si175</td><td>175</td><td>MATRIX</td><td>316536</td><td>21373.6</td><td>1.7</td><td>0.3</td></tr><tr><td>si535</td><td>535</td><td>MATRIX</td><td>21407 48450</td><td>48339.9</td><td>0.2 0.2</td><td>2.8</td></tr><tr><td>si1032</td><td>1032</td><td>MATRIX</td><td>92650</td><td>92434.4</td><td>0.2</td><td>12.6</td></tr><tr><td>st70</td><td>70</td><td>EUC_2D</td><td>675</td><td>670.9</td><td>0.6</td><td>0.1</td></tr><tr><td>swiss42</td><td>42</td><td>MATRIX</td><td></td><td>1271.8</td><td></td><td>0.0</td></tr><tr><td>ts225</td><td></td><td></td><td>1273</td><td></td><td>0.1</td><td></td></tr><tr><td></td><td>225</td><td>EUC_2D</td><td>126643</td><td>115604.6</td><td>8.7</td><td>0.5</td></tr><tr><td>tsp225</td><td>225</td><td>EUC_2D</td><td>3919</td><td>3880.3</td><td>1.0</td><td>0.5</td></tr><tr><td>u159 u574</td><td>159</td><td>EUC_2D</td><td>42080</td><td>41925.0</td><td>0.4</td><td>0.3</td></tr><tr><td></td><td>574</td><td>EUC_2D</td><td>36905</td><td>36710.3</td><td>0.5</td><td>3.3</td></tr><tr><td>u724</td><td>724</td><td>EUC_2D</td><td>41910</td><td>41648.9</td><td>0.6</td><td>5.2</td></tr><tr><td>u1060 u1432</td><td>1060 1432</td><td>EUC_2D EUC_2D</td><td>224094 152970</td><td>222626.4 152509.2</td><td>0.7 0.3</td><td>12.2</td></tr><tr><td>u1817</td><td>1817</td><td>EUC 2D</td><td></td><td>56681.7</td><td></td><td>25.7</td></tr><tr><td></td><td></td><td></td><td>57201</td><td></td><td>0.9</td><td>42.9</td></tr></table>

Table 6.1 Determination of lower bounds (Part II)

<table><tr><td>Name</td><td>Cities</td><td>Type</td><td>Optimum</td><td>Lower bound</td><td>Gap</td><td>Time</td></tr><tr><td>u2152</td><td>2152</td><td>EUC_2D</td><td>64253</td><td>63848.1</td><td>0.6</td><td>65.2</td></tr><tr><td>u2319</td><td>2319</td><td>EUC_2D</td><td>234256</td><td>234152.0</td><td>0.0</td><td>86.2</td></tr><tr><td>ulysses16</td><td>16</td><td>GEO</td><td>6859</td><td>6859.0</td><td>*0.0</td><td>0.0</td></tr><tr><td>ulysses22</td><td>22</td><td>GEO</td><td>7013</td><td>7013.0</td><td>*0.0</td><td>0.0</td></tr><tr><td>vm1084</td><td>1084</td><td>EUC_2D</td><td>239297</td><td>236144.7</td><td>1.3</td><td>12.7</td></tr><tr><td>vm1748</td><td>1748</td><td>EUC_2D</td><td>336556</td><td>332049.8</td><td>1.3</td><td>40.6</td></tr></table>

# Table 6.1 Determination of lower bounds (Part III)

The average gap between optimum and lower bound is $1 . 1 \%$ . For some of the small problems (berlin52, burma14, fri26, gr17, gr21, gr24, ulysses16 and ulysses22) the gap is zero, that is, optima are determined by subgradient optimization (marked with a \*).

Table 6.2 documents the performance of the search heuristics. The table gives the problem names along with the ratio of runs succeeding in finding the optimal solution, the minimum and average number of trials in a run, the minimum and average gap between the length of the best tour obtained and optimum as a percentage of optimum, and the minimum and average time in seconds per run.

For example, for the problem att532 of Padberg and Rinaldi [19] the optimal solution was determined in 98 runs out of 100. The minimum number of trials made to find optimum was 1. The average number of trials in a run was 66.2 (a run is stopped if the optimal solution is found, or the number of trials made equals the number of cities). The average gap between the length of the best tour obtained and optimum as a percentage of optimum was $0 . 0 0 1 \%$ . The maximum gap was $0 . 0 7 2 \%$ . Finally, the minimum and average CPU time used in a run was 0.2 and 3.6 seconds, respectively.

All instances were solved to optimality with the default parameter settings.

Table 6.2 Determination of solutions (Part I)   

<table><tr><td rowspan=1 colspan=1>Name</td><td rowspan=1 colspan=1>Success</td><td rowspan=1 colspan=1>Trials min</td><td rowspan=1 colspan=1>Trialsavg</td><td rowspan=1 colspan=1>Gapavg</td><td rowspan=1 colspan=1>Gapmax</td><td rowspan=1 colspan=3>Timemin</td><td rowspan=1 colspan=1>Timeavg</td></tr><tr><td rowspan=2 colspan=1>a280ali535</td><td rowspan=2 colspan=1>100/100100/100</td><td rowspan=2 colspan=1></td><td rowspan=2 colspan=1>1.08.0</td><td rowspan=1 colspan=1>0.000</td><td rowspan=2 colspan=1>0.0000.000</td><td rowspan=2 colspan=3>0.00.2</td><td rowspan=1 colspan=1>0.1</td></tr><tr><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.7</td></tr><tr><td rowspan=1 colspan=1>att48</td><td rowspan=1 colspan=1>100/100</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>1.0</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=3>0.0</td><td rowspan=1 colspan=1>0.0</td></tr><tr><td rowspan=1 colspan=1>att532</td><td rowspan=1 colspan=1>98/100</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>66.2</td><td rowspan=1 colspan=1>0.001</td><td rowspan=1 colspan=1>0.072</td><td rowspan=1 colspan=3>0.2</td><td rowspan=4 colspan=1>3.60.00.0</td></tr><tr><td rowspan=4 colspan=1>bayg29bays29berlin52</td><td rowspan=4 colspan=1>100/100100/100*1/0</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>1.0</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=2></td><td rowspan=1 colspan=1>0.0</td></tr><tr><td rowspan=2 colspan=1></td><td rowspan=2 colspan=1>1.0</td><td rowspan=2 colspan=1>0.000</td><td rowspan=2 colspan=1>0.000</td><td></td><td></td><td></td></tr><tr><td rowspan=1 colspan=3>0.0</td></tr><tr><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>1.0</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=3>0.0</td><td rowspan=1 colspan=1>0.0</td></tr><tr><td rowspan=1 colspan=1>bier127</td><td rowspan=1 colspan=1>100/100</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>1.1</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=3>0.0</td><td rowspan=1 colspan=1>0.0</td></tr><tr><td rowspan=4 colspan=1>brazil58brg180burma14ch130</td><td rowspan=4 colspan=1>100/100100/100*1/0100/100</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>1.0</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=3>0.0</td><td rowspan=1 colspan=1>0.0</td></tr><tr><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>3.3</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=3>0.0</td><td rowspan=1 colspan=1>0.0</td></tr><tr><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>1.0</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=3>0.0</td><td rowspan=1 colspan=1>0.0</td></tr><tr><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>3.0</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=3>0.0</td><td rowspan=1 colspan=1>0.1</td></tr><tr><td rowspan=1 colspan=1>ch150</td><td rowspan=1 colspan=1>62/100</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>62.9</td><td rowspan=1 colspan=1>0.023</td><td rowspan=1 colspan=1>0.077</td><td rowspan=1 colspan=3>0.0</td><td rowspan=1 colspan=1>0.4</td></tr><tr><td rowspan=2 colspan=1>d198d493</td><td rowspan=1 colspan=1>100/100</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>13.6</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=3>0.2</td><td rowspan=1 colspan=1>1.0</td></tr><tr><td rowspan=1 colspan=1>100/100</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>45.8</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=3>0.2</td><td rowspan=1 colspan=1>3.2</td></tr><tr><td rowspan=2 colspan=1>d657d1291</td><td rowspan=1 colspan=1>100/100</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>85.8</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=3>0.3</td><td rowspan=1 colspan=1>3.3</td></tr><tr><td rowspan=1 colspan=1>8/10</td><td rowspan=1 colspan=1>152</td><td rowspan=1 colspan=1>584.2</td><td rowspan=1 colspan=1>0.033</td><td rowspan=1 colspan=1>0.167</td><td rowspan=1 colspan=3>23.1</td><td rowspan=1 colspan=1>59.8</td></tr><tr><td rowspan=1 colspan=1>d1655</td><td rowspan=1 colspan=1>10/10</td><td rowspan=1 colspan=1>98</td><td rowspan=1 colspan=1>494.6</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=3>10.5</td><td rowspan=1 colspan=1>41.1</td></tr><tr><td rowspan=2 colspan=1>dantzig42dsj1000</td><td rowspan=1 colspan=1>100/100</td><td rowspan=1 colspan=1>1</td><td rowspan=1 colspan=1>1.0</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=3>0.0</td><td rowspan=1 colspan=1>0.0</td></tr><tr><td rowspan=1 colspan=1>7/10</td><td rowspan=1 colspan=1>90</td><td rowspan=1 colspan=1>514.1</td><td rowspan=1 colspan=1>0.035</td><td rowspan=1 colspan=1>0.116</td><td rowspan=1 colspan=3>13.1</td><td rowspan=1 colspan=1>55.1</td></tr><tr><td rowspan=1 colspan=1>eil51</td><td rowspan=1 colspan=1>100/100</td><td rowspan=1 colspan=1>1</td><td rowspan=1 colspan=1>1.0</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=3>0.0</td><td rowspan=1 colspan=1>0.0</td></tr><tr><td rowspan=3 colspan=1>eil76eil101fl417</td><td rowspan=1 colspan=1>100/100</td><td rowspan=1 colspan=1>1</td><td rowspan=1 colspan=1>1.0</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=3>0.0</td><td rowspan=1 colspan=1>0.0</td></tr><tr><td rowspan=1 colspan=1>100/100</td><td rowspan=1 colspan=1>1</td><td rowspan=1 colspan=1>1.0</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=3>0.0</td><td rowspan=1 colspan=1>0.0</td></tr><tr><td rowspan=1 colspan=1>88/100</td><td rowspan=1 colspan=1>1</td><td rowspan=1 colspan=1>64.2</td><td rowspan=1 colspan=1>0.052</td><td rowspan=1 colspan=1>0.430</td><td rowspan=1 colspan=3>1.2</td><td rowspan=1 colspan=1>12.4</td></tr><tr><td rowspan=1 colspan=1>f11400</td><td rowspan=1 colspan=1>1/10</td><td rowspan=1 colspan=1>13</td><td rowspan=1 colspan=1>1261.3</td><td rowspan=1 colspan=1>0.162</td><td rowspan=1 colspan=1>0.199</td><td rowspan=1 colspan=3>13.1</td><td rowspan=1 colspan=1>583.3</td></tr><tr><td rowspan=1 colspan=1>fl1577</td><td rowspan=1 colspan=1>2/10</td><td rowspan=1 colspan=1>134</td><td rowspan=1 colspan=1>1350.1</td><td rowspan=1 colspan=1>0.046</td><td rowspan=1 colspan=1>0.063</td><td rowspan=1 colspan=3>120.2</td><td rowspan=1 colspan=1>1097.5</td></tr><tr><td rowspan=1 colspan=1>fnl4461</td><td rowspan=1 colspan=1>6/10</td><td rowspan=1 colspan=1>665</td><td rowspan=1 colspan=1>2767.3</td><td rowspan=1 colspan=1>0.001</td><td rowspan=1 colspan=1>0.003</td><td rowspan=1 colspan=3>284.1</td><td rowspan=1 colspan=1>1097.3</td></tr><tr><td rowspan=5 colspan=1>fri26gil262gr17gr21gr24</td><td rowspan=1 colspan=1>100/100</td><td rowspan=1 colspan=1>1</td><td rowspan=1 colspan=1>1.0</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=3>0.0</td><td rowspan=1 colspan=1>0.0</td></tr><tr><td rowspan=1 colspan=1>100/100</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>13.3</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=3>0.1</td><td rowspan=1 colspan=1>0.4</td></tr><tr><td rowspan=1 colspan=1>*1/0</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>1.0</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=3>0.0</td><td rowspan=1 colspan=1>0.0</td></tr><tr><td rowspan=1 colspan=1>*1/0</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>1.0</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=3>0.0</td><td rowspan=1 colspan=1>0.0</td></tr><tr><td rowspan=1 colspan=1>100/100</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>1.0</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=3>0.0</td><td rowspan=1 colspan=1>0.0</td></tr><tr><td rowspan=7 colspan=1>gr48gr96gr120gr137gr202gr229gr431</td><td rowspan=1 colspan=1>100/100</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>1.0</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=3>0.0</td><td rowspan=1 colspan=1>0.0</td></tr><tr><td rowspan=1 colspan=1>100/100</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>10.2</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=3>0.0</td><td rowspan=1 colspan=1>0.1</td></tr><tr><td rowspan=1 colspan=1>100/100</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>1.0</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=3>0.0</td><td rowspan=1 colspan=1>0.0</td></tr><tr><td rowspan=1 colspan=1>100/100</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>1.0</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=3>0.0</td><td rowspan=1 colspan=1>0.0</td></tr><tr><td rowspan=1 colspan=1>100/100</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>1.0</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=3>0.0</td><td rowspan=1 colspan=1>0.1</td></tr><tr><td rowspan=1 colspan=1>12/100</td><td rowspan=1 colspan=1>6</td><td rowspan=1 colspan=1>216.6</td><td rowspan=1 colspan=1>0.009</td><td rowspan=1 colspan=1>0.010</td><td rowspan=1 colspan=3>0.2</td><td rowspan=1 colspan=1>1.7</td></tr><tr><td rowspan=1 colspan=1>17/100</td><td rowspan=1 colspan=1>81</td><td rowspan=1 colspan=1>401.4</td><td rowspan=1 colspan=1>0.053</td><td rowspan=1 colspan=1>0.077</td><td rowspan=1 colspan=3>4.4</td><td rowspan=1 colspan=1>13.1</td></tr><tr><td rowspan=1 colspan=1>gr666</td><td rowspan=1 colspan=1>30/100</td><td rowspan=1 colspan=1>25</td><td rowspan=1 colspan=1>531.9</td><td rowspan=1 colspan=1>0.026</td><td rowspan=1 colspan=1>0.040</td><td rowspan=1 colspan=3>2.0</td><td rowspan=1 colspan=1>18.8</td></tr><tr><td rowspan=2 colspan=1>hk48kroA100</td><td rowspan=1 colspan=1>100/100</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>1.0</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=3>0.0</td><td rowspan=1 colspan=1>0.0</td></tr><tr><td rowspan=1 colspan=1>100/100</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>1.0</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=3>0.0</td><td rowspan=1 colspan=1>0.0</td></tr><tr><td rowspan=1 colspan=1>kroB100</td><td rowspan=1 colspan=1>100/100</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>1.4</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=3>0.0</td><td rowspan=1 colspan=1>0.1</td></tr><tr><td rowspan=2 colspan=1>kroC100kroD100</td><td rowspan=2 colspan=1>100/100100/100</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>1.0</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=3>0.0</td><td rowspan=1 colspan=1>0.0</td></tr><tr><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>1.3</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=3>0.0</td><td rowspan=1 colspan=1>0.0</td></tr><tr><td rowspan=2 colspan=1>kroE100kroA150</td><td rowspan=2 colspan=1>99/100100/100</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>10.7</td><td rowspan=1 colspan=1>0.002</td><td rowspan=1 colspan=1>0.172</td><td rowspan=2 colspan=3>0.00.0</td><td rowspan=2 colspan=1>0.20.1</td></tr><tr><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>1.2</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td></tr></table>

<table><tr><td rowspan=1 colspan=4>Name</td><td rowspan=1 colspan=3>Success</td><td rowspan=1 colspan=1>Trialsmin</td><td rowspan=1 colspan=1>Trialsavg</td><td rowspan=1 colspan=1>Gapavg</td><td rowspan=1 colspan=1>Gapmax</td><td rowspan=1 colspan=1>Timemin</td><td rowspan=1 colspan=1>Timeavg</td></tr><tr><td rowspan=4 colspan=4>kroB150kroA200kroB200lin105</td><td rowspan=4 colspan=3>55/100100/100100/100100/100</td><td rowspan=2 colspan=1></td><td rowspan=2 colspan=1>97,72.1</td><td rowspan=1 colspan=1>0.003</td><td rowspan=1 colspan=1>0.008</td><td rowspan=1 colspan=1>0.1</td><td rowspan=1 colspan=1>0.8</td></tr><tr><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.1</td><td rowspan=1 colspan=1>0.2</td></tr><tr><td rowspan=2 colspan=1></td><td rowspan=1 colspan=1>2.0</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.0</td><td rowspan=1 colspan=1>0.1</td></tr><tr><td rowspan=1 colspan=1>1.0</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.0</td><td rowspan=1 colspan=1>0.0</td></tr><tr><td rowspan=8 colspan=4>lin318linhp318nrw1379p654pa561pcb442pcb1173pcb3038</td><td rowspan=8 colspan=3>71/100100/1003/10100/10099/10093/1008/109/10</td><td rowspan=2 colspan=1></td><td rowspan=1 colspan=1>154.1</td><td rowspan=1 colspan=1>0.076</td><td rowspan=1 colspan=1>0.271</td><td rowspan=1 colspan=1>0.1</td><td rowspan=1 colspan=1>2.0</td></tr><tr><td rowspan=1 colspan=1>2.4</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.0</td><td rowspan=1 colspan=1>0.1</td></tr><tr><td rowspan=1 colspan=1>414</td><td rowspan=1 colspan=1>1148.5</td><td rowspan=1 colspan=1>0.006</td><td rowspan=1 colspan=1>0.009</td><td rowspan=1 colspan=1>20.2</td><td rowspan=1 colspan=1>69.3</td></tr><tr><td rowspan=2 colspan=1></td><td rowspan=1 colspan=1>46.6</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>1.1</td><td rowspan=1 colspan=1>9.7</td></tr><tr><td rowspan=1 colspan=1>40.8</td><td rowspan=1 colspan=1>0.001</td><td rowspan=1 colspan=1>0.072</td><td rowspan=1 colspan=1>0.2</td><td rowspan=1 colspan=1>3.5</td></tr><tr><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>102.7</td><td rowspan=1 colspan=1>0.001</td><td rowspan=1 colspan=1>0.014</td><td rowspan=1 colspan=1>0.1</td><td rowspan=1 colspan=1>4.0</td></tr><tr><td rowspan=1 colspan=1>2</td><td rowspan=1 colspan=1>475.2</td><td rowspan=1 colspan=1>0.002</td><td rowspan=1 colspan=1>0.009</td><td rowspan=1 colspan=1>0.6</td><td rowspan=1 colspan=1>14.6</td></tr><tr><td rowspan=1 colspan=1>121</td><td rowspan=1 colspan=1>1084.7</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.004</td><td rowspan=1 colspan=1>39.1</td><td rowspan=1 colspan=1>323.7</td></tr><tr><td rowspan=2 colspan=4>pla7397pr76</td><td rowspan=1 colspan=3>7/10</td><td rowspan=1 colspan=1>1739</td><td rowspan=1 colspan=1>4588.4</td><td rowspan=1 colspan=1>0.001</td><td rowspan=1 colspan=1>0.004</td><td rowspan=1 colspan=1>4507.9</td><td rowspan=1 colspan=1>13022.0</td></tr><tr><td rowspan=1 colspan=3>100/100</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>1.0</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.0</td><td rowspan=1 colspan=1>0.1</td></tr><tr><td rowspan=3 colspan=4>pr107pr124pr136</td><td rowspan=1 colspan=3>100/100</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>1.0</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.0</td><td rowspan=1 colspan=1>0.0</td></tr><tr><td rowspan=1 colspan=3>100/100</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>1.4</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.0</td><td rowspan=1 colspan=1>0.1</td></tr><tr><td rowspan=1 colspan=3>100/100</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>1.0</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.1</td><td rowspan=1 colspan=1>0.2</td></tr><tr><td rowspan=2 colspan=4>pr144pr152</td><td rowspan=1 colspan=3>100/100</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>1.0</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.1</td><td rowspan=1 colspan=1>0.1</td></tr><tr><td rowspan=1 colspan=3>100/100</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>3.4</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.1</td><td rowspan=1 colspan=1>0.1</td></tr><tr><td rowspan=5 colspan=4>pr226pr264pr299pr439pr1002</td><td rowspan=1 colspan=3>100/100</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>1.0</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.1</td><td rowspan=1 colspan=1>0.1</td></tr><tr><td rowspan=1 colspan=3>100/100</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>7.5</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.2</td><td rowspan=1 colspan=1>0.5</td></tr><tr><td rowspan=1 colspan=3>100/100</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>4.5</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.3</td><td rowspan=1 colspan=1>0.8</td></tr><tr><td rowspan=1 colspan=3>98/100</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>72.8</td><td rowspan=1 colspan=1>0.001</td><td rowspan=1 colspan=1>0.041</td><td rowspan=1 colspan=1>0.1</td><td rowspan=1 colspan=1>1.6</td></tr><tr><td rowspan=1 colspan=3>10/10</td><td rowspan=1 colspan=1>38</td><td rowspan=1 colspan=1>215.1</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>1.0</td><td rowspan=1 colspan=1>3.4</td></tr><tr><td rowspan=2 colspan=4>pr2392rat99</td><td rowspan=1 colspan=3>10/10</td><td rowspan=1 colspan=1>37</td><td rowspan=1 colspan=1>396.6</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>8.7</td><td rowspan=1 colspan=1>54.5</td></tr><tr><td rowspan=1 colspan=3>100/100</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>1.0</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.0</td><td rowspan=1 colspan=1>0.0</td></tr><tr><td rowspan=2 colspan=4>rat195rat575</td><td rowspan=1 colspan=3>100/100</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>3.5</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.1</td><td rowspan=1 colspan=1>0.4</td></tr><tr><td rowspan=1 colspan=3>77/100</td><td rowspan=1 colspan=1>2</td><td rowspan=1 colspan=1>290.6</td><td rowspan=1 colspan=1>0.004</td><td rowspan=1 colspan=1>0.030</td><td rowspan=1 colspan=1>0.4</td><td rowspan=1 colspan=1>8.2</td></tr><tr><td rowspan=1 colspan=4>rat783</td><td rowspan=1 colspan=3>100/100</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>6.6</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.1</td><td rowspan=1 colspan=1>0.3</td></tr><tr><td rowspan=2 colspan=4>rd100rd400</td><td rowspan=1 colspan=3>100/100</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>1.1</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.0</td><td rowspan=1 colspan=1>0.0</td></tr><tr><td rowspan=1 colspan=3>99/100</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>51.0</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.020</td><td rowspan=1 colspan=1>0.1</td><td rowspan=1 colspan=1>1.1</td></tr><tr><td rowspan=1 colspan=4>rl1304</td><td rowspan=1 colspan=3>8/10</td><td rowspan=1 colspan=1>14</td><td rowspan=1 colspan=1>840.0</td><td rowspan=1 colspan=1>0.019</td><td rowspan=1 colspan=1>0.161</td><td rowspan=1 colspan=1>1.1</td><td rowspan=1 colspan=1>35.8</td></tr><tr><td rowspan=1 colspan=4>rl1323</td><td rowspan=1 colspan=3>1/10</td><td rowspan=1 colspan=1>244</td><td rowspan=1 colspan=1>1215.1</td><td rowspan=1 colspan=1>0.018</td><td rowspan=1 colspan=1>0.048</td><td rowspan=1 colspan=1>10.9</td><td rowspan=1 colspan=1>51.6</td></tr><tr><td rowspan=1 colspan=4>rl1889</td><td rowspan=1 colspan=3>4/10</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>1418.1</td><td rowspan=1 colspan=1>0.002</td><td rowspan=1 colspan=1>0.004</td><td rowspan=1 colspan=1>1.2</td><td rowspan=1 colspan=1>113.8</td></tr><tr><td rowspan=1 colspan=4>si175</td><td rowspan=1 colspan=3>100/100</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>6.8</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.1</td><td rowspan=1 colspan=1>0.2</td></tr><tr><td rowspan=1 colspan=4>si535</td><td rowspan=1 colspan=3>33/100</td><td rowspan=1 colspan=1>70</td><td rowspan=1 colspan=1>460.8</td><td rowspan=1 colspan=1>0.006</td><td rowspan=1 colspan=1>0.017</td><td rowspan=1 colspan=1>5.2</td><td rowspan=1 colspan=1>30.0</td></tr><tr><td rowspan=2 colspan=4>si1032st70</td><td rowspan=1 colspan=3>2/10</td><td rowspan=1 colspan=1>49</td><td rowspan=1 colspan=1>844.6</td><td rowspan=1 colspan=1>0.057</td><td rowspan=1 colspan=1>0.071</td><td rowspan=1 colspan=1>3.4</td><td rowspan=1 colspan=1>20.1</td></tr><tr><td rowspan=1 colspan=3>100/100</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>1.0</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.0</td><td rowspan=1 colspan=1>0.0</td></tr><tr><td rowspan=2 colspan=4>swiss42ts225</td><td rowspan=1 colspan=2>100/100</td><td rowspan=1 colspan=1>100/100</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>1.0</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.0</td><td rowspan=1 colspan=1>0.0</td></tr><tr><td rowspan=1 colspan=3>100/100</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>1.0</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.1</td><td rowspan=1 colspan=1>0.1</td></tr><tr><td rowspan=8 colspan=4>tsp225u159u574u724u1060u1432u1817</td><td rowspan=1 colspan=3>100/100</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>5.8</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.1</td><td rowspan=1 colspan=1>0.3</td></tr><tr><td rowspan=1 colspan=3>100/100</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>1.0</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.0</td><td rowspan=1 colspan=1>0.0</td></tr><tr><td rowspan=2 colspan=3>91/100</td><td rowspan=2 colspan=1></td><td rowspan=2 colspan=1>111.4</td><td rowspan=2 colspan=1>0.007</td><td rowspan=2 colspan=1>0.081</td><td rowspan=2 colspan=1>0.2</td><td rowspan=2 colspan=1>3.2</td></tr><tr><td rowspan=1 colspan=3>u724</td></tr><tr><td rowspan=1 colspan=2>24</td><td rowspan=1 colspan=3>98/100</td><td rowspan=1 colspan=1>4</td><td rowspan=1 colspan=1>162.5</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.005</td><td rowspan=1 colspan=1>0.6</td><td rowspan=1 colspan=1>6.8</td></tr><tr><td rowspan=1 colspan=3>9/10</td><td rowspan=1 colspan=1>2</td><td rowspan=1 colspan=1>305.9</td><td rowspan=1 colspan=1>0.000</td><td rowspan=1 colspan=1>0.003</td><td rowspan=1 colspan=1>1.6</td><td rowspan=1 colspan=1>38.0</td></tr><tr><td rowspan=2 colspan=3>10/102/10</td><td rowspan=2 colspan=1>3905</td><td rowspan=2 colspan=1>59.91707.8</td><td rowspan=1 colspan=1>0.000</td><td rowspan=2 colspan=1>0.0000.124</td><td rowspan=2 colspan=1>0.8199.6</td><td rowspan=2 colspan=1>8.0252.9</td></tr><tr><td rowspan=1 colspan=1>0.078</td></tr></table>

Table 6.2 Determination of solutions (Part II)

<table><tr><td>Name</td><td>Success</td><td>Trials</td><td>Trialsavg</td><td>Gapavg</td><td>Gapmax</td><td>Timemin</td><td>Timeavg</td></tr><tr><td>u2152</td><td>5/10</td><td>491</td><td>1706.5</td><td>0.029</td><td>0.089</td><td>85.0</td><td>274.2</td></tr><tr><td>u2319</td><td>10/10</td><td>1</td><td>3.2</td><td>0.000</td><td>0.000</td><td>0.5</td><td>2.6</td></tr><tr><td>ulysses16</td><td>*1/0</td><td></td><td>1.0</td><td>0.000</td><td>0.000</td><td>0.0</td><td>0.0</td></tr><tr><td>ulysses22</td><td>*1/0</td><td>1</td><td>1.0</td><td>0.000</td><td>0.000</td><td>0.0</td><td>0.0</td></tr><tr><td>vm1084</td><td>7/10</td><td>8</td><td>425.2</td><td>0.007</td><td>0.022</td><td>1.9</td><td>28.6</td></tr><tr><td>vm1748</td><td>4/10</td><td>65</td><td>1269.6</td><td>0.023</td><td>0.054</td><td>7.3</td><td>1016.1</td></tr></table>

# Table 6.2 Determination of solutions (Part III)

In addition to these problems, TSPLIB contains 11 symmetric problems for which no optimum solutions are known today. The dimension of these problems varies from 2103 to 85900 cities.

Table 6.3 lists for each of these problems the currently best known lower and upper bound (published in TSPLIB, October 1997).

<table><tr><td>Name</td><td>Cities</td><td>Type</td><td>Lower bound</td><td>Upper bound</td></tr><tr><td>brd14051</td><td>14051</td><td>EUC_2D</td><td>469272</td><td>469445</td></tr><tr><td>d2103</td><td>2103</td><td>EUC_2D</td><td>80099</td><td>80450</td></tr><tr><td>d15112</td><td>15112</td><td>EUC_2D</td><td>1572810</td><td>1573152</td></tr><tr><td>d18512</td><td>18512</td><td>EUC 2D</td><td>645075</td><td>645300</td></tr><tr><td>fl3795</td><td>3795</td><td>EUC 2D</td><td>28724</td><td>28772</td></tr><tr><td>pla33810</td><td>33810</td><td>CEIL 2D</td><td>65960739</td><td>66116530</td></tr><tr><td>pla85900</td><td>85900</td><td>CEIL2D</td><td>142244225</td><td>142482068</td></tr><tr><td>rl5915</td><td>5915</td><td>EUC 2D</td><td>565277</td><td>565530</td></tr><tr><td>rl5934</td><td>5934</td><td>EUC_2D</td><td>555579</td><td>556045</td></tr><tr><td>rl11849</td><td>11849</td><td>EUC_2D</td><td>922859</td><td>923368</td></tr><tr><td>usa13509</td><td>13509</td><td>EUC_2D</td><td>19981013</td><td>19982889</td></tr></table>

# Table 6.3 Problems in TSPLIB with unknown optimal solutions

When the new algorithm was executed on these problems, it found tour lengths equal to the best known upper bounds for 4 of the problems (d2103, fl3795, rl5915 and rl5934).

However, for the remaining 7 problems, the algorithm was able find tours shorter than the best known upper bounds. These new upper bounds are listed in Table 6.4.

Table 6.4 Improved upper bounds   

<table><tr><td rowspan=1 colspan=1>Name</td><td rowspan=1 colspan=1>New upper bound</td></tr><tr><td rowspan=3 colspan=1>brd14051d15112d18512</td><td rowspan=1 colspan=1>469395</td></tr><tr><td rowspan=1 colspan=1>1573089</td></tr><tr><td rowspan=1 colspan=1>645250</td></tr><tr><td rowspan=4 colspan=1>pla33810pla85900rl11849usa13509</td><td rowspan=1 colspan=1>66060236</td></tr><tr><td rowspan=1 colspan=1>142416327</td></tr><tr><td rowspan=1 colspan=1>923307</td></tr><tr><td rowspan=1 colspan=1>19982859</td></tr></table>

The new upper bound for the largest of these problems, pla85900, was found using two weeks of CPU time.

It is difficult to predict the running time needed to solve a given problem with the algorithm. As can be seen from Table 6.2, the size alone is not enough. One problem may require much more running time than a larger problem.

However, some guidelines may be given. Random problems may be used to provide estimates of running times. By solving randomly generated problems of different dimensions and measuring the time used to solve these problems, it is possible to get an idea of how running time grows as a function of problem dimension.

An algorithm for randomly generating traveling salesman problem with known optimal tours, described by Arthur and Frendewey [48], was used for this purpose. Figure 6.1 and 6.2 show total running times (in seconds) for solving symmetric with problems generated by this algorithm. The dimension varies from 50 to 1000 cities. The following parameter values have been chosen: $\rho = \ 0 . 1$ , $\sigma = \ 0 . 2 5$ (both suggested by Arthur and Frendewey), and $\mathrm { R } = \mathrm { n }$ , where n is the dimension of the problem. See [48] for details.

![](images/115d8d4db2d256cf07da70dd7867214cb58135c8a3451ba09ad88600a65ed761.jpg)  
Figure 6.1 Run time as a function of problem dimension (non-metric problems)

The problems used to produce Figure 6.1 are not required to satisfy the triangle inequality. These problems are very simple for the algorithm. For all problems, optimum was found in only one trial. The curve depicts the function $\mathrm { f ( n ) } = 8 . 6 \mathrm { e } ^ { - 6 } { * \mathrm { n } ^ { 2 . 2 } }$ (correlation coefficient: 0.997).

Figure 6.2 depicts total running time as a function of dimension for randomly generated problems satisfying the triangle inequality. These problems seem to be harder to solve (probably due to a smaller diversity in the distances). However, the optimum for these problems was also found in one trial only. The curve depicts the function $\mathrm { f ( n ) } = 3 . 2 \mathrm { e } ^ { - 5 } { * \mathrm { n } ^ { 2 . 2 } }$ (correlation coefficient : 0.944).

![](images/07727745cbe0641b8375a3ef44bc8ee37463dd296ef328e00f566de249105f37.jpg)  
Figure 6.2 Run time as a function of problem dimension (metric problems)

These results indicate that the average running time of the algorithm is approximately $\mathrm { O } ( \mathrm { n } ^ { 2 . 2 } )$ .

Another method often used in studying the average performance of TSP heuristics is to solve problem instances consisting of random points within a rectangle under the Euclidean metric. The instances are solved for increasing values of n and compared to the theoretical value for the expected length of an optimal tour $\mathrm { ( L _ { o p t } ) }$ . A well-known formula is $\mathrm { L _ { o p t } ( n , A ) = \mathrm { \ddot { K } \sqrt { n } \sqrt { A } } }$ when n cities are distributed uniformly randomly over a rectangular area of A units [49]. That is, the ratio of the optimal tour length to n A approaches a constant $\mathrm { K }$ for $\Nu \to \infty$ . Experiments of Johnson, McGeoch and Rothenberg [50] suggest that K is approximated by 0.7124.

Figure 6.3 shows the results obtained when the modified Lin-Kernighan algorithm was used to solve such problems on a $1 0 ^ { 4 } \mathrm { x } 1 0 ^ { 4 }$ square for n ranging from 500 to 5000 and n increasing by 500. The figure depicts the tour length divided by $\surd \mathrm { n } ^ { * } 1 0 ^ { 4 }$ . These results are consistent with the estimate $\mathrm { K } \approx 0 . 7 1 \bar { 2 } 4$ for large n.

![](images/e418fa278b490eb7e6303192ef66c30f082a077d3611f43b28b8ec795cfb68a4.jpg)  
Figure 6.3 Solutions of random Euclidean problems on a square

![](images/058e348bda775e40d86401b9269ff7019da77e519417237e0bfba6524e5ede13.jpg)  
Figure 6.4 shows the total running time in seconds to find the best (local optimal) tour as a function of problem dimension. The curve depicts the function $\mathrm { f ( n ) } = 2 . 9 \mathrm { e } ^ { - 5 } \ast \mathrm { n } ^ { 2 . 2 }$ (with correlation coefficient 0.968).   
Figure 6.4 Run time as a function of problem dimension

# 6.2 Asymmetric problems

The implemented algorithm is primarily intended for solving symmetric TSPs. However, any asymmetric problem may be transformed into a symmetric problem and therefore be solved by the algorithm.

The transformation method of Jonker and Volgenant [51] transforms a asymmetric problem with n nodes into a problem 2n nodes. Let $\mathrm { C = ( c _ { i j } ) }$ denote the nxn cost matrix of the asymmetric problem. Then let $\mathrm { C } ^ { \mathrm { 3 } } = ( \mathrm { c } _ { \mathrm { \scriptsize ~ i j } } ^ { \mathrm { 3 } } )$ be the $2 \mathrm { n x } 2 \mathrm { n }$ symmetric matrix computed as follows:

$$
\begin{array} { r } { { \bf c } _ { \mathrm { \tiny ~ n + i , j } } ^ { \prime } = { \bf c } _ { \mathrm { \tiny ~ j , n + i } } ^ { \prime } = { \bf c } _ { \mathrm { i , j } } \quad \mathrm { f o r ~ i = 1 , ~ } 2 , . . . , \mathrm { \tiny ~ n , } } \\ { \mathrm { \tiny ~ { \vec { ~ } j = 1 , ~ } 2 , ~ . . . , ~ n , } } \\ { \mathrm { a n d ~ i \not = j ~ } } \end{array}
$$

$$
\begin{array} { l l } { { \mathfrak { c } } _ { \mathrm { \tiny ~ n + i , i } } ^ { \prime } = { \mathfrak { c } } _ { \mathrm { \tiny ~ i , n + i } } ^ { \prime } = - { \textnormal M } } & { \mathrm { f o r ~ i = 1 , 2 , ~ . . . , ~ n ~ } } \\ { { \mathfrak { c } } _ { \mathrm { \tiny ~ i , j } } ^ { \prime } = { \textnormal M } } & { \mathrm { o t h e r w i s e } } \end{array}
$$

where $\mathbf { M }$ is a sufficiently large number, e.g., $\mathrm { M } = \mathrm { m a x } ( \mathrm { c _ { i j } } )$

It is easy to prove that any optimal solution of the new symmetric problem corresponds to an optimal solution of the original asymmetric problem.

An obvious disadvantage of the transformation is that it doubles the size of the problem. Therefore, in practice it is more advantageous to use algorithms dedicated for solving asymmetric problems. However, as can been seen from Table 6.5 the performance of the modified Lin-Kernighan algorithm for asymmetric problems is quite impressive. The optimum was obtained for all asymmetric problems of TSPLIB. The largest of these problems, rbg443, has 443 nodes (thus, the transformed problem has 886 nodes).

The problems prefixed with ft have size equal to their suffix number plus 1.

<table><tr><td>Name</td><td>Success</td><td>Trials min</td><td>Trialsavg</td><td>Gapavg</td><td>Gapmax</td><td>Timemin</td><td>Timeavg</td></tr><tr><td>br17</td><td>100/100</td><td></td><td>1.0</td><td>0.000</td><td>0.000</td><td>0.0</td><td>0.0</td></tr><tr><td>ft53</td><td>100/100</td><td></td><td>8.0</td><td>0.000</td><td>0.000</td><td>0.0</td><td>0.0</td></tr><tr><td>ft70</td><td>100/100</td><td></td><td>1.6</td><td>0.000</td><td>0.000</td><td>0.0</td><td>0.0</td></tr><tr><td>ftv33</td><td>100/100</td><td></td><td>1.0</td><td>0.000</td><td>0.000</td><td>0.0</td><td>0.0</td></tr><tr><td>ftv35</td><td>47/100</td><td></td><td>43.6</td><td>0.072</td><td>0.136</td><td>0.0</td><td>0.1</td></tr><tr><td>ftv38</td><td>53/100</td><td></td><td>40.3</td><td>0.061</td><td>0.131</td><td>0.0</td><td>0.1</td></tr><tr><td>ftv44</td><td>100/100</td><td></td><td>2.8</td><td>0.000</td><td>0.000</td><td>0.0</td><td>0.0</td></tr><tr><td>ftv47</td><td>100/100</td><td></td><td>1.5</td><td>0.000</td><td>0.000</td><td>0.0</td><td>0.0</td></tr><tr><td>ftv55</td><td>100/100</td><td></td><td>3.5</td><td>0.000</td><td>0.000</td><td>0.0</td><td>0.0</td></tr><tr><td>ftv64</td><td>100/100</td><td></td><td>3.6</td><td>0.000</td><td>0.000</td><td>0.0</td><td>0.0</td></tr><tr><td>ftv70</td><td>100/100</td><td></td><td>3.6</td><td>0.000</td><td>0.000</td><td>0.0</td><td>0.0</td></tr><tr><td>ftv170</td><td>88/100</td><td></td><td>119.7</td><td>0.039</td><td>0.327</td><td>0.0</td><td>1.0</td></tr><tr><td>kro124p</td><td>95/100</td><td></td><td>24.6</td><td>0.002</td><td>0.030</td><td>0.0</td><td>0.1</td></tr><tr><td>p43</td><td>21/100</td><td></td><td>72.2</td><td>0.014</td><td>0.018</td><td>0.0</td><td>0.5</td></tr><tr><td>rbg323</td><td>97/100</td><td>17</td><td>116.3</td><td>0.018</td><td>0.679</td><td>1.9</td><td>8.5</td></tr><tr><td>rbg358</td><td>99/100</td><td>19</td><td>96.8</td><td>0.060</td><td>6.019</td><td>2.5</td><td>8.3</td></tr><tr><td>rbg403</td><td>100/100</td><td>19</td><td>87.5</td><td>0.000</td><td>0.000</td><td>2.6</td><td>11.3</td></tr><tr><td>rbg443</td><td>100/100</td><td>18</td><td>105.2</td><td>0.000</td><td>0.000</td><td>2.5</td><td>12.6</td></tr><tr><td>ry48p</td><td>99/100</td><td>1</td><td>9.8</td><td>0.002</td><td>0.166</td><td>0.0</td><td>0.0</td></tr></table>

# Table 6.5 Performance for asymmetric problems

# 6.3 Hamiltonian cycle problems

The Hamiltonian cycle problem is the problem of deciding if a given undirected graph contains a cycle. The problem can be answered by solving a symmetric TSP in the complete graph where all edges of G have cost 0 and all other edges have a positive cost. Then G contains a Hamiltonian cycle if and only if an optimal tour has cost 0.

At present TSPLIB includes 9 Hamiltonian cycle problems ranging in size from 1000 to 5000 nodes. Every instance of the problems contains a Hamiltonian cycle. Table 6.6 shows the excellent performance of the modified LinKernighan algorithm for these problem instances.

<table><tr><td>Name</td><td>Success</td><td>Trials min</td><td>Trialsavg</td><td>Gapavg</td><td>Gapmax</td><td>Timemin</td><td>Timeavg</td></tr><tr><td>alb1000</td><td>10/10</td><td>1</td><td>1.0</td><td>0.000</td><td>0.000</td><td>0.0</td><td>0.1</td></tr><tr><td>alb2000</td><td>10/10</td><td></td><td>1.0</td><td>0.000</td><td>0.000</td><td>0.1</td><td>0.1</td></tr><tr><td>alb3000a</td><td>10/10</td><td></td><td>1.0</td><td>0.000</td><td>0.000</td><td>0.1</td><td>0.1</td></tr><tr><td>alb3000b</td><td>10/10</td><td></td><td>1.0</td><td>0.000</td><td>0.000</td><td>0.1</td><td>0.1</td></tr><tr><td>alb3000c</td><td>10/10</td><td></td><td>1.0</td><td>0.000</td><td>0.000</td><td>0.1</td><td>0.1</td></tr><tr><td>alb3000d</td><td>10/10</td><td></td><td>1.0</td><td>0.000</td><td>0.000</td><td>0.1</td><td>0.1</td></tr><tr><td>alb3000e</td><td>10/10</td><td></td><td>1.0</td><td>0.000</td><td>0.000</td><td>0.1</td><td>0.1</td></tr><tr><td>alb4000</td><td>10/10</td><td></td><td>1.0</td><td>0.000</td><td>0.000</td><td>0.1</td><td>0.1</td></tr><tr><td>alb5000</td><td>10/10</td><td></td><td>1.0</td><td>0.000</td><td>0.000</td><td>0.2</td><td>0.2</td></tr></table>

# Table 6.6 Performance for the Hamiltonian cycle problems of TSPLIB

An interesting special Hamilton cycle problem is the so-called knight’s-tour problem. A knight is to be moved around on a chessboard in such a way that all 64 squares are visited exactly once and the moves taken constitute a round trip on the board. Figure 6.5 depicts one solution of the problem. The two first moves are shown with arrows.

Figure 6.5 One solution of the knight’s-tour problem   

<table><tr><td rowspan=1 colspan=1>16</td><td rowspan=1 colspan=1>31</td><td rowspan=1 colspan=1>14</td><td rowspan=1 colspan=1>21</td><td rowspan=1 colspan=1>18</td><td rowspan=1 colspan=1>→</td><td rowspan=1 colspan=1>50</td><td rowspan=1 colspan=1>3</td></tr><tr><td rowspan=1 colspan=1>13</td><td rowspan=1 colspan=1>6</td><td rowspan=1 colspan=1>17</td><td rowspan=1 colspan=1>30</td><td rowspan=1 colspan=1>23</td><td rowspan=1 colspan=1>4</td><td rowspan=1 colspan=1>19</td><td rowspan=1 colspan=1>V64</td></tr><tr><td rowspan=1 colspan=1>32</td><td rowspan=1 colspan=1>15</td><td rowspan=1 colspan=1>22</td><td rowspan=1 colspan=1>5</td><td rowspan=1 colspan=1>20</td><td rowspan=1 colspan=1>49</td><td rowspan=1 colspan=1>2</td><td rowspan=1 colspan=1>57</td></tr><tr><td rowspan=1 colspan=1>7</td><td rowspan=1 colspan=1>12</td><td rowspan=1 colspan=1>29</td><td rowspan=1 colspan=1>24</td><td rowspan=1 colspan=1>43</td><td rowspan=1 colspan=1>52</td><td rowspan=1 colspan=1>63</td><td rowspan=1 colspan=1>56</td></tr><tr><td rowspan=1 colspan=1>28</td><td rowspan=1 colspan=1>33</td><td rowspan=1 colspan=1>8</td><td rowspan=1 colspan=1>37</td><td rowspan=1 colspan=1>48</td><td rowspan=1 colspan=1>55</td><td rowspan=1 colspan=1>44</td><td rowspan=1 colspan=1>53</td></tr><tr><td rowspan=1 colspan=1>9</td><td rowspan=1 colspan=1>38</td><td rowspan=1 colspan=1>11</td><td rowspan=1 colspan=1>42</td><td rowspan=1 colspan=1>25</td><td rowspan=1 colspan=1>62</td><td rowspan=1 colspan=1>57</td><td rowspan=1 colspan=1>60</td></tr><tr><td rowspan=1 colspan=1>34</td><td rowspan=1 colspan=1>27</td><td rowspan=1 colspan=1>40</td><td rowspan=1 colspan=1>47</td><td rowspan=1 colspan=1>36</td><td rowspan=1 colspan=1>59</td><td rowspan=1 colspan=1>54</td><td rowspan=1 colspan=1>45</td></tr><tr><td rowspan=1 colspan=1>39</td><td rowspan=1 colspan=1>10</td><td rowspan=1 colspan=1>35</td><td rowspan=1 colspan=1>26</td><td rowspan=1 colspan=1>41</td><td rowspan=1 colspan=1>46</td><td rowspan=1 colspan=1>61</td><td rowspan=1 colspan=1>58</td></tr></table>

The problem is an instance of the general “leaper” problem: “Can a $\{ \boldsymbol { \mathrm { r } } , \boldsymbol { \mathrm { s } } \}$ - leaper, starting at any square of a mxn board, visit each square exactly once and return to its starting square” [52]. The knight’s-tour problem is the $^ { \{ 1 , 2 \} }$ -leaper problem on a 8x8 board.

Table 6.7 shows the performance statistics for a few leaper problems. A small C-program, included in TSPLIB, was used for generating the leaper graphs. Edges belonging to the graph cost 0, and the remaining edges cost 1.

<table><tr><td>Problem</td><td>Success</td><td>Trials min</td><td>Trialsavg</td><td>Gapavg</td><td>Gapmax</td><td>Timemin</td><td>Timeavg</td></tr><tr><td>{1,2}, 8x8</td><td>100/100</td><td>1</td><td>1.0</td><td>0.000</td><td>0.000</td><td>0.0</td><td>0.0</td></tr><tr><td>{1,2}, 10x10</td><td>100/100</td><td>1</td><td>1.0</td><td>0.000</td><td>0.000</td><td>0.0</td><td>0.0</td></tr><tr><td>{1,2},20x20</td><td>100/100</td><td>1</td><td>2.1</td><td>0.000</td><td>0.000</td><td>0.0</td><td>0.0</td></tr><tr><td>{7,8}, 15x106</td><td>10/10</td><td>4</td><td>8.6</td><td>0.000</td><td>0.000</td><td>0.3</td><td>0.7</td></tr><tr><td>{6,7}13x76</td><td>100/100</td><td></td><td>1.1</td><td>0.000</td><td>0.000</td><td>0.3</td><td>0.5</td></tr></table>

# Table 6.7 Performance for leaper problems (Variant 1)

The last of these problems has an optimal tour length of 18. All the other problems contain a Hamiltonian cycle, i.e., their optimum tour length is 0.

Table 6.8 shows the performance for the same problems, but now the edges of the leaper graph cost 100, and the remaining edges cost 101. Lin and Kernighan observed that knight’s-tour problems with these edge costs were hard to solve for their algorithm [1].

<table><tr><td>Problem</td><td>Success</td><td>Trials min</td><td>Trialsavg</td><td>Gapavg</td><td>Gapmax</td><td>Timemin</td><td>Timeavg</td></tr><tr><td>{1,2}, 8x8</td><td>100/100</td><td>1</td><td>1.0</td><td>0.000</td><td>0.000</td><td>0.0</td><td>0.0</td></tr><tr><td>{1,2}, 10x10</td><td>100/100</td><td></td><td>1.0</td><td>0.000</td><td>0.000</td><td>0.0</td><td>0.0</td></tr><tr><td>{1,2}, 20x20</td><td>100/100</td><td></td><td>1.1</td><td>0.000</td><td>0.000</td><td>0.0</td><td>0.0</td></tr><tr><td>{7,8}, 15x106</td><td>10/10</td><td>3</td><td>10.0</td><td>0.000</td><td>0.000</td><td>0.4</td><td>1.0</td></tr><tr><td>{6,7},13x76</td><td>100/100</td><td></td><td>1.1</td><td>0.000</td><td>0.000</td><td>0.4</td><td>0.7</td></tr></table>

# Table 6.8 Performance for leaper problems (Variant 2)

As seen the new implementation is almost unaffected.

# 6.4 Pathological problems

The Lin-Kernighan algorithm is not always as effective as it seems to be with “random” or “typical” problems. Papadimitriou and Steiglitz [53] have constructed a special class of instances of the TSP for which local search algorithms, such as the Lin-Kernighan algorithm, appears to be very ineffective. Papadimitriou and Steiglitz denote this class of problems as ‘perverse’.

Each problem has ${ \mathrm { n } } = 8 { \mathrm { k } }$ nodes. There is exactly one optimal tour with cost n, and there are $2 ^ { \mathrm { k - 1 } } ( \mathrm { k - 1 } ) .$ ! tours that are next best, have arbitrary large cost, and cannot be improved by changing fewer than $3 \mathrm { k }$ edges. See [53] for a precise description of the constructed problems.

The difficulty of the problem class is illustrated in Table 6.9 showing the performance of the algorithm when subgradient optimization is left out. Note the results for the cases ${ \mathrm { k } } = 3$ and ${ \mathrm { k } } \bar { = } 5$ . Here the optimum was frequently found, whereas the implementation of the Lin-Kernighan algorithm by Papadimitriou and Steiglitz was unable to discover the optimum even once.

<table><tr><td>k</td><td>n</td><td>Success</td><td>Trials min</td><td>Trialsavg</td><td>Gapavg</td><td>Gapmax</td><td>Timemin</td><td>Timeavg</td></tr><tr><td>3</td><td></td><td>46/100</td><td></td><td>14.9</td><td>2479.5</td><td>8291.7</td><td>0.0</td><td>0.0</td></tr><tr><td></td><td></td><td>55/100</td><td></td><td>17.4</td><td>1732.8</td><td>6209.4</td><td>0.0</td><td>0.0</td></tr><tr><td></td><td></td><td>48/100</td><td></td><td>24.1</td><td>1430.4</td><td>4960.0</td><td>0.0</td><td>0.0</td></tr><tr><td></td><td>2</td><td>53/100</td><td></td><td>26.6</td><td>1045.1</td><td>4127.1</td><td>0.0</td><td>0.0</td></tr><tr><td>4</td><td>56</td><td>32/100</td><td></td><td>41.2</td><td>1368.2</td><td>3532.1</td><td>0.0</td><td>0.0</td></tr><tr><td>8</td><td>64</td><td>41/100</td><td></td><td>41.2</td><td>1040.2</td><td>3085.9</td><td>0.0</td><td>0.0</td></tr><tr><td>9</td><td>72</td><td>1/100</td><td></td><td>71.3</td><td>1574.1</td><td>2738.9</td><td>0.0</td><td>0.1</td></tr><tr><td>10</td><td>80</td><td>2/100</td><td></td><td>78.6</td><td>1700.5</td><td>4958.8</td><td>0.0</td><td>0.2</td></tr></table>

# Table 6.9 Performance for perverse problems (without subgradient optimization)

However, all problems are solved without any search, if subgradient optimization is used, provided that the initial period is sufficiently large $( 5 ^ { * } \mathrm { D I M E N S I O N } )$ . Table 6.10 shows the time (in seconds) to find the optimal solutions by subgradient optimization.

Table 6.10 Time to find optimal solutions for perverse problems (with subgradient optimization)   

<table><tr><td rowspan=1 colspan=1>k</td><td rowspan=1 colspan=1>n</td><td rowspan=1 colspan=1>Time</td></tr><tr><td rowspan=3 colspan=1>3</td><td rowspan=1 colspan=1>24</td><td rowspan=1 colspan=1>0.0</td></tr><tr><td rowspan=1 colspan=1>32</td><td rowspan=1 colspan=1>0.0</td></tr><tr><td rowspan=1 colspan=1>40</td><td rowspan=1 colspan=1>0.0</td></tr><tr><td rowspan=1 colspan=1>6</td><td rowspan=1 colspan=1>48</td><td rowspan=1 colspan=1>0.1</td></tr><tr><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>56</td><td rowspan=1 colspan=1>0.1</td></tr><tr><td rowspan=1 colspan=1>8</td><td rowspan=1 colspan=1>64</td><td rowspan=1 colspan=1>0.1</td></tr><tr><td rowspan=1 colspan=1>9</td><td rowspan=1 colspan=1>72</td><td rowspan=1 colspan=1>0.1</td></tr><tr><td rowspan=1 colspan=1>10</td><td rowspan=1 colspan=1>80</td><td rowspan=1 colspan=1>0.2</td></tr></table>

# 7. Conclusions

This report has described a modified Lin-Kernighan algorithm and its implementation. In the development of the algorithm great emphasis was put on achieving high quality solutions, preferably optimal solutions, in a reasonable short time.

Achieving simplicity was of minor concern here. In comparison, the modified Lin-Kernighan algorithm of Mak and Morton [54] has a very simple algorithmic structure. However, this simplicity has been achieved with the expense of a reduced ability to find optimal solutions. Their algorithm does not even guarantee 2-opt optimality.

Computational experiments have shown that the new algorithm is highly effective. An optimal solution was obtained for all problems with a known optimum. This is remarkable, considering that the modified algorithm does not employ backtracking.

The running times were satisfactory for all test problems. However, since running time is approximately ${ \mathrm { O } } ( { \mathrm { n } } ^ { 2 \cdot 2 } )$ , it may be impractical to solve very large problems. The current implementation seems to be feasible for problems with fewer than 100,000 cities (this depends, of course, of the available computer resources).

When distances are implicitly given, space requirements are O(n). Thus, the space required for geometrical problems is linear. For such problems, not space, but run time, will usually be the limiting factor.

The effectiveness of the algorithm is primarily achieved through an efficient search strategy. The search is based on 5-opt moves restricted by carefully chosen candidate sets. The $\mathfrak { a }$ -measure, based on sensitivity analysis of minimum spanning trees, is used to define candidate sets that are small, but large enough to allow excellent solutions to be found (usually the optimal solutions).

# Список литературы

[1] S. Lin & B. W. Kernighan, “An Effective Heuristic Algorithm for the Traveling-Salesman Problem”, Oper. Res. 21, 498-516 (1973).   
[2] E. L. Lawler, J. K. Lenstra, A. H. G. Rinnooy Kan & D. B. Shmoys (eds.), The Traveling Salesman Problem: A Guided Tour of Combinatorial Optimization , Wiley, New York (1985).   
[3] G. B. Dantzig, D. R. Fulkerson & S. M. Johnson, “Solution of a large-scale traveling-salesman problem”, Oper. Res., 2, 393-410 (1954).   
[4] J. D. C. Little, K. G. Murty, D. W. Sweeny & C. Karel, “An algorithm for the traveling salesman problem”, Oper. Res., 11, 972-989 (1963).   
[5] R. M. Karp, “Reducibility among Combinatorial Problems” in R. E. Miller & J. W. Thatcher (eds.), Complexity of Computer Computations, Plenum Press, New York, 85-103 (1972).   
[6] M. W. Padberg & G. Rinaldi, “A branch-and-cut algorithm for the resolution of large-scale symmetric traveling salesman problems”, SIAM Review, 33, 60-100 (1991).   
[7] M. Grötchel & O. Holland, “Solution of large scale symmetric travelling salesman problems”, Math. Programming, 51, 141-202 (1991).   
[8] D. Applegate, R. Bixby, V. Chvàtal & W. Cook, “Finding cuts in the TSP (A preliminary report)”, DIMACS, Tech. Report 95-05 (1995).   
[9] M. Bellmore & J. C. Malone, “Pathology of traveling-salesman subtour-elimination algorithms”, Oper. Res., 19, 278-307 (1972).   
[10] D. L. Miller & J. F. Pekny, “Exact solution of large asymmetric traveling salesman problems”, Science, 251, 754-761 (1991).   
[11] D. E. Rosenkrantz, R. E. Stearns & P. M. Lewis II, “An analysis of several heuristics for the traveling salesman problem”, SIAM J. Comput., 6, 563-581 (1977).   
[12] G. Laporte, “The Traveling Salesman Problem: An overview of exact and approximate algorithms”, Eur. J. Oper. Res., 59, 231-247 (1992).   
[13] G. Reinelt, The Traveling Salesman: Computational Solutions for TSP Applications, Lecture Notes in Computer Science, 840 (1994).   
[14] I. I. Melamed, S. I. Sergeev & I. Kh. Sigal, “The traveling salesman problem. Approximate algorithms”, Avtomat. Telemekh., 11, 3-26 (1989).   
[15] S. Lin, “Computer Solutions of the Traveling Salesman Problem”, Bell System Tech. J., 44, 2245-2269 (1965).   
[16] N. Christofides & S. Eilon, “Algorithms for Large-scale Travelling Salesman Problems”, Oper. Res. Quart., 23, 511-518 (1972).   
[17] D. S. Johnson, “Local optimization and the traveling salesman problem”, Lecture Notes in Computer Science, 442, 446-461 (1990).   
[18] D. S. Johnson & L. A. McGeoch, “The Traveling Salesman Problem: A Case Study in Local Optimization” in E. H. L. Aarts & J. K. Lenstra (eds.), "Local Search in Combinatorial Optimization", Wiley, New York (1997).   
[19] M. W. Padberg & G. Rinaldi, “Optimization of a 532-city symmetric traveling salesman problem by branch and cut”, Oper. Res. Let., 6 , 1-7 (1987).   
[20] M. Held & R. M. Karp, “The Traveling-Salesman Problem and Minimum Spanning Trees”, Oper. Res., 18, 1138-1162 (1970).   
[21] M. Held & R. M. Karp, “The Traveling-Salesman Problem and Minimum Spanning Trees: Part II”, Math. Programming, 1, 16-25 (1971).   
[22] R. C. Prim, “Shortest connection networks and some generalizations”, Bell System Tech. J., 36, 1389-1401 (1957).   
[23] T. Volgenant & R. Jonker, “The symmetric traveling salesman problem and edge exchanges i minimal 1-trees”, Eur. J. Oper. Res., 12, 394-403 (1983).   
[24] G. Carpaneto, M. Fichetti & P. Toth, “New lower bounds for the symmetric travelling salesman problem”, Math. Programming, 45, 233-254 (1989).   
[25] M. Held, P. Wolfe & H.P. Crowder, “Validation of subgradient optimization”, Math. Programming, 6, 62-88 (1974).   
[26] B.T. Poljak: “A general method of solving extremum problems”, Soviet Math. Dokl., 8, 593-597 (1967).   
[27] H. P. Crowder, “Computational improvements of subgradient optimization”, IBM Res. Rept. RC 4907, No. 21841 (1974).   
[28] P. M. Camerini, L. Fratta & F. Maffioli, “On improving relaxation methods by modified gradient techniques”, Math. Programming Study, 3, 26-34 (1976).   
[29] M. S. Bazaraa & H. D. Sherali, “On the choice of step size in subgradient optimization”, Eur. J. Oper. Res., 7, 380-388 (1981).   
[30] T. Volgenant & R. Jonker, “A branch and bound algorithm for the symmetric traveling salesman problem based on the 1-tree relaxation”, Eur. J. Oper. Res., 9, 83-89 (1982).   
[31] K. H. Helbig-Hansen & J. Krarup, “Improvements of the Held-Karp algorithm for the symmetric traveling salesman problem”, Math. Programming, 7, 87-96 (1974).   
[32] W. R. Stewart, Jr., “Accelerated Branch Exchange Heuristics for Symmetric Traveling Salesman Problems”, Networks, 17, 423-437 (1987).   
[33] G. Reinelt, “Fast Heuristics for Large Geometric Traveling Salesman Problems”, ORSA J. Comput., 2, 206-217 (1992).

[34] [35] [36] [37] [38] [39] [40] [41] [42] [43] [44] [45]

A. Adrabinski & M. M. Syslo,   
“Computational experiments with some approximation algorithms for   
the traveling salesman problem”,   
Zastos. Mat., 1 8 , 91-95 (1983).   
J. Perttunen,   
“On the Significance of the Initial Solution in Travelling Salesman Heuristics”, J. Oper. Res. Soc., 45, 1131-1140 (1994).   
G. Clarke & J. W. Wright,   
“Scheduling of vehicles from a central depot to a number of delivery points”, Oper. Res., 12, 568-581 (1964).   
N. Christofides,   
“Worst Case Analysis of a New Heuristic for the Travelling Salesman Problem”, Report 388. Graduate School of Industrial Administration,   
Carnegie-Mellon University, Pittsburg (1976).   
G. Reinelt,   
“TSPLIB - A Traveling Salesman Problem Library”,   
ORSA J. Comput., 3-4, 376-385 (1991).   
K-T. Mak & A. J. Morton,   
“Distances between traveling salesman tours”,   
Disc. Appl. Math., 58, 281-291 (1995).   
D. Applegate, R. E. Bixby, V. Chvàtal & W. Cook,   
“Data Structures for the Lin-Kernighan Heuristic”,   
Talk presented at the TSP-Workshop, CRCP, Rice University (1990).   
L. Hárs,   
“Reversible-Segment List”,   
Report No 89596-OR,   
Forshunginstitut für Discrete Mathematik, Bonn (1989).   
F. Margot,   
“Quick updates for p-opt TSP heuristics”,   
Oper. Res. Let., 11, 45-46 (1992).   
M. L. Fredman, D. S. Johnson & L. A. McGeoch,   
“Data Structures for Traveling Salesmen”,   
J. Algorithms., 16, 432-479 (1995).   
J. L. Bentley,   
“Fast Algorithms for Geometric Traveling Salesman Problems”,   
ORSA J. Comput., 4, 347-411 (1992).   
J. L. Bentley,   
“K-d trees for semidynamic point sets”,   
Sixth Annual ACM Symposium on Computational Geometry,   
Berkely, CA, 187-197 (1990).   
[46] O. Martin, S. W. Otto & E. W. Felten, “Large-Step Markov Chains for the Traveling Salesman Problem”, J. Complex Systems, 5, 219-224 (1991).   
[47] S. Sahni & T. Gonzales, “P-complete approximation algorithms”, J. Assoc. Comput. Mach., 23, 555-565 (1976).   
[48] J. L. Arthur & J. O. Frendewey, “Generating Travelling-Salesman Problems with Known Optimal Tours”, J. Opl Res. Soc., 39, 153-159 (1988).   
[49] J. Beardswood & J. M. Hammersley, “The shortest path through many points”, Proc. Cambridge Philos. Soc., 55, 299-327 (1959).   
[50] D. S. Johnson, L. A. McGeoch & E. E. Rothenberg, “Asymptotic experimental analysis for the Held-Karp traveling salesman problem”, Proc. 7th ACM SIAM Symp. on Discrete Algorithms Society of Industrial and Applied Mathematics, Philadelphia York (1996).   
[51] R. Jonker & T. Volgenant, “Transforming asymmetric into symmetric traveling salesman problems”, Oper. Res. Let., 2, 161-163 (1983).   
[52] D. E. Knuth, “Leaper Graphs”, Math. Gaz., 78, 274-297 (1994).   
[53] C. H. Papadimitriou & K. Steiglitz, “Some Examples of Difficult Traveling Salesman Problems”, Oper. Res., 26, 434-443 (1978).   
[54] K-T. Mak & A. J. Morton, “A modified Lin-Kernighan traveling-salesman heuristic”, Oper. Res. Let., 13, 127-132 (1993).