# Tackling the Travelling Salesman Problem

with Evolutionary Algorithms:

Representations and Operators

P. Larrañaga, C.M.H. Kuijpers and R.H. Murga

# TACKLING THE TRAVELLING SALESMAN PROBLEM WITHEVOLUTIONARY ALGORITHMS: REPRESENTATIONS ANDOPERATORS

# ABSTRACT

This report is the result of a study of literature carried out by the authors. It is a review of earlier studies by other researchers' published articles. The authors have not added any new information to them. Rather, they have tried to produce a review of the different attempts made to solve the Travelling Salesman Problem (TSP) with evolutionary algorithms.

Because of time and space limitations, the authors restricted themselves to three branches of evolutionary algorithms: genetic algorithms, evolution strategies and evolutionary programming. The different operators which might be used in these evolutionary algorithms make up the main subject of this report. Other subjects, e.g. selection and stop criterions of the algorithms, are not concerned, and the performance of algorithms is dealt with only briefly.

Keywords: Evolutionary algorithms; Genetic algorithms; Evolution strategies; Evolutionary programming; Crossover operator; Mutation operator; Travelling Salesman Problem.

# Contents

Abstract 1

I Introduction 3

2 Evolutionary Algorithms 5

2.1 Introduction . . 5   
2.2 Genetic Algorithms 5   
2.3 Evolutionary Programming   
2.4 Evolution Strategies 9

The Travelling Salesman Problem 11

# 4 Representations and Operators 13

4.1 Binary Representation 13

4.1.1 Classical Crossover . . . 14   
4.1.2 Classical Mutation . . 14

4.2 Adjacency Representation . . 16

4.2.1 Alternating Edge Crossover . 16

4.2.2 Subtour Chunks Crossover . 17

4.2.3 Heuristic Crossover . 17

4.3 Ordinal Representation 19

4.4 Path Representation 20

4.4.1 Partially-Mapped Crossover (PMX) 20   
4.4.2 Cycle Crossover (CX) 22   
4.4.3 Order Crossover (OX) . . . 23   
4.4.4 Heuristic Crossover . . 26   
4.4.5 Genetic Edge Recombination Crossover (ER) 26   
4.4.6 Sorted Match Crossover 30   
4.4.7 Maximal Preservative Crossover (MPX) 30   
4.4.8 Voting Recombination Crossover 31   
4.4.9 Displacement Mutation 32   
4.4.10 Exchange Mutation 33   
4.4.11 Insertion Mutation . . 33   
4.4.12 Simple Inversion Mutation . 34   
4.4.13 Inversion Mutation . . 34   
4.4.14 Scramble Mutation . 35

4.5 Matrix Representation 35

Hybridization with Local Search 43

6 Conclusions 4

Bibliography 47

# Chapter 1

# Introduction

In nature, there exist many processes which seek a stable state. These processes can be seen as natural optimization processes. Over the last 30 years several attempts have been done to develop global optimization algorithms which simulate these natural optimization processes. These attempts have resulted in the following optimization methods:

Simulated Annealing, based on natural annealing processes.

• Artificial Neural Networks, based on processes in central nervous systems.

Evolutionary Computation, based on biological evolution processes.

The algorithms inspired by Evolutionary Computation are called evolutionary algorithms. These evolutionary algorithms may be divided into the following branches: genetic algorithms, evolutionary programming, evolution strategies, classifier systems, genetic programming and other optimization algorithms based on Darwin's evolution theory of natural selection and "survival of the fittest".

In this report we only pay attention to three of the above mentioned types of algorithms: genetic algorithms, evolutionary programming and evolution strategies. We consider these algorithms in combination with the Travelling Salesman Problem (TSP). The TSP is to find the shortest tour for a travelling salesman who, starting from his home city, has to visit every city on a given list precisely once and then return to his home city. The main difficulty of this problem is the inmense number of possible tours: $( n - 1 ) ! / 2$ for $n$ cities.

The structure of this report is as follows. First, we look at what evolutionary algorithms are and we describe three different types: genetic algorithms, evolution strategies and evolutionary programming (see Chapter 2). Next, we give a brief introduction on the Travelling Salesman Problem (see Chapter 3). In Chapter 4 we describe several representations which may be used for a problem instance of the TSP, and we describe operators with which they can be combined. We look at how we can include local search in an evolutionary algorithm in Chapter 5. Lastly, conclusions are given in Chapter 6.

# Acknowledgements

This work was supported by the Diputación Foral de Gipuzkoa, under Grant OF 1522, and by the Fondo de Investigación Sanitaria, Ministerio de Sanidad y Consumo, under Grant 94/1370.

# Chapter 2

# Evolutionary Algorithms

# 2.1 Introduction

Evolutionary algorithms are probabilistic search algorithms which simulate natural evolution. They were proposed about 30 years ago (Bremermann et al. [8] and Rechenberg [47]). Their application to combinatorial optimization problems, however, only recently became an actual research topic. In recent years numerous papers on the evolutionary optimization of NP-hard problems have been published.

In this report we pay attention to three different types of evolutionary algorithms: genetic algorithms, evolutionary programming and evolution strategies. We describe these different types of algorithms below.

# 2.2 Genetic Algorithms

Holland [27] introduced genetic algorithms. In these algorithms the search space of a problem is represented as a collection of individuals. These individuals are represented by character strings (or matrices, see Chapter 4.5), which are often referred to as chromosomes. The purpose of the

# Algorithm GA

start with an initial time   
t:=0;   
initialize a usually random population of individuals   
initpopulation $\mathrm { P ( t ) }$ ,   
evaluate fitness of all initial individuals of population   
evaluate $\mathrm { P ( t ) }$ ;   
test for termination criterion (time, fitness, etc.)   
while not done do increase time counter $\mathrm { t } { : = } \mathrm { t } { + } 1$ ; select subpopulation of parents for offspring production $\mathrm { P } { : = }$ selectparents $\mathrm { P ( t ) }$ ; recombine the "genes" of selected parents crossover $\mathrm { P ^ { \prime } ( t ) }$ ; perturb the mated population stochastically mutate $\mathrm { P ^ { \prime } ( t ) }$ evaluate its new fitness evaluate $\mathrm { P ^ { \prime } ( t ) }$ ; select the survivors from actual fitness P $=$ survive P,P'(t);   
od

end GA.

Table 2.1: The pseudo cople of a genetic algorithm.

use of a genetic algorithm is to find the individual from the search space with the best "genetic material". The quality of an individual is measured with an evaluation function. The part of the search space to be examined is called the population.

Roughly, a genetic algorithm works as follows (see Table 2.1). First, the initial population is chosen, and the quality of this population is determined. Next, in every iteration parents are selected from the population. These parents produce children, which are added to the population. For all newly created individuals of the resulting population a probability near to zero exists that they will "mutate", i.e. that they will change their heriditary distinctions. After that, some individuals are removed from the population according to a selection criterion in order to reduce the population to its initial size. One iteration of the algorithm is referred to as a generation.

The operators which define the child production process and the mutation process are called the crossover operator and the mutation operator respectively. Mutation and crossover play different roles in the genetic algorithm. Mutation is needed to explore new states and helps the algorithm to avoid local optima. Crossover should increase the average quality of the population. By choosing adequate crossover and mutation operators, the probability that the genetic algorithm results in a near-optimal solution in a reasonable number of iterations is enlarged. Further description of genetic algorithms can be found in Goldberg [21] and Davis [10].

# 2.3 Evolutionary Programming

The second branch of evolutionary computation which we consider is evolution programming. Evolution programming is based on a concept offered by Fogel ([11, 12] and Fogel et al. [13]). Roughly, the structure of the algorithms is the same as for the genetic algorithms (see Table 2.2). However, there are two important differences between the genetic algorithms and evolutionary programming. First, in evolutionary programming no constraint on representation exists; individuals are

# Algorithm EP

start with an initial time   
$\mathrm { t } { : = } 0$   
initialize a usually random population of individuals   
initpopulation $\mathrm { P ( t ) }$ ;   
evaluate fitness of all initial individuals of population   
evaluate $\mathrm { P ( t ) }$ ;   
test for termination criterion (time, fitness, etc.)   
while not done do increase time counter $\mathrm { t } { : = } \mathrm { t } { + } 1$ ; perturb the whole population stochastically mutate $\mathrm { P ( t ) }$ ; evaluate its new fitness evaluate $\mathrm { P ^ { \prime } ( t ) }$ ; select the survivors from actual fitness P $=$ survive P,P'(t);   
od

end EP.

Table 2.2: The pseudo code of evolutionary programming.

not necessarily represented by character strings. Second, new individuals are created by mutation only, crossover does not exist. Therefore, evolutionary programming can be seen as the asexual counterpart of genetic algorithms. Evolutionary programming is detailed in Fogel et al. [13] and Fogel [16, 17].

There are supporters and opponents of evolutionary programming. The supporters use the argument that every state reached by crossover can also be reached by mutation. The opponents believe that genetic algorithms work better than evolutionary programming if the offspring inherits adequate information from its parents. More about the pros and cons of the use of crossover can be found in Spears [55].

# 2.4 Evolution Strategies

The last class of evolutionary algorithms to which we pay attention is the class of evolution strategies. The evolution strategies were developed by Rechenberg [47] and Schwefel [51]. Broadly speaking, the evolution strategies function like the earlier described evolutionary algorithms. In every generation parents create children by crossover and/or mutation, after which some individuals survive and others die. Two different types of evolution strategies can be distinguished: the comma strategy and the plus strategy. In the comma strategy, which is denoted by $\operatorname { E S } ( \mu , \lambda )$ , in every generation $\mu$ parents are selected to produce $\lambda$ children. The $\mu$ strongest offspring survive, the parents and the rest of the offspring die.

In the plus strategy, which is denoted by $\operatorname { E S } ( \mu + \lambda )$ , in every generation also $\lambda$ offspring are created by $\mu$ parents. However, in the plus strategy the parents are taken into account in the selection, they do not necessarily die. The best $\mu$ individuals out of the $\mu + \lambda$ existing individuals (parents plus children) survive, the rest die.

The ratio $\frac { \mu } { \lambda }$ determines the convergence properties of the evolution strategy. Mathematical analysis of the evolution strategies is quite diffcult. Therefore, up to now few precise results exist. For a detailed description of the evolution strategies, see Rechenberg [47]; Schwefel [51, 52, 53] and Bäck et al. [3].

# Chapter 3

# The Travelling Salesman Problem

As already stated in Chapter 1 the Travelling Salesman Problem is, given a collection of cities, to determine the shortest tour which visits each city precisely once and then returns to its starting point. More mathematically we may define the TSP as follows:

# TSP

Given an integer $n \geq 3$ and an $n \times n$ matrix $C = \left( c _ { i j } \right)$ , where each $c _ { i j }$ is a nonnegative integer. Which cyclic permutation $\pi$ of the integers from 1 to $n$ minimizes the sum $\scriptstyle \sum _ { i = 1 } ^ { n } c _ { i \pi ( i ) }$ ?

Through the years the Travelling Salesman Problem has occupied the mind of numerous researchers. This is for several reasons. First, the TSP is very easy to describe, yet very difficult to solve. No polynomial time algorithm is known with which it can be solved. This lack of any polynomial time algorithm is characteristic of the class of NP-complete problems, of which the TSP is a classic example. Second, the TSP is broadly applicable to a variety of routing and scheduling problems. Lastly, since a lot of information is already known about the TSP, it has become a kind of "test" problem; new combinatorial optimization methods are often applied to the TSP so that an idea

can be formed of their usefulness.

Numerous heuristic algorithms have been developed for the TSP. Many of them are described in Lawler et al. [32]. Kirkpatrick et al. [31] were the first who tried to solve the TSP with simulated annealing.

The first to tackle the Travelling Salesman Problem with genetic algorithms was Brady [7]. His example was followed by Grefenstette et al. [23]; Goldberg and Lingle [20]; Oliver et al. [44] and many others. Other evolutionary algorithms have been applied to the TSP by, amongst others, Fogel [14]; Banzhaf [4] and Ambati et al. [2].

For an extensive discussion on the TSP we refer to Lawler et al. [32]. Problem instances of the Travelling Salesman Problem, partly with their optimal solutions, can be found in a TSP library which is available via ftp as follows:

ftp sfi.santafe.edu   
Name (sfi.santafe.edu: foobar): anonymous   
Password: < e-mail address $>$   
ftp> cd pub/EC/etc/data/TSP   
ftp> type binary   
ftp> get tsplib-1.2.tar.gz

This library was compiled by G. Reinelt. More information about it can be found in Reinelt [48].

# Chapter 4

# Representations and Operators

# 4.1 Binary Representation

In a binary representation of the $n$ -cities TSP, each city is encoded as a string of $\lceil \log _ { 2 } n \rceil$ bits, an individual is a string of $n \left\lceil \log _ { 2 } n \right\rceil$ bits. For example, in the 6-cities TSP the cities are represented by 3-bit strings (see Table 4.1). Following the binary representation defined in Table 4.1, the tour

Table 4.1: Binary representation of the 6-cities TSP.   

<table><tr><td>i</td><td>city i</td><td>i</td><td>city i</td></tr><tr><td>1 2</td><td>000</td><td>4</td><td>011</td></tr><tr><td>3</td><td>001 010</td><td>5 6</td><td>100 101</td></tr></table>

$1 - 2 - 3 - 4 - 5 - 6$ is represented by

Note that 3-bit strings exist which do not correspond to any city: the strings 110 and 111.

# 4.1.1 Classical Crossover

The classical crossover operator was proposed by Holland [27]. It works as follows. Consider, for example, the following two solutions of the 6-cities TSP:

(000001 010011 100101)and

Randomly a crossover point is selected, where the strings are broken into separate parts. Suppose, for example, that we choose the crossover point to be between the ninth and the tenth bit. Hence,

(000 001 010 | 011 100 101)and

Recombination of the different parts results in

(000001 010010001 000)and

which do not represent legal tours. To change the created offspring into legal tours we need some sort of "repair" algorithm.

# 4.1.2 Classical Mutation

The classical mutation operator was also developed by Holland [27]. It alters one or more bits with a probability equal to the mutation rate, which is near to zero. For example, consider again the following string which represents the tour $1 - 2 - 3 - 4 - 5 - 6$ .

Suppose that the first and the second bit are selected for mutation. Hence, these bits change from a 0 into a 1. The result is

(110001 010011 100 101), which does not represent a tour.

Lidd [33] followed a binary vector approach for the TSP. However, although he managed to get some high quality results for small TSPs (his largest test case consisted of 100 cities), the binary representation is not considered to be very appropriate for the TSP. Whitley et al. [60, 61] developed the genetic edge recombination crossover operator for the later described path representation. They showed that this operator can also be used in combination with a binary representation which is different from the one described above. The binary representation suggested by Whitley et al. can be described as follows. First, an ordered list is defined which contains all possible edges in the TSP. With the help of this list a tour may be written as a binary vector, the length of which is equal to the number of edges in the defined list. The $i$ -th element of the binary vector is a 1 if, and only if, the $i$ -th edge out of the ordered list is part of the tour. For example, for the 6-cities TSP we define the following list of edges: (1,2), (1,3), (1,4), (1,5), (1,6), (2,3), (2,4), (2,5), (2,6), (3,4), (3,5), (3,6), (4,5), (4,6), (5,6). Then, the tour $1 - 2 - 3 - 4 - 5 - 6$ is represented by the binary vector 100011000100101. See page 26 for an explanation of the genetic edge recombination operator.

# 4.2 Adjacency Representation

In the adjacency representation (Grefenstette et al. [23]) a tour is represented as a list of $n$ cities

City $j$ is listed in position $i$ if, and only if, the tour leads from city $i$ to city $j$ . Thus, the list

represents the tour

Note that any tour has one unique adjacency list representation.

An adjacency list may represent an illegal tour. For example,

represents the following collection of cycles:

It is easy to see that also for the adjacency representation the classical crossover operator may result in illegal tours. A repair algorithm might be necessary.

Other crossover operators were defined and investigated for the adjacency representation. We will describe them one by one.

# 4.2.1 Alternating Edge Crossover

This operator works as follows (Grefenstette et al. [23]): first it chooses an edge from the first parent at random. Second, the partial tour created in this way is extended with the appropriate edge of the second parent. This partial tour is extended by the adequate edge of the first parent, etc. The partial tour is extended by choosing edges from alternating parents. In case an edge is chosen which would produce a cycle into the partial tour, the edge is not added. Instead, the operator selects randomly an edge from the edges which do not produce a cycle. For example, the result of an alternating edge crossover of the parent

might be

The first edge chosen is (1,2); it is chosen from the first parent. The second edge chosen, edge (2,5), is selected from the second parent, etc. Note that the only random edge introduced is edge (7,6) instead of edge (7,8).

# 4.2.2 Subtour Chunks Crossover

Using the subtour chunks operator (Grefenstette et al. [23]), an offspring is constructed from two parent tours as follows: first it takes a random length subtour of the first parent. This partial tour is extended by choosing a subtour of random length from the second parent. The partial tour is extended by taking subtours from alternating parents. If a subtour is selected from one of the parents which would lead to an illegal tour, it is not added. Instead, an edge is added which is chosen at random from the edges that do not produce a cycle into the partial tour.

# 4.2.3 Heuristic Crossover

The heuristic crossover operator (Grefenstette et al. [23]) first selects at random a city to be the starting point of the offspring's tour. Then, the edges which start from this city are compared and the shorter of these two edges is chosen. Next, the city on the other side of the chosen edge is selected as a reference city. The edges which start from this reference city are compared and the shortest one is added to the partial tour, etc. If, at some stage, a new edge would introduce a cycle into the partial tour, then the tour is extended with an edge chosen at random from the remaining edges which do not introduce cycles.

# Modifications

Jog et al. [29] suggested the following modification. In case choosing the shortest edge produces a cycle into the partial tour, the largest edge is checked. If choosing this edge does not lead to an illegal tour, it is accepted. Otherwise, the shortest edge from a pool of $q$ randomly selected edges is chosen, where $q$ is a parameter. This variation of the heuristic operator tries to combine short subpaths of the different parent tours. However, it might be possible that the operator is not able to remove all undesirable crossings of edges. Therefore, it is not suitable for fine local tuning.

Suh and Van Gucht [57] introduced a heuristic crossover operator which is based on the 2-opt algorithm of Lin [35]. This operator selects two random edges, $( k , l )$ and $( m , n )$ , and checks whether

$$
d ( k , l ) + d ( m , n ) > d ( k , n ) + d ( m , l ) ,
$$

where $d ( i , j )$ represents the distance between city $i$ and city $j$ . In case the inequality above is true, the edges $\left( k , l \right)$ and $( m , n )$ are replaced by the edges $( k , n )$ and $( m , l )$ .

The main advantage of the adjacency representation is that it allows hyperplane analysis, also called schemata analysis (Oliver et al. [44], Grefenstette et al. [23] and Michalewizc [38]. Unfortunately, al the operators described above give poor results. In particular, the experimental results with the alternating edge operator have been uniformly discouraging. This is because this operator often destroys good subpaths of the parent tours. Therefore, the subtour chunk operator by choosing subpaths instead of edges from the parent tours, performs better than the alternating edge operator. However, it still has quite a low performance, because it does not take into account any information available about the edges. The heuristic crossover operator on the other hand, selects the better edge of the two possible edges, and therefore it performs far better than the other two operators. However, the performance of the heuristic operator is not remarkable either (Grefenstette et al. [23]).

Note that also other mutation operators have to be developed, since the classical mutation operator is only defined for binary strings.

# 4.3 Ordinal Representation

Also in the ordinal presentation, which was introduced by Grefenstette et al. [23] a tour is represented as a list of $n$ cities. The $i$ -th element of the list is a number in the range from 1 to $n - i + 1$ . There exists an ordered list of cities, which serves as a reference point.

The easiest way to explain the ordinal representation is by giving an example. Assume, for example, that the ordered list is given by

$$
L = ( 1 2 3 4 5 6 7 8 ) .
$$

Now the tour $1 - 5 - 3 - 2 - 8 - 4 - 7 - 6$ is represented by

$$
T = ( 1 4 2 1 4 1 2 1 ) .
$$

This should be interpreted as follows:

The first number of $\mathrm { T }$ is a 1. This means that to get the first city of the tour we have to take the first element of list $L$ and remove it from $L$ .The partial tour is: 1.

The second element of $\mathrm { T }$ is a 4. Therefore, to get the second city of the tour we have to get

the fourth element of list $L$ , which is city 5. We remove city 5 from list $L$ . The partial tour is: 1 - 5.

If we continue in the above described way until all the elements of $L$ have been removed, we finally find the tour $1 - 5 - 3 - 2 - 8 - 4 - 7 - 6 .$

The advantage of the ordinal presentation is that the classical crossover operator can be used. This follows from the fact that the $i$ -th element of the tour representation is always a number in the range from 1 to $n - i + 1$ .

Unfortunately, poor experimental results (Grefenstette et al. [23] indicate that the ordinal representation together with classical crossover is not very suitable for the TSP.

# 4.4 Path Representation

The path representation is probably the most natural representation of a tour. Again a tour is represented as a list of $n$ cities. If city $i$ is the $j \cdot$ -th element of the list, city $i$ is the $j$ -th city to be visited. Hence, tour $3 - 2 - 4 - 1 - 7 - 5 - 8 - 6$ is simply represented by

Since for the TSP in combination with the path representation the classical operators are also not suitable, other crossover and mutation operators have been defined.

# 4.4.1 Partially-Mapped Crossover (PMX)

The partially-mapped crossover operator was suggested by Goldberg and Lingle [20]. It passes on ordering and value information from the parent tours to the offspring tours. A portion of one parent string is mapped onto a portion of the other parent string and the remaining information is exchanged. Consider, for example the following two parent tours:

The PMX operator creates an offspring in the following way. First, it selects uniformly at random two cut points along the strings, which represent the parent tours. Suppose that the first cut point is selected between the third and the fourth string element, and the second one between the sixth and the seventh string element. Hence,

(123|456 78) and

The substrings between the cut points are called the mapping chapters. In our example they define the mappings $4  1$ , $5  6$ and $6  8$ . Now the mapping chapter of the first parent is copied into the second offspring, and the mapping chapter of the second parent is copied into the first offspring.

Then offspring $i$ $i = 1 , 2$ ) is filled up by copying the elements of the $i$ -th parent. In case a city is already present in the offspring it is replaced according to the mappings. For example, the first element of offspring 1 would be a 1 like the first element of the first parent. However, there is already a 1 present in offspring 1. Hence, because of the mapping $1  4$ we choose the first element of offspring 1 to be a 4. The second, third and seventh elements of offspring 1 can be taken from the first parent. However, the last element of offspring 1 would be an 8, which is already present. Because of the mappings $8  6$ , and $6  5$ , it is chosen to be a 5. Hence,

Analogously, we find

Note that the absolute positions of some elements of both parents are preserved.

A variation of the PMX operator is described in Grefenstette [26]: given two parents the offspring is created as follows. First, the second parent string is copied onto the offspring. Next, an arbitrary subtour is chosen from the first parent. Lastly, minimal changes are made in the offspring necessary to achieve the chosen subtour. For example, consider parent tours

and suppose that subtour (345) is chosen. This gives offspring

# 4.4.2 Cycle Crossover (CX)

The cycle crossover operator was proposed by Oliver et al. [44]. It attempts to create an offspring from the parents where every position is occupied by a corresponding element from one of the parents. For example, consider again the parents

Now we choose the first element of the offspring equal to either the first element of the first parent tour or the first element of the second parent tour. Hence, the first element of the offspring has to be a 1 or a 2. Suppose we choose it to be 1,

$$
( 1 * * * * * * * * * ) .
$$

Now, consider the last element of the offspring. Since this element has to be chosen from one of the parents, it can only be an 8 or a 1. However, if a 1 were selected, the offspring would not represent a legal tour. Therefore, an 8 is chosen,

$$
( 1 * * * * * * * 8 ) .
$$

Analogously, we find that the fourth and the second element of the offspring also have to be selected from the first parent, which results in

$$
( 1 2 * 4 * * * 8 ) .
$$

The positions of the elements chosen up to now are said to be a cycle. Now consider the third element of the offspring. This element we may choose from any of the parents. Suppose that we select it to be from parent 2. This implies that the fifth, sixth and seventh elements of the offspring also have to be chosen from the second parent, as they form another cycle. Hence, we find the following offspring:

The absolute positions of on average half the elements of both parents are preserved. Oliver et al. [44] concluded from theoretical and empirical results that the CX operator gives better results for the Travelling Salesman Problem than the PMX operator.

# 4.4.3 Order Crossover (OX)

The OX operator was proposed by Davis [9]. It constructs an offspring by choosing a subtour of one parent and preserving the relative order of cities of the other parent. For example, consider the following two parent tours:

and suppose that we select a first cut point between the second and the third bit and a second one between the fifth and the sixth bit. Hence,

(12|345|678) and

The offspring are created in the following way. First, the tour segments between the cut point are copied into the offspring, which gives

$$
( * * | 3 4 5 | * * * ) \mathrm { ~ a n d }
$$

$$
( * * | 6 8 7 | * * * ) .
$$

Next, starting from the second cut point of one parent, the rest of the cities are copied in the order in which they appear in the other parent, also starting from the second cut point and omitting the cities that are already present. When the end of the parent string is reached, we continue from its first position. In our example this gives the following children:

Oliver et al. [44] concluded from a theoretical analysis and empirical results that the OR operator is more suitable for the TSP than the PMX operator and the CX operator.

Syswerda [58] suggested, in connection with schedule problems instead of the TSP, the following two modifications of the OX operator.

# Order Based Crossover

The order based crossover operator selects at random several positions in a parent tour, and the order of the cities in the selected positions of this parent is imposed on the other parent. For example, consider again the parents

and suppose that in the second parent the second, third, and sixth positions are selected. The cities in these positions are city 4, city 6 and city 5 respectively. In the first parent these cities are present at the fourth, fth and sixth positions. Now the offspring is equal to parent 1 except in the fourth, fifth and sixth positions:

$$
( 1 2 3 * * * 7 8 ) .
$$

We add the missing cities to the offspring in the same order in which they appear in the second parent tour. This results in

Exchanging the role of the first parent and the second parent gives, using the same selected positions,

# Position Based Crossover

The position based operator also starts with selecting a random set of positions in the parent tours. However, this operator imposes the position of the selected cities on the corresponding cities of the other parent. For example, consider the parent tours

and suppose that the second third and the sixth positions are selected. This leads to the following offspring:

# 4.4.4 Heuristic Crossover

Grefenstette [26] developed a class of heuristic crossover operators which emphasize edges. These operators create an offspring in the following way:

1. They first select at random a city to be the current city of the offspring.

2. Second, they consider the four (undirected) edges incident to the current city. Over these edges a probability distribution is defined based on their cost. The probability associated with an edge incident to a previously visited city is equal to zero.

3. An edge is selected on this distribution. (If none of the parental edges leads to an unvisited city a random edge is selected.)

4. The steps 3 and 4 are repeated until a complete tour has been constructed.

In case a uniform probability distribution is chosen, the offspring inherits about $3 0 \%$ of the edges of every parent, and about $4 0 \%$ of the edges are randomly selected. The operator described above was also used by Liepins et al. [34].

# 4.4.5 Genetic Edge Recombination Crossover (ER)

The genetic edge recombination crossover operator was developed by Whitley et al. [60, 61]. It is an operator which is suitable for the symmetrical TSP; it makes the assumption that only the values of the edges are important, not their direction. In accordance with this assumption, the edges of a tour can be seen as the carriers of the heriditary information. The ER operator attempts to preserve the edges of the parents in order to pass on a maximum amount of information to the offspring. The breaking of edges is seen as unwanted mutation.

The problem that normally occurs with operators which follow an edge recombination strategy, is that they often leave cities without a continuing edge (Grefenstette [26]). These cities become isolated and new edges have to be introduced. The ER operator tries to avoid this problem by first choosing cities which have few unused edges. Of course, there has to be a connection with a city before it can be selected. The only edge that the ER operator fails to enforce is the edge from the final city to the initial city. Therefore, a limited amount of mutation may occur. The mutation rate will be at most $1 / n$ , where $n$ is the number of cities. In practice the mutation rate turned out to be between $1 - 5 \%$ .

Now, how does the ER operator work? It uses a so-called "edge map", which gives for each city the edges of the parents that start or finish in it. Consider for example these tours:

(123456) and

The edge map for these tours is as follows:

City 1 is connected with the cities: 2 6 3 5   
City 2 is connected with the cities: 1 3 4 6   
City 3 is connected with the cities: 2 4 1   
City 4 is connected with the cities: 3 5 2   
City 5 is connected with the cities: 4 6 1   
City 6 is connected with the cities: 1 5 2

The genetic edge recombination operator works according to the following algorithm:

1. Choose the initial city from one of the two parent tours. (It can be chosen at random or according to criteria outlined in step 4.) This is the "current city".

2. Remove all occurrences of the "current city" from the left-hand side of the edge map. (These can be found by referring to the edge list for the current city.)

3. If the current city has entries in its edge list go to step 4; otherwise, go to step 5.

4. Determine which of the cities in the edge list of the current city has the fewest entries in its own edge list. The city with the fewest entries becomes the "current city". Ties are broken at random. Go to step 2.

5. If there are no remaining "unvisited" cities, then STOP. Otherwise, choose at random an "unvisited" city and go to step 2.

For our example tours we get:

1. The new child tour is initialized with one of the two initial cities from its parents. Initial cities 1 and 2 both have four edges; randomly choose city 2.

2. The edge list for city 2 indicates the candidates for the next city are the cities 1, 3, 4 and 6. The cities 3, 4 and 6 all have two edges: the initial three minus the connection with city 2. City 1 now has three edges and therefore it is not considered. Assume that city 3 is randomly chosen.

3. City 3 now has edges to city 1 and city 4. City 4 is chosen next, since it has fewer edges.

4. City 4 only has an edge to city 5, so city 5 is chosen next.

5. City 5 has edges to the cities 1 and 6, both of which have only one edge left. Randomly choose city 1.

6. City 1 must now go to city 6.

The resulting tour is

and is composed entirely of edges taken from the two parents.

The ER operator does not take into account the common sequences of the parent tours. Therefore, an enhancement of the ER operator was developed in which the edges starting from the current city which are present in both parents have priority above the edges which are unique for one of the parents. Also, there exist modifications for making better choices, when random edge selection is necessary (Starkweather et al. [56]).

Whitley et al. [60, 61] showed that the ER operator may also be used in combination with the second type of binary representation described in Chapter 4.1. If we define the ordered list: (1,2), (1,3), (1,4), (1,5), (1,6), (2,3), (2,4), (2,5), (2,6), (3,4), (3,5), (3,6), (4,5), (4,6), (5,6), the parents of our example may be written as

parent 1: 100011000100101, parent 2: 010100101100001.

In our example, the created offspring is represented by

It is easy to see that all of the edges of the offspring except its last one are taken from one of the parents:

parent 1: 100011000100101, parent 2 : 010100101100001, offspring: 000111001100100.

The edge (5,6) occurred in both parents. However, it was not passed on to the offspring.

# 4.4.6 Sorted Match Crossover

The sorted match crossover operator was proposed by Brady [7]. It (see also Mühlenbein et al. [40]) searches for subtours in both the parent tours which have the same length, which start in the same city, which end in the same city and which contain the same set of cities. If such subtours are found the cost of these substrings are determined. The offspring is constructed from the parent which contains the subtour with the highest cost by substituting this subtour for the subtour with the lowest cost. Consider, for example, the parent tours

The first parent contains the subtour (4567), and the second parent the subtour (4657). These subtours have the same length, both begin in city 4, both end in city 7, and both contain the same cities. Suppose that the cost of the subtour (4567) is higher than the cost of the subtour (4657). Then, the following offspring is created:

Mühlenbein et al. [40] concluded that the sorted match crossover was useful in reducing the computation time, but that it is a weak scheme for crossover.

# 4.4.7 Maximal Preservative Crossover (MPX)

The maximal preservative operator was introduced by Mühlenbein et al. [40]. It works in a similar way to the PMX operator. It first selects a random substring of the first parent whose length is greater than or equal to 10 (except for very small problem instances), and smaller than or equal to the problem size divided by 2. These restrictions on the length of the substring are given to assure that there is enough information exchange between the parent strings without losing too much information from any of these parents. Next, all the elements of the chosen substring are removed from the second parent. After this, the substring chosen from parent 1 is copied into the first part of the offspring. Lastly, the end of the offspring is flled up with cities in the same order as the one in which they appear in the second parent. Hence, if we consider the parent tours

and we select the substring (345) from the first parent. The MPX operator gives the following offspring

The advantage of the MPX operator is that it only destroys a limited number of edges; the maximum number of edges which may be destroyed is equal to the length of the chosen substring. Sometimes, at the beginning of the execution of an algorithm this maximum number might be reached. However, with the progress of the computation, solutions have more common edges, so that the number of destroyed edges decreases. Mühlenbein et al. [40] performed additional mutation in case less than $1 0 \%$ of the edges were destroyed.

# 4.4.8 Voting Recombination Crossover

The voting recombination operator (Mühlenbein [41]) does not originate from biology. It can be seen as a p-sexual crossover operator, where p is a natural number greater than or equal to 2. It starts by defining a threshold, which is a natural number smaller than or equal to p. Next, for every $i \in \{ 1 , 2 , \ldots , n \}$ the set of $i$ -th elements of all the parents is considered. If in this set an element occurs at least the threshold number of times, it is copied into the offspring. For example, if we consider the parents $\scriptstyle ( \mathrm { p } = 4 )$

and we define the threshold to be equal to 3 we find

$$
( 1 2 x x x 6 ) .
$$

The remaining positions of the offspring are illed with mutations. Hence, our example might result in

We remark that Mühlenbein [41] used the voting recombination operator in an evolutionary algorithm for the Quadratic Assignment Problem (QAP) instead of for the TSP.

# 4.4.9 Displacement Mutation

The displacement mutation operator (Michalewizc [38]) first selects a subtour at random. This subtour is removed from the tour and inserted in a random place. For example, consider the tour represented by

and suppose that the subtour (345) is selected. Hence, after the removal of the subtour we have

Suppose that we randomly select city 7 to be the city after which the subtour is inserted. This results in

Displacement mutation is also called cut mutation (Banzhaf [4]).

# 4.4.10 Exchange Mutation

The exchange mutation operator (Banzhaf [4]) randomly selects two cities in the tour and exchanges them. For example, consider the tour represented by

and suppose that the third and the fifth city are randomly selected. This results in

The exchange mutation operator is also referred to as the swap mutation operator (Oliver et al. [44]), the point mutation operator (Ambati et al. [2]), the reciprocal exchange mutation operator (Michalewizc [38]), or the order based mutation operator (Syswerda [58]).

Ambati et al. [2] used repeated exchange mutation. They chose the probability of the performance of exactly m exchanges equal to $p ^ { ( m - 1 ) } ( 1 - p )$ , where $p$ was a parameter and $p \in ( 0 , 1 )$ .

Beyer [6] also used repeated exchange mutation. He, however, introduced a control parameter $s$ to determine the number of exchanges. Each individual had its own $s$ -value, the $s$ -value of an offspring was determined by the $s$ -values of its parents. At the beginning of the algorithm a high number of exchanges was carried out. Through the algorithm, the number of exchanges was lowered to 1. This method is adopted from Schwefel [50].

# 4.4.11 Insertion Mutation

The insertion mutation operator (Fogel [14] and Michalewizc [38]) randomly chooses a city in the tour, removes it from this tour, and inserts it in a randomly selected place. For example, consider again the tour

and suppose that the insertion mutation operator selects city 4, removes it, and randomly inserts it after city 7. Hence, the resulting offspring is

The insertion mutationoperator is alsocalled the position based mutation perator (Syswerda [8].

# 4.4.12 Simple Inversion Mutation

The simple inversion mutation operator (Holland [27] and Grefenstette [26]) selects randomly two cut points in the string, and it reverses the substring between these two cut points. For example, consider the tour

and suppose that the first cut point is chosen between city 2 and city 3, and the second cut point between the fifth and the sixth city. This results in

The simple inversion mutation operator served as the basis for the 2-opt heuristic for the TSP developed by Lin [35] and is also used in the application of simulated annealing to the TSP (Kirkpatrick et al. [31]).

# 4.4.13 Inversion Mutation

The inversion mutation (Fogel [15, 18]) is similar to the displacement operator. It also randomly selects a subtour, removes it from the tour and inserts it in a randomly selected position. However, the subtour is inserted in reversed order. Consider again our example tour

and suppose that the subtour (345) is chosen, and that this subtour is inserted inmediately after city 7. This gives

Banzaf [4] referred to the insertion mutation operator as the cut-inverse mutation operator.

# 4.4.14 Scramble Mutation

The scramble mutation operator (Syswerda [58]) selects a random subtour and scrambles the cities in it. For example, consider the tour

and suppose that the subtour (4567) is chosen. This might result in

We would like to point out that it was suggested in connection with scheduling problems instead of with the TSP.

# 4.5 Matrix Representation

At least three attempts have been done to use a binary matrix representation.

•Fox and McMahon [19] suggested representing a tour as a matrix in which the element in row $i$ and column $j$ is a 1 if, and only if, in the tour city $i$ is visited before city $j$ . For example, the tour $2 - 3 - 1 - 4$ is represented by the matrix:

$$
\left( \begin{array} { c c c c } { { 0 } } & { { 0 } } & { { 0 } } & { { 1 } } \\ { { } } & { { } } & { { } } & { { } } \\ { { 1 } } & { { 0 } } & { { 1 } } & { { 1 } } \\ { { } } & { { } } & { { } } & { { } } \\ { { 1 } } & { { 0 } } & { { 0 } } & { { 1 } } \\ { { } } & { { } } & { { } } & { { } } \\ { { 0 } } & { { 0 } } & { { 0 } } & { { 0 } } \end{array} \right) .
$$

Suppose that a solution of the $n$ -cities TSP is represented by matrix $M , M$ has the following properties:

$$
( i , j \in \{ 1 , 2 , \dots , n \} ) ,
$$

1. $\begin{array} { r } { \sum _ { j = 1 } ^ { n } \sum _ { i = 1 } ^ { n } m _ { i j } = \frac { n ( n - 1 ) } { 2 } } \end{array}$   
2. $m _ { i i } = 0$   
3. $( m _ { i j } = 1 \land m _ { j k } = 1 ) \Rightarrow m _ { i k } = 1$

$$
( i \in \{ 1 , 2 , \dots , n \} ) ,
$$

$$
( i , j , k \in \{ 1 , 2 , \dots , n \} ) .
$$

In case the number of 1s in the matrix is less than ${ \frac { 1 } { 2 } } n ( n - 1 )$ and the other requirements are satisfied, it is possible to complete the matrix in such a way that it represents a legal tour. For this matrix representation two new crossover operators were developed: the interchapter operator and the union operator. The interchapter operator constructs an offspring $O$ from parent $P _ { 1 }$ and $P _ { 2 }$ in the following way. First, for all $i , j \in \{ 1 , 2 , \ldots , n \}$ it defines

$$
o _ { i j } : = \left\{ \begin{array} { l l } { { 1 } } & { { \mathrm { i f } \ p _ { 1 , i j } = p _ { 2 , i j } = 1 , } } \\ { { } } & { { } } \\ { { 0 } } & { { \mathrm { o t h e r w i s e . } } } \end{array} \right.
$$

Second, some 1s which are unique for one of the parents are "added" to $O$ , and the matrix is completed with the help of an analysis of the sum of rows and columns, in such a way that the result is a legal tour. For example, the parent tours $2 - 3 - 1 - 4$ and $2 - 4 - 1 - 3$ which are represented by

$$
\left( \begin{array} { c c c c } { { 0 } } & { { 0 } } & { { 0 } } & { { 1 } } \\ { { } } & { { } } & { { } } & { { } } \\ { { 1 } } & { { 0 } } & { { 1 } } & { { 1 } } \\ { { } } & { { } } & { { } } & { { } } \\ { { 1 } } & { { 0 } } & { { 0 } } & { { 1 } } \\ { { } } & { { } } & { { } } & { { } } \\ { { 0 } } & { { 0 } } & { { 0 } } & { { 0 } } \end{array} \right) \mathrm { ~ a n d ~ } \left( \begin{array} { c c c c } { { 0 } } & { { 0 } } & { { 1 } } & { { 0 } } \\ { { } } & { { } } & { { } } & { { } } \\ { { 1 } } & { { 0 } } & { { 1 } } & { { 1 } } \\ { { } } & { { } } & { { } } & { { } } \\ { { 0 } } & { { 0 } } & { { 0 } } & { { 0 } } \\ { { } } & { { } } & { { } } & { { } } \\ { { 1 } } & { { 0 } } & { { 1 } } & { { 0 } } \end{array} \right) ,
$$

give after the first phase

$$
\left( \begin{array} { c c c c } { { 0 } } & { { 0 } } & { { 0 } } & { { 0 } } \\ { { } } & { { } } & { { } } & { { } } \\ { { 1 } } & { { 0 } } & { { 1 } } & { { 1 } } \\ { { } } & { { } } & { { } } & { { } } \\ { { 0 } } & { { 0 } } & { { 0 } } & { { 0 } } \\ { { } } & { { } } & { { } } & { { } } \\ { { 0 } } & { { 0 } } & { { 0 } } & { { 0 } } \end{array} \right) .
$$

This matrix can be completed in six different ways, since the only restriction on the offspring tour is that it starts in city 2. One possible offspring is the tour $2 - 1 - 4 - 3$ which is represented by:

$$
\left( \begin{array} { c c c c } { { 0 } } & { { 0 } } & { { 1 } } & { { 1 } } \\ { { } } & { { } } & { { } } & { { } } \\ { { 1 } } & { { 0 } } & { { 1 } } & { { 1 } } \\ { { } } & { { } } & { { } } & { { } } \\ { { 0 } } & { { 0 } } & { { 0 } } & { { 0 } } \\ { { } } & { { } } & { { } } & { { } } \\ { { 0 } } & { { 0 } } & { { 1 } } & { { 0 } } \end{array} \right) .
$$

The union operator divides the set of cities into two disjoint groups. See Fox and McMahon [19] for a special method of making this division. For the first group of cities the matrix elements of the offspring are taken from the first parent, for the second group they are selected from the second parent. The resulting matrix is completed by an analysis of the sum of the rows and columns. For example, consider again the two parents given above, and suppose that we divide the set of cities into $\{ 1 , 2 \}$ and $\{ 3 , 4 \}$ . Hence, after the first step of the union operator we have

$$
\left( \begin{array} { c c c c } { { 0 } } & { { 0 } } & { { x } } & { { x } } \\ { { } } & { { } } & { { } } & { { } } \\ { { 1 } } & { { 0 } } & { { x } } & { { x } } \\ { { } } & { { } } & { { } } & { { } } \\ { { x } } & { { x } } & { { 0 } } & { { 0 } } \\ { { } } & { { } } & { { } } & { { } } \\ { { x } } & { { x } } & { { 1 } } & { { 0 } } \end{array} \right) ,
$$

which might be completed to

$$
\left( \begin{array} { c c c c } { { 0 } } & { { 0 } } & { { 0 } } & { { 0 } } \\ { { } } & { { } } & { { } } & { { } } \\ { { 1 } } & { { 0 } } & { { 0 } } & { { 0 } } \\ { { } } & { { } } & { { } } & { { } } \\ { { 1 } } & { { 1 } } & { { 0 } } & { { 0 } } \\ { { } } & { { } } & { { } } & { { } } \\ { { 1 } } & { { 1 } } & { { 1 } } & { { 0 } } \end{array} \right) ,
$$

which represents the tour $4 - 3 - 2 - 1$ .

Fox and McMahon did not define a mutation operator.

• Seniw [54] had another approach. He defined the matrix element in the $i$ -th row and the $j$ -th column to be 1 if, and only if, in the tour city $j$ is visited inmediately after city $i$ . This implies that a legal tour is represented by a matrix of which each row and each column contains precisely one 1. We remark that a matrix which has precisely one 1 in each row and in each column does not necessarily represent a legal tour. For example, consider the matrices

$$
\left( \begin{array} { c c c c } { { 0 } } & { { 0 } } & { { 0 } } & { { 1 } } \\ { { } } & { { } } & { { } } & { { } } \\ { { 0 } } & { { 0 } } & { { 1 } } & { { 0 } } \\ { { } } & { { } } & { { } } & { { } } \\ { { 1 } } & { { 0 } } & { { 0 } } & { { 0 } } \\ { { } } & { { } } & { { } } & { { } } \\ { { 0 } } & { { 1 } } & { { 0 } } & { { 0 } } \end{array} \right) \mathrm { ~ a n d ~ } \left( \begin{array} { c c c c } { { 0 } } & { { 1 } } & { { 0 } } & { { 0 } } \\ { { } } & { { } } & { { } } & { { } } \\ { { 1 } } & { { 0 } } & { { 0 } } & { { 0 } } \\ { { } } & { { 0 } } & { { 0 } } & { { 1 } } \\ { { } } & { { } } & { { } } & { { } } \\ { { 0 } } & { { 0 } } & { { 1 } } & { { 0 } } \end{array} \right) ,
$$

where the first matrix represents the tour $2 - 3 - 1 - 4$ , and the second one the set of subtours $\left\{ 1 - 2 , 3 - 4 \right\} .$

Mutation is defined as follows: first several rows and columns are selected. The elements in the interchapters of these rows and columns are removed and randomly replaced, though in such a way that the result is a matrix of which each row and each column contains precisely one 1. For example, consider again the matrix representation of the tour $2 - 3 - 1 - 4$ and suppose that we select the first and the second row and the third and the fourth column.

First, the matrix elements in the interchapters of the rows and columns are removed. Hence,

$$
\left( \begin{array} { c c c c } { { 0 } } & { { 0 } } & { { x } } & { { x } } \\ { { } } & { { } } & { { } } & { { } } \\ { { 0 } } & { { 0 } } & { { x } } & { { x } } \\ { { } } & { { } } & { { } } & { { } } \\ { { 1 } } & { { 0 } } & { { 0 } } & { { 0 } } \\ { { } } & { { } } & { { } } & { { } } \\ { { 0 } } & { { 1 } } & { { 0 } } & { { 0 } } \end{array} \right) .
$$

Randomly replacing the elements may give

$$
\left( \begin{array} { c c c c } { { 0 } } & { { 0 } } & { { 1 } } & { { 0 } } \\ { { } } & { { } } & { { } } & { { } } \\ { { 0 } } & { { 0 } } & { { 0 } } & { { 1 } } \\ { { } } & { { } } & { { } } & { { } } \\ { { 1 } } & { { 0 } } & { { 0 } } & { { 0 } } \\ { { } } & { { } } & { { } } & { { } } \\ { { 0 } } & { { 1 } } & { { 0 } } & { { 0 } } \end{array} \right) .
$$

Note that this matrix does not represent a legal tour. The crossover operator which was defined creates an offspring $O$ from parents $P _ { 1 }$ and $P _ { 2 }$ as follows. First, for all $i , j \in \{ 1 , 2 , \dots , n \}$ it defines

$$
o _ { i j } : = \left\{ \begin{array} { l l } { { 1 } } & { { \mathrm { i f } \ p _ { 1 , i j } = p _ { 2 , i j } = 1 , } } \\ { { } } & { { } } \\ { { 0 } } & { { \mathrm { o t h e r w i s e . } } } \end{array} \right.
$$

Second, it alternately takes a 1 from one of the parents, which is unique for that parent, and changes the corresponding matrix element of the offspring from a 0 into a 1. Finally, if any rows in the offspring still do not contain a 1, 1s are added randomly, though in such a way that the result is a matrix which has precisely one 1 in each row and in each column. For example, the parent tours $2 - 3 - 1 - 4$ and $2 - 4 - 1 - 3$ , which are represented by

$$
\left( \begin{array} { c c c c } { { 0 } } & { { 0 } } & { { 0 } } & { { 1 } } \\ { { } } & { { } } & { { } } & { { } } \\ { { 0 } } & { { 0 } } & { { 1 } } & { { 0 } } \\ { { } } & { { } } & { { } } & { { } } \\ { { 1 } } & { { 0 } } & { { 0 } } & { { 0 } } \\ { { } } & { { } } & { { } } & { { } } \\ { { 0 } } & { { 1 } } & { { 0 } } & { { 0 } } \end{array} \right) \mathrm { ~ a n d ~ } \left( \begin{array} { c c c c } { { 0 } } & { { 0 } } & { { 1 } } & { { 0 } } \\ { { } } & { { } } & { { } } & { { } } \\ { { 0 } } & { { 0 } } & { { 0 } } & { { 1 } } \\ { { } } & { { } } & { { } } & { { } } \\ { { 0 } } & { { 1 } } & { { 0 } } & { { 0 } } \\ { { } } & { { } } & { { } } & { { } } \\ { { 1 } } & { { 0 } } & { { 0 } } & { { 0 } } \end{array} \right) ,
$$

may create the following offspring:

$$
\left( \begin{array} { c c c c } { { 0 } } & { { 0 } } & { { 0 } } & { { 1 } } \\ { { } } & { { } } & { { } } & { { } } \\ { { 0 } } & { { 0 } } & { { 1 } } & { { 0 } } \\ { { } } & { { } } & { { } } & { { } } \\ { { 0 } } & { { 1 } } & { { 0 } } & { { 0 } } \\ { { } } & { { } } & { { } } & { { } } \\ { { 1 } } & { { 0 } } & { { 0 } } & { { 0 } } \end{array} \right) ,
$$

which is again not a representation of a legal tour.

We have seen that the defined operators do not necessarily result in legal tours. It is possible that the operators convert the parent tour(s) into a collection of subtours. These subtours are allowed in the hope that natural clustering takes place. (However, subtours which contain less than $q$ cities are not allowed, where $q$ is a parameter.) After the execution of the genetic algorithm the best solution found is converted into a legal tour. This is done with the help of a deterministic algorithm which combines pairs of subtours.

•The last approach based on a binary matrix representation was proposed by Homaifar and Guan [28]. They used the same representation as Seniw [54], but in combination with different crossover and mutation operators. The crossover operators they used exchange all entries of the parent matrices either after a 1-point crossover or a 2-point crossover. Afterwards, an additional "repair algorithm" is run to assure that the result is a matrix of which each row and each column contains precisely one 1, and to connect any cycles to produce a legal tour. A 1-point crossover can be seen as follows. Consider the representations of the tours 1-2-3-4 and $4 - 3 - 2 - 1$ . These are

$$
\left( \begin{array} { c c c c } { { 0 } } & { { 1 } } & { { 0 } } & { { 0 } } \\ { { } } & { { } } & { { } } & { { } } \\ { { 0 } } & { { 0 } } & { { 1 } } & { { 0 } } \\ { { } } & { { } } & { { } } & { { } } \\ { { 0 } } & { { 0 } } & { { 0 } } & { { 1 } } \\ { { } } & { { } } & { { } } & { { } } \\ { { 1 } } & { { 0 } } & { { 0 } } & { { 0 } } \end{array} \right) \mathrm { ~ a n d ~ } \left( \begin{array} { c c c c } { { 0 } } & { { 0 } } & { { 0 } } & { { 1 } } \\ { { } } & { { } } & { { } } & { { } } \\ { { 1 } } & { { 0 } } & { { 0 } } & { { 0 } } \\ { { } } & { { 1 } } & { { 0 } } & { { 0 } } \\ { { 0 } } & { { 0 } } & { { 1 } } & { { 0 } } \\ { { } } & { { } } & { { } } & { { } } \end{array} \right) ,
$$

respectively. Suppose, that the crossover point is chosen between the second and the third column. Hence,

Crossover results in

$$
\left( \begin{array} { c c } { { 0 } } & { { 1 } } \\ { { 0 } } & { { 0 } } \\ { { 1 } } & { { 0 } } \\ { { 0 } } & { { 0 } } \\ { { 0 } } & { { 0 } } \end{array} \right) \left( \begin{array} { c c } { { 0 } } & { { 0 } } \\ { { 1 } } & { { 0 } } \\ { { 0 } } & { { 1 } } \\ { { 1 } } & { { 0 } } \end{array} \right) \left( \begin{array} { c c } { { 0 } } & { { 0 } } \\ { { 0 } } & { { 0 } } \\ { { 1 } } & { { 0 } } \\ { { 0 } } & { { 1 } } \\ { { 0 } } & { { 0 } } \end{array} \right) \left( \begin{array} { c c } { { 0 } } & { { 1 } } \\ { { 0 } } & { { 1 } } \\ { { 0 } } & { { 0 } } \\ { { 0 } } & { { 0 } } \\ { { 0 } } & { { 0 } } \end{array} \right) .
$$

$$
\left( \begin{array} { l l } { 0 } & { 1 } \\ { 0 } & { 0 } \end{array} \right) 0 \quad 1 \quad \left( \begin{array} { l } { 0 } \\ { 1 } \end{array} \right) \quad \left( \begin{array} { l l } { 0 } \\ { 0 } \end{array} \right) \quad 0 \quad 0 \quad \left( \begin{array} { l l } { 0 } \\ { 0 } \end{array} \right) \quad \left( \begin{array} { l l } { 0 } \\ { 0 } \end{array} \right) \quad \left( \begin{array} { l l } { 0 } \\ { 0 } \end{array} \right) \quad \left( \begin{array} { l l } { 0 } \\ { 0 } \end{array} \right) \quad \left( \begin{array} { l l } { 0 } \\ { 0 } \end{array} \right) \quad \left( \begin{array} { l l } { 0 } \\ { 0 } \end{array} \right) \quad \left( \begin{array} { l l } { 0 } \\ { 0 } \end{array} \right) \quad \left( \begin{array} { l l } { 0 } \\ { 0 } \end{array} \right) \quad \left( \begin{array} { l l } { 0 } \\ { 0 } \end{array} \right) \quad \left( \begin{array} { l l } { 0 } \\ { 0 } \end{array} \right) \quad \left( \begin{array} { l l } { 0 } \\ { 0 } \end{array} \right) \quad \left( \begin{array} { l l } { 0 } \\ { 0 } \end{array} \right) \quad \left( \begin{array} { l l } { 0 } \\ { 0 } \end{array} \right) \quad \left( \begin{array} { l l } { 0 } \\ { 0 } \end{array} \right) \quad \left( \begin{array} { l l } { 0 } \\ { 0 } \end{array} \right) \quad \left( \begin{array} { l l } { 0 } \\ { 0 } \end{array} \right) \quad \left( \begin{array} { l l } { 0 } \\ { 0 } \end{array} \right) \quad \left( \begin{array} { l l } { 0 } \\ { 0 } \end{array} \right) \quad \left( \begin{array} { l l } { 0 } \\ { 0 } \end{array} \right) \quad \left( \begin{array} { l l } { 0 } \\ { 0 } \end{array} \right) \quad \left( \begin{array} { l l } { 0 } \\ { 0 } \end{array} \right) \quad \left( \begin{array} { l l } { 0 } \\ { 0 } \\ { 0 } \end{array} \right) \quad \left( \begin{array} { l l } { 0 } \\ { 0 } \end{array} \right) \quad \left( \begin{array} { l l } { 0 } \\ { 0 } \\ { 0 } \end{array} \right) \quad \left( \begin{array} { l l } { 0 } \\ { 0 } \end{array} \right) = \left( \begin{array} { l l } { 0 } \\ { 0 } \\ { 0 } \end{array} \right) \quad \left( \begin{array} { l l } { 0 } \\ { 0 } \end{array} \right) 
$$

which of course do not represent legal tours.

A 2-point crossover works according to the same idea. Consider again the two parent tours given above, and suppose that we choose the first crossover point to be between the first and the second column, and the second to be between the third and the fourth column. Hence,

The result of the crossover is

$$
\begin{array}{c} { \begin{array} { r } { { \left( \begin{array} { l l } { 0 } \\ { 0 } \end{array} \right| } 1 } & { 0 } \\ { 0 } \\ { 0 } \end{array} } { \left( \begin{array} { l l } { 0 } \\ { 0 } \\ { 1 } \end{array} \right) } = { \left( \begin{array} { l l } { 0 } \\ { 0 } \end{array} \right) } = { \left( \begin{array} { l l } { 0 } \\ { 0 } \end{array} \right) } = { \left( \begin{array} { l l } { 1 } \\ { 0 } \\ { 1 } \end{array} \right) } =  \\ { 0 } \\ { 1 } \\ { 0 } \end{array}  = { \left( \begin{array} { l l } { 0 } \\ { 0 } \\ { 1 } \end{array} \right) } = { \left( \begin{array} { l l } { 0 } \\ { 0 } \\ { 0 } \end{array} \right) } = { \left( \begin{array} { l l } { 0 } \\ { 0 } \\ { 1 } \end{array} \right) } = { \left( \begin{array} { l l } { 0 } \\ { 0 } \\ { 0 } \end{array} \right) } = { \left( \begin{array} { l l } { 0 } \\ { 0 } \\ { 0 } \\ { 1 } \end{array} \right) } = { \left( \begin{array} { l l } { 0 } \\ { 0 } \\ { 0 } \\ { 0 } \end{array} \right) } .
$$

$$
\begin{array}{c} { \begin{array} { r c l } { { \left( { \begin{array} { c c c } { 0 } \\ { 0 } \end{array} } \right) } } & { 0 } & { 0 } \\ { 0 } & { 0 } & { 0 } \\ { 0 } & { 1 } & { 0 } \\ { 1 } & { 0 } & { 1 } \\ { 1 } & { 1 } & { 0 } \end{array} } { \left( \begin{array} { c } { 0 } \\ { 0 } \\ { 1 } \\ { 0 } \end{array} \right) }  & { { \mathrm { a n d ~ } } { \left( \begin{array} { c c c } { 0 } \\ { 0 } \\ { 1 } \\ { 1 } \end{array} \right) } } & { 0 } \\ { 0 } & { 0 } & { 0 } \\ { 0 } & { 0 } & { 0 } \\ { 0 } & { 0 } & { 0 } \end{array}  { \left( \begin{array} { c } { 1 } \\ { 1 } \\ { 0 } \\ { 0 } \\ { 0 } \end{array} \right) } ,
$$

which again do not represent legal tours.

The mutation operator used by Homaifar and Guan was heuristic inversion. This operator reverses the order of the cities between two randomly chosen cut points. If the distance between two cut points is large, the operator explores connections between "good" paths, otherwise the operator performs local search.

# Chapter 5

# Hybridization with Local Search

Evolutionary algorithms can be applied to problems of which very little knowledge is available. However, Grefenstette [26] showed that in many occasions it is possible to incorporate problemspecific knowledge in these algorithms. One example of incorporated knowledge we have already seen: the heuristic crossover operator (see Chapter 4.2.3 and Chapter 4.4.4).

Another opportunity to use problem-specific knowledge is in the determination of the initial population. The initial population can be chosen at random. However, it is also possible to start with a population which already has some quality. This is called seeding. Lawler et al. [32] and Johnson [30] described how a population of medium quality can be created. Note that seeding has to be done very carefully, since an evolutionary algorithm started with an initial population of little variety may quickly converge to a local optimum. Banzhaf [4] and Grefenstette [26] defined measures of the population variance. An algorithm which is frequently used for seeding is the 2-opt algorithm (Lin [35]).

While the evolutionary algorithms are not well suited for finely tuned local search, Goldberg [21] suggested crossing them with a local search algorithm. In this way the evolutionary algorithm searches for the "hills", and the local search algorithm climbs them. Several attempts have been done to implement Goldberg's suggestion, amongst others by Ackley [1]; Gorges-Schleuter [22]; Jog et al. [29]; Mühlenbein [41, 43]; Mühlenbein and Kindermann [42]; Mühlenbein et al. [39, 40]; Suh and Van Gucht [57] and Ulder et al. [59]. They all used algorithms of the following structure:

1. Construct a (random or seeded) initial population.

2. Apply local search to every individual of the initial population and replace every individual by the better individual (e.g. local optimum), which was reached by applying local search to it.

3. Create new individuals with the help of genetic operators and add them to the population.

4. Use local search to replace each new created individual in the current population by a better individual (e.g. local optimum).

5. Reduce the extended population to its original size in accordance with a selection criterion.

6. If not complied with a stop criterion: go to step 3.

The local search in the steps 2 and 4 may be performed with, e.g. the 2-opt algorithm (Lin [35]) or the Or-opt algorithm (Or [45] and Lawler et al. [32]). Ulder et al. [59] used a local search algorithm based on Lin and Kernighan neighbourhoods (Lin and Kernighan [36]). Lin et al. [37] even applied simulated annealing. They worked with neighbourhoods determined by the swapping strategies: random 2-exchange and locally adjacent swap. Also a combination of different local search techniques may be chosen: Prinetto et al. [46] applied in every generation Or-opt, 2-opt, and Group Optimization with a probability of 0.5, 0.3 and 0.2 respectively. They also used a combination of several crossover operators.

Instead of using local search in every iteration of an evolutionary algorithm it is also possible to wait until it can be expected that the algorithm has reached an interesting area. Another possibility is to perform local search only when the evolutionary algorithm has terminated. Mühlenbein and Gorges-Schleuter developed a parallel genetic algorithm based on the above described structure (Gorges-Schleuter [22]; Mühlenbein [41, 43] and Mühlenbein et al. [39, 40]). They called their algorithm ASPARAGOS (ASynchronous PARAllel Genetic Optimization Strategy). Another parallel genetic algorithm for the Travelling Salesman Problem is described in Fogel [15].

# Chapter 6

# Conclusions

We have considered several representations and operators which may be used in evolutionary algorithms meant to solve the Travelling Salesman Problem. The first representation at which we looked was the binary representation. This representation might be useful for small problem instances of the TSP. However, for larger problem instances the binary strings which represent the tours become unmanageably large. Another disadvantage of the binary representation is that the classical operators do not necessarily result in legal offspring tours; repair algorithms would be necessary.

The second representation considered was the adjacency representation. We saw that for this representation several crossover operators were developed. However, unfortunately all the described crossover operators give a low performance. The created offspring does not inherit enough adequate information from its parents.

The third representation which we described was the ordinal representation. The advantage of this representation is that the classical operators can be used. However, it gives poor results. The last but one representation described, was the path representation. This representation can be seen as the most natural of those considered. It is also used most often, and a large variety of operators have been developed for it. These operators try to pass on two types of information to the offspring: the absolute position of the cities in the parent tours and the relative order of the cities in the parent tours. Some operators, e.g. the CX operator and the position based operator, pay most attention to the former type of information transfer. Other operators, e.g. the order based operator, the ER operator and the heuristic operator, pay more attention to the latter type. Since the TSP searches for a cycle of which the cost is independent of the chosen starting city, it can be expected that information about the relative order of the cities is more important to pass on than the information about the absolute position of the cities.

Few results can be found on the comparison of the performance of the different operators. This is, amongst other reasons, because of the fact that, for most operators, schemata analysis is quite difficult. Some results can be found. Oliver et al. [44] concluded from theoretical and empirical results that the OX operator is better than the PMX operator and that the PMX operator is better than the CX operator. Grefenstette et al. [23] showed that it was better to use a heuristic crossover operator. However, Whitley et al. [60, 61] showed that their ER operator worked even better than the heuristic crossover operator.

The last representation to which we paid attention was the matrix representation. In fact we did not consider one matrix representation, but two: the representation used by Fox and McMahon, and the representation used by Seniw and by Homaifar and Guan. A main difficulty using these matrix representations is to define operators which lead to legal offspring. In both the approaches of Seniw and Homaifar and Guan, additional repair algorithms are necessary to assure that the offspring is a legal tour.

Although it might be a bit out of the range of this report, we also spent a few words on the hybridization of an evolutionary algorithm with local search. We did this since for the creation of a good evolutionary algorithm it seems to be inevitable to include local search techniques.

# Bibliography

[1] AcKLEY, D.H. (1987), A Connectionist Machine for Genetic Hillclimbing, Kluwer Academic Publishers.

[2] AMBATI, B.K., AMBATI, J. AND MoKHTAR, M.M. (1991), Heuristic Combinatorial Optimization by Simulated Darwinian Evolution: a Polynomial Time Algorithm for the Traveling Salesman Problem, Biological Cybernetics, 65, pp. 31-35.

[3] BÄCK, T., HOFFMEISTER, F. AND ScHWEFEL, H.-P. (1991), A Survey of Evolution Strategies, in: [5], pp. 2-9.

[4] BANzHAF, W. (1990), The "Molecular" Traveling Salesman, Biological Cybernetics, 64, pp. 7-14.

[5] BELEW, R. AND BooKER, L. (EDS.) (1991), Proceedings on the Fourth International Conference on Genetic Algorithms, Morgan Kaufmann Publishers, Los Altos, CA.

[6] BEYER, H.G. (1992), Some aspects of the 'Evolution Strategy' for Solving TSP-Like Optimization Problems Appearing at the Design Studies of the $0 . 5 T e V e ^ { + } e ^ { - }$ -Linear Collider, in: R. Männer and B. Manderick (Eds.), Parallel Problem Solving From Nature 2, North-Holland, Amsterdam, pp. 461-370.

[7] BRADY, R.M. (1985), Optimiztion Strategies Gleaned From Biological Evolution, Nature, 317, pp. 804-806.

[8] BREMERMANN, H.J., ROGSON, M. AND SALAFF, S. (1965), Search by Evolution, in: M. Maxfield, A. Callahan and L.J. Fogel (Eds.), Biophysics and Cybernetic Systems, Spartan Books, Washington, pp. 157-167.

[9] DAVIs, L. (1985), Applying Adaptive Algorithms to Epistatic Domains, Proceedings of the International Joint Conference on Artificial Intelligence, pp. 162-164.

[10] DAVIs, L. (ED.) (1991), Handbook of Genetic Algorithms, Van Nostrand Reinhold, New York.

[11] FoGEL, L.J. (1962), Atonomous Automata, Ind. Res. 4, pp. 14-19.

[12] FoGEL, L.J. (1964), On the Organisation of the Intellect, Ph.D. Dissertation, UCLA.

[13] FOGEL, L.J., OwENS, A.J. AND WALSH, M.J. (1966), Artificial Intelligence through Simulated Evolution, Wiley, New York.

[14] FoGEL, D.B. (1988), An Evolutionary Approach to the Traveling Salesman Problem, Biological Cybernetics, 60, pp. 139-144.

[15] FoGEL, D.B. (1990) A Parallel Processing Approach to a Multiple Traveling Salesman Problem Using Evolutionary Programming, in: L. Canter (Ed.), Proceedings on the Fourth Annual Parallel Processing Symposium, Fullerton, CA, pp. 318-326.

[16] FoGEL, D.B. (1991) , System Identification Through Simulated Evolution: A Machine Learning Approach to Modeling, Ginn Press, Needham, MA.

[17] FoGEL, D.B. (1992), Evolving Artificial Intelligence, Doctoral Dissertation, UCSD.

[18] FoGEL, D.B. (1993), Applying Evolutionary Programming to Selected Traveling Salesman Problems, Cybernetics and Systems, 24, pp. 27-36.

[19] FoX, M.S. AND McMAHON, M.B. (1987), Genetic Operators for Sequencing Problems, in: G. Rawlings, Foundations of Genetic Algorithms: First Workshop on the Foundations of Genetic Algorithms and Classifier Systems, Morgan Kaufmann Publishers, Los Altos, CA, pp. 284-300.

[20] GoLDBERG, D.E. AND LINGLE, JR., R. (1985), Alleles, Loci and the TSP, in: [24], pp. 154-159.

[21] GoLDBERG, D.E. (1989), Genetic Algorithms in Search, Optimization and Machine Learning, AddisonWesley, Reading, MA.

[22] GoRGEs-ScHLEUTER, M. (1989), ASPARAGOS An Asynchronous Parallel Genetic Optimization Strategy, in: [49], pp. 422-427.

[23] GREfENsTETTE, J., GoPAL, R., RosMAITA, B. AND VAN GUCHT, D. (1985), Genetic Algorithms for the TSP, in: [24], pp. 160-165.

[24] GREFENsTETTE, J.J. (ED.) (1985), Proceedings of the First International Conference on Genetic Algorithms and Their Applications, Lawrence Erlbaum, Hillsdale, New Yersey.

[25] GREFENsTETTE, J.J. (ED.) (1987), Genetic Algorithms and Their Applications: Proceedings of the Second International Conference, Lawrence Erlbaum, Hillsdale, New Yersey.

[26] GREFENsTETTE, J.J. (1987), Incorporating Problem Specific Knowledge into Genetic Algorithms, in: L. Davis (Ed.), Genetic Algorithms and Simulated Annealing, Morgan Kaufmann, Los Altos, CA, pp. 42-60.

[27] HoLLAND, J. (1975), Adaptation in Natural and Artificial Systems, University of Michigan Press, Ann Arbor.

[28] HoMAIFAR, A. AND GUAN, S. (1991), A New Approach on the Traveling Salesman Problem by Genetic Algorithm, Technical Report, North Carolina A & T State University.

[29] JOG, P., SUH, J.Y. AND VAN GuCHT, D. (1989), The Effects of Population Size, Heuristic Crossover and Local Improvement on a Genetic Algorithm for the Traveling Salesman Problem, in : [49], pp. 110-115.

[30] JoHNsoN, D.S. (1990), Local Optimization and the Traveling Salesman Problem, Proc. 17th Colloq. Automata, Languages and Programming, Springer-Verlag.

[31] KIRKPATRICK, S., GELATT, C.D. AND VECCHI, M.P. (1983), Optimization by Simulated Annealing, Science, 220, pp. 671-680.

[32] LAWLER, E.L., LENSTRA, J.K., RINNOOY KAN, A.H.G. AND SHMOYS, D.B. (EDs.) (1985), The Traveling Salesman Problem: A Guided Tour of Combinatorial Optimization, Wiley, Chichester.

[33] LIDD, M.L. (1991), The Traveling Salesman Problem Domain Application of a Fundamentally New Approach to Utilizing Genetic Algorithms, Technical Report, MITRE Corporation.

[34] LIEPINS, G.E., HILLIARD, M.R., PALMER, M. AND MoRROW, M. (1987), Greedy Genetics, in: J.J. Grefenstette (Ed.), in: [25], pp. 90-99.

[35] LIN, S. (1965), Computer Solutions on the Travelling Salesman Problem, Bell Systems Techn. J., 44, pp. 2245-2269.

[36] LIN, S. AND KERNIGHAN, B.W. (1973), An Effective Heuristic Algorithm for the Traveling Salesman Problem, Operations Research, 21, pp. 498-516.

[37] LIN, F.-T, KAO, C.-Y. AND HsU, C.-C. (1993), Applying the Genetic Approach to Simulated Annealing in Solving NP-Hard Problems, IEEE Transactions on Systems, Man, and Cybernetics, Vol. 23, No. 6, pp. 1752-1767.

[38] MICHALEWICZ, Z. (1992), Genetic Algorithms $^ +$ Data Structures $=$ Evolution Programs, Springer Verlag, Berlin Heidelberg.

[39] MÜHLENBEIN, H., GORGES-SCHLEUTER, M. AND KRÄMER, O. (1987), New Solutions to the Mapping Problem of Parallel Systems: The Evolution Approach, Parallel Computing, 4, pp. 269-279.

[40] MÜHLENBEIN, H., GoRGES-SCHLEUTER, M. AND KRÄMER, O. (1988), Evolution Algorithms in Combinatorial Optimization, Parallel Computing, 7, pp. 65-85.

[41] MüHLENBEIN, H. (1989), Parallel Genetic Algorithms, Population Genetics and Combinatorial Optimization, in: [49], pp. 416-421.

[42] MÜHLENBEIN, H. AND KINDERMANN, J. (1989), The Dynamics of Evolution and Learning - Towards Genetic Neural Networks, in: J. Pfeiffer (Ed.), Connectionism in Perspectives.

[43] MÜHLENBEIN, H. (1991), Evolution in Time and Space - The Parallel Genetic Algorithm, in: G. Rawlins (Ed.), Foundations of Genetic Algorithms, Morgan Kaufmann, Los Altos, CA.

[44] OLIVER, I.M., SMITH, D.J. AND HoLLAND, J.R.C. (1987), A Study of Permutation Crossover Operators on the TSP, in: [25], pp. 224-230.

[45] OR, I. (1976), Travelling Salesman-Type Combinatorial Problems and Their Relation to the Logistics of Regional Blood Banking, PhD Thesis, Northwestern University.

[46] PRINETTO, P., REBAUDENGO, M. AND SONZA REORDA, M. (1993), Hybrid Genetic Algorithms for the Traveling Salesman Problem, in: R.F. Albrecht, C.R. Reeves and N.C. Steele (Eds.), Artificial Neural Nets and Genetic Algorithms, Springer-verlag, Wien, pp. 559-566.

[47] RECHENBERG, I. (1973), Optimierung Technischer Systeme Nach Prinzipien der Biologischen Information, Frommann Verlag, Stuttgart.

[48] REINELT, G. (1991), TSPLIB - A Traveling Salesman Library, ORSA Journal on Computing, Vol. 3, No. 4, pp. 376-384.

[49] ScHAFFER, J. (ED.) (1989), Proceedings on the Third International Conference on Genetic Algorithms, Morgan Kaufmann Publishers, Los Altos, CA.

[50] ScHwEFEL, H.-P (1975), Evolutionsstrategie und Numerische Optimierung, Doctoral Thesis Diss. D 83, TU Berlin.

[51] ScHwEFEL, H.-P (1977), Numerische Optimierung von Computer-Modellen Mittels der Evolutionsstrategie, Birkhäuser, Basel.

[52] ScHwEFEL, H.-P (1981), Numerical Optimization for Computer Models, Wiley, Chichester, UK.

[53] SCHwEFEL, H.-P (1987), Collective Phenomena in Evolutionary Systems, in: P. Checkland and I. Kiss (Eds.), Proceedings of the 31th Annual Confrence on Problems of Constancy and Change of the International Society for General System Research, Budapest, pp. 1025-1032.

[54] SENIw, D. (1991), A Genetic Algorithm for the Traveling Salesman Problem, MSc Thesis, University of North Carolina at Charlotte.

[55] SPEARs, W.M. (1993), Crossover or Mutation?, in: L.D. Whitley (Ed.), Foundations of Genetic Algorithms 2, Morgan Kaufmann, San Mateo, CA, pp. 221-234.

[56] STARKWEATHER, T., McDANIEL, S., MATHIAS, K., WHITLEY, C. AND WHITLEY, D. (1991), A Comparison of Genetic Sequencing Operators, in: [5].

[57] SUH, J.Y. AND VAN GUCHT, D. (1987), Incorporating Heuristic Information into Genetic Search, in: [25], pp. 100-107.

[58] SyswERDA, G. (1991), Schedule Optimization Using Genetic Algorithms, in: [10], pp. 332-349.

[59] ULDER, N.L.J., AARTS, E.H.L., BANDELT, H.-J., VAN LAARHOVEN, P.J.M., AND PESCH, E. (1990), Genetic Local Search Algorithms for the Traveling Salesman Problem, in: Parallel Problem Solving from Nature, Springer-Verlag, Berlin Heidelberg, pp. 106-116.

[60] WHITLEY, D., STARKWEATHER, T. AND D'ANN FUQUAY (1989), Scheduling Problems and Travelling Salesman: The Genetic Edge Recombination Operator, in: [49], pp. 133-140.

[61] WHITLEY, D., STARKWEATHER, T. AND SHANER, D. (1991), The Traveling Salesman and Sequence Scheduling: Quality Solutions Using Genetic Edge Recombination, in: [10], pp. 350-372.