# QSOL-LFM

> **A provenance-aware geometric reasoning architecture for Navier–Stokes and scientific problem solving.**

QSOL-LFM is a proposed custom language-model architecture built around a simple idea:

> **Do not ask one context window to be memory, retrieval, geometry, reasoning, simulation, and verification at the same time.**

Instead, QSOL-LFM separates those responsibilities into distinct layers:

```text
LLM FOR SOLVING NS
    ↓
QSOL_CONTEXT
    ↓
RES=RAG
    ↓
GEOMETRIC INFORMATION MAPPED LATTICE
    ↓
MODEL CONTEXT / LATENT INTERFACE
    ↓
CUSTOM REASONING
    ↓
DETERMINISTIC / FORMAL EXECUTION
    ↓
VERIFICATION
    ↓
MODEL OUTPUT
```

The initial target domain is **Navier–Stokes reasoning**, using a Liquid AI **LFM2.5** base model as the likely backbone.

The long-term objective is broader: a reusable geometric reasoning architecture in which domain-specific lattices can represent physics, mathematics, sonification, formal systems, and other structured research domains.

---

## 1. Core idea

The architecture combines six different kinds of capability:

```text
QSOL_CONTEXT
    = persistent context

RES=RAG
    = dynamic evidence retrieval

GEOMETRIC INFORMATION MAPPED LATTICE
    = structured relational representation

LFM2.5
    = learned statistical intelligence

CUSTOM REASONING
    = reasoning and execution control policy

NS-SIM / symbolic / Lean
    = executable verification
```

These are intentionally treated as **different systems** rather than flattened into one giant prompt.

---

## 2. Proposed architecture

```text
                         ┌───────────────────┐
                         │    QSOL_CONTEXT   │
                         │ contracts / state │
                         │ provenance / user │
                         └─────────┬─────────┘
                                   │
NS PROBLEM ──→ PROBLEM NORMALIZER ─┼────→ RES=RAG
                                   │         │
                                   │         ↓
                                   │   retrieved evidence
                                   │         │
                                   └────┬────┘
                                        ↓
                           CONTEXT / EVIDENCE COMPILER
                                        ↓
                 ┌────────────────────────────────────┐
                 │ GEOMETRIC INFORMATION MAPPED       │
                 │ LATTICE                            │
                 │                                    │
                 │ geometry • fields • operators      │
                 │ boundary conditions • invariants   │
                 │ provenance • uncertainty • time    │
                 └─────────────────┬──────────────────┘
                                   ↓
                        LFM2.5-8B-A1B BASE
                      ↙          ↓          ↘
              convolution     attention     lattice
                 state          state        adapter
                      ↘          ↓          ↙
                         CUSTOM REASONER
                               ↕
                 ┌─────────────┴─────────────┐
                 │                           │
              NS-SIM                  FORMAL / SYMBOLIC
        numerical execution          checks / equations
                 │                           │
                 └─────────────┬─────────────┘
                               ↓
                     SCIENTIFIC VERIFIER
                               ↓
                         MODEL OUTPUT
                               +
                   RECEIPT / CLAIM BOUNDARY
```

---

## 3. Why LFM2.5

The current preferred backbone is:

```text
LiquidAI/LFM2.5-8B-A1B-Base
```

Why this family is interesting for QSOL-LFM:

- approximately **8.3B total parameters**;
- approximately **1.5B active parameters per token**;
- **128K context window**;
- hybrid architecture combining convolutional and attention blocks;
- a Base checkpoint suitable for customization and fine-tuning;
- a relatively small active compute footprint compared with the total parameter count;
- compatible with a design where external retrieval and structured reasoning carry part of the knowledge burden.

The goal is **not** to rely on the backbone as an encyclopedic scientific database.

QSOL_CONTEXT, RES=RAG, and executable scientific tools provide external state, evidence, and verification.

The model is primarily responsible for:

- interpretation;
- reasoning;
- orchestration;
- hypothesis generation;
- tool selection;
- synthesis;
- explanation.

### Reference links

- Liquid AI LFM2.5-8B-A1B:  
  https://huggingface.co/LiquidAI/LFM2.5-8B-A1B
- Liquid Foundation Models v2 architecture overview:  
  https://www.liquid.ai/blog/liquid-foundation-models-v2-our-second-series-of-generative-ai-models

---

## 4. QSOL_CONTEXT

QSOL_CONTEXT is the persistent context layer.

It should contain machine-readable information such as:

```text
identity
projects
research contracts
software state
environment
publications
provenance
preferences
current decisions
context precedence
```

It is **not** intended to be loaded wholesale for every inference.

Instead, the architecture should select the smallest useful context profile for the current task.

Example:

```yaml
CONTEXT_PROFILE:
  domain: navier_stokes
  include:
    - current NS-SIM contract
    - current hardware environment
    - relevant reproducibility policy
    - relevant research relationships
  exclude:
    - unrelated projects
    - stale context
    - duplicate evidence
```

---

## 5. RES=RAG

RES=RAG provides dynamic evidence retrieval.

Where QSOL_CONTEXT answers:

```text
What stable context should the model know?
```

RES=RAG answers:

```text
What evidence matters for this problem right now?
```

Possible retrieval targets include:

- papers;
- equations;
- numerical references;
- benchmark datasets;
- prior experiment receipts;
- formal definitions;
- code documentation;
- solver contracts;
- archived results.

Retrieved evidence should remain provenance-bound.

The model should be able to distinguish:

```text
OBSERVED
RETRIEVED
INFERRED
HYPOTHESIZED
FORMALLY_PROVED
NUMERICALLY_MEASURED
UNVERIFIED
```

---

## 6. Geometric Information Mapped Lattice

The **Geometric Information Mapped Lattice** is the central experimental layer.

It should not merely be another text prompt.

It should become a real intermediate representation.

For Navier–Stokes, a lattice may represent:

```text
DOMAIN
├── geometry
├── coordinate system
├── discretization
└── boundary regions

FIELDS
├── velocity u
├── pressure p
├── vorticity ω
├── density ρ
└── forcing f

OPERATORS
├── ∇
├── ∇·
├── ∇²
├── advection
└── projection

CONSTRAINTS
├── ∇·u = 0
├── boundary conditions
├── CFL
├── diffusion admissibility
└── pressure gauge

TEMPORAL
├── t
├── Δt
├── previous state
└── candidate state

EVIDENCE
├── analytical
├── numerical
├── retrieved
├── formal
└── user supplied

PROVENANCE
├── source
├── experiment hash
├── backend
├── precision
└── confidence / claim class
```

Relationships become typed edges:

```text
velocity --DIVERGENCE--> incompressibility
velocity --LAPLACIAN--> viscous term
pressure --GRADIENT--> momentum equation
geometry --CONSTRAINS--> boundary condition
Δt --CONSTRAINED_BY--> CFL
experiment --EXECUTED_BY--> NS-SIM
result --SUPPORTED_BY--> receipt
```

The purpose of this layer is to preserve **structure**, not just tokens.

> RAG retrieves facts.  
> The lattice represents how those facts relate.

---

## 7. Context / Evidence Compiler

The model context window should be treated as a transport layer, not as the architecture itself.

The important question is:

> **What enters the context or latent interface?**

The Context / Evidence Compiler should combine:

```text
QSOL_CONTEXT
      +
RES=RAG
      +
GEOMETRIC LATTICE
      ↓
COMPILED MODEL INPUT
```

Example policy:

```yaml
INCLUDE:
  current_problem: true
  governing_contract: true
  relevant_qsol_context: true
  relevant_res_rag_evidence: true
  local_lattice_neighborhood: true
  current_solver_receipts: true

EXCLUDE:
  unrelated_projects: true
  stale_context: true
  duplicate_evidence: true
  historical_discussion_without_dependency: true
```

---

## 8. Lattice integration strategies

### Phase A — serialized lattice

The first implementation should remain simple.

Serialize the lattice into structured tokens:

```text
LATTICE_NODE
LATTICE_EDGE
FIELD
OPERATOR
CONSTRAINT
PROVENANCE
```

Then fine-tune LFM2.5 to reason over this representation.

Advantages:

- easy to implement;
- works with an unmodified model architecture;
- compatible with LoRA/SFT;
- easy to inspect;
- easy to benchmark.

### Phase B — lattice encoder + adapter

Once the serialized representation works:

```text
GEOMETRIC LATTICE
      ↓
LATTICE ENCODER
      ↓
PROJECTOR / ADAPTER
      ↓
LFM HIDDEN REPRESENTATION
```

This allows structured geometry to become latent state rather than requiring every relation to be converted into natural-language tokens.

### Phase C — gated lattice injection

A later experimental architecture could inject lattice state into selected LFM blocks:

```text
LFM BLOCK
    ↓
CONV
    ↓
CONV
    ↓
GQA  ←──── lattice adapter
    ↓
CONV
    ↓
CONV
    ↓
GQA  ←──── updated lattice state
    ↓
...
```

This would move QSOL-LFM from:

```text
LLM + structured prompt
```

toward:

```text
LLM + native geometric reasoning substrate
```

---

## 9. Custom reasoning layer

The model should not simply generate a hidden answer in one pass.

The reasoner should operate as a controller.

Example:

```text
1. parse problem
2. identify governing equations
3. retrieve relevant evidence
4. construct or update lattice
5. determine unknowns
6. select reasoning path
7. determine whether numerical execution is required
8. call NS-SIM / symbolic / formal engine
9. validate returned evidence
10. update lattice
11. derive bounded conclusion
12. generate answer + provenance
```

The reasoning controller should be trained to know when it **cannot** derive a trustworthy answer from text alone.

---

## 10. NS-SIM inside the reasoning loop

A model for Navier–Stokes should not pretend to be a numerical solver when a deterministic solver exists.

Bad:

```text
MODEL:
"I calculate divergence = 1.72e-13."
```

Preferred:

```text
MODEL:
"Numerical evidence is required."

        ↓

NS-SIM

experiment hash
backend
state hash
diagnostics
receipt
result

        ↓

MODEL:
"Under the declared numerical contract,
NS-SIM produced..."
```

Core rule:

```text
DO_NOT_PRETEND_YOU_SOLVED_THE_PDE
```

Numerical claims should be bound to executable evidence wherever practical.

---

## 11. Verification engines

### NS-SIM

Use for:

- deterministic Navier–Stokes execution;
- numerical verification;
- backend comparison;
- reproducibility evidence;
- diagnostics;
- receipts.

### Symbolic engine

Use for:

- algebraic manipulation;
- dimensional analysis;
- equation rearrangement;
- symbolic differentiation;
- symbolic consistency checks.

### Lean 4

Use for:

- bounded formal claims;
- definitions;
- invariant proofs;
- proof obligations;
- formalized reasoning steps where appropriate.

Formalization should not be used decoratively.

A Lean theorem should prove a clearly defined proposition, not merely make the repository look rigorous.

---

## 12. Scientific verifier

Before a final answer is emitted, claims should be classified.

Example:

```yaml
CLAIM:
  text: "The candidate backend matches the CPU reference."
  class: numerical
  evidence:
    type: NS_SIM_RECEIPT
    reproducibility_class: R3
    comparison_contract: cpu_cuda_v1
  status: supported
```

Another example:

```yaml
CLAIM:
  text: "This proves global regularity of 3D Navier-Stokes."
  class: mathematical
  evidence: none
  status: reject
```

The verifier should fail closed when strong claims lack appropriate evidence.

---

## 13. Output contract

The final output may include:

```text
natural-language answer
reasoning summary
equations
retrieved evidence
numerical evidence
formal evidence
uncertainty
claim boundaries
experiment identity
receipts
provenance
```

Possible structure:

```yaml
OUTPUT:
  answer: ...
  claims:
    - id: claim_001
      type: numerical
      status: supported
      source: ns-sim
    - id: claim_002
      type: interpretation
      status: qualified
  experiments:
    - hash: ...
      backend: cpu-reference-v1
      receipt: ...
  unresolved:
    - ...
```

---

## 14. Proposed training strategy

Start with the Base checkpoint.

```text
LFM2.5-8B-A1B-Base
        │
        ├── continued pretraining
        │     └── Navier–Stokes / applied mathematics corpus
        │
        ├── supervised fine-tuning
        │     ├── QSOL reasoning format
        │     ├── lattice serialization
        │     ├── evidence classification
        │     └── tool-selection examples
        │
        ├── LoRA / adapters
        │
        └── preference / reinforcement stage
              ├── correct evidence use
              ├── fail-closed claims
              ├── tool invocation
              └── provenance-aware outputs
```

Do **not** modify the backbone prematurely.

First prove that the external architecture improves reasoning.

Then experiment with deeper lattice integration.

---

## 15. Training data classes

Potential training examples:

```text
NS equation interpretation
boundary-condition reasoning
discretization selection
solver diagnostics
CFL reasoning
vorticity reasoning
dimensional analysis
verification cases
benchmark interpretation
failure analysis
reproducibility classification
receipt interpretation
symbolic derivation
formal invariant reasoning
retrieval provenance
unsupported-claim rejection
lattice construction
lattice traversal
tool-selection traces
```

Particularly valuable examples are those where the correct action is:

```text
INSUFFICIENT_EVIDENCE
RUN_SOLVER
RETRIEVE_SOURCE
VERIFY_FORMALLY
QUALIFY_CLAIM
REJECT_CLAIM
```

rather than merely generating another paragraph.

---

## 16. Memory model

QSOL-LFM effectively uses three separate external memory classes.

### Persistent memory

```text
QSOL_CONTEXT
```

Answers:

```text
Who?
What project?
What contract?
What environment?
What prior decision?
```

### Dynamic evidence memory

```text
RES=RAG
```

Answers:

```text
What information is relevant now?
```

### Structural memory

```text
GEOMETRIC INFORMATION MAPPED LATTICE
```

Answers:

```text
How are these objects related?
```

The model weights remain a fourth form of memory:

```text
learned statistical representation
```

These should not be conflated.

---

## 17. Initial model specification

```yaml
MODEL:
  name: QSOL-LFM-NS
  backbone: LiquidAI/LFM2.5-8B-A1B-Base
  total_parameters: approximately_8.3B
  active_parameters_per_token: approximately_1.5B
  context_window: 128K

CONTEXT:
  persistent: QSOL_CONTEXT
  dynamic: RES_RAG
  structural: GEOMETRIC_INFORMATION_MAPPED_LATTICE

REASONING:
  controller: QSOL_NS_REASONER_V1
  execution:
    - NS_SIM
    - SYMBOLIC_ENGINE
    - LEAN4

VERIFICATION:
  provenance_required: true
  numerical_claims_require_receipts: true
  unsupported_strong_claims: fail_closed

OUTPUT:
  natural_language: true
  structured_claims: true
  provenance: true
  receipts: optional_when_not_applicable
```

---

## 18. Development roadmap

### Phase 0 — specification

- freeze architecture vocabulary;
- define lattice schema;
- define claim classes;
- define output contract;
- define benchmark suite;
- define provenance contract.

### Phase 1 — external orchestration prototype

```text
QSOL_CONTEXT
+
RES=RAG
+
serialized lattice
+
LFM2.5
+
NS-SIM
```

No backbone modification.

Goal:

> prove the architecture is useful before changing the model.

### Phase 2 — fine-tuned NS reasoner

- continued pretraining;
- SFT on NS reasoning;
- lattice serialization training;
- evidence-selection training;
- tool-selection training;
- fail-closed claim training.

### Phase 3 — lattice encoder

Build:

```text
lattice
  ↓
encoder
  ↓
adapter
  ↓
LFM latent state
```

Compare against serialized-lattice baseline.

### Phase 4 — native geometric integration

Experiment with:

- gated lattice state;
- selected-block injection;
- lattice cross-attention;
- recurrent geometric state;
- learned lattice updates.

### Phase 5 — generalized QSOL-LFM

Navier–Stokes becomes one domain profile:

```text
QSOL-LFM
   │
   ├── NS LATTICE
   ├── E8 LATTICE
   ├── RES=RAG LATTICE
   ├── SONIFICATION LATTICE
   └── future domain lattices
```

---

## 19. What QSOL-LFM is not

QSOL-LFM is not intended to claim:

- that an LLM has solved the Navier–Stokes Millennium Prize problem;
- that language-model weights replace numerical simulation;
- that RAG output is automatically factual;
- that formal notation automatically constitutes proof;
- that model self-reports reveal hidden backend state;
- that large context windows are equivalent to reasoning;
- that every scientific claim can be verified by one mechanism.

Different claims require different evidence.

---

## 20. Design principles

```text
STRUCTURE OVER TOKEN DUMPING

PROVENANCE OVER CONFIDENCE

EXECUTION OVER SIMULATED EXECUTION

FORMALIZATION OVER FORMAL-SOUNDING TEXT

SELECTIVE CONTEXT OVER EVERYTHING-EVERYWHERE

GEOMETRIC RELATIONSHIPS OVER FLAT RETRIEVAL

FAIL CLOSED ON STRONG UNSUPPORTED CLAIMS

USE THE LLM AS A REASONER AND CONTROLLER,
NOT AS A REPLACEMENT FOR EVERY OTHER COMPUTATIONAL SYSTEM
```

---

## 21. One-line architecture

```text
QSOL_CONTEXT
    → RES=RAG
    → GEOMETRIC INFORMATION MAPPED LATTICE
    → LFM2.5
    → CUSTOM REASONING
    → NS-SIM / SYMBOLIC / LEAN
    → SCIENTIFIC VERIFIER
    → PROVENANCE-BOUND OUTPUT
```

---

## 22. Long-term direction

The initial problem is Navier–Stokes.

The broader experiment is more ambitious:

> **Can a language model reason more reliably when persistent context, retrieved evidence, geometric structure, executable computation, and formal verification remain separate but interoperable systems?**

If successful, QSOL-LFM would not be merely a domain-fine-tuned language model.

It would be a **geometric scientific reasoning system built around a language model**.
