# Deterministic DAG Offloading & Symbolic Solvers: System Architecture & Prompt Catalog

---

## 1. Architectural Taxonomy

Frontier reasoning systems encounter systematic failure modes when forced to perform exact combinatorial search, multi-step invariant tracking, or non-trivial arithmetic directly within autoregressive token space. 

**Deterministic DAG Offloading & Symbolic Solvers** resolve this bottleneck by decoupling the problem into:
1. **Semantic Disambiguation & Dependency Graphing:** The LLM parses natural language inputs, identifies entities, maps causal/temporal dependencies, and compiles the problem into an explicit Directed Acyclic Graph (DAG) or Formal Intermediate Representation (FIR).
2. **Deterministic Execution Offload:** Computationally brittle subgraphs—such as topological sorting, constraint satisfaction, linear programming, theorem proving, and numerical operations—are offloaded to deterministic symbolic runtimes (e.g., Z3/SMT solvers, SymPy, Datalog engines, code interpreters).
3. **Synthesis & Invariant Verification:** The solver returns exact states, counterexamples, or unsat cores. The LLM then ingests these deterministic proofs to synthesize the final domain solution and verify post-conditions.

```
+-----------------------------------------------------------------------------+
|                          NATURAL LANGUAGE INPUT                             |
+-----------------------------------------------------------------------------+
                                       |
                                       v
+-----------------------------------------------------------------------------+
|                     PHASE 1: SEMANTIC TRANSLATION (LLM)                     |
|  * Entity Extraction    * Invariant Specification   * Formal Grammar (AST)  |
+-----------------------------------------------------------------------------+
                                       |
                   +-------------------+-------------------+
                   |                                       |
                   v                                       v
+------------------------------------+  +-------------------------------------+
| CATEGORY I & V: DAG COMPILATION    |  | CATEGORY II & III: SYMBOLIC SOLVER  |
| * Causal/Temporal Edges            |  | * SMT-LIB2 / First-Order Logic      |
| * Topological Dependency Sort      |  | * Algebraic Invariants (SymPy/Z3)   |
| * Parallel Hypothesis Branching    |  | * Convex Optimization / Duals       |
+------------------------------------+  +-------------------------------------+
                   |                                       |
                   +-------------------+-------------------+
                                       |
                                       v
+-----------------------------------------------------------------------------+
|                   PHASE 2: DETERMINISTIC EXECUTION RUNTIME                  |
|  * Z3/SAT / SMT Prover  * Graph Engine  * Python REPL  * AST Verifier       |
|    Output: {Satisfiable: Model} | {Unsat: Minimal Core} | {State Vector}    |
+-----------------------------------------------------------------------------+
                                       |
                                       v
+-----------------------------------------------------------------------------+
|                   PHASE 3: RESIDUAL SYNTHESIS & METRIC AUDIT                |
|  * Reconstruct Domain Strategy      * Counterexample Invalidation           |
|  * Zero-Hallucination Proof Check   * Metric Verification                   |
+-----------------------------------------------------------------------------+
```

### Taxonomy of Causal Mechanisms

```
Deterministic Thinking Architectures
├── I. Topological Dependency Graphing (TDG)
│   └── Converts implicit narrative reasoning into strict topological state sequences.
├── II. SMT & Formal Constraint Satisfaction (SMT-CSP)
│   └── Translates multi-variable boundary problems into First-Order Logic / SMT-LIB2 models.
├── III. Algebraic & Invariant State Checking (AISC)
│   └── Isolates continuous/algebraic mechanics to symbolic engines for zero-drift proofs.
├── IV. Sandboxed Program Synthesis & Verification (SPSV)
│   └── Compiles domain logic into executable ASTs with unit assertions and property tests.
└── V. Bifurcated DAG Search & Tournament Pruning (BDST)
    └── Generates parallel hypothesis trees resolved via deterministic elimination rubrics.
```

---

## 2. Production-Grade Prompt Templates

### Category I: Topological Dependency Graphing (TDG)

#### Prompt 1: Topological Sort & Critical Path Dependency Deconfliction
* **Mechanism:** Topological Dependency Graphing
* **Target Objective:** Disentangle circular, concurrent, and sequential dependencies in distributed system failures without autoregressive drift.

```markdown
[SYSTEM ARCHITECTURE: TOPOLOGICAL DEPENDENCY DECONFLICTER]

TARGET PHENOMENON:
{{DISTRIBUTED_FAILURE_SCENARIO}}

EXECUTION DIRECTIVE:
Do not diagnose the root cause intuitively. Execute the following deterministic pipeline:

1. ENTITY & EVENT EXTRACTION:
   - Extract every discrete state change, network event, and service failure as an indexed node: N = {n_1, n_2, ..., n_k}.
   - Format: `n_i: [Timestamp / Sequence Window] [Subsystem] [Observed State Change]`

2. DIRECTED ACYCLIC GRAPH COMPILATION:
   - For every pair (n_a, n_b), establish an edge `n_a -> n_b` ONLY if:
     a) Temporal precedence holds: t(n_a) < t(n_b).
     b) Causal dependency is strictly necessary: ¬n_a => ¬n_b under baseline conditions.
   - Output an explicit adjacency list:
     `n_i -> [n_j, n_m]`

3. TOPOLOGICAL SORT & CYCLE RESOLUTION:
   - Perform an explicit Kahn's algorithm trace or depth-first topological sort.
   - If a cycle is detected (e.g., cascading retry storm), isolate the feedback loop, break the edge at the non-deterministic interface, and flag the cyclic sub-graph.
   - Output the exact linear execution order: `L = [n_ordered_1, ..., n_ordered_k]`.

4. CRITICAL PATH COMPUTATION:
   - Assign deterministic weights (latency or impact delta) to each edge.
   - Compute the Critical Path: Identify the single unbranched chain of dependency responsible for the terminal failure state.

5. FINAL AUDIT & EDUCATION CHECK:
   - Explain why an unconstrained LLM would hallucinate the root cause by pointing out the confounding edge rejected in Step 2.
```

#### Prompt 2: Causal DAG Extraction & Pearlian Counterfactual Boundary Engine
* **Mechanism:** Judea Pearl Do-Calculus Offloading
* **Target Objective:** Formalize causal inference from complex observational case studies, isolating confounders deterministically.

```markdown
[SYSTEM ARCHITECTURE: PEARLIAN CAUSAL DAG ENGINE]

INPUT SYSTEM SPECIFICATION:
{{OBSERVATIONAL_DATA_OR_CASE_STUDY}}

TASK:
Construct an explicit structural causal model (SCM) and evaluate a counterfactual intervention.

PROTOCOL:
1. VARIABLE CLASSIFICATION:
   - Endogenous Variables (V): Observable states internal to the system.
   - Exogenous Variables (U): Unobserved background noise/environment variables.
   - Interventions (X): Target variable to manipulate.
   - Outcome (Y): Dependent target variable.

2. DAG EDGES & COLLIDER IDENTIFICATION:
   - Define all directed causal relationships: `V_i -> V_j`.
   - Identify all fork structures (`A <- B -> C`), chain structures (`A -> B -> C`), and colliders (`A -> B <- C`).
   - Flag any d-separation conditions between X and Y given conditioning set Z.

3. SCM EQUATIONS (SYMBOLIC DRAFT):
   - Express each V_i as a deterministic function: `v_i = f_i(PA_i, u_i)` where PA_i are parent nodes.

4. GRAPH INTERVENTION OPERATOR (do(X = x)):
   - Sever all incoming edges into node X (mutilated graph G_{\bar{X}}).
   - Trace the downstream topological propagation of setting X to fixed constant x*.
   - Output the deterministic state shift across the remaining subgraph.

5. VERIFICATION:
   - Prove whether the observational correlation `P(Y|X)` diverges from the interventional distribution `P(Y|do(X))`. Detail the exact backdoor path that caused the divergence.
```

#### Prompt 3: State-Transition Graph & Invariant Matrix Compiler
* **Mechanism:** Finite State Machine (FSM) Formal Matrix Offloading
* **Target Objective:** Learn to convert ambiguous business logic into a mathematically validated transition matrix to prevent deadlocks.

```markdown
[SYSTEM ARCHITECTURE: DETERMINISTIC FSM COMPILER]

DOMAIN LOGIC CONSTRAINTS:
{{DOMAIN_BUSINESS_RULES}}

EXECUTION PROTOCOL:
1. STATE SPACE ENUMERATION:
   - S = {s_0, s_1, ..., s_n} where s_0 is Initial State, and F ⊆ S is the set of Terminal States.
   - Σ = {e_0, e_1, ..., e_m} representing discrete valid events/inputs.

2. TRANSITION MATRIX COMPILATION:
   - Construct a strict 2D transition table: Rows = Current State (S), Columns = Event (Σ), Cells = Next State (S').
   - Any unspecified transition MUST be labeled explicitly as `Ø (STRICT_REJECT)`.

3. DETERMINISTIC GRAPH AUDIT:
   - Deadlock Detection: Determine if ∃ s_i ∉ F such that ∀ e ∈ Σ, T(s_i, e) = Ø.
   - Reachability Analysis: Run breadth-first search from s_0. Return any state s_k for which no valid path exists.
   - Livelock Analysis: Identify closed loops in the state graph that do not include a path to F.

4. RUNTIME TRACE VERIFICATION:
   - Provide three dynamic sequence test vectors:
     a) Valid nominal path to terminal state.
     b) Edge-case malicious sequence attempting an undefined transition (`Ø`).
     c) Deadlock-inducing race condition, showing the exact matrix cell that blocks execution.

5. OUTPUT:
   - Render the complete Transition Matrix.
   - List mathematical proofs of Liveness and Safety invariants.
```

#### Prompt 4: Protocol Sequence Engine & Linear Temporal Logic (LTL) Translator
* **Mechanism:** Topological Temporal Assertion Compilation
* **Target Objective:** Formulate system interaction sequences and assert safety/liveness properties using deterministic temporal tracing.

```markdown
[SYSTEM ARCHITECTURE: TEMPORAL TRACE VERIFIER]

PROTOCOL INTERACTION CORPUS:
{{MULTI_AGENT_OR_SERVICE_INTERACTION}}

DIRECTIVES:
1. SEQUENCE TRACE EXTRACTION:
   - Parse the narrative into a discrete event timeline: `t = 0, 1, 2, ...`
   - Map states as atomic propositions: `p, q, r...`

2. LTL TRANSLATION:
   Translate domain requirements into formal Linear Temporal Logic syntax using operators:
   - G (Globally / Always)
   - F (Finally / Eventually)
   - X (Next state)
   - U (Until)
   Examples: `G(Request -> F Response)`, `G(LockAcquired -> X ¬LockAcquiredByOther)`

3. STEP-BY-STEP TRACE CHECK:
   - Evaluate the extracted timeline against each synthesized LTL formula.
   - Construct a state truth table for intervals `t_0` through `t_final`.
   - Identify the exact index `t_violation` where any property evaluates to FALSE.

4. COMPILATION OF COUNTER-TRACE:
   - If an invariant fails, isolate the minimal sub-sequence of events causing the fault.
   - Output the counter-example trace in standardized sequence diagram notation.
```

---

### Category II: SMT & Formal Constraint Satisfaction (SMT-CSP)

#### Prompt 5: Z3 SMT-LIB2 Bridge for Policy Enforcement
* **Mechanism:** First-Order Logic to SMT-LIB2 Offload
* **Target Objective:** Eliminate semantic ambiguity in complex authorization/governance policies by compiling them to provable SMT scripts.

```markdown
[SYSTEM ARCHITECTURE: FORMAL POLICY TO SMT-LIB2 COMPILER]

INPUT POLICY SPECIFICATION:
{{SECURITY_OR_GOVERNANCE_POLICIES}}

QUERY INTENT:
{{ARBITRARY_ACCESS_SCENARIO_OR_EDGE_CASE}}

EXECUTION FRAMEWORK:
1. DECLARATION OF SORTS AND CONSTANTS:
   - Translate all principal identities, resources, and actions into uninterpreted SMT sorts or bit-vectors.
   - Emit SMT-LIB2 syntax for sorts: `(declare-sort Subject)`, `(declare-sort Resource)`, `(declare-sort Action)`.

2. FORMAL AXIOM ENCODING:
   - Translate human-language policy rules into first-order logical implications:
     `∀ s ∈ Subject, r ∈ Resource, a ∈ Action: Condition(s, r, a) => Permit(s, r, a)`.
   - Output raw SMT-LIB2 assertions: `(assert (forall ((s Subject) ...) ...))`.

3. UNSAT CORE & SATISFIABILITY FORMULATION:
   - Formulate the negative hypothesis to check policy escape: Is it possible for an unauthorized actor to access Resource X?
   - Formulate the `(check-sat)` and `(get-model)` or `(get-unsat-core)` execution harness.

4. SIMULATED DETERMINISTIC RUN:
   - Execute the symbolic evaluation directly.
   - Provide the model assignment if SAT (exploit vector discovered).
   - Provide the minimal unsat core if UNSAT (formal mathematical proof of policy closure).

5. COGNITIVE CALIBRATION:
   - Highlight the precise clause where natural language intuition diverges from symbolic SMT execution.
```

#### Prompt 6: Horn-Clause Datalog Deduction Engine
* **Mechanism:** Datalog Rule Compilation & Deductive Closure
* **Target Objective:** Query complex, highly interconnected relational domain facts without recursive hallucination.

```markdown
[SYSTEM ARCHITECTURE: DATALOG DEDUCTIVE CLOSURE ENGINE]

INPUT KNOWLEDGE BASE (NATURAL LANGUAGE):
{{DOMAIN_ASSERTIONS_AND_RELATIONS}}

QUERY GOAL:
{{TARGET_RECURSIVE_DEDUCTION}}

PROTOCOL:
1. FACT EXTRACTION (EXTENSIONAL DATABASE - EDB):
   - Convert all ground facts into clean Datalog relational tuples:
     `parent(john, mary).`, `role(mary, admin).`, `boundary(zone_a, secure).`

2. RULE SYNTHESIS (INTENSIONAL DATABASE - IDB):
   - Define recursive and non-recursive Horn clauses preserving strict stratification (no negation through recursion):
     `reachable(X, Y) :- edge(X, Y).`
     `reachable(X, Y) :- edge(X, Z), reachable(Z, Y).`
   - Map all domain inference logic into these pure Horn clauses.

3. FIXPOINT CALCULATION (BOTTOM-UP EVALUATION):
   - Initialize step `R_0` with ground facts.
   - Compute `R_{k+1} = T_P(R_k) \cup R_k` iteratively until `R_{k+1} == R_k` (Fixed-point attained).
   - Display each iteration step's newly materialized tuples explicitly.

4. QUERY RESOLUTION:
   - Evaluate the user's `QUERY GOAL` against the materialized minimal fixpoint.
   - Provide an exact mathematical derivation tree (proof tree) for the returned true/false response.
```

#### Prompt 7: Combinatorial CSP Reduction & Arc Consistency (AC-3) Engine
* **Mechanism:** Constraint Satisfaction Problem Formulation & AC-3 Propagation
* **Target Objective:** Master deterministic pruning of combinatorial configuration problems before heuristic search.

```markdown
[SYSTEM ARCHITECTURE: CSP FORMALIZER & AC-3 SOLVER]

PROBLEM CONSTRAINTS:
{{RESOURCE_ALLOCATION_OR_SCHEDULING_PROBLEM}}

PIPELINE:
1. CSP TRIPLET FORMULATION:
   - Variables: `X = {X_1, X_2, ..., X_n}`
   - Domains: Explicit finite sets `D_i = {v_1, ..., v_m}` for each variable.
   - Constraints: Explicit binary relations `C_{ij} \subseteq D_i \times D_j`.

2. CONSTRAINT GRAPH ENUMERATION:
   - Output the constraint graph where vertices are variables and undirected edges represent constraints.
   - List the complete arc queue for propagation: `Q = {(X_i, X_j) | C_{ij} exists}`.

3. AC-3 ALGORITHM RUNTIME EXECUTION:
   - Step through the AC-3 algorithm trace:
     * Pop `(X_i, X_j)` from `Q`.
     * Execute `Revise(X_i, X_j)`: Remove any value `x ∈ D_i` with no supporting value `y ∈ D_j` satisfying `C_{ij}`.
     * If `D_i` changes, append all incoming arcs `(X_k, X_i)` back to `Q`.
   - Explicitly list each pruned domain value per step.

4. FINAL DOMAIN STATE:
   - Output the reduced domains `D'_i`.
   - If any `D'_i = ∅`, terminate with proof of unsolvability.
   - If domains are singular, output the deterministic global solution.
   - If domains > 1, formulate the remaining search space for deterministic backtracking.
```

#### Prompt 8: Exact 3-SAT Reduction & Solvability Verifier
* **Mechanism:** Boolean Conjunctive Normal Form (CNF) Offloading
* **Target Objective:** Learn to map NP-hard decision logic to standard CNF and run deterministic resolution algorithms.

```markdown
[SYSTEM ARCHITECTURE: 3-SAT REDUCTION & RESOLUTION COMPILER]

INPUT DECISION COMPLEX:
{{COMPLEX_DECISION_CONDITIONS}}

DIRECTIVES:
1. BOOLEAN VARIABLE COMPILATION:
   - Isolate each boolean primitive: `x_1, x_2, ..., x_k`.
   - Define their exact semantic meaning in a single verification table.

2. CNF COMPILATION (TSEITIN TRANSFORMATION):
   - Translate all multi-clause conditional rules into Conjunctive Normal Form (CNF):
     `Φ = ⋀ (l_{i,1} ∨ l_{i,2} ∨ l_{i,3})`
   - Show the step-by-step equivalence using de Morgan's laws and distributive transformations, avoiding exponential blowup via Tseitin extension variables where necessary.

3. DAVIS-PUTNAM-LOGEMANN-LOVELAND (DPLL) STEP EXECUTION:
   - Perform deterministic unit propagation: Locate all unit clauses `(l)` and propagate assignments.
   - Perform pure literal elimination: Locate variables appearing with single polarity across all active clauses.
   - Trace the branch decisions if unresolved, showing the state stack explicitly.

4. OUTPUT:
   - Provide the final satisfiability result: `SAT` (with variable truth assignments) or `UNSAT` (with resolution proof step resolving to empty clause `□`).
```

---

### Category III: Algebraic & Invariant State Checking (AISC)

#### Prompt 9: SymPy Closed-Form Symbolic Derivation & Boundary Engine
* **Mechanism:** Symbolic Algebra & Calculus Engine Simulation
* **Target Objective:** Master non-drifting derivations of complex dynamic systems by forcing execution through formal algebraic structures.

```markdown
[SYSTEM ARCHITECTURE: FORMAL SYMBOLIC MATHEMATICS HARNESS]

ANALYTICAL PROBLEM:
{{CONTINUOUS_OR_PHYSICAL_SYSTEM}}

EXECUTION PIPELINE:
1. VARIABLE & SYMBOL DECLARATION:
   - Define all independent and dependent variables, parameters, and assumptions:
     `t = Symbol('t', real=True, positive=True)`
     `k = Symbol('k', positive=True)`

2. GOVERNING DIFFERENTIAL/ALGEBRAIC EQUATION ENCODING:
   - Write out the explicit symbolic equation representation without numerical approximations:
     `Eq(f(t).diff(t, 2) + gamma * f(t).diff(t) + omega_0**2 * f(t), F_0 * cos(omega * t))`

3. CLOSED-FORM ANALYTIC RESOLUTION:
   - Execute the deterministic symbolic calculus steps:
     a) Homogeneous solution computation (characteristic equation root derivation).
     b) Particular solution computation via method of undetermined coefficients or Green's functions.
     c) Boundary/initial condition application to solve for constants `C_1, C_2`.
   - Output the exact algebraic expression for the solution function.

4. ASYMPTOTIC & BOUNDARY AUDIT:
   - Compute `lim_{t -> ∞}` of the solution.
   - Compute the Jacobian or first derivative extrema: `df/dt = 0`.
   - Validate conservation invariants (e.g., energy, mass, continuous momentum preservation).

5. ERROR PROOF:
   - Check the analytical result against the original ODE by direct substitution. Show that the residual identically equals 0.
```

#### Prompt 10: Buckingham Pi Dimensional Invariant Enforcement
* **Mechanism:** Dimensional Analysis & Matrix Null Space Verification
* **Target Objective:** Prevent dimensional inconsistency and hallucinations when formulating physical equations or complex unit relationships.

```markdown
[SYSTEM ARCHITECTURE: BUCKINGHAM PI SYMBOLIC ENGINE]

TARGET SYSTEM VARIABLES:
{{LIST_OF_PHYSICAL_VARIABLES_AND_DIMENSIONS}}

PROTOCOL:
1. FUNDAMENTAL DIMENSIONS IDENTIFICATION:
   - Use SI fundamental dimensions: `M (Mass), L (Length), T (Time), Θ (Temperature), I (Electric Current)`.
   - List the dimensional formula for each variable `q_1, ..., q_n`: `[q_i] = M^a L^b T^c ...`

2. DIMENSIONAL MATRIX FORMATION:
   - Construct matrix `A`: Rows = Fundamental dimensions, Columns = Variables.
   - Compute `Rank(A) = r` deterministically using Gaussian elimination steps.

3. NULL SPACE (KERNEL) CALCULATION:
   - Determine the number of dimensionless Pi groups: `p = n - r`.
   - Compute the basis vectors of `Null(A)`.
   - Show the intermediate reduced row echelon form (RREF) of matrix `A`.

4. SYNTHESIS OF DIMENSIONLESS GROUPS:
   - Compile the exact mathematical formulations for `Π_1, Π_2, ..., Π_p`.
   - State the universal physical law in dimensionless form: `Π_1 = Φ(Π_2, ..., Π_p)`.

5. VALIDATION:
   - Verify every derived `Π` group by showing that all exponents sum to zero across all primary dimensions:
     `[Π_k] = M^0 L^0 T^0`.
```

#### Prompt 11: Karush-Kuhn-Tucker (KKT) Convex Optimization Decomposer
* **Mechanism:** Constrained Optimization & Formal Dual Analysis
* **Target Objective:** Solve multi-variable trade-offs deterministically by offloading to formal convex optimization and complementary slackness checks.

```markdown
[SYSTEM ARCHITECTURE: CONVEX OPTIMIZATION & KKT SOLVER]

OBJECTIVE FUNCTION & CONSTRAINTS:
{{OBJECTIVE_AND_INEQUALITY_CONSTRAINTS}}

EXECUTION BLUEPRINT:
1. STANDARDIZATION:
   - Formulate as standard convex program:
     Minimize `f_0(x)`
     Subject to:
       `f_i(x) <= 0, ∀ i ∈ {1, ..., m}`
       `h_j(x) = 0, ∀ j ∈ {1, ..., p}`

2. LAGRANGIAN COMPILATION:
   - Construct the symbolic Lagrangian function:
     `L(x, λ, ν) = f_0(x) + ∑ (λ_i * f_i(x)) + ∑ (ν_j * h_j(x))`
   - Explicitly declare multiplier constraints: `λ_i >= 0`.

3. KKT SYSTEM EXTRACTION:
   - Stationarity: `∇_x L(x, λ, ν) = 0`
   - Primal Feasibility: `f_i(x) <= 0` and `h_j(x) = 0`
   - Dual Feasibility: `λ_i >= 0`
   - Complementary Slackness: `λ_i * f_i(x) = 0, ∀ i`

4. EXACT CASE ENUMERATION (COMPLEMENTARY SLACKNESS EXPLORATION):
   - Systematically branch across active vs. inactive constraints (`λ_i = 0` vs. `f_i(x) = 0`).
   - Solve each resulting linear/algebraic sub-system.
   - Reject points violating primal or dual feasibility.

5. FINAL GLOBAL OPTIMUM:
   - Output the global optimal coordinate `x*` and optimal value `p* = f_0(x*)`.
   - Provide the sensitivity analysis using dual variables `λ*`.
```

#### Prompt 12: Category-Theoretic Commutative Diagram Verifier
* **Mechanism:** Functorial Invariant Mapping & Diagram Chasing
* **Target Objective:** Master structural isomorphism and preserve domain invariants across complex system migrations or translations.

```markdown
[SYSTEM ARCHITECTURE: COMMUTATIVE DIAGRAM PROVER]

SOURCE DOMAIN (CATEGORY C):
{{SOURCE_SYSTEM_ARCHITECTURE}}

TARGET DOMAIN (CATEGORY D):
{{TARGET_SYSTEM_ARCHITECTURE}}

PROPOSED MAPPING (FUNCTOR F):
{{MIGRATION_OR_TRANSFORMATION_SPEC}}

EXECUTION TRACE:
1. CATEGORY IDENTIFICATION:
   - Explicitly define Objects: `Obj(C) = {A, B, ...}` and `Obj(D) = {F(A), F(B), ...}`.
   - Explicitly define Morphisms: `Hom_C(A, B) = {f, g, ...}`.

2. COMPOSITION & IDENTITY PROPERTIES:
   - Verify identity preservation: `F(id_A) = id_{F(A)}`.
   - Verify composition preservation: `F(g ∘ f) = F(g) ∘ F(f)`.

3. DIAGRAM CHASING VERIFICATION:
   - Set up the diagram: Let `A, B, C, D ∈ Obj(C)` with morphisms `f: A -> B`, `g: A -> C`, `h: B -> D`, `k: C -> D`.
   - Trace an arbitrary element or transformation across Path 1 (`h ∘ f`) and Path 2 (`k ∘ g`).
   - Mathematically determine whether `h ∘ f = k ∘ g` holds universally.

4. DEFECT PINPOINTING:
   - If the diagram fails to commute, pinpoint the exact morphism where state drift or data loss occurs.
   - Formulate the minimal natural transformation `α: F => G` required to restore commutativity.
```

---

### Category IV: Sandboxed Program Synthesis & Verification (SPSV)

#### Prompt 13: Deterministic Python AST Parsing & State Execution Harness
* **Mechanism:** AST Translation & Code Execution Simulation
* **Target Objective:** Stop reasoning in ambiguous natural language; compile complex graph/combinatorial logic directly into an abstract syntax tree and trace execution states.

```markdown
[SYSTEM ARCHITECTURE: AST SYNTHESIZER & TRACE INTERPRETER]

ALGORITHMIC PROBLEM:
{{ALGORITHMIC_CHALLENGE}}

PROTOCOL:
1. CODE COMPILATION (MINIMAL RUNNABLE PYTHON):
   - Synthesize a strictly typed, pure Python 3 function resolving the problem without external dependencies.
   - Include type hints (`typing`) and pre-condition/post-condition `assert` statements.

2. AST (ABSTRACT SYNTAX TREE) TRACE:
   - Emit the conceptual AST structure for the core transformation loop:
     `Module -> FunctionDef -> For -> If -> Assign`.
   - Trace the exact control flow edges deterministically.

3. MEMORY-STATE STEP EXECUTION TABLE:
   - Execute the code against a provided edge-case input vector.
   - Render a step-by-step execution state table with columns:
     `[Step #] [Line #] [Active Variables State] [Branch Condition (True/False)] [Heap/Stack Mutations]`

4. PROPERTY VERIFICATION:
   - Prove Termination: Define the loop variant function `V(state)` and prove `V(state_{k+1}) < V(state_k)` with lower bound 0.
   - Prove Correctness: Show that the final assertion holds true over all loop iterations (loop invariant).

5. OUTPUT:
   - Final clean code implementation.
   - Exhaustive execution trace proving zero runtime index/state errors.
```

#### Prompt 14: Hypothesis Property-Based Invariant Generator & Fuzzer
* **Mechanism:** Property-Based Metamorphic Testing
* **Target Objective:** Expose latent edge cases in architectures by automatically deriving invariants and testing them against synthetic adversarial domains.

```markdown
[SYSTEM ARCHITECTURE: METAMORPHIC PROPERTY TESTER]

SYSTEM SPECIFICATION:
{{FUNCTION_OR_SERVICE_SPECIFICATION}}

DIRECTIVES:
1. SYSTEM PROPERTY IDENTIFICATION:
   Extract mathematical properties that must hold true regardless of input:
   - Idempotence: `f(f(x)) == f(x)`
   - Commutativity / Order Independence: `f(a, b) == f(b, a)`
   - Invertibility: `f_inverse(f(x)) == x`
   - Invariant Preservation: `measure(f(x)) == measure(x)`

2. TEST DATA GENERATION SCHEMA:
   - Write a `hypothesis` (Python) strategy schema that targets boundary cases:
     NaN, empty strings, integer overflow limits (`2^63 - 1`), cyclic graphs, non-ASCII encodings.

3. RUNTIME EXECUTION TRACE (SIMULATED FUZZING):
   - Simulate a 100-case fuzzing run.
   - Isolate the single minimal shrinking case (simplest counterexample) that violates the property.
   - Detail the failing execution trace step-by-step.

4. ROOT-CAUSE ATTRIBUTION:
   - Identify the invalid implicit assumption in the specification.
   - Rewrite the formal specification to handle the shrunk failure vector.
```

#### Prompt 15: Cycle-Accurate Cache Coherence & Memory Model Simulator
* **Mechanism:** Hardware State Machine & Invariant Offloading
* **Target Objective:** Track distributed concurrent writes without hallucinations using strict cache-coherence protocol state transitions (e.g., MESI/MOESI).

```markdown
[SYSTEM ARCHITECTURE: MESI PROTOCOL STATE TRACKER]

CONCURRENT EXECUTION SCENARIO:
{{CORE_READ_WRITE_SEQUENCE}}

EXECUTION MATRIX:
1. INITIAL STATE MATRIX SETUP:
   - Define initial state for lines in Core 0, Core 1, Core 2, Core 3:
     States: `M (Modified), E (Exclusive), S (Shared), I (Invalid)`.
   - Address space: Focus on single line `Address A`.

2. CYCLE-BY-CYCLE BUS SNOOPING TRACE:
   - Step sequentially through each operation in the scenario:
     `t_i: Core_k [BusRd | BusRdX | BusUpgr | PrRd | PrWr]`
   - For every cycle, compute:
     a) Local cache state transition for the issuing core.
     b) Bus signal broadcasted.
     c) Snooping transitions across all non-issuing cores.
     d) Main memory write-back trigger (if any).

3. STATE TRACE TABLE:
   - Render the complete state table:
     `| Cycle | Issuer | Action | Core 0 | Core 1 | Core 2 | Core 3 | Bus Action | Memory Sync? |`

4. RACE CONDITION & DEADLOCK VERIFICATION:
   - Identify any moment where two cores simultaneously emit `BusRdX` or upgrade operations.
   - Deterministically arbitrate the collision via priority rules.
   - Output the coherent final value stored in memory address A.
```

#### Prompt 16: Formal Grammar (EBNF) Lexer/Parser State Engine
* **Mechanism:** LL(1) / LR(1) Shift-Reduce Parsing Simulation
* **Target Objective:** Master the execution of parsers and domain-specific compilers by tracing lookahead states deterministically.

```markdown
[SYSTEM ARCHITECTURE: DETERMINISTIC LR PARSER]

INPUT GRAMMAR (EBNF):
{{LANGUAGE_GRAMMAR_RULES}}

SAMPLE STRING:
{{TARGET_STRING_TO_PARSE}}

EXECUTION PROTOCOL:
1. GRAMMAR RESTRUCTURING:
   - Eliminate any left-recursion (if creating LL parser) or construct LR item sets:
     `I_0 = Closure({S' -> . S})`

2. ACTION & GOTO TABLE GENERATION:
   - Construct the deterministic transition table:
     - Columns: Terminals (Actions: `shift k`, `reduce m`, `accept`) and Non-Terminals (`goto k`).
     - Rows: Parser States `0, 1, ..., N`.

3. STEP-BY-STEP STACK TRACE:
   - Trace the parsing of the `SAMPLE STRING`:
     Render columns:
     `[Step] [Stack] [Input Buffer] [Action Applied] [Semantic Value Construction]`
   - Execute strictly according to the Action/Goto table values.

4. PARSE TREE SYNTHESIS:
   - Output the resulting concrete syntax tree (CST) as an indented, deterministic text graph.
   - If the parse fails, point out the exact state and lookahead token where the Action table lookup hits an undefined error cell.
```

---

### Category V: Bifurcated DAG Search & Tournament Pruning (BDST)

#### Prompt 17: Tree-of-Thought Monte Carlo Node Scoring Harness
* **Mechanism:** Branching Factor DAG with Minimax/Rollout Verification
* **Target Objective:** Prevent linear reasoning traps by deterministically exploring and pruning a multi-branch hypothesis tree.

```markdown
[SYSTEM ARCHITECTURE: TREE-OF-THOUGHT TOURNAMENT HARNESS]

STRATEGIC DECISION SPACE:
{{DECISION_CHALLENGE}}

PROTOCOL:
1. HYPOTHESIS GENERATION (BRANCHING):
   - At current state S_0, generate exactly 3 mutually exclusive, collectively exhaustive (MECE) candidate actions: `A_1, A_2, A_3`.
   - Formulate nodes: `N_1 = (S_0, A_1), N_2 = (S_0, A_2), N_3 = (S_0, A_3)`.

2. DETERMINISTIC HEURISTIC EVALUATION:
   - Score each node using an explicit evaluation rubric:
     `Score = w_1 * Invariant_Safety + w_2 * Complexity_Cost + w_3 * Goal_Convergence`
     (Where `w_1=0.5, w_2=0.2, w_3=0.3` and scores are normalized [0.0 - 1.0]).
   - Show the exact calculation. Reject intuition.

3. SECOND-ORDER EXPANSION (DEPTH = 2):
   - Prune the lowest-scoring node immediately.
   - Expand the remaining two top-scoring nodes into two sub-actions each:
     `N_{1a}, N_{1b}` and `N_{2a}, N_{2b}`.
   - Evaluate all 4 leaves with the same scoring function.

4. TOURNAMENT PRUNING MATRIX:
   - Lay out the comparison table of all leaf trajectories.
   - Apply Minimax or Pareto dominance: Eliminate paths dominated across all 3 metrics.

5. SELECTION & TRACE PROOF:
   - Select the winning optimal trajectory.
   - Provide the explicit mathematical proof showing why the alternative paths failed to clear the threshold.
```

#### Prompt 18: Dialectical Red-Team Tournament Scaffold
* **Mechanism:** Adversarial Prover-Verifier Invariant Testing
* **Target Objective:** Stress-test architectures by orchestrating a deterministic adversary-defender dialogue governed by formal debate rules.

```markdown
[SYSTEM ARCHITECTURE: ADVERSARIAL VERIFICATION TOURNAMENT]

PROPOSED SYSTEM DESIGN:
{{SYSTEM_DESIGN_BLUEPRINT}}

EXECUTION HARNESS:
1. THESIS FORMULATION (PROVER):
   - Extract the 3 core claims of the design: `C_1, C_2, C_3`.
   - Formalize each claim as an invariant assertion (e.g., "Throughput never drops below T under load L").

2. ADVERSARIAL COUNTER-MODEL (VERIFIER/RED-TEAM):
   - For each claim, construct the minimal counter-scenario designed to break the invariant.
   - Use concrete edge variables: Resource exhaustion, network partitioning, packet corruption, poisoned inputs.
   - Frame each attack as an explicit event sequence.

3. DETERMINISTIC ARBITRATION MATRIX:
   - Score the attack vs. defense on each claim:
     * Attack Validity (Is the edge condition physically/architecturally possible? [Yes/No])
     * System Resilience (Does the design prevent invariant violation? [Yes/No])
   - Assign outcomes: `CLAIM_VALIDATED`, `DESIGN_COMPROMISED`, or `EDGE_UNDEFINED`.

4. SYSTEMIC PATCH SYNTHESIS:
   - For any `DESIGN_COMPROMISED` status:
     Synthesize the minimal architectural mutation (DAG edge insertion or constraint rule) required to neutralize the attack vector.
   - Re-evaluate the patched claim through the verifier loop.
```

#### Prompt 19: Multi-Objective Pareto Frontier Boundary Engine
* **Mechanism:** Vector Dominance & Pareto Optimization Engine
* **Target Objective:** Eliminate arbitrary subjective trade-offs in engineering designs by calculating the non-dominated Pareto frontier.

```markdown
[SYSTEM ARCHITECTURE: PARETO FRONTIER COMPILER]

DESIGN CANDIDATES & TRADEOFF DOMAIN:
{{ENGINEERING_DESIGN_OPTIONS}}

METRIC DIMENSIONS:
- Metric 1: Cost (Minimize)
- Metric 2: Latency (Minimize)
- Metric 3: Reliability (Maximize)

EXECUTION PIPELINE:
1. VECTOR QUANTIFICATION:
   - Map each architectural candidate `C_k` to an explicit performance vector:
     `v_k = [Cost, Latency, Reliability]`.
   - If numbers are qualitative in the input, convert them to strict ordinal scales (1-10) with clearly stated semantic anchors.

2. PARETO DOMINANCE DETERMINATION:
   - Compare all pairs `(C_a, C_b)`.
   - Rule: `C_a` strictly dominates `C_b` (`C_a ≻ C_b`) if and only if:
     ∀ i, `Metric_i(C_a)` is no worse than `Metric_i(C_b)`, and
     ∃ i, `Metric_i(C_a)` is strictly better than `Metric_i(C_b)`.
   - Document every dominance elimination step explicitly.

3. PARETO FRONTIER IDENTIFICATION:
   - Extract the non-dominated set: `P = {C | ¬∃ C' such that C' ≻ C}`.
   - Discard all dominated candidates.

4. EXTREME-POINT TRADEOFF ANALYSIS:
   - Compute the marginal rate of substitution between the surviving candidates on the frontier:
     `ΔReliability / ΔCost` and `ΔLatency / ΔCost`.
   - Output the exact condition under which a system architect should select Candidate A over Candidate B.
```

#### Prompt 20: Recursive Formal Meta-Reflection Engine
* **Mechanism:** Meta-Cognitive Verification Harness
* **Target Objective:** Use a secondary internal symbolic solver prompt to inspect, prove, and correct reasoning artifacts generated in a primary reasoning chain.

```markdown
[SYSTEM ARCHITECTURE: FORMAL META-COGNITIVE INSPECTOR]

PRIMARY REASONING ARTIFACT:
{{RAW_LLM_OUTPUT_OR_REASONING_CHAIN}}

EVALUATION PROTOCOL:
1. EXTRACTION OF LATENT PREMISES:
   - Parse the primary artifact into a linear list of propositions: `P = {p_1, p_2, ..., p_m}`.
   - Separate explicit assertions from unstated implicit assumptions.

2. SYMBOLIC SOUNDNESS VERIFICATION:
   - For every inference step `p_i -> p_{i+1}`, test logical validity:
     Does `p_i` semantically entail `p_{i+1}`, or is there an unstated jump?
   - Tag each step with:
     * `VALID_DEDUCTION`
     * `NON_SEQUITUR`
     * `AFFIRMING_THE_CONSEQUENT`
     * `HALLUCINATED_INVARIANT`

3. DETERMINISTIC DAG RE-MAPPING:
   - Reconstruct the actual logical argument as a dependency DAG.
   - Run cycle and reachability checks: Does the terminal conclusion actually have a continuous path back to verified ground premises?
   - Isolate any disconnected subgraphs (reasoning islands).

4. RE-WRITE & CONVERGENCE:
   - If defects are found, purge all invalid paths.
   - Re-synthesize the argument trace strictly using validated topological edges.
   - Conclude with a confidence score computed as:
     `R = (Validated_Edges) / (Total_Attempted_Edges)`.
```

---

## 3. Operational Framework

### Execution Heuristics for Self-Paced Mastery

To build 95th-percentile intuition for when and how to offload thinking traces to deterministic DAGs and symbolic solvers, follow this structured execution loop:

```
[Problem Space]
       │
       ▼
[Phase 1: Semantic Disambiguation]
 └─ Extract Entities, Relations, Invariants
       │
       ▼
[Phase 2: Topological Boundary Check]
 ├─ Cyclic or Concurrent? ──► [Offload to TDG (Prompts 1-4)]
 └─ Sequential Linear?    ──► [Direct Execution Trace]
       │
       ▼
[Phase 3: Formal Intermediate Representation (FIR)]
 ├─ Logic / Constraint?   ──► [Compile to SMT-LIB2 / CSP (Prompts 5-8)]
 ├─ Algebraic / Dynamic?  ──► [Compile to SymPy / Convex (Prompts 9-12)]
 └─ Algorithmic / State?  ──► [Compile to Python AST (Prompts 13-16)]
       │
       ▼
[Phase 4: Deterministic Solve / Simulated Execution]
 └─ Execute external solver OR step-trace simulation
       │
       ▼
[Phase 5: Metacognitive Adversarial Audit]
 └─ Tournament Pruning & Reflection (Prompts 17-20)
       │
       ▼
[Zero-Hallucination Solution Artifact]
```

#### 1. Cold-Start Scaffolding (Formulating the FIR)
* **The Non-Deterministic Trap:** When faced with a complex problem (e.g., distributed consensus, complex scheduling, security access), resist the urge to type: `"Explain how to solve X..."` or `"Solve this puzzle..."`.
* **The FIR Shift:** Force the model into a intermediate compilation step. Instruct it: 
  > *"Do not solve this problem yet. First, extract the state variables, continuous/discrete constraints, and transform this prompt into [SMT-LIB2 / Python AST / Adjacency Matrix]."*
* **Pedagogical Value:** Inspecting the FIR reveals whether the LLM correctly grounded the domain rules before spending compute on inferences. If the FIR is broken, any conclusion is a hallucinated coincidence.

#### 2. Topological Dependency Parsing
* **Heuristic:** Whenever reasoning involves more than three interdependent variables, force the construction of an adjacency list showing dependency edges: `A -> B`.
* Run a cycle-detection pass. Autoregressive models routinely get caught in implicit circular reasoning (e.g., claiming A caused B, which was required for A).
* Explicitly demanding a **Topological Sort** or **Critical Path Analysis** forces the model's test-time compute to traverse the true causal chain in order, preventing downstream errors.

#### 3. Formal Invariant Enforcement
* Define the universal conservation laws of the domain prior to generation:
  * In distributed systems: Safety (nothing bad happens) and Liveness (something good eventually happens).
  * In arithmetic/physics: Dimensional homogeneity, mass/energy conservation, monotonic entropy.
  * In authorization: Deny-by-default, least privilege closure.
* By providing explicit assertion templates (e.g., `assert dynamic_val >= 0`), you turn the token-generation process into a self-checking proof system.

#### 4. Diagnostic Rubrics for Evaluating Model Reasoning Fidelity

Use these precise rubrics to evaluate whether a reasoning trace is truly deterministic or merely hallucinating structured thought:

| Evaluation Metric | High-Fidelity Symbolic Output (Target) | Hallucinated CoT Drift (Failure Mode) |
| :--- | :--- | :--- |
| **AST/Syntax Validity** | Code, SMT-LIB2, or logic syntax compiles and executes without syntax errors in an external runtime. | Pseudo-code or symbolic syntax uses fabricated functions, unclosed parentheses, or ungrounded methods. |
| **Graph Acyclicity** | Explicitly checks for cycles; resolves feedback loops via discrete time slicing ($t, t+1$). | Trapped in recursive loops; uses circular justifications (e.g., "A failed because of B, which failed due to A"). |
| **Constraint Soundness** | Zero violations of defined invariant rules; respects complementary slackness and domain bounds. | Asserts that constraints are satisfied while silently dropping or relaxing boundary variables. |
| **Counterexample Minimality**| Isolates the exact minimal failing edge or variable assignment (e.g., via DPLL / Unsat Core). | Emits hand-wavy explanations of edge-case failures without identifying the minimal failing state vector. |

#### 5. Failure Modes and Mitigation Matrix

* **Failure Mode 1: Combinatorial State Explosion within Context Window**
  * *Symptom:* The model attempts to exhaustively list all possible paths in a complex graph and runs out of tokens or degrades into repetitive loops.
  * *Mitigation:* Shift from exhaustive generation to symbolic solver offloading. Direct the model to emit a compact SMT-LIB2 or CSP script, formulate the optimization problem, and call an execution runtime (or emulate branch pruning using Alpha-Beta / AC-3 heuristics).

* **Failure Mode 2: Premature Branch Commitment**
  * *Symptom:* The model selects the first plausible hypothesis in Step 1 of its reasoning trace, then spends the rest of the generation rationalizing that choice.
  * *Mitigation:* Enforce **Tournament Scaffolding** (Prompt 17/18). Mandate the generation of three distinct, parallel candidate nodes ($N_1, N_2, N_3$) evaluated against a numerical matrix before allowing any second-order expansion.

* **Failure Mode 3: Semantic Drift in Long Chains of Deduction**
  * *Symptom:* A variable's definition subtly shifts meaning between Step 3 and Step 15 of a long context window.
  * *Mitigation:* Require **Step-Execution Tables** (Prompt 13/15). Every discrete state change must be written out in a fixed markdown table with strict column headers for active variable states. The tabular structure penalizes drift by making any mutation explicit in the immediate token context.
