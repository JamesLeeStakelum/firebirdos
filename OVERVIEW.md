\# Understanding FirebirdOS: A User's Guide



\*\*Version:\*\* 1.0  

\*\*Last Updated:\*\* December 4, 2025  

\*\*Audience:\*\* Developers, Architects, Technical Decision-Makers



---



\## \*\*What Is FirebirdOS?\*\*



FirebirdOS is a \*\*neuro-symbolic operating system\*\* that combines:

\- \*\*Neural language models\*\* (flexible language understanding)

\- \*\*Symbolic reasoning\*\* (verifiable knowledge graphs + formal governance)



The result: AI systems that are \*\*explainable, governable, and safe to deploy\*\* in regulated environments.



---



\## \*\*The Three-Layer Architecture\*\*



Here's how the pieces fit together:



```

┌─────────────────────────────────────────┐

│  Layer 1: LLM (Neural Intuition)        │

│  - Understands natural language         │

│  - Generates formal specifications      │

│  - Continuously learns from feedback    │

└─────────────────────────────────────────┘

&nbsp;             ↓ (constrained by)

┌─────────────────────────────────────────┐

│  Layer 2: Omega-Code (Formal Specs)     │

│  - Policies, schemas, constraints       │

│  - Machine-verifiable grammar           │

│  - Self-modification with approval      │

└─────────────────────────────────────────┘

&nbsp;             ↓ (compiles to)

┌─────────────────────────────────────────┐

│  Layer 3: Execution (HopLogic + Axiom)  │

│  - Axiom Lexicon: 1.7M meaning IDs      │

│  - HopLogic VKG: Verifiable facts       │

│  - HFF/NSP: Machine communication       │

└─────────────────────────────────────────┘

```



\*\*How It Works in Practice:\*\*



1\. \*\*User asks\*\*: "When did Beethoven's deafness begin?"

2\. \*\*LLM Layer\*\* → Breaks into sub-questions, suggests reasoning strategy

3\. \*\*Omega Layer\*\* → Formalizes query as formal specification

4\. \*\*Execution Layer\*\* → Retrieves facts from VKG, returns provenance-tracked answer



---



\## \*\*Core Components\*\*



\### \*\*1. Axiom Lexicon\*\* (Semantic Foundation)

\*\*What it does\*\*: Turns words into precise, unambiguous IDs  

\*\*How to use it\*\*:

```

\# Query the lexicon

meaning\_id = lexicon.lookup("bank statement")

\# Returns: wkt:en:noun:bank.financial\_institution (not riverbank)

```



\*\*Key features\*\*:

\- 1.7M unique `meaning\_id`s

\- Tiered abstraction (1k/10k/50k levels)

\- FAISS index for fast lookup (~ms)



\[📖 Full Lexicon Docs](docs/AXIOM\_LEXICON.md)



---



\## \*\*2. HopLogic Knowledge Engine\*\* (Memory \& Reasoning)

\*\*What it does\*\*: Stores facts in a verifiable graph  

\*\*How to use it\*\*:

```

\# Ingest a document

python tools/ingest.py --file report.pdf --project legal\_case\_123



\# Query the graph

python tools/query.py --question "Who wrote the report?" --project legal\_case\_123

```



\*\*Key features\*\*:

\- Hub-and-spoke schema (prevent ontology explosion)

\- POV framework (track who said what)

\- Multi-hop reasoning (3-15ms latency)



\[📖 Full HopLogic Docs](docs/HOPLOGIC\_OVERVIEW.md)



---



\## \*\*3. Omega-Code\*\* (Governance Layer)

\*\*What it does\*\*: Defines what the system is allowed to do  

\*\*How to use it\*\*:

```

\# Example: Block PII deletion

GOVERNANCE\_RULE NoPIIDeletion:

&nbsp;  SCOPE UserDataManagement,

&nbsp;  PREDICATE (ActionIsDelete AND TargetSchemaIs(UserProfile)),

&nbsp;  ENFORCEMENT\_CONTEXT PreventActionAndAlertAdmin,

&nbsp;  PRIORITY 99;

```



\*\*Key features\*\*:

\- 13 atomic primitives (policies, schemas, constraints)

\- EBNF-validated grammar

\- Self-modification with approval gates



\[📖 Full Omega Docs](docs/OMEGA\_OVERVIEW.md)



---



\## \*\*4. HFF/NSP Protocol\*\* (M2M Communication)

\*\*What it does\*\*: Machines talk to each other with shared meaning  

\*\*How to use it\*\*:

```

\# Create an NSP packet

packet = NSPPacket(

&nbsp;   verb="m:detect.obstacle.v",

&nbsp;   agent="ent:vehicle.av47",

&nbsp;   patient="mobstacle.road\_object.n"

)

packet.sign()  # Cryptographic signature

packet.send()  # 50 bytes transmitted

```



\*\*Key features\*\*:

\- Compact (50-200 bytes vs. 500-2000 for JSON)

\- Cryptographically verifiable

\- Works on edge devices (1K lexicon = 100KB firmware)



\[📖 Protocol Spec](docs/HFF\_NSP\_PROTOCOL.md)



---



\## \*\*Getting Started\*\*



\### \*\*Quickstart\*\*

```

\# 1. Clone the repo

git clone https://github.com/firebirdOS/firebirdOS.git



\# 2. Install dependencies

pip install -r requirements.txt



\# 3. Run example query

python examples/beethoven\_query.py



\# 4. Explore

python tools/graph\_explorer.py

```



\### \*\*Tutorials\*\*

\- \[Building Your First VKG](docs/tutorials/first\_vkg.md)

\- \[Writing Omega Policies](docs/tutorials/omega\_policies.md)

\- \[Integrating with Your LLM](docs/tutorials/llm\_integration.md)



---



\## \*\*Use Cases\*\*



\- \*\*Legal E-Discovery\*\*: Multi-hop evidence chains, viewpoint preservation

\- \*\*Clinical Trials\*\*: Temporal sequencing, FDA audit trails

\- \*\*Compliance Auditing\*\*: Machine-verifiable policy enforcement

\- \*\*Technical Support\*\*: Verifiable diagnostic trees



See \[docs/USE\_CASES.md](docs/USE\_CASES.md) for detailed examples.



---



\## \*\*Next Steps\*\*



1\. \*\*Read the architecture deep-dive\*\*: \[docs/ARCHITECTURE\_DEEP\_DIVE.md](docs/ARCHITECTURE\_DEEP\_DIVE.md)

2\. \*\*Join the community\*\*: \[Discord](https://discord.gg/firebirdos)

3\. \*\*Contribute\*\*: See \[CONTRIBUTING.md](CONTRIBUTING.md)



---



\*\*Questions?\*\* Open an issue on GitHub or ask in Discord.

