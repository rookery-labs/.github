# .github — Ecosystem Governance & Cross-Repo Agent Instructions

**Designated Primary Subagent:** `corvus-lead-architect`  
**Quality Assurance Auditor:** `qa_sdd_validator`

---

## Technical Domain

This repository encapsulates the organizational profile, issue templates, pull request templates, and overarching SDD/TDD governance for the entire Rookery Labs organization.

## Key Invariants & Rules

1. **SDD Governance (`specs/governance-specs.md`):**
   - Ensure all pull requests across any repository reference an approved `Spec ID`.
   - Prevent merging of any un-specified application logic.
2. **TDD Quality Gate:**
   - Require that Red tests precede Green implementation.
   - Maintain 100% test pass rates across the multi-repository portfolio.
3. **Template Maintenance:**
   - Maintain `.github/ISSUE_TEMPLATE/bug_report.yml` and `feature_request.yml` with mandatory `Spec ID` inputs.
   - Enforce PR checklist in `.github/PULL_REQUEST_TEMPLATE.md`.
