# NS-LLM / QSOL-LFM-NS Roadmap

This roadmap defines the staged implementation sequence for NS-LLM. The project deliberately separates the model substrate, geometric lattice, reasoning controller, and numerical solver integration so each layer can be tested independently.

> **Machine-only roadmap:** [`ROADMAP4AI.md`](ROADMAP4AI.md)  
> **Canonical machine authority:** [`docs/roadmap.json`](docs/roadmap.json)

## PR #1 — Documentation and machine contracts

**Status:** current.

Purpose: freeze enough vocabulary and authority boundaries to begin implementation without agents inventing architecture as they go.

Deliverables include the human README, `README4AI.md`, machine-only `AGENTS.md`, typed architecture/scientific/training contracts, and this roadmap.

**No runtime implementation belongs in PR #1.**

---

## PR #2 — QSOL-LFM-NS

Build the first executable model/orchestration baseline.

### Scope

- repository/package scaffold;
- typed configuration and deterministic request/response envelopes;
- QSOL-CONTEXT `ns_llm` profile ingestion;
- RES=RAG adapter/interface;
- LFM2.5-family model adapter, initially targeting `LiquidAI/LFM2.5-8B-A1B-Base` without freezing it permanently;
- context/evidence compiler interface;
- explicit extension seams for the later lattice, reasoner, verifier, and solver;
- deterministic tests and receipts where practical.

### Out of scope

- 3–5–8 lattice cell implementation;
- custom reasoning controller;
- NS-SIM execution;
- backbone surgery or native lattice injection.

The objective is to prove that the model, context, and retrieval substrate can run as a clean system before geometric state is introduced.

---

## PR #3 — Lattice Cell Arrays

Implement **Architecture Candidate A: the 3–5–8 hierarchical tri-lattice**.

```text
                    QSOL-LFM-NS
                         │
          ┌──────────────┼──────────────┐
          ↓              ↓              ↓
       3×3×3          5×5×5          8×8×8
     SIERPINSKI       RELATION         RUBIK
       CONTROL          ARRAY       TRANSFORMATION
      27 CELLS        125 CELLS       512 CELLS
          │              │              │
          └──────────────┼──────────────┘
                         ↓
                PROVENANCE LEDGER
```

### L0 — 3×3×3 Sierpinski control lattice

Role:

- epistemic state;
- task/reasoning classification;
- evidence class;
- hierarchical decomposition;
- control signals for lower lattices.

Question answered: **What kind of problem, evidence, or reasoning state is active?**

### L1 — 5×5×5 relation array

Inspired by the earlier neutral-atom-array structure, but used here as an abstract scientific relation lattice.

Role:

- fields;
- operators;
- constraints;
- physical/local relationships;
- evidence relationships.

Question answered: **What is related to what?**

### L2 — 8×8×8 Rubik transformation workspace

Role:

- active working state;
- candidate states;
- deterministic transformations;
- temporal evolution;
- operator application;
- reasoning/execution workspace.

Question answered: **How does state transform?**

### External immutable provenance ledger

Every meaningful lattice mutation should be capable of producing a receipt containing input identity, operation, coordinates or selected cells, output identity, evidence source, and relevant execution/model/context identity.

### Coupling rule

```text
L0 controls/selects L1
L1 constrains/materializes L2
L2 returns transformed state/evidence to L1
L1 updates epistemic state in L0
```

The 3–5–8 geometry is a **candidate architecture**, not yet a claim that this topology is optimal. It should later be benchmarked against simpler graph/single-lattice alternatives.

---

## PR #4 — Custom Reasoner

Implement the reasoning controller on top of the QSOL-LFM-NS substrate and tri-lattice.

Initial controller identity:

```text
QSOL_NS_REASONER_V1
```

Target loop:

```text
parse problem
→ classify reasoning/evidence state
→ retrieve evidence
→ activate/update lattice neighborhood
→ identify unknowns
→ select reasoning action
→ transform working state
→ validate available evidence
→ update epistemic state
→ derive bounded conclusion
→ emit provenance-bound result
```

The reasoner must know when it lacks numerical or formal evidence and must not simulate execution it has not performed.

NS-SIM remains an abstract execution dependency in this PR; direct solver integration is deferred to PR #5.

---

## PR #5 — NS-SIM Integration

Connect the custom reasoner to deterministic Navier–Stokes execution.

### Scope

- NS-SIM adapter/interface implementation;
- experiment identity and backend selection;
- receipt ingestion;
- solver diagnostics mapped into lattice/evidence state;
- numerical claim classification;
- fail-closed numerical output gating;
- reproducibility metadata and comparison evidence where supported by NS-SIM.

Core invariant:

```text
DO_NOT_PRETEND_YOU_SOLVED_THE_PDE
```

A numerical claim must distinguish model inference from actual solver-produced evidence.

---

## Later phases

Only after the external architecture has measurable baselines should the project consider deeper model modification, including:

- lattice encoder + model adapter;
- latent lattice injection;
- lattice cross-attention;
- recurrent geometric state;
- continued pretraining / SFT / preference optimization where justified;
- comparison of the 3–5–8 tri-lattice against simpler or learned alternatives;
- generalized QSOL-LFM domain lattices beyond Navier–Stokes.

## Governing principle

```text
MODEL SUBSTRATE
    before
LATTICE
    before
CUSTOM REASONER
    before
NUMERICAL SOLVER INTEGRATION
    before
BACKBONE MODIFICATION
```

Each PR should leave a measurable interface and regression boundary for the next one.
