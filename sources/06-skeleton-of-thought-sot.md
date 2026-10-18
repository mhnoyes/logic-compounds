### Architectural Taxonomy: Skeleton-of-Thought (SoT)

Skeleton-of-Thought (SoT) fundamentally shifts generative models from sequential autoregression across an entire response to a two-phase decoupled cognitive process:
1. **Phase 1: Macro-Structural Assembly (The Skeleton)** — Emits a minimal, non-redundant, dependency-mapped structural backbone (graph, list, state transition matrix, or outline).
2. **Phase 2: Independent/Coordinated Infill (The Flesh)** — Expands individual nodes either sequentially or via parallelized context windows, suppressing associative drift and hallucination compounding.

```
[Raw User Objective / Problem Spec]
                 │
                 ▼
┌─────────────────────────────────────────────────────────┐
│ PHASE 1: Structural Synthesis (The Skeleton)            │
│ - Topological sort / DAG generation                     │
│ - Contractual boundaries & MECE decomposition           │
│ - Strict token-budgeted constraint anchors              │
└─────────────────────────────────────────────────────────┘
                 │
      ┌──────────┼──────────┬──────────┐
      ▼          ▼          ▼          ▼
   [Node 1]   [Node 2]   [Node 3]   [Node N]  (Phase 2: Infill Expansion)
      │          │          │          │      (Evaluated against invariants)
      └──────────┴──────────┴──────────┘
                 │
                 ▼
┌─────────────────────────────────────────────────────────┐
│ INTEGRATION & SYNTHESIS GATE                            │
│ - Cross-node state reconciliation                       │
│ - Global consistency & verification pass                │
└─────────────────────────────────────────────────────────┘
```

#### Taxonomy of Causal Mechanisms

```
SKELETON-OF-THOUGHT (SoT)
├── 1. Linear & Hierarchical Decomposition
│   └── Mechanisms: Chronological pipelines, functional breakdowns, top-down tree scoping.
├── 2. Constraint-Coupled & Invariant-First
│   └── Mechanisms: State invariants, boundary contract definitions, failure-mode isolation.
├── 3. Topological & Directed Acyclic Graph (DAG)
│   └── Mechanisms: Prerequisite ordering, data-dependency resolution, asynchronous dispatch.
├── 4. Dialectical & Multi-Perspective
│   └── Mechanisms: Thesis-antithesis tension, Pareto frontiers, multi-agent red/blue partitioning.
└── 5. Recursive & Fractal Scale
    └── Mechanisms: Multi-tier resolution zooming (L1 Macro -> L2 Subsystem -> L3 Primitive).
```

---

### 20 Production-Grade Prompt Templates for SoT Mastery

---

#### Category 1: Linear & Hierarchical Decomposition

##### Template 1: Production Distributed Systems Architecture Blueprint
* **Causal Mechanism:** Macro-to-micro functional partitioning; prevents cross-tier architectural conflation by decoupling topology from component-level specifications.
* **Mastery Focus:** Learning to decouple system interface boundaries from internal component state.

```markdown
You are a Principal Distributed Systems Infrastructure Architect.
Task: Design a production-grade, globally distributed, fault-tolerant {{SYSTEM_TYPE}} handling {{LOAD_SPEC}}.

Execute strictly in two decoupled phases.

### PHASE 1: SKELETON GENERATION
Emit ONLY a numbered structural skeleton (1.0 to N.0). 
Constraints for Phase 1:
- Must follow strict MECE (Mutually Exclusive, Collectively Exhaustive) decomposition across the OSI/system stack.
- Do NOT generate prose, explanations, or code.
- Each node must contain: [Node Name] | [Exact Input Contract] | [Exact Output Contract] | [Critical Failure Mode].
- Cap token budget for this skeleton at 250 tokens.

Wait for internal verification: "SKELETON_LOCKED".

### PHASE 2: PARALLEL NODE EXPANSION
Iterate sequentially through each node from Phase 1. Expand each node into a production-grade specification containing:
1. Architectural Blueprint: Data models, consensus mechanisms, state-machine transitions.
2. Latency/Throughput Budgets: P99 latency bounds, network serialization cost, concurrency models.
3. Resilience Protocol: Dynamic failover, circuit-breaking topologies, backpressure propagation.
4. Minimal Concrete Artifact: Interface definitions (gRPC/Protobuf) or core algorithms in pseudocode.

Boundary Condition: Complete the expansion of each node in isolation without repeating the skeleton headers or leaking implementation details across non-adjacent nodes.
```

##### Template 2: Algorithmic Complexity & Correctness Proof
* **Causal Mechanism:** Top-down induction scaffolding; anchors lemmas and structural invariants before emitting rigorous operational logic.
* **Mastery Focus:** Prevents algorithmic hand-waving by requiring formal assertions prior to pseudocode realization.

```markdown
Target Problem: Design an optimal algorithm to solve {{ALGORITHMIC_PROBLEM}} under the following constraints: {{CONSTRAINTS}}.

Execute using an invariant-anchored Skeleton-of-Thought approach:

### PHASE 1: THE PROOF SKELETON
Construct the formal structural framework of the solution. Output ONLY the following components:
1. Invariant Assertions: Pre-conditions, loop/state invariants, post-conditions.
2. Inductive Base Cases: Trivial state edge cases.
3. Inductive Step Mapping: Transformation state function $T(S) \to S'$.
4. Complexity Target Ceiling: Target Time Complexity, Target Space Complexity (Auxiliary).
Do not generate implementation details. Conclude Phase 1 with delimiter: `[SKELETON_FINALIZED]`.

### PHASE 2: OPERATIONAL IMPLEMENTATION
Using the invariants defined in Phase 1 as rigid boundaries, generate:
1. Algorithmic Pseudocode (strictly typed, fully annotated with assert statements matching Phase 1).
2. Formal Correctness Proof via induction or contradiction directly referencing the skeleton's invariants.
3. Tight Asymptotic Analysis ($O$, $\Omega$, $\Theta$) with recurrence relation expansions.
```

##### Template 3: Enterprise Strategy & Quantitative GTM Framework
* **Causal Mechanism:** Functional value-chain decoupling; forces clean lines between target economics, channel mechanics, and operational execution.
* **Mastery Focus:** Eliminating strategic boilerplate by enforcing quantitative metrics at the skeleton level.

```markdown
Context: Enterprise strategic deployment of {{PRODUCT_OR_TECHNOLOGY}} targeting {{TARGET_VERTICAL}}.
Capital Constraints: {{CAPITAL_CONSTRAINTS}} | Target Horizon: {{TIME_HORIZON}}.

Generate an end-to-end Go-To-Market execution blueprint using SoT:

### PHASE 1: EXECUTION SKELETON
Emit a compressed structural matrix formatted as:
`[Pillar ID] | [Operational Scope] | [North-Star Metric] | [Fatal Execution Risk]`
Cover all critical organizational dimensions: Unit Economics, ICP Definition, Channel Architecture, Regulatory/Compliance, and Retention Loops.
Prohibit qualitative prose. Maximize information density per token.

### PHASE 2: INFILL EXECUTION
Expand each Pillar ID into a self-contained operational directive:
- Deterministic formulas for all metrics (e.g., LTV:CAC, Magic Number, Net Revenue Retention).
- Step-by-step 30-60-90 day tactical playbooks for that specific pillar.
- Failure-mode trigger actions: Explicit metrics threshold causing strategy invalidation.
```

##### Template 4: Complete Refactoring Strategy for Legacy Codebases
* **Causal Mechanism:** Dependency boundary extraction; prevents scope creep by fixing modification surfaces before touching code.
* **Mastery Focus:** Mastering safe state transition planning in high-cyclomatic-complexity systems.

```markdown
Given the following legacy codebase context: {{CODEBASE_SUMMARY_OR_SNIPPET}}.
Refactoring Objective: Modernize to {{TARGET_PARADIGM}} while maintaining 100% backward compatibility and zero downtime.

Execute using Skeleton-of-Thought:

### PHASE 1: REFACTORING SCAFFOLD
Output a chronological sequence of non-breaking transformation milestones:
- Stage ID
- Mutation Target (Classes, Functions, or Services to modify)
- Regression Invariant (What dynamic behavior MUST NOT change)
- Decoupling Mechanism (Adapter, Strangler Fig, Facade, Branch by Abstraction)

Halt output after generating the scaffold.

### PHASE 2: ATOMIC MUTATION IMPLEMENTATION
For each Stage ID in the scaffold:
1. Emit before/after abstract syntax tree or class interface signatures.
2. Provide precise diffs/implementations showing the modernization step.
3. Write automated verification contract: Integration tests or property-based test definitions ensuring the Regression Invariant holds.
```

---

#### Category 2: Constraint-Coupled & Invariant-First Skeletons

##### Template 5: Safety-Critical Finite State Machine (FSM) Specification
* **Causal Mechanism:** Closed-world assumption enforcement; bounds all possible transitions in an immutable skeleton before detailing logic.
* **Mastery Focus:** Eliminating undefined states and race conditions in concurrent/reactive systems.

```markdown
Role: Safety-Critical Systems Engineer (DO-178C / ISO 26262 standard).
System: Design the complete control logic for {{SAFETY_CRITICAL_SUBSYSTEM}}.

### PHASE 1: STATE SPACE & TRANSITION SKELETON
Map the comprehensive state space. Output ONLY a strict transition table format:
`Current State | Trigger / Event | Guard Condition | Next State | Worst-Case Failure Mode`
Requirements:
- Account for power-loss, bit-flip, sensor timeout, and out-of-bounds input.
- System must be mathematically closed: No unhandled transitions.
- No prose explanations. Output the matrix and append `[STATE_SPACE_CLOSED]`.

### PHASE 2: RIGOROUS TRANSITION INFILL
Expand every row of the transition table into:
1. Low-level algorithmic handling routines (C99 compliant, no dynamic allocation, MISRA compliant).
2. Deterministic timing bounds: Execution time ceiling ($t_{wcet}$).
3. Telemetry and fail-operational/fail-safe fallback triggers.
```

##### Template 6: Zero-Knowledge / Cryptographic Protocol Verification
* **Causal Mechanism:** Boundary contract generation; fixes verification goals, assumptions, and threat models prior to proof synthesis.
* **Mastery Focus:** Isolating trust assumptions to prevent mathematical leakage across cryptographic steps.

```markdown
Objective: Formally verify or architect a cryptographic scheme for {{CRYPTOGRAPHIC_GOAL}} under threat model {{THREAT_MODEL}}.

### PHASE 1: TRUST ASSUMPTION & INTERFACE SKELETON
Generate the formal security game skeleton:
1. Setup Parameters & Invariants
2. Hardness Assumptions (e.g., LWE, DL, CDH)
3. Oracle Interfaces (Adversary access points)
4. Formal Security Definitions (e.g., IND-CPA, IND-CCA2, Soundness, Zero-Knowledge)
Strict format: LaTeX-compatible formal statements only. No descriptive background text.

### PHASE 2: MATHEMATICAL REALIZATION
Inject the structural mechanics into each phase-1 module:
- Concrete construction of KeyGen, Sign/Prove, and Verify primitives.
- Reduction proof: Rigorous step-by-step reduction showing that breaking the scheme breaks the underlying hardness assumption.
- Security parameter sizing calculations for $\kappa = 128$ and $\kappa = 256$ bit security.
```

##### Template 7: Multi-Jurisdictional Regulatory & Compliance Engine
* **Causal Mechanism:** Legal invariant scaffolding; maps disjoint jurisdictional constraints into a shared evaluation skeleton.
* **Mastery Focus:** Structuring multi-variate compliance domains to prevent jurisdictional bleed.

```markdown
Context: Launching an autonomous {{PRODUCT/PLATFORM}} operating across: {{JURISDICTIONS_LIST}}.
Regulatory Domains: Data Sovereignty, Consumer Protection, Financial Compliance, and Algorithmic Auditing.

Execute in two SoT phases:

### PHASE 1: COMPLIANCE INVARIANT SCAFFOLD
Emit a unified compliance taxonomy. For every regulatory jurisdiction, specify:
`Jurisdiction | Regulatory Body | Statute/Rule | Strict System Invariant | Penalty Severity Ceiling`
Zero commentary. Maximum structural precision.

### PHASE 2: TECHNICAL IMPLEMENTATION INFILL
Convert each invariant row into engineering specifications:
1. Data Storage & Sharding Schema (Cryptographic guarantees, regional isolation).
2. Audit Log Provenance Architecture (Append-only, verifiable logs).
3. Automated Enforcement Engine (Interceptors, validation middleware, and automated reporting pipelines).
```

##### Template 8: Cost-Optimal Cloud Infrastructure Synthesis
* **Causal Mechanism:** Budget-bounded resource mapping; fixes cost and throughput ceilings prior to provisioning topology.
* **Mastery Focus:** Learning to treat cost/financial limits as hard computational invariants during system design.

```markdown
Objective: Design the cloud architecture for {{SYSTEM_LOAD}} within a strict monthly budget ceiling of ${{MONTHLY_BUDGET}} on {{CLOUD_PROVIDER}}.

### PHASE 1: RESOURCE ALLOCATION SKELETON
Generate the resource-to-cost allocation matrix:
`Subsystem | Service Type | Sizing/Instance Tier | Expected Utilization | Monthly Cost Allocation | Auto-scale Invariant`
Ensure the sum of all monthly cost allocations <= ${{MONTHLY_BUDGET}} * 0.85 (holding 15% buffer).
Output no descriptive text. Only the balanced ledger.

### PHASE 2: PROVISIONING INFILL
For each subsystem listed in Phase 1:
1. Infrastructure-as-Code (Terraform/OpenTofu) production block.
2. Network topology: Ingress/egress routing, VPC endpoints, NAT-gateway avoidance strategies.
3. Cost-governance automation: Anomaly-detection alerts and auto-downscaling policies.
```

---

#### Category 3: Topological & Directed Acyclic Graph (DAG) Skeletons

##### Template 9: Critical-Path Zero-Downtime Database Migration
* **Causal Mechanism:** Topological execution ordering; enforces strict serial vs. parallel node dependencies to prevent lock contention and data corruption.
* **Mastery Focus:** Mastering explicit synchronization barriers in distributed state changes.

```markdown
Input: Migrate data and live write-traffic from {{SOURCE_DB}} to {{TARGET_DB}}.
Traffic Profile: {{QPS_READS}} reads/sec, {{QPS_WRITES}} writes/sec. Max downtime allowed: 0 seconds.

### PHASE 1: TOPOLOGICAL DAG SKELETON
Map the migration as a strict Directed Acyclic Graph (DAG). Format:
`Node ID | Task Description | Explicit Prerequisites (Node IDs) | Concurrency (Serial/Parallel) | Rollback Trigger`
Order must be topologically sorted: no node can appear before its dependencies.
Emit solely the sorted DAG definition.

### PHASE 2: ATOMIC NODE DRILL-DOWN
Traverse the DAG and expand each task node:
1. Dual-write / Shadow-read proxy logic (with pseudocode/configuration).
2. Data synchronization and backfill engine with auto-throttling based on source replication lag.
3. Reconciliation and divergence detection workers.
4. Final cutover gate: Cutover criteria checklist and deterministic rollback playbook.
```

##### Template 10: Deep Learning Distributed Training Pipeline
* **Causal Mechanism:** Staged lifecycle dependencies; decouples cluster topology, data pipelines, training dynamics, and post-processing.
* **Mastery Focus:** Aligning distributed hardware configurations with algorithmic pipeline steps.

```markdown
Task: Configure the distributed training run for a {{PARAMETER_SIZE}} foundation model on {{GPU_TOPOLOGY}}.
Objective: Maximize Model FLOPs Utilization (MFU) while mitigating loss spikes.

### PHASE 1: PIPELINE DAG SKELETON
Generate the distributed training execution lifecycle as an execution graph:
Nodes must encompass: Data ingestion/packing -> Parallelism partitioning (TP/PP/DP/SP) -> Checkpointing orchestration -> Optimizer step -> Dynamic loss monitoring.
Include: `[Step ID] | [Hardware Resource Bound] | [Communication Overhead Class] | [Dependency]`.
Do not expand details. Lock the graph.

### PHASE 2: DISTRIBUTED RUNTIME INFILL
Generate the exact operational engineering specifications for each node:
1. Exact parallelization strategy configuration (Megatron-LM / DeepSpeed configuration schemas).
2. Collective communication primitives utilized (All-Reduce, All-Gather, Reduce-Scatter) and overlap with compute kernels.
3. Automated fault-tolerance: Dynamic node failure detection and elastic checkpoint reloading.
```

##### Template 11: Hardware-Software Co-Design Embedded Interface
* **Causal Mechanism:** Hardware abstraction layering; anchors register/bus capabilities before expanding software driver stacks.
* **Mastery Focus:** Eliminating memory unsafety and timing violations at bare-metal interfaces.

```markdown
Context: Building an ultra-low-latency Linux kernel driver/userspace interface for {{CUSTOM_HARDWARE_OR_FPGA}} communicating via PCIe/DMA.

Execute in two phases:

### PHASE 1: REGISTER & TRANSACTION SKELETON
Draft the exact register layout and communication pipeline graph:
1. Base Address Register (BAR) spatial memory map: Offsets, Read/Write permissions, Reset values, Bitfield definitions.
2. Hardware interrupt and DMA descriptor lifecycle DAG.
Zero natural language descriptions. Format strictly as C structs and a textual DAG.

### PHASE 2: DRIVER SUBSYSTEM REALIZATION
Flesh out the software primitives anchored to the Phase 1 skeleton:
1. Zero-copy ring buffer initialization and memory mapping logic (`mmap` interface).
2. Interrupt Service Routine (ISR) bottom-half / polling mechanism (NAPI-style or epoll-driven).
3. Memory barrier placements (`mb()`, `rmb()`, `wmb()`) preventing compiler and CPU out-of-order execution hazards.
```

##### Template 12: M&A Technical Due Diligence & Debt Audit
* **Causal Mechanism:** Systematic dependency risk analysis; categorizes enterprise risk down the functional chain from codebase to operational infrastructure.
* **Mastery Focus:** Learning systematic risk auditing without conflating subjective quality with structural failure.

```markdown
Target Entity: Acquisition target {{ACQUISITION_TARGET}}, generating ${{ARR}} ARR with a stack of {{TECH_STACK}}.
Primary Concern: Identifying technical debt, intellectual property contagion, and security vulnerabilities.

### PHASE 1: RISK AUDIT TAXONOMY SKELETON
Construct the comprehensive Due Diligence Investigation Framework:
`Audit Vector | Target Component | Diagnostic Probe / Metric | Material Deal-Breaker Threshold`
Vectors: Architecture scalability, Open Source licensing risks (GPL contamination), Infrastructure debt, Team key-person dependencies.
Provide only the matrix.

### PHASE 2: INVESTIGATION DIRECTIVES & DRILL-DOWN
Expand each Audit Vector into a complete operational methodology:
1. Specific static analysis, dependency scanning, and git forensic commands/heuristics to run.
2. Architecture stress tests: Exact queries and chaos simulations to execute during the access period.
3. Post-acquisition remediation cost model: Expected engineering headcount and capital expenditure required to bring each vector to enterprise grade.
```

---

#### Category 4: Dialectical, Adversarial & Multi-Perspective Skeletons

##### Template 13: Red-Team Offensive Attack Vector Matrix
* **Causal Mechanism:** Threat-modeling vector divergence; maps exhaustive lateral movement pathways before scripting atomic exploits.
* **Mastery Focus:** Systematic exploitation mapping without skipping persistence and privilege boundaries.

```markdown
Target System: Enterprise Kubernetes deployment running {{TARGET_APPLICATION}} with IAM integrated with AWS/GCP.
Objective: Complete penetration testing methodology assuming an initial unprivileged container compromise.

### PHASE 1: CYBER KILL-CHAIN SKELETON
Map the attack surface as an adversarial decision tree:
`Stage ID | Attack Objective | Technique (MITRE ATT&CK ID) | Required Privilege | Artifacts Left Behind`
Sequence from Discovery -> Privilege Escalation -> Lateral Movement -> Data Exfiltration.
Output only the tabular kill-chain skeleton.

### PHASE 2: EXPLOIT & DETECT INFILL
For each Stage ID in the kill-chain, generate a comprehensive dual dossier:
1. Offensive Implementation: Low-level terminal commands, API interactions, or exploit payloads.
2. Blue-Team Invariant: Exact SIEM detection rules (Sigma/YARA rules), kernel tracing triggers (eBPF), and automated defensive kill switches.
```

##### Template 14: Game-Theoretic Mechanism Design & Equilibrium Analysis
* **Causal Mechanism:** Strategic conflict partitioning; bounds players, action sets, and utility functions before solving for equilibria.
* **Mastery Focus:** Formalizing incentive landscapes prior to running behavioral or outcome derivations.

```markdown
Objective: Design a decentralized mechanism for {{MECHANISM_GOAL}} that is Byzantine-fault-tolerant, Sybil-resistant, and Collusion-resistant.

### PHASE 1: GAME-THEORETIC SKELETON
Formally define the mathematical model:
1. Agents / Players: Distinct actor classes and their information sets.
2. Action Spaces: Permissible actions per player tier.
3. Utility Functions: Quantitative payout/slashing equations for each actor.
4. Solution Concept Targets: Strong Nash Equilibrium, Bayesian-Nash, or Dominant Strategy Incentive Compatibility (DSIC).
Do not generate proofs or narratives. Output the mathematical definitions only.

### PHASE 2: MECHANISM EXPANSION & EQUILIBRIA PROOFS
Synthesize the operational rules and proofs based on Phase 1:
1. Mathematical proof of Incentive Compatibility: Show that truth-telling/optimal protocol adherence strictly dominates deviation.
2. Attack Cost Function: Minimum capital required to execute a 51%, bribery, or front-running attack.
3. Algorithmic Implementation: Smart contracts or protocol state-machine logic enforcing the payoffs.
```

##### Template 15: Architectural Trade-Off Tournament: Event-Driven vs. CRDT
* **Causal Mechanism:** Comparative dialectic scaffold; builds balanced evaluation dimensions before pitting systems against each other.
* **Mastery Focus:** Eliminating cognitive bias toward preferred architectural patterns through symmetric evaluation.

```markdown
Problem Statement: Architecting a real-time collaborative workspace platform with {{CONCURRENT_USERS_PER_DOC}} simultaneous editors under high network partition conditions.

### PHASE 1: COMPARATIVE SKELETON MATRIX
Establish the comparative tournament dimensions:
`Evaluation Axis | Paradigm A: Event-Driven Log Architecture | Paradigm B: State-based CRDT Architecture | Decisive Stress Test Metric`
Axes must include: Eventual Consistency Guarantees, Memory Growth per Document, Conflict Resolution Determinism, Client-Side Compute Overhead, and Engineering Maintenance Complexity.
Provide zero analysis. Emit the evaluation matrix only.

### PHASE 2: RIGOROUS COMPARATIVE INFILL
Expand each Evaluation Axis into a detailed, data-backed operational assessment:
1. Algorithmic trade-off breakdown with concrete edge-case walkthroughs (e.g., concurrent split-brain mutations).
2. Network serialization benchmarks and client/server CPU memory footprint projections.
3. Final Synthesized Verdict: Explicit heuristics dictating when Paradigm A must be chosen over Paradigm B, and vice-versa.
```

##### Template 16: Quantitative Portfolio Risk Factor Stress-Testing
* **Causal Mechanism:** Macro-factor decomposition; separates underlying macroeconomic shocks from correlated asset responses.
* **Mastery Focus:** Decoupling causal economic shocks from complex multi-asset volatility transmissions.

```markdown
Portfolio Profile: {{PORTFOLIO_CONSTITUENTS}} with total assets of ${{AUM}}.
Scenario: Simultaneous Stagflationary Shock + Liquidity Crisis comparable to 1973/2008.

### PHASE 1: FACTOR TRANSMISSION SKELETON
Map the risk shock transmission channels as a hierarchical matrix:
`Channel ID | Macro Factor Shock | Direct Asset Class Exposure | Secondary Liquidity Spiral Mechanism`
Cover: Sovereign Yield Curves, FX Spreads, Credit Default Spreads, Equities Multiples, and Volatility Surfaces.
Emit purely the matrix.

### PHASE 2: QUANTITATIVE DRILL-DOWN & REBALANCING PLAYBOOK
Iterate through each Channel ID:
1. Formulate the mathematical shock: Value-at-Risk (VaR), Expected Shortfall (CVaR), and maximal drawdown calculations under the shock.
2. Correlation Breakdown Analysis: Projected shifts in asset correlations ($r_{i,j} \to 1$).
3. Systematic Hedging Strategy: Derivative structures (options straddles, CDS, interest rate swaps) to neutralize the factor exposure efficiently.
```

---

#### Category 5: Recursive & Fractal Scale Skeletons

##### Template 17: Production Compiler Optimization Pass Architecture
* **Causal Mechanism:** Intermediate representation (IR) level-refinement; steps recursively through optimization tiers from AST down to machine code.
* **Mastery Focus:** Maintaining semantic invariance across multi-pass compilation pipelines.

```markdown
Language Spec: Designing an optimizing compiler pass for a high-performance DSL targeting {{HARDWARE_TARGET}}.
Goal: Maximize SIMD vectorization and minimize memory bandwidth overhead.

### PHASE 1: PASS-PIPELINE SKELETON
Generate a sequential optimization pass DAG:
`Pass Level | Pass Name | Input IR Type | Output IR Type | Preserved Semantic Invariant`
Levels must span: High-Level IR (Loop transformations) -> Mid-Level IR (SSA optimization, Constant propagation, Dead code elimination) -> Low-Level IR (Register allocation, Instruction scheduling).
Zero operational code. Skeleton only.

### PHASE 2: PASS LOGIC & PATTERN REWRITE RULES
For each Pass Name in the skeleton:
1. Pattern-matching rewrite rules in pseudocode or MLIR table-gen syntax.
2. Correctness verification: Prove that transformation does not alter observable program behavior.
3. Cost model: Heuristic estimating instruction cost before and after transformation.
```

##### Template 18: Autonomous Agent Cognitive Loop & Tool-Use Engine
* **Causal Mechanism:** Recursive meta-cognitive decomposition; separates environment perception, dynamic planning, tool selection, and reflection.
* **Mastery Focus:** Eliminating infinite agentic planning loops by hard-bounding control branches in advance.

```markdown
Objective: Construct an autonomous coding agent runtime capable of solving complex SWE-bench style issues in {{TARGET_REPO}}.

### PHASE 1: AGENT COGNITIVE STATE SKELETON
Construct the recursive operational loop topology:
`State Node | Cognitive Action | Admissible Tool Invocations | Termination Condition | Reflection Threshold`
Include: Context Ingestion -> Hypothesis Generation -> Code Localization -> Mutation -> Sandboxed Test Execution -> Error Correction.
Output only the structured topological loop.

### PHASE 2: RUNTIME SPECIFICATION INFILL
Detail each state node into an execution runtime specification:
1. Exact prompt templates and context-packing strategies for that specific step.
2. Structured tool-calling contracts (JSON-schema definitions for code search, file editing, and test execution).
3. Reflection & Self-Critique algorithms: Exact logic to detect when the agent is stuck in repetitive hallucination or unproductive edit loops.
```

##### Template 19: Domain-Specific Language (DSL) & Formal Grammar Synthesis
* **Causal Mechanism:** Syntax-to-semantics stratification; builds grammar invariants (EBNF) before implementing AST interpreters and type-checkers.
* **Mastery Focus:** Learning how grammar constraints dictate execution model correctness.

```markdown
Task: Architect a Domain-Specific Language for defining {{DSL_PURPOSE_DOMAIN}}.
Requirements: Statically typed, Turing-incomplete by design, provably terminating.

### PHASE 1: FORMAL GRAMMAR SKELETON
Output the complete EBNF (Extended Backus-Naur Form) grammar specification of the DSL.
Define:
- Lexical tokens
- Production rules
- Type declaration expressions
- Statement/expression hierarchies
Output exclusively the formal EBNF code block.

### PHASE 2: RUNTIME ENGINE REALIZATION
Anchoring directly to the EBNF grammar:
1. Synthesize the Abstract Syntax Tree (AST) node hierarchy (in TypeScript, Rust, or Python dataclasses).
2. Type-Inference & Checking Algorithm: Formal typing rules (inference judgments) with handling for invalid states.
3. Deterministic Evaluator / Interpreter: Execution loop guaranteeing termination within $O(N)$ operations.
```

##### Template 20: Complex Enterprise Re-Platforming Strategy & Governance
* **Causal Mechanism:** Fractal organizational & systems decomposition; aligns high-level business capability models down to team-level execution boundaries.
* **Mastery Focus:** Concurrently handling architectural modernization alongside organizational operational realities (Conway's Law).

```markdown
Enterprise Scope: Legacy Monolith Re-platforming for {{ENTERPRISE_DESCRIPTION}}.
Scale: {{ENGINEERING_HEADCOUNT}} engineers, {{NUM_MICROSERVICES_TARGETED}} target microservices, Zero service disruption.

### PHASE 1: MULTI-TIER ARCHITECTURAL SKELETON
Generate a multi-scale structural decomposition:
- Level 1: Domain-Driven Business Capability Domains (Bounded Contexts)
- Level 2: Team Topology & Ownership Mapping (Stream-aligned, Platform, Enabling)
- Level 3: Platform Infrastructure Core Services
Emit this purely as an indented, structured hierarchy. Append `[SKELETON_STRUCTURE_LOCKED]`.

### PHASE 2: OPERATIONAL EXECUTION DRILL-DOWN
Expand each branch of the hierarchy:
1. Bounded Context Interface Contracts: Event schemas, API gateway definitions, and domain event catalogs.
2. Conway’s Law Migration Map: Specific team restructuring, ownership handoff protocols, and cognitive-load bounding.
3. Dual-Run Verification: Methodology to run legacy monolith and modernized domain microservices in shadow parity with automated reconciliation.
```

---

### Operational Framework: Execution Heuristics for Self-Paced Mastery

#### 1. The Core Metrics of Skeleton Quality
When practicing SoT prompt design, measure the Phase 1 skeleton against these technical criteria:

| Metric | Target | Failure Mode (Drift) |
| :--- | :--- | :--- |
| **Shannon Structural Density** | High (few words, pure structure) | Conversational introductions, early implementation code, pleasantries. |
| **MECE Coefficient** | 100% (No overlapping node scopes) | Multiple nodes attempting to solve the same concern (e.g., error handling scattered vs. isolated). |
| **Interface Determinism** | Explicit I/O specifications per node | Vague outlines ("Discuss security") instead of strict contracts (`[Input: JWT] -> [Output: ClaimsPrincipal]`). |
| **Branch Invariance** | True DAG | Circular dependencies between structural nodes. |

#### 2. The Five Execution Rules for the Practitioner

##### Rule 1: The Token Barrier Invariant
Never allow the Phase 1 skeleton to consume more than 15-20% of your total context budget for the task. If a skeleton is verbose, the model loses the associative capacity needed to perform deep technical infill during Phase 2. Enforce strict delimiters like:
`"Do NOT generate prose, explanations, or code. Output only the structured matrix."`

##### Rule 2: Enforce Clean State Barriers
Always use deterministic stop-tokens or structural gates between Phase 1 and Phase 2 (e.g., `[SKELETON_LOCKED]`). When executing in multi-agent or multi-turn workflows, split the phases across separate API calls:
* *Call 1:* Generate and inspect the Skeleton.
* *Programmatic Interceptor:* Validate the skeleton using a deterministic parser (e.g., JSON schema, Pydantic, regex).
* *Calls 2 through $N$:* Parallelize the expansion of individual skeleton nodes by passing the skeleton and the specific target node into isolated prompts.

##### Rule 3: Decouple Sibling Dependencies
If Node 3 requires the output of Node 2's implementation, you have failed to build a pure Skeleton-of-Thought architecture; you have built a sequential chain. Re-architect the skeleton so that Node 2 and Node 3 depend **only** on the contractual interfaces defined in the Phase 1 skeleton, enabling true parallelization and preventing error compounding.

##### Rule 4: Dynamic Budgeting per Infill Node
Allocate variable token and compute budgets based on the complexity class of the skeleton node:
* High-complexity nodes (Algorithmic logic, formal proofs, low-level concurrency): Allocate 70% of remaining token capacity.
* Low-complexity nodes (Interface routing, configurations, boilerplate definitions): Cap tightly to avoid verbosity drift.

##### Rule 5: Recursive Verification Loop
When evaluating Phase 2 infill, always run a reconciliation pass:
$$\text{Reconciliation Gate}(Node_{expanded}) \to \text{assert}(Node_{expanded} \subseteq Invariants_{Phase 1})$$
If the infill violates any contract, state, or invariant declared in Phase 1, the output must be rejected and re-prompted using the violated invariant as a negative constraint.
