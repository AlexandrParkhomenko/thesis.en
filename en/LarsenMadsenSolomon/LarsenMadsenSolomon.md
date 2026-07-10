# The A-Priori Dynamic Traveling Salesman

# Problem with Time Windows

Allan Larsen

Informatics and Mathematical Modelling, The Technical University of Denmark

Oli B.G. Madsen

Marius M. Solomon

CTT, The Centre for Traffic and Transport, Northeastern University The Technical University of Denmark Boston, Massachusetts

Corresponding Author: Allan Larsen

Informatics and Mathematical Modelling, building 321 The Technical University of Denmark, DK-2800 Kgs. Lyngby, Denmark fax.: +45 4593 2373, e.mail: ala@imm.dtu.dk

# 1 Extended abstract

The remarkable advances in telecommunications and information technology have enabled companies to focus on velocity and timeliness throughout the supply chain. To achieve these competitive advantages, they must be able to make effective use of the vast amount of real-time information now available to them. The Dynamic Vehicle Routing Problem (DVRP) is a prime example of a distribution context where intelligent use of real-time information can differentiate one company from another by means of superior on-time service.

The DVRP is the dynamic counterpart of the traditional vehicle routing problem where several vehicles must visit and service a number of customers. Constraints such as capacity restrictions, time windows within which to start service at customers and additional requirements on the drivers and vehicles must be accounted for when seeking to minimize the travel cost. In contrast to the generic, or static, vehicle routing problem where the dispatcher can plan ahead, in the dynamic version, part or all of the necessary information becomes available only during the day of operation.

The practical significance of the DVRP is highlighted by the variety of environments it can model. An important application is the pick-up and delivery of overnight mail. Other scenarios include the distribution of heating oil or liquid gas to private households, residential utility repair services, such as cable and telephone, and appliance repair. Additional settings are the transportation of the elderly and physically disabled, taxi cab services, and emergency services, such as police, fire and ambulance dispatching.

A vast body of research directed at the vehicle routing problem has emerged over the last two decades. Notably, the DVRP has received increased attention over the last few years. Elaborate surveys have been written by Psaraftis [5] and [6] and by Powell et al. [4]. Recently, Gendreau and Potvin [2] overviewed new developments. Psaraftis [5] introduced a dynamic version of the Traveling Salesman Problem that motivated Bertsimas and Van Ryzin [1] to examine the Dynamic Traveling Repairman Problem. Later, Larsen, Madsen, and Solomon [3] recasted this problem in a partially dynamic context and examined the effect of the degree of dynamism on solution methodology and quality.

In this paper we examine the Traveling Salesman Problem with Time Windows (TSPTW) for various degrees of dynamism, i.e. as with the DVRP, part or all of the necessary information becomes available during the day of operation. We seek to minimize lateness and examine the impact of this criterion choice on the distance traveled. Our focus on lateness is motivated by the problem faced by overnight mail service providers. At both ends of their supply chain, their objective is to pick-up and deliver all letters and packages within the given time restrictions while keeping the operating costs as low as possible. The cost of lateness is very high since it results in full customer reimbursement or lost sales.

We first propose a real-time solution method that requires the vehicle, when idle, to wait at the current customer location until it can service another customer without being early. In addition, we extend the current literature by developing three enhanced versions of this method that make use of a-priori information on future requests to non-myopically reposition the vehicle at idle points different from the current location. The set of idle points are defined as locations with a high probability of generating new requests for service. Each of the policies choose the idle points to which the vehicle may go to when it becomes idle according to one of the following criterias; the nearest idle point, the busiest idle point (i.e. the one with the highest arrival intensity) or the idle point with the highest expected number of new requests where the travel time for the vehicle to reach the idle point is taken into account.

We tested the developed routing policies on both randomly generated data and a real-world case study. The results indicate that all policies proved capable of significantly reducing lateness. Our results also show that this can be accomplished with only small distance increases. The basic policy outperformed the other methods primarily when lateness and distance were equally minimized and proved very robust in all environments studied. When only lateness was considered, the policy to reposition the vehicle at a location near the current customer generally provided the largest reductions in average lateness and the number of late customers. It also traveled the least

extra distance among the repositioning policies.

The proposed policies are based on the relatively simple 3-opt heuristic. All calculations were performed within a few seconds, hence computation time is negligible. Therefore, the policies are excellent candidates for on-line implementation. Furthermore, their efficiency should prove beneficial in environments where the arrival intensities of the immediate requests are relatively high. In such cases, other methods, such as meta-heuristics will most likely not be able to improve on the initial solution they obtain before a new immediate request is received, since they require relatively extensive computation times in order to provide good quality solutions.

Further research should consider allowing diversion during repositioning or traveling from one customer to the next. Also, more sophisticated methods, such as location analysis, should be considered for choosing the idle points. Finally, the repositioning policies could be refined.

# Список литературы

[1] Dimitris Bertsimas and Garrett Van Ryzin. “A Stochastic and Dynamic Vehicle Routing Problem in the Euclidean Plane”. Operations Research, 39:601–615, 1991.   
[2] Michel Gendreau and Jean-Yves Potvin. Fleet Management and Logistics, chapter Dynamic Vehicle Routing and Dispatching, pages 115–126. Kluwer Academic Publishers, 1998.   
[3] Allan Larsen, Oli B.G. Madsen, and Marius M. Solomon. “Partially Dynamic Vehicle Routing - Models and Algorithms”. Journal of the Operational Research Society 53: 637 – 646, 2002.   
[4] Warren B. Powell, Patrick Jaillet, and Amadeo Odoni. Network Routing, volume 8, chapter Stochastic and Dynamic Networks and Routing, pages 141–295. Elsevier Science, Amsterdam, 1995.   
[5] Harilaos N. Psaraftis. Vehicle Routing: Methods and Studies, chapter Dynamic Vehicle Routing Problems, pages 223–248. Elsevier Science Publishers B.V. (North Holland), 1988.   
[6] Harilaos N. Psaraftis. “Dynamic vehicle routing: Status and prospects.” Ann. of Oper. Res., 61:143–164, 1995.