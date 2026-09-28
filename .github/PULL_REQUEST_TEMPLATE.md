## Pull Request Validation — Rookery Labs

### 1. Specification (SDD Mandatory Reference)
* **Spec ID / Document :** [SPEC-ID](specs/...)
* **Spec Status :** [ ] Draft / Proposal | [ ] Approved Specification

> ⚠️ **SDD Enforcement:** Pull requests introducing application logic without a corresponding specification update in `specs/` will be rejected automatically.

---

### 2. Test-Driven Development (TDD Verification)
- [ ] **Red Phase:** Unit tests reproducing the target behavior/contract were authored and confirmed failing prior to implementation.
- [ ] **Green Phase:** Application code has been implemented and all tests now pass cleanly.
- [ ] **Edge Cases:** Boundary conditions, timeout scenarios, and error states are covered by automated tests.
- [ ] **Local Verification:**
  - [ ] `npm test` passes (for `corvus-dom-extension`)
  - [ ] `cargo test` passes (for `laya-onnx-android`)
  - [ ] `pytest` passes (for `corvus-eval-benchmarks`)
  - [ ] `./gradlew test` passes (for `corvus-android`)

---

### 3. Summary of Changes
Provide a concise overview of changes introduced in this PR:
* 

---

### 4. Architectural & IPC Impact
- [ ] Changes adhere to JSON-RPC 2.0 schema in `specs/jsonrpc-contracts.json` (if applicable)
- [ ] Changes preserve memory constraints (e.g. 60s inactivity TTL for System 2)
- [ ] Changes do not degrade latency budgets (< 40ms for System 1 reflex)

---

### 5. Security & Privacy Audit
- [ ] No telemetry or sensitive user data leaked
- [ ] Contextual Identity tab isolation preserved
- [ ] DOM pruning guarantees removal of sensitive inline scripts and external frames
