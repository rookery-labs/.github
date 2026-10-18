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

---

## 4. Strict Development Isolation & `main` Branch Sanctuary

1. **Mandatory Dedicated Branches & Worktrees:**
   - All feature developments, bug fixes, or milestones must be implemented in dedicated branches (`feat/<name>`, `fix/<name>`, or `feat/m<id>-<name>`).
   - Isolated Git worktrees (`.worktrees/` or `just worktree-add <repo> <branch>`) are mandatory to ensure complete decoupling from other active tasks.
   - Direct editing, committing, or pushing to `main` is strictly prohibited.
2. **Sanctuary of `main`:**
   - The `main` branch is an inviolable sanctuary that must remain permanently compilable, clean, fully tested, and deployable.
   - Direct push to `main` is strictly forbidden across all repositories.
3. **Strict Merge Gate:**
   - Merging into `main` is permitted ONLY when:
     - Specifications in `specs/` are fully satisfied and updated.
     - 100% of unit and integration test suites pass with zero regressions.
     - Static analysis (Clippy, Ruff, TypeScript compiler, Gradle checks) completes with zero warnings or errors.
     - Pull requests are reviewed and approved.

---

## 5. Automated Renovate Dependency Security & Zero-Touch Releases

1. **Renovate Dependency Security Engine:**
   - Renovate scans all dependencies across tech stacks (npm, Cargo, PyPI, Gradle) on a continuous automated schedule.
   - Vulnerability alerts and patch/minor updates are generated immediately with automated PRs.
2. **Automated Merging Policy (Automerge):**
   - If and only if all automated CI tests and security quality gates pass with zero regressions, Renovate PRs are automatically merged into `main` without requiring human intervention.
   - Major version bumps or breaking changes require formal spec review and manual approval.
3. **Zero-Touch Automated Releases:**
   - Every merge into `main` triggers automated version analysis, semantic tagging (`vX.Y.Z`), changelog generation, and GitHub Release publication.
   - Maximized automated test coverage across all subprojects prevents regression releases.

