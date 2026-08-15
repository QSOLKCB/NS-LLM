# NS-LLM / QSOL-LFM-NS

> A provenance-aware geometric reasoning architecture for Navier–Stokes and scientific problem solving.

**Status:** architecture and documentation bootstrap. Model/runtime implementation begins in **PR #2**.

NS-LLM explores a language-model system in which persistent context, dynamic retrieval, geometric structure, learned reasoning, executable computation, verification, and output remain separate but interoperable layers.

```text
NS PROBLEM
    ↓
QSOL-CONTEXT
    ↓
RES=RAG
    ↓
GEOMETRIC INFORMATION MAPPED LATTICE
    ↓
MODEL CONTEXT / LATENT INTERFACE
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

## Why this architecture

The project is built around one rule:

> **Do not ask one context window to be memory, retrieval, geometry, reasoning, simulation, and verification at the same time.**

The major layers have different jobs:

| Layer | Role |
|---|---|
| **QSOL-CONTEXT** | persistent, provenance-bound project/research context |
| **RES=RAG** | dynamic evidence retrieval |
| **Geometric Information Mapped Lattice** | typed structural representation of fields, operators, constraints, evidence, time, and provenance |
| **LFM2.5-family model** | learned statistical reasoning substrate |
| **QSOL_NS_REASONER** | reasoning and execution controller |
| **NS-SIM / symbolic / Lean 4** | executable numerical, symbolic, and formal evidence |
| **Scientific Verifier** | claim classification, evidence checks, and fail-closed output gating |

## Backbone direction

The current preferred candidate is:

```text
LiquidAI/LFM2.5-8B-A1B-Base
```

This is a **preferred candidate, not a frozen dependency**. The first implementation phase should prove the external architecture before modifying the model backbone.

## The lattice

The Geometric Information Mapped Lattice is intended to be a real intermediate representation, not decorative prompt prose.

For Navier–Stokes it can represent:

- domain and geometry;
- coordinate systems and discretization;
- velocity, pressure, vorticity, density, and forcing;
- gradient, divergence, Laplacian, advection, and projection operators;
- incompressibility and boundary constraints;
- temporal state;
- analytical, numerical, retrieved, and formal evidence;
- provenance, experiment identity, backend, precision, and claim class.

Typed relationships can encode structures such as:

```text
velocity   --DIVERGENCE-->    incompressibility
pressure   --GRADIENT-->      momentum_equation
geometry   --CONSTRAINS-->    boundary_condition
dt         --CONSTRAINED_BY--> CFL
experiment --EXECUTED_BY-->   NS_SIM
result     --SUPPORTED_BY-->   receipt
```

## Numerical and formal evidence

NS-LLM should not simulate having executed scientific tools.

Core rule:

```text
DO_NOT_PRETEND_YOU_SOLVED_THE_PDE
```

When numerical evidence is required, the reasoner should invoke an executable solver such as NS-SIM and bind claims to the returned experiment identity, diagnostics, receipts, and provenance.

Formal notation is likewise not treated as proof. Lean 4 is reserved for bounded propositions that are actually checked.

## PR #1 — documentation and contracts

This documentation bootstrap establishes:

- the architecture vocabulary;
- machine-only agent instructions;
- the AI documentation entrypoint;
- context and evidence interfaces;
- the initial lattice schema;
- scientific/output claim boundaries;
- the training and backbone contract;
- the staged implementation roadmap.

**No model implementation is introduced in this PR.**

## PR #2 — first implementation target

The first implementation PR should build the external-orchestration baseline:

```text
QSOL-CONTEXT
    +
RES=RAG
    +
SERIALIZED LATTICE
    +
LFM2.5-FAMILY MODEL INTERFACE
    +
NS-SIM TOOL INTERFACE
```

The baseline should avoid modifying the backbone. It exists to test whether separated context, evidence, structure, execution, and verification improve the system before deeper lattice/model integration is attempted.

## AI / agent documentation

AI agents should **not** treat this README as their primary operating contract.

**Machine entrypoint:** [`README4AI.md`](README4AI.md)

`README4AI.md`, `AGENTS.md`, `.github/copilot-instructions.md`, and `docs/*.json` are intentionally optimized for AI agents, deterministic future models, and tooling rather than human readability.

## Claim boundary

NS-LLM does **not** claim that:

- an LLM has solved the Navier–Stokes Millennium Prize problem;
- language-model weights replace numerical simulation;
- retrieved text is automatically factual;
- formal-looking notation constitutes proof;
- a large context window is equivalent to reasoning;
- one verification mechanism is suitable for every scientific claim.

Different claims require different evidence.

## Related repositories

- QSOL-CONTEXT — persistent deterministic context substrate
- RES=RAG — dynamic evidence retrieval / protocol research
- NS-SIM — deterministic Navier–Stokes execution and numerical evidence
- NS — Navier–Stokes research artifacts

---

**Repository phase:** `ARCHITECTURE_SPECIFICATION`

**Implementation begins:** `PR #2`
