### Architectural Taxonomy of First-Principles Deconstruction

First-principles deconstruction systematically decomposes complex systems, problem spaces, or inherited dogmas into their fundamental, irreducible truths (primitives), verifies those primitives against physical, mathematical, or empirical laws, and reconstructs novel solutions strictly upward from the verified base.

```
┌────────────────────────────────────────────────────────────────────────┐
│                   FIRST-PRINCIPLES DECONSTRUCTION                      │
└────────────────────────────────────┬───────────────────────────────────┘
                                     │
       ┌─────────────────────────────┼─────────────────────────────┐
       ▼                             ▼                             ▼
┌──────────────┐              ┌──────────────┐              ┌──────────────┐
│ ONTOLOGICAL  │              │  CONSTRAINT  │              │ TELEOLOGICAL │
│  REDUCTION   │              │  DECOUPLING  │              │ RE-ANCHORING │
└──────┬───────┘              └──────┬───────┘              └──────┬───────┘
       │                             │                             │
       ├─ Semantic Stripping         ├─ Boundary Isolation         ├─ Functional Inversion
       ├─ Primitive Extraction       ├─ Physics/Limit Decoupling   ├─ Clean-Sheet Synthesis
       └─ Epistemic Grounding        └─ Path-Dependency Purge      └─ Substrate Migration
```

#### Core Causal Mechanisms
1. **Ontological Reduction (OR):** Stripping nominal labels, domain jargon, and analogical frameworks from a system to isolate raw states, fluxes, informational transformations, and mass-energy transactions.
2. **Axiomatic Grounding (AG):** Testing every derived assumption against bedrock invariants (laws of thermodynamics, information theory, formal logic, verified physical constraints) to eliminate epistemic debt.
3. **Constraint Decoupling (CD):** Isolating immutable physical or mathematical limits from mutable human, economic, organizational, and historical path-dependencies.
4. **Teleological Re-Anchoring (TR):** Isolating the absolute objective function (the *telos*) from the vehicle historically used to deliver it, enabling radical re-synthesis without legacy baggage.
5. **Adversarial Limit Testing (ALT):** Driving variables to boundary conditions ($\lim_{x \to 0}$, $\lim_{x \to \infty}$, localized failure) to identify the precise points where assumptions break down.

---

### Production-Grade Prompt Templates

#### Category 1: Ontological Reduction & Primitive Extraction

##### Template 1: The Semantic Lineage & Analogy Stripper
* **Mechanism:** Ontological Reduction (OR)
* **Objective:** Strip inherited industry terminology and analogies to expose the raw physical, logical, or data primitives of a problem space.

```markdown
You are an axiomatic ontological deconstructor. Your objective is to strip all analogical reasoning and semantic baggage from: [SYSTEM / DOMAIN PROBLEM].

Execution Protocol:
1. Lexical Audit: Identify all domain-specific metaphors, trade jargon, and inherited abstractions in [SYSTEM / DOMAIN PROBLEM]. 
2. Translation to Primitives: Map every identified term strictly into its irreducible components:
   - Physical layer: Mass, energy, material composition, physical movements.
   - Information layer: State changes, entropy, bits transferred, compute cycles, latency.
   - Economic layer: Base resources consumed, time expended, risk incurred.
3. Analogy Purge: Explicitly flag where current industry practices rely on "reasoning by analogy" (e.g., "doing X because it's like Y").
4. Bedrock State Matrix: Output a structured table of:
   | Conventional Abstraction | Irreducible Component | Governing Law/Invariant |
```

##### Template 2: Thermodynamic & Physical Limit Baseline
* **Mechanism:** Axiomatic Grounding (AG)
* **Objective:** Establish the non-negotiable physical minimum requirements for a process, ignoring all current commercial implementations.

```markdown
Analyze the theoretical versus practical limits of [PROCESS / TECHNOLOGY / WORKFLOW].

Deconstruct this process down to its governing physical and mathematical laws:
1. Thermodynamic / Theoretical Limit: What is the absolute physical minimum energy, time, or material required by fundamental laws (e.g., Carnot efficiency, Landauer's principle, Shannon capacity, Carnot/Betz limits) to achieve the terminal outcome? Provide the exact equations.
2. Current State Audit: What are the current industry metrics for achieving this outcome (energy, cost, time, waste)?
3. The Efficiency Gap: Quantify the gap between theoretical limits and current industrial practice:
   $$\text{Efficiency Delta} = \frac{\text{Current Resource Consumption}}{\text{Theoretical Minimum Resource Consumption}}$$
4. Parasitic Losses: Break down the delta into specific categories:
   - Fundamental engineering limits (near-term immutable)
   - Path-dependent design compromises (mutable)
   - Legacy procedural overhead (eliminable)
```

##### Template 3: State-Space Representation Extraction
* **Mechanism:** Ontological Reduction (OR)
* **Objective:** Convert a high-level operational or cognitive workflow into a formal state-transition graph.

```markdown
Deconstruct the following high-level operational domain into a deterministic state-space representation: [COMPLEX WORKFLOW / SYSTEM].

Perform the following reductions:
1. State Identification: Define the system strictly as $S = \{s_0, s_1, ..., s_n\}$, where each state $s$ is defined solely by measurable variables, without descriptive narrative.
2. Action Space: Define the discrete actions $A$ that transition the system between states.
3. Transition Model: Specify $T(s, a) \to s'$. Flag transitions that currently rely on probabilistic human heuristics versus deterministic execution.
4. Redundancy Identification: Identify all states $s_k$ where:
   - The state transition generates zero informational entropy reduction.
   - The state exists solely to audit, buffer, or mitigate errors introduced by a prior non-deterministic step.
Output the reduced, minimal state-transition model required to reach the terminal goal.
```

##### Template 4: Information-Theoretic Entropy Reduction
* **Mechanism:** Ontological Reduction (OR)
* **Objective:** Deconstruct decision-making or data-processing pipelines into raw signal, noise, and entropy resolution.

```markdown
Analyze the following decision-making pipeline through an information-theoretic lens: [DECISION / VERIFICATION PIPELINE].

Deconstruction Protocol:
1. Target Information Gain: What specific bit-level uncertainty is this pipeline designed to resolve? Define the prior entropy $H(X)$ and desired posterior entropy $H(X|Y)$.
2. Noise Audit: Identify every intermediate artifact, meeting, document, or check. Measure its true contribution to reducing $H(X)$.
3. Channel Capacity: Quantify the signal-to-noise ratio (SNR) across each handoff. Pinpoint where noise amplification occurs due to lossy cognitive or procedural compression.
4. Minimal Shannon Pipeline: Design the theoretically minimal path to extract the requisite bits of certainty, bypassing all non-entropy-reducing artifacts.
```

---

#### Category 2: Axiomatic Isolation & Epistemic Verification

##### Template 5: Recursive Socratic Epistemic Scaffolding
* **Mechanism:** Axiomatic Grounding (AG)
* **Objective:** Interrogate beliefs about a domain recursively until an empirically proven or mathematically irrefutable ground truth is reached.

```markdown
Subject the following claim/architecture to recursive Socratic deconstruction: [ASSERTION / CURRENT DESIGN PATTERN].

Execute a 5-layer recursive inquiry:
1. Premise Layer: What explicit assumptions support this assertion?
2. Justification Layer: For each assumption, why is it believed to be true? (Categorize: Empirical Observation, Authority/Consensus, Mathematical Proof, Historical Tradition).
3. Dependency Audit: If an assumption relies on "Authority" or "Historical Tradition," discard it immediately. Re-evaluate the surviving structure.
4. Counter-Axiomatic Stress Test: For each remaining empirical assumption, attempt to construct a viable scenario where its opposite holds true without violating foundational physical laws.
5. Indissoluble Base: Synthesize the remaining verified, uncompromised axioms. Stop only when reaching bedrock propositions that cannot be broken down any further.
```

##### Template 6: Negative Axiom (Impossibility Boundary) Mapping
* **Mechanism:** Axiomatic Grounding (AG)
* **Objective:** Define the solution space strictly by what is physically and logically impossible, eliminating false constraints inside that boundary.

```markdown
To discover novel solutions for [TARGET GOAL], we must define the problem via its negative space (what is definitively impossible).

Execution Steps:
1. Hard Impossibilities: List the absolute physical, mathematical, and logical boundaries that cannot be violated under any circumstances (e.g., speed of light, conservation laws, computational complexity bounds).
2. Soft Impossibilities (False Invariants): List all constraints currently treated as immutable by domain practitioners that are actually social, economic, regulatory, or tooling-based conventions.
3. The True Solution Manifold: Define the boundary space between Hard Impossibilities and Soft Impossibilities. 
4. Unexplored Topologies: Identify three radical approaches to [TARGET GOAL] that operate directly along the edge of Hard Impossibilities while completely disregarding the Soft Impossibilities.
```

##### Template 7: Dependency Graph Grounding
* **Mechanism:** Axiomatic Grounding (AG)
* **Objective:** Unpack a modern tech stack or operational process to map where assumptions lose direct contact with ground truths.

```markdown
Construct a directed acyclic graph (DAG) of the dependencies underlying: [SYSTEM / ARCHITECTURE / PROCESS].

Protocol:
1. Node Breakdown: Trace the system from its top-level user-facing interface down to bedrock substrate (hardware, physics, mathematical proofs).
2. Edge Validation: For every edge connecting Node A to Node B, assign an Epistemic Grounding Score from 1 to 5:
   - 5: Grounded in mathematical proof or immutable physical law.
   - 4: Grounded in rigorous, peer-reviewed, reproducible empirical data.
   - 3: Grounded in current market/economic conditions (time-variable).
   - 2: Grounded in industrial consensus or best practice.
   - 1: Grounded in historical artifact or inherited tooling constraints.
3. Vulnerability Isolation: Highlight the exact nodes where the system relies on Level 1 or 2 dependencies. 
4. Ground-Up Bypass: Propose a direct connection from the top-level interface to the nearest Level 4 or 5 node, eliminating intermediate fragile nodes.
```

##### Template 8: Empirical Invariant Isolation
* **Mechanism:** Axiomatic Grounding (AG)
* **Objective:** Isolate non-negotiable core invariants of a problem space from historical assumptions.

```markdown
Analyze the historical evolution of [INDUSTRY / ARCHITECTURE] over the past [TIMEFRAME, e.g., 20 years].

1. Variable vs. Invariant Decomposition:
   - Identify which variables have changed by $>10\times$ (e.g., compute cost, network bandwidth, storage density, manufacturing tolerances).
   - Identify which constraints have remained strictly invariant (e.g., human cognitive bandwidth, fundamental constants, cryptographic limits).
2. Legacy Coupling Detection: Reveal where the current design of [CURRENT SYSTEM] is still optimized for variables that were constrained 10-20 years ago but are now abundant.
3. Zero-Base Calibration: Reconstruct the system architecture under the assumption that historical constrained variables are now free/infinite, retaining only the true invariants.
```

---

#### Category 3: Constraint Decoupling & Boundary Testing

##### Template 9: Cost-Per-Unit Physical Limit Decomposition
* **Mechanism:** Constraint Decoupling (CD)
* **Objective:** Deconstruct the cost of a manufactured or compute artifact down to raw elemental and energy values.

```markdown
Perform a raw material and energetic cost deconstruction for: [PRODUCT / ARTIFACT / SERVICE].

1. Bill of Materials Reduction: Break the artifact down into its raw elemental or raw computational constituents (e.g., kg of carbon fiber, silicon, copper, joules of electricity, FLOPs) without any manufactured markups.
2. Commodity Spot Pricing: Calculate the aggregate market spot price of those raw, unformed constituents:
   $$\text{Theoretical Raw Cost} = \sum (\text{Mass}_i \times \text{Spot Price}_i) + \sum (\text{Energy}_j \times \text{Cost per Joule}_j)$$
3. Value-Added Layer Analysis: Compare the current market price of the completed product against the Theoretical Raw Cost. Categorize the delta:
   - Processing/conversion energy costs
   - Tooling amortizations and capital expenditures
   - Organizational, distribution, and informational transaction friction
   - Margin captured by rent-seeking or lack of competition
4. First-Principles Redesign: How can the conversion of raw constituents to the final required functional state be achieved with the absolute minimum number of intermediate thermodynamic steps?
```

##### Template 10: Path-Dependency Decoupling (Clean-Slate 2026)
* **Mechanism:** Constraint Decoupling (CD)
* **Objective:** Identify and eliminate design elements that exist only because of historical sequencing.

```markdown
Context: [SYSTEM / INSTITUTION / CODEBASE] was built sequentially through historical iterations, creating path-dependent architecture.

Task: Decouple the functional requirement from its historical path-dependency.
1. Historical Excavation: What was the original bottleneck or constraint that led to the adoption of the current structural paradigm for [SYSTEM]?
2. Obsolescence Check: Does that specific bottleneck still exist today? If not, precisely when did it cease to exist, and why did the system retain the design?
3. Clean-Slate Architecture: If you were tasked with solving the core problem today, possessing all modern capabilities (compute, materials, tooling) but zero lines of legacy assets or patterns, what does the direct architecture look like?
4. Transition Delta: Map the delta between the legacy architecture and the clean-slate architecture. What is the minimal viable path to bypass the legacy baggage?
```

##### Template 11: Artificial vs. Real Boundary Audit
* **Mechanism:** Constraint Decoupling (CD)
* **Objective:** Differentiate regulatory, psychological, and institutional constraints from physical ones to find arbitrage opportunities.

```markdown
Analyze the regulatory and operational bottleneck in: [CONSTRAINED INITIATIVE].

Execute an Artificial vs. Real Constraint Audit:
1. Taxonomy of Constraints: Catalog every operational friction point preventing [DESIRED OUTCOME].
2. Hard Invariants vs. Soft Frictions:
   - Physical Invariant: Breaking it violates physical reality (e.g., gravity, thermodynamics).
   - Regulatory/Legal Rule: Breaking it incurs legal penalties (enforced by humans).
   - Social/Corporate Norm: Breaking it violates convention or creates discomfort (enforced by peer pressure).
3. The Invariant-Compliant Bypass:
   - Assuming physical invariants are non-negotiable, how can the underlying *intent* of the regulatory or social rule be satisfied through a completely different technical substrate that does not trigger the legacy restriction?
   - Formulate a structural workaround that operates entirely within the boundaries of physical reality while rendering the conventional friction irrelevant.
```

##### Template 12: Zero-Overhead Ideal Final State (IFS)
* **Mechanism:** Constraint Decoupling (CD)
* **Objective:** Use TRIZ-derived Ideal Final State modeling to deconstruct a system to its functional action, completely eliminating the delivery machine.

```markdown
Apply the Ideal Final State (IFS) deconstructive principle to: [SYSTEM / MACHINE / ENTERPRISE FUNCTION].

1. Identify the Ultimate Functional Action: What is the single, precise state change that the end-user/system actually desires? (e.g., "The hole exists," not "The drill spins"; "The state is verified," not "The database consensus completes").
2. The Zero-Machine Thought Experiment:
   - Define the IFS: The function is performed with zero cost, zero mass, zero operational time, and zero dedicated hardware/software because the system utilizes existing ambient resources or self-executes.
3. Component Deletion Audit: List every component, module, or human role in the current architecture. For each, answer:
   - "Why can this component not be deleted while its function is performed by an existing primitive elsewhere in the environment?"
4. Radical Pruning: Synthesize a design that achieves at least 80% of the IFS by deleting at least 50% of the current operational components.
```

---

#### Category 4: Teleological Re-Anchoring & Functional Inversion

##### Template 13: Functional Utility Inversion
* **Mechanism:** Teleological Re-Anchoring (TR)
* **Objective:** Anchor on the core utility to re-synthesize alternative solutions that share zero lineage with the incumbent approach.

```markdown
Deconstruct [PRODUCT / SERVICE / PARADIGM] down to its core teleological utility.

1. Terminal Utility Isolation: Define the precise utility delivered to the recipient at the exact moment of consumption. Strip away all packaging, transport, interfaces, and business models. Express this utility as an outcome metric (e.g., "Nutrients delivered to bloodstream," "Certainty of asset transfer registered").
2. Vehicle Decoupling: List the historical vehicles used to deliver this utility across three distinct historical epochs. Demonstrate how each epoch conflated the vehicle with the core utility.
3. Radical Vehicle Synthesis: Invent three completely distinct mechanisms to deliver the exact same Terminal Utility using current technological frontiers (e.g., generative AI, synthetic biology, decentralized networks, quantum mechanics), ensuring none of the three designs share components with the current incumbent vehicle.
```

##### Template 14: Axiomatic Clean-Sheet Re-Synthesis
* **Mechanism:** Teleological Re-Anchoring (TR)
* **Objective:** Rebuild an entire technology stack or business process bottom-up using only verified base primitives.

```markdown
Perform an Axiomatic Clean-Sheet Re-Synthesis for: [PROBLEM STATEMENT].

Phase 1: Bedrock Primitives (Deconstruction)
- Extract the 3 to 5 non-negotiable physical, mathematical, or logistical facts that govern this problem space.
- Discard all current best practices, commercial architectures, and existing frameworks.

Phase 2: Upward Deduction (Re-Synthesis)
- Step 1: Combine Primitive 1 and Primitive 2. What is the absolute simplest mechanism that links them?
- Step 2: Add Primitive 3. What is the most direct architecture that accommodates this without introducing secondary dependencies?
- Continue until a coherent operational model is built.

Phase 3: Stress Testing Against the Incumbent
- Compare this clean-sheet design against the current market-standard solution.
- Where does the clean-sheet design achieve an order-of-magnitude reduction in complexity, cost, or latency?
- What edge-case or historical concern does the market-standard solution address that the clean-sheet design does not? Is that edge case still relevant today?
```

##### Template 15: Cross-Substrate Functional Migration
* **Mechanism:** Teleological Re-Anchoring (TR)
* **Objective:** Take the fundamental mechanism of a solution and migrate it to an entirely different physical or digital substrate.

```markdown
Analyze the operational architecture of [SOLUTION / SYSTEM].

1. Substrate-Independent Mechanism: Describe the core functional mechanism of this system using purely abstract, mathematical, or algorithmic terms, completely decoupled from its current physical or software medium (e.g., balance sheet reconciliation decoupled from ledgers; mechanical dampening decoupled from springs and fluids).
2. Substrate Analysis: What are the primary limits of the current substrate (e.g., biological constraints, silicon latency, mechanical wear, human cognitive load)?
3. Substrate Re-Mapping: Map the core mechanism onto three radically different substrates:
   - A biological/cellular substrate
   - A distributed cryptographic/algorithmic substrate
   - An optical, acoustic, or novel material substrate
4. Mechanics Translation: For each new substrate, how does the fundamental mechanism manifest, and what orders of magnitude of efficiency or capability are unlocked?
```

##### Template 16: Minimum Viable Topology (MVT)
* **Mechanism:** Teleological Re-Anchoring (TR)
* **Objective:** Reduce a system's organizational or software architecture down to the minimal mathematical topology required to prevent failure.

```markdown
Deconstruct the topology of [SOFTWARE ARCHITECTURE / ORGANIZATIONAL STRUCTURE].

1. Graph Formulation: Model the system as an informational network of nodes (processing units or humans) and edges (communication channels or APIs).
2. Failure Mode Invariants: What are the absolute minimum conditions under which this topology fails to deliver its core objective?
3. Topological Redundancy Audit:
   - Identify edges that exist solely to overcome the architectural deficiencies of neighboring nodes.
   - Identify nodes that act solely as relays or translators without transforming the underlying signal.
4. Contraction to Minimal Viable Topology:
   - Apply graph contraction operations to merge redundant nodes.
   - Remove all communication pathways that do not directly alter the state of the terminal sink node.
   - Output the mathematically minimal network topology required to maintain functional stability.
```

---

#### Category 5: Adversarial Boundary Stress & Counterfactual Verification

##### Template 17: Asymptotic Limit Stress-Testing ($\lim \to 0$, $\lim \to \infty$)
* **Mechanism:** Adversarial Limit Testing (ALT)
* **Objective:** Drive key parameters of a system to extremes to shatter assumptions and expose the foundational causal levers.

```markdown
Subject [BUSINESS MODEL / TECHNICAL ARCHITECTURE / SYSTEM] to asymptotic limit deconstruction.

Apply the following extreme parametric shifts:
1. $\lim_{\text{Cost of Core Resource} \to 0}$: If the primary cost driver of this system drops to absolute zero overnight, what 90% of the current architecture immediately becomes dead weight?
2. $\lim_{\text{Scale} \to 1000\times}$: If throughput requirements scale by three orders of magnitude instantly, which foundational assumption breaks first? Why is that assumption an artifact of current scale rather than a fundamental truth?
3. $\lim_{\text{Latency Tolerance} \to 0}$: If allowable execution time is reduced to the theoretical minimum allowed by the speed of light, what layers of abstraction must be completely bypassed or fused?
4. Core Invariant Isolation: Based on the asymptotic tests above, what is the single component of the system that remains invariant across all three extremes? This is your actual core value driver.
```

##### Template 18: Dialectical Invariant Probing
* **Mechanism:** Adversarial Limit Testing (ALT)
* **Objective:** Pitting two diametrically opposed architectural paradigms against each other to extract the shared underlying first principle.

```markdown
Execute a dialectical first-principles deconstruction between two competing paradigms:
- Paradigm A: [ESTABLISHED CONVENTIONAL APPROACH]
- Paradigm B: [RADICAL ALTERNATIVE APPROACH]

1. Thesis & Antithesis:
   - Deconstruct Paradigm A to its root assumptions.
   - Deconstruct Paradigm B to its root assumptions.
2. Contradiction Analysis: Identify the fundamental point of irreconcilable contradiction between the two paradigms. What underlying axiom are they interpreting differently?
3. The Substrate Synthesis:
   - Which of these competing axioms is verified by empirical reality, and which is an artifact of local optimization?
   - Construct a unified architectural model (Synthesis) that incorporates the verified physical/logical truths of both paradigms while discarding the dogmatic baggage of each.
```

##### Template 19: Chaos-Driven Primitive Isolation
* **Mechanism:** Adversarial Limit Testing (ALT)
* **Objective:** Strip away layers of an operating system or organization via systematic simulated destruction to find the indissoluble operational core.

```markdown
Apply a simulated subtractive stress test to [OPERATIONAL OR TECHNICAL SYSTEM].

Execution Protocol:
1. Subtractive Iteration 1: Randomly remove 30% of the peripheral components, tools, or dependencies. Does the primary objective function continue to execute, even at degraded capacity? If yes, classify those components as non-primitives.
2. Subtractive Iteration 2: Progressively strip away infrastructure layers (e.g., middle management, frameworks, specialized tooling, proprietary protocols) one by one. Document the exact point at which the primary objective function suffers catastrophic failure.
3. The Indissoluble Core: Identify the absolute minimum subset of components that, if preserved, allows the core objective function to survive.
4. Ground-Up Rebuild: Using *only* this indissoluble core, rebuild the operational perimeter with modern, low-friction primitives, preventing the re-introduction of the discarded components.
```

##### Template 20: Meta-Prompting Evaluator for Deconstructive Rigor
* **Mechanism:** Axiomatic Grounding (AG) & Adversarial Limit Testing (ALT)
* **Objective:** A meta-evaluation prompt to score and self-correct any reasoning output for analogical contamination, circular logic, and epistemic drift.

```markdown
You are an adversarial epistemic auditor. Your mission is to evaluate the following analysis: [INSERT PRIOR OUTPUT / REASONING CHAIN] for adherence to pure First-Principles Deconstruction.

Audit Rubric (Score each from 0.0 to 1.0):
1. Absence of Analogy: Does the output rely on comparisons to existing products/methods, or does it reason bottom-up from primitives? (1.0 = zero analogy).
2. Physical/Mathematical Grounding: Are claims verified against thermodynamic, informational, or mathematical realities, or merely industry consensus?
3. Constraint Differentiation: Does the analysis clearly separate immutable laws of nature from mutable historical, institutional, or economic constraints?
4. Parsimony & Elegance: Has the system been reduced to its minimal viable topology, or are unnecessary legacy intermediate steps retained?

Audit Execution:
- Identify and quote every instance of "reasoning by analogy" or ungrounded assertion in the text.
- Re-write each flagged section by explicitly deriving the conclusion upward from verifiable bedrock primitives.
- Assign a final Deconstructive Rigor Index (DRI) score. If DRI < 0.90, execute an automated recursive rewrite of the entire analysis until it meets the standard.
```

---

### Operational Framework: Execution Heuristics for Self-Paced Mastery

To build cognitive and prompt-engineering mastery over First-Principles Deconstruction architectures, use the following operational heuristics during execution.

```
       DECONSTRUCTIVE MASTERY LOOP
┌───────────────────────────────────────┐
│ 1. Ingest Problem / Incumbent Model   │
└──────────────────┬────────────────────┘
                   ▼
┌───────────────────────────────────────┐
│ 2. The Analogy Audit                  │
│    (Purge metaphors, history, jargon) │
└──────────────────┬────────────────────┘
                   ▼
┌───────────────────────────────────────┐
│ 3. Thermodynamic / Mathematical Bound │
│    (Calculate absolute minimum limit) │
└──────────────────┬────────────────────┘
                   ▼
┌───────────────────────────────────────┐
│ 4. Recursive Stop-Condition Check     │
│    (Can primitive be broken down?)    │
└──────────┬─────────────────┬──────────┘
      NO   │                 │ YES
           ▼                 ▼
  ┌────────────────┐   ┌────────────────┐
  │ 5. Upward      │   │ Recurse deeper │
  │    Synthesis   │   │ into primitives│
  └────────┬───────┘   └────────────────┘
           ▼
┌───────────────────────────────────────┐
│ 6. Dual-Run A/B Stress Test           │
│    (Score DRI vs baseline)            │
└───────────────────────────────────────┘
```

#### 1. The "Analogy Audit" (Eliminating Transitive Reasoning Errors)
* **The Failure Mode:** Models default to consensus answers because token prediction inherently optimizes for the most statistically common completion. Most human text reasons by analogy ("X is like Y, so we should do Z").
* **Mastery Heuristic:** Before asking a model to solve a problem, execute an explicit pre-processing step that prohibits domain-specific nouns. Force the model to state the problem purely using:
  - System components: mass, energy, time, information, state variables.
  - Operations: add, delete, transform, route, verify.
* If an output contains phrases like "industry standard," "best practice," "typically," or "similar to," flag it as a reasoning failure and trigger an immediate semantic purge.

#### 2. Thermodynamic & Computational Bounding
* **The Failure Mode:** Accepting cost, latency, or operational complexity as "fixed parameters."
* **Mastery Heuristic:** Always establish the *hard physics/math floor* prior to architectural brainstorming. 
  - If optimizing a database, calculate the theoretical minimum network packets and Landauer compute dissipation for the transaction.
  - If optimizing a supply chain, calculate the stoichiometric mass balance and theoretical transport energy.
* Anchor the prompt explicitly to the gap between the physics floor and current reality:
  $$\Delta = \frac{\text{Current Implementation Metric}}{\text{Theoretical Bound}}$$
  Direct the model's entire attention budget toward dismantling the components of $\Delta$.

#### 3. Recursive Decomposition Stop-Conditions
* **The Failure Mode:** Halting the deconstruction too early (leaving legacy assumptions intact) or descending into infinite philosophical regress (e.g., reducing a software design to subatomic particle physics).
* **Mastery Heuristic:** Apply the **Functional Indissolubility Criterion**:
  - Stop deconstruction when a component cannot be decomposed further without losing the specific properties needed to drive the terminal objective function.
  - *Example:* In evaluating a software consensus protocol, decomposing down to network latency and state serialization is functional; decomposing down to the quantum mechanical properties of copper wiring in the switch provides zero leverage for the consensus layer.
  - Use Template 20 to verify that the terminal primitive is an invariant at the layer of intervention.

#### 4. Dual-Run Contrast Testing (Analogical vs. First-Principles)
To calibrate your own diagnostic ability as a prompt engineer, run deliberate contrast evaluations:
* **Run A (Conventional Baseline):** Prompt a frontier model with standard domain framing: *"How do we optimize [SYSTEM] according to modern industry best practices?"*
* **Run B (Axiomatic Deconstruction):** Execute a multi-stage pipeline using Template 1 (Analogy Stripper), followed by Template 6 (Impossibility Boundary), culminating in Template 14 (Axiomatic Clean-Sheet Re-Synthesis).
* **Differential Analysis:** Map the two outputs side-by-side:
  - Identify components present in Run A that are completely absent in Run B. These represent dead-weight industry path-dependencies.
  - Identify solutions generated in Run B that cannot be derived from the premises of Run A. This delta represents your **First-Principles Alpha**.

#### 5. Output Verification Rubric
Grade every deconstructive prompt output against this zero-fluff validation checklist:

| Dimension | Failure Indicator (0.0) | Target Criterion (1.0) |
| :--- | :--- | :--- |
| **Epistemic Base** | Relies on authority ("Gartner says", "Industry leaders do") | Relies strictly on physical, mathematical, or empirical primitives |
| **Substrate Dependency** | Assumes the current software/hardware form factor is mandatory | Separates functional mechanics from the physical delivery medium |
| **Path-Dependency** | Retains steps whose only function is addressing historic bottlenecks | Discards all historical adaptations; optimizes purely for current constraints |
| **Simplicity Vector** | Increases system complexity by adding monitoring/mitigation layers | Reduces system complexity by deleting fragile or non-entropy-reducing nodes |
