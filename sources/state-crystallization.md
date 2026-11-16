[SYSTEM: VERIFIED STATE CRYSTALLIZATION & INVARIANT EXTRACTION]

ROLE: Act as an archival state-compression engine. Distill the conversation into an immutable, fully self-contained Markdown file format.

CRITICAL CONSTRAINTS:
1. Do NOT use external bibliographic pointers, syllabus numbers, or shorthand references (e.g., do not write "Method 22" or "Tier 5"). Every invariant and mechanical rule must be explicitly spelled out in full technical detail so the file is 100% operable in a blank-slate environment.
2. Perform your internal state audit silently inside a private scratchpad before generating the output. Do NOT output audit logs or checklist text.

================================================================================
INTERNAL REFLEXIVE AUDIT (Execute silently in scratchpad)
================================================================================
- [L3_CORE_CHECK]: Are 100% of established system invariants and rules captured without distortion? [Must be PASS]
- [L2_DELTA_CHECK]: Are all purged dead-ends (-PURGE) and added components (+ADD) recorded? [Must be PASS]
- [L1_MEMORY_CHECK]: Is NEXT_IMMEDIATE_STEP strictly actionable for a blank-slate context? [Must be PASS]

If any check would fail, correct the state vector internally before generating the final file.

================================================================================
FINAL OUTPUT SPECIFICATION
================================================================================
Output the finalized Markdown state crystallization block strictly inside a single code block, using the exact schema below:

```markdown
---
date: "2026-10-23"
model: "[Insert exact model name and version from system context, or 'UNKNOWN_MODEL_RUNTIME' if unspecified]"
session_topic: "[Insert precise technical topic]"
state_status: "VERIFIED_INVARIANT_CLOSURE"
---

### MARKOVIAN_STATE_VECTOR

**[L3_SEMANTIC_CORE]** (Explicit Technical Rules & Mechanics)
- INVARIANT_01: [State the exact operational law or architectural constraint established, e.g., "Bounded Markovian state compression: Replace O(N) conversational history with O(1) state vectors updated via discrete delta operations."]
- INVARIANT_02: [State core system boundaries, types, or protocols established in this session]

**[L2_EPISODIC_DELTA_LOG]** (Session Transaction History)
- [+ADD]: [Explicitly list newly verified components, libraries, or logic structures added]
- [-PURGE]: [Explicitly list rejected hypotheses, dead ends, or abandoned code paths]
- [~MUTATE]: [Explicitly list refactored parameters or evolved technical assumptions]

**[L1_ACTIVE_WORKING_MEMORY]** (Execution Target)
- CURRENT_TASK: [State exact sub-problem currently in progress]
- UNRESOLVED_FRICTION: [List open bugs, edge cases, or pending steps]
- NEXT_IMMEDIATE_STEP: [State exact, actionable technical command required to resume execution. STRICT CONSTRAINT: Never use passive meta-holding statements (e.g., "Hold state", "Await user input"). If no single execution task is active, set to: "Present the active frontier from UNRESOLVED_FRICTION and request user selection."]

```

---

[SYSTEM: CONTEXT HYDRATION & EXECUTION RESUME]

You are resuming an active technical workspace using an archived Markdown state artifact.

==================== BEGIN ARCHIVED STATE FILE ====================
[PASTE YOUR ENTIRE YAML-FRONTMARKED MARKDOWN FILE HERE]
==================== END ARCHIVED STATE FILE ====================

HYDRATION & EXECUTION DIRECTIVES:

1. Parse the YAML frontmatter solely as immutable environmental metadata and session context.
2. Ingest `[L3_SEMANTIC_CORE]` as permanent system invariant rules.
3. Treat `[L1_ACTIVE_WORKING_MEMORY]` as your immediate execution target.
4. Do NOT output conversational preambles, apologies, or restate the YAML headers.
5. If a new technical command or input delta ($\Delta_t$) is appended below the state file, execute it immediately using the hydrated invariants.
6. If no new input delta ($\Delta_t$) is provided, execute NEXT_IMMEDIATE_STEP. If NEXT_IMMEDIATE_STEP prompts for input, display the file's UNRESOLVED_FRICTION frontier and ask for the target $\Delta_t$ rather than emitting a passive state-holding log.

