# FirebirdOS Features

This comprehensive feature list is organized by subsystem and serves as the canonical inventory for FirebirdOS architecture and capabilities.

---

## FirebirdOS Core & Philosophy

FirebirdOS is the neuro-symbolic "umbrella" that ties Axiom Lexicon, HopLogic, Omega-Code, HFF/NSP, and the cognitive/AGI layer into a single operating system. It adds the intent-centric "mind" layer, long-horizon memory, and user-facing trust philosophy that the lower layers don't express by themselves.

### Architecture & Design
- **Neuro-symbolic operating system**: Positions the whole stack as an OS for reasoning, not a chatbot wrapper or RAG library
- **Three-layer architecture**: LLM "Neural Intuition" layer, Omega formal specification layer, and HopLogic+Axiom execution layer
- **Query/feedback/evolution flows**: Top-down query execution, bottom-up policy feedback, and governed self-evolution loops
- **Design-by-mind philosophy**: Treats the user's intent and cognitive continuity as the primary design object, not just individual prompts

### Memory & Context
- **Cognitive Kernel**: A central controller that tracks intent threads, context, emotion, and which applets should be activated, without behaving like a hard control system
- **Seven-layer memory system**: Vector, episodic, semantic, affective, relationship-aware, symbolic, and meta-memory, each with distinct roles
- **Temporal life of tasks**: Active vs. paused vs. dormant threads, with decay, resurfacing, and reprioritization rather than simple "open vs. closed" states
- **TTD (Things-To-Do) layer**: Persistent awareness of user commitments across time and context, so the system remembers what matters without constant re-prompting
- **Relationship engine**: Background processes that detect dependencies between documents, plans, agreements, and surface cross-impact when something changes

### Trust & Autonomy
- **Polite autonomy**: Default behavior is to suggest, ask, and propose options rather than silently acting or overriding the user
- **Mirror Mode**: A dry-run mode that simulates actions, shows likely outcomes, and invites user approval before high-impact operations
- **Trust "commandments"**: Explicit principles around inspectability, provenance, local-first data, and human override baked into the architecture
- **File-and-process design**: Uses plain files, SQLite and timestamped executables instead of opaque daemons or hidden services, to keep everything legible and versionable

### Integration & Usage
- **OS-style applets**: Tools are small, composable programs that FirebirdOS orchestrates, not a closed plugin marketplace
- **Creative partner stance**: Optimized for long-horizon creative work (books, films, research) where it acts as a thinking companion, not just a transactional assistant

---

## Axiom Lexicon (Semantic Substrate)

Axiom Lexicon is the system's semantic bedrock, turning polysemous language into exact, machine-checkable concepts with NSM grounding and hierarchical structure. It underlies disambiguation, VKG construction, policy grounding, and AGI-facing perception and planning.

### Core Capabilities
- **Meaning-exact representation**: Every sense gets a unique `meaning_id`, eliminating ambiguity like "bank" (river edge vs. financial institution)
- **Verifiable semantic substrate**: Designed as a logic-ready concept layer, not a plain dictionary or synonym list
- **DAG hierarchy**: Builds a directed acyclic parent graph for all senses, validated via topological sorting to prevent cycles
- **NSM grounding**: Definitions expressed in a small set of semantic primes so concepts are decomposed into logically manipulable primitives

### Construction Pipeline
- **Four-phase construction pipeline**: Ingestion/staging, enrichment/indexing, hierarchical construction, and validation/governance with explicit quality gates
- **Deterministic ingestion**: Merges WordNet, Wiktionary, and domain glossaries into a single staged lexicon DB via embeddings and an adjudicator LLM
- **Canonical ID assignment**: Assigns stable `meaning_id`s plus human-readable glosses and NSM explications, then indexes them in a vector store
- **Concept blueprints**: Each sense stores lemma, POS, gloss, NSM explication, parents, semantic role frames, confidence, and level

### Integration & Coverage
- **Lexicon coverage gate**: Documents are checked for coverage; unknown terms are routed to a Cognitive Bootstrap Engine for new provisional senses
- **Fact grounding**: Ingestion maps extracted facts to `meaning_id`s and validates role frames against the lexicon
- **Policy grounding**: Omega governance rules reference `meaning_id`s directly, so policies apply to exact concepts rather than raw strings
- **AGI integration**: Perception and planning layers query the lexicon for sense-specific objects and alternate predicates, and gap-detection drives lifelong learning
- **Tiered coverage roadmap**: Phases from ~1k core senses to 10k+ domain senses, with explicit coverage and confidence targets

---

## HopLogic VKG & RAG Engine

HopLogic is the knowledge engine and "corporate brain" that turns text into a verifiable knowledge graph, enforces isolation, and runs hallucination-resistant RAG and reasoning. It is built as a set of deterministic pipelines rather than a monolithic black box.

### Core Architecture
- **Hybrid AI knowledge engine**: Transforms unstructured text into a Verifiable Knowledge Graph for use as a machine-readable corporate brain
- **OS-for-trustworthy-AI posture**: Provided as CLI tools and pipelines that can be composed into larger workflows, especially for regulated domains
- **Hub-and-spoke fact model**: Represents each event as a dense hub node with typed semantic role edges, avoiding ontology explosion
- **Deterministic, auditable pipelines**: Same inputs always yield the same graph, and every edge can be traced back to original text

### Disambiguation & Isolation
- **Semantic ambiguity fix**: Grounds every token through Axiom Lexicon so ingestion and retrieval operate on `meaning_id`s, not fuzzy embeddings
- **Viewpoint registry**: POV framework that distinguishes proven facts from reported claims and attaches each statement to a specific speaker/source
- **Conflict preservation**: Stores contradictory claims side-by-side instead of merging them into a single "average" fact
- **Data isolation via per-project VKGs**: Physically separate graphs per client/matter/project, preventing cross-contamination like "two John Smiths"

### Knowledge Ingestion
- **Knowledge ingestion pipeline**: A multi-stage process with lexicon coverage gate, fact extraction, synapse transformation, and graph loading
- **Ingestion & Distillation Engine (IDE)**: Converts prose into atomic, fully specified facts by resolving pronouns and vague references
- **Synapse structures**: Intermediate representation that binds a predicate `meaning_id`, semantic roles, and rich provenance in a portable format
- **Idempotent graph loading**: Generated Cypher uses `MERGE` to construct deterministic VKGs in Neo4j or Kùzu
- **Verifiable Knowledge Graph**: Fact nodes store predicate IDs, roles, full provenance (document, page, span) for auditability

### RAG & Query
- **RAG & query pipeline**: Separates query disambiguation, adaptive retrieval strategy, and grounded LLM synthesis under strict rules
- **Query disambiguation (QID)**: Grounds user questions into `meaning_id`s before retrieval, so search is by intended sense
- **Adaptive retrieval tiers**: Chooses from single-fact, local multi-hop, or abstract definitional chains depending on question type
- **Golden Rule prompting**: Instructs LLMs to answer only from supplied VKG facts and to return supporting fact IDs
- **Tight coupling to Axiom Lexicon**: Uses lexicon for WSD, semantic roles, and hierarchy-aware retrieval

---

## Omega-Code Governance Layer

Omega-Code is the formal governance and specification layer that defines how the system may behave, how it learns, and how it can safely change itself. It provides a small set of primitives with EBNF-defined syntax that can be verified, audited, and reasoned about.

### Foundation
- **Formal pseudocode meta-language**: Machine-readable specification for governance, safety, and self-modification, not just prompts or prose policy docs
- **EBNF-defined grammar**: Syntactic rules that make Omega programs parseable and suitable for tooling and verification
- **Governance-layer role**: Answers "what should we do with what's true?" while HopLogic answers "what is true?"
- **Deterministic policies**: Rules express obligations, permissions, and prohibitions in a way that is not probabilistic or heuristic
- **Full auditability**: Each decision can be traced back to specific rules and their evaluations
- **Verifiability**: Designed so that formal proofs of policy adherence and system properties are possible

### Core Primitives (13 Atomic Types)
- **Context rules**: Specify reasoning modes (temporal, probabilistic, ethical) and allowed inconsistency within that context
- **Temporal relations**: Encode before/after/overlaps relationships between events as first-class objects
- **Resource bounds**: Declare hard consumption limits with attached violation handling
- **Data type schemas**: Define structured data with semantic tags like PII or PHI
- **State transitions**: Model atomic changes with preconditions, actions, and postconditions
- **Trust elements**: Represent verifiable claims and associated proof protocols
- **Governance rules**: Define enforceable policies with scope, predicate, enforcement context, priority, and audit requirements
- **Self-reference points**: Allow the system to refer to and inspect its own definitions and rules
- **Mutation rules**: Specify when and how the system is permitted to alter its own specs, under explicit approval policies
- **Perception maps**: Describe how raw sensor or external data becomes structured internal knowledge
- **Learning axioms**: Encode the conditions and constraints under which learning processes may update knowledge
- **Meta-definition rules**: Provide a controlled way for Omega's own vocabulary to evolve

### Real-World Application
- **Real-world templates**: Includes concrete HIPAA, cold-chain, and trading-risk rules that demonstrate structural enforcement (e.g., halting trades at fixed drawdown)

---

## HFF/NSP Protocol & Cross-Stack Semantics

HFF/NSP is the neuro-symbolic protocol that standardizes how facts and observations are encoded, transmitted, and checked across machines, including edge devices with minimal resources. It closes the gap between symbolic knowledge, Omega policies, and machine-to-machine communication.

### Fact Representation
- **Hub-and-spoke fact instances**: Each complex event is a single hub node linked via a fixed set of semantic roles, compressing what would be many RDF triples
- **Canonical verb and entity IDs**: Every predicate and participant uses Axiom `meaning_id`s, not ad-hoc strings
- **Explicit epistemic status**: Facts carry `povstatus` such as sensor data, claim, or proven fact, with confidence scores
- **Rich provenance**: Fact instances include source document or sensor ID, page/span or timestamp, and other metadata

### Protocol Design
- **NSP packet format**: A compact, typed message structure for serializing fact instances with roles, temporal info, and signatures
- **Semantic roles in packets**: AGENT, PATIENT, LOCATION, TEMPORAL, THEME, and others are encoded as role entries with `targetmeaningid`
- **Cryptographic signatures**: Packets include signatures to support zero-trust validation across network boundaries
- **Bandwidth efficiency**: NSP reduces serialized fact size compared to verbose JSON while increasing semantic content

### Cross-System Interoperability
- **M2M semantic resolution**: Receivers can interpret packets by looking up `meaning_id`s in a local lexicon cache, eliminating schema-guessing
- **Language-independent semantics**: Systems in different human languages can interoperate by sharing canonical IDs instead of translated strings
- **KG-optional deployment**: Edge devices can send/receive NSP without hosting a full VKG; gateways and cloud nodes integrate with full graphs
- **Tiered lexicon at the edge**: Small devices carry only a compact subset of the lexicon tuned to their domain

### Reasoning & Execution
- **Essence predicates**: Axiom entries can include executable predicate lambdas that express capabilities and constraints (e.g., for "cargo truck")
- **Predicate inheritance**: Concept-level lambdas inherit behavior from parents (vehicle, container, etc.), supporting compositional reasoning
- **Deterministic reasoning**: Omega queries these lambdas to answer capability questions with logical truth values rather than neural guesses

### Integration with Governance
- **Two-layer design (data vs. logic)**: HFF/NSP provides the "what is known" predicates, Omega encodes "what must be done" over those predicates
- **Policy execution over facts**: Governance rules inspect NSP-backed fact streams (e.g., delete actions on PHI) and enforce block/allow behavior
- **Independent evolution**: Fact formats and policies can evolve separately while remaining interoperable via shared meaning IDs

---

## Next Steps

This feature inventory can be used to:
- Generate machine-readable specification documents (JSON, YAML)
- Drive the rewrite of `FIREBIRDOS_OVERVIEW.md`
- Create detailed implementation roadmaps for each subsystem
- Establish testing and validation criteria for feature completeness
