# AN ANALYSIS OF THE BEHAVIOR OF A CLASS OF GENETIC ADAPTIVE SYSTEMS

# by Kenneth Alan De Jong

A dissertation submitted in partial fulrillment of the requirements for the degree of Doctor of Philosophy (Computer and Communication Sciences) in the University of Michigan 1975

# Doctoral Committee:

Professor John H. Holland, Chairman Associate Professor Larry K. Flanigan Associate Professor Richard A. Volz Associate Professor Bernard P. Zeigler

# ACKNOWLEDGEMENTS

I would like to thank those persons who made this research not only possible, but also worthwhile and enjoyable. A special note of appreciation to John H. Holland whose enthusiasm for and insight into genetic algorithms provided a constant source of encouragement; to my committee members Larry K. Flanigan, Richard A. Volz, and Bernard P. Zeigler for their time and interest; and especially to my wife, Ruth, who chose to remain in that status even though called upon to be typist, editor, mother, housewife, teacher, and companion during this period.

This research was partially supported by the National Aeronautics and Space Administration under grant NSG 1176. The computer simulations were done on the excellent facilities provided by the University of Michigan Computing Center.

# TABLE OF CONTENTS

ACKNOWLEDGMENTS. 1i   
LIST OF TABLES. . v   
LIST OF ILLUSTRATIONS . . . . vi   
Chapter 1: FORMAL ADAPTIVE SYSTEMS . . 1 1.1: Introduction... 20 1.2: Some Problems for Adaptation. 1.2.1: Data Structure Design 1.2.2: Algorithm Design. . . 1.2.3: Game-playing Programs 1.2.4: Two-armed Bandits . 1.3: A Formal Framework. : . : 1.4: The Problem of Function Optimization. 1.5: A Reduction in Scope. . o 1.6: Summary . . . . .   
Chapter 2: GENETIC ADAPTIVE MODELS . 15 2.1: Introduction. 20 2.2: Genetic Population Models 2.3: Reproductive Plans.. 2.4: The Basic Reproductive Plan: R1 2.5: K-armed Bandits .. • • 2.6: Hyperplane Analysis of R1 2.7: An Example of Rl. 2.8: Summary . .   
Chapter 3: STOCHASTIC EFFECTS IN FINITE GENETIC MODELS. . . . . • . . . . . . 48 Introduction... 48 The Problem of Premature Convergence. 48 Genetic Drift. • 20 The Effects of Population Size on RI. 3:2 The Erfec o Mation ate  R1. The Effects of Generation Gap on RI . Improving the Performance of A1 on F1 Summary . . . . . . . . . . . . . .   
Chapter 4: PERFORMANCE EVALUATION OF GENETIC ADAPTIVE PLANS. . .. 4.1: Introduction.. 96 4.2: The Performance of RI on E. .

$\begin{array} { r l } { \mathrm { 4 . ~ 3 : } } & { { } } \\ { \mathrm { 4 . ~ 4 . } } & { { } } \\ { \mathrm { 4 . ~ 5 . } } & { { } } \\ { \mathrm { 4 . ~ 6 . } } & { { } } \\ { \mathrm { 4 . ~ 6 . } } & { { } } \\ { \mathrm { 4 . ~ 7 : } } & { { } } \\ { \mathrm { 4 . ~ 8 : } } & { { } } \\ { \mathrm { 4 . ~ 9 : } } & { { } } \end{array}$ \$\f07ac{ }\$   
128   
Crowding Factor Model R5 . 1136   
Gemeralized Crossover Model R6 • 160   
Chapter 5: PERFORMANCE ANALYSIS OF FUNCTION   
OPTIMIZERS . . .. . 163   
Performance Evaluation Conventions \$1G0   
Performance Evaluation of PRAXIS and DFP 169   
Summary. . . . . . . . . 185   
Chapter 6: SUMMARY AND CONCLUSIONS. . . 190   
ApPendi A: THE ENVIRONMENT E 196   
A.1: Introduction .. \$196 6   
A.2: Test Function Fi   
A.3: Test Function F2 1   
A.4: Test Function F3 20   
A.5: Test Function F4 203   
A.6: Test Function F5 203   
APpendix B: RANDOM SEARCH ON E 211   
B.1: Introduction . 211   
B.2: Validating RANDoM on E 212   
B.3 RANDOM on F1 • 21   
B RANDOM on F2 . \$20 c\$   
RANDOM on F3 \*   
RANDOM on F4   
B.7: BANDOM on F5 226   
Appendix C: PLAN RI ON E 233   
Introduction:   
: Plan 21 on P \$246   
C.5: Plan R1 on F5. 249   
C.7: Robustness of Plan R1 249   
BIBLIOGRAPHY . . . 253

# LIST OF TABLES

# Table

4.1a: 3.1: Off-line performance of Ri on_E. The data soiated wih a singn 10   
4.1b: On-line performance of R1 on E.   
4.2a: Off-line performance of R4 on E. o   
4.2b: On-line performance of R4 on E. . 121   
4.3a: Off-line performance of R5 on E. 146   
4.3b: On-line performance of R5 on E . 147   
4.4a: Off-line performance of R6 on E. 158   
4.4b: On-line performance of R6 on E . • 159   
5.1a: Off-line performance indices for PRAxIS   
and DFP on E . . . . .. . • • 186   
5.1b: On-line performance indices for PRAxIS   
and DFP on E.. 187

2.1: Expected losses over 50 trials on bandits B1(9.1) and B2(8,1). . . 27   
2.2: Optimal iosses incurred over T trials on two bandits B1(9,1) and B2(8,1). : . 29   
2.3: Optimal distribution of T trials between two bandits B1(9.1) and B2(8,1). . 30   
2.4: DTS erpected losses over 50 trials on 32   
2.5: DTS and the optimal on two bandits B1(9,1)and B2(8,1)...... • • 34   
2.6: Simulated losses over 100 trials using TVS on two bandits B1(9,1) and B2(8,1) : : 36   
2.7: A comparison of expected losses over T trials on two bandits Bi(9.1) and B2(8,1) . • \* 38   
2.8: A comparison of the allocation of T trials to two bandits B1(9.1) and B2(8,1) . : 39   
3.1: The rate of allele loss due to genetic drirt as a function of population size .. • • 56   
3.2: The rate of allele loss due to genetic drift as a function of population size .. • • 57   
3.3: The rate of allele loss due to genetic drift as a function of the mutation rate . • • 59   
3.4: The rate of allele loss due to genetic drift as a function of the mutation rate .. 60   
3.5: The effects of population size on allele loss for R1 on test function Fi. ... . 63   
3.6: The effects of population size on off-line performance of R1 on test function Fi. . 65   
3.7: The effects of population size on onoline performance of R1 on test function Fi. . 66   
3.8: The effects of mutation rate on allele loss for Hi on test function Fl. . . . 69   
3.9: The effects of mutation rate on off-line performance of R1 on test function F1. 70   
3.10: The effects of mutation rate on on-line performance of R1 on test function F1. 71   
3.11: The effects of crossover rate on allele loss for HI on test function F1. : : 74   
3.12: The effects of crossover rate on off-line performance of R1 on test function F1. . 75   
3.13: The effects of crossover rate on on-line performance of R1 on test function Fi. . 76   
3.14: The effects of generation gap on allele loss of Al on test function Fi . . . 80

# Figures

3.15: The effects of generation gap on off-line performance of R1 on test function FI. . 81   
3.16: The effects of generation gap on on-line performance of Ri on test function F1. . 82   
3.17: off-line performance of A1 on F1 as a function of crossover rate and generation gap. . 86   
3.18: On-line performance of R1 on Fi as a function of crossover rate and generation gap. . 87   
3.19: Off-line performance of R1 on F1 as a function of mutation rete. .. .. 89   
3.20: On-line performance of A1 on F1 as a function of mutation rate. .. 90   
3.21: Off-line perforeance of R1 on Fi as a function of population size. . 92   
3.22: On-line performance of R1 on F1 as a function of population size. 93   
4.1: Allele loss for R2 on F1 .. 103   
4.2: Off-line performance curves for H2 on F1 104   
4.3: On-line performance curves for R2 on Fl. 105   
4.4: Allele loss for R3 on Fl . . . ... . .. 110   
4.5: Off-line performance curve for R3 on F1. 111   
4.6: On-line performance curve for R3 on F1 . 112   
4:.8: Alnmr. 115   
4.9: On-line performance curve for R4 on F1 . 117   
4.10: A comparison of off-line performance curves Agemerated Fofr-line performance curves 123   
4.11:   
4.12: A comprrtsdnf f-line performance curves 124   
4.13: Agomprrsd -line performance curves 125 generated on F4...... . .. ... .... 126   
4.14: A comparison of off-line performance curves generated on F5. . 4 127   
4.15: off-line performance curves for genetic orplans oprfomance for 4 on asa 129   
4.16: 134   
4.17: function of mutation rate. . 135   
4.19: 1 139 function of the crowding factor. . . 140   
4.20: On-line performance for R5 on F5 as a function of the crowding factor. . . 141

# Figures

4.21: Off-line performance for R5 on F5 as a 143   
4.22: function of the crowding factor. . : 144   
4.23: Loss probability curves for second order hyperplanes on chromosomes of length 30 as a function of the number of crossover Alleletoss or R6 on Fi as afunction o 152   
4.24: the number of crossover points , • • • 154   
4.25: Off-line performance curves for R6 on Fi as a function of the $^ \ast$ number of crossover points .. . • • • • • 156   
4.26: On-line performance curves for R6 on F1 as a function of the number of crossover points.... • •. 157   
5.1: off-line performance curves for PRAxIS and DFP in local mode on F1. : : ... 170   
5.2: On-line performance curves for PRAxis and o- in oca on Pl. PAXI 171   
5.3: 173   
5.4: in 174   
5.5: 175   
5.6: o-l n    d 176   
5.7: DFP in local mode on F4. .. 178   
5.8: On-line performance curves for PRAXIS and - in   A 179   
5.9: 180   
5.10: oD-P in oa ono 181   
5.11: o-P in global de o  oPAxs and 183   
5.12: DFP in global mode on F5 . ;. 184   
A.1a: Top surface defined by the 2-dimensional version of Fl. .. • 198   
A.1b: Bottom surface derined by the 2-dimensional version of F1. ..... 201   
A.2a: Top surface defined by test runction F2. : .   
A.2b: Bottom surface defined by test function F2 . : 202

# Figures

A.3: Surface defined by the 2-dimensional version of test function F3 . 204   
A.4a: Top surface defined by the 2-dimensional version of test function F4 . . 205   
A.4b: Bottom surface derined by the 2-dimensional version of test function F4 . .. 206   
A.5a: Top surface defined by test runction F5 . 209   
A.5b: Bottom surface defined by test function F5. 210   
B.1a: Off-line performance curves for random search on test function F1. . . • 216   
B.ib: On-line performance curves for random   
B.2a: oarch uin anm 217 search on test function F2. : : 218   
B.2b: On-line performance curves for random   
B.3a: oearch on tert funtion rand 220 search on test function F3. . . : 222   
B.3b: On-line performance curves for random search on test function F3. . . . 223   
B.4a: off-line performance curves.for random search on test function F4. , 225   
B.4b: On-line performance curves for random search on test function F4. . . . 227   
B.5a: off-line performance curves for random search on test function F5. . .. 230   
B.5b: On-line performance curve for random 231   
C.1a: R1 on test function Fl. . . 237   
C.1b: On-line performance curve for plan 238   
C.2a: 240   
C.2b: Rl on test funotion F2. • 241   
C.3a: off-line performance curve for plan R1 on test function F3. . . .. 244   
C.3b: On-line performance curve for plan B1 on test function F3. . . . , 245   
C.4a: off-line performance curve for plan B1 on test function F4. 247   
C.4b: On-line performance curve for plan R1 on test function F4. .. • . 248   
C.5a: off-line performance curve for plan R1 on test function F5. .. .. 250

# LIST OF ILLUSTRATIONS

# Figures

C.5b: On-line performance curve for plan Ri on test function F5. ... . . . . . .. 251

# ABSTRACT

# AN ANALYSIS OF THE BEHAVIOR OF A CLASS OF GENETIC ADAPTIVE SYSTEMS

by

Kenneth Alan De Jong

Chairman: John H. Holland

This thesis is concerned with the design and analysis of adaptive systems, particularly in the area of adaptive computer sortware. To that end a formalism for the study of adaptive systems is introduced and, within this framework, a means of evaluating the performance of adaptive systems is defined. The central feature of the evaluation process is robustness: the ability of an adaptive system to rapidly respond to its environment over a broad range of situations. To provide a concrete measure of robustness, a family E of environmental response surfaces was carefully chosen to include a wide variety of surfaces, including multimodal and discontinuous ones. The performance of an adaptive system is evaluated over E by computer simulation by monitoring two distinct performance curves: on-line and off-line performance. With on-line performance every response of the adaptive system is evaluated, reflecting situations in which an adaptive system is used to dynamically improve the performance of a system, with off-line performance only responses which improve performance are evaluated, reflecting situations in whioh testing can be done independently of the system being controlled.

Within this evaluation framework, a class of genetic adaptive systems is introduced for analysis and evaluation. These artificial genetic systems, called reproductive plans, generate adaptive responses by simulating the information processing achieved in natural systems by means of the mechanisms of heredity and evolution. This is accomplished internally by maintaining a population of individuals whose "genetic" material specifies a particular point on the response surface. New individuals (responses) are produced by simulating population development via mating rules, production of offspring, mixing of genetic material, and so on.

Even the most elementary genetic adaptive plan is shown to produce performance on E which is superior to pure random search of the response surfaces. However, these elementary genetic plans were shown to be easily affected by stochastic side-effects resulting from internal random processes. By suitable adjustments in parameters and modifications to the basic genetic plan, a considerable improvement in the performance was achieved on E.

As a final point of comparison, the performance of two standard function optimization techniques was evaluated on E. Their performance is shown to be superior on the continuous quadratic-like functions for which they were

designed. However, the genetio plans are shown to be superior on the discontinuous and multimodal surfaces, suggesting that genetic plans hold a valid position between specialized local adaptive techniques and pure random search.