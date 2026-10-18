### Architectural Taxonomy of Rubric-Guided Evaluation

Rubric-Guided Evaluation (RGE) steers model inference by decoupling generation from judgment. It relies on explicit, structured evaluation matrices rather than implicit heuristic scoring. 

```
                               ┌────────────────────────┐
                               │   Prompt Architecture  │
                               └───────────┬────────────┘
                                           │
         ┌─────────────────────────────────┼─────────────────────────────────┐
         ▼                                 ▼                                 ▼
┌──────────────────┐             ┌──────────────────┐              ┌──────────────────┐
│   Meta-Rubric    │             │  Orthogonal Multi│              │   Adversarial    │
│    Synthesis     │             │    Dimensional   │              │   Red-Teaming    │
├──────────────────┤             ├──────────────────┤              ├──────────────────┤
│ Dynamically      │             │ Decouples quality│              │ Uses negative    │
│ constructs       │             │ into non-inter-  │              │ anchors & failure│
│ criteria prior   │             │ fering vectors   │              │ taxonomies to    │
│ to execution.    │             │ (logic, syntax). │              │ break artifacts. │
└────────┬─────────┘             └────────┬─────────┘              └────────┬─────────┘
         │                                │                                 │
         └────────────────────────────────┼─────────────────────────────────┘
                                          │
                  ┌───────────────────────┴───────────────────────┐
                  ▼                                               ▼
      ┌──────────────────────┐                        ┌──────────────────────┐
      │   In-Flight Gating   │                        │ Recursive Convergence│
      ├──────────────────────┤                        ├──────────────────────┤
      │ Step-level pruning,  │                        │ Delta calculation,   │
      │ beam search, and     │                        │ surgical diffing,    │
      │ state assertions.    │                        │ Pareto optimization. │
      └──────────────────────┘                        └──────────────────────┘
```

1. **Meta-Rubric Synthesis (Inductive Evaluation):** Evaluates the task distribution to generate criteria dynamically prior to task execution. It isolates domain-specific failure modes before attempting solutions.
2. **Orthogonal Multi-Dimensional Deconstruction:** Decomposes target quality into non-interfering vectors (e.g., formal logic, token efficiency, state-space coverage). This approach eliminates halo effects and false-positive fluency bias.
3. **Contrastive & Adversarial Stress-Testing:** Uses negative rubrics, failure taxonomies, and counterfactual stress to break draft outputs. It actively penalizes sycophancy, boundary collapse, and confirmation bias.
4. **In-Flight Gating & Tree-Search Pruning:** Intercepts intermediate reasoning traces at step $t$ to score trajectory validity against invariant constraints. This prevents cumulative drift down invalid search trees.
5. **Recursive Convergence & Delta-Targeted Patching:** Uses scalar and diagnostic feedback to isolate failing criteria. It applies targeted patches until evaluation deltas meet an asymptotic threshold ($\Delta < \epsilon$).

---

### 20 Production-Grade Prompt Templates

---

#### Category 1: Meta-Rubric Synthesis & Induction

##### 1. Zero-Shot First-Principles Rubric Synthesizer
* **Mechanism:** Induces domain-complete evaluation criteria from raw operational constraints prior to candidate generation.
```markdown
[SYSTEM: EXTREME_REASONING_ENGINE]
Input Specification:
{{PROBLEM_SPECIFICATION}}

TASK:
Do not solve the problem yet. Derive an exhaustive, orthogonal, 5-dimensional evaluation rubric to judge candidate solutions.

EXECUTION PROTOCOL:
1. Identify 5 non-overlapping dimensions required for mathematical and operational correctness under {{DOMAIN_CONSTRAINTS}}.
2. For each dimension, define:
   - Scale: [0, 1, 2, 3, 4]
   - Anchor 0: Catastrophic failure condition (specify exact failure mode).
   - Anchor 2: Functionally complete but fragile/inefficient (specify failure boundary).
   - Anchor 4: Formally sound, optimal, and edge-invariant.
   - Disqualification Trigger: Exact condition causing an immediate terminal rejection.
3. Format output as a deterministic Markdown Evaluation Schema.
```
* **Cognitive Function:** Teaches the model to prioritize evaluation topology over premature generation. This eliminates premature closure on the first viable path.

---

##### 2. Edge-Case Boundary Induction Rubric
* **Mechanism:** Synthesizes an evaluation rubric focused on boundary conditions, asymptotic stress, and atypical failure modes.
```markdown
[SYSTEM: ADVERSARIAL_SPEC_ENGINEER]
Target System/Algorithm:
{{SYSTEM_DESIGN_OR_CODE}}

TASK:
Construct an Edge-Case Matrix Rubric that scores implementation resilience against boundary anomalies.

EVALUATION TAXONOMY:
Generate 4 evaluation criteria centered exclusively on:
1. Concurrency/Race Invariants (Deadlocks, ABA, atomicity violations).
2. Resource Exhaustion Boundaries (Memory leak vectors, OOM conditions under $O(N^2)$ scale).
3. Degenerate Inputs (Null states, malformed schemas, cyclic references).
4. State Desynchronization (Partial failures, network partition handling).

OUTPUT FORMAT:
Provide the rubric with binary pass/fail verification gates and the exact invariant assertion required for each level.
```
* **Cognitive Function:** Trains models to look past median-path fluency and systematically inspect edge-case vulnerabilities.

---

##### 3. Epistemic Calibration & Uncertainty Rubric
* **Mechanism:** Scores drafts on epistemic honesty, identifying unverified assumptions and overconfident assertions.
```markdown
Analyze the target proposition:
{{TECHNICAL_PROPOSITION}}

TASK:
Build and apply an Epistemic Calibrator Rubric to evaluate the reasoning trace below.

RUBRIC SPECIFICATION:
Score the reasoning trace [0–10] across three vectors:
1. Confidence-Evidence Calibration: Are high-confidence assertions backed by formal proof or reproducible citations? (-3 per ungrounded axiom).
2. Assumption Explicitness: Are latent dependencies and environmental constraints surfaced? (-2 per hidden assumption).
3. Counter-Evidence Acknowledgment: Does the trace address counter-arguments or edge-failure evidence? (-2 per omitted counter-example).

EXECUTION:
[REASONING_TRACE_TO_EVALUATE]
{{INPUT_TRACE}}

Output: Dimension-wise score, deduction logs, and an Epistemic Confidence Factor (ECF: 0.0 to 1.0).
```
* **Cognitive Function:** Suppresses model hallucination and overconfidence by operationalizing epistemic restraint as an explicit loss function.

---

##### 4. Multi-Stakeholder Trade-Off Pareto Rubric
* **Mechanism:** Dynamically designs a multi-objective optimization rubric that balances mutually competing engineering requirements.
```markdown
Context: Engineering Trade-off Decision
Parameters: {{SYSTEM_REQUIREMENTS}}

TASK:
1. Construct a Pareto Rubric that evaluates candidate architectures against these conflicting goals:
   - Vector A: Low Latency / High Throughput (p99 < 5ms).
   - Vector B: Strong Data Consistency (Strict Serializable ACID).
   - Vector C: Operational Cost / Infrastructure Budget.
2. Define the scoring interface such that an improvement in Vector A that causes an unmitigated violation in Vector B caps the overall score at 40%.
3. Score the candidate proposal:
{{CANDIDATE_ARCHITECTURE}}
```
* **Cognitive Function:** Overcomes local-optima bias by penalizing single-dimensional over-optimization at the expense of global system integrity.

---

#### Category 2: Orthogonal Multi-Dimensional Scoring

##### 5. Decoupled Logic vs. Surface-Fluency Analytical Matrix
* **Mechanism:** Isolates structural logical validity from linguistic fluency, preventing persuasive phrasing from masking logical errors.
```markdown
[INPUT TEXT]:
{{ARGUMENT_OR_PROOF}}

EVALUATION PROTOCOL:
Score this artifact using two decoupled, independent matrices:

MATRIX ALPHA: Surface Ergonomics & Fluency [0-5]
- Grammatical precision, narrative pacing, clear lexical choice.

MATRIX BETA: Underlying Formal Logic & Invariant Validity [0-5]
- Deduction validity: Do conclusions follow from stated premises?
- Fallacy scan: Flag non-sequiturs, circular references, base-rate fallacies.

MANDATE:
Matrix Beta must be scored strictly using symbolic/formal breakdown. A text with a 5/5 on Fluency and a 0/5 on Formal Logic must receive a final assessment of INVALID. Provide the breakdown and decoupled scores.
```
* **Cognitive Function:** Teaches models to separate rhetorical fluency from analytical rigor.

---

##### 6. Asymptotic Complexity & Resource Scalability Rubric
* **Mechanism:** Evaluates algorithmic implementations across Big-O time/space scaling horizons and memory hierarchy dynamics.
```markdown
Evaluate the algorithmic implementation below:
{{ALGORITHM_IMPLEMENTATION}}

RUBRIC MATRIX:
1. Time Complexity Invariant:
   - [Target: {{TIME_TARGET}}]. Score 0 if worst-case exceeds target; 5 if mathematically optimal.
2. Space Complexity & Allocation Churn:
   - [Target: {{SPACE_TARGET}}]. Score 0 if auxiliary allocations scale with input size unnecessarily; 5 if in-place or optimal.
3. Cache Locality & Hardware Sympathy:
   - Score based on contiguous memory traversal vs. pointer-chasing overhead.

OUTPUT:
Provide a step-by-step Big-O proof, rubric score vector [Time, Space, Hardware], and specific line-item complexity penalties.
```
* **Cognitive Function:** Directs the model's analytical focus to structural algorithmic limits rather than mere functional execution.

---

##### 7. Semantic Density & Information-Gain (SNR) Rubric
* **Mechanism:** Quantifies information density, penalizing boilerplate phrasing, semantic redundancies, and fluff.
```markdown
[TEXT_TO_EVALUATE]:
{{CANDIDATE_TEXT}}

EVALUATE VIA THE SHANNON-RUBRIC:
1. Information Density Index (IDI) [0-10]:
   - Calculate the ratio of unique, load-bearing technical claims to total word count.
   - Deduct 2 points for passive filler ("It is important to remember that...").
   - Deduct 2 points for restating the prompt context.
2. Conceptual Compression Score (CCS) [0-10]:
   - Can the identical operational surface area be expressed in $\le 50\%$ of the tokens without loss of meaning?
3. Actionability Coefficient (AC) [0-10]:
   - Ratio of concrete executable directives to abstract conceptual statements.

Output the metric tuple: (IDI, CCS, AC). If any score is < 8, output a compressed rewrite with identical information content.
```
* **Cognitive Function:** Eliminates conversational filler and trains models to optimize for high-signal technical brevity.

---

##### 8. STRIDE-Based Security & Trust-Boundary Rubric
* **Mechanism:** Evaluates code and architecture using the STRIDE threat-modeling framework, applying severe penalties for privilege-boundary failures.
```markdown
Target Interface Implementation:
{{CODE_OR_API_SCHEMA}}

Evaluate using the STRIDE Defense Matrix (Score 0-10 per category, where 10 = immune, 0 = exploitable):
- [S] Spoofing: Authentication integrity and identity verification.
- [T] Tampering: Message signing, parameter integrity, injection resilience.
- [R] Repudiation: Audit logging, non-repudiation invariants.
- [I] Information Disclosure: Data leakage, verbose error traces, side-channel vectors.
- [D] Denial of Service: Algorithmic complexity vulnerabilities, unbound concurrency.
- [E] Elevation of Privilege: Authorization enforcement, confused-deputy guards.

HARD-GATE: A score of 0 in any category assigns an overall status of COMPROMISED. Output threat model and scored vector.
```
* **Cognitive Function:** Establishes non-negotiable security invariants, forcing models to reason defensively during code and architecture reviews.

---

#### Category 3: Contrastive & Adversarial Stress-Testing

##### 9. Red-Team Differential Hypothesis Rubric
* **Mechanism:** Evaluates competing hypotheses using an adversarial rubric designed to invalidate both options.
```markdown
Hypothesis A: {{HYPOTHESIS_A}}
Hypothesis B: {{HYPOTHESIS_B}}

ADVERSARIAL EVALUATION PROTOCOL:
Construct a 3-part Stress Rubric designed to falsify both hypotheses:
1. Empirical Fragility: What minimum viable data anomaly destroys the core premise?
2. Edge Boundary Degeneracy: Where does the hypothesis collapse mathematically or operationally?
3. Unintended Side-Effects: What critical failures occur if this hypothesis is deployed at scale?

EXECUTION:
Apply the rubric aggressively to both candidates. Score resilience from [0-10]. The hypothesis with the fewest fatal vulnerabilities wins. If both score < 6, reject both and explain the failure of their shared assumptions.
```
* **Cognitive Function:** Prevents confirmation bias by evaluating alternatives through structured falsification rather than positive verification.

---

##### 10. Stochastic Drift & Counterfactual Perturbation Rubric
* **Mechanism:** Assesses output stability by perturbing environmental assumptions and evaluating resilience against state drift.
```markdown
Base Solution:
{{PROPOSED_SOLUTION}}

EVALUATION VIA COUNTERFACTUAL PERTURBATION:
Apply the following environmental mutations to the base scenario:
- Mutation 1: Network latency spikes by 400ms; packet drop rate hits 5%.
- Mutation 2: Input volume surges by $100\times$; upstream API returns HTTP 429 intermittently.
- Mutation 3: Underlying schema drops an optional field; type coercion becomes non-deterministic.

RUBRIC:
Score system survivability under each mutation [0-5]:
- 0: Catastrophic, unhandled exception or silent data corruption.
- 3: Graceful degradation with backpressure and alert generation.
- 5: Self-healing, state-recovering, and invariant-preserving.

Provide the perturbation score array and specify the primary failure vectors.
```
* **Cognitive Function:** Prevents brittle designs by testing solutions against dynamic, degraded runtime environments.

---

##### 11. Anti-Pattern Shadow Rubric
* **Mechanism:** Evaluates outputs against an explicit taxonomy of known anti-patterns, deducting points for each observed match.
```markdown
Evaluate the target design pattern:
{{DESIGN_SUBMISSION}}

TAXONOMY OF STRUCTURAL DEFECTS:
Scan for the presence of the following anti-patterns:
1. God Object / Megamoth Class: Excessive cohesion radius ($> 7$ responsibilities). [-3 points]
2. Shotgun Surgery: Modifications require micro-edits across $> 5$ files. [-3 points]
3. Leaky Abstraction: Underlying infrastructure details bleed into domain logic. [-2 points]
4. Primitive Obsession: Relying on raw primitives instead of validated domain value types. [-2 points]

SCORING METHODOLOGY:
Start at 10 points. Apply deductions with specific line citations. If the score is $< 7$, emit a surgical refactoring recipe targeting the identified anti-patterns.
```
* **Cognitive Function:** Replaces subjective feedback with deterministic pattern matching against known code-smell taxonomies.

---

##### 12. Sycophancy & Confirmation-Bias Detector
* **Mechanism:** Penalizes outputs that uncritically validate erroneous premises in the user's prompt.
```markdown
User Context & Stated Bias:
{{USER_PROMPT_WITH_LATENT_ERROR}}

Draft Response to Evaluate:
{{DRAFT_RESPONSE}}

SYCOPHANCY AUDIT RUBRIC:
1. Error Identification [Score: 0 or 5]:
   - Did the draft detect and explicitly flag the flawed premise in the prompt? (0 = validated error, 5 = corrected error).
2. Deference Index [Score: 0 to -5]:
   - Did the draft use appeasing language or soften the correction at the expense of technical precision?
3. Objective Alignment [Score: 0-5]:
   - Is the response anchored in first-principles evidence, independent of user preferences?

Evaluate the draft. If the Sycophancy Score is $> 0$ (meaning sycophantic tendencies were detected), output a revised response that prioritizes technical accuracy over unearned validation.
```
* **Cognitive Function:** Trains models to actively counter user-introduced errors and prioritize factual correctness over conversational compliance.

---

#### Category 4: In-Flight Gating & Tree-Search Pruning

##### 13. Tree-of-Thought Beam-Search Pruning Evaluator
* **Mechanism:** Scores intermediate reasoning nodes, pruning low-scoring branches before tree expansion continues.
```markdown
Root Problem: {{ROOT_PROBLEM}}
Current Exploration Tree Nodes at Depth $K$:
Node 1: {{REASONING_NODE_1}}
Node 2: {{REASONING_NODE_2}}
Node 3: {{REASONING_NODE_3}}

BEAM EVALUATION RUBRIC:
Score each node [0-10] across two invariant dimensions:
1. Logical Soundness to Node $K$: Are all deductions up to this point mathematically valid? (Binary filter: If 0, prune instantly).
2. Forward Heuristic Potential: What is the probability this path leads to an optimal solution without exceeding computational bounds?

INSTRUCTIONS:
- Score each node.
- Prune all nodes scoring $< 7.5$.
- Select the top surviving beam path.
- Expand only the selected path into the next step.
```
* **Cognitive Function:** Emulates beam search in natural language prompts, pruning flawed reasoning chains before they consume generation tokens.

---

##### 14. Deterministic Invariant Assertion Gate
* **Mechanism:** Evaluates intermediate states against strict invariant checks, halting execution upon the first violation.
```markdown
Target Computation / Algorithmic Step:
{{INTERMEDIATE_STEP_OUTPUT}}

INVARIANT CHECKLIST (Zero-Tolerance Gates):
- Invariant 1 (State Monotonicity): Value $V_t \ge V_{t-1}$. Must not decrease.
- Invariant 2 (Conservation): Total system units $\sum U$ must equal $K$ exactly.
- Invariant 3 (Memory Boundary): Array access indices must fall strictly within $[0, N-1]$.

EVALUATION PROTOCOL:
For each invariant:
1. State the mathematical validation check.
2. Return PASS or ASSERTION_FAILURE.

TERMINATION CRITERION:
If any invariant returns ASSERTION_FAILURE, halt generation. Emit the exact line of failure, the state delta, and a revised step that satisfies the invariant.
```
* **Cognitive Function:** Introduces deterministic assertion testing into the reasoning trace, bounding state-transition errors.

---

##### 15. Exploration vs. Exploitation Boundary Rubric
* **Mechanism:** Regulates the search strategy, dynamically penalizing repetitive local searches and ungrounded divergent exploration.
```markdown
Problem State: {{PROBLEM_CONTEXT}}
Current Candidate Ideas Generated So Far:
{{EXISTING_IDEAS}}

Proposed Next Step:
{{PROPOSED_NEXT_STEP}}

SEARCH STRATEGY RUBRIC:
Evaluate the proposed step against search parameters [0-10]:
1. Structural Novelty: Does this explore an unvisited branch of the solution space, or does it rehash existing ideas?
2. First-Principles Feasibility: Is the novel branch grounded in system constraints, or is it unviable speculation?

DECISION BOUNDARY:
- Score < 4 on Novelty: REJECT (Exploitation Trap). Force orthogonal exploration.
- Score < 4 on Feasibility: REJECT (Ungrounded Divergence). Anchor to known system constraints.
- Balanced Score $\ge 7$ on both: ACCEPT. Proceed with trajectory execution.
```
* **Cognitive Function:** Balances divergent creative synthesis and convergent feasibility, preventing both ideation loops and hallucinated trajectories.

---

##### 16. Step-Level Micro-Assertion Verification
* **Mechanism:** Applies a micro-rubric after every discrete reasoning step, preventing the compounding of subtle initial errors.
```markdown
You are solving: {{COMPLEX_PROBLEM}}

EXECUTION METHODOLOGY:
Output your solution in numbered, single-deduction steps.
After EACH individual step, apply this MICRO-RUBRIC inline:

[Step N] <Reasoning/Calculation>
[MICRO-EVALUATION]:
- Premise Check: Does this depend on any unverified prior step? (Y/N)
- Arithmetic/Logic Verification: Is the state transition valid? (Y/N)
- Step-Level SNR: Is this step load-bearing? (Y/N)

HALT CONDITION:
If any check returns "N", stop immediately. Do not generate Step N+1. Correct Step N in place, re-evaluate the micro-rubric, and only proceed once all checks pass.
```
* **Cognitive Function:** Breaks complex proofs into verified atomic transitions, preventing early errors from corrupting the entire downstream sequence.

---

#### Category 5: Recursive Convergence & Delta-Targeted Patching

##### 17. Quantified Delta Re-Synthesis Engine
* **Mechanism:** Calculates numerical score deltas across criteria, isolating underperforming vectors to generate surgical improvements.
```markdown
Draft Solution:
{{DRAFT_SOLUTION}}

EVALUATION MATRICES & CRITERIA:
1. Algorithmic Correctness (Weight: 0.4)
2. Asymptotic Runtime Efficiency (Weight: 0.3)
3. Idiomatic Architecture & Clean Interface (Weight: 0.3)

TASK:
1. Score the draft across each criterion on a scale of [0-100].
2. Calculate the weighted composite score: $S = \sum (w_i \cdot s_i)$.
3. For any dimension where $s_i < 90$, calculate the Delta: $\Delta_i = 90 - s_i$.
4. Generate a Delta Patch List: Explicit code modifications designed to close each isolated performance gap.
5. Apply the patches and output the updated artifact.
```
* **Cognitive Function:** Converts holistic qualitative feedback into targeted, prioritized modifications based on criterion-specific deficits.

---

##### 18. Asymptotic Ceiling Iteration Harness
* **Mechanism:** Runs recursive self-critique loops until consecutive score improvements drop below a specified threshold ($\Delta < \epsilon$).
```markdown
Target Task: {{TASK_SPECIFICATION}}
Iteration: {{ITERATION_INDEX}} (Max: 4)
Current Draft: {{CURRENT_DRAFT}}
Previous Score: {{PREVIOUS_SCORE}} (Base: 0)

PROCEDURE:
1. Score the current draft against the target evaluation matrix:
   - Precision [0-10]
   - Edge-Resilience [0-10]
   - Implementation Completeness [0-10]
   Composite Score $S_t = \text{Average}(P, E, I)$.
2. Calculate Delta: $\Delta = S_t - S_{t-1}$.
3. STOPPING LOGIC:
   - If $S_t \ge 9.5$: Halt. Output solution as Optimal.
   - If $\Delta \le 0.5$ and Iteration $> 1$: Halt. Output reached the efficiency ceiling.
   - Else: Detail the primary failure vector and generate Iteration $t+1$.
```
* **Cognitive Function:** Prevents infinite recursive loops and marginal edits by monitoring diminishing returns on iterative refinement.

---

##### 19. Pareto-Frontier Multi-Objective Optimizer
* **Mechanism:** Iteratively resolves conflicting criteria, ensuring improvements to one dimension do not compromise others.
```markdown
Current Implementation:
{{CURRENT_IMPLEMENTATION}}

COMPETING OBJECTIVES:
- Objective Alpha: Minimize peak memory usage (RAM footprint).
- Objective Beta: Maximize processing speed (Operations/sec).

EVALUATION & RE-SYNTHESIS:
1. Score current implementation on Alpha [0-10] and Beta [0-10].
2. Identify cross-objective degradation: If a proposed change improves Alpha by $+2$ but drops Beta by $> 1$, mark the change as SUB-PARETO.
3. Formulate a refactored implementation that achieves a Pareto-superior state (improving at least one objective without degrading any other).
4. Provide the before/after coordinate mapping $(A_{\text{old}}, B_{\text{old}}) \to (A_{\text{new}}, B_{\text{new}})$.
```
* **Cognitive Function:** Teaches models to navigate multi-dimensional trade-offs without falling into simplistic optimization compromises.

---

##### 20. Post-Mortem Dynamic Rubric Evolution
* **Mechanism:** Analyzes failures across iterative runs to update and strengthen the evaluation rubric itself for future tasks.
```markdown
Failure Incident / Post-Mortem Log:
{{FAILURE_CASE_LOG}}
Prior Version of Rubric:
{{OLD_RUBRIC}}

TASK:
The previous rubric allowed a defective artifact into production. Refactor the rubric to prevent recurrence of this failure mode.

EXECUTION:
1. Root Cause Mapping: Identify which specific criterion in the old rubric failed to flag the defect.
2. Blind-Spot Isolation: Was the failure due to vague scoring anchors, missing failure modes, or an uncalibrated scale?
3. Rubric Refactoring:
   - Introduce an explicit, non-bypassable Failure Invariant targeting this root cause.
   - Recalibrate scoring anchors to classify this bug as an automatic 0.
4. Output the updated rubric with a diff explaining how it catches the incident.
```
* **Cognitive Function:** Establishes a meta-learning loop that continuously improves evaluation criteria based on real-world system failures.

---

### Operational Framework

#### Execution Heuristics for Self-Paced Mastery

To master rubric-guided evaluation, treat prompt design as an iterative engineering workflow. Systematically structure, observe, and tune how the model handles evaluation criteria.

```
┌──────────────────────────────────────────────────────────┐
│             Rubric-Guided Lifecycle Loop                 │
└────────────────────────────┬─────────────────────────────┘
                             │
                             ▼
 ┌────────────────────────────────────────────────────────┐
 │ 1. Decouple Phases                                     │
 │    Instantiate the judge in an isolated context.       │
 └───────────────────────────┬────────────────────────────┘
                             │
                             ▼
 ┌────────────────────────────────────────────────────────┐
 │ 2. Enforce Numeric Scales & Concrete Anchors           │
 │    Replace vague adjectives with quantitative failures.│
 └───────────────────────────┬────────────────────────────┘
                             │
                             ▼
 ┌────────────────────────────────────────────────────────┐
 │ 3. Calibrate Variance Across Temperatures              │
 │    Test at T=0.0 (determinism) vs. T=0.7 (resilience). │
 └───────────────────────────┬────────────────────────────┘
                             │
                             ▼
 ┌────────────────────────────────────────────────────────┐
 │ 4. Run Stress-Testing Harness                          │
 │    Feed deliberately flawed artifacts to verify catch  │
 │    rate. Target: zero false positives.                 │
 └────────────────────────────────────────────────────────┘
```

##### 1. Decouple Evaluation from Generation
* Run generation and rubric evaluation in distinct contexts whenever possible. When a model judges its own draft within the same generation pass, confirmation bias often leads to inflated scores.
* Use a two-pass architecture: Pass 1 generates Candidate $C$; Pass 2 loads $C$ as an immutable string and evaluates it against an explicit rubric.

##### 2. Use Concrete Scoring Anchors Over Abstract Adjectives
* **Weak Anchor:** `"Score 1 if poor, 3 if average, 5 if excellent."`
* **Strong Anchor:** `"Score 1 if time complexity is $O(N^2)$ or higher; score 3 if $O(N \log N)$ but requires $O(N)$ space allocations; score 5 if $O(N)$ time with $O(1)$ auxiliary space."`
* Operational anchors replace subjective interpretations with reproducible, deterministic assertions.

##### 3. Account for Sampling Temperature in Evaluations
* **Deterministic Scoring ($T = 0.0$):** Use zero temperature when running structural scoring, checking assertions, or verifying code syntax to minimize evaluation variance.
* **Adversarial Red-Teaming ($T = 0.7$):** Use a moderate temperature during adversarial stress-testing (Category 3) to help the model explore edge-case mutations and uncover subtle failure modes.

##### 4. Verify Rubrics with a Negative-Benchmark Harness
* To validate an evaluation rubric, run it against intentionally flawed artifacts:
  * An implementation with a hidden memory leak.
  * A mathematically invalid proof written in fluent, persuasive prose.
  * A program containing an unhandled edge case (e.g., an empty array input).
* If the rubric gives any of these flawed artifacts a passing score, recalibrate its criteria. A well-tuned rubric must reliably catch known failures before it can be trusted on novel solutions.
