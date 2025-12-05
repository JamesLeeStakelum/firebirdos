Here is the \*\*`AXIOM\_LEXICON\_OVERVIEW.md`\*\*:



```markdown

\# Axiom Lexicon Overview



\*\*Version:\*\* 1.0  

\*\*Last Updated:\*\* December 4, 2025  



---



\## The Polysemy Problem: Why Words Must Be Explicit



Standard AI systems treat language as token patterns, not grounded meanings. When you query "bank," vector search averages riverbank, financial institution, data bank, and aircraft maneuvers into a single fuzzy point—returning irrelevant, dangerous results.\[file:446]



The Axiom Lexicon eliminates this by grounding \*\*every concept to a precise, unambiguous `meaning\_id`\*\* with formal definition, parent hierarchy, and semantic primitives. This is not a dictionary—it's a \*\*verifiable semantic substrate\*\* that makes hallucination structurally impossible.\[file:446]\[file:447]



---



\## The Four-Phase Construction Pipeline



Building the lexicon is deterministic and auditable, not crowdsourced guesswork.



\### Phase 1: Ingestion \& Staging



\*\*Goal:\*\* Import raw lexical data and align sources into a unified foundation.



\*\*Process:\*\*

\- Import WordNet, Wiktionary, and domain-specific glossaries

\- Compute rich contextual embeddings for each sense

\- Align sources using text similarity + embeddings

\- Resolve ambiguous alignments via "Adjudicator" LLM

\- Output: `merged\_lexicon.db` with unified sense inventory\[file:446]



\*\*What you run:\*\*

```

python lexicon\_ingest.py --sources wordnet wiktionary --output merged\_lexicon.db

python adjudicator.py --conflicts conflicts.tsv --model gpt-4o

```



---



\### Phase 2: Enrichment \& Indexing



\*\*Goal:\*\* Stabilize identity and make the lexicon searchable.



\*\*Process:\*\*

\- Assign canonical `meaning\_id` to every concept (e.g., `m:bank.financial\_institution.n`)

\- Generate human-facing glosses and usage examples via "Enricher" LLM

\- Create vector index in ChromaDB for similarity search

\- Output: `axiom\_lexicon.db` + searchable embeddings\[file:446]



\*\*Key artifact:\*\*

```

{

&nbsp; "meaning\_id": "m:bank.river\_edge.n",

&nbsp; "lemma": "bank",

&nbsp; "pos": "noun",

&nbsp; "gloss": "The sloping ground at the edge of a river or lake",

&nbsp; "nsm\_explication": "A PART OF THE GROUND THAT IS NEAR A RIVER AND IS HIGHER THAN THE WATER",

&nbsp; "embedding": "\[0.342, -0.128, ...]"

}

```



---



\### Phase 3: Hierarchical Construction



\*\*Goal:\*\* Build a directed acyclic graph (DAG) where every concept is positioned relative to its parents.



\*\*Process:\*\*

\- "Analyzer" LLM generates \*\*NSM Explication\*\* for each sense (definition using only 65 irreducible semantic primes like THINK, FEEL, GOOD, BAD, BIG, SMALL)

\- Propose parent molecules based on semantic containment

\- Use vector search + LLM adjudication to deterministically link each concept to parents

\- Run in waves until full hierarchy converges\[file:446]



\*\*Example parent chain:\*\*

```

m:bank.river\_edge.n

&nbsp; └─> m:edge.boundary.n

&nbsp;     └─> m:part.whole\_relation.n

&nbsp;         └─> m:thing.entity.n

```



---



\### Phase 4: Validation \& Governance



\*\*Goal:\*\* Ensure topological integrity and assign confidence scores.



\*\*Process:\*\*

\- Run `vet\_and\_relevel.py` → performs \*\*topological sort (Kahn's Algorithm)\*\* to detect cycles and assign hierarchical levels

\- "Scorer" LLM assigns confidence to each parent link (0.0–1.0)

\- Generate final "sense-aware" embeddings from validated NSM explications

\- Output: `axiom\_lexicon\_final.db` + `confidence\_report.tsv`\[file:446]



\*\*Quality gate:\*\*

```

python vet\_and\_relevel.py --lexicon axiom\_lexicon.db

\# Fails if cycles detected or confidence < 0.85 for core concepts

```



---



\## Meaning IDs \& NSM Explications: The Grounding Format



Every sense is a \*\*Concept Blueprint\*\*:



| Field | Purpose | Example |

| :--- | :--- | :--- |

| `meaning\_id` | Stable, canonical identifier | `m:bank.financial\_institution.n` |

| `lemma` | Base form | `bank` |

| `pos` | Part of speech | `noun` |

| `gloss` | Human-readable definition | "A business that holds money..." |

| `nsm\_explication` | \*\*Definition using only 65 semantic primes\*\* | "A PLACE WHERE PEOPLE PUT MONEY SO THAT OTHER PEOPLE CAN USE IT TO BUY THINGS" |

| `parent\_meaning\_ids` | Directed edges in DAG | `\["m:institution.organization.n", "m:depository.container.n"]` |

| `semrole\_frame` | Valid semantic roles | `\["HAS\_AGENT", "HAS\_THEME", "HAS\_LOCATION"]` |

| `confidence` | Link validation score | `0.94` |

| `level` | Topological depth | `5` |



\*\*NSM primes\*\* are irreducible: GOOD, BAD, BIG, SMALL, THINK, FEEL, WANT, KNOW, DO, HAPPEN, TRUE, FALSE, IF, BECAUSE, etc. Every complex concept decomposes into these.\[file:446]\[file:447]



---



\## Integration Points: How the Lexicon Serves the Stack



\### With HopLogic (Knowledge Ingestion)

\- \*\*Lexicon Coverage Gate\*\*: `lexicon\_analyzer.py` scans documents before processing. If coverage < threshold, unknown terms are sent to \*\*Cognitive Bootstrap Engine (CBE)\*\* for provisional definition.\[file:446]

\- \*\*Fact Grounding\*\*: `fact\_axiom\_mapper.py` performs WSD against the lexicon, mapping every word in extracted facts to its `meaning\_id`.\[file:446]

\- \*\*Synapse Assembly\*\*: Uses `semrole\_frame` to validate that facts have required roles (e.g., `m:order.request\_food.v` requires `HAS\_AGENT`, `HAS\_THEME`).\[file:446]



\### With Omega (Governance)

\- \*\*Policy Grounding\*\*: Governance rules reference `meaning\_id` directly:

&nbsp; ```

&nbsp; GOVERNANCE\_RULE NoPHIDeletion:

&nbsp;   PREDICATE: (ActionType == DELETE AND 

&nbsp;               DataSchema.contains(m:phi.protected\_health\_info.n))

&nbsp; ```

\- \*\*Constraint Validation\*\*: Omega checks that actions use lexicon-sanctioned predicates before execution.\[file:446]



\### With AGI Cognitive Layers

\- \*\*Perception\*\*: Vision grounding queries lexicon for object senses (`m:door.artifact.n`, `m:red.color.n`)\[file:451]

\- \*\*Planning\*\*: Planner uses parent relations to find alternative predicates (e.g., if `m:order.request\_food.v` fails, try parent `m:request.ask\_for.v`)\[file:451]

\- \*\*Lifelong Learning\*\*: Lexicon gap detector flags unknown words; CBE proposes new senses for human review\[file:451]



---



\## Bootstrapping Strategy: Coverage Gates and Phases



The lexicon must reach critical mass before the system becomes self-sustaining.



\### Phase 0: Foundation (Current)

\- \*\*Size\*\*: ~1,000 core senses (NSM primes, basic actions, entities)

\- \*\*Coverage\*\*: 50% of everyday language

\- \*\*Goal\*\*: Bootstrap initial pipeline



\### Phase 1: Expansion (Target: Q1 2026)

\- \*\*Size\*\*: 10,000 senses

\- \*\*Coverage\*\*: 85% of business/legal/medical core vocabulary

\- \*\*Process\*\*: 

&nbsp; - Ingest domain-specific glossaries (HIPAA, GDPR, medical ontologies)

&nbsp; - Run Phase 1–4 pipeline automatically

&nbsp; - Human review for confidence < 0.90



\### Phase 2: Maturity (Target: Q3 2026)

\- \*\*Size\*\*: 50,000 senses

\- \*\*Coverage\*\*: 95% of specialized jargon across industries

\- \*\*Process\*\*:

&nbsp; - Deploy CBE in production to handle unknown terms

&nbsp; - Community contributions via "Alexandria Project"

&nbsp; - Automated validation with spot-checking



\### Coverage Gate Enforcement



```

\# lexicon\_analyzer.py

def analyze\_coverage(text: str, threshold: float = 0.85) -> bool:

&nbsp;   unknown = \[token for token in tokenize(text) 

&nbsp;              if not lexicon.lookup(token)]

&nbsp;   coverage = 1 - len(unknown) / len(tokenize(text))

&nbsp;   

&nbsp;   if coverage < threshold:

&nbsp;       cbe.bootstrap(unknown)  # Create provisional senses

&nbsp;       return False  # Block pipeline until review

&nbsp;   return True

```



---



\## The Cognitive Bootstrap Engine (CBE)



When the lexicon encounters an unknown term, CBE automatically proposes a new sense:



1\. \*\*Context Harvesting\*\*: Extract 10–50 usage examples from documents

2\. \*\*LLM Proposal\*\*: Generate provisional `meaning\_id`, NSM explication, and parent candidates

3\. \*\*Human Review\*\*: UI shows definition + examples + parent choices for approval

4\. \*\*Promotion\*\*: Approved senses are merged into master lexicon and versioned\[file:446]



\*\*Example CBE workflow:\*\*

```

User text: "The heisenbug only appears in production."

Unknown: "heisenbug"

CBE proposal:

&nbsp; meaning\_id: "m:heisenbug.software\_bug.n"

&nbsp; gloss: "A bug that disappears when you try to observe it"

&nbsp; nsm: "A BAD THING IN A COMPUTER PROGRAM THAT YOU CANNOT SEE WHEN YOU TRY TO FIND IT"

&nbsp; parents: \["m:bug.software\_error.n", "m:phenomenon.observable\_event.n"]

&nbsp; confidence: 0.78

Human approves → Added to lexicon → Pipeline re-runs

```



---



\## Versioning \& Governance



The lexicon is immutable and versioned:



\- \*\*Git-backed\*\*: Every change is a commit with diff showing added/removed senses

\- \*\*Provenance\*\*: Each `meaning\_id` tracks origin (CBE auto-generated vs. human-curated)

\- \*\*Rollback\*\*: If a sense causes contradictions, revert to previous version

\- \*\*Deprecation\*\*: Senses are never deleted; marked `deprecated: true` with superseding `meaning\_id`



---



\## Why This Matters: The Cognitive Moat



Most AI systems rely on scale—bigger models, more data, more compute—hoping intelligence emerges. The Axiom Lexicon takes a different path: \*\*intelligence by design\*\*.



\- \*\*Explicit semantics\*\*: Every symbol has stable, grounded meaning

\- \*\*Structured memory\*\*: Every fact is queryable, explainable, verifiable

\- \*\*Universal format\*\*: HFF/NSP flows through all components

\- \*\*Governance from day one\*\*: Policies reference explicit `meaning\_id`s



This is the foundation that makes the AGI cognitive layers (perception, planning, learning, coordination) possible. Without it, you're just prompting a stochastic parrot. With it, you're building a semantic operating system.\[file:446]\[file:447]



---



\## Next Steps



\- \*\*Read\*\*: `HOPLOGIC\_OVERVIEW.md` (how the lexicon feeds the knowledge graph)

\- \*\*Read\*\*: `OMEGA\_OVERVIEW.md` (how policies ground in lexicon senses)

\- \*\*Read\*\*: `AGI\_COGNITIVE\_LAYERS\_OVERVIEW.md` (how the lexicon enables perception \& planning)





