# **Omega-Code Language Reference Manual**

**Document Version:** 2.0 (Revised and Enhanced)
**Date:** June 16, 2025
**Status:** Official Release

This document provides the definitive formal definition of the Omega-Code pseudocode meta-language. It is intended for system architects, developers, and verification engineers who need to write, understand, or implement systems using Omega-Code.

---

### **1. Introduction & Purpose of Omega-Code**

Omega-Code is a formally verifiable pseudocode meta-language designed for the unambiguous specification and reasoning about complex, adaptive, and autonomous systems. Its purpose is to provide a single, provable source of truth for a system's design, spanning diverse domains from robotics and AI to foundational software like operating systems and programming languages.

The core objective of the Omega-Code initiative is to create a language that is:
* **Unambiguous:** With explicit semantics formally defined by a machine-readable EBNF grammar.
* **Evolvable:** Designed for extensibility and scale, with meta-level primitives that allow the language itself to adapt to future paradigms.
* **Inherently Governed:** Weaving safety, ethics, and auditable oversight into a system's core design specifications.

### **2. Core Design Principles**

The architecture of Omega-Code is guided by six foundational principles, synthesized from a multi-stage design and adversarial review process.

1.  **The Principle of Reality & Resource Constraints:** Specifications must be grounded in physical and computational reality. They must formally declare acknowledged boundaries, including computational limits, real-time guarantees, and resource consumption models.
2.  **The Principle of Radical Consolidation & Extensibility:** The core language is maximally simple and universal. All domain-specific complexity resides in external, composable libraries, supported by minimal abstract hooks and directives in the core.
3.  **The Principle of Inherent Governance & Ethical Oversight:** A system's governance framework must be proactive. It must include primitives for formal normative logic, conflict arbitration, and predictive impact modeling, overseen by an auditable, human-in-the-loop process.
4.  **The Principle of First-Class Agency & Emergence:** The language provides a universal, abstract framework for defining agents and their interactions, including first-class support for specifying emergent, self-organizing behaviors.
5.  **The Principle of Meta-Cognition & Evolution:** A system must be able to reason about and adapt itself. The language provides primitives for reflection (introspection) and evolution (self-modification) within a stable, controlled logical hierarchy.
6.  **The Principle of Cognitive & Cultural Ergonomics:** A specification is a form of communication. The language must support effective human reasoning by providing hooks for multi-modal interfaces and managing concepts across different value systems via versioned cultural ontologies.

### **3. Lexical Structure**

An Omega-Code specification is a sequence of tokens. The primary categories of tokens are:

* **Identifiers:** Used for names of modules, functions, variables, and all unique IDs (e.g., `ContextID`, `EntityID`, `RuleID`). They must begin with a letter (`a-z`, `A-Z`) and can be followed by any number of letters, digits (`0-9`), or underscores (`_`). Identifiers are case-sensitive and cannot be the same as a reserved keyword.
* **Keywords:** Reserved words with special meaning in the language, such as `MODULE`, `IF`, `LOOP`, `FUNCTION`, and the names of the 13 atomic primitives (e.g., `CONTEXT_RULE`). They are always written in uppercase.
* **Literals:** Represent fixed values.
    * **Boolean:** `TRUE`, `FALSE`
    * **Integer:** `123`, `0`, `42`
    * **Float:** `3.14`, `0.5`
    * **String:** `"Sequences of characters in double quotes"`
* **Operators:** Symbols for performing operations, such as `+`, `*`, `==`, `AND`, `OR`, `NOT`.
* **Delimiters & Punctuation:** Characters for structuring code, such as `( )`, `{ }`, `,`, `:`, and `;`.
* **Comments:** Ignored by the parser.
    * **Line Comments:** Begin with `--` and extend to the end of the line.
    * **Block Comments:** Begin with `(*` and end with `*)`, and can span multiple lines.

### **4. EBNF Notation Conventions**

This document uses the following Extended Backus-Naur Form (EBNF) notation to formally define the Omega-Code syntax:

* `::=` : "is defined as" or "consists of"
* `|` : "or" (separates alternatives)
* `[ item ]` : Optional item (appears zero or one time)
* `{ item }` : Item that can be repeated zero or more times
* `( item1 item2 )` : Grouping of items
* `'literal'` : Terminal symbol (must appear exactly as shown)
* `<non_terminal>` : Non-terminal symbol (defined by another rule)
* `(* comment *)` : Comments within the EBNF grammar itself

### **5. Syntax Definition (High-Level Overview)**

The Omega-Code grammar defines the structure of a valid specification. At the highest level, a program is a collection of module definitions, standalone statements, and comments.

* **Modules:** The primary organizational unit is the `MODULE`, which contains a block of statements and helps create namespaces.
* **Statements:** Statements are the core executable units. They can be simple (e.g., assignment, `RETURN`) or compound (e.g., `IF`, `LOOP`). All simple statements and primitive calls must be terminated by a semicolon (`;`).
* **Expressions:** Expressions produce values and are used in assignments, conditions, and function arguments. They are composed of literals, variables, operators, and function calls.
* **Primitives:** The 13 atomic primitives are invoked with a specific keyword-based syntax, resembling function calls with named parameters.

The complete and definitive grammar is provided in **Appendix A: Full EBNF Grammar**.

### **6. Formal Semantic Cross-Reference**

Each language construct has precise semantics defined in the *Technical Specifications: Omega-Code Pseudocode Meta-Language (v1.4)*. The following table provides a cross-reference to the relevant section for each feature and primitive.

| Feature / Primitive | Semantic Definition Reference |
| :--- | :--- |
| **Inherent Features** | |
| Syntax & Grammars | §4.1 |
| Basic Control Flow | §4.2 |
| Function/Procedure Definition | §4.3 |
| Variable Declaration & Scoping | §4.4 |
| Module/Namespace System | §4.5 |
| Primitive Data Types | §4.6 |
| Entity Identity | §4.7 |
| Formal Verification Engine Hooks| §4.8 |
| Inherent Actions/Operations | §4.9 |
| **Atomic Primitives** | |
| `CONTEXT_RULE` | §5.1.1 |
| `TEMPORAL_RELATION` | §5.1.2 |
| `RESOURCE_BOUND` | §5.1.3 |
| `ENVIRONMENT_INTERFACE_POINT` | §5.1.4 |
| `DATA_TYPE_SCHEMA` | §5.2.1 |
| `STATE_TRANSITION` | §5.2.2 |
| `TRUST_ELEMENT` | §5.2.3 |
| `GOVERNANCE_RULE` | §5.3.1 |
| `SELF_REFERENCE_POINT` | §5.3.2 |
| `MUTATION_RULE` | §5.3.3 |
| `PERCEPTION_MAP` | §5.3.4 |
| `LEARNING_AXIOM` | §5.3.5 |
| `META_DEFINITION_RULE` | §5.3.6 |

### **7. Inherent Language Features**

These are the foundational capabilities intrinsic to Omega-Code.

* **Syntax & Grammars**
    * **Purpose:** To ensure unambiguous, machine-readable specifications via a formal grammar that is itself extensible.
    * **EBNF Syntax:** See Appendix A for the full grammar, rooted at `<OmegaCode>`.
    * **Semantics:** Any valid specification must conform to the EBNF rules. The `META_DEFINITION_RULE` primitive can operate on these rules to allow for formal evolution of the language itself.

* **Basic Control Flow**
    * **Purpose:** To express algorithmic logic through sequential, conditional, and iterative execution.
    * **EBNF Syntax:**
        ```ebnf
        IfStatement ::= 'IF' <BooleanExpression> 'THEN' <Block> [ 'ELSE' <Block> ] 'END IF'
        LoopStatement ::= 'LOOP' ( 'WHILE' <BooleanExpression> | 'FOR' <VariableName> 'IN' <Range> ) <Block> 'END LOOP'
        ```
    * **Semantics:** `IF` provides conditional branching. `LOOP` provides iteration based on a `WHILE` condition or a `FOR` loop over a range. `BREAK` and `CONTINUE` are supported for loop control. Statements execute sequentially.

* **Function/Procedure Definition**
    * **Purpose:** To enable modularity, abstraction, and reusability of logic.
    * **EBNF Syntax:**
        ```ebnf
        FunctionDefinition ::= 'FUNCTION' <FunctionName> '(' [ <ParameterList> ] ')' [ 'RETURNS' <ReturnType> ] <Block> 'END FUNCTION'
        ```
    * **Semantics:** Defines a named, callable block of logic. Parameters are passed by value. A function with a `RETURNS` type must terminate with a `RETURN` statement providing a value of that type.

* **Variable Declaration & Scoping**
    * **Purpose:** To define, store, and manage data with a clear lifecycle.
    * **EBNF Syntax:**
        ```ebnf
        VariableDeclaration ::= ( 'DECLARE' | 'VAR' ) <VariableName> [ ':' <DataType> ] [ 'AS' <InitialValue> ]
        ```
    * **Semantics:** `DECLARE` or `VAR` creates a new, mutable, lexically-scoped variable. If no initial value is provided, a type-appropriate default is used (e.g., `0`, `FALSE`, `""`).

* **Module/Namespace System**
    * **Purpose:** To provide hierarchical organization for large specifications, preventing naming conflicts.
    * **EBNF Syntax:**
        ```ebnf
        ModuleDefinition ::= 'MODULE' <ModuleName> <Block> 'END MODULE'
        ```
    * **Semantics:** Defines a named scope. Identifiers within a module can be accessed from outside using qualified names (e.g., `ModuleName.function_name`).

* **Primitive Data Types**
    * **Purpose:** To provide fundamental representations for all information.
    * **EBNF Syntax:**
        ```ebnf
        DataType ::= 'BOOLEAN' | 'INTEGER' | 'FLOAT' | 'STRING' | <SchemaID> | <Identifier>
        Literal ::= 'TRUE' | 'FALSE' | <IntegerLiteral> | <FloatLiteral> | <StringLiteral>
        ```
    * **Semantics:** Defines built-in types for boolean logic, whole numbers, floating-point numbers, and character sequences. Complex types are defined via `DATA_TYPE_SCHEMA`.

* **Entity Identity**
    * **Purpose:** To provide a universal mechanism for addressing and referencing any distinct component, agent, or concept.
    * **EBNF Syntax:**
        ```ebnf
        EntityID ::= <Identifier>
        ```
    * **Semantics:** An `EntityID` is a unique identifier used to formally refer to subjects and objects in primitive calls, enabling precise relationships to be defined.

### **8. The 13 Atomic Core Primitives**

#### **Primitives at a Glance**

| Primitive | High-Level Purpose |
| :--- | :--- |
| `CONTEXT_RULE` | Establishes a formal context for reasoning (e.g., temporal, probabilistic). |
| `TEMPORAL_RELATION`| Asserts a time-based ordering between two events or entities. |
| `RESOURCE_BOUND` | Declares a quantifiable limit on a resource like memory or CPU. |
| `ENVIRONMENT_INTERFACE_POINT`| Defines a boundary for interaction with the external world (e.g., a sensor). |
| `DATA_TYPE_SCHEMA` | Defines a new, custom, structured data type. |
| `STATE_TRANSITION`| Specifies an atomic, conditional change in an entity's state. |
| `TRUST_ELEMENT` | Makes a verifiable claim about an entity (e.g., identity, authorization). |
| `GOVERNANCE_RULE`| Defines a normative policy (obligation, permission, prohibition). |
| `SELF_REFERENCE_POINT`| Creates an addressable handle to the system's own definitions for introspection. |
| `MUTATION_RULE` | Defines a formal, governed rule for how the system can modify itself. |
| `PERCEPTION_MAP` | Transforms raw environmental data into structured internal concepts. |
| `LEARNING_AXIOM` | Defines the formal contract for a learning process (inputs, goals, constraints). |
| `META_DEFINITION_RULE` | Defines how to formally extend the language's own core concepts. |

---
#### **Detailed Primitive Definitions**

* **CONTEXT\_RULE**
    * **Purpose:** Defines a formal context for reasoning, specifying its modalities (e.g., temporal, probabilistic) and tolerance for inconsistency.
    * **EBNF Syntax:** `CONTEXT_RULE <ContextID> ':' 'MODALITY' '{' <ModalityType> { ',' <ModalityType> } '}' [ 'INCOHERENCE_TOLERANCE' <Expression> ]`
    * **Semantics:** Establishes a named boundary that dictates how subsequent statements are interpreted, including the paradigm of reasoning (e.g., `Temporal`, `Probabilistic`, `Normative`).

* **TEMPORAL\_RELATION**
    * **Purpose:** Defines a fundamental temporal ordering or relationship (e.g., `BEFORE`, `AFTER`, `OVERLAPS`) between two entities or events.
    * **EBNF Syntax:** `TEMPORAL_RELATION <RelationID> ':' 'SUBJECT_A' <EntityID> ',' 'SUBJECT_B' <EntityID> ',' 'TYPE' <TemporalRelationTypeID> [ 'INTERVAL_A' <IntervalDefinitionID> ] [ 'INTERVAL_B' <IntervalDefinitionID> ]`
    * **Semantics:** Asserts a specific temporal relationship, which is crucial for defining causality, planning, and real-time system behavior.

* **RESOURCE\_BOUND**
    * **Purpose:** Declares a formal, quantifiable limit on a resource (e.g., memory, CPU cycles, API calls) associated with an entity.
    * **EBNF Syntax:** `RESOURCE_BOUND <BoundID> ':' 'SUBJECT' <EntityID> ',' 'TYPE' <ResourceTypeID> ',' 'METRIC' <MetricID> ',' 'THRESHOLD' <NumericExpression> ',' 'VIOLATION_POLICY' <PolicyID>`
    * **Semantics:** Enforces scarcity and capacity constraints. If the `THRESHOLD` is crossed, the specified `VIOLATION_POLICY` is invoked.

* **ENVIRONMENT\_INTERFACE\_POINT**
    * **Purpose:** Defines an atomic point of interaction (e.g., a sensor, an actuator, a network socket) between a system entity and an external entity.
    * **EBNF Syntax:** `ENVIRONMENT_INTERFACE_POINT <InterfaceID> ':' 'SUBJECT' <EntityID> ',' 'EXTERNAL_REFERENT' <EntityID> ',' 'INTERACTION_TYPE' <InteractionTypeID> ',' 'DATA_SCHEMA' <SchemaID> [ 'UNCERTAINTY_MODEL' <ModelID> ]`
    * **Semantics:** Specifies how a system senses, acts upon, or communicates with its environment, defining the data format and interaction type.

* **DATA\_TYPE\_SCHEMA**
    * **Purpose:** Provides the formal schema for defining new, structured data types and their intrinsic semantic properties (e.g., `PII`).
    * **EBNF Syntax:** `DATA_TYPE_SCHEMA <SchemaID> ':' 'DEFINITION' <SchemaDefinition> [ 'SEMANTIC_PROPERTIES' '{' <PropertyID> { ',' <PropertyID> } '}' ]`
    * **Semantics:** Defines a reusable, named data structure, analogous to a `struct` or `record`, allowing for the creation of complex information and knowledge models.

* **STATE\_TRANSITION**
    * **Purpose:** Defines an atomic, conditional change in the state of an entity.
    * **EBNF Syntax:** `STATE_TRANSITION <TransitionID> ':' 'SUBJECT' <EntityID> ',' 'PRECONDITION' <BooleanExpression> ',' 'POSTCONDITION' <BooleanExpression> ',' 'ACTION' <ActionID> [ 'REVERSION_PROTOCOL' <ProtocolID> ]`
    * **Semantics:** Describes a state change by specifying the `PRECONDITION` that must hold, the `ACTION` to be performed, and the `POSTCONDITION` that will hold after the action.

* **TRUST\_ELEMENT**
    * **Purpose:** Defines an atomic, verifiable assertion about one entity's relationship to or property concerning another.
    * **EBNF Syntax:** `TRUST_ELEMENT <ElementID> ':' 'SUBJECT' <EntityID> ',' 'PREDICATE' <BooleanExpression> ',' 'OBJECT' <EntityID> [ 'PROOF_PROTOCOL' <ProtocolID> ]`
    * **Semantics:** States a verifiable claim (e.g., identity, authorization, data integrity) and specifies the `PROOF_PROTOCOL` (e.g., `DigitalSignature`, `OAuth2`) required to validate it.

* **GOVERNANCE\_RULE**
    * **Purpose:** Defines an atomic normative statement (obligation, permission, prohibition) that governs system behavior.
    * **EBNF Syntax:** `GOVERNANCE_RULE <RuleID> ':' 'SCOPE' <ScopeID> ',' 'PREDICATE' <BooleanExpression> ',' 'ENFORCEMENT_CONTEXT' <ContextID> [ 'PRIORITY' <NumericExpression> ]`
    * **Semantics:** Specifies a policy that applies within a given `SCOPE`. If its `PREDICATE` evaluates to true, the rule is enforced according to its `ENFORCEMENT_CONTEXT` (e.g., `LogOnly`, `PreventAction`).

* **SELF\_REFERENCE\_POINT**
    * **Purpose:** Defines a formal, addressable point within the system's own definition (e.g., its grammar, schemas, or rules) for introspection or modification.
    * **EBNF Syntax:** `SELF_REFERENCE_POINT <PointID> ':' 'TARGET_TYPE' <TargetTypeID> ',' 'ACCESS_PROTOCOL' <ProtocolID>`
    * **Semantics:** Creates a named handle to a meta-level element, enabling the system to reason about its own structure and behavior.

* **MUTATION\_RULE**
    * **Purpose:** Defines an atomic rule for the system to formally and safely modify itself.
    * **EBNF Syntax:** `MUTATION_RULE <RuleID> ':' 'TARGET_REFERENCE' <SelfReferencePointID> ',' 'CONDITION' <BooleanExpression> ',' 'TRANSFORM_ACTION' <ActionID> [ 'APPROVAL_POLICY' <PolicyID> ]`
    * **Semantics:** Enables dynamic adaptation and self-repair by specifying a `CONDITION` under which a `TRANSFORM_ACTION` can be applied to a `TARGET_REFERENCE` (a `SELF_REFERENCE_POINT`), governed by an `APPROVAL_POLICY`.

* **PERCEPTION\_MAP**
    * **Purpose:** Defines the transformation from raw input received via an `ENVIRONMENT_INTERFACE_POINT` into structured, meaningful internal concepts.
    * **EBNF Syntax:** `PERCEPTION_MAP <MapID> ':' 'INPUT_INTERFACE' <InterfaceID> ',' 'OUTPUT_SCHEMA' <DataSchemaID> ',' 'TRANSFORMATION_FUNCTION' <ActionID> [ 'UNCERTAINTY_MODEL' <ModelID> ]`
    * **Semantics:** Bridges the gap between raw environmental data and the system's internal knowledge representation by applying a `TRANSFORMATION_FUNCTION` to map input to a structured `OUTPUT_SCHEMA`.

* **LEARNING\_AXIOM**
    * **Purpose:** Defines the formal contract for a learning process, specifying its inputs, outputs, objectives, constraints, and how it updates knowledge.
    * **EBNF Syntax:** `LEARNING_AXIOM <AxiomID> ':' 'INPUT_SCHEMA' <DataSchemaID> ',' 'OUTPUT_SCHEMA' <DataSchemaID> ',' 'OBJECTIVE_METRIC' <MetricID> ',' 'CONSTRAINT_SET' '{' <ResourceBoundID> { ',' <ResourceBoundID> } '}' ',' 'KNOWLEDGE_UPDATE_RULE' <RuleID>`
    * **Semantics:** Specifies a learning task by defining its data schemas, the `OBJECTIVE_METRIC` to optimize, the `CONSTRAINT_SET` it must operate within, and the `KNOWLEDGE_UPDATE_RULE` (a `STATE_TRANSITION` or `MUTATION_RULE`) used to integrate what it has learned.

* **META\_DEFINITION\_RULE**
    * **Purpose:** Enables the extension of Omega-Code's own meta-level vocabulary, such as defining new types of resources, modalities, or interactions.
    * **EBNF Syntax:** `META_DEFINITION_RULE <RuleID> ':' 'TARGET_TYPE' <TargetTypeID> ',' 'DEFINITION_SCHEMA' <DataSchemaID> ',' 'VALIDATION_PROTOCOL' <ProtocolID>`
    * **Semantics:** Provides a mechanism to formally extend the language's core concepts, ensuring that Omega-Code is future-proof and can adapt to new technological or conceptual paradigms.

### **9. Extensibility via META\_DEFINITION\_RULE**

The `META_DEFINITION_RULE` is the ultimate primitive for future-proofing Omega-Code. It allows designers to extend the fundamental vocabulary of the language itself in a formal, verifiable manner.

* **Purpose:** Instead of hardcoding all possible concepts like `ResourceTypeID` or `ModalityType`, `META_DEFINITION_RULE` provides a formal mechanism to create new ones. This allows the language to adapt to unforeseen requirements without altering the core grammar or parser.
* **Function:** It defines a rule for creating new instances of a `TARGET_TYPE` (e.g., `ResourceTypeID`). The `DEFINITION_SCHEMA` specifies the structure that a new definition must have, and the `VALIDATION_PROTOCOL` ensures that any new definition is well-formed and compliant.
* **EBNF Syntax:**
    ```ebnf
    MetaDefinitionRuleCall ::= 'META_DEFINITION_RULE' <RuleID> ':' 'TARGET_TYPE' <TargetTypeID> ',' 'DEFINITION_SCHEMA' <SchemaDefinition> ',' 'VALIDATION_PROTOCOL' <ProtocolID>
    ```

### **10. Common Composition Patterns**

Primitives are designed to be composed to model complex behaviors.

* **Sensor-to-Action Feedback Loop:**
    1.  `ENVIRONMENT_INTERFACE_POINT`: Defines a raw sensor input.
    2.  `PERCEPTION_MAP`: Translates raw data from the interface into a structured internal concept.
    3.  `STATE_TRANSITION`: Uses the structured concept as a `PRECONDITION` to trigger a resulting `ACTION`.

* **Governed Self-Modification:**
    1.  `SELF_REFERENCE_POINT`: Creates a handle to an adaptable system parameter (e.g., a `RESOURCE_BOUND` threshold).
    2.  `GOVERNANCE_RULE`: Defines the policy that must be satisfied for any change to occur (e.g., requires human approval).
    3.  `MUTATION_RULE`: Defines the logic for adapting the parameter, but is constrained by the `APPROVAL_POLICY` which points to the governance rule.

* **Verifiable Learning Contract:**
    1.  `RESOURCE_BOUND`: Constrains the `CPU_Time` and `Memory` a learning process can consume.
    2.  `MUTATION_RULE`: Defines how the system's knowledge base is to be updated based on learning.
    3.  `LEARNING_AXIOM`: Composes the above, defining the learning task's objective while operating within the `CONSTRAINT_SET` and using the specified `KNOWLEDGE_UPDATE_RULE`.

### **11. Reserved Words & Keywords**

The following words are reserved and cannot be used as identifiers.

```
ACCESS_PROTOCOL         ACTION                  AND                     APPROVAL_POLICY
AS                      ASSIGN                  BOOLEAN                 BREAK
CONDITION               CONSTRAINT_SET          CONTEXT_RULE            CONTINUE
DATA_SCHEMA             DATA_TYPE_SCHEMA        DECLARE                 DEFINITION
DEFINITION_SCHEMA       ELSE                    END FUNCTION            END IF
END LOOP                END MODULE              ENFORCEMENT_CONTEXT     ENVIRONMENT_INTERFACE_POINT
EXTERNAL_REFERENT       FALSE                   FIELD                   FLOAT
FOR                     FUNCTION                GOVERNANCE_RULE         IF
IN                      INCOHERENCE_TOLERANCE   INPUT_INTERFACE         INPUT_SCHEMA
INTEGER                 INTERACTION_TYPE        INTERVAL_A              INTERVAL_B
KNOWLEDGE_UPDATE_RULE   LEARNING_AXIOM          LOOP                    METRIC
META_DEFINITION_RULE    MODALITY                MODULE                  MUTATION_RULE
NOT                     OBJECT                  OBJECTIVE_METRIC        OR
OUTPUT_SCHEMA           PERCEPTION_MAP          POSTCONDITION           PRECONDITION
PREDICATE               PRIORITY                PROPERTY                PROOF_PROTOCOL
RESOURCE_BOUND          RETURN                  RETURNS                 REVERSION_PROTOCOL
SCOPE                   SELF_REFERENCE_POINT    SEMANTIC_PROPERTIES     STATE_TRANSITION
STRING                  SUBJECT                 SUBJECT_A               SUBJECT_B
TARGET_REFERENCE        TARGET_TYPE             TEMPORAL_RELATION       THEN
THRESHOLD               TO                      TRANSFORMATION_FUNCTION TRANSFORM_ACTION
TRUE                    TRUST_ELEMENT           TYPE                    UNCERTAINTY_MODEL
VALIDATION_PROTOCOL     VAR                     VIOLATION_POLICY        VOID
WHILE
```

### **12. Primitive Summary Table**

| Primitive Name | Purpose | Key Parameters | Semantic Ref |
| :--- | :--- | :--- | :--- |
| `CONTEXT_RULE`| Defines a formal reasoning context. | `Modality`, `IncoherenceTolerance` | §5.1.1 |
| `TEMPORAL_RELATION`| Asserts temporal order between entities. | `SubjectA`, `SubjectB`, `Type` | §5.1.2 |
| `RESOURCE_BOUND` | Declares a limit on a resource. | `Subject`, `Type`, `Metric`, `Threshold` | §5.1.3 |
| `ENVIRONMENT_INTERFACE_POINT`| Defines a system-environment boundary. | `Subject`, `ExternalReferent`, `InteractionType` | §5.1.4 |
| `DATA_TYPE_SCHEMA` | Defines a custom structured data type. | `Definition`, `SemanticProperties` | §5.2.1 |
| `STATE_TRANSITION`| Defines an atomic state change. | `Subject`, `Precondition`, `Postcondition`, `Action` | §5.2.2 |
| `TRUST_ELEMENT` | Makes a verifiable claim about an entity. | `Subject`, `Predicate`, `Object`, `ProofProtocol` | §5.2.3 |
| `GOVERNANCE_RULE`| Defines a normative policy. | `Scope`, `Predicate`, `EnforcementContext` | §5.3.1 |
| `SELF_REFERENCE_POINT`| Creates a handle to the system's own definition. | `TargetType`, `AccessProtocol` | §5.3.2 |
| `MUTATION_RULE` | Defines a rule for self-modification. | `TargetReference`, `Condition`, `TransformAction` | §5.3.3 |
| `PERCEPTION_MAP`| Maps raw input to internal concepts. | `InputInterface`, `OutputSchema`, `TransformationFunction`| §5.3.4 |
| `LEARNING_AXIOM`| Defines a formal contract for a learning process. | `InputSchema`, `ObjectiveMetric`, `KnowledgeUpdateRule`| §5.3.5 |
| `META_DEFINITION_RULE`| Defines how to extend the language's own concepts. | `TargetType`, `DefinitionSchema`, `ValidationProtocol` | §5.3.6 |

---

### **13. Appendix A: Full EBNF Grammar**

(* This grammar is a verbatim copy from Technical Specifications v1.4, Section 2.2 *)
```ebnf
(* Top-level Structure *)
OmegaCode ::= { ModuleDefinition | Statement | Comment }

(* Module Definition *)
ModuleDefinition ::= 'MODULE' <ModuleName> <Block> 'END MODULE'
ModuleName ::= <Identifier>

(* Block Structure: A sequence of statements or comments *)
Block ::= { Statement | Comment }

(* Statements can be simple or compound. Comments can appear anywhere. *)
Statement ::= SimpleStatement ';'
            | CompoundStatement
            | PrimitiveCall ';' (* Primitive calls are standalone statements *)

SimpleStatement ::= Assignment
                  | ReturnStatement
                  | FunctionCall
                  | ActionCall (* For inherent operations like LOG, INCREMENT *)
                  | 'BREAK'
                  | 'CONTINUE'

CompoundStatement ::= IfStatement
                    | LoopStatement
                    | FunctionDefinition
                    | VariableDeclaration (* Variable declarations can be top-level statements *)

Assignment ::= <VariableName> 'ASSIGN' <Expression>
ReturnStatement ::= 'RETURN' [ <Expression> ]

(* Control Flow *)
IfStatement ::= 'IF' <BooleanExpression> 'THEN' <Block> [ 'ELSE' <Block> ] 'END IF'
LoopStatement ::= 'LOOP' ( 'WHILE' <BooleanExpression> | 'FOR' <VariableName> 'IN' <Range> ) <Block> 'END LOOP'
Range ::= <Expression> 'TO' <Expression> | <Identifier> (* e.g., '1 TO 10', 'list_of_items' *)

(* Function Definition *)
FunctionDefinition ::= 'FUNCTION' <FunctionName> '(' [ <ParameterList> ] ')' [ 'RETURNS' <ReturnType> ] <Block> 'END FUNCTION'
FunctionName ::= <Identifier>
ParameterList ::= <Parameter> { ',' <Parameter> }
Parameter ::= <ParameterName> ':' <DataType>
ParameterName ::= <Identifier>
ReturnType ::= <DataType> | 'VOID'

(* Variable Declaration *)
VariableDeclaration ::= ( 'DECLARE' | 'VAR' ) <VariableName> [ ':' <DataType> ] [ 'AS' <InitialValue> ]
VariableName ::= <Identifier>
InitialValue ::= <Expression>

(* Primitive Data Types and Expressions *)
DataType ::= 'BOOLEAN' | 'INTEGER' | 'FLOAT' | 'STRING' | <SchemaID> | <Identifier> (* for user-defined types *)
Expression ::= <Literal> | <VariableName> | <FunctionCall> | <OperatorExpression>
Literal ::= 'TRUE' | 'FALSE' | <IntegerLiteral> | <FloatLiteral> | <StringLiteral>
IntegerLiteral ::= <Digit> { <Digit> }
FloatLiteral ::= <IntegerLiteral> '.' <IntegerLiteral>
StringLiteral ::= '"' { <CharInString> } '"' (* Changed to CharInString *)
Char ::= (* any Unicode character *)
Digit ::= '0' | '1' | '2' | '3' | '4' | '5' | '6' | '7' | '8' | '9'
Letter ::= 'a' | ... | 'z' | 'A' | ... | 'Z'
Identifier ::= <Letter> { <Letter> | <Digit> | '_' }

OperatorExpression ::= <Operand> <Operator> <Operand> | <UnaryOperator> <Operand>
Operand ::= <Expression> | '(' <Expression> ')'
Operator ::= '+' | '-' | '*' | '/' | '==' | '!=' | '<' | '>' | '<=' | '>=' | 'AND' | 'OR' | 'NOT'
UnaryOperator ::= 'NOT' | '-'

FunctionCall ::= <FunctionName> '(' [ <ArgumentList> ] ')'
ArgumentList ::= <Expression> { ',' <Expression> }

ActionCall ::= <ActionID> '(' [ <ArgumentList> ] ')' (* For inherent operations like LOG, INCREMENT *)

(* Boolean Expressions (for Conditions and Predicates) *)
BooleanExpression ::= <Expression> ( '==' | '!=' | '<' | '>' | '<=' | '>=' ) <Expression>
                    | 'NOT' <BooleanExpression>
                    | <BooleanExpression> 'AND' <BooleanExpression>
                    | <BooleanExpression> 'OR' <BooleanExpression>
                    | '(' <BooleanExpression> ')'
                    | <FunctionCall> (* if function returns BOOLEAN *)

(* Numeric Expressions (for Quantities and Priorities) *)
NumericExpression ::= <IntegerLiteral> | <FloatLiteral>
                    | <VariableName> (* resolves to numeric type *)
                    | '(' <NumericExpression> ')'
                    | <NumericExpression> <ArithmeticOperator> <NumericExpression>
                    | <UnaryNumericOperator> <NumericExpression>
ArithmeticOperator ::= '+' | '-' | '*' | '/'
UnaryNumericOperator ::= '-'

(* Characters for specific contexts *)
CharInString ::= (* any Unicode character except '"' *)
CharInComment ::= (* any Unicode character except newline, or '*' followed by ')' for BlockComment *)

(* Comments *)
Comment ::= BlockComment | LineComment
BlockComment ::= '(*' { <CharInComment> } '*)'
LineComment ::= '--' { <CharInComment> } <Newline>
Newline ::= '\n' | '\r\n' | '\r'

(* Identifiers for Primitives and Entities *)
ContextID ::= <Identifier>
EntityID ::= <Identifier>
TemporalRelationTypeID ::= <Identifier>
IntervalDefinitionID ::= <Identifier>
BoundID ::= <Identifier>
ResourceTypeID ::= <Identifier>
MetricID ::= <Identifier>
PolicyID ::= <Identifier>
InterfaceID ::= <Identifier>
InteractionTypeID ::= <Identifier>
SchemaID ::= <Identifier>
ActionID ::= <Identifier> (* Named inherent language operation *)
ProtocolID ::= <Identifier>
RuleID ::= <Identifier>
ScopeID ::= <Identifier>
Value ::= <NumericExpression> (* for Priority and other simple values where numeric is expected *)
PointID ::= <Identifier>
TargetTypeID ::= <Identifier>
SelfReferencePointID ::= <Identifier>
TransformAction ::= <ActionID> (* Refers to a named action for mutation *)
ModelID ::= <Identifier> (* for UncertaintyModel *)
PropertyID ::= <Identifier>
TransitionID ::= <Identifier>
ElementID ::= <Identifier>
MapID ::= <Identifier>
AxiomID ::= <Identifier>

(* Revised Schema Definition: defines fields within a data type schema *)
SchemaDefinition ::= '(' { FieldDefinition } ')'
FieldDefinition ::= ( 'VAR' | 'FIELD' | 'PROPERTY' ) <FieldName> ':' <DataType> [ 'AS' <InitialValue> ] ';'
FieldName ::= <Identifier>
Quantity ::= <NumericExpression> (* for Threshold *)


(* Primitive Calls - Detailed in Section 5 *)
PrimitiveCall ::= ContextRuleCall
                | TemporalRelationCall
                | ResourceBoundCall
                | EnvironmentInterfacePointCall
                | DataTypeSchemaCall
                | StateTransitionCall
                | TrustElementCall
                | GovernanceRuleCall
                | SelfReferencePointCall
                | MutationRuleCall
                | PerceptionMapCall
                | LearningAxiomCall
                | MetaDefinitionRuleCall


ContextRuleCall ::= 'CONTEXT_RULE' <ContextID> ':' 'MODALITY' '{' <ModalityType> { ',' <ModalityType> } '}' [ 'INCOHERENCE_TOLERANCE' <Expression> ]
ModalityType ::= <Identifier>

TemporalRelationCall ::= 'TEMPORAL_RELATION' <RelationID> ':' 'SUBJECT_A' <EntityID> ',' 'SUBJECT_B' <EntityID> ',' 'TYPE' <TemporalRelationTypeID> [ 'INTERVAL_A' <IntervalDefinitionID> ] [ 'INTERVAL_B' <IntervalDefinitionID> ]

ResourceBoundCall ::= 'RESOURCE_BOUND' <BoundID> ':' 'SUBJECT' <EntityID> ',' 'TYPE' <ResourceTypeID> ',' 'METRIC' <MetricID> ',' 'THRESHOLD' <NumericExpression> ',' 'VIOLATION_POLICY' <PolicyID>

EnvironmentInterfacePointCall ::= 'ENVIRONMENT_INTERFACE_POINT' <InterfaceID> ':' 'SUBJECT' <EntityID> ',' 'EXTERNAL_REFERENT' <EntityID> ',' 'INTERACTION_TYPE' <InteractionTypeID> ',' 'DATA_SCHEMA' <SchemaID> [ 'UNCERTAINTY_MODEL' <ModelID> ]

DataTypeSchemaCall ::= 'DATA_TYPE_SCHEMA' <SchemaID> ':' 'DEFINITION' <SchemaDefinition> [ 'SEMANTIC_PROPERTIES' '{' <PropertyID> { ',' <PropertyID> } '}' ]

StateTransitionCall ::= 'STATE_TRANSITION' <TransitionID> ':' 'SUBJECT' <EntityID> ',' 'PRECONDITION' <BooleanExpression> ',' 'POSTCONDITION' <BooleanExpression> ',' 'ACTION' <ActionID> [ 'REVERSION_PROTOCOL' <ProtocolID> ]

TrustElementCall ::= 'TRUST_ELEMENT' <ElementID> ':' 'SUBJECT' <EntityID> ',' 'PREDICATE' <BooleanExpression> ',' 'OBJECT' <EntityID> [ 'PROOF_PROTOCOL' <ProtocolID> ]

GovernanceRuleCall ::= 'GOVERNANCE_RULE' <RuleID> ':' 'SCOPE' <ScopeID> ',' 'PREDICATE' <BooleanExpression> ',' 'ENFORCEMENT_CONTEXT' <ContextID> [ 'PRIORITY' <NumericExpression> ]

SelfReferencePointCall ::= 'SELF_REFERENCE_POINT' <PointID> ':' 'TARGET_TYPE' <TargetTypeID> ',' 'ACCESS_PROTOCOL' <ProtocolID>

MutationRuleCall ::= 'MUTATION_RULE' <RuleID> ':' 'TARGET_REFERENCE' <SelfReferencePointID> ',' 'CONDITION' <BooleanExpression> ',' 'TRANSFORM_ACTION' <ActionID> [ 'APPROVAL_POLICY' <PolicyID> ]

PerceptionMapCall ::= 'PERCEPTION_MAP' <MapID> ':' 'INPUT_INTERFACE' <InterfaceID> ',' 'OUTPUT_SCHEMA' <SchemaID> ',' 'TRANSFORMATION_FUNCTION' <ActionID> [ 'UNCERTAINTY_MODEL' <ModelID> ]

LearningAxiomCall ::= 'LEARNING_AXIOM' <AxiomID> ':' 'INPUT_SCHEMA' <SchemaID> ',' 'OUTPUT_SCHEMA' <SchemaID> ',' 'OBJECTIVE_METRIC' <MetricID> ',' 'CONSTRAINT_SET' '{' <ResourceBoundID> { ',' <ResourceBoundID> } '}' ',' 'KNOWLEDGE_UPDATE_RULE' <RuleID>

MetaDefinitionRuleCall ::= 'META_DEFINITION_RULE' <RuleID> ':' 'TARGET_TYPE' <TargetTypeID> ',' 'DEFINITION_SCHEMA' <SchemaDefinition> ',' 'VALIDATION_PROTOCOL' <ProtocolID>
```

### **14. Illustrative Examples**

This section provides simple, focused examples for individual language constructs.

**Example: Function and Loop**
```omega
MODULE CounterExample
    FUNCTION check_status(id: INTEGER) RETURNS BOOLEAN
        -- Imagine complex logic here...
        RETURN id < 10;
    END FUNCTION;

    LOOP FOR i IN 1 TO 5
        IF check_status(i) == TRUE THEN
            -- ActionCall to an inherent operation
            LOG_ACTION("Status OK");
        END IF;
    END LOOP;
END MODULE;
```

**Example: DATA_TYPE_SCHEMA**
```omega
-- Defines a structured record for a sensor reading.
DATA_TYPE_SCHEMA SensorReading:
    DEFINITION (
        VAR sensor_id: STRING;
        VAR value: FLOAT;
        VAR unit: STRING AS "Kelvin";
    )
    SEMANTIC_PROPERTIES { TelemetryData };
;
```

**Example: RESOURCE_BOUND**
```omega
-- Limits an agent's API call rate.
RESOURCE_BOUND LlmApiRateLimit:
    SUBJECT LlmAgent_01,
    TYPE ApiCalls,
    METRIC CallsPerMinute,
    THRESHOLD 100,
    VIOLATION_POLICY ThrottleRequestsPolicy;
;
```

**Example: STATE_TRANSITION**
```omega
-- Describes the atomic action of promoting a user account.
STATE_TRANSITION PromoteUser:
    SUBJECT User_Acct_1138,
    PRECONDITION (UserHasTrialStatus(User_Acct_1138) AND PaymentIsConfirmed()),
    POSTCONDITION (UserHasPremiumStatus(User_Acct_1138)),
    ACTION UpdateUserAccountType;
;
```

**Example: GOVERNANCE_RULE**
```omega
-- Enforces a policy that PII data cannot be deleted without consent.
GOVERNANCE_RULE DataDeletionPolicy:
    SCOPE UserDataManagement,
    PREDICATE (ActionIsDelete(target) AND TargetHasPii(target) AND NOT ConsentGiven(target)),
    ENFORCEMENT_CONTEXT PreventActionAndAudit,
    PRIORITY 999;
;
```

### **15. Appendix B: Parser Validation Test Suite**

#### **Valid Test Snippets**

These snippets should be successfully parsed.

**Snippet 1: Minimal Module Definition**
```omega
MODULE EmptyModule
    -- This is an empty module block
END MODULE;
```

**Snippet 2: Full Primitive Call with Optional Fields**
```omega
TEMPORAL_RELATION FullRelationExample:
    SUBJECT_A Event_A,
    SUBJECT_B Event_B,
    TYPE OVERLAPS,
    INTERVAL_A Interval_One,
    INTERVAL_B Interval_Two;
;
```

**Snippet 3: Nested Control Flow**
```omega
LOOP FOR i IN 1 TO 5
    IF i > 2 THEN
        BREAK;
    ELSE
        CONTINUE;
    END IF;
END LOOP;
```

#### **Invalid (Negative) Test Snippets**

These snippets should be rejected by the parser.

**Snippet 1: Missing Semicolon**
```omega
VAR x: INTEGER AS 5 --<-- Missing semicolon
VAR y: INTEGER AS 10;
```
*Reason for Invalidity:* The `VariableDeclaration` is a `SimpleStatement` and requires a terminating semicolon (`;`).

**Snippet 2: Incorrect Keyword Order in Primitive**
```omega
RESOURCE_BOUND BadOrder:
    SUBJECT MyProcess,
    THRESHOLD 512,  --<-- THRESHOLD appears before TYPE and METRIC
    TYPE Memory,
    METRIC Megabytes,
    VIOLATION_POLICY Halt;
;
```
*Reason for Invalidity:* The `ResourceBoundCall` rule specifies a strict order for its parameters (`SUBJECT`, `TYPE`, `METRIC`, `THRESHOLD`, `VIOLATION_POLICY`).

**Snippet 3: Unmatched Block Terminator**
```omega
IF TRUE THEN
    VAR a: BOOLEAN AS FALSE;
END LOOP; --<-- Incorrect terminator. Should be END IF.
```
*Reason for Invalidity:* An `IfStatement` must be terminated with `END IF`, not `END LOOP`.

**Snippet 4: Using Reserved Keyword as an Identifier**
```omega
VAR MODULE: STRING AS "MyData"; --<-- 'MODULE' is a reserved keyword.
```
*Reason for Invalidity:* `MODULE` is a reserved keyword and cannot be used as a `<VariableName>` identifier.
