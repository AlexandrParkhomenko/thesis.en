# EVOLUTIONARY OPTIMIZATION IN DYNAMIC ENVIRONMENTS

JURGEN BRANKE

# Contents

Preface xi

1. BRIEF INTRODUCTION TO EVOLUTIONARY ALGORITHMS 1

1. From Biology to Software 1

2. Basic Evolutionary Algorithm 4

3. Further Aspects 7

3.1 Representation 7   
3.2 Parallelization 8   
3.3 Runtime Comparisons 10

Part I Enabling Continuous Adaptation

# 2. OPTIMIZATION IN DYNAMIC ENVIRONMENTS 13

1. Categorization of Dynamic Environments 14   
2. Suitable Benchmark Problems 17   
2.1 Dynamic Bit-Matching 17   
2.2 Moving Parabola 18   
2.3 Time-Varying Knapsack Problem 19   
2.4 Moving Peaks Function 20   
2.5 Scheduling Problems 24   
2.6 Oscillating Peaks 25

3. Measuring Performance 26

4. Detecting Changes in the Environment 28

3. SURVEY: STATE OF THE ART 31

1. Restart / Re-Initialization 31

2. Adapting Mutation 34

3. Implicit or Explicit Memory 38   
4. Modifying Selection 42

5. Multi-Population Approaches 44

5.1 Self-Organizing Scouts 44   
5.2 Shifting Balance GA 45   
5.3 Multinational GA 45   
6. Other Approaches 46   
6.1 Immune Systems 46   
6.2 Parallel EA Variants 46   
6.3 Evolving Control Rules 46   
6.4 Modeling the System 47   
6.5 Stochastic Genetic Algorithm 47   
6.6 Clan-based Evolution 48   
6.7 Dual and Folding Genetic Algorithm 48

# 7. Further Aspects 49

7.1 Steady-State or Generational Replacement? 49   
7.2 Darwinian vs. Lamarckian Learning 50   
7.3 Parameter Settings 51   
7.4 Other Related Work 51

# 4. FROM MEMORY TO SELF-ORGANIZATION

1. Memory/Search 54   
1.1 General Thoughts about Memory 54   
1.2 The Best of Two Worlds 56   
2. Self-Organizing Scouts 58

# 5. EMPIRICAL EVALUATION 67

1. General Remarks on the Experimental Setup 67

2. Default Parameter Settings 69

3. Oscillating Peaks Function 71

3.1 Standard Test Case 72   
3.2 The Influence of Change Frequency 76   
3.3 Non-vanishing Peaks 78

4. Moving Peaks Function 81

4.1 Sensitivity of Parameter Settings 81   
4.2 The Effect of Peaks Movements 86   
4.3 Changing the Number of Peaks 90   
4.4 The Influence of Change Frequency 94   
4.5 Higher Dimensionality 96

Contents ix

4.6 Correlation of Shifts 97

6. SUMMARY OF PART 1 99

Part II Considering Adaptation Cost

# 7. ADAPTATION COST VS. SOLUTION QUALITY 105

1. Introduction to Multi-Objective EAs 106   
2. Related Work 109   
3. Guided Multi Objective Evolutionary Algorithm 111   
4. Experimental Results 114   
5. Summary of Chapter 7 121

Part III Robustness and Flexibility — Precaution against Changes

# 8. SEARCHING FOR ROBUST SOLUTIONS 125

1. Motivation 125   
2. Related Work 128   
3. Test Problems 132   
4. Experimental Setup and Default Parameters 136   
5. How to select the final solution? 138   
6. Influence of Several EA Parameters 141   
6.1 The Number of Samples Throughout the Run 141   
6.2 Allowed Running Time 142   
6.3 Selection Pressure 143   
6.4 Steady State vs. Generational Reproduction 144   
6.5 Population Size 147   
6.6 The Island Model 153   
6.7 Selection Method 154   
7. Evaluating Good Individuals More Often 156   
8. Minimizing the Estimation Error 158   
9. Better Sampling Methods 160   
10. Changing the Sample Size 163   
11. Looking at Other Individuals in the Neighborhood 167   
12. Summary of Chapter 8 169

9. FROM ROBUSTNESS TO FLEXIBILITY 173

1. Related Work 174

2. Dynamic Job Shop Scheduling 175   
2.1 Decomposing Dynamic JSSPs 175   
2.2 The Role of Schedule Builders 176   
3. A Flexibility Measure for Dynamic Stochastic JSSPs 178   
4. Empirical Evaluation 180   
5. Summary of Chapter 9 183

10. SUMMARY AND OUTLOOK 185

References 191

# Index

# 207

# Preface

Many complex real-world optimization problems are dynamic, and stochastically change over time: new jobs are arriving continuously and have to be added to the schedule, machines may break down or wear out slowly, raw material is of changing quality, production tolerances have to be taken into account, etc.

These problems require powerful heuristics that account for the uncertainty present in the real world. Evolutionary algorithms (EAs) have proven successful in a vast number of static applications and the number of papers produced in this area is still growing fast. But they also seem to be particularly suitable for dynamic and stochastic optimization problems, not only because they draw their inspiration from the principles of natural evolution, which is a stochastic and dynamic process as well.

This book is concerned with the special intricacies due to the uncertainties in dynamic optimization problems, and provides the state of the art and latest research on how evolutionary algorithms may be applied to this kind of problems.

A standard approach to deal with uncertainty and dynamism in optimization problems is to regard each change as the arrival of a new problem instance that has to be solved from scratch (cf. e.g. [RT93]). However, this simple idea is often impractical for a number of reasons:

solving a problem from scratch without reusing information from the past is too time consuming,   
a change might be difficult to discover, or at least remain undetected for some time,   
the solution of the new problem should not differ too much from the solution of the old problem, or   
it is not possible or economically sensible to adapt the solution after every small change.

In this book, three special aspects of dynamic optimization problems that can be derived from the above difficulties are identified and treated in the context of evolutionary algorithms.

Firstly, the algorithm should be capable of continuously and efficiently adapting the solution to a changing environment.

Secondly, since in practice a change of a solution often involves additional efforts, it should be possible to integrate the change cost into the optimization criteria and to determine a good trade-off between solution quality and change costs.

And thirdly, many changes are actually very small or occur so often that an adaptation of the solution is impracticable. For example, it is probably impossible to adapt a schedule to small variations in processing times. In that case, one should aim at creating robust solutions that maintain a high solution quality even when the environment changes slightly.

In short, large and infrequent changes in the environment should be handled by adaptation, and with consideration of change costs, while frequent small changes should be accounted for by creating robust solutions.

All these aspects are addressed in this book, providing a holistic view on the challenges and opportunities of applying evolutionary algorithms to dynamic optimization problems, and suitable novel approaches are developed for each aspect.

Part I concentrates on enabling the EA to quickly locate other high performance solutions after the environment has changed and rendered the current solution improper. Loosely speaking, during its search for one optimum, the EA gathers information about the search space which, when retained, may be useful when searching for the next optimum after a change has occurred. Thus, by allowing the EA to transfer knowledge from one step to the next, it should be possible to improve the performance compared to the standard EA. In Chapter 2, some fundamental issues are addressed: A classification of dynamic optimization problems is suggested, and several performance measures are discussed. Also in that chapter, a number of suitable benchmark problems are described, and a new benchmark is developed aimed at closing the gap between too simple toy problems and too complicated real-world problems. Chapter 3 contains a comprehensive survey of literature in the area. Then, in Chapter 4, two new approaches are developed. The Memory/Search approach combines sensibly the ideas of memorization and diversification, while the Self-Organizing Scouts approach uses a novel multi-population concept to continuously track several promising high-performance regions of the search space. The approaches are evaluated under several scenarios in Chapter 5.

Part II focuses on the integration of change cost into the adaptation process: not only the solution quality, but also the required effort to change the current into the new solution is to be considered. The approach suggested here is to regard the problem as a multi-objective optimization problem. Since EAs are population-based search methods, they allow the concurrent search for many Pareto-optimal solutions, which may then be returned to the decision maker to select the solution to be implemented. While the use of EAs to search for a Pareto-optimal front in multi-objective optimization problems has already been extensively studied by numerous researchers ([VL00]), Chapter 7 will present a new way to focus the search on some "interesting" part of the Pareto-optimal front, thereby allowing a more efficient search and a more thorough coverage of this specific area.

Part III addresses the issue of finding solutions that are not only optimal with respect to the current situation, but also with respect to expected changes or uncertainties in the environment. In Chapter 8, the aim is to find robust solutions, i.e. solutions that perform well over a wide range of environmental conditions, thus reducing the need to adapt the solution. On the other hand, in Chapter 9, it is expected that adaptations are necessary, and subsequently solutions are sought that are flexible, i.e. that allow easy and successful adaptation after the environment has changed. For the case of job shop scheduling, a flexibility measure is suggested that, when taken into account during optimization, may yield significantly better results in a dynamic environment with new jobs arriving over the time.

The book concludes in Chapter 10 with a summary and an outlook on future work.

# Acknowledgements

This monograph was written while I was working at the Institute for Applied Computer Science and Formal Description Methods (AIFB) at the University of Karlsruhe. In December 2000, the Department of Economics and Business Engineering at the University of Karlsruhe accepted the monograph as partial fulfillment of a doctoral degree. It could not have been accomplished without the help and support of numerous people which shall hereby be gratefully acknowledged.

First of all, I would like to thank my advisor, Professor Dr. Hartmut Schmeck, for his support and advice during the various stages of my work, and for giving me the time and freedom to follow my own research interests. I also owe thanks to Professor Dr. Georg Bol and Professor Dr. Lothar Thiele for co-refereeing the work and for helpful comments.

I am grateful to all members of the institute who, each in his or her own way, helped to create an enjoyable and inspiring work atmosphere. In particular, I am grateful to Dr. Udo Kohlmorgen, Dr. Martin Middendorf, and Daniel Merkle for all the fun and interesting discussions we had together.

Special thanks go to Dr. Dirk Mattfeld with whom I had the privilege to collaborate on the issue of solution flexibility. Also, I was glad to have some excellent students to work with, in particular Thomas KauBler and Christian Schmidt.

Naturally, an undertaking as a dissertation comes at the expense of long work hours and some unavoidable tensions. I am indebted to all my friends and family for their understanding and patience. I owe gratitude to my parents for their unconditional support and encouragement since I can remember, and especially to my wife Julia, for her understanding, her affection, and her help during the final stages of the work.

Finally, I would like to thank my little daughter Janina who, by her expected birth, set the necessary pressure to eventually finish up the project.