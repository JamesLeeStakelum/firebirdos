# Axiom Lexicon Overview

**Version:** 1.0  
**Last Updated:** December 4, 2025

---

## The Polysemy Problem: Why Words Must Be Explicit

Standard AI systems treat language as token patterns, not grounded meanings. When you query "bank," vector search averages riverbank, financial institution, data bank, and aircraft maneuvers into a single fuzzy point—returning irrelevant, dangerous results.

The Axiom Lexicon eliminates this by grounding **every concept to a precise, unambiguous `meaning_id`** with formal definition, parent hierarchy, and semantic primitives. This is not a dictionary—it's a **verifiable semantic substrate** that makes hallucination structurally impossible.

---

## The Four-Phase Construction Pipeline

Building the lexicon is deterministic and auditable, not crowdsourced guesswork.

### Phase 1: Ingestion & Staging

**Goal:** Import raw lexical data and align sources into a unified foundation.

**Process:**
- Import WordNet, Wiktionary, and domain-specific glossaries
- Compute rich contextual embeddings for each sense
- Align sources using text similarity + embeddings
- Resolve ambiguous alignments via "Adjudicator" LLM
- Output: `merged_lexicon.db` with unified sense inventory

**What you run:**
```bash
python lexicon_ingest.py --sources wordnet wiktionary --output merged_lexicon.db
python adjudicator.py --conflicts conflicts.tsv --model gpt-4o
```

---

### Phase 2: Enrichment & Indexing

**Goal:** Stabilize identity and make the lexicon searchable.

**Process:**
- Assign canonical `meaning_id` to every concept (e.g., `m:bank.financial_institution.n`)
- Generate human-facing glosses and usage examples via "Enricher" LLM
- Create vector index in ChromaDB for similarity search
- Output: `axiom_lexicon.db` + searchable embeddings

**Key artifact:**
```json
{
  "meaning_id": "m:bank.river_edge.n",
  "lemma": "bank",
  "pos": "noun",
  "gloss": "The sloping ground at the edge of a river or lake",
  "nsm_explication": "A PART OF THE GROUND THAT IS NEAR A RIVER AND IS HIGHER THAN THE WATER",
  "embedding": "[0.342, -0.128, ...]"
}
```

---

### Phase 3: Hierarchical Construction

**Goal:** Build a directed acyclic graph (DAG) where every concept is positioned relative to its parents.

**Process:**
- "Analyzer" LLM generates **NSM Explication** for each sense (definition using only 65 irreducible semantic primes like THINK, FEEL, GOOD, BAD, BIG, SMALL)
- Propose parent molecules based on semantic containment
- Use vector search + LLM adjudication to deterministically link each concept to parents
- Run in waves until full hierarchy converges

**Example parent chain:**
```
m:bank.river_edge.n
  └─> m:edge.boundary.n
      └─> m:part.whole_relation.n
          └─> m:thing.entity.n
```

---

### Phase 4: Validation & Governance

**Goal:** Ensure topological integrity and assign confidence scores.

**Process:**
- Run `vet_and_relevel.py` → performs **topological sort (Kahn's Algorithm)** to detect cycles and assign hierarchical levels
- "Scorer" LLM assigns confidence to each parent link (0.0–1.0)
- Generate final "sense-aware" embeddings from validated NSM explications
- Output: `axiom_lexicon_final.db` + `confidence_report.tsv`

**Quality gate:**
```bash
python vet_and_relevel.py --lexicon axiom_lexicon.db
# Fails if cycles detected or confidence < 0.85 for core concepts
```

---

## Meaning IDs & NSM Explications: The Grounding Format

Every sense is a **Concept Blueprint**:

| Field | Purpose | Example |
|:------|:--------|:--------|
| `meaning_id` | Stable, canonical identifier | `m:bank.financial_institution.n` |
| `lemma` | Base form | `bank` |
| `pos` | Part of speech | `noun` |
| `gloss` | Human-readable definition | "A business that holds money..." |
| `nsm_explication` | **Definition using only 65 semantic primes** | "A PLACE WHERE PEOPLE PUT MONEY SO THAT OTHER PEOPLE CAN USE IT TO BUY THINGS" |
| `parent_meaning_ids` | Directed edges in DAG | `["m:institution.organization.n", "m:depository.container.n"]` |
| `semrole_frame` | Valid semantic roles | `["HAS_AGENT", "HAS_THEME", "HAS_LOCATION"]` |
| `confidence` | Link validation score | `0.94` |
| `level` | Topological depth | `5` |

**NSM primes** are irreducible: GOOD, BAD, BIG, SMALL, THINK, FEEL, WANT, KNOW, DO, HAPPEN, TRUE, FALSE, IF, BECAUSE, etc. Every complex concept decomposes into these.

---

## Integration Points: How the Lexicon Serves the Stack

### With HopLogic (Knowledge Ingestion)

- **Lexicon Coverage Gate**: `lexicon_analyzer.py` scans documents before processing. If coverage < threshold, unknown terms are sent to **Cognitive Bootstrap Engine (CBE)** for provisional definition.
- **Fact Grounding**: `fact_axiom_mapper.py` performs WSD against the lexicon, mapping every word in extracted facts to its `meaning_id`.
- **Synapse Assembly**: Uses `semrole_frame` to validate that facts have required roles (e.g., `m:order.request_food.v` requires `HAS_AGENT`, `HAS_THEME`).

### With Omega (Governance)

**Policy Grounding**: Governance rules reference `meaning_id` directly:
```
GOVERNANCE_RULE NoPHIDeletion:
  PREDICATE: (ActionType == DELETE AND 
              DataSchema.contains(m:phi.protected_health_info.n))
```

**Constraint Validation**: Omega checks that actions use lexicon-sanctioned predicates before execution.

### With AGI Cognitive Layers

- **Perception**: Vision grounding queries lexicon for object senses (`m:door.artifact.n`, `m:red.color.n`)
- **Planning**: Planner uses parent relations to find alternative predicates (e.g., if `m:order.request_food.v` fails, try parent `m:request.ask_for.v`)
- **Lifelong Learning**: Lexicon gap detector flags unknown words; CBE proposes new senses for human review

---

## Bootstrapping Strategy: Coverage Gates and Phases

The lexicon must reach critical mass before the system becomes self-sustaining.

### Phase 0: Foundation (Current)

- **Size**: ~1,000 core senses (NSM primes, basic actions, entities)
- **Coverage**: 50% of everyday language
- **Goal**: Bootstrap initial pipeline

### Phase 1: Expansion (Target: Q1 2026)

- **Size**: 10,000 senses
- **Coverage**: 85% of business/legal/medical core vocabulary
- **Process**: 
  - Ingest domain-specific glossaries (HIPAA, GDPR, medical ontologies)
  - Run Phase 1–4 pipeline automatically
  - Human review for confidence < 0.90

### Phase 2: Maturity (Target: Q3 2026)

- **Size**: 50,000 senses
- **Coverage**: 95% of specialized jargon across industries
- **Process**:
  - Deploy CBE in production to handle unknown terms
  - Community contributions via "Alexandria Project"
  - Automated validation with spot-checking

### Coverage Gate Enforcement

```python
# lexicon_analyzer.py
def analyze_coverage(text: str, threshold: float = 0.85) -> bool:
    unknown = [token for token in tokenize(text) 
               if not lexicon.lookup(token)]
    coverage = 1 - len(unknown) / len(tokenize(text))

    if coverage < threshold:
        cbe.bootstrap(unknown)  # Create provisional senses
        return False  # Block pipeline until review
    return True
```

---

## The Cognitive Bootstrap Engine (CBE)

When the lexicon encounters an unknown term, CBE automatically proposes a new sense:

1. **Context Harvesting**: Extract 10–50 usage examples from documents
2. **LLM Proposal**: Generate provisional `meaning_id`, NSM explication, and parent candidates
3. **Human Review**: UI shows definition + examples + parent choices for approval
4. **Promotion**: Approved senses are merged into master lexicon and versioned

**Example CBE workflow:**
```
User text: "The heisenbug only appears in production."
Unknown: "heisenbug"
CBE proposal:
  meaning_id: "m:heisenbug.software_bug.n"
  gloss: "A bug that disappears when you try to observe it"
  nsm: "A BAD THING IN A COMPUTER PROGRAM THAT YOU CANNOT SEE WHEN YOU TRY TO FIND IT"
  parents: ["m:bug.software_error.n", "m:phenomenon.observable_event.n"]
  confidence: 0.78
Human approves → Added to lexicon → Pipeline re-runs
```

---

## Versioning & Governance

The lexicon is immutable and versioned:

- **Git-backed**: Every change is a commit with diff showing added/removed senses
- **Provenance**: Each `meaning_id` tracks origin (CBE auto-generated vs. human-curated)
- **Rollback**: If a sense causes contradictions, revert to previous version
- **Deprecation**: Senses are never deleted; marked `deprecated: true` with superseding `meaning_id`

---

## Why This Matters: The Cognitive Moat

Most AI systems rely on scale—bigger models, more data, more compute—hoping intelligence emerges. The Axiom Lexicon takes a different path: **intelligence by design**.

- **Explicit semantics**: Every symbol has stable, grounded meaning
- **Structured memory**: Every fact is queryable, explainable, verifiable
- **Universal format**: HFF/NSP flows through all components
- **Governance from day one**: Policies reference explicit `meaning_id`s

This is the foundation that makes the AGI cognitive layers (perception, planning, learning, coordination) possible. Without it, you're just prompting a stochastic parrot. With it, you're building a semantic operating system.

---

## Next Steps

- **Read**: `HOPLOGIC_OVERVIEW.md` (how the lexicon feeds the knowledge graph)
- **Read**: `OMEGA_OVERVIEW.md` (how policies ground in lexicon senses)
- **Read**: `AGI_COGNITIVE_LAYERS_OVERVIEW.md` (how the lexicon enables perception & planning)
