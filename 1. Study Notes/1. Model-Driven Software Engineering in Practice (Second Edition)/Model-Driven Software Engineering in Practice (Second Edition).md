Title: Sans titre  
Author:

# CHAPTER 3 MDSE Use Cases #

MDSE’s most prominent application is *software development automation*, or model-driven development (MDD). MDD automates as much of the software lifecycle as possible, from requirements to deployment. However, MDSE’s potential applications extend far beyond this scope. MDD is merely a part of the MDSE iceberg (Figure 3.1). In this context, MD(S)E can be interpreted as *Model-Driven Everything*, implying that the MDSE approach can be applied to any software engineering task.

![Figure 3.1: MDD is just the most visible side of MDSE.](./3.%20CHAPTER%203%20MDSE%20Use%20Cases//Figures/Figure%203.1.png)  
3.1 AUTOMATING SOFTWARE DEVELOPMENT

Software development automation starts with a high-level representation of desired software features and gradually transforms it into a functional application. This process may involve user interaction during generation.
Following an MDSE approach, the running application can be obtained through model transformations that progressively refine the software description until an executable version is reached. Figure 3.2 illustrates an MDSE-based development process. In each phase, models are (semi)-automatically generated using model-to-model transformations, utilizing models from the previous phase (and manually completing or refining when necessary). In the final step, the final code is generated through a model-to-text transformation from the design models.
Introducing MDSE into the development process offers several advantages. It bridges the communication gap between requirements/analysis and implementation by capturing and organizing the system’s understanding. This facilitates discussions among team members and integrates new ones. MDE increases communication effectiveness between stakeholders and productivity of the development team due to (partial) automation. It also reduces the number of defects in the final code by inadvertently introduced by developers.
To generate a running system from models, they must be executable. An executable model is complete enough to be executed. Theoretically, a model is executable when its operational semantics are fully specified. In practice, the executability of a model may depend more on the execution engine than on the model itself. Some models may not be entirely specified but can be executed by advanced tools that fill in the gaps. Conversely, complex and complete models may not be executable due to the absence of an appropriate execution engine. 











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




 

3.1.1 CODE GENERATION