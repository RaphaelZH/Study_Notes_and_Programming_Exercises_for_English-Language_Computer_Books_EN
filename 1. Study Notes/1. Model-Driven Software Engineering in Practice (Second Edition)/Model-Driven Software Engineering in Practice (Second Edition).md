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
> * Domain-driven design (DDD) focuses on the domain and uses models for complex designs.
> 
> * DDD emphasizes domain representation for developers and experts.
> 
> * DDD and MDSE share similarities in domain modeling and platform-independent development.
> 
> * MDSE enhances DDD by using model transformation and code generation to represent and manage domain models.

---

## 5.5 TEST-DRIVEN DEVELOPMENT AND MDSE

Test-driven development (TDD) follows the test-first philosophy, where developers write executable test cases to check new functionality. If a test fails, the developer writes the code to pass it, effectively forcing implementation. Once the code passes the full test suite, it’s refactored, and the process repeats.

MDSE can be integrated into TDD at two levels: when models are used for code generation to automatically derive system implementation, and when they aren’t.

---

> **Résumé** :
> 
> * Test-driven development (TDD) involves writing executable test cases before code, ensuring functionality is implemented and refactored iteratively.
> 
> * MDSE integrates with TDD at two levels: code generation and non-generation.

---

### 5.5.1 MODEL-DRIVEN TESTING

Models can be used to derive tests for system implementations to ensure they behave as expected. This is known as model-based testing. As shown in Figure 5.2, a test generation strategy is applied at the model level to derive a set of tests, which are then translated into executable tests for the system’s technological platform. Testing strategies depend on the model and test type. For instance, constraint solvers generate test cases for static models, while model checkers generate relevant execution traces for dynamic models.

![Figure 5.2: Model-based testing.](./05.%20CHAPTER%205%20Integration%20of%20MDSE%20in%20your%20Development%20Process/Figures/Figure%205.2.png)

---

> **Résumé** :
> 
> * Model-based testing uses models to derive tests for system implementations, ensuring expected behavior. Test generation strategies, tailored to model and test type, generate test cases or execution traces.

---

### 5.5.2 TEST-DRIVEN MODELING

When software is derived from models, testing the code is unnecessary (assuming complete code generation and trust in the code generator). Instead, test the models. Some test-driven development approaches for modeling artifacts follow this philosophy: before developing a model excerpt, write the model test to evaluate new functionality at the modeling level. Model the new functionality and execute the test to ensure model correctness. This practice requires executable models (see Chapter 3). Chapter 10 discusses tools for exhaustive and systematic model testing and validation.

---

> **Résumé** :
> 
> * Testing software derived from models is unnecessary; instead, test the models. Test-driven development approaches for modeling artifacts involve writing model tests before developing model excerpts to evaluate new functionality.

---

# CHAPTER 6 Modeling Languages at a Glance

Modeling languages are conceptual tools that let designers formalize their thoughts and visualize reality explicitly, whether textually or graphically. This chapter describes the main features of modeling languages, considering general-purpose languages (GPLs), domain-specific languages (DSLs), and intermediate solutions that customize GPLs for specific purposes.

---

> **Résumé** :
> 
> * Modeling languages formalize thoughts and visualize reality, covering general-purpose languages (GPLs), domain-specific languages (DSLs), and customize GPLs.

---

## 6.1 ANATOMY OF MODELING LANGUAGES

A modeling language is defined by three core ingredients:

* *Abstract syntax*: Describes the language’s structure and how primitives can be combined, regardless of representation.

* *Concrete syntax*: Describes specific representations, including encoding and visual appearance. It can be textual or graphical and is a reference for designers during modeling.

* *Semantics*: Describes the meaning of language elements and combinations.

Modeling languages require three mandatory ingredients: semantics, abstract syntax, and concrete syntax. Figure 6.1 illustrates their relationships. Semantics defines abstract syntax, which indirectly defines concrete syntax; the concrete syntax represents the abstract syntax.

This applies to both general-purpose languages (GPLs) and domain-specific ones (DSLs). Unfortunately, language designers and users often neglect aspects, especially semantics. This is likely due to the concrete syntax’s visibility, representing the actual notation used in everyday applications.

However, defining a language without fully specifying its conceptual elements and meanings is illogical. A partial or incorrect semantics leads to incorrect language usage, misunderstandings, and differing interpretations of concepts and models. This can cause confusion and errors.

![Figure 6.1: The three main ingredients of a modeling language (semantics, abstract syntax, and concrete syntax) and their relationships.](./06.%20CHAPTER%206%20Modeling%20Languages%20at%20a%20Glance/Figures/Figure%206.1.png)

Modeling languages describe the real world at a specific level of abstraction and from a particular perspective. Their semantics, which aims to describe this in detail, enables correct language usage. Semantics can be defined as:

* *Denotational*: Defining the meaning of concepts, properties, relationships, and constraints through mathematical expressions.

* *Operational*: Defining the language’s meaning by implementing an interpreter that directly defines model behavior.

* *Translational*: Mapping language concepts to another language with clearly defined semantics.

---

> **Résumé** :
> 
> * A modeling language consists of abstract syntax, concrete syntax, and semantics.
> 
> * Modeling languages require semantics, abstract syntax, and concrete syntax. Semantics defines abstract syntax, which indirectly defines concrete syntax; the concrete syntax represents the abstract syntax.
> 
> * Language designers and users often neglect semantics, focusing instead on concrete syntax.
> 
> * Defining a language without specifying semantics leads to incorrect usage and misunderstandings.
> 
> * Modeling languages describe the real world at a specific level of abstraction. Their semantics, which defines the meaning of concepts, can be denotational (using mathematical expressions), operational (through an interpreter), or translational (mapping to another language).

---

## 6.2 MULTI-VIEW MODELING AND LANGUAGE EXTENSIBILITY

In software engineering, you typically model orthogonal system aspects using different modeling languages or a multi-viewpoint modeling language with various diagram types.

System aspects are classified into *static (or structural)* and dynamic aspects. Static aspects describe the main ingredients and their relations, while *dynamic* aspects describe their behavior in terms of actions, events, and interactions. Separating static and dynamic aspects is usually a good practice.

Languages often include extensibility mechanisms that allow designers to define new modeling elements, which is common in GPLs that need specialization for specific domains or problems. This can lead to domain-specific languages developed from general-purpose ones.

A well-known example is UML, the GPL proposed by OMG within the MDA framework. UML is a general-purpose language with various diagrams and extension mechanisms. Several extensions have become standard languages, such as SysML and SoaML. Therefore, UML can be seen as a *family of languages (or language suite)* in three senses: as a whole with enough variability to be considered a group of languages, paired with correlated languages like OCL that improve its expressive power, and accompanied by domain-specific profiles defined around it.

---

> **Résumé** :
> 
> * Software engineering models orthogonal system aspects using different modeling languages or multi-viewpoint modeling languages.
> 
> * System aspects are classified into static and dynamic aspects. Static aspects describe ingredients and relations, while dynamic aspects describe behavior.
> 
> * Languages often include extensibility mechanisms for defining new modeling elements, leading to domain-specific languages.
> 
> * UML, proposed by OMG within the MDA framework, is a general-purpose language with various diagrams and extension mechanisms. It can be seen as a family of languages due to its variability, correlated languages like OCL, and domain-specific profiles.

---

## 6.3 GENERAL-PURPOSE VS. DOMAIN-SPECIFIC MODELING LANGUAGES

As mentioned in Chapter 1, modeling languages are classified as domain-specific or general-purpose.

*Domain-Specific Modeling Languages (DSMLs, or DSLs for short)* are languages designed for specific domains, contexts, or companies to support people describing things in those domains.

*General-Purpose Modeling Languages (GPMLs, or GMLs/GPLs)* are modeling notations applicable to any sector or domain.

However, this distinction is not so deterministic and well-defined. Deciding whether a language is a DSL or GPL is not a binary choice. For instance, UML and similar languages seem to belong to the latter group, since they can model any domain. However, if we consider modeling in general, UML is a DSL tailored to the specification of (mainly object-oriented) software systems.

The decision on whether to use UML (or any other GPL) or a DSL for a modeling project is significant. While UML may not be the best option for certain domains (like user interaction design), a domain-specific language tailored to that domain can produce better results. However, discussing DSL vs. UML without acknowledging UML’s many-domains language (MDL) nature is misleading. UML may not be suitable for all domains, but it can be easily applied to model many of them successfully.

UML may have flaws, but we’re aware of them. Creating an unnecessary DSL may repeat UML’s mistakes. Avoid reinventing the wheel. If your DSL resembles UML, consider using a subset of UML and avoiding new "almost-UML" notations.

On the theoretical side, concerning GPLs, one may wonder if a language to be a GPL must also be Turing-complete. If not, it means it’s not truly "general," since it can’t solve every problem. However, this interpretation is rarely considered, and the definition of a language as GPL or DSL is more a matter of practice or subjectivity. Martin Fowler clarifies that even deciding whether a set of concepts (or operations) is a language or just a set of operations within another language is a matter of perspective.

---

> **Résumé** :
> 
> * Modeling languages are classified as domain-specific or general-purpose.
> 
> * Domain-Specific Modeling Languages (DSMLs, or DSLs for short) are designed for specific domains to support people describing things in those domains.
> 
> * General-Purpose Modeling Languages (GPMLs, or GMLs/GPLs) are applicable to any sector or domain.
> 
> * The distinction between DSL and GPL is not binary, as seen with UML, which can model any domain but is tailored to software systems.
> 
> * UML, while not suitable for all domains, can be effectively applied to model many domains successfully.
> 
> * Avoid reinventing the wheel by using a subset of UML instead of creating a new DSL.
> 
> * The definition of a language as GPL or DSL is subjective, with the distinction often based on practical considerations rather than strict theoretical criteria.

---

## 6.4 GENERAL-PURPOSE MODELING: THE CASE OF UML

This section provides an overview of the *Unified Modeling Language (UML)*. UML is widely known and adopted, making it an interesting example for discussing general characteristics of modeling languages. It’s a full-fledged language suite with various diagrams for describing a system from different perspectives. Figure 6.2 shows the taxonomy of UML diagrams, with 7 for static aspects and 7 for dynamic aspects. As shown in Figure 6.3, some diagrams describe class characteristics, while others describe instance features and behavior. Some diagrams can describe both levels.

![Figure 6.2: UML diagrams taxonomy.](./06.%20CHAPTER%206%20Modeling%20Languages%20at%20a%20Glance/Figures/Figure%206.2.png)

![Figure 6.3: Dichotomy between class- and instance-based models in UML.](./06.%20CHAPTER%206%20Modeling%20Languages%20at%20a%20Glance/Figures/Figure%206.3.png)

UML is a modeling language that doesn’t enforce a specific development method. It’s often mentioned with the Unified Process (UP), particularly its specialization, Rational Unified Process (RUP). RUP is an iterative software development process framework created by Rational Software Corporation (now IBM). While RUP and UML work well together, adopting RUP isn’t necessary for using UML.

UML, a unifying language for software modeling, has a long history of merges and restructuring. Some pieces, like Harel’s statecharts and Booch’s notations, date back to the mid-1980s when various notations existed. The first version of UML emerged in 1996 from the fusion of Booch, Rumbaugh, and Jacobson’s approaches. Discussed at OOPSLA, it was submitted to OMG in August 1997 and released as UML 1.1 in November 1997. Despite criticisms, UML remains a complex and inconsistent language, yet remains a crucial tool for software modeling.

---

> **Résumé** :
> 
> * UML is a widely adopted modeling language suite with various diagrams for describing systems. It includes 14 diagrams, seven for static and seven for dynamic aspects, covering class characteristics, instance features, and behavior.
> 
> * UML is a modeling language that can be used independently of the Unified Process (UP) or its specialization, Rational Unified Process (RUP).
> 
> * UML, a software modeling language, emerged in 1996 from the fusion of Booch, Rumbaugh, and Jacobson’s approaches. Despite criticisms, it remains a crucial tool for software modeling.

---

### 6.4.1 DESIGN PRACTICES

UML facilitates system design and promotes good design practices. It offers several features:

* Integrated and orthogonal models: UML’s diagrams share symbols and allow cross-referencing between modeling artifacts.
- Modeling at different levels of detail: UML allows designers to choose the right amount of information to include in diagrams based on the purpose and phase of development.

* Extensibility: UML provides features for designing customized modeling languages.

* Pattern-based design: UML includes well-known design patterns defined by the Gang of Four.

The following sections describe a few details about UML modeling to provide an overview of a typical GPL.

---

> **Résumé** :
> 
> * UML enables system design through integrated models, customizable modeling languages, and pattern-based design, allowing designers to choose the right level of detail for their needs.
> 
> * UML modeling details are provided to overview a typical GPL.

---

### 6.4.2 STRUCTURE DIAGRAMS (OR STATIC DIAGRAMS)

*Structure diagrams* describe the elements in a system being modeled. They’re used extensively in documenting software systems at two main levels.

* The system’s *conceptual items* of interest. This level of design describes the domain and system in terms of concepts and their associations. Typical diagrams describe this part.

	1. *Class diagram*: Describes a system’s structure using classes, attributes, and relationships. Classes can be described at different levels of detail.

	2. *Composite structure diagram*: Describes the internal structure of a class and its collaborations. They use a syntax similar to class diagrams but exploit containment and connections between items. The core concepts are *parts* (i.e., roles played at runtime by instances), *ports* (i.e., interaction points connecting classifiers), and *connectors* (undirected edges connecting entities through ports).

	3. *Object diagram*: A view of the structure of example instances of modeled concepts at a specific point in time, possibly including property values. Similar to class diagrams, objects are identified by underlined names. They can also be identified by the tuple object name and class name, the simple object name, or the class they’re instantiated from. The respective notations are as follows:

		`objectName:ClassName` or `objectName` or `:ClassName`

* The *architectural representation* of the system. This level of design describes the system’s architectural organization and structure. It typically consists of reuse and deployment-oriented information, based on the conceptual modeling done in the previous step. The diagrams in this part of the design include:

	1. *Component diagram*: Describes how a software system is divided into components and their dependencies. In UML, a component is a distributable piece of implementation, including software code and other information, that implements a subsystem.

	2. *Package diagram*: Describes how a system is divided into logical groupings called packages in UML, along with their dependencies.

	3. *Deployment diagram*: Describes how software artifacts are deployed on hardware in systems’ implementations.

---

> **Résumé** :
> 
> * Structure diagrams describe system elements, used extensively in software documentation.
> 
> * The system’s conceptual items are described using class, composite structure, and object diagrams. These diagrams illustrate the system’s structure, internal class composition, and example instances of modeled concepts.
> 
> * The architectural design level describes the system’s organization and structure, including component, package, and deployment diagrams.

---

### 6.4.3 BEHAVIOR DIAGRAMS (OR DYNAMIC DIAGRAMS)

*Behavior diagrams* describe system events and interactions. Different diagrams describe dynamic aspects, some equivalent in information. Designers choose graphical notation based on prominent aspects. Behavioral models with these diagrams usually describe a single or few system features and their dynamic interactions. The behavioral diagrams are the following:

* *Use case diagram*: Describes a system’s functionality in terms of external actors, their goals, and dependencies. They help understand the system’s boundaries and clarify usage scenarios. They’re particularly relevant in the requirement specification phase and early
design phase.

* *Activity diagram*: Describes the step-by-step workflows of activities to reach a goal. It shows the overall flow of data and control through an oriented graph, with nodes representing the *activities*.

* *State machine diagram (or statechart)*: Describes the states and state transitions of a system, subsystem, or object. They’re suitable for describing event-driven, discrete behavior, but not continuous behavior. In statecharts, nodes represent states (not actions), unlike in activity diagrams.

* *Interaction diagrams*: A subset of behavior diagrams focus on the flow of control and data among system elements. They include the following diagrams.

	1. *Sequence diagram*: Shows how objects communicate through a temporal sequence of messages. Messages are sequenced vertically on a timeline, and the lifespan of associated objects is reported. Interaction diagrams describe system execution scenarios.

	2. *Communication or collaboration diagram*: Shows the interactions between objects or classes using solid, undirected lines connecting elements that can interact. Messages flow through these links. Sequencing information is obtained by numbering messages. They describe both some static structure (links and nodes) and dynamic behavior (messages) of the system, combining information from class, sequence, and use case diagrams. 

	3. *Interaction overview diagram*: Shows interaction diagrams represented by nodes.

	4. *Timing diagrams*: Interaction diagrams that focus on timing constraints.

---

> **Résumé** :
> 
> * Behavior diagrams describe system events and interactions, with different diagrams focusing on dynamic aspects. Use case, activity, state machine, and interaction diagrams are used to describe system functionality, workflows, states, and interactions, respectively.

---

### 6.4.4 UML TOOLS

Given UML’s popularity, many UML modeling tools are available. They’re easily distinguishable from other MDD tools because they focus solely on UML design, with limited support for various MDE scenarios. For instance, they differ from metamodeling tools, which focus on designing new modeling languages.

UML tools create UML models, import/export them in XMI format, and sometimes provide partial code generation. The market offers various UML tool licenses, from open source to freeware to commercial. Wikipedia has a comprehensive list of UML tools with their main features.

---

> **Résumé** :
> 
> * UML modeling tools, popular due to UML’s prevalence, differ from metamodeling tools by focusing solely on UML design with limited support for other MDE scenarios.
> 
> * UML tools create models, import/export XMI, and sometimes generate code. Wikipedia lists UML tools with features.

---

### 6.4.5 CRITICISMS AND EVOLUTION OF UML

UML has been criticized for being verbose, cumbersome, incoherent, and unusable in domain-specific scenarios. These criticisms, as reported in Bell’s 2004 article "Death by UML Fever," are prevalent online. While some criticisms may be partially true, UML remains the reference design language for software engineers. OMG has taken these criticisms seriously and is simplifying the UML specification.

---

> **Résumé** :
> 
> * UML, despite criticisms of verbosity and complexity, remains the reference design language for software engineers. OMG is simplifying the UML specification in response to these criticisms.

---

## 6.5 UML EXTENSIBILITY: THE MIDDLE WAY BETWEEN GPL AND DSL

If the development requires unusual modeling, consider using a domain-specific language. Instead of a new DSL, extend the existing GPL to fit the needs. For example, we show UML’s extensibility features.

UML offers various extension features: stereotypes, constraints, tagged values, and profiles. The *Profile diagram*, focusing on language extensibility, shows stereotypes as classes and profiles as packages at the metamodel level. The extension relationship indicates the metamodel element a stereotype extends. This section provides an overview of these extensibility options.

---

> **Résumé** :
> 
> * Consider extending existing GPLs with domain-specific languages for unusual modeling needs.
> 
> * UML offers extensibility through stereotypes, constraints, tagged values, and profiles. The Profile diagram shows stereotypes as classes and profiles as packages.

---

### 6.5.1 STEREOTYPES

Stereotypes extend meta-classes by defining additional semantics for their concept. A model element can be stereotyped multiple ways. To define a stereotype, specify the following properties:

* *Base metaclasses*, defining the elements to be extended.

* *Constraints*, defining the special rules and semantics that apply to this specialization, characterizing the stereotype in terms of semantics.

* *Tagging values*, defining zero or more values the stereotype may need for proper functioning.

* *Icon*, defining the visual appearance of stereotyped elements in the diagrams.

One doubt may arise: why not use standard sub-classing instead of stereotyping? Subclassing defines a special relation between items in the same model, while stereotypes define new modeling concepts used to create models. Stereotypes are typically used to define (i) additional semantic constraints, (ii) semantics outside UML’s scope (e.g., metadata for code generators), or (iii) new modeling concepts with specific behavior or properties that will often be reused.

---

> **Résumé** :
> 
> * Stereotypes extend metaclasses by defining additional semantics for their concept. A model element can be stereotyped multiple ways, specifying base metaclasses, constraints, tagging values, and an icon.
> 
> * Stereotypes define new modeling concepts, while subclassing defines a special relation between items in the same model. Stereotypes are used for additional semantic constraints, semantics outside UML’s scope, and new modeling concepts.

---