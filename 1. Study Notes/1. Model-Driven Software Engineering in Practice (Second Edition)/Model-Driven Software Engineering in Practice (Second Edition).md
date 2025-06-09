Title: Sans titre  
Author:

# Table of Contents

[TOC]

# CHAPTER 6 Modeling Languages at a Glance

Modeling languages are conceptual tools that let designers formalize their thoughts and visualize reality explicitly, whether textually or graphically. This chapter describes the main features of modeling languages, considering general-purpose languages (GPLs), domain-specific languages (DSLs), and the intermediate solutions that customize GPLs for specific purposes.

> **Résumé** :
> 
> * Modeling languages formalize thoughts and visualize reality, covering general-purpose languages (GPLs), domain-specific languages (DSLs), and the intermediate solutions that customize GPLs.

## 6.1 ANATOMY OF MODELING LANGUAGES

A modeling language is defined by three core ingredients:

* *Abstract syntax*: Describes the language’s structure and how primitives can be combined, regardless of representation.

* *Concrete syntax*: Describes specific representations, including encoding and visual appearance. It can be textual or graphical and is a reference for designers during modeling.

* *Semantics*: Describes the meaning of language elements and combinations.

Modeling languages require three mandatory ingredients: semantics, abstract syntax, and concrete syntax. Figure 6.1 illustrates their relationships. Semantics defines abstract syntax, which indirectly defines concrete syntax; the concrete syntax represents the abstract syntax.

![Figure 6.1: The three main ingredients of a modeling language (semantics, abstract syntax, and concrete syntax) and their relationships.](./06.%20CHAPTER%206%20Modeling%20Languages%20at%20a%20Glance/Figures/Figure%206.1.png)

This applies to both general-purpose languages (GPLs) and domain-specific ones (DSLs). Unfortunately, language designers and users often neglect aspects, especially semantics. This is likely due to the concrete syntax’s visibility, representing the actual notation used in everyday applications.

However, defining a language without fully specifying its conceptual elements and meanings is illogical. A partial or incorrect semantics leads to incorrect language usage, misunderstandings, and differing interpretations of concepts and models. This can cause confusion and errors.

Modeling languages describe the real world at a specific level of abstraction and from a particular perspective. Their semantics, which aims to describe this in detail, enables correct language usage. Semantics can be defined as:

* *Denotational*: Defining the meaning of concepts, properties, relationships, and constraints through mathematical expressions.

* *Operational*: Defining the language’s meaning by implementing an interpreter that directly defines model behavior.

* *Translational*: Mapping language concepts to another language with clearly defined semantics.

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
> * Modeling languages describe the real world at a specific abstraction level. Their semantics details this, enabling correct language usage, which can be denotational (using mathematical expressions), operational (through an interpreter), or translational (mapping to another language).

## 6.2 MULTI-VIEW MODELING AND LANGUAGE EXTENSIBILITY

In software engineering, you typically model orthogonal system aspects using different modeling languages or a multi-viewpoint modeling language with various diagram types.

System aspects are classified into *static* (or *structural)* and dynamic aspects. Static aspects describe the main ingredients and their relations, while *dynamic* aspects describe their behavior in terms of actions, events, and interactions. Separating static and dynamic aspects is usually a good practice.

Furthermore, languages often include extensibility mechanisms that allow designers to expand coverage by defining new modeling elements. This is common in GPLs, which often need specialization for specific domains or problems. This can lead to a well-known domain-specific language from general-purpose ones.

UML, a general-purpose language proposed by OMG within the MDA framework, comprises various diagrams for system description and extension mechanisms. Several extensions have become standard languages like SysML and SoaML. Thus, UML can be considered a family of languages in three senses: it allows enough variability to be considered a group of languages, pairs with correlated languages like OCL to enhance its expressive power, and is accompanied by domain-specific profiles.

> **Résumé** :
> 
> * Software engineering models orthogonal system aspects using different modeling languages or multi-viewpoint modeling languages.
> 
> * System aspects are classified into static (or structural) and dynamic aspects. Static aspects describe ingredients and relations, while dynamic aspects describe behavior. Separating these aspects is beneficial.
> 
> * Languages often include extensibility mechanisms for defining new modeling elements, especially in GPLs for domain-specific specialization, can lead to the creation of domain-specific languages.
> 
> * UML, a general-purpose language, is a family of languages due to its variability, correlated languages like OCL, and domain-specific profiles.

## 6.3 GENERAL-PURPOSE VS. DOMAIN-SPECIFIC MODELING LANGUAGES

As mentioned in Chapter 1, modeling languages are classified as domain-specific or general-purpose.

*Domain-Specific Modeling Languages (DSMLs, or DSLs for short)* are languages designed for specific domains, contexts, or companies to support people describing things in those domains.

*General-Purpose Modeling Languages (GPMLs, or GMLs/GPLs)* are modeling notations applicable to any sector or domain.

However, this distinction is not so deterministic and well-defined. Deciding whether a language is a DSL or GPL is not a binary choice. For instance, UML and similar languages seem to belong to the latter group, since they can model any domain. However, if we consider modeling in general, UML is a DSL tailored to the specification of (mainly object-oriented) software systems.

The decision on whether to use UML (or any other GPL) or a DSL for a modeling project is significant. While UML may not be the best option for certain domains (like user interaction design), a domain-specific language tailored to that domain can produce better results. However, discussing DSL vs. UML without acknowledging UML’s many-domains language (MDL) nature is misleading. UML may not be suitable for all domains, but it can be easily applied to model many of them successfully.

UML may have flaws, but we’re aware of them. Creating an unnecessary DSL may repeat UML’s mistakes. Avoid reinventing the wheel. If your DSL resembles UML, consider using a subset of UML and avoiding new "almost-UML" notations.

On the theoretical side, concerning GPLs, one may wonder if a language to be a GPL must also be Turing-complete. If not, it means it’s not truly "general," since it can’t solve every problem. However, this interpretation is rarely considered, and the definition of a language as GPL or DSL is more a matter of practice or subjectivity. Martin Fowler clarifies that even deciding whether a set of concepts (or operations) is a language or just a set of operations within another language is a matter of perspective.

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

## 6.4 GENERAL-PURPOSE MODELING: THE CASE OF UML

This section provides an overview of the *Unified Modeling Language (UML)*. UML is widely known and adopted, making it an interesting example for discussing general characteristics of modeling languages. It’s a full-fledged language suite with various diagrams for describing a system from different perspectives. Figure 6.2 shows the taxonomy of UML diagrams, with 7 for static aspects and 7 for dynamic aspects. As shown in Figure 6.3, some diagrams describe class characteristics, while others describe instance features and behavior. Some diagrams can describe both levels.

![Figure 6.2: UML diagrams taxonomy.](./06.%20CHAPTER%206%20Modeling%20Languages%20at%20a%20Glance/Figures/Figure%206.2.png)

![Figure 6.3: Dichotomy between class- and instance-based models in UML.](./06.%20CHAPTER%206%20Modeling%20Languages%20at%20a%20Glance/Figures/Figure%206.3.png)

UML is a modeling language that doesn’t enforce a specific development method. It’s often mentioned with the Unified Process (UP), particularly its specialization, Rational Unified Process (RUP). RUP is an iterative software development process framework created by Rational Software Corporation (now IBM). While RUP and UML work well together, adopting RUP isn’t necessary for using UML.

UML, a unifying language for software modeling, has a long history of merges and restructuring. Some pieces, like Harel’s statecharts and Booch’s notations, date back to the mid-1980s when various notations existed. The first version of UML emerged in 1996 from the fusion of Booch, Rumbaugh, and Jacobson’s approaches. Discussed at OOPSLA, it was submitted to OMG in August 1997 and released as UML 1.1 in November 1997. Despite criticisms, UML remains a complex and inconsistent language, yet remains a crucial tool for software modeling.

> **Résumé** :
> 
> * UML is a widely adopted modeling language suite with various diagrams for describing systems. It includes 14 diagrams, seven for static and seven for dynamic aspects, covering class characteristics, instance features, and behavior.
> 
> * UML is a modeling language that can be used independently of the Unified Process (UP) or its specialization, Rational Unified Process (RUP).
> 
> * UML, a software modeling language, emerged in 1996 from the fusion of Booch, Rumbaugh, and Jacobson’s approaches. Despite criticisms, it remains a crucial tool for software modeling.

### 6.4.1 DESIGN PRACTICES

UML facilitates system design and promotes good design practices. It offers several features:

* Integrated and orthogonal models: UML’s diagrams share symbols and allow cross-referencing between modeling artifacts.

* Modeling at different levels of detail: UML allows designers to choose the right amount of information to include in diagrams based on the purpose and phase of development.

* Extensibility: UML provides features for designing customized modeling languages.

* Pattern-based design: UML includes well-known design patterns defined by the Gang of Four.

The following sections describe a few details about UML modeling to provide an overview of a typical GPL.

> **Résumé** :
> 
> * UML facilitates system design with integrated and orthogonal models, modeling at different levels of detail, extensibility (customized modeling languages), and pattern-based design.
> 
> * UML modeling details are provided to overview a typical GPL.

### 6.4.2 STRUCTURE DIAGRAMS (OR STATIC DIAGRAMS)

*Structure diagrams* describe the elements in a system being modeled. They’re used extensively in documenting software systems at two main levels.

* The system’s *conceptual items* of interest. This level of design describes the domain and system in terms of concepts and their associations. Typical diagrams describe this part.

	1. *Class diagram*: Describes a system’s structure using classes, attributes, and relationships. Classes can be described at different levels of detail.

	2. *Composite structure diagram*: Describes the internal structure of a class and its collaborations. They use a syntax similar to class diagrams but exploit containment and connections between items. The core concepts are *parts* (i.e., roles played at runtime by instances), *ports* (i.e., interaction points connecting classifiers), and *connectors* (undirected edges connecting entities through ports).

	3. *Object diagram*: A view of the structure of example instances of modeled concepts at a specific point in time, possibly including property values. Similar to class diagrams, objects are identified by underlined names. They can also be identified by the tuple object name and class name, the simple object name, or the class they’re instantiated from. The respective notations are as follows:

		<ins>objectName:ClassName</ins> or <ins>objectName</ins> or <ins>:ClassName</ins>

* The *architectural representation* of the system. This level of design describes the system’s architectural organization and structure. It typically consists of reuse and deployment-oriented information, based on the conceptual modeling done in the previous step. The diagrams in this part of the design include:

	1. *Component diagram*: Describes how a software system is divided into components and their dependencies. In UML, a component is a distributable piece of implementation, including software code and other information, that implements a subsystem.

	2. *Package diagram*: Describes how a system is divided into logical groupings called packages in UML, along with their dependencies.

	3. *Deployment diagram*: Describes how software artifacts are deployed on hardware in systems’ implementations.

> **Résumé** :
> 
> * Structure diagrams describe system elements, used extensively in software documentation.
> 
> * The system’s conceptual items are described using class, composite structure, and object diagrams. These diagrams illustrate the system’s structure, internal class composition, and example instances of modeled concepts.
> 
> * The architectural design level describes the system’s organization and structure, including component, package, and deployment diagrams.

### 6.4.3 BEHAVIOR DIAGRAMS (OR DYNAMIC DIAGRAMS)

*Behavior diagrams* describe system events and interactions. Different diagrams describe dynamic aspects, some equivalent in information. Designers choose graphical notation based on prominent aspects. Behavioral models with these diagrams usually describe a single or few system features and their dynamic interactions. The behavioral diagrams are the following:

* *Use case diagram*: Describes a system’s functionality in terms of external actors, their goals, and dependencies. They help understand the system’s boundaries and clarify usage scenarios. They’re especially relevant in the requirements and early design phases.

* *Activity diagram*: Describes the step-by-step workflows of activities to reach a goal. It shows the overall flow of data and control through an oriented graph, with nodes representing the *activities*.

* *State machine diagram* (or *statechart*): Describes the states and state transitions of a system, subsystem, or object. They’re suitable for describing event-driven, discrete behavior, but not continuous behavior. In statecharts, nodes represent states (not actions), unlike in activity diagrams.

* *Interaction diagrams*: A subset of behavior diagrams focus on the flow of control and data among system elements. They include the following diagrams.

	1. *Sequence diagram*: Shows how objects communicate through a temporal sequence of messages. Messages are sequenced vertically on a timeline, and the lifespan of associated objects is reported. Interaction diagrams describe system execution scenarios.

	2. *Communication or collaboration diagram*: Shows the interactions between objects or classes using solid, undirected lines connecting elements that can interact. *Messages* flow through these *links* (solid, undirected lines connecting interacting elements). Sequencing information is obtained by numbering messages. They describe both some static structure (links and nodes) and dynamic behavior (messages) of the system, combining information from class, sequence, and use case diagrams. 

	3. *Interaction overview diagram*: Shows interaction diagrams represented by nodes.

	4. *Timing diagrams*: Interaction diagrams that focus on timing constraints.

> **Résumé** :
> 
> * Behavior diagrams describe system events and interactions, with different diagrams focusing on dynamic aspects. Use case, activity, state machine, and interaction diagrams are used to describe system functionality, workflows, states, and interactions, respectively.

### 6.4.4 UML TOOLS

Given UML’s popularity, many UML modeling tools are available. They’re easily distinguishable from other MDD tools because they focus solely on UML design, with limited support for various MDE scenarios. For instance, they differ from metamodeling tools, which focus on designing new modeling languages.

UML tools create UML models, import/export them in XMI format, and sometimes provide partial code generation. The market offers various UML tool licenses, from open source to freeware to commercial. Wikipedia has a comprehensive list of UML tools with their main features.

> **Résumé** :
> 
> * UML modeling tools, popular due to UML’s prevalence, differ from metamodeling tools by focusing solely on UML design with limited support for other MDE scenarios.
> 
> * UML tools create models, import/export them in XMI format, and sometimes generate code. Wikipedia lists UML tools with features.

### 6.4.5 CRITICISMS AND EVOLUTION OF UML

UML has been criticized for being verbose, cumbersome, incoherent, and unusable in domain-specific scenarios. These criticisms, as reported in Bell’s 2004 article "Death by UML Fever," are prevalent online. While some criticisms may be partially true, UML remains the reference design language for software engineers. OMG has taken these criticisms seriously and is simplifying the UML specification.

> **Résumé** :
> 
> * UML, despite criticisms of verbosity and complexity, remains the reference design language for software engineers. OMG is simplifying the UML specification in response to these criticisms.

## 6.5 UML EXTENSIBILITY: THE MIDDLE WAY BETWEEN GPL AND DSL

If the development requires unusual modeling, consider using a domain-specific language. Instead of a new DSL, extend the existing GPL as an intermediate solution to fit the needs. For example, we show UML’s extensibility features.

UML offers various extension features: stereotypes, constraints, tagged values, and profiles. The *Profile diagram*, focusing on language extensibility, shows stereotypes as classes and profiles as packages at the metamodel level. The extension relationship indicates the metamodel element a stereotype extends. This section provides an overview of these extensibility options.

> **Résumé** :
> 
> * Consider using a domain-specific language for unusual modeling, or extending an existing GPL.
> 
> * UML offers extensibility through stereotypes, constraints, tagged values, and profiles. The Profile diagram shows stereotypes as classes and profiles as packages.

### 6.5.1 STEREOTYPES

Stereotypes extend meta-classes by defining additional semantics for their concept. A model element can be stereotyped multiple ways. To define a stereotype, specify the following properties:

* *Base metaclasses*, defining the elements to be extended.

* *Constraints*, defining the special rules and semantics that apply to this specialization, characterizing the stereotype in terms of semantics.

* *Tagging values*, defining zero or more values the stereotype may need for proper functioning.

* *Icon*, defining the visual appearance of stereotyped elements in the diagrams.

One doubt may arise: why not use standard sub-classing instead of stereotyping? Subclassing defines a special relation between items in the same model, while stereotypes define new modeling concepts used to create models. Stereotypes are typically used to define (i) additional semantic constraints, (ii) additional semantics outside UML’s scope (e.g., metadata for code generators), or (iii) new modeling concepts with specific behavior or properties that will often be reused.

> **Résumé** :
> 
> * Stereotypes extend metaclasses by defining additional semantics for their concept. A model element can be stereotyped multiple ways, specifying base metaclasses, constraints, tagging values, and an icon.
> 
> * Stereotypes define new modeling concepts, while subclassing defines a special relation between items in the same model. Stereotypes are used for additional semantic constraints, additional semantics outside UML’s scope, and reusable new modeling concepts.

### 6.5.2 PREDICATES

Another way to vary UML semantics is to use *restriction predicates* (e.g., OCL expressions) that reduce semantic variation of modeling elements. Predicates can be attached to any UML meta-class or stereotype and can be formal or informal expressions. To be coherent with UML symbols, expressions must not contradict the inherited base semantics of elements.

> **Résumé** :
> 
> * Restriction predicates, such as OCL expressions, can be used to vary UML semantics by reducing the semantic variation of modeling elements. These predicates can be attached to any UML meta-class or stereotype and can be formal or informal expressions.

### 6.5.3 TAGGED VALUES

*Tagged values* consist of a tag-value pair that can be attached as a typed property to a stereotype. They allow designers to specify additional information useful for implementing, transforming, or executing a model, such as defining project management data. For example, a tagged value "status = unit_tested" can declare that a component has gone through the unit testing phase.

> **Résumé** :
> 
> * Tagged values are typed properties attached to stereotypes, providing additional information for model implementation, transformation, or execution.

### 6.5.4 UML PROFILING

*UML profiles* are packages of related and coherent extensibility elements defined with the above techniques. They capture domain-specific variations and usage patterns for the language. In essence, profiles are domain-specific interpretations of UML, akin to domain-specific languages defined by extending or restricting UML.

Designers can define their profiles, but several UML profiles are standardized and widely used. Examples include well-known profiles that became standards in OMG (mentioned in Chapter 4 without highlighting they were UML profiles).

* UML Testing Profile (UTP): A UML profile that extends UML to support designing, visualizing, specifying, analyzing, constructing, and documenting testing artifacts.

* OMG Systems Modeling Language (SysML).

* Service-oriented architecture Modeling Language (SoaML).

* UML profile for a System on a Chip (SoCP).

* UML Profile for Schedulability, Performance, and Time.

* UML Profile for Modeling and Analyzing Real-time and Embedded Systems (MARTE).

The complete list is available online on the OMG website.

> **Résumé** :
> 
> * UML profiles are domain-specific interpretations of UML, capturing domain-specific variations and usage patterns for the language.
> 
> * Several standardized UML profiles, including UTP, SysML, SoaML, SoCP, and MARTE, extend UML to support various modeling needs.
> 
> * The complete list is available online.

## 6.6 OVERVIEW ON DSLS

Domain-Specific Modeling Languages (DSMLs), also known as Domain-Specific Languages (DSLs), are designed to address the needs of a specific application domain. They are tailored to the domain’s requirements, both in terms of expressive power and notation, making them particularly useful.

DSLs don’t force users to learn more general-purpose languages with irrelevant concepts. Instead, they provide appropriate modeling abstractions and primitives closer to the domain.

> **Résumé** :
> 
> * Domain-Specific Modeling Languages (DSMLs), also known as Domain-Specific Languages (DSLs), are tailored to specific application domains, enhancing their usefulness.
> 
> * DSLs simplify domain-specific modeling by providing relevant abstractions and primitives.

### 6.6.1 PRINCIPLES OF DSLS

DSLs are essential for many application scenarios, beyond software development. Designing a DSL requires deep domain knowledge and language engineering practices. Finding the right abstractions for defining a DSL is challenging and time-consuming.

To be useful, the DSL should follow these principles:

* The language should provide good abstractions, be intuitive, and simplify development, not complicate it.

* The language should be adopted and used by everyone, and its definition should be agreed upon after some evaluation, not just by one person.

* The language must evolve and be updated based on user and context needs to avoid extinction.

* Domain experts prioritize maximizing productivity in their domains, but they’re unwilling to invest significant time in defining methods and tools. Therefore, the language must be combined with supporting tools and methods.

* A good DSL should be open for extensions but closed for modifications, following the open-close principle that "software entities should be open for extension, but closed for modification."

Good DSLs don’t appear out of nowhere. MDSE aims to have good language designers who build suitable DSLs for the right audience. Refining a good language takes years, involving industrial experience and thousands of users. While DSL development is encouraged, careful design is essential. Defining a new DSL is not trivial and may lead to a language with weaknesses or drawbacks for future users. Tools, design interfaces, and runtime architectures should be tailored to the domain to avoid user rejection.

**Classification of DSLs**

DSLs can be classified based on focus, style, notation, internality, and execution.

**Focus**

DSLs can be vertical or horizontal. Vertical DSLs target specific industries or fields, like configuration languages for home automation, modeling languages for biological experiments, and analysis languages for financial applications. Horizontal DSLs have broader applicability and can apply to many applications. Examples include SQL, Flex, IFML, WebML, and more.

**Style**

DSLs can be declarative or imperative. Declarative DSLs express computation logic without describing control flow. They define what a program should accomplish, not how. Service choreography is a typical declarative definition, defining Web service coupling rules. Imperative DSLs require defining an executable algorithm with steps and control flow to complete a job. Service orchestration is a typical imperative definition, defining a start-to-end flow of execution between Web services.

**Notation**

DSLs can be graphical or textual. Graphical DSLs use visual models and graphical development primitives like blocks, arrows, edges, containers, and symbols. Textual DSLs include XML-based notations, structured text notations, and textual configuration files.

**Internality**

External DSLs, as defined by Martin Fowler, have their own custom syntax. You can write a full parser for them and use them to create self-standing, independent models and programs.

Internal DSLs extend a host language to mimic a specific domain or objective. This can be achieved by embedding DSL pieces in the host language or providing abstractions, structures, or functions. Embedding allows reuse of host language tools and facilities.

**Execution**

Executability can be implemented through model interpretation (reading and executing DSL scripts at runtime) or code generation (applying a complete model-to-text (M2T) transformation at deployment time).

> **Résumé** :
> 
> * DSLs require domain knowledge and language engineering practices for design.
> 
> * A useful DSL should provide good abstractions, be intuitive, and evolve based on user needs. It should be adopted by all, combined with supporting tools, and follow the open-close principle.
> 
> * Good DSLs require careful design, industrial experience, and thousands of users over years. Defining a new DSL is not trivial and should be tailored to the domain.
> 
> * DSLs are classified based on focus, style, notation, internality, and execution.
> 
>	 * **Focus** : DSLs can be vertical, targeting specific industries, or horizontal, with broader applicability. Examples include SQL, Flex, IFML, and WebML.
>	 
>	 * **Style**: DSLs can be declarative, defining what a program should accomplish, or imperative, defining an executable algorithm with steps and control flow.
>	 
>	 * **Notation**: DSLs can be graphical or textual, using visual models or structured text.
>	 
>	 * **Internality**: Internal DSLs extend a host language to mimic a domain, while external DSLs have their own custom syntax and can be used independently.
>	 
>	 * **Execution**: Executability can be implemented through model interpretation or code generation.