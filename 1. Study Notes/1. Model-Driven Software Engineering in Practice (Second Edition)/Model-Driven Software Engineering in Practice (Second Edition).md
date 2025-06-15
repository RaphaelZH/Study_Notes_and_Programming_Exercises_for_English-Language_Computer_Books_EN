Title: Sans titre  
Author:

# CHAPTER 8 Model-to-Model Transformations

Models are dynamic entities that undergo various processes during an MDE process. These processes include *merging*, *aligning*, *refactoring*, *refining*, and *translating* models.

All these model operations are implemented as model transformations, either Model-to-Model (M2M) or Model-to-Text (M2T) transformations. In M2M, the input and output are models; in M2T, the output is a text string. Text-to-Model (T2M) transformations have a text string as input and a model as output; they’re typically applied in reverse engineering (cf. Chapter 3).

Many efforts have been spent designing specialized languages for specifying M2M transformations, ranging from textual to visual, declarative to imperative, and semi-formal to formal, in the last decade. We review most of them in the next sections and focus on two protagonists to illustrate their main characteristics.

> **Résumé** :
> 
> Models are dynamic entities undergoing ***merging***, ***alignment***, ***refactoring***, ***refinement***, and ***translation*** within an MDE process.
> 
> Model transformations, implemented as Model-to-Model (M2M) or Model-to-Text (M2T), convert models to models or text strings, respectively. Text-to-Model (T2M) transformations, used in reverse engineering, convert text strings to models.
> 
> Various M2M transformation languages have been designed, ranging from textual to visual and declarative to imperative. Two languages are highlighted to illustrate their characteristics.

## 8.1 MODEL TRANSFORMATIONS AND THEIR CLASSIFICATION

Transformations are a key software engineering technique since the introduction of high-level programming languages compiled to assembler. Model transformations are equally crucial in MDE and come in various flavors to address different tasks.

An M2M transformation is a program that takes one or more models as input and produces one or more models as output. *One-to-one* transformations are usually sufficient, but *one-to-many*, *many-to-one*, or *many-to-many* transformations may be required, for example, in a model merge scenario to unify multiple class diagrams.

Besides classifying model transformations based on input and output models, another dimension is whether the transformation is between models from different languages (*exogenous*) or within the same language (*endogenous*). An example of an exogenous transformation is transforming a platform-independent model (e.g., a UML model) to a platform-specific model (e.g., a Java model). An example of an endogenous transformation is model refactoring, which involves restructuring models to improve quality.

Exogenous model transformations are useful for both *vertical* and *horizontal* transformations. Vertical transformations change the abstraction level of the input and output models, as seen in the UML to Java scenario. Horizontal transformations change the abstraction level of the input and output models, but they remain similar. For example, horizontal transformations are used for model exchange between modeling tools, such as translating a UML class diagram to an ER diagram.

Two central execution paradigms for model transformations emerged in the last decade, as compared in Figure 8.1. First, *out-place* transformations *generate* the output model from scratch (Figure 8.1a), suitable for exogenous transformations. Second, *in-place* transformations *rewrite* the model by creating, deleting, and updating elements in the input model (Figure 8.1b), perfect for endogenous transformations like refactorings.

![Figure 8.1: Different kinds of model transformations: (a) exogenous out-place vs. (b) endogenous in-place.](./08.%20CHAPTER%208%20Model-to-Model%20Transformations/Figures/Figure%208.1.png)

We present how to specify *exogenous* transformations as *out-place* transformations using ATL and *endogenous* transformations as *in-place* transformations using graph transformation languages.

> **Résumé** :
> 
> * Model transformations are crucial in MDE, solving various tasks through different techniques.
> 
> * M2M transformations convert models into other models, with ***one-to-one*** transformations being the most common, but ***one-to-many***, ***many-to-one***, and ***many-to-many*** transformations are also possible.
> 
> * Model transformations are classified based on input/output models and language. ***Exogenous*** transformations involve different languages, while ***endogenous*** transformations occur within the same language, such as model refactoring.
> 
> * Exogenous model transformations are useful for both ***vertical*** and ***horizontal*** transformations, enabling model exchange between different modeling tools.
> 
> * Two model transformation paradigms emerged: ***out-place*** transformations for ***generating*** output models and ***in-place*** transformations for ***rewriting*** input models.
> 
> * ***Exogenous*** transformations are specified as ***out-place*** transformations using ATL, while ***endogenous*** transformations are specified as ***in-place*** transformations using graph transformation languages.

## 8.2 EXOGENOUS, OUT-PLACE TRANSFORMATIONS

ATLAS Transformation Language (ATL) is the illustrative transformation language for developing exogenous, out-place transformations. It’s widely used in academia and industry, with mature tool support. ATL is a rule-based language that builds on OCL but provides dedicated features for model transformations missing in OCL, like creating model elements.

ATL, a hybrid model transformation language, combines declarative and imperative constructs. It’s *uni-directional*, requiring two transformations for language A to B and vice versa. ATL transformations operate on *read-only* source models and produce *write-only* target models. For out-place transformations, we use *source model* for *input model* and *target model* for *output model*.

During ATL transformations, source models are queried but not modified. Target model elements are created but not queried directly. These restrictions ensure that query results from source and target models remain consistent regardless of the transformation’s execution state, which contradicts the declarative nature of ATL.

<font style="color: #006ec7 ">Anatomy of ATL transformations.</font> &emsp; An ATL transformation is represented as a *module* with a *header* and a *body* section. The header section specifies the module name and declares the source and target models, which are typed by their metamodels. ATL transformations can have multiple input and output models.

The ATL transformation body consists of *rules* and *helpers* stated in arbitrary order after the header section.

* **Rules**: Each rule describes how a part of the target model should be generated from a part of the source model. ATL has two kinds of declarative rules: *matched* rules and *lazy* rules. Matched rules are automatically matched by the ATL execution engine, while lazy rules require explicit calling from another rule, giving the transformation developer more control over the execution.

	Rules consist of *input* and *output* patterns. The input pattern filters source model elements relevant to the rule by defining input pattern elements. Each input pattern element requires an obligatory type (corresponding to a metaclass in the source metamodel) and an optional filter condition (expressed as an OCL expression). These constraints determine the applicable model elements. The output pattern details how the target model elements are created from the input. Each output pattern element can have multiple *bindings* to initialize the features of the target model elements. Binding values are calculated by OCL expressions.

* **Helpers**: A helper is an auxiliary function that enables the possibility of factoring ATL code used in different points of the transformation. There are two types of helpers: one simulates a derived attribute that needs to be accessible throughout the transformation, and the other represents an operation that calculates a value for a given context object and input parameters. Unlike rules, helpers cannot produce target model elements; they can only return values that are further processed within rules.

<font style="color: #006ec7 ">Execution phases of ATL transformations.</font> &emsp; ATL, a powerful language, allows us to define transformations concisely. To understand its syntax, let’s examine the actual transformation execution by the ATL virtual machine. ATL transformations are executed in three sequential phases.

**Phase 1: Module initialization.** In the first phase, the *trace model* for storing *trace links* between source and target elements is initialized. In phase 2, each matched rule execution creates a trace link pointing to the matched input and output elements. The trace model is crucial for exogenous transformations: (i) stopping transformations and (ii) assigning target element features based on source element values.

**Phase 2: Target elements allocation.** In the second phase, the ATL transformation engine finds valid configurations of source model elements that match the source pattern of the matched rules. When a matched rule’s condition is fulfilled by a configuration, the engine allocates the corresponding target model elements based on the declared target pattern elements. Only the elements are created, not their features. Each match creates a trace link connecting the matched source elements to the generated target elements.

**Phase 3: Target elements initialization.** In the third phase, each allocated target model element is initialized by executing the bindings defined for the target pattern element. These bindings often invoke the *resolveTemp* operation, which allows references to any target model elements generated in the second execution phase for a given source model element. The resolveTemp operation has the signature `resolveTemp(srcObj: OclAny, targetPatternElementVar: String)`. The first parameter represents the source model element for which target elements need to be resolved, while the second parameter is the variable name of the target pattern element to retrieve. This parameter is required because multiple target pattern elements can be used in a rule to generate multiple target elements for a single source element.

<font style="color: #006ec7 ">Internal vs. external trace models.</font> &emsp; The internal trace model of the ATL transformation engine enables convenient setting of target element features and stopping rule execution. Rules are only executed if the matched input elements are not covered by an existing trace link.

If external traceability requires a persistent trace model, e.g., to see the impact of source model changes on the target model, the internal trace model (defaultly transient) may be persisted as a separate output model of the transformation.

<font style="color: #006ec7 ">Alternatives to ATL.</font> &emsp; Besides ATL, there are other dedicated transformation approaches for exogenous, out-of-place transformations.

**QVT.** The OMG’s Query-View-Transformation (QVT) standard supports three languages for model transformation development: QVT Relational, QVT Operational, and QVT Core. QVT Relational defines bi-directional correspondences between metamodels, enabling the derivation of transformations in both directions and consistency checks. QVT Operational is an imperative language for uni-directional transformations with out-of-the-box tracing support, but transformation rule dispatching requires user definition, similar to lazy rules in ATL. QVT Core is a low-level language designed for the QVT Relational compiler, not for direct transformation writing. Eclipse provides tool support for QVT Relations, QVT Core, and QVT Operational languages.

**TGG.** Triple Graph Grammars (TGGs) define a correspondence graph between two metamodels, enabling bidirectional model transformations. They synchronize models and check consistency. Similar to QVT Relations, TGGs offer a strong theoretical basis. MOFLON and Eclipse support TGGs through the TGG Interpreter and the TGG tool at MDElab.

**ETL.** The Epsilon project developed several languages for model management. The Epsilon Transformation Language (ETL) supports out-of-place model transformations similar to ATL, but it also offers features like modifying input model elements during transformations.

> **Résumé** :
> 
> * ATLAS Transformation Language (ATL), a widely used rule-based transformation language, is chosen for developing exogenous transformations due to its industry and academic adoption and mature tool support.
> 
> * ATL is a hybrid model transformation language with declarative and imperative constructs. It performs ***uni-directional*** transformations on ***read-only*** source models to produce ***write-only*** target models.
> 
> * During ATL transformations, source models are queried but not modified, while target models are created but not queried directly to maintain declarative consistency.
> 
> * An ATL transformation is a ***module*** with a ***header*** and ***body*** section. The header declares the transformation module name and source/target models, which can be multiple.
> 
> * ATL transformation body consists of ***rules*** and ***helpers***.
> 
>	 * ATL has two rule types: ***matched*** and ***lazy***. Matched rules are automatically executed, while lazy rules require explicit calls, providing more control.
> 
>	 * Rules consist of ***input*** and ***output*** patterns. The input pattern filters source model elements using metaclass types and OCL expressions, while the output pattern defines target model elements and their feature initialization.
> 
>	 * Helpers are auxiliary functions in ATL code, enabling code factorization. They simulate derived attributes or represent operations, returning values processed within rules.
> 
> * ATL transformation execution consists of three sequential phases.
> 
>	 * Phase 1 initializes the ***trace model***, storing ***trace links*** between source and target elements. Phase 2 stores each matched rule execution in the trace model.
> 
>	 * In Phase 2, the ATL transformation engine finds source model element configurations that match source patterns, allocating corresponding target model elements and creating trace links.
> 
>	 * Phase 3 initializes target model elements by executing bindings defined for target pattern elements. The ***resolveTemp*** operation is used to reference generated target model elements.
> 
> * The internal trace model in ATL is crucial for setting target element features and stopping rule execution based on existing trace links.
> 
> * Persistent trace model may be needed for external traceability, such as tracking source model changes.
> 
> * Other transformation approaches exist besides ATL for exogenous transformations.
> 
>	 * The OMG’s Query-View-Transformation (QVT) standard includes three languages for model transformations: QVT Relational (declarative, bi-directional), QVT Operational (imperative, uni-directional), and QVT Core (low-level, compiler target). Eclipse provides tool support for all three languages.
> 
>	 * Triple Graph Grammars (TGG) define correspondence graphs between metamodels, enabling model transformation, synchronization, and consistency checks. TGGs are supported by MOFLON and Eclipse.
> 
>	 * The Epsilon Transformation Language (ETL) supports out-place model transformations and allows modifying input model elements.