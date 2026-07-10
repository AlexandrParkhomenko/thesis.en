# Efficient Algorithms for the Longest Path Problem

Ryuhei UEHARA (JAIST) Yushi UNO (Osaka Prefecture University)

# The Longest Path Problem

• F i n d i n g a l o n g est (ve rtex d i sj o i nt) path i n a given graph

• M otivation (com pa ri ng to H a m i lton ia n path ) : Approx. Algorith m , Parameterized Com plexity M o re p ra ct i ca l /n at u ra l M o re d i ffi cu l t( ? )

# The Longest Path Problem

Known (ha rd n ess) resu lts ;

• We ca n not fi nd a path of l e ngth n-n ε i n a g ive n Hamiltonian graph in poly-time unless P=NP [Karger, Motwani, Ramkumar; 1997]

• We ca n fi nd O (log n) l e ngth path [Alon , Yuste r, Zwi ck; 1 995] (⇒O((log n/loglog n)2) [Björklund, Husfeldt; 2003])

• Approx. Alg . ach ieves O(n/log n) [AYZ95] (⇒O(n(loglog n/log n)²)[BH03])

O Expon e ntia l a lgorith m [M on ie n 1 985]

# The Longest Path Problem

Known polynom ia l ti me a lgorith m ;  
D ij kstra ’ s Al g . ( 1 9 6 ? ) ： L i n e a r a l g . fo r fi n d i n g a l o n g est p ath i n a tre e ;

![](images/f33ebc73d7452ff365c9bddfee4b584bae0fe8b9cf41235fcb27699e51991966.jpg)

# The Longest Path Problem

Known polynom ia l ti me a lgorith m ;  
D ij kstra ’ s Al g . ( 1 9 6 ? ) ： L i n e a r a l g . fo r fi n d i n g a l o n g est p ath i n a tre e ;

![](images/f116ed0e48f19dab04e5368300b8e9ebda03f2fcf53968e0f9aff626b35420ce.jpg)

# The Longest Path Problem

) Known polynom ia l ti me a lgorith m ;  
D ij kstra ’ s Al g . ( 1 9 6 ? ) ： L i n e a r a l g . fo r fi n d i n g a l o n g est p ath i n a tre e ;

![](images/40ffa6ad2a9745ab52958910574dd9d90c248041f3fa44b8b2d7da1478373106.jpg)

# The Longest Path Problem

0 Known polynom ia l ti me a lgorith m ;

D ij kstra ’ s Al g . ( 1 9 6 ? ) ： L i n e a r a l g . fo r fi n d i n g a l o n g est p ath i n a tre e ;

![](images/996044cbea5201704ea41d2ea6a026c7039de7f7c933f2fbb42985d44d7a8931.jpg)

# Approaches to the Efficient Algs to Longest Path Problem

1. Exte ns ion of th e D ij kstra’s a lgorith m We i g hted trees ( l i n ea r) , b l ock g ra p h s ( l i n ea r) , cacti $( \mathsf { O } ( n ^ { 2 } ) )$ .

(ISAAC 2004)

2. G ra p h cl asses s . t. H a m i lton i a n Path ca n be fou nd in poly time

Some g ra ph classes havi ng i nterval representations (bipartite permutation, interval biconvex graphs)

3. Dyna m i c prog ra m m i ng to the g ra p h cl asses that tree re p rese ntations (on goi ng )

C a ct i ( l i n e a r) ,

# Approaches to the Efficient Algs to Longest Path Problem

1. Exte ns ion of th e D ij kstra’s a lgorith m We i g hted trees ( l i n ea r) , b l ock g ra p h s ( l i n ea r) , cacti $( \mathsf { O } ( n ^ { 2 } ) )$ .

(ISAAC 2004)

2. G ra p h cl asses s . t. H a m i lton i a n Path ca n be fou nd in poly time

Some g ra ph classes havi ng i nterval representations (bipartite permutation, interval biconvex graphs)

(ISAAC 2004)

3. Dyna m i c prog ra m m i ng to the g ra p h cl asses that have tree representations (on going)

C a ct i ( l i n e a r) ,

# 1. Ex of Dijkstra's Alg

et . a l . ( IPL , 2 0 02 ) s h owed th at the correctness of Dijkstra's alg stands for;

For each $u , v ,$ length of the shortest path between u and v = length of the longest path between u and v

For each $u , v , w ,$ , $\mathsf { d } ( u , v ) \equiv \mathsf { d } ( u , w ) + \mathsf { d } ( w , v )$

3. For each $u , v , w ,$ ${ \mathsf { d } } ( u , v ) = { \mathsf { d } } ( u , w ) + { \mathsf { d } } ( w , v )$ if and only if is on the u n iq u e path betwee n u a nd v

# 1. Ex of Dijkstra's Alg

Construct $G ^ { \prime } { = } ( V ^ { \prime } , E ^ { \prime } )$ from G=(V,E) s.t. :

V⊆ V’   
For each $u , v \in V ,$ length of the shortest path between u,v on G' = length of the longest path between u,v on G

For each $u , v \in V ,$

the shortest path between u,v on G' is unique

# 1. Ex of Dijkstra's Alg

Theorem: ExDijkstra finds a longest path if G and G' satisfy the conditions.

ExDijkstra: $G = ( V , E )$ and $G ^ { \prime } { = } ( V ^ { \prime } , E ^ { \prime } )$

p i ck a ny ve rtex w i n V;   
2. fi n d x ∈ V w i t h m ax{ d( w, x)} o n G ’; fi n d y ∈ V w i t h m ax{ d(x, y)} o n G ’;   
4 x a n d y a re th e e nd poi nts of th e long est path i n G, and $d ( x , y )$ on G' is its length.

# 1. Ex of Dijkstra's Alg (Summary)

Theorem: Vertex/edge weighted tree (linear)

Theorem: Block graph (O(|VI+|El))

( O ( | V| 2 ) )

# 1. Ex of Dijkstra's Alg (Cacti)

Cactus:

Each block is a cycle

Two cycle share at most one vertex which is a separator

![](images/df5982503f4e31c39dca4b3aaea5eceb2f42042d5d460a61c0729de4c13b9f20.jpg)

![](images/2bf0d0a63b677bd9a7e6144bd1d3f1daf238764f61816a9a2946c27642409dba.jpg)

The longest path The shortest path between = between u and v on G u and v on G'

# 1. Ex of Dijkstra's Alg (Cacti)

Sample

![](images/bd9a378077ff3c1e733ae53eb4ff01a4f9238669f8f220dd25aefec0e2eaf575.jpg)

# 1. Ex of Dijkstra's Alg (Cacti)

Sample

![](images/5452b34fa01de4eafb7f19928a55448c9633c4857e1675aaccd9249f783a96af.jpg)

# 1. Ex of Dijkstra's Alg (Cacti)

Sample

![](images/7c0a15581c8bc88d2a3c7b9e0b3cf8a547e5cdbbe43f07142cb8c4cc458fe605.jpg)

# 1. Ex of Dijkstra's Alg (Cacti)

Sample

![](images/16c84bd35a98cefe1fb1eb1a74213d288ba3a5452e5edb63e5aa9486ba5c3b18.jpg)

# 1. Ex of Dijkstra's Alg (Cacti)

Sample

![](images/9c64a8f2edd3ea3b4f2873134b4727a64476c426add32b39f945ef53e30fcd74.jpg)

# 1. Ex of Dijkstra's Alg (Cacti)

Sample

![](images/c19418b1c6a3d148d385f987f9aabbe9df45236d8bce6e9f7d01af12233dac8c.jpg)

# 1. Ex of Dijkstra's Alg (Cacti)

Sample

![](images/3c105bbc819ee55f03014157887d21918b33898e7d676bd47e875a93d82d41a4.jpg)

# Graph classes s.t. Hamiltonian Path can be found in poly time

Fact 1:

Hamiltonian Path is NP-hard on a chordal graph.

(In fact, strongly chordal split graph[Müller,1997].)

Fact 2:

Hamiltonian Path is solvable on an interval graph in linear time. [Damaschke, 1993].

Our goal:

Poly-time algorithm for Longest Path on an interval graph.

# Interval Graphs

0 An i nterval g ra ph $G = ( V , E )$ h a s a n i n te rva l representation s.t. {u,v}E iff $I _ { u } \cap I _ { v } \neq \varphi$ 5

![](images/f450d4b0bbebc753bd308f4e6adbb382db28106db29197969d8f8ce5413f942d.jpg)

![](images/6c41545555d1bc42066e4478038fc224630fcfa29227b84187219b47dbfbb6a8.jpg)

# Interval Graphs

0 An i nterval g ra ph $G = ( V , E )$ h a s a n i n te rva l representation s.t. {u,v}E iff $I _ { u } \cap I _ { v } \neq \emptyset$

![](images/b37bc0d20989b55016fa0e67c35d4ce26036ca01b8b629d81c9bfa54f6597236.jpg)

Hamiltonian Path: linear time solvable.

Longest Path: ????

Restri cted i nterval g ra phs …

![](images/4dda89f480ae41789e12bf67cfa5ec68cc3b7bb09463fb4660f864be2d041581.jpg)

# Restricted Interval Graphs

• An i nterval biconvex g ra ph G=( S ∪ Y, E) has an interval representation s.t...

![](images/9036d2b5f396aed882ff1633430ac07feb6f298c4bce8edf7dee0338e1baf8ad.jpg)  
S: integer points

http://www.jaist.ac.jp/\~uehara/ps/longest.pdf

# Restricted Interval Graphs

• I nterval biconvex g ra ph G=( S ∪ Y, E) is introduced [Uehara, Uno; 2004] from graph theoretical viewpoints;

Natural analogy of biconvex graphs (bipartite graph class)   
Generalization of proper interval graphs   
Generalization of threshold graphs

Best possible class longest path can be found in poly time …

# Poly-time alg for longest path on an interval biconvex graph (idea)

F i n d t h e t ri v i a l l o n g e st p at h P o n G [ Y] ;   
E m bed th e ve rti ces i n S i nto P as poss i b l e ;   
Adj ust e nd poi nts if n ecessa ry .

![](images/65f0f52d0bc3707a44b87dc71218d0001a71d13af53bcaefb6f848f0f0d5b1b2.jpg)

# Poly-time alg for longest path on an interval biconvex graph (idea)

F i n d t h e t ri v i a l l o n g e st p at h P o n G [ Y] ;   
E m bed th e ve rti ces i n S i nto P as poss i b l e ;   
Adj ust e nd poi nts if n ecessa ry .

![](images/fae977eb1aa5d4a6bcd1d5e4eeb80d5265a6fda8d4e88f19d6c34f164d08e10e.jpg)

# Poly-time alg for longest path on an interval biconvex graph (idea)

F i n d t h e t ri v i a l l o n g e st p at h P o n G [ Y] ;   
E m bed th e ve rti ces i n S i nto P as poss i b l e ;   
Adj ust e nd poi nts if n ecessa ry.

![](images/90c1929b5bb96a7e7ffe93ab2fa957ca9bdd305118b9149391f733a6947132f6.jpg)

# Poly-time alg for longest path on an interval biconvex graph (idea)

F i n d t h e t ri v i a l l o n g e st p at h P o n G [ Y] ;   
E m bed th e ve rti ces i n S i nto P as poss i b l e ;   
Adj ust e nd poi nts if n ecessa ry.

![](images/8fd64713f422e92719e94c816d2b4fb5be0811279738b42f7dc09f6d0429619c.jpg)

# Poly-time alg for longest path on an interval biconvex graph (idea)

F i n d t h e t ri v i a l l o n g e st p at h P o n G [ Y] ;   
E m bed th e ve rti ces i n S i nto P as poss i b l e ;

Adj ust e nd poi nts if n ecessa ry.

![](images/64be7e0e91d9cca96c97252bc174429356173269e479aa99bc2d3780a4de4211.jpg)

![](images/55eee92eb51563cf082ba2869cfbacfb8f021dd31769094e18fbb4daa4440c14.jpg)

H ow ca n we d ete rm i n e the vertices in S? Where do we em bed them?

# Poly-time alg for longest path on an interval biconvex graph (idea)

E m bed th e ve rti ces i n S i nto P as poss i b l e ;

![](images/46c4b3836f0cc3e2253ff5c42c98b2f4754a6c2c01740833de707e56d972e4cc.jpg)

![](images/b1691f7a89a906db774986873d330e61257bb23e67c10c5d50fdd4cf0e28ba1f.jpg)

# Poly-time alg for longest path on an interval biconvex graph (idea)

E m bed th e ve rti ces i n S i nto P as poss i b l e ;

![](images/34da83f50dc330ad7a1f5edfd46348b0992694486d2caba20c6bd416c2b723c4.jpg)  
http://www.jaist.ac.jp/\~uehara/ps/longest.pdf

# Open Problems

Longest Path on a n i nterval g ra ph ??

Com bi nation of DP/Dijkstra and weighted maximum matching on MPQ-tree representation?

Related to the fol lowi ng open problem ?

with a start poin t o n a n i n te rva l g ra p h ? [Damaschke, 1993].

Exte nsion to

Longest cycl e on some g ra ph classes

H a m i lton ia n cycl e/path on some g ra ph classes

http://www.jaist.ac.jp/\~uehara/ps/longest.pdf