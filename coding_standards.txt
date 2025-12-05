## FirebirdOS Coding Standards

## **I. CORE MANDATES** (1-17)

**Foundational engineering discipline**
1. **Atomicity/SRP everywhere** - Systems → Scripts → Functions → Statements. No side effects, single purposes.
2. **Test-Driven Design (TDD)** - Test plan MANDATORY in every tech spec, woven into design.
3. **Skeleton-first development** - Systems/Scripts/Functions hierarchy before coding.
4. **Storage plan required** - SQL/Vector/Graph DB needs explicitly defined.
5. **CLI args explicit** - All command-line parameters/flags documented.
6. **Simplicity-first** - SQLite/Kuzu/ChromeDB >> AWS/Docker/K8s/Oracle/Salesforce.
7. **ZeroMQ for IPC** - Preferred interprocess communication.
8. **ONNX Runtime preferred** - Avoid sentence-transformers lib collisions, use ONNX models.
9. **Minimal Python dependencies** - Avoid incompatible/crash-prone libs when possible.
10. **Observability mandatory** - Logs/metrics/tracing every atomic unit.
11. **Security-by-design** - Injection defense, secrets, rate limits, audits.
12. **Anti-overengineering** - Simpler working > complex perfect.

**V5 PRODUCTION MANDATES** (NEW)
13. **FAILSAFE CHAIN** - Triple fallback for ALL critical components (bootloader/kernel/tools).
14. **SANDBOX MANDATORY** - New toolbox tools: <30s timeout, <512MB RAM, no-net default.
15. **BUDGET ENFORCEMENT** - Daily/hourly limits: LLM calls(100), builds(3), toolbox(1GB).
16. **CONTRARIAN JUDGE** - MMS requires 1 judge arguing AGAINST majority opinion.
17. **TOOLBOX GC** - Quarterly: delete unused(90+ days AND <5 uses), non-critical only.

---

## **II. SPEC DESIGN DISCIPLINE** (18-27)

**Requirements before implementation**
18. Test plan in specs - TDD verification before building.
19. Skeleton hierarchy - Map Systems/Processes/Functions.
20. Storage container plan - ONNX embeddings + SQLite/Kuzu/ChromeDB.
21. CLI contract - --input --output --verbose --mode --config standardized.
22. Dependency audit - List ALL libs + collision risk assessment.
23. Lib compatibility matrix - Test all deps together before production.
24. ZeroMQ everywhere - Message passing between atomic components.
25. Reproducibility artifacts - Intermediates saved for CICD.
26. Graceful degradation - Handle missing deps with fallbacks.
27. requirements.txt freeze - Exact versions to prevent drift.

---

## **III. LLM INTERACTION** (28-42)

**Reliable prompting/output handling**
28. No JSON output - Use answer...answer tags.
29. No markdown fences - Explicit tags only.
30. Key/value pairs one line - Simple structured format.
31. answer...answer mandatory - Clean extraction.
32. comments...comments - Separate explanation.
33. Tag extraction only - Supervisory ignores outside tags.
34. Centralized router - Never direct API calls.
35. External YAML/JSON config - Keys/models/endpoints.
36. Default model fallback - Config-defined.
37. Explicit output mode - Plain/Markdown/typed/Structured.
38. Agentic patterns - Simple/Long/Hill-climb/MMS.
39. Local model warm-up - Cold-start services only.
40. Format headers - --- OUTPUT FORMAT ---.
41. ASCII-primary - Minimal UTF-8.
42. No emojis/symbols.

---

## **IV. RESPONSE PROCESSING** (43-49)

**Normalize for reliability**
43. Strip emoticons/emojis.
44. Normalize quotes/dashes.
45. Remove non-UTF8.
46. Explicit encoding.
47. ENDREPLY signaling.
48. Max iterations.
49. Empty output termination.

---

## **V. GENERATION ORCHESTRATION** (50-61)

**Quality patterns**
50. Strip end tokens.
51. Continuation overlap.
52. Hill-climbing refinement.
53. MMS proposer-judge.
54. Parent orchestrator + atomic children.
55. Clear I/O contracts.
56. Time budget enforcement.
57. Semantic chunking.
58. Entity maps throughout.
59. Multi-stage pipelines.
60. Dedup policies.
61. Provenance metadata.

---

## **VI. ARCHITECTURE PATTERNS** (62-83)

**Production reliability**
62. No complex regex - Tags/loops/simple patterns.
63. Proactive error handling.
64. Sanitize external input.
65. Complete regeneration - No placeholders.
66. --verbose mandatory, silent default.
67. Worker polling coordination.
68. Lazy global caching.
69. Cross-platform paths.
70. ONNX-first embeddings - Avoid sentence-transformers collisions.
71. Core-first deps.
72. Data contracts.
73. Comment-first dev.
74. Explained defaults.
75. Subprocess isolation.
76. Cost monitoring.
77. Retry/backoff.
78. State persistence.
79. ZeroMQ locking.
80. Ensemble consensus.
81. Atomic testing.
82. Edge case coverage.
83. Lib collision testing.

---

## **VII. PRODUCTION OPERATIONS** (84-106)

**Testing (84-87)**
84. Contract testing.
85. Edge cases.
86. CICD artifacts.
87. TDD integration.

**Security (88-93)**
88. Prompt injection defense.
89. Secrets vault.
90. Rate limiting.
91. Audit trail.
92. RBAC.
93. Input validation.

**Observability (94-97)**
94. Structured logging.
95. Metrics collection.
96. Distributed tracing.
97. Health checks.

**Operations (98-106)**
98. Containerization.
99. Config as code.
100. Graceful rollback.
101. Blue-green deployment.
102. Capacity planning.
103. Disaster recovery.
104. Incident response.
105. Performance benchmarking.
106. Technical debt tracking.

---

## **VIII. MANDATORY SPEC TEMPLATE** (10 Sections)

Every technical specification must include these sections:

```
1. SYSTEMS OVERVIEW
   - 3-5 atomic systems

2. STORAGE PLAN
   - SQLite tables/schema
   - ONNX Vector DB/Kuzu/ChromeDB needs
   - NO sentence-transformers

3. DEPENDENCY MATRIX
   - Core: Python stdlib/ONNX Runtime/ZeroMQ
   - AVOID: sentence-transformers collisions

4. SCRIPT HIERARCHY
   - Parent → Atomic Children

5. CLI CONTRACTS
   - Standardized flags (--input --output --verbose --mode --config)

6. TEST PLAN
   - TDD + 7 edge cases:
     * TEST_001_INFINITE_IDLE
     * TEST_002_TOOLBOX_POISON  
     * TEST_003_KERNEL_STORM
     * TEST_004_META_ESCALATION
     * TEST_005_DISK_EXHAUSTION
     * TEST_006_JUDGE_COLLUSION
     * TEST_007_BOOTLOADER_DEATH

7. ZeroMQ IPC PLAN
   - Message bus architecture
   - IPC protocols and patterns

8. FAILURE SAFEGUARDS (V5)
   - Triple fallback chain: v6→v5→v1
   - Sandbox checklist: <30s, <512MB, no-net
   - Budgets: LLM=100/day, builds=3/day, toolbox=1GB
   - GC policy: 90days+<5uses quarterly
   - Contrarian judge: weekly rotation schedule

9. COGNITIVE THREADS (V6 Firebird)
   - TTD table schema + relationship graph
   - Cognitive thread lifecycle
   - Emotional tone tracking

10. FIREBIRD SAFEGUARDS (V6)
    - Mirror thresholds (risk ≥80%)
    - Second Mind audit requirements
    - Performance Governor limits
    - Relationship cascade rules
```

---

## **IX. FIREBIRD MANDATES** (107-112)

**V6 Cognitive OS Requirements**

107. **FIRESCRIPT REQUIRED** - toolbox192+.exe format, YAML contracts only
108. **SECOND MIND EVERY TASK** - Audit vs TTD intent (193), <90% → retry/ask
109. **TTD PERSISTENCE** - SQLite cognitive_threads table mandatory (194)
110. **MIRROR MODE ≥80% RISK** - Pre-simulate ethical/emotional impact (195)
111. **WINDOWS 11 NATIVE** - .exe only, no Python subprocess, PowerShell bootstrap
112. **COGNITIVE HYGIENE** - Thread decay, relationship cascades, weekly meta-rules review

---

## **X. V5 DEPENDENCY RULES**

**Core Dependencies (Required)**
```
ONNX Runtime       - Embeddings without collisions
SQLite/Kuzu/ChromeDB - Free, embedded, reliable
ZeroMQ             - Battle-tested IPC
Python stdlib      - Maximize built-in usage
```

**Avoided Dependencies (Known Issues)**
```
sentence-transformers - KNOWN lib conflicts/crashes → AVOID
Complex regex libs    - Use simple patterns instead
Heavy ML frameworks   - ONNX models preferred
Cloud-only services   - Local-first architecture
```

**Dependency Approval Checklist**
- [ ] No known collisions with existing deps
- [ ] License compatible (MIT/Apache/BSD preferred)
- [ ] Actively maintained (commits within 6 months)
- [ ] Cross-platform support (Windows/Linux/macOS)
- [ ] Minimal transitive dependencies
- [ ] Test coverage >80%
- [ ] Security scan passed

---

**Document Metadata:**

- **Version:** 3.2
- **Last Updated:** 2025-12-05
- **Total Rules:** 112
- **Target:** Agentic coding systems + human developers
- **Related:** meta_architecture.txt, bootstrapping_specification.txt, feature_list.txt
