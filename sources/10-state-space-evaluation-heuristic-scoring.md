# ARCHITECTURAL TAXONOMY: STATE-SPACE REASONING & HEURISTIC EVALUATION

State-Space Evaluation translates deterministic search algorithms ($A^*$, Beam Search, Monte Carlo Tree Search, Branch-and-Bound) into natural language prompt architectures. When applied to large language models, the generation process ceases to be an unconstrained linear sequence and becomes an explicit traversal over a directed graph $(\mathcal{S}, \mathcal{A}, \mathcal{T}, \mathcal{H})$:

$$\mathcal{M} = \langle \mathcal{S}, \mathcal{A}, \mathcal{T}, \mathcal{H}, \mathcal{G} \rangle$$

*   **State Space ($\mathcal{S}$):** The structured representation of the current problem state, including historical commitments, working memory, constraints satisfied, and remaining subproblems.
*   **Action Space ($\mathcal{A}$):** The parameterized generation operators that mutate state $s_t \to s_{t+1}$.
*   **Transition Operator ($\mathcal{T}: \mathcal{S} \times \mathcal{A} \to \mathcal{S}$):** The deterministic or probabilistic update rule mapping actions over states.
*   **Heuristic Scoring Function ($\mathcal{H}: \mathcal{S} \to \mathbb{R}^k$):** Multi-dimensional evaluation tensors that score candidate states on admissibility, cost-to-come $g(s)$, estimated cost-to-go $h(s)$, epistemic uncertainty, and constraint violation penalties.
*   **Goal Test ($\mathcal{G}: \mathcal{S} \to \{0, 1\}$):** Explicit termination criteria establishing convergence.

```
       [Current State: S_t]
                │
    ┌───────────┼───────────┐
    ▼           ▼           ▼
[Action A1] [Action A2] [Action A3]
    │           │           │
    ▼           ▼           ▼
[State S_t+1] [State S_t+1] [State S_t+1]
    │           │           │
    └─────► [Heuristic Scoring Engine: H(S)] ◄─────┘
                │
        [Prune / Retain / Backtrack]
                │
                ▼
       [Selected Frontier S*]
```

### Core Causal Mechanisms

1. **Deterministic Frontier Search (Beam & Priority Queues):** Greedy and semi-greedy candidate winnowing via scalar utility thresholds.
2. **Admissible Metric Estimation ($A^*$ & Distance-to-Goal):** Cost-balanced expansion prioritizing minimal remaining work under non-overestimating path bounds.
3. **Stochastic Rollouts & Lookahead (MCTS & Simulation):** Path evaluations derived from simulated downstream completions rather than static evaluations.
4. **Pruning & Bounding Mechanisms (Branch-and-Bound / Minimax):** Early-exit drop conditions based on mathematical bounding and constraint violations.
5. **Multi-Criteria Value Decomposition (MAUT & Vector Evaluations):** Disentangled objective evaluation functions preventing single-metric collapse.

---

# 20 PRODUCTION-GRADE STATE-SPACE PROMPT TEMPLATES

---

## Class 1: Deterministic Frontier Search (Beam, Best-First & Plateau Navigation)

### Template 1: Fixed-Width Beam Search with Entropy Pruning
* **Causal Mechanism:** Breadth-constrained state tracking with local score evaluation to prevent combinatorial divergence.
* **Educational Utility:** Teaches how to force an LLM to maintain parallel hypothesis tracks ($k$-width beam) while computing explicit state-transition delta values.

```markdown
You are an execution engine running a Beam Search (width k=3) over solution trajectories.

[PROBLEM CONTEXT]
{{PROBLEM_INPUT}}

[OBJECTIVE FUNCTION]
Maximize precision, structural soundess, and adherence to operational constraints.

[EXECUTION PROTOCOL]
1. INITIALIZATION: Generate 3 distinct root actions (Candidate States: S1_0, S2_0, S3_0).
2. EXPANSION (Depth t): For each candidate state S_i, generate 2 forward transition operators:
   - S_i.1 = apply(Operator_A, S_i)
   - S_i.2 = apply(Operator_B, S_i)
3. HEURISTIC EVALUATION: Score all 6 expanded states using the vector H(S) = [Feasibility (0-10), Information_Density (0-10), Risk_Penalty (-10 to 0)].
   - Calculate Aggregate Score: Score = (Feasibility * 0.4) + (Information_Density * 0.4) + Risk_Penalty.
   - Explicitly display the scoring matrix.
4. PRUNING: Select the top k=3 scoring states. Drop the remaining 3 with explicit failure-mode notes.
5. TERMINATION CHECK: If target depth t=3 is reached, select S* = argmax(H(S)) and output the full trajectory.

Follow this exact computational schema for each depth iteration.
```

---

### Template 2: Best-First Priority Queue with Explicit Backtracking
* **Causal Mechanism:** Dynamic priority ordering with a fallback open-list when local score falls below a rejection threshold.
* **Educational Utility:** Demonstrates state retrievability and non-linear backtracking when an LLM enters an unviable reasoning branch.

```markdown
Run an agenda-driven Best-First Search to synthesize an optimal solution for the target query.

[QUERY]
{{TARGET_QUERY}}

[AGENDA STATE MANAGEMENT]
Maintain two explicit data structures in your response:
- OPEN_LIST: Set of unexplored candidate paths ranked by Priority Score P(S) ∈ [0.00, 1.00].
- CLOSED_LIST: Visited states with final outcome ratings.

[ITERATION LOOP]
Step 1: Pop the highest-priority state S_curr from OPEN_LIST.
Step 2: Propose 3 discrete transition steps forward.
Step 3: Evaluate each step with the scoring rubric:
  - Admissibility: Does this step directly satisfy requirements without hallucination? [Weight: 0.5]
  - Progress Metric: Distance delta toward full problem resolution [Weight: 0.5]
Step 4: Branching Decision:
  - IF max(Score) < 0.65: Declare LOCAL MINIMUM. Push S_curr to CLOSED_LIST with status "DEAD_END". Backtrack to next highest node in OPEN_LIST.
  - IF max(Score) >= 0.65: Append winner to Active Path, push alternates to OPEN_LIST.
Step 5: Output state transition logs at every step. Complete when Progress Metric == 1.0.

[INPUT DATA]
{{RAW_SYSTEM_SPECIFICATION}}
```

---

### Template 3: Dynamic Beam Expansion with Variable Information-Density Metrics
* **Causal Mechanism:** Elastic width adjustment where the search beam expands under high epistemic uncertainty and contracts when confidence is high.
* **Educational Utility:** Teaches dynamic compute allocation within prompts based on state-uncertainty heuristics.

```markdown
Resolve the target architectural paradox using Variable-Width State-Space Search.

[PARADOX / SYSTEM CHALLENGE]
{{INPUT_CASE}}

[ALGORITHM SPECIFICATION]
For each step n of derivation:
1. FORMULATE STATE: Define State S_n.
2. UNCERTAINTY AUDIT: Calculate Epistemic Entropy E(S_n) ∈ [Low, Medium, High].
   - If Low: Set Beam Width k = 1 (Deterministic greedy expansion).
   - If Medium: Set Beam Width k = 2 (Bifurcation).
   - If High: Set Beam Width k = 4 (Multi-hypothesis exploratory expansion).
3. GENERATE EXPANSIONS: Produce k distinct branches.
4. HEURISTIC FILTER: Score each branch on:
   - Metric C (Coherence): [0-1]
   - Metric E (Empirical Grounding): [0-1]
   - Unified Score H = 2 * (C * E) / (C + E + 1e-5) [Harmonic Mean]
5. WINNOW: Retain the single highest H-score branch if H >= 0.75. If all branches score H < 0.75, preserve top-2 and re-sample transitions.

Execute until terminal convergence.
```

---

### Template 4: Steepest-Ascent Hill-Climbing with Random Restarts
* **Causal Mechanism:** Local optimization tracking local gradients, resetting to distinct initializations when trapped on local plateaus.
* **Educational Utility:** Illuminates the difference between local gradient alignment and global search in reasoning models.

```markdown
Execute Steepest-Ascent Hill Climbing with Random Restart capability to design an optimal technical solution.

[OBJECTIVE]
{{ENGINEERING_PROBLEM}}

[STATE EVALUATION METRIC]
Quality Function Q(S) = (Efficiency × 0.3) + (Fault_Tolerance × 0.4) + (Maintainability × 0.3).
Every metric is scored on a [0.0 - 10.0] scale. Target: Q(S) ≥ 8.8.

[SEARCH PROTOCOL]
- RUN 1 (Initialization A): Generate baseline design S_0. Compute Q(S_0).
  - Mutate S_0 into 3 neighboring variations: N_1, N_2, N_3.
  - Evaluate Q(N_i). 
  - If max(Q(N_i)) > Q(S_0): Transition to best neighbor. Repeat iteration up to Step 3.
  - If max(Q(N_i)) ≤ Q(S_current) AND Q(S_current) < 8.8: TRIGGER RESTART. Flag as "Plateau Reached".

- RUN 2 (Restart B - Orthogonal Approach): Instantiate completely distinct architecture S_alt.
  - Repeat the mutation and climbing sequence.
  - Compare Global Maxima across both runs.

Select and present the globally superior state.
```

---

## Class 2: Admissible Metric Estimation ($A^*$ Traversal & Distance-to-Goal)

### Template 5: Formal $A^*$ Reasoner with Admissible Cost Decomposition
* **Causal Mechanism:** Explicit evaluation using $f(n) = g(n) + h(n)$, tracking consumed steps alongside an admissible, non-overestimating remaining distance heuristic.
* **Educational Utility:** Forces students to decouple "effort expended" from "unresolved requirements" via formal heuristic functions.

```markdown
Act as a formal A* graph traversal solver to engineer the requested protocol.

[START STATE S_0]
Raw requirements: {{SYSTEM_REQUIREMENTS}}

[GOAL CRITERIA S_G]
Zero ambiguous edge-cases, full structural resilience, minimal implementation complexity.

[EVALUATION ENGINE]
For every transition state n:
- g(n): Accumulated Cost. Count of logic-tokens/complexity points added so far (normalized to 1.0 per milestone).
- h(n): Admissible Remaining Distance. Absolute count of unmet core system requirements (Each unmet requirement = 1.5).
  *Rule: h(n) must never overestimate the effort to complete.*
- f(n) = g(n) + h(n).

[EXPANSION CYCLE]
1. Propose three possible successor modules for the current state.
2. Calculate g(n), h(n), and resulting f(n) for each candidate.
3. Select node with MINIMUM f(n).
4. Print the traversal tree in a markdown table:
   | Node Candidate | g(n) | h(n) | f(n) | Selected? (Y/N) | Justification |
5. Repeat until h(n) = 0.
```

---

### Template 6: Weighted $A^*$ for Time-Bounded Solution Synthesis
* **Causal Mechanism:** Introducing an inflation factor $\epsilon > 1$ to $h(n)$ ($f(n) = g(n) + \epsilon \cdot h(n)$) to sacrifice theoretical optimality for generation velocity.
* **Educational Utility:** Teaches explicit parameterization of greedy-vs-optimal tradeoffs in prompt-based derivation.

```markdown
Analyze the target code vulnerability and plan a remediation path using Weighted A* Search ($W-A^*$).

[TARGET VULNERABILITY]
{{VULNERABILITY_PAYLOAD}}

[SEARCH PARAMETERS]
Weight parameter: ε = 1.6 (Bias heavily toward reducing remaining distance to safety).
Evaluation equation: f(n) = g(n) + 1.6 * h(n)

- g(n): Implementation overhead, operational disruption risk [0-10 scale].
- h(n): Residual exploit surface area remaining unresolved [0-10 scale].

[EXECUTION LOG]
At each remediation step:
1. Define Current State.
2. Generate 2 distinct implementation branches.
3. Compute f(n) explicitly for both.
4. Execute aggressive pruning: instantly terminate any branch where h(n) increases relative to its parent node regardless of low g(n).
5. Advance the frontier with minimum f(n).

Provide final unified remediation patch upon reaching h(n) == 0.
```

---

### Template 7: Bidirectional State-Space Convergence
* **Causal Mechanism:** Simultaneous forward search from initial conditions ($S_0$) and backward search from the goal state ($S_G$) with midpoint intersection heuristics.
* **Educational Utility:** Shows how bidirectional heuristic scoring mitigates exponential search-tree expansion in long-horizon reasoning.

```markdown
Solve the target system migration path using Bidirectional State-Space Traversal.

[INITIAL STATE - S_0]
Legacy monolithic infrastructure described here: {{LEGACY_STATE}}

[GOAL STATE - S_G]
Target cloud-native decoupled infrastructure: {{TARGET_STATE}}

[BIDIRECTIONAL PROTOCOL]
Iterate by alternating forward and backward steps:
- FORWARD THREAD (From S_0): Generate forward transition step S_fwd_t.
  - Evaluation metric: Distance toward Target H_fwd(S) = unmigrated interfaces count.
- BACKWARD THREAD (From S_G): Generate backward precondition step S_bwd_t.
  - Evaluation metric: Dependency feasibility on legacy systems H_bwd(S).
- CONVERGENCE SCORER:
  - Compute State Delta Δ(S_fwd_t, S_bwd_t).
  - Score compatibility on an alignment scale: [0.00 - 1.00].

If Δ score ≥ 0.85, bridge the remaining structural gap directly and terminate.
Print each bidirectional transition and its associated heuristic delta.
```

---

### Template 8: Hierarchical State-Space Abstraction Search
* **Causal Mechanism:** Macro-state navigation at high abstraction layers down-projected to micro-state operational actions.
* **Educational Utility:** Demonstrates hierarchical decomposition where heuristics are evaluated at varying resolutions of abstraction.

```markdown
Deploy a Hierarchical State-Space Search (H-SSS) to architect the requested distributed algorithm.

[DOMAIN CONTEXT]
{{DISTRIBUTED_SYSTEM_CHALLENGE}}

[TIER 1: MACRO-STATE GRAPH (Global Strategy)]
1. Generate 3 high-level architectural topologies (Macro-States: M1, M2, M3).
2. Score each Macro-State using Macro-Heuristic:
   $H_{macro} = (Horizontal\_Scalability \times 0.5) + (CAP\_Theorem\_Fit \times 0.5)$
3. Prune lowest 2; lock down the winning Macro-State $M^*$.

[TIER 2: MICRO-STATE EXPANSION (Operational Implementation)]
1. Expand $M^*$ into a graph of sequential operational micro-states (m_0 → m_1 → ... → m_k).
2. Evaluate each micro-transition against the Micro-Heuristic:
   $H_{micro} = Latency\_Impact (ms) + Serialization\_Overhead + Concurrency\_Contention\_Risk$.
3. If any micro-step scores an unacceptable risk level (> 7/10), backtrack to previous micro-state and re-route execution logic.

Output full resolution with explicit macro and micro heuristic score logs.
```

---

## Class 3: Stochastic Simulation & Lookahead (MCTS & Rollout Scoring)

### Template 9: Monte Carlo Tree Search (MCTS) with UCB1 Frontier Balancing
* **Causal Mechanism:** Iterative selection, expansion, random/pseudo-random simulation (rollout), and backpropagation using Upper Confidence Bound bounds.
* **Educational Utility:** Teaches how to balance exploration (untested hypotheses) vs. exploitation (high-scoring hypotheses) in natural language.

```markdown
Process the prompt's scenario through an emulated Monte Carlo Tree Search (MCTS) with UCB1 branch selection.

[PROBLEM SCENARIO]
{{HIGH_STAKES_DECISION}}

Run 3 explicit MCTS iterations. For each iteration, trace:

1. SELECTION: 
   Identify current explored nodes. Use the UCB1 formula to choose the active node:
   $UCB1 = \bar{X}_j + C \times \sqrt{\frac{\ln N}{n_j}}$
   (Where $\bar{X}_j$ is the branch average score, $N$ is total parent visits, $n_j$ is node visit count, set exploration constant $C = 1.41$).
   *Note: For unvisited nodes, treat UCB1 as infinity.*

2. EXPANSION:
   Create a new logical sub-action branch from the selected node.

3. SIMULATION (Rollout):
   Rapidly project the action 3 steps forward to a prospective terminal state. 
   Apply Heuristic Terminal Evaluation $V \in [0.0, 1.0]$.

4. BACKPROPAGATION:
   Update visit counts $n$ and average value scores $\bar{X}$ all the way up to the root.

Show all tabular calculations after each iteration. Deliver the final action dictated by the most visited node ($n$).
```

---

### Template 10: Counterfactual Lookahead Rollouts
* **Causal Mechanism:** Simulating alternative futures across divergent action branches to assess downstream tail-risk before committing to a step.
* **Educational Utility:** Imparts understanding of step-level regret minimization and failure-mode pre-computation.

```markdown
Execute Counterfactual Rollout Scoring to design an incident mitigation strategy.

[CRITICAL INCIDENT]
{{INCIDENT_TELEMETRY}}

[EVALUATION ENGINE]
For the current incident state, propose Candidate Action A and Candidate Action B.

Execute a 2-step Lookahead Rollout for BOTH candidates:
- Project Step +1: Immediate system reaction.
- Project Step +2: Cascading side-effects on dependencies.

Compute Counterfactual Regret Metric (CRM):
- Positive Utility: Expected uptime recovery speed [1-10].
- Negative Utility: Tail risk of catastrophic data loss [1-10].
- CRM = (Negative Utility * 1.5) - Positive Utility. (Lower is better).

[BRANCH PRUNING]
Explicitly drop any branch where Projected Step +2 produces an irrecoverable state, regardless of Step +1 success.

Select the winning action path with explicit justification from the rollout data.
```

---

### Template 11: Ensemble Self-Consistency Verification with Value Scoring
* **Causal Mechanism:** Sampling parallel inference trajectories, scoring each against an invariant verification heuristic, and clustering consensus values.
* **Educational Utility:** Demonstrates stochastic generation verification, pruning ungrounded outliers via scoring consensus.

```markdown
Perform Ensemble Multi-Path Value Scoring on the following logical challenge.

[CHALLENGE]
{{COMPLEX_DEDUCTION}}

[PARALLEL GENERATION]
Generate 3 distinct reasoning paths: Path Alpha, Path Beta, Path Gamma.

[STATE-SCORING MATRIX]
Score each path at its conclusion using the following criteria (Scale 0-100):
1. Invariant Integrity: Zero contradictions of explicit prompt constraints.
2. Step Deductibility: Every claim strictly follows from its immediate predecessor.
3. Edge Robustness: Extreme boundaries handled cleanly.

[TABULATE SCORES]
| Path | Invariant Integrity | Step Deductibility | Edge Robustness | Mean Score |
|------|---------------------|---------------------|-----------------|------------|
| ...  | ...                 | ...                 | ...             | ...        |

[CONSENSUS SYNTHESIS]
- IF Highest Mean Score >= 85: Output winning path directly.
- IF Highest Mean Score < 85: Extract highest-scoring sub-components from each path, recombine into an optimized Path Delta, and re-score to guarantee threshold compliance.
```

---

### Template 12: Depth-Limited Rollout with Terminal Value Approximation
* **Causal Mechanism:** Lookahead truncated at horizon $d=2$, relying on an analytical terminal value function to approximate infinite-horizon viability.
* **Educational Utility:** Explains computational-budget conservation through horizon truncation and terminal heuristic estimation.

```markdown
Act as a finite-horizon planner to design an API integration layer.

[API SPEC & CONSTRAINTS]
{{SYSTEM_INTERFACES}}

[EXECUTION PROTOCOL]
Depth Horizon: d = 2.
At the initial state:
1. Generate 3 initial architectural hooks (Branch 1, Branch 2, Branch 3).
2. For each branch, project forward to Depth 2 (Data transformations & error handling).
3. TRUNCATE SEARCH: Do not plan past Depth 2.
4. TERMINAL VALUE FUNCTION: Evaluate the terminal state of each branch using:
   $V_{terminal} = \frac{Type\_Safety + Idempotency\_Guarantee}{Resource\_Cost + Latency\_Score}$
   (Score each variable on a 1-5 scale).

Display the terminal evaluation scores for all 3 paths. Select the path with max($V_{terminal}$) and expand it into full implementation code.
```

---

## Class 4: Constraint-Satisfaction & Branch-and-Bound Pruning

### Template 13: Strict Branch-and-Bound Combinatorial Optimization
* **Causal Mechanism:** Maintains an incumbent optimal value ($B$), pruning branches whose optimistic heuristic bound falls below $B$.
* **Educational Utility:** Imparts the mechanics of early stopping and branch elimination via strict mathematical bounding in reasoning tasks.

```markdown
Run a Branch-and-Bound optimization search to design a zero-trust network policy.

[NETWORK ACCESS PROFILE]
{{RESOURCE_ACCESS_REQUIREMENTS}}

[BOUND TRACKING]
Maintain Incumbent Best Score: B = -∞.

[SEARCH STEP]
Explore candidate permission assignments sequentially:
- Propose Candidate Architecture S_k.
- Compute Realized Security Score: g(S_k) ∈ [0, 50].
- Compute Optimistic Upper Bound for Remaining System: h_upper(S_k) ∈ [0, 50].
  *Note: h_upper must represent the most optimistic possible score the unconfigured components could achieve.*
- Total Potential Bound: U(S_k) = g(S_k) + h_upper(S_k).

[PRUNING RULE]
- IF U(S_k) < B: PRUNE INSTANTLY. Do not generate details for this branch. Label as "Pruned: Sub-optimal Bound".
- IF U(S_k) >= B: Expand S_k completely. 
  - Compute actual total score Score(S_k).
  - If Score(S_k) > B: Update incumbent best: Set B = Score(S_k).

Document each node exploration, bounded values, and cuts clearly.
```

---

### Template 14: Invariant Assertion Gating with Hard Failure Drop
* **Causal Mechanism:** Immediate pruning of any state that violates binary non-negotiable assertions, regardless of heuristic performance.
* **Educational Utility:** Demonstrates the interaction between soft optimization heuristics and hard boundary constraints.

```markdown
Synthesize an enterprise cryptographic key lifecycle policy.

[ENVIRONMENT CONSTRAINTS]
{{REGULATORY_ENVIRONMENT}}

[HARD INVARIANTS (Boolean Gating)]
Every generated state MUST clear all 3 invariants:
- INV_1: Keys must never exist in plaintext in persistent storage.
- INV_2: Key rotation must not cause service downtime.
- INV_3: Must comply with FIPS 140-3 standards.

[TRAVERSAL & EVALUATION]
For each procedural phase of the policy:
1. Propose 2 implementation variations.
2. ASSERTION CHECK:
   - Run candidate through INV_1, INV_2, INV_3.
   - If any candidate registers a single FAIL, drop it immediately without scoring. Label: "DROPPED: INVARIANT VIOLATION [INV_X]".
3. HEURISTIC RANKING: For surviving candidates, calculate:
   Score = (Operational_Simplicity * 0.4) + (Audit_Automation * 0.6).
4. Advance the highest-scoring invariant-safe candidate to the next lifecycle phase.
```

---

### Template 15: Pareto-Frontier Pruning for Multi-Objective Tradeoffs
* **Causal Mechanism:** Vector dominance evaluation; state $S_A$ is pruned if and only if state $S_B$ is strictly superior in at least one metric and equal or superior in all others.
* **Educational Utility:** Prevents simplistic single-metric collapse in systems with competing fundamental trade-offs (e.g., speed vs. memory).

```markdown
Evaluate system optimization patterns by tracking a non-dominated Pareto Frontier.

[SYSTEM PARAMETERS]
{{WORKLOAD_PROFILE}}

[OBJECTIVE VECTOR]
Evaluate candidates across three non-reducible metrics:
$\vec{M}(S) = [ Throughput\ (req/s),\ Memory\_Efficiency\ (MB),\ Latency\_p99\ (ms) ]$
(Goal: Maximize Throughput, Maximize Memory Efficiency, Minimize Latency).

[ALGORITHM]
1. Generate 4 candidate architectural setups.
2. Measure/Estimate $\vec{M}(S)$ for each.
3. PARETO DOMINANCE AUDIT:
   Compare candidates pairwise.
   - State A dominates State B ($A \succ B$) iff $\forall i, M_i(A) \ge M_i(B)$ and $\exists i, M_i(A) > M_i(B)$.
   - If a candidate is dominated by any other candidate, PRUNE IT.
4. Tabulate the surviving non-dominated candidates (The Pareto Set).
5. Explain the precise trade-off boundary among the surviving frontier states.
```

---

### Template 16: Minimax Search with Alpha-Beta Cutoffs for Adversarial Environments
* **Causal Mechanism:** Alternating Max-layer (defensive system design) and Min-layer (adversarial exploit exploration) with structural pruning of dominated branches.
* **Educational Utility:** Teaches adversarial game-theoretic state-space evaluation inside software and prompt architecture.

```markdown
Act as a strategic security architect executing Minimax with Alpha-Beta Pruning.

[ATTACK SURFACE]
{{CRITICAL_INFRASTRUCTURE_MODULE}}

[BOUND TRACKING]
Initialize Alpha α = -∞, Beta β = +∞.

[SEARCH TREE EXECUTION (Depth = 3)]
- LEVEL 1 (MAX - Defensive Control):
  Propose 2 defensive architectural patterns: Control_A and Control_B.
  
- LEVEL 2 (MIN - Adversary Attack Vector):
  For each control, simulate 2 adversarial attacks:
  - Attack 1, Attack 2.
  - Adversary objective: Maximize breach severity (Scale: 1-100).
  - Compute adversarial utility. Update Beta β.
  - Cutoff Rule: If at any point β ≤ α, stop evaluating remaining sibling attack branches. Note as "Alpha Cutoff Triggered".

- LEVEL 3 (MAX - Mitigating Patch):
  Deploy compensatory control. Compute final defensive security rating. Update Alpha α.

Output the complete evaluation tree, explicitly marking any pruned branches with their respective α and β values. Select the minimax-optimal defensive control.
```

---

## Class 5: Dynamic Value Decomposition & Reflexive Scoring

### Template 17: Multi-Attribute Utility Theory (MAUT) Decomposition with Dynamic Weighting
* **Causal Mechanism:** Deconstruction of evaluation into orthogonal utility attributes modulated by context-dependent dynamically computed weights.
* **Educational Utility:** Demonstrates sophisticated vector scoring without flattening multi-variable trade-offs into uncalibrated scalar rankings.

```markdown
Resolve the software architectural impasse using Multi-Attribute Utility Theory (MAUT) state scoring.

[TECHNICAL DISPUTE]
{{ARCHITECTURAL_OPTIONS}}

[DYNAMIC WEIGHT ESTIMATION]
Based on the input context, calculate environment criticality weights $\vec{W}$ such that $\sum w_i = 1.0$:
- $w_{perf}$: Performance under high concurrency
- $w_{cost}$: Infrastructure cost impact
- $w_{maint}$: Developer maintainability and cognitive load
- $w_{sec}$: Security/Attack surface area

[STATE EVALUATION]
For each candidate architecture:
1. Assign normalized individual scores $U_i \in [0.00, 1.00]$ across all 4 attributes.
2. Show attribute score justification with technical evidence.
3. Compute the scalar dot product: Total Utility $U(S) = \vec{W} \cdot \vec{U}(S) = \sum (w_i \times U_i)$.
4. Run sensitivity analysis: Re-calculate $U(S)$ with $w_{perf}$ increased by 50% and $w_{cost}$ decreased by 50%.

Deliver the optimal configuration based on absolute utility and sensitivity robustness.
```

---

### Template 18: Epistemic Uncertainty vs. Aleatoric Risk Value Decomposition
* **Causal Mechanism:** Disentangling state score components into structural lack-of-knowledge (epistemic) and inherent environment randomness (aleatoric) to guide frontier expansion.
* **Educational Utility:** Teaches how to target information-gathering actions specifically toward reducing high epistemic uncertainty states.

```markdown
Evaluate deployment strategies using Dual-Risk State-Space Scoring.

[DEPLOYMENT ENVIRONMENT]
{{SYSTEM_SCALE_AND_DEPENDENCIES}}

[DECOMPOSED SCORING ENGINE]
Score every state across two distinct, uncombined risk dimensions:

1. Epistemic Uncertainty Score $EU(S) \in [0, 10]$
   (Measures lack of knowledge, ambiguous assumptions, missing profiling data).
   - If $EU(S) \ge 6$: Transition action must be an INFORMATION ACQUISITION step (e.g., benchmark, canary, log gathering).
   
2. Aleatoric Risk Score $AR(S) \in [0, 10]$
   (Measures intrinsic, irreducible system volatility, network partitions, hardware failures).
   - If $AR(S) \ge 6$: Transition action must be a BLAST-RADIUS CONTAINMENT step (e.g., circuit breaker, redundancy).

[EXECUTION LOG]
- Map out the transition states.
- For each step, explicitly compute $[EU(S), AR(S)]$.
- Choose the next state transition specifically targeted to reduce whichever index is higher.
- Stop when both $EU(S) \le 2$ and $AR(S) \le 3$.
```

---

### Template 19: Stepwise Residual Error Estimation ($\Delta$-Scoring)
* **Causal Mechanism:** Tracking delta variance between expected heuristic score outcomes and actual realized sub-state outputs.
* **Educational Utility:** Illustrates adaptive calibration of heuristic accuracy across execution chains.

```markdown
Analyze the target mathematical/logic proof via Stepwise Residual Delta-Scoring.

[INPUT PROOF / DERIVATION]
{{PROOF_STEPS}}

[DELTA-SCORING ENGINE]
For each discrete step $k$ in the deduction:
1. Prior Heuristic Expectation $E(S_k)$: Score representing predicted validity before parsing details [0-10].
2. Realized Step Soundness $R(S_k)$: Actual formal validity after structural parsing [0-10].
3. Compute Step Residual Error: $\Delta_k = |E(S_k) - R(S_k)|$.
4. Cumulative Invalidation Metric: $C_k = \sum_{j=1}^k \Delta_j$.

[CALIBRATION DRIFT ALGORITHM]
- IF $\Delta_k \ge 3$: Flag step $k$ as "High Divergence / Hallucination Risk". Halt derivation; regenerate step $k$ with explicit intermediate logical assertions.
- IF $C_k \ge 6$: Terminate entire proof trajectory. Step-level variance indicates compound hallucination drift. Re-initialize from the last known state where $\Delta == 0$.

Produce the complete Stepwise Score Card and verified sound proof.
```

---

### Template 20: Meta-Evaluative Controller with Dynamic Heuristic Re-weighting
* **Causal Mechanism:** A meta-level supervisory loop that dynamically audits the efficacy of lower-level heuristic scoring weights throughout search traversal.
* **Educational Utility:** Teaches meta-prompting and dynamic self-reflection at the scoring-function level.

```markdown
Act as a Dual-Level Reasoning Architecture (Meta-Controller + Search Agent) to resolve the strategic roadmap challenge.

[BUSINESS & TECHNICAL CONFLICT]
{{STRATEGIC_SCENARIO}}

[LEVEL 1: SEARCH AGENT]
Proposes candidate execution paths and scores them using the active heuristic vector:
$\vec{H}(S) = [w_1 \cdot Speed\_to\_Market + w_2 \cdot Tech\_Debt\_Avoidance + w_3 \cdot Unit\_Economics]$

[LEVEL 2: META-CONTROLLER (Runs every 2 steps)]
1. Audit the effectiveness of $\vec{H}(S)$:
   - Are the current weights causing the Search Agent to generate fragile solutions?
   - If YES: Mutate the weights. (e.g., Increase $w_2$, Decrease $w_1$).
   - Log weight update: $\vec{W}_{old} \to \vec{W}_{new}$ with operational rationale.
2. Evaluate Search Frontier:
   - Calculate search momentum: Rate of score improvement over the last two iterations.
   - If momentum < 10%: Inject a disruptive constraint perturbation to force exploration of alternate state spaces.

Execute the dual-loop optimization until the Meta-Controller certifies convergence on an optimal, robust state.
```

---

# OPERATIONAL FRAMEWORK: EXECUTION HEURISTICS FOR SELF-PACED MASTERY

To extract maximum signal when practicing and deploying State-Space Evaluation prompt architectures, adhere to the following operational parameters.

```
       [Prompt Execution]
               │
               ▼
   [Score Spread Audit: σ > 1.5] ──(FAIL: Collapse)──► [Amplify Contrasts / Force Rationale]
               │ (PASS)
               ▼
   [Pathological Path Pruning]  ──(FAIL: Leakage)───► [Enforce Hard Invariants & Early Exits]
               │ (PASS)
               ▼
[Convergence & Monotonicity Check]
```

### 1. Heuristic Function Calibration & Antidotes to Metric Collapse

| Diagnostic Failure | Root Cause | Architectural Fix |
| :--- | :--- | :--- |
| **Heuristic Flattening** (All states score identical values, e.g., 8/10). | LLM exhibits central-tendency bias when judging its own generations. | **Enforce Relative Ranking Prior to Absolute Scoring:** Force the model to pairwise-rank candidates before assigning scalar ratings. Define anchor rubrics with strict explicit penalties (e.g., `-3 points automatically if dependency X is unaddressed`). |
| **Optimism Hallucination** ($h(n)$ rapidly decreases without real progress). | Model awards credit for intent rather than realized constraints. | **Negative Evidence Weighting:** Require the prompt to extract explicit "Deficiencies & Failure Modes" *before* writing down the numeric score. Make $h(n)$ an inverse count of unresolved verified criteria. |
| **Metric Dominance** (A single easy-to-satisfy metric dictates output). | Vector collapse into unweighted scalar sums. | **Non-Linear Utility Penalties:** Use multiplicative interaction terms (e.g., $Score = Metric_A \times Metric_B$) or harmonic means where an abysmal score on one metric zero-out the aggregate state value. |

### 2. Concrete Practice Protocol for Students

To master these architectures through deliberate practice:

1. **Step 1: The Score-Spread Test:** Run a template with temperature $T=0.7$. Check the variance $\sigma^2$ across your heuristic scores. If $\sigma < 1.5$ on a 10-point scale, your evaluation function lacks operational contrast. Add adversarial evaluation rubrics.
2. **Step 2: Pathological Edge Injection:** Inject toxic or unviable constraints into `{{INPUT}}`. Monitor whether the algorithm actually triggers pruning, backtracking, or invariant hard-drops. If the model accommodates the toxic constraint by smoothing the score, tighten the rejection threshold.
3. **Step 3: Traversal Graph Visualization:** Extract the log tables output by the LLM and plot them using a Mermaid.js state diagram or tree graph. If the graph is purely linear ($1 \to 1 \to 1$), the state-space framing is failing to enforce exploration. True state-space reasoning creates bifurcations, prunes dead branches, and displays explicit backtrack loops.

### 3. Sampling Engine Configuration

| Hyperparameter | Setting for Search Prompts | Rationale |
| :--- | :--- | :--- |
| **Temperature** | `0.2 - 0.4` (Evaluation) / `0.7 - 0.8` (Expansion) | High temperature during candidate generation expands the frontier width; low temperature during scoring guarantees objective evaluation consistency. |
| **Top-P** | `0.85 - 0.92` | Prevents tail-entropy hallucination from entering the candidate pool while preserving enough variance for viable branching. |
| **Presence Penalty** | `0.3 - 0.5` (When expanding branches) | Penalizes token overlap across parallel candidate states, preventing the search beam from collapsing into redundant paraphrases. |
