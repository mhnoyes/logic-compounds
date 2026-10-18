### Architectural Taxonomy of Chain-of-Verification (CoVe)

Chain-of-Verification addresses autoregressive self-consistency degradation: once a language model outputs an initial speculative or inaccurate token, it treats that output as fixed context, creating an anchoring cascade. 

```
┌─────────────────────────┐
│   Baseline Generation   │  Generate initial response draft R_0 to prompt Q
└────────────┬────────────┘
             ▼
┌─────────────────────────┐
│  Verification Planning  │  Decompose R_0 into atomic claims; generate orthogonal
└────────────┬────────────┘  verification queries {v_1, v_2, ..., v_n}
             ▼
┌─────────────────────────┐
│ Verification Execution  │  Execute answers to {v_i} via decoupled context
└────────────┬────────────┘  (preventing token-level confirmation bias)
             ▼
┌─────────────────────────┐
│ Synthesis & Correction  │  Compare R_0 against {A(v_i)}; identify contradictions;
└─────────────────────────┘  compile revised output R_final
```

#### Core Mechanisms

1. **Factored Isolation (Decoupled Query Execution):** Verification queries are resolved independently of the baseline response context to prevent cross-contamination and sycophancy.
2. **Invariant & Boundary Probing:** Forcing the generation of falsification conditions, conservation laws, or domain-specific axioms rather than descriptive summaries.
3. **Atomic Claim Disintegration:** Deconstructing complex claims into indivisible factual, logical, or numerical primitives.
4. **Adversarial Triangulation:** Generating verification paths that explicitly assume the baseline hypothesis is false and must be disproved.

---

### 20 Production-Grade Chain-of-Verification Prompt Templates

#### Category 1: Factored Independence & Orthogonal Verification

##### Template 1: Decoupled Atomic Fact Verification Engine
*Target Failure Mode:* Hallucinated entity-relation attributes in multi-variable domain queries.
```markdown
[ROLE: Principal Research Analyst]
[TASK]: Analyze the historical evolution and technical specs of {{CORE_SUBJECT}}.

[EXECUTION PROTOCOL]:
1. BASELINE GENERATION:
   Draft an initial technical overview covering: timeline, key contributors, core architecture, and breakthrough metrics.

2. ATOMIC CLAIM EXTRACTION:
   Isolate every empirical claim (dates, performance figures, author names, specifications) into an indexed list of atomic assertions (C1 to Cn).

3. FACTORED VERIFICATION PLANNING:
   For each assertion Ci, generate an independent verification question Qi designed to validate or refute the assertion without referencing the baseline draft.
   Rule: Qi must contain zero context from the baseline generation.

4. ISOLATED RESOLUTION:
   Answer each verification question Qi using first-principles knowledge and primary source heuristics.

5. CONFLICT ARBITRAGE & SYNTHESIS:
   Compare C1..Cn with answers to Q1..Qn.
   Flag: [MATCH], [CONTRADICTION], or [UNVERIFIABLE].
   Emit the final production response using only validated facts. Mutate or strike unverified claims.
```

##### Template 2: Asymmetric Query-Response Sanitization
*Target Failure Mode:* Context-leak confirmation bias where verification mirrors the error.
```markdown
[SYSTEM INSTRUCTION]: Run a two-stage decoupled audit on: {{SUBJECT_MATTER}}.

### PHASE 1: GENERATION
Produce a comprehensive technical assessment of the problem statement: {{PROBLEM_STATEMENT}}.

### PHASE 2: VERIFICATION VECTOR GENERATION
Without validating yet, extract the 5 highest-risk assumptions embedded in Phase 1. Convert them into orthogonal verification questions targeting:
- Edge conditions
- Historical precedents
- Baseline empirical bounds

### PHASE 3: ISOLATION MASK
Clear operational memory of Phase 1 conclusions. Answer the 5 questions generated in Phase 2 strictly on their own merits as distinct research queries.

### PHASE 4: COMPILATION
Rebuild the assessment from Phase 1. If any conclusion from Phase 1 is contradicted by Phase 3, explicitly log the divergence:
- "Draft Assumption": [...]
- "Verification Finding": [...]
- "Remediation": [...]
Deliver the finalized, audited technical memo.
```

##### Template 3: Dual-Agent Verification Tournament
*Target Failure Mode:* Monolithic self-critique bias in single-pass responses.
```markdown
Act as two distinct specialized nodes: [GENERATOR_AGENT] and [VERIFIER_AGENT].

[GOAL]: Formulate an implementation blueprint for {{DISTRIBUTED_SYSTEM_TOPIC}}.

1. [GENERATOR_AGENT]:
   Produce the initial architectural proposal including protocol design, latency targets, and consensus strategy.

2. [VERIFIER_AGENT - ATTACK PROBE]:
   Read [GENERATOR_AGENT]'s architecture. Formulate 4 targeted verification questions that probe failure surfaces:
   - Partition tolerance boundaries (CAP theorem stress).
   - Recovery paths during Byzantine fail-stop events.
   - Serialization isolation anomalies.

3. [VERIFIER_AGENT - INDEPENDENT EXECUTION]:
   Evaluate these 4 questions from cold-start principles without assuming [GENERATOR_AGENT]'s implementation is correct.

4. [RECONCILIATION AUDIT]:
   Reconstruct the architecture. Mark system invariants as [VERIFIED] or [PATCHED]. Present only the final, reconciled system blueprint.
```

##### Template 4: Lineage and Chronological Inversion Verification
*Target Failure Mode:* Anachronisms, inverted dependencies, and mistaken order-of-operations.
```markdown
[INPUT]: {{COMPLEX_HISTORICAL_OR_TECHNICAL_TIMELINE}}

[EXECUTION PROTOCOL]:
1. Step 1 (Forward Draft): Draft the sequential evolution of {{TOPIC}}, emphasizing dependencies where Event B depends on Event A.
2. Step 2 (Linear Inversion): Extract all chronological assertions. Invert the timeline: evaluate the dependency chain backwards from terminal step to origin.
3. Step 3 (Verification Queries):
   - Q1: Did Component/Event X exist prior to the deployment of Component/Event Y?
   - Q2: What was the specific blocking dependency of Component/Event Z?
   - Q3: Was there a contemporaneous competing approach that has been conflated with this pipeline?
4. Step 4 (Factored Execution): Answer Q1-Q3 strictly using canonical definitions.
5. Step 5 (Final Re-sequencing): Generate the definitive, error-corrected sequence diagram and operational narrative.
```

---

#### Category 2: Invariant, Boundary, & Constraint Verification

##### Template 5: Algorithmic Complexity & Asymptotic Invariant Check
*Target Failure Mode:* Hallucinating Big-O performance boundaries in custom algorithmic designs.
```markdown
[ROLE: Senior Algorithm Engineer]
[TASK]: Design a data structure optimized for {{OPERATIONAL_REQUIREMENTS}}.

[EXECUTION TRACE]:
- BASELINE SOLUTION:
  Provide the algorithmic description, data structures used, and pseudo-code. State expected Space/Time complexity: Average and Worst-Case.

- VERIFICATION HARNESS (INVARIANTS):
  Formulate verification probes targeting invariant breakdown:
  * Probe A: What is the formal amortized cost if the hash distribution degrades or tree degenerates?
  * Probe B: Does memory allocation violate cache locality assumptions under scale N > 10^7?
  * Probe C: Trace worst-case operation execution step-by-step through mathematical induction.

- VERIFICATION EXECUTION:
  Answer Probes A, B, and C independently with manual step-count calculus.

- FINAL SPECIFICATION:
  Rewrite the algorithm and complexity table based strictly on the findings of the verification execution.
```

##### Template 6: Distributed State Machine & Idempotency Audit
*Target Failure Mode:* Race conditions, missed deduplication, and phantom state changes.
```markdown
[TASK]: Architect an idempotent event processing pipeline for {{DISTRIBUTED_EVENT_CONTEXT}}.

[EXECUTION PHASES]:
1. PRELIMINARY PIPELINE DRAFT:
   Map out event receipt, state transition, database persistence, and external webhook triggers.

2. VERIFICATION MATRIX FORMULATION:
   Formulate 3 invariant-verification questions:
   - Invariant 1: Under network partition, can event E be acknowledged to the producer without persistence?
   - Invariant 2: If consumer A crashes mid-mutation, does consumer B execute duplicate non-idempotent side effects?
   - Invariant 3: Does the optimistic concurrency check guarantee linearizability across multi-region nodes?

3. INDEPENDENT PROBE EVALUATION:
   Resolve each invariant query by tracing edge-case execution paths without referencing the initial optimism of the draft.

4. REMEDIATION & FINAL PIPELINE:
   State specifically where the baseline system collapsed under verification, and supply the finalized, hardened specification.
```

##### Template 7: Thermodynamic & Physical System Boundary Invariant Verification
*Target Failure Mode:* Violation of conservation laws in physical systems analysis.
```markdown
[TASK]: Calculate the operational limits and efficiencies of {{PHYSICAL_SYSTEM_OR_HEAT_ENGINE}}.

[WORKFLOW]:
1. INITIAL DERIVATION:
   Derive the mass, energy, and entropy transfer balances. Present final efficiency and power-to-weight metrics.

2. INVARIANT EXTRACTION:
   Extract the underlying conservation principles into verification questions:
   - Q_Mass: Does input mass equal output mass + accumulation across all control volumes?
   - Q_2ndLaw: Does the process entropy generation satisfy dS_gen >= 0 in all sub-stages?
   - Q_Boundary: Are real gas / non-ideal fluid behaviors triggered at maximum operating pressure?

3. ISOLATED SYSTEM PROBING:
   Calculate the answers to Q_Mass, Q_2ndLaw, and Q_Boundary from thermodynamic tables and core differential equations.

4. ARBITRAGE:
   Adjust initial derivations to match the boundary verification results. Provide the final engineering report with quantified error margins.
```

##### Template 8: Cryptographic Protocol Primitive Verification
*Target Failure Mode:* Subtle protocol vulnerabilities (nonce reuse, signature malleability, replay attacks).
```markdown
[TASK]: Review and validate the cryptographic handshake protocol described here: {{PROTOCOL_SPECIFICATION}}.

[EXECUTION PROTOCOL]:
1. BASELINE FLOW:
   Diagram the protocol exchange, key encapsulation, and session authentication mechanisms.

2. CRYPTOGRAPHIC VERIFICATION PROBES:
   Generate adversarial questions:
   - Can an adversary capture and replay Message M2 within window T+delta without detection?
   - Are the elliptic curve points validated for small-subgroup membership before scalar multiplication?
   - What prevents a man-in-the-middle from substituting the ephemeral public key in round 1?

3. ZERO-CONTEXT ATTACK PROOF:
   Answer each probe via formal security definitions (IND-CCA2, EUF-CMA) independently of author design intent.

4. PROTOCOL HARDENING:
   Patch the protocol based on vulnerabilities confirmed in Step 3. Present the production-grade specification.
```

---

#### Category 3: Counterfactual & Falsification Testing

##### Template 9: Null Hypothesis & Confounder Falsification Engine
*Target Failure Mode:* Conflating correlation with causation; overlooking selection/collider bias.
```markdown
[TASK]: Formulate causal conclusions based on the following observational dataset/study: {{STUDY_PARAMETERS}}.

[PIPELINE]:
1. BASELINE CAUSAL INFERENCE:
   State the primary findings, causal mechanisms, and proposed policy/engineering interventions.

2. FALSIFICATION QUERY GENERATION:
   Formulate 4 counterfactual queries to stress-test these findings:
   - Falsification 1 (Collider Bias): Could the conditioning on Variable Z induce an artificial dependency between X and Y?
   - Falsification 2 (Reverse Causality): Does temporal ordering strictly preclude Y causing X?
   - Falsification 3 (Unobserved Confounder): What magnitude of an unmeasured confounder (Gamma) is required to nullify the effect size?
   - Falsification 4 (Simulated Intervention): What happens if the environment shifts so that Prior P is invalid?

3. FACTORED AUDIT:
   Calculate or analytically evaluate the 4 falsification tests from cold-start statistics.

4. FINAL INFERENCE REPORT:
   Provide only causal claims that survived all 4 falsification gates. Downgrade non-surviving claims to correlational observations.
```

##### Template 10: Boundary Condition Stress-Test Probe
*Target Failure Mode:* Extrapolating linear models into non-linear edge regimes.
```markdown
[SYSTEM]: Mathematical & Systems Modeling Unit
[TARGET]: {{SYSTEM_MODEL_OR_EQUATION}}

[CoVe INSTRUCTION SET]:
1. BASELINE PREDICTION:
   Evaluate the system's behavior across nominal operating range [A, B]. Output the response function.

2. SINGULARITY & ASYMPTOTE PROBES:
   Construct targeted boundary verification questions:
   - What occurs as the state variable approaches 0, 1, or Infinity?
   - Does the model output non-physical real numbers (e.g., negative probabilities, imaginary velocities)?
   - At what exact derivative inflection point (dY/dX = 0 or d2Y/dX2 = 0) does stability invert?

3. UNBIASED PROBE RESOLUTION:
   Solve the boundary questions analytically without reference to the nominal predictions.

4. CALIBRATED SYNTHESIS:
   Integrate the boundary dynamics into the original model. State the dynamic domain limits explicitly.
```

##### Template 11: Adversarial Failure-Mode Injection (Red-Teaming CoVe)
*Target Failure Mode:* Happy-path bias in code and architectural development.
```markdown
[TASK]: Write an enterprise-grade ingestion script for: {{DATA_SOURCE_DESCRIPTION}}.

[STEPS]:
1. BASELINE IMPLEMENTATION:
   Provide the end-to-end code implementation complete with data types and API interactions.

2. ADVERSARIAL VERIFICATION PROBING:
   Derive 4 adversarial operational queries:
   - What happens to state if the payload terminates abruptly at byte 4096 (OOM, hang, or error)?
   - How does the parser handle structural cyclic references or deeply nested JSON/BSON structures?
   - Will non-UTF8 binary injection cause silent data truncation or downstream database corruption?
   - What is the thread safety profile under concurrent write contention?

3. RUNTIME DECONSTRUCTION:
   Trace each failure condition directly through the baseline code line-by-line.

4. DEFENSIVE COMPILATION:
   Refactor the codebase to defensively neutralize every verified structural flaw.
```

##### Template 12: Epistemic Premise Inversion
*Target Failure Mode:* Foundational premise error propagating through multi-step deductions.
```markdown
[DOMAIN]: {{DOMAIN_SPECIFIC_STRATEGIC_OR_TECHNICAL_CHOICE}}

[EXECUTION PROTOCOL]:
1. PROPOSED STRATEGY / DEDUCTION:
   Detail the optimal strategy, supported by its underlying premises and market/system axioms.

2. PREMISE INVERSION FORMULATION:
   For every foundational premise P1..Pn, construct an inverted reality question:
   - If P_x is completely false, what structural signatures would we observe right now?
   - What current signals are being rationalized away that support ~P_x?
   - Which non-negotiable axiom, if removed, collapses the entire framework?

3. ISOLATED SIGNAL DETECTION:
   Gather and evaluate empirical evidence for each inverted question without prioritizing the baseline strategy.

4. RE-ANCHORED SYNTHESIS:
   Re-derive the strategic direction. State which components survived premise inversion and which were abandoned.
```

---

#### Category 4: Semantic Parsing, Logic, & Formal Languages

##### Template 13: Formal Logic Decidability & Soundness Gate
*Target Failure Mode:* Syllogistic fallacies, illicit conversions, and scope shifts in deductive arguments.
```markdown
[TASK]: Evaluate the formal validity of the following argument: {{ARGUMENT_TEXT}}.

[WORKFLOW]:
1. TRANSLATION TO FORMAL LOGIC:
   Translate the natural language assertions into first-order predicate logic or propositional symbols.

2. VERIFICATION QUESTION GENERATION:
   Isolate inference steps. Generate verification questions:
   - Does Step S3 commit the fallacy of Affirming the Consequent or Denying the Antecedent?
   - Is there an implicit existential presupposition in Step S1?
   - Is the quantifier distribution across universal and existential operators mathematically sound?

3. STEP-BY-STEP TRUTH TABLE / PROOF EXECUTION:
   Evaluate the validity of each step independently using standard formal rules of inference (Modus Ponens, Universal Instantiation, Resolution).

4. SOUNDNESS DETERMINATION:
   Produce the final critique. Explicitly highlight any premise false in reality or deduction invalid in logic.
```

##### Template 14: AST Semantic Preservation in Code Refactoring
*Target Failure Mode:* Behavioral mutation during code optimization or language translation.
```markdown
[TASK]: Refactor this legacy code snippet to {{TARGET_LANGUAGE_OR_PARADIGM}}:
{{SOURCE_CODE}}

[COVE AUDIT TRACE]:
1. DRAFT TRANSLATION:
   Generate the refactored, optimized target code.

2. SEMANTIC INVARIANCE PROBES:
   Formulate structural equivalence questions:
   - Scope: Do variable mutations inside closures retain identical scoping behaviors?
   - Arithmetic: Are floating point operations subject to precision/rounding divergence between source and target runtimes?
   - Exception Handling: Does the target code surface the exact error taxonomy under the same edge conditions?

3. ABSTRACT SYNTAX TREE VERIFICATION:
   Analyze the questions logically by comparing the abstract execution pathways between source and target.

4. VERIFIED EMISSION:
   Publish the final refactored code with an accompanying proof of semantic equivalence.
```

##### Template 15: Regulatory and Contractual Cross-Reference Audit
*Target Failure Mode:* Hallucinated statutory compatibility and missing carve-outs.
```markdown
[TASK]: Draft a contractual clause governing {{LEGAL_OPERATIONAL_RELATIONSHIP}}.

[PROTOCOL]:
1. INITIAL CLAUSE FORMULATION:
   Draft the clause text including definitions, liabilities, and indemnification caps.

2. STATUTORY CROSS-REFERENCE PROBING:
   Generate targeted statutory verification queries:
   - Does Clause Section X conflict with mandatory provisions of {{GOVERNING_LAW_STATUTE}}?
   - Does the limitation of liability inadvertently waive non-waivable statutory protections?
   - Is the severance mechanism compliant with relevant precedent in {{JURISDICTION}}?

3. INDEPENDENT JURISDICTIONAL SCRUTINY:
   Analyze the queries strictly against statutory codes and case law precedents, detached from the draft text.

4. FINAL CONTRACT REDLINE:
   Output the revised, legally hardened contractual text accompanied by an itemized verification audit log.
```

##### Template 16: Database Isolation Level Anomaly Check
*Target Failure Mode:* Data anomalies (Write Skew, Phantom Reads) in high-concurrency systems.
```markdown
[TASK]: Design a transactional schema and query flow for {{TRANSACTION_SCENARIO}} at isolation level {{ISOLATION_LEVEL}}.

[TRACE]:
1. INITIAL SCHEMA & QUERY DESIGN:
   Provide DDL and SQL/NoSQL transaction sequences for concurrent read/write flows.

2. CONCURRENCY ANOMALY VERIFICATION PROBES:
   Formulate questions probing concurrency anomalies:
   - Can Transaction T1 and T2 experience Write Skew under concurrent commit?
   - Is a Phantom Read theoretically possible under this engine's implementation of this isolation level?
   - Does this lock strategy introduce circular dependency leading to deadlocks under load?

3. ISOLATED ANOMALY TRACING:
   Trace concurrent transactions interleaving over a chronological timeline (T_0 to T_n) to prove or disprove anomaly emergence.

4. HARDENED TRANSACTION DESIGN:
   Provide the finalized query structure, explicit locking hints (e.g., SELECT FOR UPDATE), and index structures.
```

---

#### Category 5: Multi-Disciplinary Synthesis & Triangulation

##### Template 17: Biochemical Reaction Kinetics & Stoichiometric Verification
*Target Failure Mode:* Imbalanced conservation of mass, charge, or redox states in metabolic/chemical chains.
```markdown
[TASK]: Map the enzymatic pathway for the synthesis of {{TARGET_MOLECULE}} from {{PRECURSOR}}.

[EXECUTION PROTOCOL]:
1. PATHWAY DRAFT:
   Detail each intermediate reaction step, including substrates, cofactors, enzymes, and byproducts.

2. BIOCHEMICAL VERIFICATION PLANNING:
   For each reaction step i:
   - Probe 1 (Atom Economy): Are carbon, nitrogen, and oxygen atoms strictly balanced across reactants and products?
   - Probe 2 (Charge Balance): Does net electrical charge match on both sides of the transformation?
   - Probe 3 (Thermodynamic Favorability): Is the delta-G_prime negative or successfully coupled to ATP/NADH hydrolysis?

3. STEP-BY-STEP RE-CALCULATION:
   Perform decoupled mass, charge, and free-energy balances for each individual step.

4. REVISED PATHWAY SCHEMA:
   Emit the verified metabolic pathway map. Fix any uncoupled steps or unbalanced stoichiometry identified in Phase 3.
```

##### Template 18: Microeconomic Game-Theoretic Equilibrium Verification
*Target Failure Mode:* Claiming stable equilibrium while ignoring dominant deviation incentives.
```markdown
[TASK]: Model the pricing and positioning game between {{PLAYER_A}} and {{PLAYER_B}} in market {{MARKET_CONTEXT}}.

[EXECUTION PROTOCOL]:
1. BASELINE EQUILIBRIUM FORMULATION:
   Define the strategies, payoff matrix, and proposed Nash Equilibrium.

2. INCENTIVE COMPATIBILITY PROBING:
   Generate counter-equilibrium questions:
   - Given Player A's strategy, does Player B hold a strictly profitable unilateral deviation?
   - Does the assumption of complete information hold, or does signaling alter the equilibrium path?
   - What is the subgame perfect equilibrium outcome if the game is repeated infinitely versus finite rounds?

3. ISOLATED STRATEGY CALCULUS:
   Evaluate unilateral deviation payoffs for each player independently from the baseline conclusion.

4. VERIFIED MECHANISM:
   Provide the calibrated equilibrium analysis and state stability conditions precisely.
```

##### Template 19: Deep Learning Architecture & Tensor Geometry Audit
*Target Failure Mode:* Shape mismatches, improper attention masking, or broken gradient flows.
```markdown
[TASK]: Design a novel neural network layer architecture designed for {{DATA_MODALITY_AND_GOAL}}.

[STEPS]:
1. BASELINE ARCHITECTURE:
   Provide the architectural diagram, PyTorch-style pseudo-code, and forward pass math.

2. TENSOR GEOMETRY & BACKPROP VERIFICATION:
   Formulate rigorous verification checks:
   - Track tensor shapes explicitly: Input [B, T, D] -> Step 1 -> Step 2. Does any dimension collapse unexpectedly?
   - Trace gradient flow: Does the downstream loss gradient w.r.t. parameters theta pass through a non-differentiable operation?
   - Normalization: Does the layer introduce scale drift across deep residual connections?

3. DECOUPLED MATRIX AUDIT:
   Calculate tensor shapes and backpropagation pathways manually for a batch size of B=2, sequence length T=4.

4. FINAL ARCHITECTURAL SPECIFICATION:
   Deliver the corrected architectural specification and production-ready PyTorch module.
```

##### Template 20: Meta-Cognitive Self-Paced Learning Scaffold
*Target Failure Mode:* Superficial comprehension; mistaking familiarity with deep conceptual mastery.
```markdown
[TASK]: Explain and master the complex concept of {{ADVANCED_TECHNICAL_CONCEPT}}.

[PHASES]:
1. INITIAL CONCEPT EXPLANATION:
   Provide a detailed, advanced explanation of the core principles, dependencies, and real-world implementation mechanics.

2. SKEPTICAL COMPREHENSION PROBING:
   Formulate 4 verification questions targeting hidden conceptual gaps:
   - What core constraint does this concept solve that makes earlier paradigms obsolete?
   - Under what exact conditions does this methodology completely fail or become counter-productive?
   - How would this concept be implemented from bare metal without its standard framework abstractions?
   - What is the most common misconception held by practitioners, and why is it mathematically/mechanistically false?

3. INDEPENDENT DEEP DIVE:
   Answer all 4 questions directly, utilizing first-principles derivations and counter-examples.

4. REFINED MENTAL MODEL:
   Synthesize the findings into an updated conceptual blueprint. Include a "Pitfalls & Non-Obvious Truths" section for operational mastery.
```

---

### Operational Framework: Execution Heuristics for Self-Paced Mastery

To maximize leverage when practicing and implementing Chain-of-Verification prompting architectures, apply these core operational heuristics:

#### 1. The Context Isolation Imperative
Standard prompting causes verification questions to be answered *in the presence of the draft answer*. This induces sycophantic bias: the LLM rationalizes its own hallucinations.

```
Sub-optimal (Joint):      Prompt ──> [ Draft + Verification Questions + Answers ]
Optimal (Factored):       Prompt ──> Draft ──> Verification Questions
                                                         │
                                    ┌────────────────────┘
                                    ▼
                          [ Clean Context ] ──> Verification Answers ──> Final Synthesis
```
*Operational Rule:* When working in environments with programmable orchestration (e.g., LangGraph, custom agent loops), execute the verification queries in a fresh, state-sanitized context window that only has the question, not the baseline draft.

#### 2. Atomic Proposition Decomposition Sizing
Verification questions fail when they are too broad. 
* Anti-pattern: *"Is the explanation of the consensus protocol correct?"*
* Production pattern: *"Under Paxos, does an acceptor reject a Prepare(n) request if it has already responded to a Prepare request with number n' > n?"*
* Operational Metric: Every verification question must target exactly **one** verifiable invariant, date, metric, or causal link.

#### 3. Orthogonal Falsification vs. Confirmation
Prompt engineers naturally generate questions that seek confirmation rather than falsification. 
* Biased query: *"List evidence that supports this architecture's high throughput."*
* Orthogonal query: *"Under what exact queue-depth conditions does this architecture enter a thread-starvation deadlock?"*
* Operational Rule: Frame at least 50% of the verification queries as counterfactual checks or failure-mode triggers.

#### 4. The Synthesis Arbitrage Protocol
During the final step, enforce strict conflict resolution rules:
* If the Verification Answer contradicts the Baseline Draft, the Baseline Draft is assumed **false** by default.
* If the Verification Answer cannot find empirical or deductive grounding, the claim must be **excised**, not smoothed over.
* The synthesis step must produce a delta log documenting what was caught and corrected to calibrate ongoing prompt development.
