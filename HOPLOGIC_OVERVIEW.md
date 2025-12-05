# HopLogic Overview: The Verifiable Knowledge Graph Engine

**Version:** 1.1  
**Last Updated:** December 4, 2025  

***

## What Is HopLogic?

HopLogic is the **semantic kernel** that transforms unstructured text into a **Verifiable Knowledge Graph (VKG)**—a machine-readable "Corporate Brain" where every fact is grounded, queryable, and auditable. It sits between the Axiom Lexicon (semantic substrate) and the AGI cognitive layers (perception, planning, learning, coordination), providing the universal memory substrate for trustworthy AI.[1][2]

Instead of acting as a monolithic app, HopLogic is a modular **"Operating System for Trustworthy AI"**: a collection of command-line tools and pipelines that eliminate ambiguity, preserve provenance, and enforce isolation across projects and tenants.[3][1]

HopLogic is designed for teams in **regulated, high-stakes domains**—legal, healthcare, finance, public sector—where "I don't know" is safer than a confident hallucination, and every answer must be citable back to its exact source text.[3]

***

## The AI Trust Problems HopLogic Solves

Modern LLM and vector-RAG stacks are fluent but untrustworthy: they blur meanings, conflate viewpoints, and mix private data across boundaries. HopLogic is engineered as a defense-in-depth response to four specific failure modes.[1][3]

### 1. Semantic Ambiguity – "The Bank Problem"

Standard vector search represents all senses of a word as a single embedding, so queries about a *river bank* often retrieve documents about *financial banks*, even in high-risk contexts.[3]

HopLogic grounds every token into the **Axiom Lexicon**, assigning a precise `meaning_id` such as `m:bank.financial_institution.n` vs. `m:bank.river_edge.n`, and runs all ingestion and retrieval against those IDs instead of raw strings.[1][3]

### 2. Viewpoint Ambiguity – "He Said, She Said"

Conventional RAG merges testimony, allegations, and evidence into a flattened "fact," leading to dangerous outputs like combining a plaintiff's claim that "the brake failed" with a defendant's report that "the brake engaged" into a single contradictory statement.[1][3]

HopLogic's **Viewpoint Registry** (POV framework) explicitly distinguishes `proven_fact` from `reported_claim`, attaches each statement to its source, and preserves conflicts instead of averaging them away.[3][1]

### 3. Data Contamination – "The John Smith Problem"

Single-bucket vector stores can leak confidential data: a query about one "John Smith" can pull records about another, with potentially life-threatening consequences in medical or legal settings.[1][3]

HopLogic uses **physically isolated VKGs**—one per client, matter, or project—so data never co-mingles across boundaries, and each knowledge graph can be permissioned, audited, and archived independently.[3][1]

### 4. Multi-Hop Reasoning Failures – "The Bag of Facts"

Vector systems operate on disconnected text chunks, so they fail on questions that require connecting multiple documents (e.g., "Which city is relevant to Dr. Evans's clinical work?" across trial participation, sponsor, and headquarters facts).[3]

HopLogic encodes facts as **hub-and-spoke graph structures** with semantic roles and then performs bounded multi-hop traversals, allowing it to chain relations like `PARTICIPATED_IN → SPONSORED_BY → LOCATED_IN` to surface "Berlin" even when the name never appears in the same paragraph as "Dr. Evans".[3]

***

## Core Architecture: Dual-Dimension Schema

Every HFF fact hub carries two dimensions simultaneously, enabling both semantic understanding and operational capability.

### Dimension A: Linguistic/Semantic Classification

*What the event means in language.*

| Tier | Description | Examples |
| :--- | :--- | :--- |
| **Tier 1: Semantic Roles** (12) | Participants and properties of an event | `AGENT`, `PATIENT`, `RECIPIENT`, `ATTRIBUTE`, `MANNER`, etc. |
| **Tier 2: Semantic Categories** (35) | Broad type of meaning | `ACTION`, `COMMUNICATION`, `EXCHANGE`, `CREATION`, `CAUSATION`, `EMOTION`, `LOCATION`, `MOVEMENT`, `OWNERSHIP` |
| **Tier 3: Event Properties** | Fine-grained classification | `event_type` (Birth, Commerce, LegalAction), `event_subtype` (Positive/Negative, Intentional/Accidental) |
| **Tier 4: Verb Metadata** | Link to Axiom Lexicon | `meaning_id`, `nsm_explication`, `parent_meaning_ids`, `semrole_frame` |

**Example:** "You ordered pizza" → `semantic_category: EXCHANGE`, `event_type: Commerce`, `verb_sense_uid: m:order.request_food.v`, roles: `agent: YOU`, `theme: PIZZA`, `source: VENDOR_X`[2]

### Dimension B: Domain/Application Classification

*What kind of real-world thing the event is.*

| Field | Purpose | Examples |
| :--- | :--- | :--- |
| **`domain_type`** | Application-level event class | `FOOD_ORDER`, `EMAIL_MESSAGE`, `CALENDAR_EVENT`, `FILE_OPERATION`, `TOOL_ACTION`, `WEB_SEARCH`, `PURCHASE`, `POLICY_RULE` |
| **`source_system`** | Origin of the fact | `gmail`, `doordash_api`, `filesystem`, `chat_ui`, `firebird_kernel` |
| **`artifact_type`** | Generic class of artifact | `MESSAGE`, `ORDER`, `EVENT`, `FILE`, `ACTION`, `TRANSACTION`, `POLICY` |
| **`external_id`** | Link to source system | Gmail message ID, calendar event ID, file path, order number |

**Example:** Same pizza order → `domain_type: FOOD_ORDER`, `source_system: doordash_api`, `artifact_type: ORDER`, `external_id: dd_order_xyz789`[2]

### How Dimensions Work Together

```json
{
  "fact_id": "ORDER_EVENT_042",
  "dimension_a": {
    "semantic_category": "EXCHANGE",
    "event_type": "Commerce",
    "verb_sense_uid": "m:order.request_food.v",
    "roles": {
      "agent": "YOU#s1001",
      "theme": "PIZZA#s2002",
      "source": "VENDOR_X#s3003"
    }
  },
  "dimension_b": {
    "domain_type": "FOOD_ORDER",
    "source_system": "doordash_api",
    "artifact_type": "ORDER",
    "external_id": "dd_order_xyz789"
  }
}
```

The semantic layer enables reasoning: *"What does 'order' mean?"* The domain layer enables action: *"Route this to the DoorDash API and apply spending policies."*[2]

***

## HFF/NSP: The Universal Thought Format

### HFF (Hub-and-Spoke Fact Format)

Represents each fact as a **central hub** with typed **spokes** radiating outward. This mirrors natural language clauses and keeps all event participants grouped together (unlike RDF triples that scatter information across chains).[2]

**Conceptual structure:**
```
Hub: ORDER_EVENT_042
├─ predicate: m:order.request_food.v
├─ AGENT: YOU#s1001
├─ THEME: PIZZA#s2002
├─ SOURCE: VENDOR_X#s3003
├─ temporal: "2025-11-30T19:00:00Z"
└─ provenance: {source_system: "chat_ui", confidence: 0.94}
```

### NSP (Neuro-Symbolic Protocol)

The **deterministic JSON encoding** of HFF for storage and transmission. All fields are strongly typed, IDs follow conventions, and the format is parseable without ambiguity.[2]

**NSP Schema:**
```json
{
  "fact_id": "string (unique)",
  "predicate_id": "string (meaning_id)",
  "roles": {
    "agent": "string (entity_id)",
    "patient": "string (entity_id)",
    "recipient": "string (entity_id)",
    "...": "..."
  },
  "pov_status": "enum [CONFIRMED_SENSOR, REPORTED_CLAIM, INFERRED, ...]",
  "validity_period": {"start": "ISO8601", "end": "ISO8601"},
  "temporal": {"event_time": "ISO8601"},
  "provenance": {
    "source_system": "string",
    "confidence": "float [0.0, 1.0]",
    "source_text": "string"
  },
  "semantic_category": "string",
  "event_type": "string",
  "domain_type": "string",
  "artifact_type": "string"
}
```

**Why Hub-and-Spoke Beats Triples:**
- **Semantic coherence:** All arguments stay grouped, not scattered
- **Efficient querying:** Query the hub once, not chase chains
- **Natural mapping:** Parse trees map directly to HFF structure[2]

***

## Knowledge Ingestion Pipeline

Transforms raw documents into grounded HFF facts in four deterministic steps.

### Step 1: Lexicon Coverage Gate

Before processing, `lexicon_analyzer.py` scans the document. If vocabulary coverage is below threshold (e.g., 85%), unknown terms are sent to the **Cognitive Bootstrap Engine (CBE)** for provisional sense creation. This ensures every word can be grounded.[1]

```bash
python lexicon_analyzer.py --doc input.txt --threshold 0.85
# Output: coverage_report.json, unknown_terms.tsv
```

### Step 2: Fact Extraction (IDE)

The **Ingestion & Distillation Engine (IDE)** uses an LLM to:
- Split text into atomic, self-contained facts
- Resolve pronouns and relative time references
- Output: `facts.jsonl` (one fact per line)

```json
{"fact_id": "f-001", "text": "Beethoven composed Symphony No. 5 in 1808.", "provenance": "doc:beethoven_bio.pdf"}
{"fact_id": "f-002", "text": "The symphony premiered in Vienna.", "provenance": "doc:beethoven_bio.pdf"}
```

### Step 3: Synapse Transformation

`fact_axiom_mapper.py` performs:
- **Word Sense Disambiguation (WSD)** against Axiom Lexicon
- Maps each term to `meaning_id`
- Assembles HFF hub-and-spoke structure
- Validates required semantic roles per `semrole_frame`
- Output: `synapse_facts.jsonl` (HFF/NSP format)

```json
{
  "fact_id": "f-001",
  "predicate_id": "m:compose.create_music.v",
  "roles": {
    "agent": "ent:beethoven#s123",
    "patient": "ent:symphony_no_5#s456"
  },
  "temporal": {"event_time": "1808"},
  "provenance": {"source_system": "ide", "confidence": 0.92}
}
```

### Step 4: Graph Loading

Auto-generated `synapse_load.cypher` uses idempotent `MERGE` commands to bulk-load into **Kùzu/Neo4j** graph database. Each HFF hub becomes a node; spokes become edges to concept nodes.[1]

```cypher
MERGE (f:FactInstance {fact_id: 'f-001'})
MERGE (f)-[:HAS_HUB]->(p:Concept {meaning_id: 'm:compose.create_music.v'})
MERGE (f)-[:HAS_AGENT]->(a:Concept {meaning_id: 'ent:beethoven#s123'})
MERGE (f)-[:HAS_PATIENT]->(p2:Concept {meaning_id: 'ent:symphony_no_5#s456'})
```

**Run the pipeline:**
```bash
hoplogic ingest --project-id my-corpus --batch
# Executes: analyze → ide → synapse → load
```

***

## RAG & Query Pipeline

Retrieves precise, verifiable context for LLM synthesis.

### Step 1: Query Disambiguation (QID)

The user's natural language query is parsed and mapped to `meaning_id`s using the Axiom Lexicon. This resolves polysemy before retrieval.[1]

**Query:** "What did Beethoven compose?"  
**QID output:**
```json
{
  "query_meanings": {
    "Beethoven": "ent:beethoven#s123",
    "compose": "m:compose.create_music.v"
  }
}
```

### Step 2: Adaptive RAG Strategy

The system assembles a **tiered context package** based on query complexity:

| Tier | Use Case | Retrieval Method |
| :--- | :--- | :--- |
| **Tier 1: Atomic Fact** | Simple lookup | `MATCH (f)-[:HAS_PATIENT]->(:Concept {meaning_id: 'ent:symphony_no_5#s456'}) RETURN f.text` |
| **Tier 2: Multi-hop Chain** | Relational queries | Traverse graph: `Beethoven → COMPOSED → Symphony → PREMIERED_IN → Vienna` |
| **Tier 3: Definitional Chain** | Abstract concepts | Fetch NSM explications + parent hierarchy for `m:compose.create_music.v` |

### Step 3: Grounded LLM Synthesis

The **Golden Rule of RAG Prompting** is enforced: *"Answer using ONLY the provided facts. Do not use prior knowledge. Cite each fact by ID."*[1]

**Prompt template:**
```
You are a precision AI. Answer using ONLY the facts below.

Facts:
[f-001] Beethoven composed Symphony No. 5 in 1808. (source: beethoven_bio.pdf)
[f-002] The symphony premiered in Vienna. (source: beethoven_bio.pdf)

Question: What did Beethoven compose?

Answer:
Beethoven composed Symphony No. 5 in 1808 [f-001]. It premiered in Vienna [f-002].
```

This makes hallucination **structurally impossible**—the LLM is constrained to the verified context.

***

## Two Storage Modes

### Mode A: Knowledge Extraction (Atomized Facts)

**Use for:** Corporate documents, policies, manuals, reference material—anything you want to **reason over and query**.

**Behavior:**
1. Ingest text → parse sentences → extract atomic facts
2. Store as small HFF fact hubs (subject-predicate-object + semantic roles)
3. Disambiguate entities using Axiom Lexicon sense IDs
4. Create edges in KG for graph traversal

**Example:**
```
Input: "Beethoven composed Symphony No. 5 in 1808."

Stored as:
- Event hub: COMPOSE_EVENT_789
- Roles: agent=BEETHOVEN#s123, patient=SYMPHONY_NO_5#s456, temporal=1808
- Provenance: sourcedoc=beethoven_biography.pdf
```

**Enables queries:** "What did Beethoven compose?" or "Show all Creation events in 1808"[2]

### Mode B: Artifact Preservation (Whole Creations)

**Use for:** Poems, emails, chat messages, drafts—where **exact wording matters** and atomizing would destroy value.

**Behavior:**
1. Store creation as **two nodes** connected by an edge:
   - **EVENT node**: The act (`COMPOSE`, `CREATE`, `SEND`) with semantic metadata
   - **ARTIFACT node**: The full text/content with metadata
2. Do NOT split into atomic facts (except maybe high-level tags)
3. Edge: `EVENT -[CREATED]-> ARTIFACT`

**Example:**
```
Email draft: "Hi Mom, Thanksgiving plans..."

Stored as:
- Event: compose_event_099
  - predicate: m:compose.write_message.v
  - roles: agent=SYSTEM, recipient=MOM#person3, subject="Thanksgiving plans"
- Artifact: email_artifact_099
  - artifact_kind: EMAIL
  - full_text: "Hi Mom, Thanksgiving plans..."
- Edge: compose_event_099 -[:CREATED]-> email_artifact_099
```

**Goal:** Preserve exact artifact while still knowing who created it, for whom, when, and why[2]

### Hybrid Approach

Sometimes you want **both**: store the email as a whole artifact (Mode B) but also extract key facts for reasoning (Mode A):
- Email mentions Thanksgiving date → temporal fact
- Recipient is MOM → relation fact
- Store these as separate lightweight fact hubs referencing the email artifact

This gives you **coherent artifacts for retrieval + atomic facts for reasoning**[2]

***

## Integration Points

### With Axiom Lexicon

- **Coverage Gate**: Unknown terms trigger CBE for provisional sense creation
- **WSD**: `fact_axiom_mapper.py` queries lexicon for `meaning_id` resolution
- **Validation**: `semrole_frame` ensures HFF facts have required roles
- **Enrichment**: NSM explications provide definitional chains for abstract concepts[1]

### With Omega (Governance)

- **Policy Grounding**: Omega rules reference `meaning_id` directly:
  ```cypher
  GOVERNANCE_RULE NoPHIDeletion:
    PREDICATE: (ActionType == DELETE AND 
                DataSchema.contains(m:phi.protected_health_info.n))
  ```
- **Pre-execution Check**: Governor validates plans against policies before acting
- **Audit Trail**: Every HFF fact logs provenance for compliance[1]

### With AGI Cognitive Layers

- **Perception**: Vision grounding queries lexicon for object senses → creates `PERCEPTION_EVENT` HFF hubs
- **Planning**: Planner uses parent relations from lexicon to find alternative predicates
- **Learning**: Pattern miner discovers regularities in HFF event streams
- **Coordination**: Agents communicate via HFF/NSP messages over shared KG[2]

***

## Performance & Scalability

The engine uses **Perl** where raw text processing speed and streaming performance matter (e.g., pipeline orchestration, regex-heavy transformations) and **Python** where deep learning and ML ecosystems are strongest (e.g., embeddings, LLM calls, FAISS).[3]

This polyglot approach balances C-like performance with modern AI tooling, without locking the system into a single language's constraints.[3]

### Key Optimizations:
- **Idempotent loading**: Re-run pipeline safely; `MERGE` prevents duplicates
- **Isolated graphs**: One Kùzu/Neo4j folder per project—easy to secure, backup, ship
- **Batch processing**: `run_pipeline_batch.pl` processes thousands of documents in parallel[1]

***

## Quick Start: Build Your First VKG

```bash
# 1. Initialize project
hoplogic init --project-id my-first-vkg

# 2. Add documents
cp /path/to/docs/* ./projects/my-first-vkg/docs/

# 3. Run ingestion pipeline
hoplogic ingest --project-id my-first-vkg --batch

# 4. Query with precision
hoplogic query --project-id my-first-vkg \
  --question "What did Beethoven compose?" \
  --output citations.json

# 5. Inspect the graph
hoplogic explore --project-id my-first-vkg
```

**Result:** Every answer includes `fact_id` citations linking back to source text and line numbers.[1]

***

## Why This Changes Everything

Most AI systems are **black boxes**—fluent but untrustworthy. HopLogic is a **glass box** where every decision is traceable, every fact is verifiable, and every action is governable.

- **For developers**: Build hallucination-free RAG and governed agents in hours, not months
- **For enterprises**: Deploy AI in regulated industries with provable compliance
- **For AGI research**: A semantic substrate that supports perception, planning, learning, and coordination[2][1]

The path from **verifiable truth** (Axiom Lexicon) to **general intelligence** (AGI layers) runs through HopLogic.[2]

***

**Next Steps:**
- **Deep dive**: `AXIOM_LEXICON_OVERVIEW.md` (semantic substrate)
- **Governance**: `OMEGA_OVERVIEW.md` (policy enforcement)
- **Cognition**: `AGI_COGNITIVE_LAYERS_OVERVIEW.md` (perception, planning, learning, coordination)

