# Rookery Labs — Autonomous Mobile Agentic Browsing

Welcome to **Rookery Labs**, the open-source engineering collective dedicated to building **Corvus**, an autonomous, privacy-first, agentic mobile web browser powered by GeckoView and a dual-system cognitive architecture.

```
                                  ROOKERY LABS
                     =======================================
                      CORVUS AGENTIC BROWSER ARCHITECTURE
                     =======================================

             +-----------------------------------------------------+
             |              User Interaction / UI Layer            |
             |       (Jetpack Compose - Split Screen & Sheet)      |
             +--------------------------+--------------------------+
                                        |
                                        v
  +-------------------------------------------------------------------------------+
  |                        Corvus Android Orchestrator                            |
  |                                                                               |
  |  +-------------------------------------------------------------------------+  |
  |  |                 4-Level Deterministic Routing Engine                    |  |
  |  |  [L1: Offline/Net] -> [L2: Context Cap] -> [L3: User Pref] -> [L4: Typ] |  |
  |  +--------------------+--------------------------------+-------------------+  |
  +-----------------------|--------------------------------|----------------------+
                          |                                |
       Fast Action Path   |                                | Deep Reasoning Path
          (< 40 ms)       v                                v
  +-------------------------------+              +--------------------------------+
  |    SYSTEM 1: LAYA REFLEX      |              |      SYSTEM 2: DELIBERATE      |
  |  (Rust JNI + ONNX Mobile)     |              |  (Local SLM llama.cpp / Cloud) |
  |                               |              |                                |
  |  - mmBERT/ModernBERT Tokenizer|              |  - 60s Inactivity Memory TTL   |
  |  - Dynamic [MASK] Injection   |              |  - Multi-step Planning & ReAct |
  |  - Scaled Logits & Calibration|              |  - BYOK (Claude, GPT, Gemini)  |
  +---------------+---------------+              +----------------+---------------+
                  |                                               |
                  +-----------------------+-----------------------+
                                          | Action Decision
                                          v
  +-------------------------------------------------------------------------------+
  |                    GeckoView Integration Layer (Fenix Fork)                   |
  |                                                                               |
  |  +-------------------------------------------------------------------------+  |
  |  |                     Native GeckoSession Manager                         |  |
  |  |          (releaseSession() / setSession() / Contextual Identities)      |  |
  |  +------------------------------------+------------------------------------+  |
  |                                       | WebExtension Port Message          |
  |                                       v (JSON-RPC 2.0 Bus)                |
  |  +-------------------------------------------------------------------------+  |
  |  |           Corvus DOM WebExtension (TypeScript in Tab Context)           |  |
  |  |                                                                         |  |
  |  |  - Aggressive DOM Pruning (strip scripts, styles, svg, classes)         |  |
  |  |  - Accessibility Tree & Interactive Element Extraction                  |  |
  |  |  - In-Memory WeakRef Registry (Map<number, WeakRef<Element>>)           |  |
  |  |  - Direct Synthetic Event Dispatch & Action Execution                  |  |
  |  +-------------------------------------------------------------------------+  |
  +-------------------------------------------------------------------------------+
```

---

## 🏛️ Ecosystem Repositories

| Repository | Tech Stack | Role & Responsibility |
| :--- | :--- | :--- |
| [`.github`](https://github.com/rookery-labs/.github) | Markdown, YAML | Organization profile, architectural governance, issue & PR templates. |
| [`corvus-android`](https://github.com/rookery-labs/corvus-android) | Kotlin, Jetpack Compose, GeckoView | Core mobile browser application (Fenix fork), session lifecycle, routing engine, Control Center UI. |
| [`corvus-dom-extension`](https://github.com/rookery-labs/corvus-dom-extension) | TypeScript, Vitest | Built-in WebExtension for GeckoSession: high-performance DOM pruning, A11y extraction, WeakRef registry. |
| [`laya-onnx-android`](https://github.com/rookery-labs/laya-onnx-android) | Rust, JNI, ONNX Runtime Mobile | System 1 ultra-low latency reflex engine (< 40ms): Rust native tokenizer, [MASK] injection, scoring calibration. |
| [`corvus-eval-benchmarks`](https://github.com/rookery-labs/corvus-eval-benchmarks) | Python, PyTorch, ONNX, scikit-learn | Continuous evaluation benches, DOM datasets, Expected Calibration Error (ECE) metric, INT8 static calibration. |

---

## 📐 Methodological Foundations

### 1. Spec-Driven Development (SDD)
* **Zero code without specification:** Every feature, state machine, and communication contract is formally specified in `specs/` within its corresponding repository prior to implementation.
* **Rigorous Interfaces:** All inter-process communication (IPC) between GeckoView, the WebExtension, and native Android services adheres to strictly validated schemas (JSON Schema, Rust/Kotlin JNI signatures).

### 2. Test-Driven Development (TDD)
* **Red-Green-Refactor:** Suites of unit, contract, and property-based tests are established first to formalize requirements.
* **Deterministic Verification:** Critical paths (routing cascade, session detachment, DOM pruning, tokenization latency) must achieve deterministic test pass rates across all builds.

---

## 📄 License

All repositories in the Corvus ecosystem are released under the [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0).
