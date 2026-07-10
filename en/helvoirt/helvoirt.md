# Discrete Tomography and Nonograms

Walter Kosters, Universiteit Leiden

April 16, 2009; Helvoirt www.liacs.nl/home/kosters/

![](images/eb5fb5a78831d08ed6e0bdd599427e5a6964f62590a0032215f0abf0a97a9701.jpg)

When talking about Japanese puzzles, everyone thinks of Sudoku.

<table><tr><td rowspan=1 colspan=1>5</td><td rowspan=1 colspan=1>|3</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>7</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1></td></tr><tr><td rowspan=1 colspan=1>6</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>1</td><td rowspan=1 colspan=1>9</td><td rowspan=1 colspan=1>5</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1></td></tr><tr><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>9</td><td rowspan=1 colspan=1>|8</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>6</td><td rowspan=1 colspan=1></td></tr><tr><td rowspan=1 colspan=1>8</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>6</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>3</td></tr><tr><td rowspan=1 colspan=1>4</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>8</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>3</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>1</td></tr><tr><td rowspan=1 colspan=1>7</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>2</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>6</td></tr><tr><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>6</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>2</td><td rowspan=1 colspan=1>8</td><td rowspan=1 colspan=1></td></tr><tr><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>4</td><td rowspan=1 colspan=1>1</td><td rowspan=1 colspan=1>9</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>5</td></tr><tr><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>8</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>7 9</td><td rowspan=1 colspan=1>7 9</td></tr></table>

When talking about Japanese puzzles, everyone thinks of Sudoku.

<table><tr><td rowspan=1 colspan=1>5</td><td rowspan=1 colspan=1>3</td><td rowspan=1 colspan=1>4</td><td rowspan=1 colspan=1>6</td><td rowspan=1 colspan=1>7</td><td rowspan=1 colspan=1>8</td><td rowspan=1 colspan=1>9</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>2</td></tr><tr><td rowspan=1 colspan=1>6</td><td rowspan=1 colspan=1>7</td><td rowspan=1 colspan=1>2</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>9</td><td rowspan=1 colspan=1>5</td><td rowspan=1 colspan=1>3</td><td rowspan=1 colspan=1>4</td><td rowspan=1 colspan=1>8</td></tr><tr><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>9</td><td rowspan=1 colspan=1>8</td><td rowspan=1 colspan=1>3</td><td rowspan=1 colspan=1>4</td><td rowspan=1 colspan=1>2</td><td rowspan=1 colspan=1>5</td><td rowspan=1 colspan=1>6</td><td rowspan=1 colspan=1>7</td></tr><tr><td rowspan=1 colspan=1>8</td><td rowspan=1 colspan=1>5</td><td rowspan=1 colspan=1>9</td><td rowspan=1 colspan=1>7</td><td rowspan=1 colspan=1>6</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>4</td><td rowspan=1 colspan=1>2</td><td rowspan=1 colspan=1>3</td></tr><tr><td rowspan=1 colspan=1>4</td><td rowspan=1 colspan=1>2</td><td rowspan=1 colspan=1>6</td><td rowspan=1 colspan=1>8</td><td rowspan=1 colspan=1>5</td><td rowspan=1 colspan=1>3</td><td rowspan=1 colspan=1>7</td><td rowspan=1 colspan=1>9</td><td rowspan=1 colspan=1></td></tr><tr><td rowspan=1 colspan=1>7</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>3</td><td rowspan=1 colspan=1>9</td><td rowspan=1 colspan=1>2</td><td rowspan=1 colspan=1>4</td><td rowspan=1 colspan=1>8</td><td rowspan=1 colspan=1>5</td><td rowspan=1 colspan=1>6</td></tr><tr><td rowspan=1 colspan=1>9</td><td rowspan=1 colspan=1>6</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>5</td><td rowspan=1 colspan=1>3</td><td rowspan=1 colspan=1>7</td><td rowspan=1 colspan=1>2</td><td rowspan=1 colspan=1>8</td><td rowspan=1 colspan=1>4</td></tr><tr><td rowspan=1 colspan=1>2</td><td rowspan=1 colspan=1>8</td><td rowspan=1 colspan=1>7</td><td rowspan=1 colspan=1>4</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>9</td><td rowspan=1 colspan=1>6</td><td rowspan=1 colspan=1>3</td><td rowspan=1 colspan=1>5</td></tr><tr><td rowspan=1 colspan=1>3</td><td rowspan=1 colspan=1>4</td><td rowspan=1 colspan=1>5</td><td rowspan=1 colspan=1>2</td><td rowspan=1 colspan=1>8</td><td rowspan=1 colspan=1>6</td><td rowspan=1 colspan=1></td><td rowspan=1 colspan=1>7</td><td rowspan=1 colspan=1>9</td></tr></table>

source: Wikipedia

But we will talk about Nonograms today.

A Nonogram is a puzzle; a small example:

![](images/480ad3447e8b2e19499627db411cb4d42ef10855e67d49ecc2513ac6a371af89.jpg)

Next to each row and column we enumerate the lengths of consecutive series of red pixels.

Where are these red = black pixels?

The (unique) solution looks like this:

![](images/77a2469e20dc45f2cc28e55a04aea769f72159ba9000b1658761a7ca01f8837e.jpg)

![](images/5d09e26ff5584c700ee297a9b00e3db8c8bcfe06c898f9cca6a055c99a3f7bbe.jpg)

Next to each row and column we enumerate the lengths of consecutive series of red pixels — in order.

Why are scientists interested in Nonograms?

Tomography tries to solve the following problem: How to reconstruct an object from projections?

Examples:

0 Solve Nonograms

![](images/39d583e9df2657d82c68f8be296074643ebfceebe7f64d331e0f070fb40f243e.jpg)

How do we look like, given CT-scans? (Computerized Tomography = CT 2 DT = Discrete Tomography)

Where are the "holes" in a diamond?

In Discrete Tomography we try to reconstruct an object from its projections.

An object "is" a finite subset of $\mathbf { Z } ^ { 2 }$ (so integer points in 2D space).

A projection gives all relevant "linesums" over lines parallel to a given line, e.g., all horizontal lines and all vertical lines (2 projections). It is also possible to use all lines through a given point.

In CT one typically has many projections, in DT a few.

A small example of a Discrete Tomography problem:

![](images/1665ee863c92068ba6204e4e01a34881057d2addd54a8749ccc42b7df08b1bc7.jpg)

Next to each row and column we give the (total) number of red pixels.

Where are these red = black pixels?

A (non-unique) solution looks like this:

![](images/64449895aac6f745095420169a55b40cdc5e968bca45e438ca0bda2cc84a298a.jpg)

![](images/fe956ab775b42bb8a8acef62a451c3d1c325a2574d4f79136da7b08a261c844e.jpg)

Next to each row and column we give the (total) number of red pixels.

The problem can be defined more general:

Given an unknown function $f$ on some domain $D$ (discrete, or just some subset of $\mathbf { R } ^ { n }$ ), with a discrete range $\subseteq \mathbf { R }$ , the task is to (approximately) reconstruct $f$ , given sums (integrals) over certain subsets of $D$

In our case, the range is $\{ 0 , 1 \} = \{ { \mathsf { w h i t e } } , { \mathsf { b l a c k } } \} .$

General reference: G.T. Herman & A. Kuba, Discrete tomography, Foundations, algorithms and applications, Birkhäuser, 1999.

Usually we have three tasks:

Consistency Does an object with the given projection values (a "solution to the puzzle") exist?

Uniqueness Suppose there is a solution. Does there exist another one?

Reconstruction Construct a solution.

All three problems, with horizontal and vertical projections, are solved in polynomial time by Ryser's Theorem from 1957.

But the problems for 3 or more projections are NP-hard!

If you were to use a flashlight in 2D, it would flicker like when throwing a stone into the water.

Ryser's Theorem Given two vectors $R = ( r _ { 1 } , \ldots , r _ { m } ) \in$ $\mathbf { N } _ { 0 } ^ { m }$ (the row sums) and $S = ( s _ { 1 } , \ldots , s _ { n } ) \in \mathbb { N } _ { 0 } ^ { n }$ (the column sums). Then there is a binary matrix $A = ( a _ { i j } )$ with $\Sigma _ { j = 1 } ^ { n } a _ { i j } = r _ { i }$ $( 1 \leq i \leq m )$ and $\Sigma _ { i = 1 } ^ { m } a _ { i j } = s _ { i }$ $( 1 \leq j \leq n )$ and only if $\Sigma _ { j = \ell } ^ { n } s _ { j } ^ { \prime } \geq \Sigma _ { j = \ell } ^ { n } \overline { { s } } _ { j }$ $( 2 \leq \ell \leq n )$

Here the $s _ { j } ^ { \prime }$ r the (non-increasing) sorted $s _ { j }$ , and the $\overline { { s } } _ { j }$ are the column sums of the matrix with the $r _ { i }$ as row sums, and ones in the leftmost positions.

Furthermore, all solutions can be obtained from one another by a series of switchings with switching components.

Ryser's algorithm constructs a solution working backward from the last column. The column sums are already sorted in non-increasing order $( s = s ^ { \prime } \ \mathsf { a n d } \ \overline { { s } } )$

![](images/94129ccfe00a73f47c14912c38c54363e34e3e4ab230d27a59eab33602390cf2.jpg)

![](images/c784a538aa44297c15e786a7ecc37bc69a43d98c3eb16a524629f10b4e90f0f5.jpg)

![](images/17dee6ae1859d7b361d3cdf09bbb26fd82994b3a1878e0cf24ce0c7c5428e2d7.jpg)

![](images/749c7031e06f139bb008abeedcff6210c017e83e7ba1dcc2d69c019d700dfd10.jpg)

![](images/651a8b7d94fa069301a88a186b562beb5015d8b36deedbc13b326f5511702f09.jpg)

In an $h$ -convex object all rows must consist of consecutive black pixels: the rows have the "Nonogram property"

![](images/c16d8bdee5adf5e9a43eac71906700b4287d3fa85e2613ba89c266ac02838946.jpg)

![](images/2d6da2d3a6d81620f6fab6b1d705ccfa781d2cf46b46b5b9a33c051e9b8c3320.jpg)

For $h$ -convex objects the 2 projections Reconstruction problem is NP-complete . ..

Now back to Nonograms: how to solve them?

Most humans use logic rules, combined with heuristics like "interchange row reasoning and column reasoning"

An example of a logic rule is: "if the number 3 is next to a row/column of width 5, the middle pixel must be red". In this particular rule one looks at one row or column at a time.

Suppose you already know:

<table><tr><td>3,2,1</td><td>??</td><td></td><td></td><td></td><td>?</td><td>•</td><td>?????</td><td></td><td></td><td></td><td></td></tr></table>

A • means a known white/empty pixel, a denotes a known filled pixel. The rest is still unknown.

Remember that we enumerate the lengths of consecutive series of red $=$ black pixels — in order.

What can we conclude?

We conclude that for this row:

![](images/400fec3cbf42cc221b90d38a3102c6ac2a414af39a4703e0b25200a43ed51080.jpg)

A • means a known white/empty pixel, a denotes a known filled pixel. The rest is still unknown.

So by examining a single row or column we can make progression.

How can a computer program draw such conclusions?

A first option is to use brute-force: try "all" possibilities. But a $5 \times 5$ Nonogram has

$$
2 ^ { 2 5 } = 2 ^ { 1 0 } \cdot 2 ^ { 1 0 } \cdot 2 ^ { 5 } = 1 0 2 4 \cdot 1 0 2 4 \cdot 3 2 \approx 3 2
$$

possible solutions! And the $^ { 1 1 } 8 0 \times 5 0$ Einstein" has $\cdot$ 101200 possibilities.

So ... no way! (But for small parts it might work.) We therefore first try some logic reasoning for a single line = row or column.

For a single line one can use Dynamic Programming.

We want a string $s _ { 1 } s _ { 2 } \ldots s _ { \ell }$ over the alphabet $\Sigma \cup \{ ? \}$ to match a regular expression $d _ { 1 } d _ { 2 } \ldots = \sigma _ { 1 } \{ a _ { 1 } , b _ { 1 } \} \sigma _ { 2 } \{ a _ { 2 } , b _ { 2 } \}$ (so first between $a _ { 1 }$ and $b _ { 1 }$ times the character $\sigma _ { 1 }$ , . . . ) in the following sense: $F i x ( i , j )$ is true if and only if the prefix $s _ { 1 } s _ { 2 } \ldots s _ { i }$ can be made to match $d _ { 1 } d _ { 2 } \dots d _ { j }$ by "fixing" ?'s to elements from ∑ (e.g., $\Sigma = \{ \bullet , \quad \} )$

$$
\begin{array} { r }  x ( i , j ) = \bigcirc { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc }  { \bigcirc \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc } { \bigcirc }  { \bigcirc } { \bigcirc }  \ \end{array}
$$

Here $A _ { j } = \textstyle \sum _ { p = 1 } ^ { j } a _ { p } , B _ { j } = \textstyle \sum _ { p = 1 } ^ { j } b _ { p }$ and $L _ { i } ^ { \sigma } ( s )$ is the argest index $h \leq i$ with $s _ { h } \notin \{ \sigma , ? \}$ if this exists (and O otherwise).

This polynomial time Dynamic Programming approach allows for efficient solving of most puzzles from newspapers. One can repeatedly apply the method to all rows and columns, thereby also introducing a difficulty measure.

See K.J. Batenburg & WAK, Solving Nonograms by combining relaxations, Pattern Recognition, 2009.

percentage unsolved pixels for randomly generated puzzles of different size, black percentage

![](images/f035d8ef7da1f129745214fa7d572bd7a4889cee55f4148a8eee69f9080859cd.jpg)

How far can we get by looking at a single row/column? Again, with • for a white pixel, and for a filled one:

![](images/8ca11ecf703b0032ef00fec0dc2102c5caa24488004f271829fe6280592d97a8.jpg)

![](images/8b499a576a2b00785392b7cd1eede9e197c22334102d5ba6bd78e71ca5a7f7b2.jpg)

But now we are stuck . .. unless we use rows and columns together.

We have this:

![](images/d6c400a95f0bdf7925c18c9ffb751bdde2ca7a58958594e86a6be46122229c24.jpg)

![](images/3bcd266ac3008de1c443e59c1d883eee02f5a9832fd408bf22cf07be5970be87.jpg)

Suppose that $u =$ , then (column) v must be empty, and so (row) $w = \bullet$ , and therefore (column) $x$ must be empty. Contradiction (row)! So u must be empty.

The rest is simple.

The logic we used here has rules like "if this pixel is red, that pixel must be white" . This can be modeled through a 2-SAT problem, which happens to be solvable in polynomial time — in contrast with 3-SAT, which is NP-complete.

This adds another difficult measure.

Solving a Nonogram in general is NP-complete.

As an illustration that this 2-SAT logic sometimes fails to catch everything:

<table><tr><td rowspan="5"></td><td></td><td>2 1</td><td>1</td><td>1 1 1</td><td></td></tr><tr><td>1 ?</td><td></td><td>?</td><td></td><td>?</td></tr><tr><td></td><td></td><td></td><td>2?????</td><td></td></tr><tr><td>1 ?</td><td></td><td>?</td><td></td><td>0</td></tr><tr><td></td><td></td><td>2?????</td><td></td><td></td></tr><tr><td></td><td>1 ?</td><td></td><td>?</td><td></td><td>?</td></tr></table>

Partially solved $5 \times 5$ Nonogram, where the fact that pixel $\bigcirc$ must be white is hard to infer.

![](images/690e9adc9b4b371a4eaf85304ed0f11021fc7fb668e708f28f7cc219a05340e8.jpg)

Randomly generated partially solved $3 0 \times 3 0$ Nonogram, with 50 $\%$ black pixels; the grey cells denote the unknown pixels. This Nonogram has six solutions.

# How to build $=$ design your own Nonogram?

![](images/26f1952c52a3defbf11bc7d3071aa76ae4e7c3304f8c3933a0dc87a237ea794b.jpg)

http://www.liacs.nl/home/kosters/nono/

Remember that a good Nonogram should have a unique solution.

In general they have many different solutions with switching components!

1 1 1 1 1 1 1 →

![](images/456df629f3ec56b9c780fcd4d8ce2130176a8a15991b7e43167b26dd2e8b34e6.jpg)

![](images/ee01d96ecf05d664ef05cdbaf98effca4a7d8cc3508d13b86cdf870c882318db.jpg)

![](images/03f64b35b4fa3c9f2604bbc6ea02c0a9ba58055794d784d8631e1e3990d7439a.jpg)

There are several interesting questions attached to a game like Tetris:

How to play well? (AI — Artificial Intelligence)

C How hard is it? (complexity)

• What might happen?

It has been shown that certain Tetris-problems are NPcomplete (joint work with researchers from MIT & HJH), that you can reach almost all configurations, but that not all problems are "decidable".

The 7 Tetris-pieces:

![](images/2668312835dc63e43da1083f9e8a6ab0eda7695dc838b701f8d296e547d973f9.jpg)

Random pieces fall down, and filled lines are cleared.

The question "Is it possible, given a finite ordered series of these pieces, to clear a partially filled game board?" is NP-complete.

If someone clears the board, this is easy to verify. If clearing is not possible however, up till now the only thing one can do to prove this is to check all possibilities, one by one!

An "arbitrary" configuration:

![](images/d214b04d7630f6d32d094e9b08bf07775de22430386043930b62e6edddf2f373.jpg)

This figure can be made by dropping 276 suitable Tetrispieces in the appropriate way, see

http://www.liacs.nl/home/kosters/tetris/

Claim: on a game board of odd width every configuration is reachable.