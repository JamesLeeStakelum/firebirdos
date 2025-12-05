# AGI Cognitive Layers Overview

**Version:** 1.0  
**Last Updated:** December 4, 2025

---

## The FirebirdOS Semantic Kernel: Foundation Complete

The foundation of FirebirdOS is a **verifiable semantic kernel** that grounds language, stores memory, and enforces governance. This kernel is already specified and partially implemented:

- **Axiom Lexicon**: A hierarchical dictionary where every concept has a canonical `meaning_id`, NSM-based explication, and validated parent relations. This eliminates polysemy and provides stable semantics.
- **HopLogic (Verifiable Knowledge Graph)**: Transforms natural language into structured, citable fact hubs (HFF/NSP) stored in a dual-dimension knowledge graph. Every fact is traceable to source text and disambiguated by meaning.
- **Omega-Code Governance Layer**: Formal policies (GOVERNANCE_RULE, RESOURCE_BOUND, etc.) that enforce constraints, safety limits, and compliance—making hallucination structurally impossible.

This kernel answers **"What is true?"** (HopLogic) and **"What should we do?"** (Omega) deterministically, with full provenance.

---

## The Four Cognitive Layers: Path to AGI-Like Behavior

On top of this semantic kernel, four cognitive layers enable perception, planning, learning, and coordination. Each layer reads and writes HFF/NSP fact hubs to the shared knowledge graph.

### 1. Perception: Grounding the World

**What it is**: Converting raw sensory input (vision, audio, sensor data) into structured HFF facts in the knowledge graph—not just detecting objects, but grounding them to lexicon senses.

**Why it's needed**: AGI must interact with the physical and digital world beyond text. The "red door" in your command must map to actual `door_object_42` in a scene graph.

**How it connects to HopLogic**:
- Vision system detects objects, attributes, spatial relations
- Grounding module maps detections to axiom lexicon senses
- Writes perception events to KG with roles: `observer`, `perceived_object`, `attribute`, `location`
- Links perceptual facts to action plans (e.g., "open the red door")

**What you'd build**:
- Vision/audio modules using off-the-shelf models
- Grounding service that queries lexicon for matching senses and creates HFF perception events
- Scene graph in KG updated continuously

---

### 2. Robust Planning: Goals to Actions

**What it is**: Taking high-level goals expressed in HFF and decomposing them into executable, feasible action sequences—handling failures, replanning, and adaptation.

**Why it's needed**: Current LLMs propose plans but cannot verify feasibility or recover from failures. AGI needs: "Order pizza → check if vendor open, if payment valid, if address set → if not, ask or fix → if order fails, try alternate vendor."

**How it connects to HopLogic**:
- User goal arrives as HFF command: `ACHIEVE_GOAL: PIZZA_DELIVERED_TO_USER`
- Planner uses axiom lexicon to understand predicates (PIZZA, DELIVERY, ORDER) and their preconditions/effects
- Queries KG for user preferences, past orders, current state
- Generates HFF plan with steps: `VERIFY_PAYMENT`, `CALL_VENDOR_API`, `CONFIRM_ORDER`, `WAIT_DELIVERY`
- Governor checks plan against Omega rules before execution
- If step fails, planner writes failure event to KG, reasons over alternatives, proposes revised plan

**What you'd build**:
- Planner module (PDDL-style, HTN-style, or LLM-assisted with symbolic verification)
- Execution monitor that tracks progress, detects failures, triggers replanning
- All plans logged as HFF events in KG

---

### 3. Lifelong Learning: Continuous Improvement

**What it is**: The system continuously improving its knowledge, skills, and behavior from experience—not just memorizing, but discovering gaps, refining definitions, and self-correcting.

**Why it's needed**: Static knowledge bases become outdated. User preferences change. New domains/tools emerge. AGI must adapt without constant human retraining.

**How it connects to HopLogic**:
- **Learning from corrections**: User says "No, John is my colleague, not my boss" → updates `PERSON:john` node, changes relation type, logs correction with provenance
- **Pattern learning**: System notices "User always orders Thai food on Fridays" → creates preference fact hub `USER_PREFERENCE(user, food=THAI, day=FRIDAY, confidence=0.85)`
- **Lexicon gap detection**: Unknown word "sashimi" → flags gap, LLM proposes sense definition and parents, human reviews and adds to lexicon
- **Consistency checking**: Scans KG for contradictions (e.g., Person X is both ALIVE and DEAD), flags for review or auto-repair
- **Generalization**: Mines HFF events for regularities (e.g., after `LATE_MEETING`, user orders food) → creates rule templates

**What you'd build**:
- Inconsistency detector running periodic graph scans
- Pattern learner (statistical mining over HFF events)
- Lexicon gap detector and proposal engine (LLM-assisted)
- Human-in-the-loop review UI for accepting/rejecting new senses, parent relations, preferences

---

### 4. Multi-Agent Coordination: Specialists Working Together

**What it is**: Multiple specialized agents (vision, planning, tools, critics, domain experts) working together via HFF/NSP, sharing the same KG and semantic language.

**Why it's needed**: Monolithic systems don't scale to diverse, complex tasks. Specialization improves quality. Coordination enables division of labor.

**How it connects to HopLogic**:
- Each agent is a service that reads/writes HFF fact hubs to/from the shared KG
- Speaks HFF/NSP protocol for inter-agent communication
- Has access to relevant slices of the axiom lexicon
- **Example workflow**: "Book a restaurant for Friday"
  - Orchestrator breaks into sub-tasks: `CHECK_CALENDAR`, `FIND_RESTAURANT`, `BOOK_RESERVATION`
  - Calendar agent queries KG, writes available slots
  - Search agent queries preferences, calls API, writes candidates
  - Booking agent calls API, writes `RESERVATION` event
  - Safety/critic agent monitors actions, checks Omega policies, can veto

**What you'd build**:
- Agent orchestrator for task decomposition and routing
- Specialist agents as microservices (calendar, search, email, file, booking, etc.)
- Message bus/queue for inter-agent HFF messages
- Shared KG with clear `domaintype` partitioning
- Conflict resolver using Omega rules and user preferences

---

## Phased Implementation Roadmap

The cognitive layers are built incrementally atop the semantic kernel:

| Phase | Focus | Deliverable | Documentation Reference |
|:------|:------|:------------|:------------------------|
| **Phase 1** | Lexicon Enrichment | 1k → 10k well-defined senses, NSM explications, validated parent DAG | `AXIOM_LEXICON_OVERVIEW.md` |
| **Phase 2** | NL ↔ HFF Pipeline | Robust parser producing HFF/NSP from natural language with WSD | `HOPLOGIC_OVERVIEW.md` |
| **Phase 3** | Tool/Actuator Layer | Tool registry, API mappings, deterministic execution engine | `ARCHITECTURE_LAYERS_AND_TIERS.md` |
| **Phase 4** | Omega Curriculum | Governance rule library (HIPAA, GDPR, safety, spending) | `OMEGA_OVERVIEW.md` |
| **Phase 5** | Perception & Planning | Vision grounding, PDDL-style planner, execution monitor | `AGI_COGNITIVE_LAYERS_OVERVIEW.md` (this doc) |
| **Phase 6** | Learning & Coordination | Pattern miner, lexicon gap detector, multi-agent orchestrator | `AGI_COGNITIVE_LAYERS_OVERVIEW.md` (this doc) |
| **Phase 7** | Full Semantic OS | Integration, testing, deployment recipes | `FIREBIRD_ARCHITECTURE_OVERVIEW.md` |

---

## How This Integrates with Existing Docs

- **HopLogic Overview**: Explains the **Knowledge Ingestion Pipeline** that feeds the kernel with grounded facts from text.
- **Omega-Code Overview**: Defines the **Governance Layer** that constrains all cognitive layers—ensuring perception, planning, and coordination respect policies.
- **Firebird Architecture**: Positions the **semantic kernel + cognitive layers** within the three-layer neuro-symbolic OS (LLM intuition → Omega governance → HopLogic execution).
- **Axiom Lexicon**: Provides the **semantic substrate** that all layers use for disambiguation and reasoning.

---

## From Recipe to Reality

The **Bootstrapped AGI Recipe** (published chapter) describes the vision and principles. This document maps that vision to **concrete components, files, and implementation phases** that are already specified or in development.

Each cognitive layer is designed to be:
- **Modular**: Can be built and tested independently
- **Verifiable**: Produces HFF/NSP facts that can be audited
- **Governable**: Constrained by Omega-Code policies
- **Composable**: Layers stack cleanly on the semantic kernel

This is the path from **verifiable truth** (HopLogic) to **general intelligence** (AGI-like behavior) through **explicit engineering**, not scale alone.
