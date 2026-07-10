# Constrained Optimisation Problems

I Many optimisation problems have inherent constraints on their solutions

I For such problems, not all solutions are valid

I We have already seen examples of this for permutation-based problems such as TSP

For < obiects. not all strings of length < are valid solutions Only those which are permutations of all objects are valid I        \`I The proportion of valid strings is hence \`!

\` \` I Various approaches to these kinds of problems have been proposed, particularly

I Penalties   
Repair   
I Multiple objectives   
Modified representations, operators and problem formulations

# Penalties

One solution to the generation of non-viable individuals is to implement some form of penalty   
I The ultimate ‘death-penalty’ is to exclude them from the population I However, it is common to find the global optimum in the vicinity of a constraint boundary I Ignoring the degree of infeasibility of a solution discards some information

I Alternatively, we can modify the objective function by including a penalty function

The penalty function should be based on distance from a constraint boundary I E.g. number of constraints violated, and amount violated by If penalties are too small, many non-viable solutions may spread in the population If penalties are too large, the search will be too conservative and prevented from exploring the search space near its contraint boundaries

# Repair

# Multiple Objectives

# Modified Representations, Operators and Formulations

I Another strategy for dealing with non-viable offspring is to repair them before insertion into the population   
I Repair operators will be problem and representation specific, but might include I Allele substitution to repair a ‘fatal’ mutation Repair around a crossover site that has resulted in a non-viable solution   
I We can either insert the original or repaired version of the offspring into the population I Inserting the repaired version may be too conservative by limiting search near a constraint boundary   
I We can also tackle constrained optimisation as a multiobjective optimisation problem I Maximise objective fitness Minimize unftness (infeasability)   
Using a multiobective GA we can find a non-dominated set of solutions   
with varying degrees of compromise between fitness and infeasability   
I This approach assumes that: I We can assign a meaningful objective fitness to infeasible solutions We can meaningfully measure the extent to which the ontimisatior problem’s constraints have been violated   
I Good results are likely to be obtained by tailoring the GA to the problem at hand   
We can modify I Representations (encodings) Genetic operators The problem formulation itself   
One example of this was shown in lecture 2 for permutation problems, such as the TSP Partially Matched Crossover (PMX)   
Let us now look at modified approaches to grouping problems

# Object Membership

# Context Insensitivity in Membership Encoding

I Grouping problems are those in which objects must be assigned membership of different groups I E.g. the bin-packing problem (BPP) I For a set of objects having different weights, and a supply of bins of fixed size, find the assignment of objects to bins that minimises the number of hins needed   
I Grouping problems can be formulated in two obvious ways I Object membership Object permutation   
I We will now look at drawbacks of these two approaches

I The object membership representation encodes each solution using one locus per object, and one allele per group

# AACBAB

I Encodes a solution with six objects assigned to three groups, A, B and C

Such an encoding is clearly highly redundant E.g. AACBAB and BBACBC both encode solutions where the same objects are assigned to the same groups

o suffers from context insensitivityunder crossover

I Object membership encoding disregards the context of group membership under standard crossover operators E.a. consider two-point crossover performed on the individuals

A|BC|ADD and C|AD|CBB

These individuals encode identical solutions to the problem, in which objects 1 and 4, and 5 and 6 are grouped together I Applying 2X at the marked crosspoints gives one of the offspring as

# CBCCBB

I This individual differs completely from both its parents, despite the parents being identical to each other

# Object Permutation

I Alternatively we can represent a solution to an object grouping problem as a permutation of the objects   
I A heuristic is then used to decode the permutation I E.g. for each object in the chromosome, put it into the first bin in which it will fit, or in a new bin if no such bin exists   
I As with membership encoding, permutation encoding is highly redundant   
I E.g. the three individuals

3210|45678|9   
0123|87654|9   
87645|1032|9

all encode the same solution

# Context Insensitivity in Permutation Encoding

I Permutation encoding also suffers from context insensitivity I As a solution is decoded from left to right, assignment of objects to groups depends on the objects that have appeared earlier in the chromosome I Hence changing the objects encoded earlier in the chromosome may disrupt groups of objects encoded later in the chromosomes I E.g. simply swapping the first and third bin contents in the encoded solution, where sufficient space remains in the third bin to fit object 3

results in the radicaly different solutior

7893|4560|12

# The Grouping Genetic Algorithm - Encoding

I The Grouping Genetic Algorithm (GGA) manipulates groups rather than individual objects   
I The first major innovation is the encoding   
I The standard object membership encoding is extended with a group part, based on one gene for one group, e.g.

# ADBFEB:BEFDAAAABBB:AB

I The group part identifies the groups present in the solution, the object part assigns individual objects into these groups I As the number of groups is not normally predetermined in a grouping problem, chromosomes will be of variable length

# The Grouping Genetic Algorithm - Operators

# The Grouping Genetic Algorithm - Crossover

James Marshall COMSM0302 : Evolutionary Computing

The Grouping Genetic Algorithm - Operators

I The GGA operators work with the group part of the chromosome I The group labels of the objects indicate which objects should be considered when manipulating a particular group I Operators explicitly manipulate groups of objects, rather than independent objects I Operators must work with variable length chromosomes

for both parents do uniformly randomly select two crosspoints within group part of chromoome;   
end   
for 1 to 2 do create clone offspring of first parent with same crosspoints; inject first crossing section of second parent at first crosspoint of offspring; for all objects occuring twice in offspring do delete object from group in offspring in which object originally resided; end apply problem-dependent heuristics to satisfy constraints; swap first and second parent roles;   
end   
I Standard mutation is too destructive for grouping problems   
I Hence a problem-specific mutation operator must be designed, which might I Create a new group I Eliminate an existing group I Shuffle objects among groups   
I Inversion can be applied without modification to the group part of chromosomes in the GGA

# Formae and Respect

I The GGA embodies the principles of forma and respect

I A subset of chromosomes that are similar in some, typically phenotypic, way

I Respect

I Operators should respect the formae of the chromosomes on which they operate I Phenotypic characteristics should largely be transmitted intact I If parents share a particular characteristic, their offspring should inherit it

I These ideas capture a crucial aspect of GA design Careful design of representation and operators, using knowledge of the problem domain

I Forma can be compared with the original explanation for how GAs work, schema theory, which we will cover later in the course