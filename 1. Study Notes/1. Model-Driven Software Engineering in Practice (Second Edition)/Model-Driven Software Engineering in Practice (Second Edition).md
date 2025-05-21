Title: Sans titre  
Author:

# CHAPTER 3 MDSE Use Cases

MDSE’s most prominent application is *software development automation*, or model-driven development (MDD). MDD automates as much of the software lifecycle as possible, from requirements to deployment. However, MDSE’s potential applications extend far beyond this scope. MDD is merely a part of the MDSE iceberg (Figure 3.1). In this context, MD(S)E can be interpreted as *Model-Driven Everything*, implying that the MDSE approach can be applied to any software engineering task.

![Figure 3.1: MDD is just the most visible side of MDSE.](/Users/haozhang/GitHub/Study_Notes_and_Programming_Exercises_for_English-Language_Computer_Books_EN/1.%20Study%20Notes/1.%20Model-Driven%20Software%20Engineering%20in%20Practice%20(Second%20Edition)/3.%20CHAPTER%203%20MDSE%20Use%20Cases//Figures/Figure%203.1.png)

3.1 AUTOMATING SOFTWARE DEVELOPMENT

Software development automation starts with a high-level representation of desired software features and gradually transforms it into a functional application. This process may involve user interaction during generation.
Following an MDSE approach, the running application can be obtained through model transformations that progressively refine the software description until an executable version is reached. Figure 3.2 illustrates an MDSE-based development process. In each phase, models are (semi)-automatically generated using model-to-model transformations, utilizing models from the previous phase (and manually completing or refining when necessary). In the final step, the final code is generated through a model-to-text transformation from the design models.







There are other benefits of introducing MDSE into the development
process. One of the main advantages is to bridge the communication gap
between requirements/analysis and implementation. . Overall, the most direct benefits of MDE can be
summarized as the increase of communication effectiveness between the
stakeholders and increase in the productivity of the development team thanks
to the (partial) automation of the development process. As a side effect, this
automation reduces also the number of defects in the final code that could be
inadvertently introduced by the developers.


In order to be able to generate a running system from the models, they
must be executable.
An executable model is a model complete enough to be
executable. From a theoretical point of view, a model is executable when its
operational semantics are fully specified. In practice, the executability of a
model may depend more on the adopted execution engine than on the model
itself. On the one hand, we may find some models which are not entirely
specified but that can be executed by some advanced tools that are able to
“fill the gaps” and execute them; on the other hand, we may have very
complex and complete models that cannot be executed because an
appropriate execution engine is missing. 


The most well-known family of executable models are those based on
the UML language, generically referred as executable UML.
 Executable
UML models make extensive use of an action language (kind of imperative
pseudocode) to precisely define the behavior of all class methods, state
transitions, etc. The OMG itself has recently standardized this notion of
executable UML models. In particular, the OMG has standardized the
semantics of a Foundational Subset for Executable UML Models (fUML)
that suffices to model software specifications in a way that makes them
suitable to be the input of an automated software development process. The
adopted action language for fUML is known as the Action Language for
fUML, or Alf. Alf is basically a textual notation for UML behaviors that can
be attached to a UML model at any place a fUML behavior can be.
Syntactically, Alf looks at first much like a typical C/C++/Java legacy
language, which softens its learning curve.


Code generation and model interpretation are then two different
alternative strategies to “implement” execution tools and thus make
executable models actually execute.




# 111
## 222
### 333

3.1.1 CODE GENERATION

 