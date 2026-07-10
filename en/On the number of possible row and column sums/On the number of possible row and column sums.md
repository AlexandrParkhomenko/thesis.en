# On the number of possible row and column sums of 0,1-matrices

Daniel Goldstein and Richard Stong Center for Communications Research 4320 Westerra Court San Diego, CA 92121 dgoldste@ccrwest.org

Department of Mathematics Rice University Houston, TX 77005 stong@math.rice.edu

Submitted: Aug 9, 2005; Accepted: Apr 4, 2006; Published: Apr 18, 2006 Mathematics Subject Classification: 05A15

# Abstract

For $n$ a positive integer, we show that the number of of $2 n$ -tuples of integers that are the row and column sums of some $n \times n$ matrix with entries in $\{ 0 , 1 \}$ is evenly divisible by $n + 1$ . This confirms a conjecture of Benton, Snow, and Wallach.

We also consider a $q$ -analogue for $m \times n$ matrices. We give an efficient recursion formula for this analogue. We prove a divisibility result in this context that implies the $n + 1$ divisibility result.

# 1 Introduction

We study the number $p ( m , n )$ of $( m + n )$ -tuples of integers that are the row and column sums of some $m \times n$ matrix with entries in $\{ 0 , 1 \}$ . For each $n \geq 1$ , the sequence $\{ p ( m , n ) \} _ { m = 1 } ^ { \infty }$ is a linear recursion of degree $n$ . Moreover, this recursion is annihilated by the polynomial $( T - ( n + 1 ) ) ^ { n }$ . It follows that if $1 \leq n \leq m$ , then $p ( m , n )$ is evenly divisible by $( n + 1 ) ^ { m - n + 1 }$ . This confirms a conjecture of Benton, Snow, and Wallach.

For positive integers $m$ and $n$ , let $\mathcal { M } = \mathcal { M } _ { m , n }$ be the set of $m \times n$ matrices with entries in $\{ 0 , 1 \}$ . For $M$ in $\mathcal { M }$ , we write $M = ( M _ { i j } )$ .

We have two vector-valued functions on $\mathcal { M }$ : the vector $x ( M ) = ( x _ { 1 } , \ldots , x _ { m } )$ of row sums, where $\begin{array} { r } { x _ { i } = \sum _ { 1 \leq j \leq \underline { { n } } } M _ { i j } } \end{array}$ for $1 \leq i \leq m$ , and the vector $y ( M ) = ( y _ { 1 } , . . . , y _ { n } )$ o f Pcolumn sums, where $\begin{array} { r } { y _ { j } = \sum _ { 1 \leq i \leq m } M _ { i j } } \end{array}$ for $1 \leq j \leq n$ .

Define $\mathcal { R } \mathcal { C } = \mathcal { R } \mathcal { C } _ { m , n }$ to be the set of pairs of row and column sums $( x ( M ) , y ( M ) )$ a s $M$ ranges over $\mathcal { M }$ . Our main result concerns the cardinality $p ( m , n )$ of ${ \mathcal { R } } { \mathcal { C } } _ { m , n }$ .

# Theorem 1 We have

1. $p ( 1 , 1 ) = 2$ .

2. $p ( m , n ) = p ( n , m )$ for $m , n \geq 1$ .

Of these statements, part (1) is clear, and part (2) follows by taking transpose, for $x ( M ^ { t } ) = y ( M )$ and $y ( M ^ { t } ) = x ( M )$ .

Part (3) says that, for each $n \geq 1$ , the sequence $\{ p ( m , n ) \} _ { m = 1 } ^ { \infty }$ is a linear recursion of degree $n$ that is annihilated by the polynomial $( T - ( n + 1 ) ) ^ { n }$ . Note that, for any fixed $n$ , the recursion (3) is equivalent to $p ( m , n ) = r _ { n } ( m ) ( n + 1 ) ^ { m }$ for some polynomial $r _ { n } ( m )$ o f degree $\leq n - 1$ .

Part (3) implies the following corollary.

Corollary 2 The number $p ( m , n )$ is evenly divisible by $( n + 1 ) ^ { m - n + 1 }$ if $1 \leq n \leq m$ .

Indeed each of the $n$ terms in the sum representing $p ( m , n )$ is divisible by this quantity.   
A second consequence of part (3) is an efficient algorithm for computing $p ( m , n )$ .

Algorithm 3 We construct a table of the values $p ( i , j )$ , for $1 \leq i , j \leq m$ by induction on $j$ . First we fill in $p ( i , 1 ) = 2 ^ { \iota }$ , for $1 \leq i \leq m$ . Next, for a given $j \leq m$ , having filled in $p ( i , j ^ { \prime } )$ for $1 \leq j ^ { \prime } < j$ , we fill in $p ( i , j )$ by induction on $i$ , using part (2) if $i \leq j$ and part (3) if $i > j$ .

# 2 A generalization

We mention a mild generalization of Theorem 1 and its corollary. Define the polynomial P = Pm,n(q) = (x,y) m,n , where $| x | = x _ { 1 } + \cdot \cdot \cdot + x _ { m }$ . We recover $p ( m , n )$ by P ∈RCevaluating the polynomial $P _ { m , n }$ at $q = 1$ .

# Theorem 4 We have

1. $P _ { 1 , 1 } = 1 + q$

2. $P _ { m , n } = P _ { n , m }$ for $m , n \geq 1$ .

3. If $1 \leq n \leq m$ , then $\begin{array} { r } { P _ { m , n } = \sum _ { 1 \leq i \leq n } ( - 1 ) ^ { i + 1 } { \binom { n } { i } } ( 1 + q + \cdot \cdot \cdot + q ^ { n } ) ^ { i } P _ { m - i , n } . } \end{array}$

4. If $1 \leq n \leq m$ , then the polynomial $P _ { m , n }$ is evenly divisible by $( 1 + q + \cdot \cdot \cdot + q ^ { n } ) ^ { m - n + 1 }$ in $\mathbb { Z } [ x ]$ .

Part (4) answers a conjecture of J. Benton, R. Snow, and N. Wallach in [1].

# 3 Start of the proof

Let $\mathbb { N } = \{ 0 , 1 , \dots \}$ . Define the weight of a matrix $N$ to be the sum of its entries, and write $| N |$ for the weight of $N$ . With this definition, we have $| x ( M ) | = | M | = | y ( M ) |$ for $M \in \mathcal { M }$ . Thus, a necessary condition for $x$ and $y$ to be row and column sums of a matrix is that they have the same weight.

Clearly, the row sums of a member of $\mathcal { M }$ are at most $n$ . Conversely, if $x = ( x _ { 1 } , \ldots , x _ { m } ) $ and $0 \leq x _ { i } \leq n$ , let $R = R ( x )$ be the $m \times n$ matrix such that $R _ { i j } = 1$ if $1 \leq j \leq x _ { i }$ and $R _ { i j } = 0$ otherwise. Then $R$ lies in $\mathcal { M }$ and has row sums equal to $x$ . This proves:

Lemma 5 Let $x = ( x _ { 1 } , \ldots , x _ { m } ) \in \mathbb { N } ^ { m }$ . Then $x$ is the vector of row sums of an $m \times n$ matrix with entries in $\{ 0 , 1 \}$ if and only if $x _ { i } \leq n$ for all $i$ .

Let $a _ { j }$ be the number of rows of $R$ that have exactly $j$ ones. Write $a = ( a _ { 0 } , \ldots , a _ { n } ) =$ $a ( x )$ in $\mathbb { N } ^ { n + 1 }$ . We note that $| a | = m$ , and write $\binom { m } { a }$ for the multinomial coefficient $\frac { m ! } { a _ { 0 } ! \cdots a _ { n } ! }$ With this notation, we have the following lemma.

Lemma 6 Let a in $\mathbb { N } ^ { n + 1 }$ satisfy $| a | = m$ . Then the number of $x$ in $\mathbb { N } ^ { m }$ such that $a ( x ) = a$ is $\binom { m } { a }$ .

Let $\lambda = ( \lambda _ { 1 } , . . . , \lambda _ { n } ) = \lambda ( x )$ be the column sums of the matrix $R$ constructed above. It satisfies the dominance condition:

$$
\lambda _ { 1 } \geq \cdots \geq \lambda _ { n } .
$$

Note that $a$ in $\mathbb { N } ^ { n + 1 }$ with $| a | = m$ determines a dominant $\lambda$ in $\mathbb { N } ^ { n }$ with $m \geq \lambda _ { 1 }$ , and vice versa. For, given $\lambda$ , set $\lambda _ { 0 } = m$ and $\lambda _ { n + 1 } = 0$ , and define $a _ { j } = \lambda _ { j } - \lambda _ { j + 1 }$ , for $j = 0 , \ldots , n$ . Conversely, given $a$ in $\mathbb { N } ^ { n + 1 }$ , define $\lambda _ { j } = a _ { j } + \cdots + a _ { n }$ .

The weights of these vectors are related by $\begin{array} { r } { | x | = | \lambda | = \sum _ { 0 \leq j \leq n } j a _ { j } } \end{array}$

Given $y , \lambda$ in $\mathbb { N } ^ { n }$ with $\lambda$ dominant, we define $y \preceq \lambda$ if

$$
y _ { 1 } + \cdot \cdot \cdot + y _ { j } \leq \lambda _ { 1 } + \cdot \cdot \cdot + \lambda _ { j } ,
$$

for all $j$ in the range $1 \leq j \leq n$ .

The symmetric group $S _ { n }$ acts on $\mathbb { N } ^ { n }$ by permuting coordinates. For $y \in N ^ { n }$ and $\sigma \in S _ { n }$ , we set $y \sigma = ( y _ { \sigma ( 1 ) } , \dots , y _ { \sigma ( n ) } )$ .

The next result, proved in [2, Corollary 6.2.5] or [3, Theorem 16.1], gives necessary and sufficient conditions for a pair of vectors to lie in ${ \mathcal { R } } { \mathcal { C } } _ { m , n }$ .

Lemma 7 Let $x$ in $\mathbb { N } ^ { m }$ be the vector of row sums of a matrix in $\mathcal { M }$ , and set $\lambda = \lambda ( x )$ . Then $( x , y ) \in \mathcal { R C }$ if and only if $y \in \mathbb { N } ^ { n }$ satisfies

(i) $| y | = | \lambda |$ , and (ii) $y \sigma \preceq \lambda$ for all $\sigma \in S _ { n }$ .

Let $N ( \lambda )$ be the number of $y \in \mathbb { N } ^ { n }$ that satisfy (i) and (ii). Then

$$
P _ { m , n } ( q ) = \sum _ { x \in \{ 0 , \ldots , n \} ^ { m } } N ( \lambda ( x ) ) q ^ { | x | } .
$$

Combined with Lemma 6, this gives:

$$
P _ { m , n } ( q ) = \sum _ { \underset { | a | = m } { a \in \mathbb { N } ^ { n + 1 } } } \binom { m } { a } N ( \lambda ) q ^ { a _ { 1 } + 2 a _ { 2 } + \cdots + n a _ { n } } .
$$

# 4 Key Lemma

Lemma 8 Let $n \geq 1$ . There is a polynomial $G = G _ { n }$ in $\mathbb { Q } [ z _ { 1 } , \ldots , z _ { n } ]$ of total degree $\leq n - 1$ such that $N ( \lambda ) = G ( \lambda _ { 1 } , . . . , \lambda _ { n } )$ for any dominant $\lambda = ( \lambda _ { 1 } , \ldots , \lambda _ { n } )$ in $\mathbb { N } ^ { n }$ .

To count $N ( \lambda )$ , we will condition on the first term $y _ { 1 }$ of the vector $y$ . We will need a subsidiary function. Let $N ( \lambda ; t )$ be the number of solutions of (i) and (ii) with $y _ { 1 } = t$ . By definition, $\begin{array} { r } { N ( \lambda ) = \sum _ { t \geq 0 } N ( \lambda ; t ) } \end{array}$ .

P ≥ We need one more definition to state the next lemma. Suppose $\lambda = ( \lambda _ { 1 } , \ldots , \lambda _ { n } )$ has $n$ parts, and $\lambda _ { j + 1 } < t \leq \lambda _ { j }$ . Then we define $\mu ( t )$ with $n - 1$ parts to be

$$
\mu ( t ) = ( \lambda _ { 1 } , \ldots , \lambda _ { j - 1 } , \lambda _ { j } + \lambda _ { j + 1 } - t , \lambda _ { j + 2 } , \ldots , \lambda _ { n } ) .
$$

(In the definition of $\mu ( t )$ , $\lambda _ { j }$ and $\lambda _ { j + 1 }$ have been removed and $\lambda _ { j } + \lambda _ { j + 1 } - t$ has been inserted.) Note that if $\lambda$ is dominant, then so also is $\mu ( t )$ since $\lambda _ { j } > \lambda _ { j } + \lambda _ { j + 1 } - t \ge \lambda _ { j + 1 }$ .

# Lemma 9 We have:

(a) If $t < \lambda _ { n }$ or if $t > \lambda _ { 1 }$ , then $N ( \lambda ; t ) = 0$ . (b) $N ( \lambda ; \lambda _ { n } ) = N ( ( \lambda _ { 1 } , . . . , \lambda _ { n - 1 } ) ) .$ (c) Suppose that $\lambda _ { j + 1 } < t \leq \lambda _ { j }$ . Then $N ( \lambda ; t ) = N ( \mu ( t ) )$ .

Proof. If $y _ { 1 } > \lambda _ { 1 }$ then (ii) is violated. Suppose $y$ satisfies (i) and $y _ { 1 } < \lambda _ { n }$ . Then

$$
y _ { 2 } + y _ { 3 } + \cdot \cdot \cdot + y _ { n } > \lambda _ { 1 } + \lambda _ { 2 } + \cdot \cdot \cdot + \lambda _ { n - 1 } ,
$$

thus (ii) is violated if $\sigma ( n ) = 1$ . Therefore $N ( \lambda , y _ { 1 } ) = 0$ , proving (a), and we turn to (b). Set $\lambda ^ { \prime } = ( \lambda _ { 1 } , \ldots , \lambda _ { n - 1 } )$ . We claim that the correspondence

$$
( y _ { 1 } , y _ { 2 } \ldots , y _ { n } ) \longleftrightarrow ( y _ { 2 } \ldots , y _ { n } )
$$

gives a bijection between the sets counting $N ( \lambda ; y _ { 1 } )$ and $N ( \lambda ^ { \prime } )$ . One direction follows by definition: if $\left( y _ { 1 } , \ldots , y _ { n } \right)$ is counted by $N ( \lambda )$ , then $\left( y _ { 2 } , \ldots , y _ { n } \right)$ is counted by $N ( \lambda ^ { \prime } )$ .

Conversely, suppose that $\left( y _ { 2 } , \ldots , y _ { n } \right)$ is counted by $N ( \lambda ^ { \prime } )$ . Now (i) (for $y$ and $\lambda$ ) follows since $y _ { 1 } = \lambda _ { n }$ . To prove (ii), let $\sigma \in S _ { n }$ . Set $k = \sigma ^ { - 1 } ( 1 )$ . Now

$$
\begin{array} { l l l } { { y _ { \sigma ( 1 ) } + \cdot \cdot \cdot + y _ { \sigma ( j ) } } } & { { \leq } } & { { \bigl ( \lambda _ { 1 } + \cdot \cdot \cdot + \lambda _ { j - 1 } \bigr ) + \lambda _ { n } } } \\ { { } } & { { \leq } } & { { \lambda _ { 1 } + \cdot \cdot \cdot + \lambda _ { j } } } \end{array}
$$

if $j \geq k$ . The inequality is clear if $j < k$ .

Part (c) is proved using the same correspondence used in part (b). The straightforward but tedious calculation is omitted.

Proof of Lemma 8. Suppose $n = 1$ and let $\lambda = \left( \lambda _ { 1 } \right)$ . Then $N ( \lambda _ { 1 } ) = 1$ , a polynomial of degree 0.

Thus the lemma holds for $n = 1$ . We proceed by induction to prove it for all $n$ Suppose the lemma has been proved for $n$ and we wish to prove it for $n + 1$ .

We break up the sum that counts $N ( \lambda )$ , by conditioning on $y _ { 1 }$ . By Lemma $9 ( \mathrm { a } )$ , it is enough to consider $y _ { 1 }$ in the range $\lambda _ { n } \leq y _ { 1 } \leq \lambda _ { 1 }$ . Either $y _ { 1 } = \lambda _ { n }$ , or $\lambda _ { j + 1 } < y _ { 1 } \le \lambda _ { j }$ for a unique $j$ in the range $1 \leq j < n$ , and therefore

$$
N ( \lambda ) \ = \ N ( \lambda ; \lambda _ { n } ) + \ \sum _ { 1 \leq j < n } \ \sum _ { \lambda _ { j + 1 } < t \leq \lambda _ { j } } N ( \lambda ; t ) .
$$

In view of Lemma 9(b) and (c), this yields

$$
N ( \lambda ) \ = \ N ( ( \lambda _ { 1 } , \ldots , \lambda _ { n - 1 } ) ) + \ \sum _ { 1 \leq j < n } \ \sum _ { \lambda _ { j + 1 } < t \leq \lambda _ { j } } N ( \mu ( t ) ) .
$$

To see that $N ( \lambda )$ is a polynomial of degree at most $n$ , it suffices to show that each term on the right is a polynomial of total degree at most $n$ . This is true for the first term $N ( ( \lambda _ { 1 } , . . . , \lambda _ { n - 1 } ) )$ by the inductive hypothesis.

Each of the subsequent terms is itself a sum. By the inductive hypothesis, each summand in each term is a polynomial of degree $\leq n - 1$ . But, for any polynomial $f$ , we have that $\textstyle \sum _ { x < t \leq y } f ( t )$ is a polynomial in $x$ and $y$ of degree $\leq \deg f + 1$ .

PBy induction and (4) it follows that the coefficients of $G$ are rational numbers. This proves the lemma.

# 5 End of the proof

Since $G$ is a polynomial of degree $\leq \ n - 1$ by Lemma 8, so also is $H$ defined by $H ( a _ { 0 } , a _ { 1 } , \ldots , a _ { n } ) = G _ { n } ( \lambda _ { 1 } , \ldots , \lambda _ { n } )$ , since the transformation from $\lambda$ to $a$ is linear.

By (3) we have

$$
P _ { m , n } = \sum _ { \stackrel { a \in \mathbb { N } ^ { n + 1 } } { | a | = m } } { \binom { m } { a } } H ( a _ { 0 } , \ldots , a _ { n } ) q ^ { a _ { 1 } + \cdots + n a _ { n } } .
$$

Proof of Theorem 4. We are free to assume $n \leq m$ .

We define the function $E$ of the variables $z _ { 0 } , \ldots , z _ { n }$ by

$$
E ( z _ { 0 } , \dots , z _ { n } ) = \sum _ { \stackrel { a \in N ^ { n + 1 } } { | a | = m } } { \binom { m } { a } } H ( a _ { 0 } , \dotsc , a _ { n } ) e ^ { a _ { 0 } z _ { 0 } + \dots + a _ { n } z _ { n } } .
$$

By (5) and (6), we have $P _ { m , n } ( q ) = E ( 0 , \log ( q ) , 2 \log ( q ) , \dots , n \log ( q ) ) .$

The following lemma is proved by induction.

Lemma 10 Let $H \in \mathbb { Q } [ z _ { 0 } , \dots , z _ { n } ]$ be a polynomial. Write $z ~ = ~ ( z _ { 0 } , \ldots , z _ { n } )$ and $a =$ $( a _ { 0 } , \ldots , a _ { n } )$ , and set $a \cdot z = a _ { 0 } z _ { 0 } + \cdot \cdot \cdot + a _ { n } z _ { n }$ . Then there is a linear differential operator $D$ in $z _ { 0 } , \ldots , z _ { n }$ such that $H ( z ) e ^ { a \cdot z } = D e ^ { a \cdot z }$ . Moreover, $\deg ( D ) = \deg ( H )$ .

By the lemma, we have

$$
E ( z ) = \sum _ { \stackrel { a \in N ^ { n + 1 } } { | a | = m } } { \binom { m } { a } } D e ^ { a \cdot z } = D \left( \sum { \binom { m } { a } } e ^ { a \cdot z } \right) .
$$

By the multinomial theorem

$$
\sum _ { a \in N ^ { n + 1 } } \binom { m } { a } e ^ { a \cdot z } = ( e ^ { z _ { 0 } } + \cdot \cdot \cdot + e ^ { z _ { n } } ) ^ { m } ,
$$

whence $E$ is $( e ^ { z _ { 0 } } + \cdot \cdot \cdot + e ^ { z _ { n } } ) ^ { m - n + 1 }$ times a polynomial $f _ { 1 } ( m , e ^ { z _ { 0 } } , \ldots , e ^ { z _ { n } } )$ whose degree in $m$ is $\leq n - 1$ .

Set $f ( m , q ) = f _ { 1 } ( m , 1 , q , \dots , q ^ { n } )$ . When evaluated at $z _ { i } = i \log ( q )$ , $e ^ { z _ { 0 } } + \cdots + e ^ { z _ { n } }$ becomes $( 1 + q + \cdots + q ^ { n } )$ , whence $P _ { m , n } = f ( m , q ) ( 1 + q + \cdot \cdot \cdot + q ^ { n } ) ^ { m - n + 1 }$ . Since $f ( m , q )$ is a polynomial in $m$ of degree at most $n - 1$ , part (3) follows immediately.

Set $\pi = ( 1 + q + \cdot \cdot \cdot + q ^ { n } ) ^ { n - m + 1 }$ . Finally, to prove part (4), it remains to show that, for each $m$ , the coefficients of $f ( m , q )$ , as a polynomial in $q$ , are integers.

One way to see this is to regard $f = P _ { m , n } / \pi$ as a power series identity and formally equate coefficients of $q ^ { i }$ , because $\pi$ is a polynomial in $q$ with constant term 1. Theorem 4 is proved.

# Список литературы

[1] J. Benton, R. Snow, and N. Wallach. A combinatorial problem associated with nonograms, Linear Algebra and its Applications, Volume 412, Issue 1, 1 January 2006, Pages 30–38.   
[2] R. H. Brualdi and H. J. Ryser. Combinatorial matrix theory. Cambridge University Press, 1991.   
[3] J. H. van Lint and R. M. Wilson. A course in combinatorics. Cambridge University Press, 1992.