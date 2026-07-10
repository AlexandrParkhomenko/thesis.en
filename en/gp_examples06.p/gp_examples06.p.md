Let us look at an example application of GP, eaming a multiplexer   
Multiplexers are a class of addressing problems Instances have k 'address' bits, followed by 2 'data' bits The address bits index a bit in the data bits, and the class of the instance is the value of that bit The 11-multiplexer has 11-bit instances, of 3 address bits plus 2³ data bits, e.g. 01001011011  Class 0 10101011011  Class 1 00001010011  Class 0 01101010011  Class ? 10001010011  Class?

Te frst step is to chos the fncin and terml sts

Terminal set

in the problem T = (A0, A1,A2, D0, D1, D2, D3, D4, D5, D6, D7}

Function set

Choosing the function set is slightly more interesting As the multiplexer is a boolean function we choose some boolean operators F = {^, V,¬,F} input to any function, and all functions are defined fr both of these values

# GP Example - Learning the 11-Multiplexer

#

We also need to select a fitness function W l  f   i il a • Raw fitness therefore varies between 0 and 2048   
Hence we are using GP to perform function approximation, or concept learning on the 1-multiplexer • This contrasts with the traditional Machine Learning problem of predicting the classes of new unseen instances (generalisation)   
After 9 generations the best individual so far correctly classifies all fitness cases IFAD0 (IF A2 (IF A1D7 (IF A0 D5 DO) (IF AD (IF A1 (IF A2 D7 D3) D1) DO)) (IF A2 (IF A1 D6 D4) (IF A2 D4 (IF A1 D2 (IF A2 D7 DI)))   
This is rather hard for a human to parse in their head…   
We can simplify it by applying an editing operation, to give the logically equivalent (IF AD (IF A2 (IF A1 D7 D5) (IF A1 D3 D1) IF A2 (IF A1 D6 D4) (IF A1 D2 DO))

Editing is an asexual operation that simplifies a single individual

Simplification is done using a combination of a domain-independent editing rule....

Universal editing rule: if a function without side-effects occurs in a tree w constn gun vaahenc nep w result

.….and domain-dependent editing rules

PAA-A De Morgan's Laws etc.

Editing can be used as an operator during the GP search

Tpially d   pe when ntetin heesult   GP run, as here

COcas y Coin

# GP Example - Learning the 11-Multiplexer

# GP Example - Learning the 11-Multiplexer

GP Example - Learning the 11-Multiplexer

It is informative to notice that the best solution found by GP is hierarchical   
Two multiplexer problems exists that are smaller than 11-multiplexer • 6 multiplexer - 2 address bits + 2² data bits 3 multplexer - 1 address bit + 2' data bits   
Looking again at our simplified solution, we see that it is a composition of two 6-multiplexers • A0 is used to decide whether the A1 and A2 address bits should index into D7,D5,D3,D1, or into D6,D4,D2,D0   
Furthermore, at the lowest level these 6-multiplexers are each a composition of two 3-multiplexers • The 3-multiplexer can be solved by a single IF-ELSE function   
The best individual in generation 9 is a boolean function that perfectly matches all our fitness cases   
How likely is is that random search would have found this particular boolean function so quickly?   
We can estimate this by calculating the number of distinct boolean functions • Exercise: Derive an expression for the number of possible boolean functions operating on n variables and returning one boolean value as the result. Evaluate this for n = 11 to calculate the probability of finding the 11-multiplexer function by random search in that function space   
N.B. actually the number of GP trees implementing the same boolean probability of finding a GP tree to solve the 11-multiplexer by random search will be even smaller   
We have already established that F  T satisfies the closure property   
We have also demonstrated its sufficiency, by using it to find an individual that completely solves the problem   
Would a subset of F have the sufficiency property? What is the smallest subset that is sufficient to solve the problem? • Exercise: Determine analytically the minimum subset(s) of F that are sufficient to solve the multiplexer problem. Run a GP system on the function set F and examining the best-of-run individuals produced

# Hierarchy in GP

The multiplexer example ustrates a general principle of GP GP works with hierarchies of building blocks   
In the multiplexer the building blocks are repeatedly and independently discovered by the GP algorithm   
It would seem useful to be able  re-use building blocks ce discovered   
Two approaches to this exist •Encapsulation Automatically Defined Functions

# ADF - Initialisation

We first decide on how many ADFs the GP algorithm will be allowed for the problem

•We also specitly how many arguments each ADF should be allowed to use

We then put a placeholder 'LIST' node of appropriate arity at the rot of all tees in the population

nenc    eacn er heval subtree

Finally, we randomly initialise the population with the foowing funcon and terminal sets

• Function set - standard function set F selected for problem Value-returning subtree • Function set - standard function set plus ADF set, F U (ADFO,ADF1...ADFn} •Terminal set - standard terminal set 7 selected for problem

# Symbolic Regression with Constants

Clearly it's not practical to include all the real numbers we might need in the terminal set   
Even for integers we face the same problem   
The solution is to use random ephemeral constants • The ephemeral random constant is an additional terminal in the set T It is labelled 3 • At population initialisation, whenever a R is chosen as a terminal it is assigned a random value in some appropriate range These random constants can then be moved between trees by crossover and combined together with arithmetic and mathematical operators to give new values In doing so new constants can be created We can optionally use the edit or encapsulation operations to protect them from destruction by crossover

# Encapsulation

The encapsulation operator works quite simply on a single parent, to produce a single offspring As its name suggests, it encapsulates some part of the parent making it available for use in other individuals

Clone the parent   
teco off el e neal n nd that subtree   
• Define a new member of the function set F that evalutes that subtree removed

# ADF - Crossover

We must be careful in applying crossover to trees containing ADFs   
In particular, what happens if we select a crosspoint in an ADF subtree i pare n n thealetun subn the he pnt?   
To avoid this, we must implement a structure preserving crossover operator A crosspoint is randomly selected in one parent A crosspoint of the same type is then randomly selected in the other parent   
The types for GP trees with ADFs are Root LIST node Nodes inside a particular ADF subtree Nodes inside the value-returning subtree   
We have now covered the basics of Genetic Programming   
Various advanced techniques exist for you to investigate, if you're interested, e.g. Iteration Recursion Cascading variables Hierarchical ADFs Strongly-typed GP

# Automatically Defined Functions

Encapsulation allows useful functions to be created, which do not take any parameters   
For the multiplexer, the building blocks do take parameters The address and data bits used in a smaller multiplexer   
To create building blocks with parameters we can use Automatically Defined Functions (ADFs) i encpulation  fin  new nc bas n uu alohaci variables Tis works in a slightly more complicated way than encapsulation

# Symbolic Regression with Constants

So far we have been looking at symbolic regression on boolean functions   
These are the simplest functions • In particular, there are only two values members of the terminal set T can take, 0 and 1   
We might also want to do symbolic regression on more complicated fnctins, such s those whose domn and rnge ae real nubers   
E.g. imagine we want to learn the function for the area of a circle 8 = xr2   
Solution of this problem requires us to put the constant pi in the terminal set • s is a pretty useful constant, so if we know we're doing geometry it's not unreasonable to put it in Not all constants are so obvious.. what should we do?