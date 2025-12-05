Here is the updated comprehensive list, organized by subsystem. This will be the canonical inventory to drive the new `FIREBIRDOS_OVERVIEW.md` rewrite.

***

## FirebirdOS core & philosophy

FirebirdOS is the neuro‑symbolic “umbrella” that ties Axiom Lexicon, HopLogic, Omega‑Code, HFF/NSP, and the cognitive/AGI layer into a single operating system. It adds the intent‑centric “mind” layer, long‑horizon memory, and user‑facing trust philosophy that the lower layers don’t express by themselves.[1][2]

- Neuro‑symbolic operating system: positions the whole stack as an OS for reasoning, not a chatbot wrapper or RAG library.[1]
- Three‑layer architecture: LLM “Neural Intuition” layer, Omega formal specification layer, and HopLogic+Axiom execution layer.[1]
- Query / feedback / evolution flows: top‑down query execution, bottom‑up policy feedback, and governed self‑evolution loops.[1]
- Design‑by‑mind philosophy: treats the user’s intent and cognitive continuity as the primary design object, not just individual prompts.[2]
- Cognitive Kernel: a central controller that tracks intent threads, context, emotion, and which applets should be activated, without behaving like a hard control system.[2]
- Seven‑layer memory system: vector, episodic, semantic, affective, relationship‑aware, symbolic, and meta‑memory, each with distinct roles.[2]
- Temporal life of tasks: active vs. paused vs. dormant threads, with decay, resurfacing, and reprioritization rather than simple “open vs. closed” states.[2]
- TTD (Things‑To‑Do) layer: persistent awareness of user commitments across time and context, so the system remembers what matters without constant re‑prompting.[2]
- Relationship engine: background processes that detect dependencies between documents, plans, agreements, and surface cross‑impact when something changes.[2]
- Polite autonomy: default behavior is to suggest, ask, and propose options rather than silently acting or overriding the user.[2]
- Mirror Mode: a dry‑run mode that simulates actions, shows likely outcomes, and invites user approval before high‑impact operations.[2]
- Trust “commandments”: explicit principles around inspectability, provenance, local‑first data, and human override baked into the architecture.[2]
- File‑and‑process design: uses plain files, SQLite and timestamped executables instead of opaque daemons or hidden services, to keep everything legible and versionable.[2]
- OS‑style applets: tools are small, composable programs that FirebirdOS orchestrates, not a closed plugin marketplace.[2]
- Creative partner stance: optimized for long‑horizon creative work (books, films, research) where it acts as a thinking companion, not just a transactional assistant.[2]

***

## Axiom Lexicon (semantic substrate)

Axiom Lexicon is the system’s semantic bedrock, turning polysemous language into exact, machine‑checkable concepts with NSM grounding and hierarchical structure. It underlies disambiguation, VKG construction, policy grounding, and AGI‑facing perception and planning.[3][1]

- Meaning‑exact representation: every sense gets a unique `meaning_id`, eliminating ambiguity like “bank” (river edge vs. financial institution).[3]
- Verifiable semantic substrate: designed as a logic‑ready concept layer, not a plain dictionary or synonym list.[3]
- Four‑phase construction pipeline: ingestion/staging, enrichment/indexing, hierarchical construction, and validation/governance with explicit quality gates.[3]
- Deterministic ingestion: merges WordNet, Wiktionary, and domain glossaries into a single staged lexicon DB via embeddings and an adjudicator LLM.[3]
- Canonical ID assignment: assigns stable `meaning_id`s plus human‑readable glosses and NSM explications, then indexes them in a vector store.[3]
- DAG hierarchy: builds a directed acyclic parent graph for all senses, validated via topological sorting to prevent cycles.[3]
- Concept blueprints: each sense stores lemma, POS, gloss, NSM explication, parents, semantic role frames, confidence, and level.[3]
- NSM grounding: definitions expressed in a small set of semantic primes so concepts are decomposed into logically manipulable primitives.[3]
- Lexicon coverage gate: documents are checked for coverage; unknown terms are routed to a Cognitive Bootstrap Engine for new provisional senses.[3]
- Fact grounding: ingestion maps extracted facts to `meaning_id`s and validates role frames against the lexicon.[4][3]
- Policy grounding: Omega governance rules reference `meaning_id`s directly, so policies apply to exact concepts rather than raw strings.[5][3]
- AGI integration: perception and planning layers query the lexicon for sense‑specific objects and alternate predicates, and gap‑detection drives lifelong learning.[3]
- Tiered coverage roadmap: phases from ~1k core senses to 10k+ domain senses, with explicit coverage and confidence targets.[3]

***

## HopLogic VKG & RAG engine

HopLogic is the knowledge engine and “corporate brain” that turns text into a verifiable knowledge graph, enforces isolation, and runs hallucination‑resistant RAG and reasoning. It is built as a set of deterministic pipelines rather than a monolithic black box.[4][1]

- Hybrid AI knowledge engine: transforms unstructured text into a Verifiable Knowledge Graph for use as a machine‑readable corporate brain.[4]
- OS‑for‑trustworthy‑AI posture: provided as CLI tools and pipelines that can be composed into larger workflows, especially for regulated domains.[4]
- Semantic ambiguity fix: grounds every token through Axiom Lexicon so ingestion and retrieval operate on `meaning_id`s, not fuzzy embeddings.[4]
- Viewpoint registry: POV framework that distinguishes proven facts from reported claims and attaches each statement to a specific speaker/source.[4]
- Conflict preservation: stores contradictory claims side‑by‑side instead of merging them into a single “average” fact.[4]
- Data isolation via per‑project VKGs: physically separate graphs per client/matter/project, preventing cross‑contamination like “two John Smiths.”[4]
- Hub‑and‑spoke fact model: represents each event as a dense hub node with typed semantic role edges, avoiding ontology explosion.[1][4]
- Knowledge ingestion pipeline: a multi‑stage process with lexicon coverage gate, fact extraction, synapse transformation, and graph loading.[4]
- Ingestion & Distillation Engine (IDE): converts prose into atomic, fully specified facts by resolving pronouns and vague references.[4]
- Synapse structures: intermediate representation that binds a predicate `meaning_id`, semantic roles, and rich provenance in a portable format.[4]
- Idempotent graph loading: generated Cypher uses `MERGE` to construct deterministic VKGs in Neo4j or Kùzu.[4]
- Verifiable Knowledge Graph: fact nodes store predicate IDs, roles, full provenance (document, page, span) for auditability.[4]
- RAG & query pipeline: separates query disambiguation, adaptive retrieval strategy, and grounded LLM synthesis under strict rules.[4]
- Query disambiguation (QID): grounds user questions into `meaning_id`s before retrieval, so search is by intended sense.[4]
- Adaptive retrieval tiers: chooses from single‑fact, local multi‑hop, or abstract definitional chains depending on question type.[4]
- Golden Rule prompting: instructs LLMs to answer only from supplied VKG facts and to return supporting fact IDs.[4]
- Deterministic, auditable pipelines: same inputs always yield the same graph, and every edge can be traced back to original text.[4]
- Tight coupling to Axiom Lexicon: uses lexicon for WSD, semantic roles, and hierarchy‑aware retrieval.[1][4]

***

## Omega‑Code governance layer

Omega‑Code is the formal governance and specification layer that defines how the system may behave, how it learns, and how it can safely change itself. It provides a small set of primitives with EBNF‑defined syntax that can be verified, audited, and reasoned about.[5][1]

- Formal pseudocode meta‑language: machine‑readable specification for governance, safety, and self‑modification, not just prompts or prose policy docs.[5]
- EBNF‑defined grammar: syntactic rules that make Omega programs parseable and suitable for tooling and verification.[5]
- Governance‑layer role: answers “what should we do with what’s true?” while HopLogic answers “what is true?”.[5]
- Deterministic policies: rules express obligations, permissions, and prohibitions in a way that is not probabilistic or heuristic.[5]
- Full auditability: each decision can be traced back to specific rules and their evaluations.[5]
- Verifiability: designed so that formal proofs of policy adherence and system properties are possible.[5]
- 13 atomic primitives: foundational building blocks for context, time, resources, data schemas, state, trust, governance, self‑reference, mutation, perception, learning, and meta‑definition.[5]
- Context rules: specify reasoning modes (temporal, probabilistic, ethical) and allowed inconsistency within that context.[5]
- Temporal relations: encode before/after/overlaps relationships between events as first‑class objects.[5]
- Resource bounds: declare hard consumption limits with attached violation handling.[5]
- Data type schemas: define structured data with semantic tags like PII or PHI.[5]
- State transitions: model atomic changes with preconditions, actions, and postconditions.[5]
- Trust elements: represent verifiable claims and associated proof protocols.[5]
- Governance rules: define enforceable policies with scope, predicate, enforcement context, priority, and audit requirements.[5]
- Self‑reference points: allow the system to refer to and inspect its own definitions and rules.[5]
- Mutation rules: specify when and how the system is permitted to alter its own specs, under explicit approval policies.[5]
- Perception maps: describe how raw sensor or external data becomes structured internal knowledge.[5]
- Learning axioms: encode the conditions and constraints under which learning processes may update knowledge.[5]
- Meta‑definition rules: provide a controlled way for Omega’s own vocabulary to evolve.[5]
- Real‑world templates: includes concrete HIPAA, cold‑chain, and trading‑risk rules that demonstrate structural enforcement (e.g., halting trades at fixed drawdown).[5]

***

## HFF/NSP protocol & cross‑stack semantics

HFF/NSP is the neuro‑symbolic protocol that standardizes how facts and observations are encoded, transmitted, and checked across machines, including edge devices with minimal resources. It closes the gap between symbolic knowledge, Omega policies, and machine‑to‑machine communication.[6][1]

- Hub‑and‑spoke fact instances: each complex event is a single hub node linked via a fixed set of semantic roles, compressing what would be many RDF triples.[6]
- Canonical verb and entity IDs: every predicate and participant uses Axiom `meaning_id`s, not ad‑hoc strings.[6]
- Explicit epistemic status: facts carry `povstatus` such as sensor data, claim, or proven fact, with confidence scores.[6]
- Rich provenance: fact instances include source document or sensor ID, page/span or timestamp, and other metadata.[6]
- NSP packet format: a compact, typed message structure for serializing fact instances with roles, temporal info, and signatures.[6]
- Semantic roles in packets: AGENT, PATIENT, LOCATION, TEMPORAL, THEME, and others are encoded as role entries with `targetmeaningid`.[6]
- Cryptographic signatures: packets include signatures to support zero‑trust validation across network boundaries.[6]
- Bandwidth efficiency: NSP reduces serialized fact size compared to verbose JSON while increasing semantic content.[6]
- M2M semantic resolution: receivers can interpret packets by looking up `meaning_id`s in a local lexicon cache, eliminating schema‑guessing.[6]
- Language‑independent semantics: systems in different human languages can interoperate by sharing canonical IDs instead of translated strings.[6]
- KG‑optional deployment: edge devices can send/receive NSP without hosting a full VKG; gateways and cloud nodes integrate with full graphs.[6]
- Tiered lexicon at the edge: small devices carry only a compact subset of the lexicon tuned to their domain.[6]
- Essence predicates: Axiom entries can include executable predicate lambdas that express capabilities and constraints (e.g., for “cargo truck”).[3][6]
- Predicate inheritance: concept‑level lambdas inherit behavior from parents (vehicle, container, etc.), supporting compositional reasoning.[6]
- Deterministic reasoning: Omega queries these lambdas to answer capability questions with logical truth values rather than neural guesses.[6][5]
- Two‑layer design (data vs. logic): HFF/NSP provides the “what is known” predicates, Omega encodes “what must be done” over those predicates.[6][5]
- Policy execution over facts: governance rules inspect NSP‑backed fact streams (e.g., delete actions on PHI) and enforce block/allow behavior.[6][5]
- Independent evolution: fact formats and policies can evolve separately while remaining interoperable via shared meaning IDs.[6][5]

***

If you want, the next step can be either:

- Turn this into a machine‑readable checklist (e.g., JSON or Markdown table) to use as a spec reference, or  
- Go straight to rewriting `FIREBIRDOS_OVERVIEW.md` using this list as the backbone for the structure and claims.

