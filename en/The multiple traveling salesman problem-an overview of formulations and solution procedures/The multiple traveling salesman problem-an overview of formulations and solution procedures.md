# The multiple traveling salesman problem: an overview of formulations and solution procedures

Tolga Bektas

Department of Industrial Engineering, Baskent University, Baglica Kampusu, Eskisehir Yolu 20. km., 06530 Ankara, Turkey

Received 2 December 2003; accepted 11 October 2004 Available online 8 January 2005

# Abstract

The multiple traveling salesman problem (mTSP) is a generalization of the well-known traveling salesman problem (TSP), where more than one salesman is allowed to be used in the solution. Moreover, the characteristics of the mTSP seem more appropriate for real-life applications, and it is also possible to extend the problem to a wide variety of vehicle routing problems (VRPs) by incorporating some additional side constraints. Although there exists a wide body of the literature for the TSP and the VRP, the mTSP has not received the same amount of attention. The purpose of this survey is to review the problem and its practical applications, to highlight some formulations and to describe exact and heuristic solution procedures proposed for this problem.

$©$ 2004 Elsevier Ltd. All rights reserved.

Keywords: Multiple traveling salesman; Survey

# 1. Introduction

A generalization of the well-known traveling salesman problem (TSP) is the multiple traveling salesman problem (mTSP), which consists of determining a set of routes for $m$ salesmen who all start from and turn back to a home city (depot). Although the TSP has received a great deal of attention, the research on the mTSP is limited. The purpose of this paper is to review the existing literature on the mTSP, with an emphasis on practical applications, integer programming formulations (ILPFs) and solution procedures devised specifically for this problem.

The rest of the paper will proceed as follows: The following section formally defines the problem and presents some important variations. Section 3 describes practical applications of the mTSP reported in the literature and explores its connections with other type of problems. Integer programming formulations, exact and heuristic solution procedures are presented in Sections 4–6, respectively. Section 7 describes the transformation-based approaches to solve the problem. Finally, Section 8 presents some concluding results and further remarks.

# 2. Problem definition and variations

The mTSP can in general be defined as follows: Given a set of nodes, let there be $m$ salesmen located at a single depot node. The remaining nodes (cities) that are to be visited are called intermediate nodes. Then, the mTSP consists of finding tours for all $m$ salesmen, who all start and end at the depot, such that each intermediate node is visited exactly once and the total cost of visiting all nodes is minimized. The cost metric can be defined in terms of distance, time, etc. Possible variations of the problem are as follows:

• Single vs. multiple depots: In the single depot case, all salesmen start from and end their tours at a single point.

On the other hand, if there exist multiple depots with a number of salesman located at each, the salesmen can either return to their original depot after completing their tour or return to any depot with the restriction that the initial number of salesmen at each depot remains the same after all the travel. The former is referred as the fixed destination case whereas the latter is named as the nonfixed destination case.   
Number of salesmen: The number of salesman in the problem may be a bounded variable or fixed a priori.   
Fixed charges: When the number of salesmen in the problem is not fixed, then each salesman usually has an associated fixed cost incurring whenever this salesman is used in the solution. In this case, the minimization of the number of salesman to be activated in the solution may also be of concern.   
Time windows: In this variation, certain nodes need to be visited in specific time periods, named as time windows. This is an important extension of the mTSP and referred to as the multiple traveling salesman problem with time windows (mTSPTW). The mTSPTW has immediate applications in school bus, ship and airline scheduling problems.   
Other special restrictions: These restrictions may consist of bounds on the number of nodes each salesman visits, the maximum or minimum distance a salesman travels or other special constraints.

The mTSP can be considered as a relaxation of the VRP, with the capacity restrictions removed. This means that all the formulations and solution approaches proposed for the VRP are also valid and applicable to the mTSP, by assigning sufficiently large capacities to the salesmen (vehicles). However, as this review is for the mTSP only, we will not describe the existing research on the VRP. The reader is referred to the book of Toth and Vigo [1] for a detailed treatment of the subject. On the other hand, when there is only a single salesman, then the mTSP reduces to the well-known TSP, for which an extensive amount of research exists (e.g. [2–5]). Since the TSP is a special case of the mTSP, all the formulations and algorithms described in this paper are also valid for the former problem.

In this paper, we will only concentrate on the research tailored specifically for the mTSP. The following section describes some applications to demonstrate the practical importance of the problem.

# 3. Applications and connections with other problems

This section is further subdivided into three parts. The first part describes the main practical applications of the mTSP. The second part points out the relationships of the mTSP with other problems. The third part specifically deals with the connections between the mTSP and the well-known VRP.

# 3.1. Main applications

Compared to the TSP, the mTSP is more adequate to model real life situations, since it is capable of handling more than one salesman. These situations arise mostly in various routing and scheduling problems. Some reported applications are presented below.

(1) Print press scheduling: One of the primary applications of the mTSP, given by Gorenstein [6], arises in scheduling a printing press for a periodical with multi-editions. Here, there exist five pairs of cylinders between which the paper rolls and both sides of a page are printed simultaneously. There exist three kind of forms, namely 4-, 6- and 8-page forms, which are used to print the editions. The scheduling problem consists of deciding which form will be on which run and the length of each run. In the mTSP vocabulary, the plate change costs are the inter-city costs. In a similar context, the mTSP can also be used to develop a production schedule for pre-printed insert advertisements for newspapers, as recently pointed out by Carter and Ragsdale [7]. In this problem, advertisers are to insert specific advertisements into or deliver with the newspaper, for distribution to different geographical regions. Each specific region receives the same set of advertisements. In the mTSP context, the regions correspond to the cities and each production line corresponds to a salesman.

(2) Crew scheduling: Svestka and Huckfeldt [8] report an application for deposit carrying between different branch banks. Here, deposits need to be picked up at branch banks and returned to the central office by a crew of messengers. The problem is to determine the routes of messengers with a total minimum cost. Lenstra and Rinnooy Kan [9] describe two similar applications, where the first application consists of finding the routes of a technical crew, which has to visit telephone boxes in North Holland. The second application involves designing the routes of vehicles to visit 200 mailboxes in Utrecht, such that the number of vehicles used is minimum. Another application of the mTSP in crew scheduling is reported by Zhang et al. [10], who investigate the problem of scheduling multiple teams of photographers to a large number of elementary and secondary schools.

(3) School bus routing problem: The problem of scheduling buses is investigated by Angel et al. [11] as a variation of the mTSP with some side constraints. The objective of the scheduling is to obtain a bus loading pattern such that the number of routes is minimized, the total distance travelled by all buses is kept at minimum, no bus is overloaded and the time required to traverse any route does not exceed a maximum allowed policy.

(4) Interview scheduling: Gilbert and Hofstra [12] describe an application of a multiperiod variation of the mTSP, where the problem arises in scheduling interviews between tour brokers and vendors of the tourism industry. Each broker corresponds to a salesman who must visit a specified set of vendor booths, which are represented by a set of $T$ cities.

(5) Mission planning: Mission planning generally arises in the context of autonomous mobile robots, where a variety of applications include construction, military reconnaissance, warehouse automation, post-office automation and planetary exploration. The mission plan consists of determining the optimal path for each robot to accomplish the goals of the mission in the smallest possible time. The mission planner uses a variation of the mTSP where there are $n$ robots, $m$ goals which must be visited by some robot, and a base city to which all robots must eventually return. The application of the mTSP in mission planning is reported by Brummit and Stentz [13] and in unstructured environments by Brummit and Stentz [14]. Planning of autonomous robots is modelled as a variant of the mTSP by Yu et al. [15] in the field of cooperative robotics. Similarly, the routing problems arising in the planning of unmanned aerial vehicle applications, as investigated by Ryan et al. [16], can be modelled as an mTSP with time windows.

(6) Hot rolling scheduling: In the iron and steel industry, orders must be scheduled on the hot strip rolling mill for a production shift such that the total transition (setup) cost in the production sequence is minimized. A recent application of modelling such a problem encountered in an iron and steel complex in China as an mTSP is given by Tang et al. [17]. Here, the orders correspond to the cities and the distance between two cities is the penalty cost for production changeover between two orders. The solution of the model will yield a complete schedule for the hot strip rolling mill.

(7) Design of global navigation satellite system surveying networks: A very recent and an interesting application of the mTSP, as investigated by Saleh and Chelouah [18] arises in the design of global navigation satellite system (GNSS) surveying networks. A GNSS is a space-based satellite system which provides coverage for all locations worldwide and are quite crucial in real-life applications such as early warning and management for disasters, environment and agriculture monitoring, etc. The goal of surveying is to determine the geographical positions of unknown points on and above the earth using satellite equipment. These points, on which receivers are placed, are co-ordinated by a series of observation sessions. When there are multiple receivers or multiple working periods, the problem of finding the best order of sessions for the receivers can be formulated as an mTSP. For technical details, the reader is referred to Saleh and Chelouah [18].

# 3.2. Relationships with other problems

The above-mentioned practical cases can directly be modelled as an mTSP, with some minor extensions if necessary. However, the mTSP is also important in that it arises as a subproblem in the solution of more general problems. One example to such a problem is balancing the workload among the salesmen, as discussed by Okonjo-Adigwe [19]. Here, an mTSP-based modelling and solution approach is presented to solve a workload scheduling problem with additional restrictions, such as lower and upper bounds on travel times and the total weight of each salesmen. Another example is the overnight security service problem, investigated by Calvo and Cordone [20]. This problem consists of assigning duties to a number of guards, who are to perform routine inspection services on a given set of locations. There are also some constraints that should be respected, such as capacity and time windows. A decomposition approach is offered for the solution of the problem, in which one of the subproblems is an mTSPTW.

The mTSP also arises as a subproblem in scheduling of quay cranes in ship operation planning. This problem is investigated by Kim and Park [21], who utilize the mTSP to find tight lower bounds in a branch and bound algorithm offered for the solution to this problem.

The mTSP with time windows can be used to model problems in intermodal freight transport, as noted by Macharis and Bontekoning [22]. In this context, Wang and Regan [23] model a local truckload pickup and delivery problem as an asymmetric mTSP with time windows. The solution of the problem is obtained through an iterative method using timewindow discretization.

An interesting application of the mTSP lies in the problem of coordinating the motion of multiple objects, as pointed out by Basu et al. [24]. Such a problem may arise in the assembly of electronic circuits, memory management of distributed systems, and coordination of mobile robots in a structured space such as a warehouse. The problem is defined on a rectangular grid which is partitioned into a number of squares. The squares may either contain an object or may be blank. Then, the optimal movement of objects on a grid with multiple blank spaces can be found using an mTSP model.

# 3.3. Connections with the VRP

Due to its close connections, mTSP can also be utilized in solving several types of VRPs. For instance, Mole et al. [25] discuss several vehicle routing algorithms, and present a heuristic method which searches over a solution space formed by the large number of feasible solutions to an mTSP. In a similar context, the mTSP can be used to calculate the minimum number of vehicles required to serve a set of customers in a distance-constrained VRP, in which each customer has an associated nonnegative demand and each vehicle cannot travel more than a predefined amount of distance (see [26,27]). The mTSP also appears as a firststage problem in a two-stage solution procedure of a VRP with stochastic service times, where the solution found in the first-stage is used to calculate the expected costs in the second stage. This is discussed further by Hadjiconstantinou and Roberts [28]. The close connection of the mTSP and the VRP further motivates the interest in the former problem. In fact, Ralphs [29] mentions that the VRP instances arising in practice can be extremely difficult to solve, since the underlying mTSP is also complex in nature. This statement, in turn, raises the need to efficiently solve the mTSP in order to attack large-scale VRPs arising in real-life situations.

The mTSP is also related to the pickup and delivery problem (PDP) in that the latter is a constrained version of the former as noted by Ruland and Rodin [30]. The PDP consists of determining the optimal routes for a set of vehicles to fulfill the customer requests, which are specified by an origin-destination pair. The additional restriction is that origins must precede destinations in each tour. If the customers are to be served within specific time intervals, then the problem becomes the PDP with time windows (PDPTW). As also indicated by Mitrovi´c-Mini´c et al. [31], the PDPTW reduces to the mTSPTW if the origin and destination points of each request coincide.

# 3.4. Discussion

As a summary of the applications presented in this section, we provide Table 1, which shows the possible application areas of the mTSP, where the first column shows the application context and the second presents the specific type of application.

As Table 1 presents, the mTSP can be used in a variety of planning/scheduling type problems, ranging from scheduling of prints to transportation and mission planning. Thus, the mTSP is not only important for theoretical interest, but also for its capability to model many strategic decision problems.

Although the mTSP is a relaxation of the VRP and all the solution approaches developed for the latter are valid for the former, these approaches may not always be efficient and well-suited to the mTSP. In fact, since these procedures are not developed specifically for the mTSP, degeneracies may arise in the solution process, causing unnecessary difficulties. Although not many, a number of solution procedures have been proposed in the literature, tailored exclusively for the mTSP. These procedures generally consist of algorithms based on integer linear programming formulations and transformations of the problem to the TSP.

In Section 4, we initially present the several integer programming formulations of the mTSP. We then overview the exact solution procedures developed for the mTSP in Section 5. Heuristic solution procedures and transformations of the mTSP to the standard TSP are presented in subsequent sections.

Table 1 Application contexts for the mTSP   

<table><tr><td>Application context</td><td>Type of application</td></tr><tr><td>Print Scheduling</td><td>Print press scheduling [6] Pre-print advertisement scheduling [7]</td></tr><tr><td>Workforce planning</td><td>Bank crew scheduling [8] Technical crew scheduling [9] Photographer team scheduling [10] Interview scheduling [12] Workload balancing [19]</td></tr><tr><td>Transportation planning</td><td>School bus routing [11] Crane scheduling [21] Local truckload pickup and delivery [23]</td></tr><tr><td>Mission planning</td><td>Planning of autonomous mobile robots [1315,24]</td></tr><tr><td>Production planning</td><td>Planning of unmanned air vehicles [16]</td></tr><tr><td>Satellite systems</td><td>Hot rolling scheduling [17] Designing satellite surveying</td></tr></table>

# 4. Integer programming formulations

Different types of integer programming formulations are proposed for the mTSP. Before presenting them, some technical definitions are as follows. The mTSP is defined on a graph $G = ( V , A )$ , where $V$ is the set of $n$ nodes (vertices) and $A$ is the set of arcs (edges). Let $C = ( c _ { i j } )$ be a cost (distance) matrix associated with $A$ . The matrix $C$ is said to be symmetric when $c _ { i j } = c _ { j i } , \forall ( i , j ) \in A$ and asymmetric otherwise. If $c _ { i j } + c _ { j k } \geqslant c _ { i k } , \forall i , j , k \in V$ , $C$ is said to satisfy the triangle inequality.

Various integer programming formulations for the mTSP have been proposed earlier in the literature, among which there exist assignment-based formulations, a tree-based formulation and a three-index flow-based formulation. We now present each of them in the following sections.

# 4.1. Assignment-based integer programming formulations

The mTSP is usually formulated using an assignmentbased double-index integer linear programming formulation. We first define the following binary variable:

$$
x _ { i j } = { \left\{ \begin{array} { l l } { 1 } & { { \mathrm { i f ~ } } \operatorname { a r c } ( i , j ) { \mathrm { ~ i s ~ u s e d ~ o n ~ t h e ~ t o u r } } , } \\ { 0 } & { { \mathrm { o t h e r w i s e } } . } \end{array} \right. }
$$

Then, a general scheme of the assignment-based directed integer linear programming formulation of the mTSP can

be given as follows:

mize

$$
\begin{array} { r l } & { \frac { n } { 2 } \displaystyle \sum _ { i = 1 } ^ { n } c _ { i j } x _ { i j } } \\ & { \frac { n } { 2 } \displaystyle \sum _ { i = 1 } ^ { n } x _ { i j } = m , } \\ & { \frac { n } { 2 } \displaystyle x _ { i j } = m , } \\ & { \displaystyle \sum _ { j = 2 } ^ { n } x _ { j 1 } = m , } \\ & { \displaystyle \sum _ { i = 1 } ^ { n } x _ { i j } = 1 , \ j = 2 , \ldots , n , } \\ & { \displaystyle \sum _ { j = 1 } ^ { n } x _ { i j } = 1 , \ j = 2 , \ldots , n , } \\ & { \displaystyle \sum _ { i = 1 } ^ { n } x _ { i j } = 1 , \ i = 2 , \ldots , n , } \end{array}
$$

+subtour elimination constraints,

$$
x _ { i j } \in \{ 0 , 1 \} , \forall ( i , j ) \in A ,
$$

where (3), (4) and (6) are the usual assignment constraints, (1) and (2) ensure that exactly $m$ salesmen depart from and return back to node 1 (the depot). Although constraints (2) are already implied by (1), (3) and (4), we present them here for the sake of completeness. Constraints (5) are used to prevent subtours, which are degenerate tours that are formed between intermediate nodes and not connected to the origin. These constraints are named as subtour elimination constraints (SECs).

Several SECs have been proposed for the mTSP in the literature. The first group of SECs is based on that of Dantzig et al. [32] originally proposed for the TSP, but also valid for the mTSP. These constraints can be shown as follows:

$$
\sum _ { i \in S } \sum _ { j \in S } x _ { i j } \leqslant | S | - 1 , \quad \forall S \subseteq V \backslash \{ 1 \} , \ : \ : S \neq \emptyset
$$

or alternatively in the following form

$$
\sum _ { i \notin { S } } \sum _ { j \in { S } } x _ { i j } \geqslant 1 , \quad \forall { S } \subseteq { V } \backslash \{ 1 \} , { S } \ne \emptyset .
$$

Constraints (7) or (8) impose connectivity requirements for the solution, i.e. prevent the formation of subtours of cardinality $S$ not including the depot. Unfortunately, both families of these constraints increase exponentially with increasing number of nodes, hence are not practical for neither solving the problem nor its linear programming relaxation directly. Miller et al. [33] overcame this problem by introducing $O ( n ^ { 2 } )$ additional continuous variables, namely node potentials, resulting in a polynomial number of SECs. Their SECs are given as follows (denoted by MTZ-SECs):

$$
u _ { i } - u _ { j } + p x _ { i j } \leqslant p - 1 \quad { \mathrm { f o r ~ } } 2 \leqslant i \neq j \leqslant n .
$$

Here, $p$ denotes the maximum number of nodes that can be visited by any salesman. The node potential of each node indicates the order of the corresponding node in the tour.

Another group of SECs for the mTSP which require augmenting the original cost matrix with new rows and columns is proposed by Svestka and Huckfeldt [8]. However, Gavish [34] showed that their constraints are not correct for $m \geqslant 2$ and provided the correct constraints as follows:

$$
u _ { i } - u _ { j } + ( n - m ) x _ { i j } \leqslant n - m - 1 \quad { \mathrm { f o r ~ } } 2 \leqslant i \neq j \leqslant n .
$$

Other MTZ-based SECs for the mTSP have also been proposed. The following constraints are due to Kulkarni and Bhave [35] (denoted by KB-SECs):

$$
u _ { i } - u _ { j } + L x _ { i j } \leqslant L - 1 \quad { \mathrm { f o r ~ } } 2 \leqslant i \neq j \leqslant n .
$$

In these constraints, the $L$ is same as $p$ in (9). It is clear that MTZ-SECs and KB-SECs are equivalent.

A very recent group of SECs for the mTSP is due to Kara and Bektas [36]. These constraints differ from other existing SECs with respect to an inclusion of an additional side constraint, which can be used to impose a lower bound on the number of nodes a salesman visits $( K )$ . Such lower bounds may arise in case of collections, where each salesman may be required to stop by at least $K$ customers to pick up some goods, etc. These constraints are given as follows:

$$
\begin{array} { r l } & { u _ { i } + ( L - 2 ) x _ { 1 i } - x _ { i 1 } \leqslant L - 1 , \quad i = 2 , \ldots , n , } \\ & { } \\ & { u _ { i } + x _ { 1 i } + ( 2 - K ) x _ { i 1 } \geqslant 2 , \quad i = 2 , \ldots , n , } \\ & { } \\ & { u _ { i } - u _ { j } + L x _ { i j } + ( L - 2 ) x _ { j i } \leqslant L - 1 , } \\ & { \quad 2 \leqslant i \neq j \leqslant n . } \end{array}
$$

Here, $L$ has the same meaning as in (11). Constraints (12) and (13) are used to impose bounds on the number of nodes a salesman visits.

# 4.2. Laporte and Nobert’s formulations

Laporte and Nobert [37] presented two formulations for the mTSP, for asymmetrical and symmetrical cost structures, respectively, and consider a common fixed cost $f$ for each salesman used in the solution. These formulations include an exponential number of SECs, and are thus used in a cutting plane framework. These formulations are also based on the two-index variable $x _ { i j }$ defined previously. The formulation for the asymmetric mTSP is as follows:

$$
\begin{array}{c} \sum _ { i \ne k } ^ { \sum } c _ { i j } x _ { i j } + f m  \\ { \sum _ { i \ne j } ^ { \lfloor \# 2 \rfloor } ( x _ { 1 j } + x _ { j 1 } ) = 2 m , } \\ { \sum _ { i \ne k } ^ { \sum } x _ { i k } = 1 , \quad k = 2 , \ldots , n , } \\ { \sum _ { j \ne k } x _ { k j } = 1 , \quad k = 2 , \ldots , n , } \end{array}
$$

$$
\begin{array} { r l } & { \displaystyle \sum _ { i \neq j ; i , j \in S } x _ { i j } \leqslant | S | - 1 , } \\ & { \quad \quad 2 \leqslant | S | \leqslant n - 2 , \ S \subseteq V \backslash \{ 1 \} , } \\ & { \quad \quad x _ { i j } \in \{ 0 , 1 \} , \quad \forall i \neq j , } \\ & { \quad \quad m \geqslant 1 \ \mathrm { a n d ~ i n t e g e r } . } \end{array}
$$

This formulation is a pure binary integer formulation where the objective is to minimize the total cost ofthe travel as well as the total number of salesmen used in the solution. Note that constraints (16) and (17) are the standard assignment constraints, and constraints (18) are the SECs of Dantzig et al. [32]. The only different constraints are (15), which impose degree constraints on the depot node.

Laporte and Nobert’s formulation for the symmetric mTSP is as follows:

s.t.

$$
\begin{array} { l } { \displaystyle \sum _ { i < j } c _ { i j } x _ { i j } + f m } \\ { \displaystyle \sum _ { j = 2 } ^ { n } x _ { 1 j } = 2 m , } \\ { \displaystyle \sum _ { i < k } x _ { i k } + \sum _ { j > k } x _ { k j } = 2 , \quad k = 2 , \ldots , n , } \end{array}
$$

$E _ { 2 }$ : edges adjacent to the depot $| E _ { 2 } | = y$ , $0 \leqslant y \leqslant m$ ), $E _ { 3 }$ : edges not adjacent to the depot $( | E _ { 3 } | = m - y )$ .

We define the following binary variable for this formulation:

$$
x _ { l } ^ { t } = \left\{ { \begin{array} { r r } { 1 } & { { \mathrm { i f ~ } } \mathrm { e d g e } \ l { \mathrm { ~ b e l o n g s ~ t o ~ t h ~ } } } \\ { \ } & { ( t = 1 , 2 , 3 ; l \in E ) , } \\ { 0 } & { { \mathrm { o t h e r w i s e } } } \end{array} } \right.
$$

Also, let $E ^ { i }$ be the set of edges adjacent to node $i$ . Then, the formulation is as follows:

$$
\begin{array} { r l } { \mathrm { m i n i m i z e } } & { \displaystyle \sum _ { l \in E } c _ { l } ( x _ { l } ^ { 1 } + x _ { l } ^ { 2 } + x _ { l } ^ { 3 } ) } \\ { \mathrm { s . t . } } & { \displaystyle \sum _ { l \in ( S , \bar { S } ) } x _ { l } ^ { 1 } \geqslant 1 , \quad S \subset V , | S | \geqslant 1 , } \\ & { \displaystyle \sum _ { l \in ( S , \bar { S } ) } x _ { l } ^ { 1 } \geqslant 1 , \quad S \subset V , | S | \geqslant 1 , } \end{array}
$$

$$
\begin{array} { r l } & { ~ \displaystyle \sum _ { i < j ; i , j \in S } x _ { i j } \leqslant | S | - 1 , } \\ & { ~ i < j ; i , j \in S } \\ & { ~ 3 \leqslant | S | \leqslant n - 2 , ~ S \subseteq V \backslash \{ 1 \} , } \\ & { ~ x _ { i j } \in \{ 0 , 1 \} , ~ 1 < i < j , } \\ & { ~ x _ { 1 j } \in \{ 0 , 1 , 2 \} , ~ j = 2 , . . . , n , } \\ & { ~ m \geqslant 1 \mathrm { ~ a n d ~ i n t e g e r } . } \end{array}
$$

$$
\begin{array} { r l } & { \frac { \gamma } { \lambda } \succcurlyeq ( \frac { \lambda } { \lambda } + \frac { \lambda } { 2 } + \frac { \lambda } { 3 } ) } \\ & { \leq \sum _ { j \in \mathcal { K } _ { j } } \frac { \gamma } { \lambda } \leq \lambda \leq \frac { \lambda } { 2 } , } \\ & { \leq \lambda \leq \frac { \lambda } { 2 } , } \\ & { \leq \frac { \gamma } { \lambda } \leq \frac { \lambda } { 2 } , } \\ & { \leq \frac { \gamma } { \lambda } \leq \frac { \lambda } { 2 } , } \\ & { \leq \frac { \gamma } { \lambda } \leq \frac { \lambda } { 2 } , } \\ & { \leq \frac { \gamma } { \lambda } \leq \frac { \lambda } { 2 } , } \\ & { \leq \frac { \gamma } { \lambda } \leq \frac { \gamma } { \lambda } , } \\ & { \leq \frac { \gamma } { \lambda } \leq \frac { \gamma } { \lambda } , } \\ & { \leq \frac { \gamma } { \lambda } \leq \frac { \gamma } { \lambda } , } \\ & { \leq \frac { \gamma } { \lambda } \leq \frac { \gamma } { \lambda } , } \\ & { \leq \frac { \gamma } { \lambda } \leq \frac { \gamma } { \lambda } , } \\ & { \leq \frac { \gamma } { \lambda } \leq \frac { \gamma } { \lambda } + \frac { \gamma } { \lambda } \leq 2 , } \\ & { \leq \frac { \gamma } { \lambda } \leq \frac { \gamma } { \lambda } , } \\ & { \leq \frac { \gamma } { \lambda } \leq \frac { \gamma } { \lambda } \leq ( \frac { \gamma } { \lambda } ) , \ \ \varepsilon \leq 1 , \ \varepsilon } \end{array}
$$

The interesting issue about this formulation is that it is not a pure binary integer formulation due to the variable $x _ { 1 j }$ which can either be 0, 1 or 2. Note here that the variable $x _ { i j }$ is only defined for $i < j ,$ , since the problem is symmetric and only a single variable is sufficient to represent each edge used in the solution. Constraints (21) and (22) are the degree constraints on the depot node and intermediate nodes, respectively. Other constraints are as previously defined.

# 4.3. $k$ -Degree centre tree-based formulation

A formulation for the symmetric mTSP is due to Christofides et al. [38]. This formulation is based on a $k \mathrm { \cdot }$ - degree centre tree $k$ -DCT), which is a tree where the depot has exactly $k$ adjacent arcs. This formulation can also be used to derive a lower bound to a VRP. In the formulation, the edge set is partitioned as follows (this representation is due to Laporte [39]):

$E _ { 0 }$ : edges not belonging to the solution, $E _ { 1 }$ : edges forming the $k$ -DCT,

In the formulation, $( S , { \bar { S } } )$ denotes the set of all edges with one end in $S$ and the other in $\bar { S }$ . The objective is to minimize the total cost of each edge used in the solution, where $c _ { l }$ denotes the cost of using edge $l$ in the solution. Constraints (27) impose that the tree is connected. Furthermore, constraints (28) imply that there should be $k = 2 m - y$ arcs adjacent to the depot. Other constraints (29)–(31) are associated with the number of arcs in the solution. Finally, constraints (32) imply that the degree of every node other than the depot is 2.

# 4.4. A flow-based formulation

Christofides et al. [38] proposed a three-index VRP formulation based on MTZ-SECs. Their formulation can be adapted to the mTSP by excluding the capacity and cost constraints. Although this formulation is proposed for the VRP, we would like to introduce the adaptation of this formulation to the mTSP in that it is the only three-index formulation with interesting features. Before presenting the formulation, we define the following three-index variable:

$$
x _ { i j k } = \left\{ { \begin{array} { c l } { 1 } & { { \mathrm { i f ~ } } { \mathrm { v e h i c l e ~ } } k } \\ { \qquad { \mathrm { n o d e ~ } } i , } \\ { 0 } & { { \mathrm { o t h e r w i s e . } } } \end{array} } \right.
$$

The formulation can then be given as follows:

$$
\begin{array} { l } { { \mathrm { m i r c } \displaystyle \sum _ { i = 1 } ^ { n } \sum _ { j = 1 } ^ { n } c _ { i j } \sum _ { k = 1 } ^ { m } \sum _ { \substack { k = 1 } } ^ { m } } } \\ { { \mathrm { s . t . } \sum _ { i = 1 } ^ { n } \sum _ { k = 1 } ^ { m } \sum _ { i \neq j \in \mathbf { I } _ { i } \backslash k } = 1 , \quad j = 1 , \ldots , n , } } \\ { { \mathrm { ~ } \displaystyle \sum _ { i = 1 } ^ { n } x _ { i j k } - \sum _ { j = 1 } ^ { n } x _ { j j k } = 1 , \quad } } \\ { { \mathrm { ~ } \displaystyle \sum _ { i = 1 } ^ { n } x _ { i j k } - \sum _ { j = 1 } ^ { n } x _ { j j k } = 0 , } } \\ { { \mathrm { ~ } \displaystyle \sum _ { k = 1 } ^ { n } \dots , \dots , m , \quad p = 1 , \ldots , n , } } \\ { { \mathrm { ~ } \displaystyle \sum _ { j = 1 } ^ { n } x _ { 1 j k } = 1 , \quad k = 1 , \ldots , m , } } \end{array}
$$

$$
\begin{array} { l } { { \displaystyle u _ { i } - u _ { j } + n \sum _ { k = 1 } ^ { m } x _ { i j k } \leqslant n - 1 , } } \\ { { \displaystyle i \neq j = 2 , \ldots , n } } \\ { { \displaystyle x _ { i j k } \in \{ 0 , 1 \} , \quad \forall i , j , k . } } \end{array}
$$

Constraints (35) state that each customer should be visited exactly once and (36) are the flow conservation constraints which ensure that once a salesman visits a customer, then he must also depart from the same customer. Constraints (37) ensure that each vehicle is used exactly once and (38) are the extensions of MTZ-based SECs to a three-index model. Unfortunately, since the number of variables in this formulation is enormous even for moderate sized mTSPs, it may not be practical to directly solve this formulation to optimality.

# 5. Exact algorithms

The first approach to solve the mTSP directly, without any transformation to the TSP (see Section 7) is due to Laporte and Nobert [37], who propose an algorithm based on the relaxation of some constraints of the problem. The motivation for such a direct approach is that a transformed problem would include many equivalent suboptimal solutions and thus would be harder to solve. The problem they consider is an mTSP with a fixed cost $f$ associated with each salesman, activated whenever a salesman is used in the solution. The algorithm consists of solving the problem by initially relaxing the SECs and performing a check as to whether any of the SECs are violated, after an integer solution is obtained. If this is the situation, then a constraint is introduced to remove such a subtour. This approach is named as the straight algorithm. As opposed to this approach, a reverse algorithm is also considered where the SECs are relaxed again but checking is performed before an integer solution has been reached. The authors report that better computational results have been obtained with the reverse algorithm and problems up to 100 nodes have been solved to optimality on a CYBER 173 computer. An interesting result of this paper in terms of the solution strategies for the mTSP is the following: The solution time of the algorithm decreases with $m$ , but it takes longer to solve the transformed problem as $m$ increases. This result is probably due to the degeneracy of the transformed problem, which grows as $m$ increases.

Ali and Kennington [40] propose a branch- and boundbased algorithm for the asymmetric TSP. The algorithm uses a Lagrangean relaxation of the degree constraints and a subgradient algorithm to solve the Lagrangean dual. The algorithm was tested on asymmetrical problems with sizes up to $n = 1 0 0$ , as well as symmetrical and Euclidean problems with sizes up to $n = 5 9$ .

The first attempt to solve large-scale symmetric mTSPs to optimality is due to Gavish and Srikanth [41]. The proposed algorithm is a branch-and-bound method, where lower bounds are obtained from the following Lagrangean problem constructed by relaxing the degree constraints. The Lagrangean problem is solved using a degree-constrained minimal spanning tree which spans over all the nodes. Lagrange multipliers are updated by a subgradient optimization procedure and fast sensitivity analysis techniques are applied to reduce the problem size. Extensive computational analyses are performed and the authors were able to solve nonEuclidean problems of sizes up to 500 nodes and $m = 2 , 4 , 6 , 8 , 1 0 .$ . and Euclidean problems up to 100 cities and 10 salesmen with this algorithm on an $\mathrm { I B M } ~ 3 0 3 2$ and an IBM 3081D computer. The results indicate that the integer gap obtained by the Lagrangean relaxation decreases as the problem size increases and turns out to be zero for all problems with $n \geqslant 4 0 0$ . Euclidean problems are shown to be harder than nonEuclidean ones. The algorithm is also compared to that of Ali and Kennington [40] and Laporte and Nobert [37] and the authors state that their algorithm “appears to be significantly superior”. Transformations to the TSP were also tested but for larger values of $m$ $( m \geqslant 4 )$ , the transformed problem happened to be harder to solve than the original one.

Another exact solution method proposed for the mTSP is due to Gromicho et al. [42]. This paper considers the asymmetric mTSP with a fixed number of salesman. The algorithm is based on a quasi-assignment (QA) relaxation obtained by relaxing the SECs, since the QA-problem is solvable in polynomial time. An additive bounding procedure is applied to strengthen the lower bounds obtained via different $r$ -arborescence and $r$ -anti-arborescence relaxations and this procedure is embedded in a branch-andbound framework. It is observed that the additive bounding procedure has a significant effect in improving the lower bounds, for which the QA-relaxation yields poor bounds. The proposed branch-and-bound algorithm is superior to the standard branch-and-bound approach with a QA-relaxation in terms of number of nodes, ranging from $1 0 \%$ less to 10 times less. Symmetric instances are observed to yield larger improvements. Using an IBM PS/70 computer with an 80386 CPU running at $2 5 \mathrm { M H z }$ , the biggest instance solved via this approach has 120 nodes with the number of salesman ranging from 2 to 12 in steps of one [43].

# 6. Heuristic solution procedures

One of the first heuristics addressing the problem of $m$ - tours in TSP with some side conditions is due to Russell [44], although the solution procedure is based on transforming the problem to a single TSP on an expanded graph. The algorithm is an extended version of the Lin and Kernighan [45] heuristic originally developed for the TSP. Another heuristic based on an exchange procedure for the mTSP is given by Potvin et al. [46].

A parallel processing approach to solve the mTSP using evolutionary programming is proposed by Fogel [47]. The approach considers two salesmen and an objective function minimizing the difference between the lengths of the routes of each salesman. Problems with 25 and 50 cities were solved and it is noted that the evolutionary approach obtained exceedingly good near-optimal solutions.

Several artificial neural network (NN) approaches have also been proposed to solve the mTSP, but they are generally extended versions of the ones proposed for the TSP. Wacholder et al. [48] have extended the Hopfield-Tank ANN model to the mTSP but their model has been evaluated to be too complex with its inability to guarantee feasible solutions [49]. Hsu et al. [50] presented a neural network approach to solve the mTSP, based on solving $m$ standard TSPs. The authors state that their results are superior to that of Wacholder et al. [48]. A self-organizing NN approach for the mTSP is due to Vakhutinsky and Golden [51], which is based on the elastic net approach developed for the TSP. Another self-organizing NN approach for the mTSP is proposed by Goldstein [52]. Torki et al. [53] describe a self-organizing NN for the VRP based on an enhanced mTSP NN model. Recently, Modares et al. [54] and Somhom et al. [49] developed a self-organizing NN approach for the mTSP with a minmax objective function, which minimizes the cost of the most expensive route among all salesmen. Their approach seems to outperform the elastic net approach.

Utilizing genetic algorithms (GA) for the solution of mTSP seems to be first due to Zhang et al. [10]. A recent application by Tang et al. [17], uses genetic algorithms to solve the mTSP model developed for hot rolling scheduling. The approach is based on modeling the problem as an mTSP, converting it into a single TSP and applying a modified genetic algorithm to obtain a solution. Yu et al. [15] also use GAs to solve the mTSP in path planning.

Tabu search is used in solving a mTSP with time windows by Ryan et al. [16]. The authors offer an integer linear programming formulation, but solve the problem through a reactive tabu search algorithm within a discrete event simulation framework.

Recently, Song et al. [55] proposed an extended simulated annealing approach for the mTSP with fixed costs associated with each salesman. The approach is tested on an mTSP with 400 cities and three salesman, which, however, required about $5 1 \mathrm { { m i n } }$ to be solved on an IBM PC-586 $( 4 0 0 \mathrm { M H z } )$ .

Gomes and Von Zuben [56] present a neuro-fuzzy system based on competitive learning to solve the mTSP along with the capacitated VRP. The proposed method employs unsupervised learning of the network guided by a fuzzy rule base. Sofge et al. [57] implemented and compared a variety of evolutionary computation algorithms to solve the mTSP, including the use of a neighborhood attractor schema, the shrink-wrap algorithm for local neighborhood optimization, particle swarm optimization, Monte-Carlo optimization, genetic algorithms and evolutionary strategies.

# 7. Transformations to the TSP

One of the approaches used for solving the mTSP is to transform the problem to a standard TSP, thus being able to use any algorithm developed for the latter to be used to obtain a solution to the former. One of the first transformations for the single depot mTSP is due to Gorenstein [6]. He proposes that a TSP with $m$ salesmen can be solved using an augmented TSP with $( m - 1 )$ additional home cities, where infinite costs are assigned to home-to-home distances to prohibit such travels and zero costs are assigned between additional ‘home cities’ and other cities. The minimum cost solution for the single salesman and the multiple salesmen problem will be the same. However, Svestka and Huckfeldt [8] argue that this transformation will not be appropriate and result in an unnecessary increase in the distance matrix. Instead, they suggest a transformation where the original distance matrix is augmented with $m - 1$ new rows and columns such that each new row and column is a duplicate of the first row and column of the original distance matrix. This algorithm initially solves the assignment problem defined by constraints (3) and (4) and checks whether any of the SECs are violated. If there exist such violated constraints, then the distance matrix is modified as to introduce the violated constraints into the problem and the resulting assignment problem is solved again. The algorithm keeps solving such assignment problems until all the constraints are satisfied and the procedure terminates with an optimal solution. The authors have solved problems with up to 60 cities. Two main results that the authors found is that the hardest case for the mTSP is the one-salesman case, and the minimum computation time is achieved when $3 \leqslant n / m \leqslant 7$ .

Orloff [58] has provided a general transformation of the $m$ vehicle general routing problem $\mathbf { \dot { \nabla } } m$ -GRP) to a GRP on a modified graph. It is also shown as a special case that solving any mTSP is equivalent to a TSP solution on a transformed graph. Based on this result, a subtour elimination algorithm for the solution of the mTSP is also presented.

Bellmore and Hong [59] showed that the asymmetric mTSP with $m$ salesmen and $n$ nodes can be converted into a standard asymmetric TSP with $( n + m - 1 )$ nodes. This study also considers a fixed cost for each salesman $C _ { i }$ , incurring only when salesman $i$ is activated. A similar transformation is due to Hong and Padberg [60], where the symmetric mTSP with $m$ salesmen and $n$ nodes is transformed into a standard symmetric TSP with $( n + m + 4 )$ nodes, considering the fixed charges as well. Rao [61] extended the transformation given by Bellmore and Hong [59] for the asymmetrical case to a standard symmetric TSP with $( n + m - 1 )$ nodes. A mathematically equivalent formulation to that of Rao [61] was given by Gheysens [62]. Lastly, Jonker and Volgenant [66] improved the standard transformation of the symmetric multiple traveling salesman problem to a standard TSP with a sparser edge configuration. They argue that introducing $m - 1$ copies of the depot results in a highly degenerate transformed problem, where an optimal solution of the mTSP corresponds to $m !$ optimal solutions of the TSP. The authors indicate that, with a sparser edge configuration around the duplicated depot, the transformed problem turns out to be less degenerate and when employed in a branchand-bound scheme, the procedure has much less computational effort compared to that of Gavish and Srikanth [41].

There also exist a number of transformations of the multidepot mTSP to the standard TSP in the literature. The most relevant references to our discussion are as follows: Laporte et al. [63] considered the fixed destination MMP with a transformation resulting in a constrained assignment problem which is used in a branch-and-bound scheme. As GuoXing [64] points out, this is an incomplete transformation since the resulting problem has nonassignment constraints. As for the nonfixed destination case, a complete transformation of the asymmetric multidepot mTSP to the standard asymmetric TSP has been given by GuoXing [64]. However, Kara and Bektas [36] propose a polynomial-size integer linear programming model for this problem and show that solving the transformed problem is far more arduous than solving the original problem.

# 8. Conclusion

The multiple traveling salesman problem is an important problem in terms of both theoretical and practical reasons. First of all, it generalizes the traveling salesman problem (TSP) and can be studied to achieve a better understanding of the TSP from a theoretical point of view. On the other hand, by incorporating additional side constraints such as capacity, distance and time windows restrictions, it could easily be extended to a variety of vehicle routing problems (VRPs). A natural consequence of these discussions reveal the evident role of the mTSP in the context of the TSP and the VRP, in that it links these two important problems. Hence, the mTSP itself plays a central role in practical distribution and routing. Unfortunately, not much has been done on the problem and its solution methods.

Table 2 Solution procedures proposed for the mTSP   

<table><tr><td>Type of approach</td><td>Solution procedure</td></tr><tr><td>Exact solution</td><td>Integer linear programming formulations [35,36] Cutting plane [37] Branch and Bound [40,42] Lagrangean relaxation + branch and</td></tr><tr><td>Heuristics</td><td>bound [41] Simple heuristics [44,46] Evolutionary algorithm [47] Simulated annealing [55]</td></tr><tr><td></td><td>Tabu search [16] Genetic algorithms [10,15,17]</td></tr><tr><td></td><td></td></tr><tr><td>Transformations Asymmetric mTSP to asymmetric TSP [59]</td><td>Neural networks [4854]</td></tr></table>

As far as the solution of the problem is concerned, we present Table 2, which summarizes the existing solution procedures proposed for the mTSP. The first column of the table indicates the type of approach whereas the second column refers to the specific solution procedure.

As Table 2 clearly presents, several exact solution procedures exist, consisting mainly of branch-and-bound type methods, which are limited to solving only problems of reasonable sizes. On the other hand, we observe that the literature has a tendency on heuristic solution techniques, of which Neural Network-based procedures seem to be the most popular. There also exist some transformation-based procedures.

Solution procedures based on transforming the mTSP to the standard TSP do not seem efficient, since the resulting TSP is highly degenerate, especially with the increasing number of salesman. This is also pointed out for the mTSP in [37,65] and for the multidepot mTSP in [36]. However, efforts in reducing the amount of degeneracy in the transformed problem may lead to efficient solution procedures, which is the approach taken in [66]. For now, efficient exact solution procedures for the problem seem to be branchand-bound methods provided that good initial bounds are used. In general, biggest asymmetric mTSPs solved to optimality have about 500 nodes and symmetric problems with about 100 nodes (assuming a limited number of salesman). In order to optimally solve larger problems, we believe that better integer programming formulations and exact solution procedures specifically tailored for the mTSP still deserve attention.

As far as the heuristic algorithms for the mTSP are concerned, the previous literature has an emphasis on artificial neural networks. However, we believe that other modern heuristic methodologies for the mTSP deserve much more attention. To the best of our knowledge, no efficient heuristic algorithms exist for the solution of large-scale mTSPs. We offer for further research the application of heuristics to the mTSP that are known to be very successful for the solution of VRPs, such as tabu search (see [67]).

# Acknowledgements

The author would like to thank Imdat Kara for suggesting the topic. Thanks are also due to Ben Lev and the two anonymous referees for their valuable comments, which helped to improve the presentation of the subject.

# Список литературы

[1] Toth P, Vigo D, editors. The vehicle routing problem. SIAM Monographs on Discrete Mathematics and Applications, Philadelphia, 2002.   
[2] Golden B, Levy L, Dahl R. Two generalizations of the traveling salesman problem. Omega 1981;9(4):439–41.   
[3] Lawler EL, Lenstra JK, Rinnooy Kann AHG, Shmoys DB. The traveling salesman problem. Chichester: Wiley; 1985.   
[4] Laporte G. The traveling salesman problem: an overview of exact and approximate algorithms. European Journal of Operational Research 1992;59:231–47.   
[5] Gutin G, Punnen AP, editors. Traveling salesman problem and its variations. Dordrecht: Kluwer Academic Publishers; 2002.   
[6] Gorenstein S. Printing press scheduling for multi-edition periodicals. Management Science 1970;16(6):B373–83.   
[7] Carter AE, Ragsdale CT. Scheduling pre-printed newspaper advertising inserts using genetic algorithms. Omega 2002;30:415–21.   
[8] Svestka JA, Huckfeldt VE. Computational experience with an $m$ -salesman traveling salesman algorithm. Management Science 1973;19(7):790–9.   
[9] Lenstra JK, Rinnooy Kan AHG. Some simple applications of the traveling salesman problem. Operational Research Quarterly 1975;26:717–33.   
[10] Zhang T, Gruver WA, Smith MH. Team scheduling by genetic search. Proceedings of the second international conference on intelligent processing and manufacturing of materials, vol. 2, 1999. p. 839–44.   
[11] Angel RD, Caudle WL, Noonan R, Whinston A. Computer assisted school bus scheduling. Management Science 1972;18:279–88.   
[12] Gilbert KC, Hofstra RB. A new multiperiod multiple traveling salesman problem with heuristic and application to a scheduling problem. Decision Sciences 1992;23:250–9.   
[13] Brummit B, Stentz A. Dynamic mission planning for multiple mobile robots. Proceedings of the IEEE international conference on robotics and automation, April 1996.   
[14] Brummit B, Stentz A. GRAMMPS: a generalized mission planner for multiple mobile robots. Proceedings of the IEEE international conference on robotics and automation, May 1998.   
[15] Yu Z, Jinhai L, Guochang G, Rubo Z, Haiyan Y, An implementation of evolutionary computation for path planning of cooperative mobile robots. Proceedings of the fourth world congress on intelligent control and automation, vol. 3, 2002. p. 1798–802.   
[16] J.L. Ryan, T.G. Bailey, J.T. Moore, W.B. Carlton, Reactive Tabu search in unmanned aerial reconnaissance simulations. Proceedings of the 1998 winter simulation conference, vol. 1, 1998. p . 873–9.   
[17] Tang L, Liu J, Rong A, Yang Z. A multiple traveling salesman problem model for hot rolling scheduling in Shangai Baoshan Iron & Steel Complex. European Journal of Operational Research 2000;124:267–82.   
[18] Saleh HA, Chelouah R. The design of the global navigation satellite system surveying networks using genetic algorithms. Engineering Applications of Artificial Intelligence 2004;17:111–22.   
[19] Okonjo-Adigwe C. An effective method of balancing the workload amongst salesmen. Omega 1988;16(2):159–63.   
[20] Calvo RW, Cordone R. A heuristic approach to the overnight security service problem. Computers and Operations Research 2003;30:1269–87.   
[21] Kim KH, Park Y. A crane scheduling method for port container terminals. European Journal of Operational Research 2004;156:752–68.   
[22] Macharis C, Bontekoning YM. Opportunities for OR in intermodal freight transport research: a review. European Journal of Operational Research 2004;153:400–16.   
[23] Wang X, Regan AC. Local truckload pickup and delivery with hard time window constraints. Transportation Research Part B 2002;36:97–112.   
[24] Basu A, Elnagar A, Al-Hajj A. Efficient coordinated motion. Mathematical and Computer Modelling 2000;31:39–53.   
[25] Mole RH, Johnson DG, Wells K. Combinatorial analysis for route first-cluster second vehicle routing. Omega 1983;11(5):507–12.   
[26] Laporte G, Nobert Y, Desrochers M. Optimal routing under capacity and distance restrictions. Operations Research 1985;33(5):1050–73.   
[27] Toth P, Vigo D. Branch-and-bound algorithms for the capacitated VRP. In: Paolo Toth, Daniele Vigo, editors. The vehicle routing problem. SIAM Monographs on Discrete Mathematics and Applications, Philadelphia, 2002. p. 29–51.   
[28] Hadjiconstantinou E, Roberts D. Routing under uncertainty: an application in the scheduling of field service engineers. In: Paolo Toth, Daniele Vigo, editors. The vehicle routing problem. SIAM Monographs on Discrete Mathematics and Applications, Philadelphia, 2002. p. 331–52.   
[29] Ralphs TK. Parallel branch and cut for capacitated vehicle routing. Parallel Computing 2003;29:607–29.   
[30] Ruland KS, Rodin EY. The pickup and delivery problem. Computers and Mathematics with Applications 1997;33(12): 1–13.   
[31] Mitrovi´c-Mini´c S, Krishnamurti R, Laporte G. Double-horizon based heuristics for the dynamic pickup and delivery problem with time windows. Transportation Research 2004;28(8):   
[32] Dantzig GB, Fulkerson DR, Johnson SM. Solution of a large-scale traveling salesman problem. Operations Research 1954;2:393–410.   
[33] Miller CE, Tucker AW, Zemlin RA. Integer programming formulation of traveling salesman problems. Journal of Association for Computing Machinery 1960;7:326–9.   
[34] Gavish B. A note on the formulation of the msalesman traveling salesman problem. Management Science 1976;22(6):704–5.   
[35] Kulkarni RV, Bhave PR. Integer programming formulations of vehicle routing problems. European Journal of Operational Research 1985;20:58–67.   
[36] Kara I, Bektas T. Integer programming formulations of multiple salesman problems and its variations. (2004), submitted for publication.   
[37] Laporte G, Nobert Y. A cutting planes algorithm for the $m$ -salesmen problem. Journal of the Operational Research Society 1980;31:1017–23.   
[38] Christofides N, Mingozzi A, Toth P. Exact algorithms for the vehicle routing problem, based on spanning tree and shortest path relaxations. Mathematical Programming 1981;20: 255–82.   
[39] Laporte G. The vehicle routing problem: an overview of exact and approximate algorithms. European Journal of Operational Research 1992;59:345–58.   
[40] Ali AI, Kennington JL. The asymmetric $m$ -traveling salesmen problem: a duality based branch-and-bound algorithm. Discrete Applied Mathematics 1986;13:259–76.   
[41] Gavish B, Srikanth K. An optimal solution method for large-scale multiple traveling salesman problems. Operations Research 1986;34(5):698–717.   
[42] Gromicho J, Paixão J, Branco I. Exact solution of multiple traveling salesman problems. In: Mustafa Akgül, et al., editors. Combinatorial optimization. NATO ASI Series, vol. F82. Berlin: Springer; 1992. p. 291–92.   
[43] Gromicho J. Private communication, 2003.   
[44] Russell RA. An effective heuristic for the $m$ -tour traveling salesman problem with some side conditions. Operations Research 1977;25(3):517–24.   
[45] Lin S, Kernighan B. An effective heuristic algorithm for the traveling salesman problem. Operations Research 1973;21: 498–516.   
[46] Potvin J, Lapalme G, Rousseau J. A generalized k-opt exchange procedure for the MTSP. INFOR 1989;27(4): 474–81.   
[47] Fogel DB. A parallel processing approach to a multiple traveling salesman problem using evolutionary programming. In: Proceedings of the fourth annual symposium on parallel processing. Fullerton, CA, 1990. p. 318–26.   
[48] Wacholder E, Han J, Mann RC. A neural network algorithm for the multiple traveling salesmen problem. Biology in Cybernetics 1989;61:11–9.   
[49] Somhom S, Modares A, Enkawa T. Competition-based neural network for the multiple traveling salesmen problem with minmax objective. Computers and Operations Research 1999;26(4):395–407.   
[50] Hsu C, Tsai M, Chen W. A study of feature-mapped approach to the multiple travelling salesmen problem. IEEE International Symposium on Circuits and Systems 1991;3:1589–92.   
[51] Vakhutinsky IA, Golden LB. Solving vehicle routing problems using elastic net. Proceedings of the IEEE international conference on neural network, 1994. p. 4535–40.   
[52] Goldstein M. Self-organizing feature maps for the multiple traveling salesmen problem. In: Proceedings of the IEEE international conference on neural network. San Diego, CA, 1990. p. 258–61.   
[53] Torki A, Somhon S, Enkawa T. A competitive neural network algorithm for solving vehicle routing problem. Computers and Industrial Engineering 1997;33(3–4):473–6.   
[54] Modares A, Somhom S, Enkawa T. A self-organizing neural network approach for multiple traveling salesman and vehicle routing problems. International Transactions in Operational Research 1999;6:591–606.   
[55] C. Song, K. Lee, W.D. Lee, Extended simulated annealing for augmented TSP and multi-salesmen TSP. Proceedings of the international joint conference on neural networks, vol. 3, 2003. p. 2340–43.   
[56] Gomes LDT, Von Zuben FJ. Multiple criteria optimization based on unsupervised learning and fuzzy inference applied to the vehicle routing problem. Journal of Intelligent and Fuzzy Systems 2002;13:143–54.   
[57] Sofge D, Schultz A, De Jong K. Evolutionary computational approaches to solving the multiple traveling salesman problem using a neighborhood attractor schema. Lecture notes in computer science, vol. 2279. Berlin: Springer; 2002. p. 151–60.   
[58] Orloff CS. Routing a fleet of M vehicles to/from a central facility. Networks 1974;4:147–62.   
[59] Bellmore M, Hong S. Transformation of multisalesmen problem to the standard traveling salesman problem. Journal of Association for Computing Machinery 1974;21:500–4.   
[60] Hong S, Padberg MW. A note on the symmetric multiple traveling salesman problem with fixed charges. Operations Research 1977;25(5):871–4.   
[61] Rao MR. A note on the multiple traveling salesman problem. Operations Research 1980;28(3):628–32.   
[62] Gheysens FJ. A more compact transformation of the symmetric multiple traveling salesman problem with fixed charges, Working paper MS/S #82-014, College of Business and Management, University of Maryland, 1982.   
[63] Laporte G, Nobert Y, Taillefer S. Solving a family of multi-depot vehicle routing and location-routing problems. Transportation Science 1988;22(3):161–72.   
[64] GuoXing Y. Transformation of multidepot multisalesmen problem to the standard traveling salesman problem. European Journal of Operational Research 1995;81:557–60.   
[65] Gavish B, Graves SC. The traveling salesman problem and related problems, Working paper GR-078-78, Operations Research Center, Massachusetts Institute of Technology, 1978.   
[66] Jonker R, Volgenant T. An improved transformation of the symmetric multiple traveling salesman problem. Operations Research 1988;36(1):163–7.   
[67] Cordeau JF, Gendreau M, Laporte G, Potvin JY, Semet F. A guide to vehicle routing heuristics. Journal of the Operational Research Society 2002;53:512–22.