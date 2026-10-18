``` ASCII
+-----------------------------------------------------------------------+
|                 TIER 1: Epistemic & Attentional Gating                |
|      (Filtering Noise, Isolating Axioms, Logit-Masking/GCD Bounds)    |
+-----------------------------------------------------------------------+
                                   |
                                   v
+-----------------------------------------------------------------------+
|                 TIER 2: Structural Decomposition                      |
|       (Step-Back Abstraction, Macro-Outlining, Task Sequencing)       |
+-----------------------------------------------------------------------+
                                   |
                                   v
+-----------------------------------------------------------------------+
|                 TIER 3: Non-Linear State Search                       |
|     (Branching Paths, Heuristic Evaluation, Backcasting Strategy)     |
+-----------------------------------------------------------------------+
                                   |
                                   v
+-----------------------------------------------------------------------+
|             TIER 4: Reflexive Verification & Alignment                |
|   (Claim Auditing, Pre-Mortems, Metacognitive Human Interrupts/HITL)  |
+-----------------------------------------------------------------------+
                                   |
                                   v
+-----------------------------------------------------------------------+
|             TIER 5: Dynamic Execution, Offloading & Lifecycle         |
|  (Dynamic DAG Assembly, Symbolic Solvers/WASM, State Compression)     |
+-----------------------------------------------------------------------+

```

---

### Tier 1: Epistemic & Attentional Gating

- **1. System 2 Attentional Filtering**
    - **Objective:** Purge conversational fluff, context noise, and narrative distractors before generating reasoning traces.
    - **Prerequisites:** Raw input context.
    - **Invariant:** Only validated operational constraints advance to the active reasoning buffer.


- **2. First-Principles Deconstruction**
    - **Objective:** Strip industry idioms, analogies, and legacy assumptions down to irreducible physical, logical, or economic constants.
    - **Prerequisites:** System 2 Attentional Filtering.
    - **Invariant:** Solutions are derived strictly from surviving foundational axioms.


- **3. Negative Constraint Boundary**
    - **Objective:** Define explicit negative search spaces, forbidden tokens, illegal state transitions, and explicit anti-patterns.
    - **Prerequisites:** System 2 Attentional Filtering.
    - **Invariant:** Prevents standard default fallbacks and common hallucination pathways.


- **4. Grammar-Constrained Decoding (GCD) & Schema Scaffolding**
    - **Objective:** Enforce token-level grammars (e.g., GBNF, JSON Schema) and structural bounds (e.g., XML) to isolate meta-instructions, lock logits, and sandbox code blocks.
    - **Prerequisites:** None.
    - **Invariant:** Guarantees non-leaking, type-safe output parsing and deterministic section isolation.



---

### Tier 2: Structural Decomposition

- **5. Step-Back Abstraction**
    - **Objective:** Elevate specific queries to high-level domain principles before deriving concrete step-by-step solutions.
    - **Prerequisites:** First-Principles Deconstruction.
    - **Invariant:** Eliminates hyper-local overfitting to noisy prompt edge cases.


- **6. Skeleton-of-Thought (SoT)**
    - **Objective:** Generate a concise, non-redundant structural outline prior to expanding individual component blocks.
    - **Prerequisites:** Grammar-Constrained Decoding & Schema Scaffolding, Step-Back Abstraction.
    - **Invariant:** Decouples macro-architectural planning from micro-text generation.


- **7. Least-to-Most Decomposition**
    - **Objective:** Break monolithic problems into a strict linear sequence of sub-problems where each step consumes the verified output of the prior step.
    - **Prerequisites:** Step-Back Abstraction.
    - **Invariant:** Eliminates cognitive load compounding across complex multi-step problems.


- **8. In-Context Analogical Framing**
    - **Objective:** Force the self-generation of a solved isomorphic sub-problem before executing the target task.
    - **Prerequisites:** Step-Back Abstraction.
    - **Invariant:** Establishes explicit procedural patterns directly inside the active window.



---

### Tier 3: Non-Linear State Search

- **9. Tree-of-Thoughts (ToT) Branching**
    - **Objective:** Generate multiple distinct intermediate reasoning paths simultaneously rather than committing to a greedy single-path token decoding trajectory.
    - **Prerequisites:** Skeleton-of-Thought (SoT).
    - **Invariant:** Prevents early logic lock-in on sub-optimal paths.


- **10. State-Space Evaluation (Heuristic Scoring)**
    - **Objective:** Apply explicit value functions or quantitative heuristics to score active reasoning nodes before advancing the search.
    - **Prerequisites:** Tree-of-Thoughts (ToT) Branching.
    - **Invariant:** Enables systematic pruning of invalid or low-probability reasoning branches.


- **11. Counterfactual Perturbation**
    - **Objective:** Alter critical variables or assumptions mid-reasoning to test output stability and uncover hidden logic dependencies.
    - **Prerequisites:** State-Space Evaluation.
    - **Invariant:** Verifies robust causality over superficial correlation.


- **12. Backcasting (Inverse Horizon Planning)**
    - **Objective:** Set an idealized successful end-state as an absolute operational constraint and reason backward chronologically to derive prerequisite steps.
    - **Prerequisites:** First-Principles Deconstruction, Least-to-Most Decomposition.
    - **Invariant:** Prevents goal drift caused by forward-stepping assumption accumulation.



---

### Tier 4: Reflexive Verification & Alignment

- **13. Chain-of-Verification (CoVe)**
    - **Objective:** Generate candidate factual claims, formulate independent validation questions, answer them in isolation, and reconcile contradictions.
    - **Prerequisites:** Grammar-Constrained Decoding & Schema Scaffolding.
    - **Invariant:** Decouples claim generation from claim verification to eliminate confirmation bias.


- **14. Simulated Reflexion**
    - **Objective:** Maintain an internal error and critique log across execution steps to evaluate intermediate outputs against target constraints.
    - **Prerequisites:** Grammar-Constrained Decoding & Schema Scaffolding, State-Space Evaluation.
    - **Invariant:** Intercepts logical drift and formatting failures mid-stream before final generation.


- **15. Adversarial Red-Teaming (Pre-Mortem)**
    - **Objective:** Simulate edge-case failures, malicious inputs, or operational bottlenecks against a candidate plan prior to output commitment.
    - **Prerequisites:** Counterfactual Perturbation, Negative Constraint Boundary.
    - **Invariant:** Hardens execution pipelines against edge-case failures.


- **16. Rubric-Guided Evaluation**
    - **Objective:** Score output drafts against an explicit, weighted multi-dimensional rubric prior to final response delivery.
    - **Prerequisites:** Grammar-Constrained Decoding & Schema Scaffolding.
    - **Invariant:** Standardizes quality output criteria against non-deterministic outputs.


- **17. Metacognitive Interrupts & Ergonomic Alignment Gating**
    - **Objective:** Trigger automated Human-in-the-Loop (HITL) execution pauses during high uncertainty, SMT solver unsatisfiability, or high-risk state mutations.
    - **Prerequisites:** Simulated Reflexion, Rubric-Guided Evaluation.
    - **Invariant:** Prevents runaway computational drift and maintains human alignment on high-stakes execution steps.



---

### Tier 5: Dynamic Execution, Offloading & Lifecycle

- **18. Dynamic Skeleton-of-Thought (D-SoT)**
    - **Objective:** Dynamically evaluate incoming query complexity at runtime to discover and construct a tailored execution Directed Acyclic Graph (DAG).
    - **Prerequisites:** Skeleton-of-Thought (SoT), Simulated Reflexion.
    - **Invariant:** Avoids static overhead on simple queries while maintaining deep structure for complex tasks.


- **19. Reason and Act (ReAct Interleaving)**
    - **Objective:** Alternate sequentially between explicit linguistic reasoning steps and external environment or tool calls.
    - **Prerequisites:** Grammar-Constrained Decoding & Schema Scaffolding, Least-to-Most Decomposition.
    - **Invariant:** Prevents ungrounded, hallucinated state tracking during environment interactions.


- **20. Temporal & Contextual Anchoring**
    - **Objective:** Explicitly lock dynamic context, retrieved documents, or dynamic state variables relative to fixed temporal and spatial reference frames.
    - **Prerequisites:** System 2 Attentional Filtering.
    - **Invariant:** Prevents context drift and timeline degradation over long conversation histories.


- **21. Deterministic DAG Offloading & Symbolic Solvers**
    - **Objective:** Translate natural language specifications into a deterministic DAG and offload math, formal logic proofs, and state machines to external runtimes (`Z3`, `SymPy`, `NetworkX`).
    - **Prerequisites:** First-Principles Deconstruction, Grammar-Constrained Decoding.
    - **Invariant:** Guarantees mathematical and logical decidability, eliminating stochastic calculation and reasoning errors.


- **22. Context Lifecycle & State Compression**
    - **Objective:** Compress, roll up, or hard-purge intermediate thinking traces, reflexion logs, and raw tool outputs into minimal, high-density state payloads before advancing downstream passes.
    - **Prerequisites:** System 2 Attentional Filtering, Grammar-Constrained Decoding.
    - **Invariant:** Preserves context window headroom, eliminates "lost-in-the-middle" attention degradation, and prevents token exhaustion in multi-pass execution.



---

### Tier Matrix & Operational Dependencies

| Primitive Tier | Primitives Included | Key Architectural Function | Primary Input Dependency | Primary Output Value | Deterministic / Structural Implementation |
| --- | --- | --- | --- | --- | --- |
| **Tier 1: Epistemic Gating** | #1–#4 | Attentional filtering, axiom isolation & logit-level masking | Unstructured Context / User Prompt | Clean Invariants & Type Bounds | Logit masking (Grammar-Constrained Decoding via GBNF) & System 2 filters |
| **Tier 2: Decomposition** | #5–#8 | Macro-planning, abstraction & structural sequencing | Clean Invariants & Axioms | Executable Structure Outline | `<sot_blueprint>` & XML/JSON schema scaffolding |
| **Tier 3: Non-Linear Search** | #9–#12 | Multi-path exploration, heuristic state scoring & backcasting | Structure Outline | High-Confidence Reasoning Paths | Heuristic evaluation functions & ToT/GoT tree search state management |
| **Tier 4: Verification & Alignment** | #13–#17 | Claim verification, pre-mortems & human alignment interrupts | Candidate Reasoning Paths | Verified Logical Artifacts & Delta Summaries | Automated tests, rubric scoring matrices & HITL execution breakpoints |
| **Tier 5: Dynamic Execution & Lifecycle** | #18–#22 | Dynamic DAG assembly, symbolic offloading & state compression | Verified Logical Artifacts | Production-Ready Outputs & Minimal State | `Z3` SMT, `SymPy`, WASM sandboxing runtime & state payload compression |
