Title: Sans titre  
Author:

# CHAPTER 3 MDSE Use Cases

MDSE’s most prominent application is *software development automation*, or model-driven development (MDD). MDD automates as much of the software lifecycle as possible, from requirements to deployment. However, MDSE’s potential applications extend far beyond this scope. MDD is merely a part of the MDSE iceberg (Figure 3.1). In this context, MD(S)E can be interpreted as *Model-Driven Everything*, implying that the MDSE approach can be applied to any software engineering task.

![Figure 3.1: MDD is just the most visible side of MDSE.](./03.%20CHAPTER%203%20MDSE%20Use%20Cases/Figures/Figure%203.1.png)

## 3.1 AUTOMATING SOFTWARE DEVELOPMENT

Software development automation starts with a high-level representation of desired software features and gradually transforms it into a functional application. This process may involve user interaction during generation.

Following an MDSE approach, the running application can be obtained through model transformations that progressively refine the software description until an executable version is reached. Figure 3.2 illustrates an MDSE-based development process. In each phase, models are (semi)-automatically generated using model-to-model transformations, utilizing models from the previous phase (and manually completing or refining when necessary). In the final step, the final code is generated through a model-to-text transformation from the design models.

![Figure 3.2: A typical MDSE-based software development process.](./03.%20CHAPTER%203%20MDSE%20Use%20Cases/Figures/Figure%203.2.png)

Introducing MDSE into the development process offers several advantages. It bridges the communication gap between requirements/analysis and implementation by capturing and organizing the system’s understanding. This facilitates discussions among team members and integrates new ones. MDE increases communication effectiveness between stakeholders and the productivity of the development team due to (partial) automation. It also reduces the number of defects in the final code inadvertently introduced by developers.

To generate a running system from models, they must be executable. An executable model is complete enough to be executed. Theoretically, a model is executable when its operational semantics are fully specified. In practice, the excitability of a model may depend more on the execution engine than on the model itself. Some models may not be entirely specified but can be executed by advanced tools that fill in the gaps. Conversely, complex and complete models may not be executable due to the absence of an appropriate execution engine.

*Executable UML*, a well-known family of executable models, uses an action language (imperative pseudocode) to precisely define the behavior of class methods, state transitions, etc. The OMG has standardized executable UML models, including a Foundational Subset for Executable UML Models (fUML) that models software specifications suitable for automated software development. The adopted *Action Language for fUML*, Alf, is a textual notation for UML behaviors attached to UML models at fUML behavior locations. Syntactically, Alf resembles typical C/C++/Java legacy languages, easing learning.

Code generation and model interpretation are two alternative strategies to “implement” execution tools and make executable models execute.

3.1.1 CODE GENERATION

## 5.4 DOMAIN-DRIVEN DESIGN AND MDSE

Domain-driven design (DDD) is a software development approach based on two main principles:

1. Focus on the domain and not technical details.

2. Use a model for complex domain designs.

DDD emphasizes an appropriate and effective representation of the system-to-be’s problem domain. It provides design practices and techniques for software developers and domain experts to share and represent their domain knowledge using models.

DDD shares aspects with MDSE, arguing for using models to represent domain knowledge and focusing on platform-independent aspects during development. MDSE provides techniques for modeling, creating DSLs, and more to implement DDD.

MDSE complements DDD (Figure 5.1) by enhancing developer benefits from domain models. Model transformation and code generation techniques allow domain models to represent the domain (structure, rules, dynamics) and generate the actual software system to manage it.

![Figure 5.1: Relationship between DDD and MDD.](./05.%20CHAPTER%205%20Integration%20of%20MDSE%20in%20your%20Development%20Process/Figures/Figure%205.1.png)

---

> **Résumé** :
> 
> * **DDD Principles**: Focus on the domain and uses models for complex designs.
> 
> * **DDD’s Focus**: Emphasizes representing the problem domain effectively using models.
> 
> * **Relationship with MDSE**: Shares the use of models for domain knowledge representation and platform-independent development.
> 
> * **MDSE’s Role in DDD**: Enhances DDD by providing techniques like model transformation and code generation to implement the domain model.

---

## 5.5 TEST-DRIVEN DEVELOPMENT AND MDSE

Test-driven development (TDD) follows the test-first philosophy, where developers write executable test cases to check new functionality. If a test fails, the developer writes the code to pass it, effectively forcing implementation. Once the code passes the full test suite, it’s refactored, and the process repeats.

MDSE can be integrated into TDD at two levels: when models are used for code generation to automatically derive system implementation, and when they aren’t.

---

> **Résumé** :
> 
> * **TDD Definition**: Developers write executable test cases to check new functionality before writing the code.
> 
> * **TDD Process**: Write a test, write code to pass the test, refactor the code, and repeat.
> 
> * **MDSE Integration**: MDSE can be integrated into TDD when models are used for code generation or not.

---

### 5.5.1 MODEL-DRIVEN TESTING

Models can be used to derive tests for system implementations to ensure they behave as expected. This is known as model-based testing. As shown in Figure 5.2, a test generation strategy is applied at the model level to derive a set of tests, which are then translated into executable tests for the system’s technological platform. Testing strategies depend on the model and test type. For instance, constraint solvers generate test cases for static models, while model checkers generate relevant execution traces for dynamic models.

![Figure 5.2: Model-based testing.](./05.%20CHAPTER%205%20Integration%20of%20MDSE%20in%20your%20Development%20Process/Figures/Figure%205.2.png)

---

> **Résumé** :
> 
> * **Model-Based Testing**: Models are used to derive tests for system implementations to ensure expected behavior.
> 
> * **Test Generation**: A test generation strategy is applied at the model level to derive a set of tests, which are then translated into executable tests.
> 
> * **Testing Strategies**: Depend on the model and test type, such as constraint solvers for static models and model checkers for dynamic models.

---

### 5.5.2 TEST-DRIVEN MODELING

When software is derived from models, testing the code is unnecessary (assuming complete code generation and trust in the code generator). Instead, test the models. Some test-driven development approaches for modeling artifacts follow this philosophy: before developing a model excerpt, write the model test to evaluate new functionality at the modeling level. Model the new functionality and execute the test to ensure model correctness. This practice requires executable models (see Chapter 3). Chapter 10 discusses tools for exhaustive and systematic model testing and validation.

---

> **Résumé** :
> 
> * **Testing Focus**: Test the models instead of the generated code.
> 
> * **Model Testing Approach**: Write model tests before developing model excerpts to ensure correctness.
> 
> * **Model Requirement**: Executable models are necessary for this approach.

---