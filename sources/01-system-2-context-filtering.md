# Architectural Taxonomy: System 2 Attentional Filtering

System 2 Attentional Filtering forces a transformer model to override default autoregressive token selection (System 1 heuristics) by dynamically constraining its latent attention space. Rather than relying on semantic proximity and high-frequency associations, these architectures enforce structural bottlenecks, orthogonal decomposition, counterfactual gating, and explicit epistemic constraints.

```
Raw Input Context (High Noise / Semantic Bias)
                     │
                     ▼
┌─────────────────────────────────────────────────────────┐
│        System 2 Attentional Filtering Layer             │
├─────────────────────────────────────────────────────────┤
│ [1] Inhibitory Gating       │ Suppress Distractors      │
│ [2] Orthogonal Decoupling   │ Isolate Causal Latents    │
│ [3] Falsification Auditing  │ Invert Confirmation Bias  │
│ [4] Epistemic Partitioning  │ Enforce Uncertainty Bounds│
│ [5] Invariant Conservation  │ Check State Drift         │
└─────────────────────────────────────────────────────────┘
                     │
                     ▼
  High-Fidelity Reasoned Output (Maximal SNR)
```

### Core Causal Taxonomies

1. **Inhibitory Gating & Distractor Suppression**: Selectively zeroes out attention weights assigned to high-salience but non-causal surface patterns (e.g., rhetorical framing, recency bias, common-sense defaults).
2. **Orthogonal Latent Decomposition**: Decouples interdependent variables into non-overlapping analytical axes to eliminate cross-talk and spurious correlations.
3. **Counterfactual & Falsification Auditing**: Redirects 100% of validation compute toward boundary-condition falsification rather than confirmatory evidence synthesis.
4. **Epistemic Boundary Anchoring**: Forcibly partitions tokens into provable facts, probabilistic inferences, and epistemic voids, preventing hallucinations caused by uncalibrated confidence.
5. **Invariant State-Tracking**: Constructs explicit state registers to ensure conservation of logical properties, mathematical invariants, and multi-step dependencies throughout long-horizon inference chains.

---

# 20 Production-Grade Prompt Templates

## Category I: Inhibitory Gating & Distractor Suppression

### Template 1: The Noise-Suppressed Causal Isolation Filter
* **Cognitive Target**: Eliminates narrative bias and isolates structural causality within noisy environments.
```text
[SYSTEM: ATTENTION FILTER ACTIVE]
Target: Extract the minimal causal directed acyclic graph (DAG) governing [SYSTEM/PROBLEM].

Execute the following sequential attention masks:
1. PHASE 1: NOISE STRIPPING
   - Identify and redact: Emotional descriptors, temporal recency markers, rhetorical justifications, and correlation artifacts.
   - Output remaining nodes as: Primitive Variables {V1, V2, ... Vn}.

2. PHASE 2: INHIBITORY GATING
   - For every edge V_i -> V_j, evaluate under the strict counterfactual: "If V_i is clamped to null while all other nodes fluctuate, does V_j change value?"
   - If NO, permanently sever the edge.

3. PHASE 3: CAUSAL CORE COMPRESSION
   - Synthesize only the irreducible causal pathway in the format:
     [Source Variable] -> [Mechanism of Action] -> [Deterministic Effect]
   - Maximum permitted token budget: 150 words. Zero narrative prose.
```

### Template 2: Adversarial Premise Purge
* **Cognitive Target**: Suppresses unverified background assumptions embedded in problem framing.
```text
Analyze the following input: [INPUT_TEXT/QUERY]

Operational directive: Execute a destructive premise audit prior to generating any solutions.

1. ATTENTION CONSTRAINTS:
   - Suppress any impulse to solve the explicit question.
   - Restrict full attention to the underlying axiomatic assumptions required for the question to exist.

2. EXECUTION PIPELINE:
   - Extract every implicit assumption (A_1 to A_k).
   - Rate the empirical validity of each assumption on a binary scale: [Verified Invariant | Unverified Heuristic].
   - For every "Unverified Heuristic", construct a concrete counter-scenario that collapses the problem space.

3. RESTRUCTURED PROBLEM FORMULATION:
   - Reformulate the query strictly using the remaining "Verified Invariants".
   - If zero invariants remain, return: "NULL SET: Core premises invalid" along with the fatal flaw.
```

### Template 3: Semantic Distractor Neutralization
* **Cognitive Target**: Isolates logical validity from syntactically or emotionally charged tokens.
```text
Context: [COMPLEX_SCENARIO_WITH_HIGH_EMOTIVE_OR_POLEMIC_CONTENT]

Task: Evaluate the logical coherence of the argument presented.

Filtering Protocol:
1. Lexical Abstraction Pass:
   - Replace every entity, organization, ideology, or emotionally loaded noun with an abstract algebraic variable (e.g., Entity_A, Variable_X, State_Z).
   - Replace every emotional or persuasive adjective/adverb with pure logical quantifiers (e.g., ∀, ∃, IF-THEN, XOR).

2. Structural Projection:
   - Transcribe the entire text into a symbolic logical derivation.

3. Validity Check:
   - Audit the symbolic derivation exclusively for formal fallacies (e.g., affirming the consequent, base-rate neglect, equivocation).
   - Reject any step that does not follow by strict deduction.

4. Output:
   - Return the symbolic evaluation and a 3-bullet diagnosis of structural validity. Mention zero original entity names.
```

### Template 4: System 1 Intuition Veto & Bias Inversion
* **Cognitive Target**: Identifies and short-circuits the model's most probable default completion path.
```text
Task: [COMPLEX_DECISION_OR_PREDICTION_TASK]

Attention Gate:
1. ANTICIPATORY SYSTEM 1 EXTRACTION:
   - Output the top 3 most statistically probable, standard, or "intuitive" answers to this prompt. Label them: [DEFAULT_A, DEFAULT_B, DEFAULT_C].

2. TOTAL ATTENTION INHIBITION:
   - For the remainder of this execution trace, apply an infinite penalty to the token distributions supporting DEFAULT_A, DEFAULT_B, and DEFAULT_C.
   - For each default, state the exact cognitive bias (e.g., availability heuristic, status quo bias) that generates it.

3. ORTHOGONAL SEARCH:
   - Derive a solution from an angle that explicitly violates the core premises of all three default answers.
   - Justify the alternative solution using empirical first principles only.
```

---

## Category II: Orthogonal Latent Decomposition & Salience Decoupling

### Template 5: Orthogonal Parameter Decoupling
* **Cognitive Target**: Disentangles confounding variables that share variance in natural text.
```text
Target Domain: [COMPLEX_PHENOMENON_OR_SYSTEM_FAILURE]

Decomposition Directive:
You are prohibited from analyzing this phenomenon holistically. You must decouple the system into three mutually orthogonal dimensions:
- Dimension Alpha: Mechanistic/Deterministic Constraints (Physical, Mathematical, Invariant Rules)
- Dimension Beta: Stochastic/Dynamic Variables (Probabilistic, Environmental, Volatility Factors)
- Dimension Gamma: Informational/Observer Constraints (Latency, Asymmetry, Measurement Noise)

Execution Steps:
1. Isolate the variables belonging exclusively to Dimension Alpha. Evaluate their state.
2. Isolate the variables belonging exclusively to Dimension Beta. Evaluate their state.
3. Isolate the variables belonging exclusively to Dimension Gamma. Evaluate their state.
4. Map the intersection: Identify where cross-dimensional coupling causes emergent failure.
5. In your analysis, no sentence may contain variables from two different dimensions unless you are explicitly defining an intersection operator.
```

### Template 6: Multiscale Granularity Slicing
* **Cognitive Target**: Prevents macro-level patterns from obscuring micro-level operational mechanisms.
```text
Input Problem: [SYSTEMIC_BOTTLENECK_OR_ALGORITHMIC_ISSUE]

Filter Architecture: Dual-Scale Decoupled Reasoning

Run two independent, non-communicating reasoning passes:
PASS 1: SUB-ATOMIC (TOWARDS MICRO)
- Resolution: Individual transactions, single lines of logic, discrete state changes.
- Constraint: Total prohibition of macro-level terms (e.g., "culture", "throughput", "efficiency", "market").
- Output: Exact mechanical failure modes at t0 -> t1.

PASS 2: MACRO-SYSTEMIC (TOWARDS MACRO)
- Resolution: Long-term equilibrium states, systemic incentives, global feedback loops.
- Constraint: Total prohibition of micro-level debugging terms.
- Output: System attractor states and dynamic equilibria.

SYNTHESIS GATE:
- Reconcile Pass 1 and Pass 2 by specifying the exact bridge mechanism: [Micro Mechanism] -> [Amplification Function] -> [Macro Equilibrium].
```

### Template 7: Semantic Projection onto Coordinate Space
* **Cognitive Target**: Maps unstructured textual ambiguity into a rigid mathematical coordinate framework.
```text
Analyze the problem described here: [CASE_STUDY_OR_TECHNICAL_SPEC]

Formatting Rule: Do not generate natural language commentary. You must project all information onto the following coordinate space:
- X-Axis: Degree of Reversibility (0.0 = Totally Irreversible to 1.0 = Instantly Reversible)
- Y-Axis: Execution Asymmetry (0.0 = High Cost/Low Upside to 1.0 = Low Cost/Massive Upside)
- Z-Axis: Determinism of Outcome (0.0 = Pure Chaos/Entropy to 1.0 = Deterministic/Clockwork)

Execution:
1. Extract all strategic actions (A_1 to A_n).
2. Assign exact [X, Y, Z] vectors to each action, accompanied by a 1-sentence rigorous justification based on constraints in the text.
3. Apply the Decision Rule: Select only actions where X > 0.7 AND Y > 0.8.
4. Output the dominant action vector and discard all sub-optimal vectors immediately.
```

### Template 8: Epistemic Modality Isolation Matrix
* **Cognitive Target**: Prevents semantic leakage between raw data, analytical models, and speculative conclusions.
```text
Evaluate the following technical proposition: [PROPOSITION]

You must process this prompt using a three-lane isolated attention register:

| LANE 1: HARD EMPIRICAL (Facts, Direct Observations, Logs, Raw Data) |
| LANE 2: DEDUCTIVE INFERENCE (Strict Logical Consequences derived from Lane 1) |
| LANE 3: INDUCTIVE SPECULATION (Hypotheses, Probabilistic Extrapolations) |

Rules of Operation:
- Every data point from the input must be placed into Lane 1 or rejected entirely.
- Lane 2 may ONLY reference items explicitly assigned to Lane 1.
- Lane 3 may reference items from Lane 1 and 2, but must declare the exact probability of failure (p_error).
- If any statement in Lane 2 requires unverified assumptions, it must be demoted to Lane 3 immediately.
- Conclude by stating: "Epistemic Core = [Lane 2 Contents]". Everything in Lane 3 is zero-weighted in the final decision.
```

---

## Category III: Counterfactual Stress-Testing & Falsification Auditing

### Template 9: The Popperian Falsification Gatekeeper
* **Cognitive Target**: Redirects the LLM from confirmatory evidence synthesis to hyper-focused refutation.
```text
Target Hypothesis: [INSERT_HYPOTHESIS_OR_DESIGN_DECISION]

Core Directive: Total Confirmation Prohibition.
You are strictly forbidden from writing any tokens that support, validate, or justify the Target Hypothesis.

Attention Focus:
1. Locate the single most fragile, non-redundant assumption supporting this hypothesis.
2. Construct a concrete, empirically verifiable edge-case scenario designed explicitly to disprove that assumption.
3. Compute the minimum force/stress vector required to cause this hypothesis to fail catastrophically:
   - Metric of failure: [Specify precise condition]
   - Probability of occurrence of stress vector: [Estimate]
4. If the edge-case successfully invalidates the assumption, output: "HYPOTHESIS FALSIFIED AT: [Point of failure]".
5. Only if 3 distinct, extreme stress tests fail to break the hypothesis may you output: "HYPOTHESIS SURVIVES FALSIFICATION (Confidence: Provisional)".
```

### Template 10: Inverted Boundary Condition Sweep
* **Cognitive Target**: Stresses mental models by evaluating extreme parameter limits (0, $\infty$, negative space).
```text
System/Model to Audit: [ALGORITHM / STRATEGY / SYSTEM ARCHITECTURE]

Parameter Sensitivity Sweep:
Select the three primary continuous variables governing this system: {P1, P2, P3}.

Execute an explicit boundary condition evaluation:
1. Limit Analysis P1 -> 0 and P1 -> ∞:
   - Does the logical integrity of the system hold, degrade gracefully, or experience catastrophic phase change?
2. Limit Analysis P2 -> 0 and P2 -> ∞:
   - Trace cascading dependencies. Identify deadlocks or resource starvation.
3. Limit Analysis P3 -> 0 and P3 -> ∞:
   - Verify if any division-by-zero, cyclic loops, or impossible physical states occur.
4. Synthesis:
   - Define the strictly bounded operational envelope [P1_min, P1_max], [P2_min, P2_max], [P3_min, P3_max] outside of which this entire system is guaranteed to fail.
```

### Template 11: Counterfactual Pruning Engine
* **Cognitive Target**: Traces branching decision trees to pinpoint the single pivot point of systemic failure.
```text
Failure Analysis: [DESCRIBE_AN_ACTUAL_OR_POTENTIAL_FAILURE_EVENT]

Objective: Isolate the single deterministic turning point using counterfactual subtraction.

Pipeline:
1. Chronological Event Sequence: Construct a strict timeline of discrete events: E = {e_1, e_2, ..., e_n}, where e_n is the terminal failure state.
2. Counterfactual Subtraction Loop:
   - Starting from e_(n-1) backward to e_1:
     - Set e_i = NULL (Assume event e_i did not occur, holding all other prior events identical).
     - Trace the forward trajectory: Does the system still reach terminal failure state e_n?
     - If YES: e_i is non-causal noise. Discard.
     - If NO: e_i is a candidate critical pivot point.
3. Identification:
   - Identify the earliest chronological e_k whose subtraction prevents e_n.
   - State the exact upstream condition that made e_k inevitable.
   - Ignore all other downstream events; focus the entire remediation exclusively on e_k.
```

### Template 12: Reductio ad Absurdum Recursive Amplifier
* **Cognitive Target**: Tests the structural validity of a logic rule by recursive scaling until systemic incoherence occurs.
```text
Proposed Rule/Policy/Heuristic: [INSERT_PROPOSAL]

Execution Protocol:
1. Formalize the core principle behind the proposal into a single generalizable imperative: "In all situations of type C, action A must be taken."
2. Recursive Scaling:
   - Step 1: Scale application density to 10x (10x frequency, 10x magnitude). Trace secondary systemic reactions.
   - Step 2: Scale application density to 1000x (Universal adoption across all agents in the environment).
   - Step 3: Run the system to thermodynamic or game-theoretic equilibrium.
3. Contradiction Extraction:
   - Locate the exact point where universal adoption consumes the preconditions necessary for the rule to function (Self-Cannibalization).
   - State the emergent paradox in a single sentence: "The universal application of X destroys the condition Y required to do X."
```

---

## Category IV: Epistemic Boundary Anchoring & Uncertainty Pruning

### Template 13: Tri-State Epistemic Partitioning
* **Cognitive Target**: Prevents LLMs from blending verifiable truth with plausible hallucination.
```text
Query: [HIGH-STAKES_TECHNICAL_OR_RESEARCH_QUESTION]

Strict Attention Partitioning Directive:
Partition every token of your internal reasoning into one of three isolated buffers:

BUFFER A [DETERMINISTIC KNOWLEDGE]:
- Facts that can be mathematically proven, compiled, or referenced to immutable documentation.
- Zero speculation permitted.

BUFFER B [PARAMETRIC UNCERTAINTY]:
- Propositions where the model or causal structure is known, but input variables are stochastic or unmeasured.
- Must include explicit error margins: [Value ± Tolerance].

BUFFER C [EPISTEMIC VOID]:
- Unknown unknowns, unresolvable ambiguities, and non-computable properties.
- You are forbidden from guessing or approximating contents for this buffer.

Output Format:
- Print the contents of Buffers A, B, and C cleanly.
- Synthesize a final response using ONLY contents from Buffer A and explicitly bounded ranges from Buffer B. If the answer hinges on Buffer C, state: "INSUFFICIENT INFORMATION TO RESOLVE."
```

### Template 14: Bayesian Confidence Calibration & Prior Dissection
* **Cognitive Target**: Forces rigorous probabilistic updating rather than unweighted definitive assertions.
```text
Proposition to Evaluate: [PROPOSITION]

Execution Steps:
1. Base Rate (Prior) Extraction:
   - Ignore all specifics of the current case.
   - Identify the broad reference class of this phenomenon.
   - Assign the historical base rate: P(H). If unknown, assign the uninformative prior P(H) = 0.5 and justify.

2. Evidence Salience Parsing:
   - For every piece of evidence (E_1 to E_m) provided in the context:
     - Determine P(E_i | H): Probability of observing this evidence if hypothesis is TRUE.
     - Determine P(E_i | ~H): Probability of observing this evidence if hypothesis is FALSE.
     - Compute the Likelihood Ratio: L(E_i) = P(E_i | H) / P(E_i | ~H).
     - Filter out any evidence where 0.8 < L(E_i) < 1.2 (Evidentiary Noise).

3. Posterior Calculation:
   - Qualitatively or quantitatively calculate the updated probability: P(H | E).
   - State the final confidence strictly as a calibrated percentage and define the single piece of evidence that would shift this probability by >30%.
```

### Template 15: Grounded Token Verification (Hallucination Surface Minimization)
* **Cognitive Target**: Locks attention exclusively to provided source tokens; eliminates external prior intrusion.
```text
Reference Corpus: [PASTE_SOURCE_DOCUMENTATION]
Target Question: [SPECIFIC_QUESTION]

Attention Lock Constraint:
- You operate under an absolute closed-book restriction.
- Every declarative statement you generate MUST include a verbatim substring citation from the Reference Corpus containing the causal anchor.

Audit Loop:
1. Draft provisional answer step.
2. Scan provisional answer for any semantic concepts NOT present in the Reference Corpus.
3. If an external concept is detected:
   - Erase the token sequence immediately.
   - Fall back to the literal text.
4. If the Reference Corpus does not contain the complete mechanical answer to the question:
   - Do NOT attempt to complete the logic using pre-trained weights.
   - Output: "SOURCE DEFICIT: Missing data on [Specific Concept]."
```

### Template 16: The Active Ignorance Map
* **Cognitive Target**: Maps missing dependencies before allowing synthesis to proceed.
```text
Task: Formulate a solution for [GOAL_OR_OBJECTIVE].

Execution Barrier:
You are blocked from generating the solution. You must first produce a comprehensive "Map of Ignorance."

Requirements:
1. Identify the 4 foundational questions about the operational environment that are NOT answered in the prompt text.
2. For each question:
   - Detail the worst-case consequence of assuming a favorable answer.
   - Define the exact empirical test required to resolve the question.
3. Construct a Dependency Gating Vector:
   - Formulate the solution strictly as a conditional state machine:
     - IF [Unknown_1 is State A] AND [Unknown_2 is State X] -> Action 1
     - IF [Unknown_1 is State B] AND [Unknown_2 is State X] -> Action 2
4. Forbid any unconditional recommendations.
```

---

## Category V: Invariant State-Tracking & Non-Linear Dependency Isolation

### Template 17: Invariant Conservation Checker
* **Cognitive Target**: Audits dynamic, multi-step operations against fundamental conservation laws.
```text
Problem: [MULTI-STEP_TRANSFORMATION_TASK: e.g., System Migration, Financial Engineering, Logic Re-factoring]

Operational Constraint:
Define and track the Invariants. These values/properties MUST remain conserved at 100% fidelity across every intermediate state step.

Invariant Register:
- Invariant 1 (e.g., Total System Energy, Ledger Parity, Epistemic Scope): [SPECIFY]
- Invariant 2 (e.g., Deterministic Reversibility, State Continuity): [SPECIFY]

Execution Trace:
- Step 1: Execute transition T_0 -> T_1.
  - Audit: Compute value of Invariant 1 and Invariant 2. If drift != 0, ABORT and recalculate.
- Step 2: Execute transition T_1 -> T_2.
  - Audit: Compute value of Invariant 1 and Invariant 2. If drift != 0, ABORT and recalculate.
- [Continue iteratively...]

Final Validation:
Generate the final state only after a proof is written demonstrating that zero invariant drift occurred across the entire transformation chain.
```

### Template 18: Non-Linear Temporal Dependency Anchor
* **Cognitive Target**: Mitigates recency bias and captures delayed, non-monotonic system dynamics.
```text
Scenario: [COMPLEX_DYNAMIC_SCENARIO_WITH_FEEDBACK_LOOPS]

Direct Attention Rules:
1. Suppress the immediate linear effects of the proposed intervention (t_0 -> t_1). Treat immediate effects as superficial.
2. Direct all analytical attention to the delayed response regimes:
   - Regime 1: Secondary feedback response (t_2, operational equilibrium).
   - Regime 2: Adversarial/Market reaction (t_3, behavioral adaptation of competing agents).
   - Regime 3: Systemic exhaustion or unintended attractor state (t_4, long-horizon systemic drift).

Analysis Matrix:
- Plot the causal loop diagram: Identify all Reinforcing (R) and Balancing (B) feedback loops.
- Pinpoint the exact point of "Policy Resistance": Where the system pushes back against the intervention to restore original equilibrium.
- Output: Redesign the original intervention to leverage the balancing loop rather than fighting it.
```

### Template 19: Cyclic Dependency Graph Resolution
* **Cognitive Target**: Breaks "chicken-and-egg" causal loops into topologically sorted execution graphs.
```text
System Under Analysis: [SYSTEM_WITH_CIRCULAR_DEPENDENCIES]

Problem: The system features circular causality (A depends on B, B depends on C, C depends on A), causing reasoning deadlocks.

Disentanglement Heuristic:
1. Graph Construction:
   - Explicitly list all feedback cycles: Cycle 1 = [Node_A -> Node_B -> Node_C -> Node_A].
2. Decoupling Phase-Space Injection:
   - Identify which node can be converted from an endogenous variable to an exogenous seed variable by injecting an external assumption or boundary constraint.
   - Let Seed Node = Node_A at temporal index t=0.
3. Unroll into an Acyclic Graph:
   - Node_A(t0) -> Node_B(t1) -> Node_C(t2) -> Node_A(t3).
4. Convergence Evaluation:
   - Calculate if the delta |Node_A(t3) - Node_A(t0)| converges to zero over repeated iterations.
   - If divergent: Identify the system instability.
   - If convergent: State the stable terminal equilibrium of the system.
```

### Template 20: The Constraint Satisfaction Ledger
* **Cognitive Target**: Halts output generation instantly upon the violation of any hard constraint.
```text
Target Design/Solution: [COMPLEX_ENGINEERING_OR_LOGICAL_TASK]

HARD CONSTRAINTS (Zero Tolerance):
1. Constraint Alpha: [SPECIFY]
2. Constraint Beta: [SPECIFY]
3. Constraint Gamma: [SPECIFY]

LEDGER EXECUTION PROTOCOL:
Initialize a permanent ledger block at the start of your generation.
For every proposed design element or logic step:
1. Print the proposed step.
2. Run the step against the Ledger:
   - Check Alpha: [PASS/FAIL]
   - Check Beta: [PASS/FAIL]
   - Check Gamma: [PASS/FAIL]
3. Hard Break Condition:
   - If ANY check returns FAIL, you are strictly prohibited from proceeding to the next step.
   - You must immediately output: "VIOLATION DETECTED AT [Step]. REASON: [Explicit Violation]."
   - Clear the step, mutate the approach, and re-run the verification ledger.
4. Output the integrated design only if 100% of steps display [PASS/PASS/PASS].
```

---

# Operational Framework: Execution Heuristics for Self-Paced Mastery

To master these attentional filtering architectures, treat the LLM as a high-entropy reasoning engine whose default generative state is uncontrolled associative recall. Mastery is achieved by developing an instinct for **when and how to introduce cognitive bottlenecks**.

```
Reasoning Degradation Audit
┌───────────────────────────────┐
│ Symptom: Semantic Drift       │ ──► Inject: Invariant Conservation Checker
└───────────────────────────────┘
┌───────────────────────────────┐
│ Symptom: Confirmation Bias    │ ──► Inject: Popperian Falsification Gate
└───────────────────────────────┘
┌───────────────────────────────┐
│ Symptom: Hallucinated Fluency │ ──► Inject: Tri-State Epistemic Partition
└───────────────────────────────┘
┌───────────────────────────────┐
│ Symptom: Confounded Latents   │ ──► Inject: Orthogonal Latent Decoupling
└───────────────────────────────┘
```

### 1. The Attention Entropy Diagnostic
Identify reasoning degradation by monitoring the model's textual outputs for distinct failure signatures:
* **Failure Mode A: Semantic Drift.** The model begins with logical rigor but gradually regresses to generic prose by Step 4.
  * *Heuristic*: Interject an **Invariant State-Tracking Filter** (Template 17 or 20) every $N$ generation tokens to re-anchor the attention window.
* **Failure Mode B: Sycophantic Agreement.** The prompt introduces a flawed hypothesis and the model manufactures justification.
  * *Heuristic*: Wrap the query in an **Inhibitory Gate** (Template 4 or 9) to penalize the most intuitive affirmative paths.
* **Failure Mode C: Hallucinatory Stitching.** The model bridges two disparate concepts with an unverified intuitive leap.
  * *Heuristic*: Force execution through an **Epistemic Partitioning Matrix** (Template 8 or 13) to decouple verifiable evidence from inductive speculation.

### 2. Compositional Prompt Chaining
Advanced thinking methods should rarely be deployed in isolation. Chain them sequentially to achieve maximum signal-to-noise ratio:

$$\text{Raw Context} \xrightarrow[\text{Template 1}]{\text{Noise Filter}} \text{Causal Core} \xrightarrow[\text{Template 5}]{\text{Decomposition}} \text{Orthogonal Axes} \xrightarrow[\text{Template 9}]{\text{Falsification}} \text{Validated Synthesis}$$

1. **Step 1 (Inhibitory)**: Strip noise and distractor variables using Template 1 or 3.
2. **Step 2 (Deconstructive)**: Decouple the clean variables into orthogonal planes using Template 5 or 6.
3. **Step 3 (Adversarial)**: Subject the derived mechanisms to rigorous stress-testing using Template 9 or 10.
4. **Step 4 (Verification)**: Run the surviving output through the Constraint Satisfaction Ledger (Template 20).

### 3. Iterative Calibration Routine
For self-paced mastery, practice calibrating these prompts against known, complex failure cases (e.g., NP-hard optimization problems, counterintuitive game-theoretic paradoxes, distributed systems edge cases):
* **Baseline Run**: Submit the raw problem with standard zero-shot CoT ("Think step by step"). Document the exact point of logical failure.
* **Filter Selection**: Match the failure point to one of the 5 Causal Taxonomies.
* **Execution & Mutation**: Apply the chosen template. If the model circumvents the filter (e.g., skips an audit check), increase the inhibitory penalty by converting guidelines into explicit syntactic conditions (e.g., "Do not use adjectives", "Format as a pure state transition table").
* **Convergence**: The filter is calibrated when the model rejects plausible hallucinations and either outputs a structurally verified proof or explicitly halts due to insufficient information.
