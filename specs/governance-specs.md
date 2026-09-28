# Specification: Rookery Labs Ecosystem Governance & Methodological Standards

**Spec ID:** `SPEC-GOV-001`  
**Status:** VALIDATED  
**Scope:** Organization-wide (`rookery-labs/*`)

---

## 1. Spec-Driven Development (SDD) Protocol

1. **Primacy of Specifications:**
   - Every repository must maintain a top-level `specs/` directory.
   - Specifications must define:
     - Functional objectives and domain invariants.
     - Formal state machine transitions (with states, events, guards, and transition actions).
     - Typed interface contracts (JSON Schema for IPC, C/JNI signatures for native bridges, Kotlin/TypeScript types).
2. **Schema-First Inter-Component Communication:**
   - Any communication protocol (notably JSON-RPC 2.0 between GeckoView and WebExtension) must be formalized in `specs/jsonrpc-contracts.json` before writing serialization/deserialization code.
   - Changes to schemas must be backwards-compatible or versioned (`v1`, `v2`).

---

## 2. Test-Driven Development (TDD) Protocol

1. **Red-Green-Refactor Lifecycle:**
   - Step 1: Write an automated test covering the specification interface and edge cases (Red).
   - Step 2: Write minimal implementation code to satisfy the test contract (Green).
   - Step 3: Refactor for performance, memory limits, and clarity while preserving Green status.
2. **Zero Failing Tests Policy:**
   - Pull requests must not merge if any unit or integration test fails.
   - Test suites must be runnable locally without external cloud dependencies.

---

## 3. Cognitive Systems Architecture Invariants

1. **System 1 (Laya Reflex):**
   - Must operate strictly under a 40ms end-to-end inference budget on `arm64-v8a`.
   - Tokenization latency must remain under 1ms.
   - Outputs must be scalar-calibrated via temperature scaling before routing decisions.
2. **System 2 (Deliberate LLM/SLM):**
   - Local on-device SLM execution must enforce a 60-second inactivity TTL.
   - Memory must be freed upon timer expiration (`release_model()`).
   - Remote BYOK APIs must enforce streaming and token cost boundaries.
3. **DOM Security and Privacy:**
   - DOM representations exported by `corvus-dom-extension` must strictly strip scripts, styles, iframes, SVG blobs, and non-accessibility metadata.
