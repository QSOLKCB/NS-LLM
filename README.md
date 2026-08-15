# NS-LLM / QSOL-LFM-NS

> A provenance-aware geometric reasoning architecture for Navier–Stokes and scientific problem solving.

**Status:** architecture/documentation bootstrap. Implementation begins in **PR #2**.

NS-LLM separates persistent context, dynamic retrieval, geometric structure, learned reasoning, executable computation, verification, and output instead of collapsing them into a single context window.

```text
NS PROBLEM
    ↓
QSOL-CONTEXT
    ↓
RES=RAG
    ↓
GEOMETRIC INFORMATION MAPPED LATTICE
    ↓
LFM2.5-FAMILY BACKBONE
    ↓
CUSTOM REASONER
    ↓
NS-SIM / SYMBOLIC / LEAN 4
    ↓
SCIENTIFIC VERIFIER
    ↓
PROVENANCE-BOUND OUTPUT
```

## Core idea

> **Do not ask one context window to be memory, retrieval, geometry, reasoning, simulation, and verification at the same time.**

| Layer | Role |
|---|---|
| **QSOL-CONTEXT** | persistent provenance-bound context |
| **RES=RAG** | dynamic evidence retrieval |
| **Geometric Information Mapped Lattice** | typed structural memory |
| **LFM2.5-family model** | learned statistical reasoning substrate |
| **QSOL_NS_REASONER** | reasoning/execution controller |
| **NS-SIM / symbolic / Lean 4** | executable evidence |
| **Scientific Verifier** | evidence checks and fail-closed claim gating |

## Backbone direction

Current preferred candidate:

```text
LiquidAI/LFM2.5-8B-A1B-Base
```

This is a preferred candidate, **not a frozen dependency**. The architecture should be benchmarked before any backbone surgery.

## 3–5–8 lattice direction

The first concrete lattice candidate will be implemented in **PR #3**:

```text
3×3×3 Sierpinski control lattice
        +
5×5×5 scientific relation array
        +
8×8×8 Rubik transformation workspace
        +
immutable provenance ledger
```

The 3–5–8 topology is an **architecture candidate**, not yet a claim of optimality.

## Implementation roadmap

The staged sequence is intentionally strict:

```text
PR #1  Documentation + contracts
   ↓
PR #2  QSOL-LFM-NS model/orchestration substrate
   ↓
PR #3  3–5–8 Lattice Cell Arrays
   ↓
PR #4  Custom Reasoner — QSOL_NS_REASONER_V1
   ↓
PR #5  NS-SIM integration + numerical evidence gating
```

See the full human roadmap: **[`ROADMAP.md`](ROADMAP.md)**.

## Numerical and formal evidence

Core rule:

```text
DO_NOT_PRETEND_YOU_SOLVED_THE_PDE
```

Numerical claims should be bound to actual solver-produced evidence when execution is required. Formal notation is not treated as proof unless a checked formal artifact supports the proposition.

## AI / agent documentation

AI agents should **not** treat this README as their operating contract.

- Machine entrypoint: [`README4AI.md`](README4AI.md)
- Machine roadmap: [`ROADMAP4AI.md`](ROADMAP4AI.md)
- Canonical agent contract: [`AGENTS.md`](AGENTS.md)
- Machine authority map: [`docs/index.json`](docs/index.json)

Agent-facing documents are intentionally optimized for machine consumption and deterministic future models rather than human readability.

## Claim boundary

NS-LLM does **not** claim that:

- an LLM has solved the Navier–Stokes Millennium Prize problem;
- language-model weights replace numerical simulation;
- retrieval is automatically factual;
- formal-looking notation constitutes proof;
- large context windows are equivalent to reasoning;
- the proposed 3–5–8 lattice is already known to be optimal.

The project is an architecture and engineering experiment in separating reasoning, structured memory, evidence, execution, and verification.
