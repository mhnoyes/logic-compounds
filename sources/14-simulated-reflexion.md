# Architectural Taxonomy of Simulated Reflexion

Simulated Reflexion operationalizes verbal reinforcement learning within a single inference context or orchestrated multi-turn loop. Instead of relying on parameter updates ($\Delta \theta$), it leverages a dynamic memory buffer ($\mathcal{M}$), a structured critique policy ($\mathcal{R}$), and a self-supervised adaptation policy ($\Pi_{\text{refine}}$) to iteratively eliminate epistemic blind spots, hallucinations, and structural drift.

```
       ┌────────────────────────────────────────────────────────┐
       │                   Task / Context (x)                   │
       └──────────────────────────┬─────────────────────────────┘
                                  │
                                  ▼
       ┌────────────────────────────────────────────────────────┐
┌─────►│                Actor Engine: Trial (y_t)               │
│      └──────────────────────────┬─────────────────────────────┘
│                                 │
│                                 ▼
│      ┌────────────────────────────────────────────────────────┐
│      │             Evaluator: Scalar / Rubric Gating          │
│      └──────────────────────────┬─────────────────────────────┘
│                                 │
│                   Fail          ▼          Pass
│      ┌────────────────────────────────────────┐   ┌───────────┐
│      │ Evaluator Decision: Threshold Met?     ├──►│ Canonical │
│      └──────────────────┬─────────────────────┘   │ Output    │
│                         │                         └───────────┘
│                         ▼
│      ┌────────────────────────────────────────────────────────┐
│      │        Reflector: Causal Diagnosis & Heuristic         │
│      │                Policy Extraction (r_t)                 │
│      └──────────────────────────┬─────────────────────────────┘
│                                 │
│                                 ▼
│      ┌────────────────────────────────────────────────────────┐
│      │      Episodic Memory Buffer: M_{t+1} = M_t ∪ {r_t}     │
└──────┴────────────────────────────────────────────────────────┘
```

### Taxonomy Dimensions

1. **Trace-Level Error Attribution & Causal Inversion:** Isolating the exact logical inflection point where reasoning diverged, executing counterfactual simulations to determine root cause.
2. **Dual-Agent & Dialectical Adversarial Convergence:** Pitting orthogonal objectives (e.g., speed vs. correctness, attack vs. defense) against each other to surface implicit assumptions.
3. **Rubric-Gated Multi-Pass Iteration:** Binding execution to strict quantitative criteria and deterministic invariant checks; looping until a floor score or boolean invariant is satisfied.
4. **Episodic Working Memory & Trajectory Synthesis:** Maintaining a persistent state of prior failures and distilled heuristics to prevent cyclic error states across iterations.
5. **Meta-Algorithmic Structural Self-Correction:** Self-auditing the operational framework itself, pruning cognitive load, resolving ambiguity, and validating proof trees via cross-methodological parity.

---

# 20 Production-Grade Prompt Templates

---

## Category 1: Trace-Level Error Attribution & Causal Inversion

### 1. Counterfactual Pivot Triangulation
* **Mechanism:** Pinpoints the exact semantic token or logical node where the reasoning trajectory deviated from ground truth, then generates counterfactual execution paths.
* **Mastery Target:** Teaches the model to decouple symptoms from root causes, avoiding surface-level rephrasing during self-correction.

```markdown
You are a deterministic execution engine configured with reflexive counterfactual analysis.

TASK SPECIFICATION:
Solve the following complex analytical problem:
{{PROBLEM_STATEMENT}}

EXECUTION PROTOCOL:
Phase 1: Initial Derivation (Draft 0)
- Generate a complete, end-to-end solution trace. Number every discrete logical leap as [Node X].

Phase 2: Adversarial Audit & Inflection Pinpointing
- Audit each [Node X] against physical, mathematical, or empirical laws.
- Identify the exact [Node K] where the earliest divergence, assumption violation, or calculation error occurs.
- Explicitly state:
  * Erroneous Premise at [Node K]: <precise_statement>
  * Causal Mechanism of Error: <why this mistake was committed>
  * Counterfactual State: <what must be true at Node K to preserve validity>

Phase 3: Branch Re-Execution
- Discard all downstream states [Node > K].
- Resume execution from the corrected [Node K], enforcing invariant constraints.

OUTPUT FORMAT:
<draft_zero>...</draft_zero>
<pivot_audit>
  <inflection_node>Node K</inflection_node>
  <root_cause>...</root_cause>
  <counterfactual_condition>...</counterfactual_condition>
</pivot_audit>
<canonical_execution>...</canonical_execution>
```

---

### 2. Upstream Premise Falsification Engine
* **Mechanism:** Reverses derivation flow to extract hidden axiomatic dependencies, attempting to systematically falsify them before validating downstream outputs.
* **Mastery Target:** Exposes implicit defaults and cognitive heuristics that introduce epistemic drift.

```markdown
Analyze the target proposition through reflexive premise invalidation:

TARGET:
{{PROPOSITION_OR_HYPOTHESIS}}

PIPELINE:
1. FORWARD DEDUCTION:
   Synthesize the primary argument, concluding with a structural recommendation or result.

2. AXIOM DECONSTRUCTION (Reflexion Phase):
   Extract the top 3 implicit foundational axioms underpinning your forward deduction.
   For each axiom:
   - Construct a high-probability boundary condition under which this axiom collapses.
   - Trace the downstream fallout on the primary argument if the axiom is nullified.

3. RESILIENT SYNTHESIS:
   Reconstruct the final argument such that it either survives axiom nullification or defines explicit validity boundaries.

Present your trace within <deduction>, <axiom_falsification>, and <hardened_output> tags.
```

---

### 3. Latent Assumption Boundary Stress-Testing
* **Mechanism:** Stress-tests edge cases against latent variables (scale, concurrency, extreme boundary inputs) to induce intentional failure, feeding failures back into system design.
* **Mastery Target:** Teaches preemptive edge-case discovery in distributed systems, financial modeling, and algorithmic design.

```markdown
System Architecture/Logic Under Analysis:
{{SYSTEM_LOGIC}}

Execute a 3-Cycle In-Context Stress Reflexion:

[CYCLE 1: NAIVE IMPLEMENTATION]
Provide an optimal implementation assuming standard enterprise operational bounds.

[CYCLE 2: EDGE-CASE DESTRUCTION (Simulated Evaluator)]
Subject Cycle 1 to the following stress dimensions:
a) Asymptotic Input Scale ($N \to \infty$)
b) Zero/Null/Pathological Input Structures
c) Byzantine/Adversarial Interventions
Detail the exact mechanism of failure for each dimension.

[CYCLE 3: REFLEXIVE PATCHING]
Formulate a "Failure Catalog" mapping each breakdown from Cycle 2 to its architectural patch. 
Produce the finalized implementation integrating all defensive patches.
```

---

### 4. Deterministic Invariant Preservation Loop
* **Mechanism:** Enforces zero-tolerance invariant rules (e.g., memory safety, transactional idempotency, formal logic rules) via a deterministic loop.
* **Mastery Target:** Replaces probabilistic generation with rule-bounded correctness enforcement.

```markdown
Perform the following technical task while maintaining strict invariant enforcement:
TASK: {{TASK_SPECIFICATION}}

MANDATORY INVARIANTS:
1. {{INVARIANT_1}} (e.g., strictly O(1) auxiliary space)
2. {{INVARIANT_2}} (e.g., zero modification of input arrays)
3. {{INVARIANT_3}} (e.g., thread-safe state synchronization)

EXECUTION MATRIX:
[ATTEMPT 1]
Generate candidate solution.

[INVARIANT AUDIT]
Build a verification matrix checking Attempt 1 against each invariant:
| Invariant | Pass/Fail | Formal Verification/Proof of Compliance |
If any invariant evaluates to FAIL, state the precise source of non-compliance.

[REFLEXIVE CORRECTION]
If failed, state the architectural change required to enforce the violated invariant without regressing passing invariants. Re-implement until all invariants evaluate to PASS.

Produce output labeled with <attempt_1>, <invariant_audit>, and <final_hardened_solution>.
```

---

## Category 2: Dual-Agent & Dialectical Adversarial Convergence

### 5. Multi-Specialist Consensus Auction
* **Mechanism:** Simulates distinct agent personas with contradictory optimization functions, resolving competing designs through a consensus auction.
* **Mastery Target:** Teaches trade-off optimization between orthogonal performance metrics (e.g., latency, cost, reliability).

```markdown
DOMAIN SCENARIO:
{{SCENARIO_DESCRIPTION}}

Instantiate three competing personas to evaluate and optimize the solution:
- Persona A: The Ultra-Reliability SRE (Prioritizes zero-downtime, fault tolerance, defensive fallback).
- Persona B: The Latency/Performance Purist (Prioritizes bare-metal execution speed, minimal overhead, non-blocking I/O).
- Persona C: The Economic Pragmatist (Prioritizes unit economics, operational complexity minimization, ROI).

ORCHESTRATION:
Step 1: Persona A, B, and C each submit their independent solutions to the scenario.
Step 2: Adversarial Cross-Critique: Each persona identifies the fatal architectural flaw in the other two proposals.
Step 3: Reflexion Synthesis: Act as the Lead Enterprise Architect. Review the cross-critiques, extract non-negotiable requirements, and build a unified design reconciling the trade-offs.

Output format must isolate <independent_proposals>, <adversarial_critique>, and <unified_synthesis>.
```

---

### 6. Formal Red-Team Infiltration / Blue-Team Hardening
* **Mechanism:** Explicitly alternates between attacker and defender postures to iteratively strip vulnerabilities out of code, logic, or policy.
* **Mastery Target:** Builds intuition for attack surface modeling and zero-trust protocol design.

```markdown
TARGET SPECIFICATION (Protocol, Policy, or API Spec):
{{TARGET_SPEC}}

Run an alternating 4-Step Red/Blue Reflexion Loop:

STEP 1: BLUE TEAM (Initial Deployment)
Draft the baseline design/protocol securing the asset.

STEP 2: RED TEAM (Exploit Generation)
Identify three distinct attack vectors (e.g., race condition, authorization bypass, logic flaw).
For each vector, provide a functional exploit payload or scenario.

STEP 3: BLUE TEAM (Reflexive Mitigation)
Analyze the structural vulnerability exposed by each exploit. 
Reflect on why the Step 1 baseline permitted these surfaces to exist.
Design explicit mitigation mechanisms for each vector.

STEP 4: ZERO-TRUST PRODUCTION SPEC
Produce the hardened specification along with regression test proofs for each resolved vector.
```

---

### 7. Extreme Edge Pessimist vs. Pragmatic Synthesizer
* **Mechanism:** Forces an extreme adversarial critic to systematically break the generator's confidence, driving the synthesizer to justify every line of output.
* **Mastery Target:** Eliminates sunny-day cognitive bias from technical and strategic decision-making.

```markdown
PROPOSED STRATEGY / ARCHITECTURE:
{{INPUT_PLAN}}

Execute the Dialectic Pressure Engine:

ROUND 1: The Generator
Draft the complete, optimistic rollout/execution strategy.

ROUND 2: The Malicious Critic
Assume malicious compliance, catastrophic dependencies, and cascading environmental failures.
- Enumerate 5 critical failure modes that would cause total collapse.
- Rate the probability and impact of each failure mode.
- Highlight specific statements in Round 1 that are fatally naive.

ROUND 3: Reflexive Pivot & Re-Synthesis
- Address each failure mode directly.
- Segregate the plan into: (a) Inherent risks to be mitigated, (b) Structural flaws requiring redesign, and (c) Acceptable tail-risks with fallback tripwires.
- Output the fully adjusted, disaster-resilient plan.
```

---

### 8. The Auditor-Driven Zero-Trust Policy Engine
* **Mechanism:** Employs an external auditor model to verify legal, regulatory, or formal compliance, denying execution until clear proof is established.
* **Mastery Target:** Teaches alignment of creative/generative problem solving with compliance constraints (e.g., GDPR, HIPAA, SEC).

```markdown
REGULATORY & COMPLIANCE FRAMEWORK:
{{COMPLIANCE_STANDARDS}} (e.g., SOC2, GDPR, HIPAA, Basel III)

PROPOSED ACTION / IMPLEMENTATION:
{{SYSTEM_ACTION}}

Execute the following Reflexion Protocol:

1. COMPLIANCE DISCOVERY:
   Draft the implementation plan for the proposed action.

2. THE REGULATORY INQUISITOR (Reflexion Sub-Routine):
   Audit the implementation strictly against the standards.
   Flag every violation using the format:
   - Clause: [Standard X.Y]
   - Violation Vector: [Exact mechanism of non-compliance]
   - Severity: [Critical/High/Medium]
   - Remediation Mandate: [What the architecture must drop or add]

3. CERTIFIED IMPLEMENTATION:
   If violations exist, discard non-compliant segments. Rewrite the implementation so that it passes a zero-trust audit without diminishing the core utility.
   Provide an audit-ready compliance matrix alongside the final implementation.
```

---

## Category 3: Rubric-Gated Multi-Pass Iteration

### 9. Multi-Dimensional Likert Threshold Convergence
* **Mechanism:** Assigns scalar evaluations across independent quality vectors, terminating the iterative loop only when every dimension crosses a target threshold ($S \ge \tau$).
* **Mastery Target:** Trains prompt designers to enforce strict quality gates instead of relying on stochastic variance.

```markdown
OBJECTIVE:
{{TASK_DESCRIPTION}}

QUALITY RUBRIC (Target Threshold: $\ge 9/10$ across all axes):
- Axis 1: Logical Rigor (Axiomatic precision, absence of non-sequiturs)
- Axis 2: Technical Conciseness (Signal-to-noise ratio, absence of filler)
- Axis 3: Edge-Case Coverage (Robustness under boundary conditions)
- Axis 4: Actionability (Deterministic execution clarity)

ALGORITHM:
Run Iteration $t=1$:
1. Produce Output Candidate $Y_t$.
2. Self-Score Candidate across Axis 1-4 with explicit justifications.
3. Compute Convergence Condition: If $\min(\text{Scores}) < 9$:
   - Generate Reflexion Delta $\Delta_t$: Detail the precise operational adjustments needed for sub-9 axes.
   - Run Iteration $t+1$ incorporating $\Delta_t$.
4. Terminate when $\forall \text{Axis}, \text{Score} \ge 9$.

Format with explicit XML tags: `<iteration_1>`, `<audit_1>`, `<reflexion_delta_1>`, etc., terminating in `<converged_solution>`.
```

---

### 10. Information Density & SNR Compression Loop
* **Mechanism:** Repeatedly rewrites technical content to maximize information density while monitoring semantic preservation.
* **Mastery Target:** Mastering high-leverage prompt construction, executive briefings, and minimal-overhead LLM system instructions.

```markdown
RAW SOURCE MATERIAL:
{{SOURCE_TEXT_OR_SPEC}}

Apply the Reflexive Density Compression Engine:

PASS 1: Raw Functional Extraction
Extract all core semantic claims, mathematical invariants, and operational mandates into an uncompressed draft. Compute baseline word count.

PASS 2: Entropy Audit & Loss Analysis (Reflexion Step)
- Identify all conversational padding, redundant adjectives, and structural scaffolding.
- Measure Semantic Loss Risk: Which words can be deleted without losing functional specificity?
- Identify opportunities to replace multi-word descriptions with formal domain nomenclature.

PASS 3: High-Density Compression
Produce a compressed version achieving at least a 50% token reduction from Pass 1.

PASS 4: Reconstruction Parity Verification
Audit Pass 3 against Pass 1. Can the complete, original system logic be fully reconstructed from Pass 3 alone without ambiguity? If NO, restore the minimum necessary tokens. Output the finalized high-SNR artifact.
```

---

### 11. Code Complexity & Cyclomatic Pruning Loop
* **Mechanism:** Generates baseline code, calculates structural complexity metrics, reflects on algorithmic debt, and rewires the code toward optimal time/space boundaries.
* **Mastery Target:** Program synthesis, refactoring, and deterministic algorithmic optimization.

```markdown
ALGORITHMIC REQUIREMENT:
{{PROBLEM_STATEMENT}}

LANGUAGE & CONSTRAINTS:
{{LANGUAGE_AND_CONSTRAINTS}}

EXECUTION RUNBOOK:

[STEP 1: WORKING DRAFT]
Generate an idiomatic, correct solution. Ensure functional correctness over optimization.

[STEP 2: STATIC COMPLEXITY REFLEXION]
Analyze the Step 1 code:
- Asymptotic Complexity: Calculate exact Big-O for Time and Space.
- Branching Complexity: Estimate Cyclomatic Complexity (count conditionals, nested loops).
- Memory Allocation: Identify hidden allocations, object cloning, or cache misses.
- Bottleneck Node: Identify the single most expensive operation in the runtime path.

[STEP 3: ALGORITHMIC RE-FACTORING]
Reflect: How can the dynamic state be represented differently to drop the time/space complexity class, or eliminate branch divergence?
Implement the production-grade, optimized solution with documented complexity proofs.
```

---

### 12. The Popperian Falsification Engine
* **Mechanism:** Formulates an analytical hypothesis, generates targeted tests designed specifically to break the hypothesis, and updates the core thesis based on failure modes.
* **Mastery Target:** Scientific reasoning, hypothesis-driven product development, and root-cause debugging.

```markdown
CORE HYPOTHESIS / INVESTIGATION:
{{PROBLEM_HYPOTHESIS}}

Apply the Popperian Reflexion Protocol:

PHASE 1: Theory Formalization
State the hypothesis as a collection of testable, deterministic assertions.

PHASE 2: Falsification Design (Evaluator)
Design 3 critical experiments or tests specifically engineered to disprove the hypothesis. 
For each test, define the "Falsification Threshold"—the exact observation that decisively proves the hypothesis false.

PHASE 3: Simulated Execution & Reflexive Adaptation
Simulate the outcome of these tests against extreme empirical or logical realities.
- If a test triggers the Falsification Threshold, declare the hypothesis invalid.
- Document the causal reason for the failure.
- Mutate the hypothesis into an updated version that accounts for the observed limitation.

PHASE 4: Validated Theory Formulation
Output the revised, empirically resilient model, accompanied by its defined boundaries of validity.
```

---

## Category 4: Episodic Working Memory & Trajectory Synthesis

### 13. Rolling Reflexion Buffer Across Multi-Trial Convergence
* **Mechanism:** Maintains a persistent memory buffer $\mathcal{M}$ containing explicit trial histories: trial actions, critiques, and derived operational heuristics.
* **Mastery Target:** Emulates agent architectures like Shinn et al. within a single prompt, preventing cyclic reasoning errors.

```markdown
TASK:
{{COMPLEX_OPTIMIZATION_TASK}}

You have an episodic memory buffer $\mathcal{M}$. You will execute up to 3 iterative trials to solve this task.

Initialize Memory: $\mathcal{M}_0 = \emptyset$

---
[EXECUTION LOOP TEMPLATE]
For Trial $t \in \{1, 2, 3\}$:

1. Policy Execution:
   Attempt the task, using the rules stored in $\mathcal{M}_{t-1}$.
   Label output as: <trial_t>

2. Evaluator Inspection:
   Audit <trial_t> against edge-case correctness and optimization bounds.
   Identify every failure, sub-optimality, or drift.
   Label output as: <critique_t>

3. Reflexion & Memory Update:
   Formulate a high-leverage operational heuristic $h_t$ that prevents the observed failure.
   Update memory: $\mathcal{M}_t = \mathcal{M}_{t-1} \cup \{h_t\}$.
   Label output as: <memory_state_t>

Terminate the loop early if <critique_t> identifies zero flaws. 
Output the finalized, canonical result with the complete trace of $\mathcal{M}$.
```

---

### 14. Negative Example Distillation (Anti-Pattern Registry)
* **Mechanism:** Collects all observed failure modes into an explicit negative registry, training the system to avoid recurring anti-patterns.
* **Mastery Target:** Eliminates regression loops in complex multi-step reasoning.

```markdown
GOAL:
{{OBJECTIVE_DESCRIPTION}}

CONSTRAINTS:
{{SYSTEM_CONSTRAINTS}}

PHASE 1: EXPLORATORY ATTEMPTS
Generate two radically different approaches to solving the goal.

PHASE 2: ANTI-PATTERN EXTRACTION (Reflexion)
Analyze both approaches from Phase 1. Identify the structural anti-patterns, inefficient conventions, or latent vulnerabilities present in either attempt.
Extract these into an "Anti-Pattern Registry":
| Anti-Pattern Name | Where it appeared | Why it is sub-optimal | Prohibition Rule |
|-------------------|-------------------|------------------------|------------------|

PHASE 3: SHADOW-PREVENTATIVE EXECUTION
Synthesize the final, canonical solution.
Explicitly demonstrate that zero items from the Anti-Pattern Registry appear in the final solution design.
```

---

### 15. Dual-Memory Semantic Consolidation
* **Mechanism:** Separates ephemeral working scratchpads from durable operational guidelines, mimicking human memory consolidation.
* **Mastery Target:** Preserves coherence over long contexts by preventing memory buffer saturation.

```markdown
INPUT CONTEXT & TASK:
{{LONG_CONTEXT_TASK}}

You possess two explicit memory architectures:
1. Working Scratchpad (Ephemera: Scratch calculations, discarded paths, intermediate checks).
2. Long-Term Consolidated Heuristic Store (Durable: Absolute truths, systemic invariants, immutable design choices).

EXECUTION PROTOCOL:
Step 1: Execute Attempt 1 on the Working Scratchpad. Show raw derivations, rough modeling, and partial outputs.
Step 2: Memory Consolidation Routine (Reflexion Engine):
   - Review the Working Scratchpad.
   - Strip out 100% of the noise, false paths, and intermediate metrics.
   - Distill the core successful insights into the Durable Store as numbered axioms: [AX-1], [AX-2], etc.
Step 3: Flush the Working Scratchpad entirely.
Step 4: Execute the final solution, referencing exclusively the axioms from the Durable Store.

Present in clear segments: `<working_scratchpad>`, `<consolidation_event>`, `<durable_store>`, and `<final_execution>`.
```

---

### 16. Heuristic Policy Gradient Extraction
* **Mechanism:** Quantifies the performance difference between two distinct iterations and abstracts that difference into an explicit decision heuristic for future steps.
* **Mastery Target:** Teaches dynamic in-context policy improvement and systematic reasoning optimization.

```markdown
SYSTEM UNDER TRANSFORMATION:
{{TARGET_SYSTEM_OR_TEXT}}

TASK: Maximize throughput and clarity according to these criteria: {{METRIC_CRITERIA}}

TRAJECTORY:
1. BASELINE RUN:
   Execute an initial baseline version of the task.

2. GRADIENT MEASUREMENT (Evaluator Step):
   - Identify the top 3 friction points in the baseline.
   - Propose an explicit modification vector for each friction point.

3. REFINED RUN:
   Execute the modified version applying those vectors.

4. POLICY GRADIENT EXTRACTION (Reflexion Step):
   Reflect on the performance delta between the Baseline and Refined Run.
   Formulate a Generalized Policy Directive:
   $\Delta\Pi = \text{Condition} \implies \text{Optimal Transformation}$
   Write out the generalized rules that explain why the Refined Run outperformed the Baseline.

5. MASTER PROTOCOL:
   Generate the final production artifact governed explicitly by $\Delta\Pi$.
```

---

## Category 5: Meta-Algorithmic Structural Self-Correction

### 17. Self-Supervised Consistency Parity Engine
* **Mechanism:** Implements two completely different methodologies (e.g., iterative vs. recursive, deductive vs. empirical) to solve the same problem, reflecting on discrepancies between their outputs.
* **Mastery Target:** Teaches verification of complex logic and code via dual-track synthesis without relying on ground-truth external labels.

```markdown
PROBLEM TO RESOLVE:
{{HARD_PROBLEM}}

Execute Dual-Track Execution and Parity Reflexion:

[TRACK 1: First-Principles Deductive Path]
Solve the problem through formal deductive derivation, step by step. State the final output as: Result_1.

[TRACK 2: Inductive / Empirical Simulation Path]
Solve the exact same problem using a distinct cognitive framework (e.g., simulation, extreme boundary testing, heuristic approximation, or inversion). State the final output as: Result_2.

[PARITY AUDIT (The Reflexion Engine)]
Compare Result_1 and Result_2.
- Do they match? (YES/NO)
- If NO:
  * Map the diverging execution steps between Track 1 and Track 2.
  * Which track suffered from an invalid assumption or precision loss?
  * Root cause analysis of the divergence.
- If YES:
  * Audit whether both tracks share a common hidden assumption (collusive failure mode).

[CANONICAL RECONCILIATION]
Output the reconciled, fully verified answer based on the parity audit.
```

---

### 18. Cognitive Load & Ambiguity Disambiguation
* **Mechanism:** Forces the model to pause before task completion to evaluate its own semantic uncertainty and flag ambiguous assumptions.
* **Mastery Target:** Prevents premature problem-solving on under-specified inputs; teaches requirement engineering.

```markdown
INCOMING AMBIGUOUS BRIEF:
{{UNCLEAR_OR_COMPLEX_USER_PROMPT}}

EXECUTE PRE-EMPTIVE AMBIGUITY REFLEXION:

STEP 1: INTENT DECONSTRUCTION
Parse the input. Identify:
- Explicit Requirements: What is strictly specified?
- Latent Ambiguities: What critical specifications are missing?
- Hidden Traps: What interpretations could lead to completely different implementations?

STEP 2: BIFURCATION MAPPING (Reflexion Phase)
Develop the two most probable conflicting interpretations of this brief:
- Interpretation Alpha: [Premise, Target Audience, Functional Goal]
- Interpretation Beta: [Premise, Target Audience, Functional Goal]
Analyze the trade-offs and operational risks of selecting Alpha over Beta.

STEP 3: THE DEFENSIVE EXECUTION
Formulate the optimal implementation. Explicitly prefix your solution with the selected interpretation path and document why that path was chosen over alternatives.
```

---

### 19. Recursive Formal Proof Verification & Rollback
* **Mechanism:** Operates like a proof-assistant kernel: systematically checks each line of reasoning against upstream lemmas, rolling back to the parent state upon detecting any non-sequitur.
* **Mastery Target:** Formal mathematical derivation, structural system design, and rigorous policy construction.

```markdown
THEOREM / LOGICAL CLAIM TO PROVE OR DISPROVE:
{{CLAIM}}

EXECUTE PROOF-CHECKER REFLEXION:

Initialize State: Step 0 (Premise)

LOOP:
Step $N$:
- State the derived assertion.
- Formal Warrant: What explicit axiom, rule of inference, or prior step validates this assertion?

PROOF-AUDITOR (In-Line Reflexion):
- Check Step $N$: Does it follow soundly from the declared warrant?
- If INVALID:
  * FLAG: Invalid inference detected at Step $N$.
  * ROLLBACK: Revert state back to Step $N-1$.
  * REFLECT: Explain why the rejected step failed.
  * BRANCH: Provide an alternative valid inference path.
- If VALID:
  * Advance to Step $N+1$.

Execute the proof until the claim is definitively confirmed or disproved. Conclude with a complete, clean proof trace.
```

---

### 20. Meta-Prompt Self-Evolution Engine
* **Mechanism:** Treats the user's prompt as an unoptimized software system, executing the task, reflecting on input limitations, and rewriting the prompt itself into a production-grade template.
* **Mastery Target:** Meta-prompt engineering, prompt evaluation frameworks, and automated LLM pipeline construction.

```markdown
ORIGINAL INPUT PROMPT:
{{BASE_PROMPT}}

GOAL: Optimize both the execution output and the prompt itself through structural Reflexion.

PHASE 1: BASELINE EXECUTION
Run the original prompt as written. Evaluate the quality of the output.

PHASE 2: META-PROMPT AUDIT (Reflexion Engine)
Critique the original prompt across these vectors:
- Specificity & Constraint Hardening
- Edge-Case Inoculation
- Structural Delimiters & Cognitive Scaffolding
- Cognitive Load: Does the prompt ask for too much unstructured work in a single step?

PHASE 3: META-PROMPT COMPILATION
Rewrite the original prompt into a production-grade template that integrates automated self-correction, strict semantic delimiters, and verification gates.

PHASE 4: SUPERIOR RE-RUN
Execute the newly compiled prompt from Phase 3 on the original input domain, demonstrating the resulting quality improvement.
```

---

# Operational Framework: Execution Heuristics for Self-Paced Mastery

To master, adapt, and run these simulated reflexion templates effectively, apply the following operational mechanics.

### 1. Structural Delimitation & State Isolation
* **Failure Mode:** "Bleed-Through"—the model hallucinates that its previous attempt was correct, causing the Reflector to praise flawed work (sycophancy) rather than critically auditing it.
* **Mitigation:** Use strict structural enclosures (e.g., XML blocks like `<trial_k>`, `<evaluator>`, `<reflexion_buffer>`). Treat these blocks as separated variables in an execution runtime.

### 2. The Evaluator-Actor Temperature Decoupling Heuristic
* **Single-Call In-Context:** When using single-turn prompts (e.g., Prompts 1, 9, 17), force the prompt to switch operational modes via role tags. The Evaluator persona must be instructed to adopt a distinct cognitive posture (e.g., "Assume the prior step contains a subtle flaw; your task is to isolate it").
* **Multi-Turn Pipelines:** Run the Actor at higher temperatures ($\tau \approx 0.7$) to ensure exploratory diversity across hypotheses, while running the Evaluator and Reflector at lower temperatures ($\tau \approx 0.0\text{--}0.2$) to ensure deterministic, critical auditing.

### 3. Avoiding Semantic Pseudo-Reflection
* **Failure Mode:** The model produces generic reflective text (e.g., *"I will try harder to be concise and accurate"*) without changing its downstream reasoning trajectory.
* **Mitigation:** Constrain the reflection phase to operational delta statements:
  $$\Delta = \{\text{Identified Defect}\} \to \{\text{Root Cause}\} \to \{\text{Actionable Constraint Mutation}\}$$
  Require the subsequent trial to explicitly cite the constraint mutation before running its derivation.

### 4. Telemetry: Measuring Reflexion Efficacy
When evaluating whether a prompt template is working as intended, monitor these three diagnostic metrics:
1. **Divergence Factor:** Does the text in `Trial N+1` meaningfully depart from `Trial N` in structure and logic, or is it merely a lexical rewrite?
2. **Error Isolation Rate:** Does the Evaluator successfully identify genuine logical inflection points, or does it focus on trivial stylistic adjustments?
3. **Monotonic Metric Improvement:** When tracking quantitative rubrics (e.g., Prompt 9), do scores advance monotonically toward the threshold, or does fixing one issue trigger regressions elsewhere?
