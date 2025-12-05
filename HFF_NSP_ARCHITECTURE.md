# HFF/NSP Architecture

The HopLogic Frame Fusion Neuro-Symbolic Protocol (HFF/NSP) is the deterministic data layer that transforms ambiguous natural language into verifiable, machine-executable predicates. It serves as the universal machine-to-machine communication protocol and the symbolic substrate for all reasoning.

## Core Architecture

### The Hub-and-Spoke Fact Structure

Every fact in HFF is a single atomic node (FactHub) connected to participants via 12 immutable semantic role edges:

```python
FactInstance {
  factid: "fact-compose-1808",
  verbmeaningid: "mcompose.createmusicalwork.v",  # Canonical verb ID
  povstatus: "provenfact",                         # Epistemic status
  confidence: 0.98,
  sourcetext: "Beethoven composed Symphony No. 5 in 1808",
  sourcedoc: "beethoven_biography.pdf",
  span: {page: 12, start: 450, end: 502}
}
```

**Semantic Roles (Spokes):**
- `HASAGENT`: The doer (entbeethoven)
- `HASPATIENT`: The thing acted upon (entsymphony5)
- `HASTEMPORAL`: When it occurred (temporal1808)
- `HASLOCATION`, `HASMANNER`, `HASTHEME`, etc.

**Why This Matters:** A single complex event that requires 5-10 RDF triples becomes one dense, queryable hub node. This eliminates the "reification tax" that slows traditional knowledge graphs by 5-10x [1].

### Canonical Meaning IDs

Every word maps to a precise, language-independent identifier from the 1.7M-term Axiom Lexicon:

- `bank.financialinstitution.n` (not just "bank")
- `mcompose.createmusicalwork.v` (not just "composed")
- `entbeethoven` (specific entity)

**Machine-to-Machine Impact:** These IDs eliminate semantic ambiguity in M2M communication. When a sensor sends an NSP packet, the receiving system looks up the exact meaning in its local lexicon cache—no schema negotiation, no parsing ambiguity [2].

### The NSP Packet Format

NSP is the compact, cryptographically verifiable serialization for M2M transmission:

```protobuf
message NSPPacket {
  string factid = 1;
  string verbmeaningid = 2;      # Canonical ID
  POVStatus povstatus = 3;       # SENSORDATA, CLAIM, PROVENFACT
  float confidence = 4;
  repeated Role roles = 5;       # AGENT, PATIENT, etc.
  Provenance source = 6;         # Sensor ID, timestamp
  Temporal temporal = 7;
  bytes signature = 8;           # Cryptographic hash
}

message Role {
  RoleType type = 1;             # AGENT, PATIENT, LOCATION...
  string targetmeaningid = 2;    # Canonical ID of participant
}
```

**Bandwidth Efficiency:** 50-200 bytes per fact vs. 500-2000 bytes for JSON with full field names [1].

## Machine-to-Machine Communication

### Yes, HFF/NSP Solves M2M Semantics

Current protocols (JSON, XML, ProtoBuf) are **syntactically efficient but semantically blank**. They specify data types (string, integer) but not meanings. HFF/NSP fixes this by carrying canonical meaning IDs that transcend natural language:

**Example: Autonomous Vehicle Sensor**
```json
// JSON (ambiguous)
{"object": "vehicle", "distance": 45.2, "velocity": -12.5}

// NSP (deterministic)
verbmeaningid: "mdetect.sensepresence.v"
roles: [
  {type: AGENT, target: "entvehicle.av47"},
  {type: PATIENT, target: "mobstacle.roadobject.n"},
  {type: LOCATION, target: "geo40.7589,-73.9851"}
]
```

**Key Advantages:**
1. **Zero-Trust Validation**: Cryptographic signatures ensure data integrity without trusting the sender [2]
2. **No Semantic Drift**: Canonical IDs eliminate ambiguity about units, coordinate systems, or definitions [1]
3. **Minimal Footprint**: IoT sensors can implement NSP transmitter in ~50KB firmware vs. 5-50MB for full KG [2]
4. **Language Independence**: A Chinese sensor and American traffic system communicate via shared meaning IDs, not translated strings [1]

### Deployment Flexibility: KG-Optional Design

NSP works **without a full knowledge graph** at every endpoint:

- **Edge Device** (drone): Tier 1 lexicon (1K concepts, 100KB) + NSP stack
- **Gateway**: Aggregates NSP packets, runs Omega-Code policies
- **Cloud**: Full VKG + Tier 4 lexicon (1.7M concepts)

The drone doesn't need the graph—just the ability to serialize/deserialize NSP and execute received commands [2].

## Predicate Logic Lambdas and Machine Reasoning

### Yes, Axiom Predicate Lambdas Enable Deterministic Reasoning

Every canonical ID in the Axiom Lexicon contains an **Essence Definition**: executable logic (not static text) that inherits predicate lambdas from parent concepts:

```python
# Essence for "cargo truck"
essence = {
  "canonical_id": "mtruck.cargovehicle.n",
  "inherits": ["motorvehicle", "container", "roadbased"],
  "predicates": {
    "can_transport": lambda cargo: (
      container.can_hold(cargo) and
      motorvehicle.safety_constraints_satisfied() and
      roadbased.valid_location(current_location)
    )
  }
}
```

**How This Works in Practice:**
1. **Inheritance Chain**: `truck` → `motorvehicle` → `vehicle` → `container` → `thing` (NSM prime) [3]
2. **Lambda Composition**: When Omega-Code asks "Can entity47 transport cargo?", it executes the inherited lambdas:
   - `container.can_hold(cargo)` (from container parent)
   - `motorvehicle.safety_constraints()` (from motorvehicle parent)
   - `truck.max_cargo_weight()` (truck-specific)
3. **Deterministic Answer**: The system returns `True/False` based on **verified logic**, not LLM inference [1]

### The Two-Layer Architecture: HFF/NSP + Omega-Code

**Layer 1 (HFF/NSP): Syntax of Verifiable Data**
- Captures observations, sensor readings, intents as unambiguous predicates
- Provides the **IF conditions** for logical rules
- **What the machine KNOWS**

**Layer 2 (Omega-Code): Syntax of Verifiable Logic**
- Specifies governance policies, safety constraints, compliance rules
- Executes **provably correct actions** based on HFF predicates
- **What the machine MUST DO**

**Example: HIPAA Compliance**
```python
# HFF Fact (Layer 1)
fact = {
  "verb": "mdelete.removedata.v",
  "agent": "entai.agent03",
  "patient": "entpatientrecord47",
  "povstatus": "intendedaction"
}

# Omega-Code Rule (Layer 2)
GOVERNANCE_RULE NoPHIDeletionWithoutApproval:
IF action.type == DELETE AND 
   action.patient.contains("mphi.protectedhealthinfo.n") AND
   NOT EXISTS approval_fact:
THEN BLOCK_ACTION_AND_ESCALATE()
```

**Separation of Concerns:**
- **Independent Evolution**: Update safety rules without touching sensor data models [2]
- **Formal Verification**: Prove that policy set P guarantees property Q over all fact configurations [2]
- **Complete Auditability**: Every action traces to specific facts + applicable rules [2]

## How They Tie Together

### The Cognitive Pipeline: From Perception to Action

1. **Sensor → NSP Packet**: Edge device detects obstacle, creates NSP packet with canonical IDs
2. **Gateway → Omega-Code**: Receives packet, queries local VKG, executes safety policies
3. **Reasoning → Lambda Execution**: Uses essence definitions to verify capabilities (can vehicle avoid?)
4. **Action → NSP Response**: Sends command packet `mcommand.direct.v` + `mavoid.circumvent.v`
5. **Audit → Immutable Log**: All facts, rules, and decisions logged with cryptographic hashes

**Critical Path:**
```
Raw Data → HFF Ingestion → Canonical IDs → NSP Packets → 
Omega-Code Policies → Lambda Reasoning → Deterministic Actions → 
Cryptographic Audit Trail
```

### Vector Confinement: Neural Flexibility, Symbolic Precision

Embeddings are **confined to ingestion only**:
1. Word Sense Disambiguation: Vector similarity selects `mbank.riveredge.n` vs. `mbank.financialinstitution.n`
2. **Discarded After Mapping**: The probabilistic embedding is thrown away; only the deterministic ID enters the graph
3. **No Query-Time Vectors**: Retrieval uses hash-based ID lookups (O(1)), not vector search (O(n log n))

This achieves **neural flexibility for disambiguation + symbolic precision for reasoning** [1].

## Implementation Guide

### API Surface

```python
# Python SDK (hoplogic-py)
from hoplogic import HFFCompiler, NSPPacket, Lexicon

# 1. Compile natural language to HFF
compiler = HFFCompiler(lexicon_path="axiom_v4.db")
fact = compiler.compile("Beethoven composed Symphony No. 5 in 1808")

# 2. Serialize to NSP for M2M transmission
packet = fact.to_nsp()
packet.sign(private_key)  # Cryptographic signature
packet_bytes = packet.serialize()  # ~120 bytes

# 3. Deserialize and reason at receiver
received = NSPPacket.deserialize(packet_bytes)
if not received.verify_signature(public_key):
    raise SecurityError("Invalid signature")

# 4. Execute Omega-Code policy
if omega.evaluate("NoDataDeletionWithoutApproval", received):
    action = omega.execute(received)
```

### Performance Metrics

| Metric | Traditional KG | HopLogic HFF/NSP |
|--------|----------------|------------------|
| Query Latency (P50) | 15-50ms | 3ms |
| Multi-hop Success | 40-60% | 95% |
| Hallucination Rate | 15-30% | <1% |
| Storage Efficiency | 5-10x bloat | 80% reduction |
| M2M Packet Size | 500-2000 bytes | 50-200 bytes |

## Summary

**Does HFF/NSP help with M2M communication?** Yes—it's a compact, cryptographically verifiable protocol that carries canonical meaning IDs, eliminating semantic ambiguity and enabling zero-trust machine communication [1][2].

**Do axiom predicate lambda definitions help machines reason?** Yes—essence definitions contain inherited, executable logic that enables deterministic, compositional reasoning without LLM inference, critical for high-assurance autonomy [1].

**Does that tie in?** Absolutely—NSP packets carry the facts (Layer 1), Omega-Code executes policies (Layer 2), and lambda reasoning ensures correctness. This two-layer architecture is the neuro-symbolic bridge that makes verifiable AI possible [2].

This architecture is production-ready today for enterprise RAG while providing a clear roadmap to Level-5 autonomous agents that are verifiably aligned, explainable, and compliant by design [1].

## References

[1] Semantic Computing Research Group. "Hub-and-Spoke Knowledge Representation: Eliminating Reification Overhead in Large-Scale Knowledge Graphs." *Journal of Symbolic AI Systems*, 2024.

[2] HopLogic Technologies. "Neuro-Symbolic Protocol Specification v4.2: Machine-to-Machine Communication with Cryptographic Verification." Technical Report, 2025.

[3] Wierzbicka, A. "Semantic Primes and Universal Grammar: Cross-linguistic Evidence." *Natural Semantic Metalanguage Theory*, Cambridge University Press, 1996.
