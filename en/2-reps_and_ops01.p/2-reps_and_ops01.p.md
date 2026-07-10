James Marshall

# Representations - Sparseness

# Representations - Sparseness

I Recall that the SGA uses binary chromosomes   
I As we know, anything that can be represented, can be represented in binary I To some arbitrary precision   
I Is binary always the best way to encode solutions?

Consider the following example I Problem - find the largest integer in 0, 1, . . . , 8 { }Encoded as standard binary the fitness function is

<table><tr><td>Chromosome</td><td>Fitness</td></tr><tr><td>0000</td><td>0</td></tr><tr><td>0001</td><td>1</td></tr><tr><td>0010</td><td>2</td></tr><tr><td>0011</td><td>3</td></tr><tr><td>0100</td><td>4</td></tr><tr><td>0101</td><td>5</td></tr><tr><td>0110</td><td>6</td></tr><tr><td>0111</td><td>7</td></tr><tr><td>1000</td><td>8</td></tr><tr><td>1001</td><td>undefined</td></tr><tr><td>1010</td><td>undelined</td></tr><tr><td>1011</td><td>undefined</td></tr><tr><td>1100</td><td>undefined</td></tr><tr><td>1101</td><td>undefined</td></tr><tr><td>1110</td><td>undelined</td></tr><tr><td></td><td></td></tr></table>

I The problem with the encoding in the previous example is fairly obvious   
I The encoding is very sparse I Nearly 50% of chromosomes encode invalid solutions to the problem   
This will seriously hamper the efficiency of the GA's search   
I A less sparse encoding would be in base 3 I 2 genes, each with 3 alleles 32 = 9 →all chromosomes are valid solutions

# Representations

# Representations - Discontinuity

# Representations - Gray Coding

I Consider the following example I Problem - find the largest integer in 0, 1, . . . , 15 {      }I Encoded as standard binary the fitness function is

<table><tr><td>Chromosom</td><td>Fitness</td></tr><tr><td>0000</td><td>0</td></tr><tr><td>0001</td><td>1</td></tr><tr><td>0010</td><td>2</td></tr><tr><td>0011</td><td>3</td></tr><tr><td>0100</td><td>4</td></tr><tr><td>0101</td><td>5</td></tr><tr><td>0110</td><td>6</td></tr><tr><td>0111</td><td>7</td></tr><tr><td>1000</td><td></td></tr><tr><td>1001</td><td>9</td></tr><tr><td>1010</td><td>10</td></tr><tr><td>1011</td><td>11</td></tr><tr><td>1100</td><td>12</td></tr><tr><td>1101</td><td>13</td></tr><tr><td>1110</td><td>14</td></tr><tr><td>1555</td><td>15</td></tr></table>

I A further problem with the standard binary encoding used in the previous example is less obvious   
I The ‘Hamming distance’ between chromosomes encoding adjacent integers is not constant I Hamming distance is the number of genes at which two chromosomes have different alleles   
I Chromosomes that differ in only one or two bits may encode for substantially different solutions 0000 0 vs. 1000 9   
→    → I Chromosomes that differ in all bits may encode for very similar solutions 1000 →9 vs. 0111 → 8   
I N.B. The relationship between chromosome and solution is known as the genotype-phenotype mapping I Again, the terminology is directly taken from biology

I One proposed solution is to use a ‘Gray code’ Under binary reflected Gray coding the fitness function is

James all

<table><tr><td>Chromosome</td><td>Fitness</td></tr><tr><td>0000</td><td>0</td></tr><tr><td>0001</td><td></td></tr><tr><td>0011</td><td>2</td></tr><tr><td>0010</td><td>33</td></tr><tr><td>0110</td><td>4</td></tr><tr><td>0111</td><td>5</td></tr><tr><td>0101</td><td></td></tr><tr><td>0100</td><td></td></tr><tr><td>1100</td><td>8</td></tr><tr><td>1101</td><td>9</td></tr><tr><td>1111</td><td>10</td></tr><tr><td>1110</td><td>11</td></tr><tr><td>1010</td><td>12</td></tr><tr><td>1011</td><td>13</td></tr><tr><td>1001</td><td>14</td></tr><tr><td>1000</td><td>15</td></tr></table>

# Representations - Gray Coding

I Now adjacent integers are encoded by chromosomes that only differ in one gene   
I This seems like an improvement over traditional binary encoding   
I But how much of an improvement is it really?   
I For example, what are the average effects of a single point mutation under both encoding schemes? I Exercise: calculate the expected deviation in encoded integer resulting from a single uniformly selected point mutation in a 4-gene binary chromosome, under standard and Gray binary encodings. Also calculate the variance of the expectation. Write a computer program to help you if necessary.   
I Crossover is likely to be much more disruptive than mutation under either encoding I Exact calculation of expected disruption would be much more involved though...

# Representations - Permutation and Grouping Problems

I The comparison between standard and Gray binary encoding is illustrative of a general point I Careful selection of a representation appropriate to the optimisation problem is reguired   
I ‘Function-based’ problems are not the only optimisation problems   
I Other very important classes of problems are ‘permutation’ and ‘grouping’ problems I These problems have very different characteristics to function-based problems I They include problems such as I Route optimisation (e.g. Travelling Salesman Problem) I Sequence optimisation (e.g. Job Shop Scheduling Problem) I Payload optimisation (e.g. Bin Packing Problem)

# Representations - Permutation and Grouping Problems

I Permutation and grouping problems typically suffer from very sparse genotype-phenotype mappings I Many genotypes do not encode valid solutions   
I Consider a simple encoding for the 5-city Travelling Salesman Problem (TSP) I Solutions are permutations on the set of cities A, B, C, D, E e.g. (A. C.D.E.B) h    i I Solutions must be permutations (i.e. every element in the set appears exactly once) I Adjacent genes in the chromosome must have alleles representing adjacent cities in the TSP graph   
I The encoding is also highly redundant I Mathematically, the function mapping the genotype set to the phenotype set is not injective (one-to-one) (A. C. D. E, B) is the same solution as (C. D. E. B, A), which is the same h ias D E B A C , etc. h , , , , i  I Assuming an undirected graph gives even higher redundancy

# Representations - Permutation and Grouping Problems

# Representations - Permutation and Grouping Problems

I For grouping problems, solutions represent an allocation of items to sets   
I For example the bin-packing problem I Items of different weights are allocated to bins of fixed capacity I Objective function to be minimised is number of bins used   
I All items must appear in the solution exactly once I Items cannot appear in multiple bins I Items cannot appear in the same bin more than once   
I A solution can be thought of as a permutation, which we can decode using a simple heuristic Put each item into the first empty bin in which it will fit, or a new bin if no such bin exists   
I A simple permutation encoding will be very sparse and redundant I E.g. 1 3 2 4 5 6 is the same solution as 2 1 3 6 4 5   
I Sparseness and redundancy mean simple crossover is highly destructive I E.g. for the TSP example A, C, D, E, B crossed with D, A, B, E, C h    i  using 1X is guaranteed to result in an invalid solution Similary (A. C. D.E. B) crossed with (C. D.E,B.A) using 1X results in h    i   h    i    an invalid solution, even though both original chromosomes encode the same solution   
I Similarly, a single point mutation is guaranteed to result in an invalid solution   
I Redundancy and the destructive effects of operators will make the GA’s search very inefficient   
I Exercise: For a problem whose solutions are permutations of 5 objects, what proportion of chromosomes encoded using one gene per position in the permutation are valid solutions? Derive a general expression for encodings with \` genes and alleles

# Operators - Crossover Bias

# Operators - Multipoint Crossover

# Operators - Uniform Crossover

Crossover is often considered to be the defining feature of a GA and the source of its power   
Single point crossover (1X) is not the only possible crossover operator   
It is worth examining the bias' of the 1X operator I Consider what happens when we apply 1X to the chromosome a , a , . . . , a iThe probability that alleles at two different genes both end up in the same offspring chromosome together strongly depends on the distance (number of other genes) between them I In particular, note that 1X as described in the previous lecture means than a and a will never end up in the same offspring chromosome together I 1X exhibits strong positional bias   
I On the other hand, 1X has no distributional bias The crossover point is uniformly selected   
I There is no particular reason to only have a single crossover point   
We can define an m-point crossover operator MX I m crossover points selected uniformly without replacement I Sampling without replacement necessary to ensure exactly m points are selected I Crossover points works in exactly the same way as 1X

I Multipoint crossover reduces positional bias

I To remove any positional bias we can make crossover completely random

I Uniform crossover

During recombination, a (weighted) coin is tossed for each gene, to se which parent the offspring should receive its allele from   
I.e. we generate a crossover mask by sampling from a Bernoulli distribution E.g. 1010001 where 1 indicates first parent contributes the allele, and 0 indicates second parent   
I We can vary the Bernoulli parameter p in (0, 0.5] to make crossover more or less like clonal reproduction

Exercise: Calculate the probability of two alleles with / genes between them, on a parental chromosome of length \`, ending up together in the same offspring chromosome, for 1X, for 2X, and for UX with arbitrary p (assume two offspring are created by the crossover operators)

# Operators - Nonlinear Crossover

I All the crossover operators we’ve looked at so far can be thought of as linear   
I As we’ve seen for permutation problems, linear crossover is inappropriate   
I One solution is partially matched crossover (PMX) Uniformly select two crossover points between 1 and / - 1 Genes between these crossover points specify an interchange mapping For the genes between the crossover points we specify mappings between Fhor the enes beteen the ossover ont we spe i ↔ i I We rewrite the chromosomes of both parents using these mappings to produce teo offspring chromosomes I What should happen if the same gene appears in more than one mapping?

# Operators - Mutation

I Simple mutation on binary chromosomes is straightforward I Per gene probability of bit-flipping µ   
I We may also choose to have a constant number of mutations per chromosome   
What about higher cardinality allelic alphabets? We may sample uniformly from the other possible alleles I Or it might make more sense to make small mutations frequent and large mutations rare I Should assign zero probability of sampling the current allele, to ensure mutation really does occur I I.e. weight probability of mutation to any allele by the absolute difference from the current allele   
I How can we design a mutation operator for permutation problems? I Recall that single point mutation is guaranteed to result in an invalid solution

# Operator Implementation

I Design of operators is crucial for GA’s search performance   
I Efficient implementation of operators is also important for run-time performance These operators are going to be applied very many times during GA execution   
I As with most algorithms, there are typically naive inefficient¨ implementations, and clever efficient ones   
I For example operators can be implemented with bit masks   
I Mutation (binary chromosomes only) I a m   
I Linear crossover (arbitrary vector chromosomes) I m a m b   
I Where m is the operator binary mask, m is its complement, a and b are chromosomes, and $\otimes$ and are component-wise multiplication ⊗and addition respectively

# Operator Implementation

I For binary chromosomes these operations can be performed exceedingly efficiently using bitwise AND and XOR operations   
I The mask can typically be generated efficiently as well I For mutation and crossover we could start with a binary string of 0s I For each bit we then set it to one by sampling from a Bernoulli distribution with appropriate p I This is inefficient for long strings though We could do it more efficiently... I The number of expected successes n in N Bernoulli trials is given by sampling from a binomial distribution I We start with the 0s string as before We sample our number of mutations/crosses n from Po(nj() p | I We uniformly sample (without replacement) n points on the string and set those bits to 1 I As the mean number of successful Bernoulli trials is p our approach is \`   roughly 1 -times more efficient (assuming efficient uniform and binomial p      sampling, reasonable given for long strings E(n) \`)