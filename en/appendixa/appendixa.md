# Appendix A

# GA User Questionnaire

The following appendix presents a copy of the original email and questionnaire used in the GA user study described in Chapter 3.

# The Visualization of Genetic Algorithms:

Genetic Algorithms typically produce vast quantities of multi-dimensional data on their way toward what is hoped will be a near-optimal solution. Understanding these vast data sets can be a somewhat daunting task. I aim to alleviate this task using Software Visualization techniques. By Software Visualization I mean \the use of the crafts of typography, graphic design, animation and cinematography with modern human-computer interaction technology to facilitate the human understanding and eective use of computer software."

However, in order to fully realise the potential that Software Visualization oers to GAs it is essential to have a thorough understanding of the tasks and diculties associated with GAs. In order to gain this insight I need the help of those working with GAs. Therefore, I want to know as much about your experiences with GAs as possible. Please either email me with your anecdotes, or, ll in the attached questionnaire and email it back to me.

The types of things that I am particularly interested in hearing about are;

 - Which problems you have applied GAs to and how successful you found them,  - What you nd dicult about constructing a GA, e.g. designing the evaluation function,

selecting which genetic operators to use, etc.

 - Any problems you may have encountered whilst trying to evaluate a GAs solution(s)?

 - How you would foresee the application of Software Visualization (as dened above) to GAs, e.g. tness graphs, population analysis, etc.

I have little or no preference as to which form of response I get, please respond by whichever method you feel most comfortable with. Feel free to browse through the attached questionnaire as this may help spark o ideas for any anecdotes you may have. This questionnaire is also available on the World Wide Web as a form document suitable for completion with formssupporting browsers, such as Netscape and Mosaic. The web page for this questionnaire is http://kmi.open.ac.uk/ trevor/Quest1.html .

I am relying on the comments and advice that I receive from you, so that I may ensure that this pro ject shall produce something of practical signicance. Once a robust version of the GA visualization tool is created it will be made freely available to those of you who have helped in its creation. So please help me to help you.

yours thankfully,

Trevor Collins.

# The Visualization of Genetic Algorithms:

The use of lmcraft and animation to illustrate the execution of Genetic Algorithms (\GAs") in which the User takes on a Director's role.

Trevor Collins,

Research Student.

The Knowledge Systems Group,

The Knowledge Media Institute,

The Open University.

Walton Hall,

Milton Keynes MK7 6AA, UK.

phone: 01908-654506   
email: t.d.collins@open.ac.uk   
www: http://kmi.open.ac.uk/trevor/trevor.html

# Introduction

In attempting to design a visualization system specically for supporting the design and application of genetic algorithms, it would be foolish to ignore the ideas and opinions of those involved in that very task. It is for this reason that the following questionnaire has been designed and it is hoped that with your help this will provide some insight into the complex task of GA application. This is not a performance assessment document, there are no prizes to be won, and there is no hidden agenda, so please be as truthful and informative as you can. Some details on the purpose of the questions asked in the questionnaire are available by clicking here. Although I do request you to ll in your name and email address this is only so that I may contact you if the need arises. Any information received will be considered private and condential, your name shall not be referenced in any associated publications.

If the questions raised within this questionnaire do not apply to your particular use of GAs please do let me know as I do not want to alienate any section of the GA community from using the resulting system. Please feel free to raise any additional issues that you think may be worth exploring. The GA visualization system will be made available to those who have helped in its creation, it is hoped that this will provide some incentive to those who may benet from its use. Just in case there is any need to contact you in the future, please type in your name:

and email address:

# Background Information

1. How long have you been using GAs?

2. During this time what have you used GAs for?

3. Why did you use GAs for these tasks?

4. What environment(s) do you use when working with GAs? Please specify each computing environment separately i.e. the computer system, programming language and/or application tool.

# Your Approach to GAs

5. What do you nd dicult, if anything, about the following set-up steps involved in creating a GA:

(a) Dening the mapping between the problem domain and the string representation used by the GA?

(b) Producing an eective evaluation function?

(c) Choosing the GA's components, e.g. the initial population creation method, what reproduction gene-pool selection criterion to adopt, which genetic operators to apply, etc.?

(d) Selecting suitable parameters for the GA, e.g. the population size, the mutation rate (if appropriate), etc.?

(e) Are there any other set-up steps that you use before running the GA? If so please note them and any associated diculties you encounter below.

6. Having applied a GA to a particular problem what approach do you take, in order to:

(a) Assess the quality of any solution(s) found?

(b) Examine how representative the output of the GA is in terms of all the possible points within the problem-space?

# What Characteristics to Visualize

The output of a GA typically takes the form of a set of representative strings (\chromosomes") and their corresponding evaluation ratings (\tness"). The tness values are often then illustrated using a tness verses generation graph. This may show; the highest tness rating, the average tness rating, and/or the lowest tness rating plotted over sequential generations. This is of course a very useful aid for identifying the relative tness ratings of the population across dierent generations, and illustrates one example of the communicative power of graphical representation.

7. If the following typical output characteristics were to be represented what advantages or disadvantages, if any, could you foresee?

(a) All of the individual chromosomes within each population. Advantages:

Disadvantages:

(b) A User dened selection of representative chromosomes. Advantages:

Disadvantages:

(c) The rate of change in the populations tness values, i.e. the gradient values of a tness versus generation graph.

Advantages:

Disadvantages:

8. As well as directly illustrating the output of the GA, visualization could be used to represent additional information either derived from the output dataset or recorded separately. If visualization were used to represent the following characteristics what advantages or disadvantages, if any, could you foresee?

(a) The chromosomes in the reproduction gene-pool. Advantages:

Disadvantages:

(b) The occurrence of mutation in chromosomes where a mutation operator has been applied. Advantages:

Disadvantages:

(c) The internal actions of the genetic operators being applied to the chromosomes, e.g. the splitting and crossover between two chromosomes by a single point crossover operator.

Advantages:

Disadvantages:

(d) A \similarity" rating for each chromosome based on how little they diered to the ttest chromosome, e.g. a ten bit binary chromosome that diered from the ttest chromosome in three of its bit positions (\loci") may have a similarity rating of 0.7.

Advantages:

Disadvantages:

9. Please speciy any other direct or indirect characteristics that you would be interested in seeing visualized.

# Interaction Opportunities

The most common form of GA interaction is that of set-up and run, i.e. the algorithm and its parameters are dened in a set-up phase, and then executed in a run phase. The resulting output is typically examined after execution with any interesting solutions being further scrutinised at the User's discretion.

Software Visualisation however oers two-way interaction throughout a Genetic Algorithm's execution. This could be applied simply to permit some control over the speed of execution so as to further examine the visual representations for each generation, or in a more direct manner to manipulate the algorithm's parameters or the current generation's internal values.

10. How helpful, or destructive, would you nd each of the following interaction opportunities for your use of GAs?

(a) Execution control through the use of a control panel to run, pause, step forward, step backward, save a snapshot, and/or stop execution.

(b) Editing the algorithm's parameters during execution.

(c) Editing the population's chromosomes between two generations.

(d) Editing the reproduction gene-pool's chromosomes within a generation.

11. Please specify any other forms of additional interaction that you would consider benecial.

# Any Other Comments

12. Do you have any other suggestions on how GAs could be made easier to use? Or any other comments at all about GAs? Please note them below.

# Future Contact

13. Finally, would you have any ob jection to being contacted in the future with reference to this pro ject and the evaluation of the resulting GA visualization system?

Yes. I would ob ject to being contacted in the future.

No. I would not ob ject to being contacted in the future.

Thank you very much for taking the time to complete this questionnaire. I hope you found it interesting. Providing I received your consent to contact you again, I shall email you once a robust system is available and inform you of the associated anonymous ftp site. If you are happy with your responses please email them back to me - t.d.collins@open.ac.uk

Milton Keynes MK7 6AA, UK.

Oce Phone: +44 908 654506

Departmental Fax: +44 908 653169

Email: t.d.collins@open.ac.uk

WWW: http://kmi.open.ac.uk/ trevor/trevor.html