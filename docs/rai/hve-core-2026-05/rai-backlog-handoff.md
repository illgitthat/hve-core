---
title: "RAI Backlog Handoff - HVE Core (May 2026)"
description: "Twenty-item Responsible AI backlog for HVE Core, framed against the NIST AI Risk Management Framework 1.0 trustworthiness characteristics."
author: HVE Core RAI Reviewers
ms.date: 2026-05-14
ms.topic: reference
keywords:
  - responsible-ai
  - rai
  - nist-ai-rmf
  - backlog
  - hve-core
estimated_reading_time: 25
---

GitHub-format backlog (twenty items). Temporary IDs `{{RAI-TEMP-N}}` are placeholders to be replaced with real GitHub issue numbers if and when individual issues are filed; the umbrella issue accompanying this PR proposes that maintainer triage decide which items become individual issues. Cross-Reference column intentionally empty (no Security Plan exists; a separate group will run that assessment).

Sanitization applied: internal tracking paths replaced with descriptive references; standards references (NIST AI RMF) preserved.

## Work Item Summary

| Category               | Count  | Immediate | Near-term | Planned | Backlog |
|------------------------|--------|-----------|-----------|---------|---------|
| Remediation            | 4      | 1         | 3         | 0       | 0       |
| Control Implementation | 7      | 1         | 5         | 1       | 0       |
| Monitoring Setup       | 1      | 0         | 0         | 1       | 0       |
| Documentation          | 8      | 3         | 2         | 3       | 0       |
| Enhancement            | 0      | 0         | 0         | 0       | 0       |
| **Total**              | **20** | **5**     | **10**    | **5**   | **0**   |

## Suggested Remediation Horizon Breakdown

| Horizon            | Count | Key Items                                                                                                                |
|--------------------|-------|--------------------------------------------------------------------------------------------------------------------------|
| Pre-Production     | 10    | Public claims audit, Transparency Note, AI-disclosure marker, Customer Card Render redaction, persona stereotyping audit |
| Early Operations   | 4     | Multi-agent audit trail, telemetry / drift / re-assessment cadence, memory-layer retention, gitleaks in cloud agent CI   |
| Ongoing Governance | 6     | Customer-handoff governance, accessibility audit, language coverage, evaluation cohort diversity, agent discoverability  |

## Security Planner Cross-References

No Security Plan exists for HVE Core. A separate group will run that assessment independently. This table will be populated during a future cross-reference pass once the Security Plan completes.

| RAI Item | Security Item | Relationship |
|----------|---------------|--------------|
| -        | -             | -            |

## Outstanding Tradeoffs

* TO-100 - Velocity vs Accountable-and-Transparent: rapid agent iteration vs the need for a Transparency Note and per-agent capability statements before customer redistribution.
* TO-101 - Lo-fi prototyping vs stakeholder buy-in: deliberately rough fidelity may underperform stakeholder expectations of polish in customer-handoff settings.
* TO-102 - Customer-handoff reach vs audit trail: the customer-handoff channel is the most opaque of six channels; broader reach increases governance debt.
* TO-103 - Memory persistence vs Privacy-Enhanced: persistent memory layers improve agent continuity but increase data-retention surface for participant content.

## Next Steps

1. Maintainer triage of the 20 work items and their suggested priorities, horizons, and tags. The umbrella issue accompanying this PR proposes that maintainers decide which items become individual tracker issues; the templates below are pre-formatted for direct conversion.
2. On adoption, RAI Owner assignment during backlog refinement (default "TBD").
3. When individual issues are filed, replace `{{RAI-TEMP-N}}` placeholders with real GitHub issue numbers.
4. Cross-reference pass once the separate Security Plan completes.

---

## Work Items

### {{RAI-TEMP-1}} - Audit public-materials safety and fitness claims

```yaml
---
rai_characteristic: Accountable and Transparent
threat_id: T-RAI-012
suggested_priority: Immediate
suggested_horizon: Pre-Production
category: Remediation
depth_tier: Comprehensive
security_cross_ref: ""
---
```

**Title:** `[RAI-Accountable-and-Transparent] Audit public-materials safety and fitness claims`

**Labels:** `accountable-transparent`, `valid-reliable`

**Body:**

```markdown
## RAI Control: Public-claims fitness and safety audit

**NIST Characteristic:** Accountable and Transparent
**Threat:** T-RAI-012 - Public-facing materials assert fitness or safety beyond what the static repository can verify
**Control Surface:** Prevent - content review of README, docs, marketing copy
**Suggested Priority:** Immediate
**Suggested Remediation Horizon:** Pre-Production

### Implementation

Inventory all public-facing materials (README, docs site, marketing copy, extension descriptions, plugin manifests). For each safety, fitness, accuracy, or capability claim, verify whether the claim is supported by what the repository ships versus what downstream agents do at runtime. Rewrite or remove unsupported claims. Add a "What HVE Core does and does not do" section to top-level documentation.

### Acceptance Criteria

* [ ] Inventory of public-facing materials with each claim categorized as supported, scope-restricted, or unsupported
* [ ] Unsupported claims removed or rewritten
* [ ] Top-level documentation includes a "What HVE Core does and does not do" section
* [ ] Review by RAI reviewer documented

*Note: AI-assisted content. Review and validate before use.*
```

---

### {{RAI-TEMP-2}} - Author HVE Core Transparency Note

```yaml
---
rai_characteristic: Accountable and Transparent
threat_id: T-RAI-009
suggested_priority: Immediate
suggested_horizon: Pre-Production
category: Documentation
depth_tier: Comprehensive
security_cross_ref: ""
---
```

**Title:** `[RAI-Accountable-and-Transparent] Author HVE Core Transparency Note`

**Labels:** `accountable-transparent`

**Body:**

```markdown
## RAI Control: HVE Core Transparency Note

**NIST Characteristic:** Accountable and Transparent
**Threat:** T-RAI-009 - Users cannot tell what the system does, what it does not do, and where it can fail
**Control Surface:** Prevent - published Transparency Note
**Suggested Priority:** Immediate
**Suggested Remediation Horizon:** Pre-Production

### Implementation

Author a Transparency Note for HVE Core covering system purpose, capabilities, limitations, data usage (none at runtime within repository scope; downstream model usage delegated to host platform), decision process (artifacts instruct downstream models; no inference inside repository), human oversight (artifacts are advisory), and contact and feedback. Use the outline below as a starting point. Include the Phase 2 dimension revisit conclusion (att 0.50, data 0.80, explain 0.60; baseline kept) as part of the limitations section.

### Acceptance Criteria

* [ ] Transparency Note covers all sections in the outline
* [ ] Phase 2 dimension revisit conclusion documented in limitations
* [ ] Reviewed by RAI reviewer
* [ ] Published in a discoverable location

*Note: AI-assisted content. Review and validate before use.*
```

---

### {{RAI-TEMP-3}} - Add per-agent capability and limitation statements

```yaml
---
rai_characteristic: Accountable and Transparent
threat_id: T-RAI-009
suggested_priority: Immediate
suggested_horizon: Pre-Production
category: Documentation
depth_tier: Comprehensive
security_cross_ref: ""
---
```

**Title:** `[RAI-Accountable-and-Transparent] Add per-agent capability and limitation statements`

**Labels:** `accountable-transparent`, `explainable-interpretable`

**Body:**

```markdown
## RAI Control: Per-agent capability and limitation statements

**NIST Characteristic:** Accountable and Transparent
**Threat:** T-RAI-009 - Users cannot tell what each agent does and where it can fail
**Control Surface:** Prevent - frontmatter and rendered docs
**Suggested Priority:** Immediate
**Suggested Remediation Horizon:** Pre-Production

### Implementation

For each custom agent shipped in this repository, add a capability statement (what the agent does), a limitation statement (what it does not do), and an intended-use statement (in-scope usage contexts). Render the statements in agent frontmatter and in the corresponding agent docs. Add a validation script to the lint suite to flag agents missing the statements.

### Acceptance Criteria

* [ ] Every custom agent has capability, limitation, and intended-use statements
* [ ] Statements rendered in both frontmatter and rendered docs
* [ ] Validation script added to lint suite

*Note: AI-assisted content. Review and validate before use.*
```

---

### {{RAI-TEMP-4}} - Adopt Microsoft Privacy, SDL, Accessibility standards

```yaml
---
rai_characteristic: Privacy-Enhanced
threat_id: T-RAI-002
suggested_priority: Near-term
suggested_horizon: Pre-Production
category: Remediation
depth_tier: Comprehensive
security_cross_ref: ""
---
```

**Title:** `[RAI-Privacy-Enhanced] Declare adoption of Microsoft Privacy Standard, SDL, Accessibility Standards, and AI Code of Conduct`

**Labels:** `privacy-enhanced`, `secure-resilient`, `fair-bias-managed`, `accountable-transparent`

**Body:**

```markdown
## RAI Control: Microsoft standards adoption declaration

**NIST Characteristic:** Privacy-Enhanced, Secure and Resilient, Fair with Harmful Bias Managed, Accountable and Transparent
**Threat:** T-RAI-002, T-RAI-003 - Privacy and Code of Conduct standards adoption status undocumented
**Control Surface:** Prevent - published adoption declarations and conformance evidence
**Suggested Priority:** Near-term
**Suggested Remediation Horizon:** Pre-Production

### Implementation

Document the repository's adoption status against Microsoft Privacy Standard, SDL, Microsoft Accessibility Standards, and Microsoft AI Code of Conduct. For each standard, list the relevant practices the repository follows, gaps to close, and ownership. Publish the declaration in a discoverable location. Treat this as the umbrella item; sub-issues may be opened per standard during refinement.

### Acceptance Criteria

* [ ] Each of the four standards has an adoption status entry
* [ ] Gaps and ownership documented per standard
* [ ] Declaration published in a discoverable location
* [ ] Sub-issues opened for any standard requiring substantive remediation

*Note: AI-assisted content. Review and validate before use.*
```

---

### {{RAI-TEMP-5}} - Author per-agent Impact Assessments

```yaml
---
rai_characteristic: Accountable and Transparent
threat_id: T-RAI-007
suggested_priority: Near-term
suggested_horizon: Pre-Production
category: Documentation
depth_tier: Comprehensive
security_cross_ref: ""
---
```

**Title:** `[RAI-Accountable-and-Transparent] Author per-agent Impact Assessments for governance-bearing agents`

**Labels:** `accountable-transparent`

**Body:**

```markdown
## RAI Control: Per-agent Impact Assessments

**NIST Characteristic:** Accountable and Transparent
**Threat:** T-RAI-007 - Governance-bearing agents shipped without an Impact Assessment record
**Control Surface:** Prevent - IA artifact per agent
**Suggested Priority:** Near-term
**Suggested Remediation Horizon:** Pre-Production

### Implementation

Identify governance-bearing agents (Security Planner, RAI Planner, SSSC Planner, Pull Request agents, code-review agents). For each, author a per-agent Impact Assessment covering intended use, fitness assessment, stakeholder impact, mitigations, and residual risks. Apply a structured Impact Assessment template.

### Acceptance Criteria

* [ ] List of governance-bearing agents documented
* [ ] IA authored for each
* [ ] IAs reviewed by RAI reviewer
* [ ] IAs published with the agent docs

*Note: AI-assisted content. Review and validate before use.*
```

---

### {{RAI-TEMP-6}} - Build multi-agent orchestration audit trail

```yaml
---
rai_characteristic: Accountable and Transparent
threat_id: T-RAI-004
suggested_priority: Near-term
suggested_horizon: Early Operations
category: Control Implementation
depth_tier: Comprehensive
security_cross_ref: ""
---
```

**Title:** `[RAI-Accountable-and-Transparent] Build multi-agent orchestration audit trail`

**Labels:** `accountable-transparent`

**Body:**

```markdown
## RAI Control: Multi-agent orchestration audit trail

**NIST Characteristic:** Accountable and Transparent
**Threat:** T-RAI-004 - Subagent dispatch and result merging not exportable in a structured audit format
**Control Surface:** Detect - structured trace export
**Suggested Priority:** Near-term
**Suggested Remediation Horizon:** Early Operations

### Implementation

Define a structured audit trace schema for parent-agent and subagent execution: invoking agent, invoked agent, inputs, outputs, decision points, and timing. Export traces from session logs into the schema. Provide a CLI to query traces by session, agent, or decision class.

### Acceptance Criteria

* [ ] Audit trace schema defined and documented
* [ ] Exporter implemented for session logs
* [ ] Query CLI available
* [ ] Sample trace export validated against schema

*Note: AI-assisted content. Review and validate before use.*
```

---

### {{RAI-TEMP-7}} - Enforce AI-disclosure marker on agent-produced artifacts

```yaml
---
rai_characteristic: Accountable and Transparent
threat_id: T-RAI-009
suggested_priority: Immediate
suggested_horizon: Pre-Production
category: Control Implementation
depth_tier: Comprehensive
security_cross_ref: ""
---
```

**Title:** `[RAI-Accountable-and-Transparent] Enforce AI-disclosure marker on agent-produced artifacts`

**Labels:** `accountable-transparent`

**Body:**

```markdown
## RAI Control: AI-disclosure marker enforcement

**NIST Characteristic:** Accountable and Transparent
**Threat:** T-RAI-009 - AI-disclosure marker inconsistent across agent-produced artifacts
**Control Surface:** Prevent and Detect - template enforcement and lint check
**Suggested Priority:** Immediate
**Suggested Remediation Horizon:** Pre-Production

### Implementation

Standardize the AI-disclosure footer across all agent-produced artifact templates. Add a lint check to the validation suite that flags agent-produced artifacts missing the footer. Update agent prompts to require the footer.

### Acceptance Criteria

* [ ] Standard AI-disclosure footer defined
* [ ] All agent-produced artifact templates updated
* [ ] Lint check added to validation suite
* [ ] Agent prompts updated to require the footer

*Note: AI-assisted content. Review and validate before use.*
```

---

### {{RAI-TEMP-8}} - Establish customer-handoff governance

```yaml
---
rai_characteristic: Accountable and Transparent
threat_id: T-RAI-013
suggested_priority: Near-term
suggested_horizon: Ongoing Governance
category: Documentation
depth_tier: Comprehensive
security_cross_ref: ""
---
```

**Title:** `[RAI-Accountable-and-Transparent] Establish customer-handoff governance`

**Labels:** `accountable-transparent`

**Body:**

```markdown
## RAI Control: Customer-handoff governance

**NIST Characteristic:** Accountable and Transparent
**Threat:** T-RAI-013 - Customer-handoff is the most opaque distribution channel; downstream usage cannot be observed
**Control Surface:** Respond - handoff documentation, scope-of-use, and acknowledgment
**Suggested Priority:** Near-term
**Suggested Remediation Horizon:** Ongoing Governance

### Implementation

Define a customer-handoff governance pack: scope-of-use document, customer-side acknowledgment template, redaction checklist for engagement-specific content, and re-engagement cadence. Require sign-off before handoff.

### Acceptance Criteria

* [ ] Scope-of-use document drafted
* [ ] Customer-side acknowledgment template drafted
* [ ] Redaction checklist drafted
* [ ] Sign-off process defined and adopted

*Note: AI-assisted content. Review and validate before use.*
```

---

### {{RAI-TEMP-9}} - Production telemetry, drift detection, and re-assessment cadence

```yaml
---
rai_characteristic: Valid and Reliable
threat_id: T-RAI-005
suggested_priority: Planned
suggested_horizon: Early Operations
category: Monitoring Setup
depth_tier: Comprehensive
security_cross_ref: ""
---
```

**Title:** `[RAI-Valid-and-Reliable] Set up production telemetry, drift detection, and RAI re-assessment cadence`

**Labels:** `valid-reliable`, `accountable-transparent`

**Body:**

```markdown
## RAI Control: Production telemetry and re-assessment cadence

**NIST Characteristic:** Valid and Reliable
**Threat:** T-RAI-005 - Drift in agent behavior over time not detectable
**Control Surface:** Detect - telemetry, drift signals, scheduled re-assessment
**Suggested Priority:** Planned
**Suggested Remediation Horizon:** Early Operations

### Implementation

Define telemetry signals appropriate for a static-artifact repository (extension install counts, agent invocation telemetry where available from host platform, issue and bug rates by agent). Define drift indicators (regression in agent quality, change in issue mix). Schedule a recurring RAI re-assessment cadence (suggested annually or on major release).

### Acceptance Criteria

* [ ] Telemetry signals defined and instrumented where feasible
* [ ] Drift indicators documented
* [ ] Re-assessment cadence published

*Note: AI-assisted content. Review and validate before use.*
```

---

### {{RAI-TEMP-10}} - Document language and code-language coverage

```yaml
---
rai_characteristic: Fair with Harmful Bias Managed
threat_id: T-RAI-010
suggested_priority: Planned
suggested_horizon: Ongoing Governance
category: Documentation
depth_tier: Comprehensive
security_cross_ref: ""
---
```

**Title:** `[RAI-Fair-with-Harmful-Bias-Managed] Document language and code-language coverage`

**Labels:** `fair-bias-managed`

**Body:**

```markdown
## RAI Control: Language and code-language coverage statement

**NIST Characteristic:** Fair with Harmful Bias Managed
**Threat:** T-RAI-010 - Language and code-language coverage skewed; inequitable utility for non-English natural-language users and for less-common programming-language users
**Control Surface:** Prevent - explicit coverage statement
**Suggested Priority:** Planned
**Suggested Remediation Horizon:** Ongoing Governance

### Implementation

Catalog which natural languages and which programming languages each agent supports well, partially, or not at all. Publish the matrix. Create issues for high-leverage gaps to triage.

### Acceptance Criteria

* [ ] Coverage matrix published
* [ ] Gap-triage issues opened

*Note: AI-assisted content. Review and validate before use.*
```

---

### {{RAI-TEMP-11}} - Run persona stereotyping audit

```yaml
---
rai_characteristic: Fair with Harmful Bias Managed
threat_id: T-RAI-011
suggested_priority: Near-term
suggested_horizon: Pre-Production
category: Remediation
depth_tier: Comprehensive
security_cross_ref: ""
---
```

**Title:** `[RAI-Fair-with-Harmful-Bias-Managed] Run persona stereotyping audit`

**Labels:** `fair-bias-managed`

**Body:**

```markdown
## RAI Control: Persona stereotyping audit

**NIST Characteristic:** Fair with Harmful Bias Managed
**Threat:** T-RAI-011 - Persona templates and example stakeholders may reinforce stereotypes
**Control Surface:** Prevent - content audit
**Suggested Priority:** Near-term
**Suggested Remediation Horizon:** Pre-Production

### Implementation

Audit all persona templates, example stakeholders, customer-card templates, and Design Thinking reference scenarios for stereotyping. Apply a structured rubric. Rewrite or remove flagged content. Add stereotyping review to the contribution checklist.

### Acceptance Criteria

* [ ] Audit rubric defined and applied
* [ ] Flagged content rewritten or removed
* [ ] Stereotyping review added to contribution checklist

*Note: AI-assisted content. Review and validate before use.*
```

---

### {{RAI-TEMP-12}} - Run accessibility audit

```yaml
---
rai_characteristic: Fair with Harmful Bias Managed
threat_id: T-RAI-014
suggested_priority: Planned
suggested_horizon: Ongoing Governance
category: Remediation
depth_tier: Comprehensive
security_cross_ref: ""
---
```

**Title:** `[RAI-Fair-with-Harmful-Bias-Managed] Run accessibility audit`

**Labels:** `fair-bias-managed`

**Body:**

```markdown
## RAI Control: Accessibility audit

**NIST Characteristic:** Fair with Harmful Bias Managed
**Threat:** T-RAI-014 - Accessibility of generated artifacts and docs not validated against Microsoft Accessibility Standards
**Control Surface:** Prevent and Detect - accessibility checks
**Suggested Priority:** Planned
**Suggested Remediation Horizon:** Ongoing Governance

### Implementation

Audit docs site, agent-produced templates, and PowerPoint outputs against Microsoft Accessibility Standards (color contrast, alt text, structural headings, screen-reader compatibility). Add automated accessibility checks where feasible. Remediate flagged issues.

### Acceptance Criteria

* [ ] Audit completed against Microsoft Accessibility Standards
* [ ] Automated checks integrated into CI where feasible
* [ ] Remediation tracked

*Note: AI-assisted content. Review and validate before use.*
```

---

### {{RAI-TEMP-13}} - Diversify evaluation cohorts

```yaml
---
rai_characteristic: Fair with Harmful Bias Managed
threat_id: T-RAI-015
suggested_priority: Planned
suggested_horizon: Ongoing Governance
category: Documentation
depth_tier: Comprehensive
security_cross_ref: ""
---
```

**Title:** `[RAI-Fair-with-Harmful-Bias-Managed] Diversify evaluation cohorts`

**Labels:** `fair-bias-managed`, `valid-reliable`

**Body:**

```markdown
## RAI Control: Evaluation cohort diversification

**NIST Characteristic:** Fair with Harmful Bias Managed, Valid and Reliable
**Threat:** T-RAI-015 - Evaluation cohorts skewed toward authors of the artifacts; downstream user populations underrepresented
**Control Surface:** Prevent - diversified evaluation roster
**Suggested Priority:** Planned
**Suggested Remediation Horizon:** Ongoing Governance

### Implementation

Define evaluation roles and the diversity dimensions that matter for HVE Core (engineering function, role seniority, Microsoft tenure, customer-engagement experience, geographic distribution, native language). Recruit reviewers across the dimensions. Capture demographic-distribution metadata about the reviewer pool without capturing PII.

### Acceptance Criteria

* [ ] Diversity dimensions defined
* [ ] Reviewer pool recruited across dimensions
* [ ] Reviewer-pool composition documented

*Note: AI-assisted content. Review and validate before use.*
```

---

### {{RAI-TEMP-14}} - Specify memory-layer retention, consent, and redaction

```yaml
---
rai_characteristic: Privacy-Enhanced
threat_id: T-RAI-002
suggested_priority: Near-term
suggested_horizon: Early Operations
category: Control Implementation
depth_tier: Comprehensive
security_cross_ref: ""
---
```

**Title:** `[RAI-Privacy-Enhanced] Specify memory-layer retention, consent, and redaction`

**Labels:** `privacy-enhanced`

**Body:**

```markdown
## RAI Control: Memory-layer retention, consent, and redaction

**NIST Characteristic:** Privacy-Enhanced
**Threat:** T-RAI-002, T-RAI-003 - User-memory and session-memory layers persist content across conversations without explicit retention or consent declarations
**Control Surface:** Prevent and Respond - retention spec, consent, redaction CLI
**Suggested Priority:** Near-term
**Suggested Remediation Horizon:** Early Operations

### Implementation

Specify retention windows for user memory, session memory, and repository memory. Specify consent posture (default opt-in, opt-out, or no-write) per layer. Provide a redaction CLI that removes content from memory by pattern or scope. Document the spec in the contributor docs.

### Acceptance Criteria

* [ ] Retention spec published per memory layer
* [ ] Consent posture documented
* [ ] Redaction CLI implemented and tested
* [ ] Documentation updated

*Note: AI-assisted content. Review and validate before use.*
```

---

### {{RAI-TEMP-15}} - Publish sensitive customer data handling guidance

```yaml
---
rai_characteristic: Privacy-Enhanced
threat_id: T-RAI-003
suggested_priority: Near-term
suggested_horizon: Ongoing Governance
category: Documentation
depth_tier: Comprehensive
security_cross_ref: ""
---
```

**Title:** `[RAI-Privacy-Enhanced] Publish sensitive customer data handling guidance`

**Labels:** `privacy-enhanced`, `accountable-transparent`

**Body:**

```markdown
## RAI Control: Sensitive customer data handling guidance

**NIST Characteristic:** Privacy-Enhanced
**Threat:** T-RAI-003 - Customer-engagement workflows may pass sensitive data through agents without redaction guidance
**Control Surface:** Prevent - published handling guidance
**Suggested Priority:** Near-term
**Suggested Remediation Horizon:** Ongoing Governance

### Implementation

Author handling guidance covering what counts as sensitive customer data in HVE Core workflows (PII, financial data, health data, security secrets, NDA-restricted content), what users must redact before sending to agents, what the agents will store across the memory layers, and how to request deletion. Cross-link to the Microsoft Privacy Standard adoption declaration.

### Acceptance Criteria

* [ ] Handling guidance published
* [ ] Cross-link to Privacy Standard adoption added
* [ ] Reviewed by RAI reviewer

*Note: AI-assisted content. Review and validate before use.*
```

---

### {{RAI-TEMP-16}} - Customer Card Render redaction and stereotyping review

```yaml
---
rai_characteristic: Privacy-Enhanced
threat_id: T-RAI-008
suggested_priority: Immediate
suggested_horizon: Pre-Production
category: Control Implementation
depth_tier: Comprehensive
security_cross_ref: ""
---
```

**Title:** `[RAI-Privacy-Enhanced] Add Customer Card Render redaction step and persona-template stereotyping review`

**Labels:** `privacy-enhanced`, `fair-bias-managed`

**Body:**

```markdown
## RAI Control: Customer Card Render redaction and stereotyping review

**NIST Characteristic:** Privacy-Enhanced, Fair with Harmful Bias Managed
**Threat:** T-RAI-008..011 - Customer Card Render is the only direct generative-AI touchpoint and lacks an explicit redaction step and stereotyping review
**Control Surface:** Prevent - redaction step and review gate
**Suggested Priority:** Immediate
**Suggested Remediation Horizon:** Pre-Production

### Implementation

Customer Card Render is the only direct generative-AI touchpoint in HVE Core and is the only direct generative-AI touchpoint. Add a mandatory redaction step before image generation. Add a persona-template stereotyping review against the rubric from RAI-TEMP-11. Add a human-review gate before any customer-facing distribution of rendered cards.

### Acceptance Criteria

* [ ] Redaction step implemented and required
* [ ] Persona-template stereotyping review applied
* [ ] Human-review gate enforced before customer distribution
* [ ] Reviewed by RAI reviewer

*Note: AI-assisted content. Review and validate before use.*
```

---

### {{RAI-TEMP-17}} - Add instruction-content prompt-injection lint

```yaml
---
rai_characteristic: Valid and Reliable
threat_id: T-RAI-001
suggested_priority: Near-term
suggested_horizon: Pre-Production
category: Control Implementation
depth_tier: Comprehensive
security_cross_ref: ""
---
```

**Title:** `[RAI-Valid-and-Reliable] Add instruction-content prompt-injection lint`

**Labels:** `valid-reliable`

**Body:**

```markdown
## RAI Control: Instruction-content prompt-injection lint

**NIST Characteristic:** Valid and Reliable
**Threat:** T-RAI-001 - Instruction content may inadvertently contain prompt-injection patterns that downstream models would execute
**Control Surface:** Prevent - lint check on instruction content
**Suggested Priority:** Near-term
**Suggested Remediation Horizon:** Pre-Production

### Implementation

Add a lint check that scans instruction files, prompt files, and agent files for known prompt-injection patterns (instruction overrides, role-reset patterns, tool-misuse patterns). Run in CI. Fail builds on detection or surface as warnings depending on severity.

### Acceptance Criteria

* [ ] Pattern set defined and reviewed
* [ ] Lint check implemented
* [ ] Wired into CI
* [ ] Documented in contributor guide

*Note: AI-assisted content. Review and validate before use.*
```

---

### {{RAI-TEMP-18}} - Add AI-authored workflow review gate

```yaml
---
rai_characteristic: Valid and Reliable
threat_id: T-RAI-006
suggested_priority: Near-term
suggested_horizon: Pre-Production
category: Control Implementation
depth_tier: Comprehensive
security_cross_ref: ""
---
```

**Title:** `[RAI-Valid-and-Reliable] Add AI-authored workflow review gate`

**Labels:** `valid-reliable`, `accountable-transparent`

**Body:**

```markdown
## RAI Control: AI-authored workflow review gate

**NIST Characteristic:** Valid and Reliable, Accountable and Transparent
**Threat:** T-RAI-006 - Workflow files authored by AI agents may contain logic errors, security gaps, or unsafe defaults
**Control Surface:** Prevent - required human review on AI-authored workflows
**Suggested Priority:** Near-term
**Suggested Remediation Horizon:** Pre-Production

### Implementation

Establish a CODEOWNERS rule and PR-template requirement that AI-authored workflow files (under .github/workflows) require explicit human review by a designated owner before merge. Mark AI-authored PRs in the PR template. Document the rule in the contributor guide.

### Acceptance Criteria

* [ ] CODEOWNERS rule in place for workflow files
* [ ] PR template flag for AI-authored PRs
* [ ] Documented in contributor guide

*Note: AI-assisted content. Review and validate before use.*
```

---

### {{RAI-TEMP-19}} - Lift gitleaks into cloud agent CI

```yaml
---
rai_characteristic: Privacy-Enhanced
threat_id: T-RAI-002
suggested_priority: Planned
suggested_horizon: Early Operations
category: Control Implementation
depth_tier: Comprehensive
security_cross_ref: ""
---
```

**Title:** `[RAI-Privacy-Enhanced] Lift gitleaks into cloud agent CI`

**Labels:** `privacy-enhanced`, `secure-resilient`

**Body:**

```markdown
## RAI Control: gitleaks in cloud agent CI

**NIST Characteristic:** Privacy-Enhanced
**Threat:** T-RAI-002 - Secrets accidentally committed by agents in the cloud agent environment would not be detected at commit time
**Control Surface:** Detect - gitleaks scan in CI
**Suggested Priority:** Planned
**Suggested Remediation Horizon:** Early Operations

### Implementation

gitleaks runs in the devcontainer but is not present in the cloud Copilot agent CI. Add gitleaks to the cloud agent CI workflow with sensible defaults. Document the addition.

### Acceptance Criteria

* [ ] gitleaks added to cloud agent CI workflow
* [ ] Documentation updated

*Note: AI-assisted content. Review and validate before use.*
```

---

### {{RAI-TEMP-20}} - Promote agent discoverability into user-facing docs

```yaml
---
rai_characteristic: Fair with Harmful Bias Managed
threat_id: T-RAI-010
suggested_priority: Near-term
suggested_horizon: Ongoing Governance
category: Documentation
depth_tier: Comprehensive
security_cross_ref: ""
---
```

**Title:** `[RAI-Fair-with-Harmful-Bias-Managed] Promote agent discoverability into user-facing docs`

**Labels:** `fair-bias-managed`, `accountable-transparent`

**Body:**

```markdown
## RAI Control: Agent discoverability promotion

**NIST Characteristic:** Fair with Harmful Bias Managed
**Threat:** T-RAI-010 - Some agents are well-promoted, others are buried; discoverability inequality leads to inequitable utility
**Control Surface:** Prevent - discoverability index in user-facing docs
**Suggested Priority:** Near-term
**Suggested Remediation Horizon:** Ongoing Governance

### Implementation

Promote the discoverability conventions from contributor docs into user-facing documentation. Provide a top-level agent index covering all shipped agents with the same depth of description.

### Acceptance Criteria

* [ ] Top-level agent index published
* [ ] Each agent reaches the same minimum description depth
* [ ] Linked from main entry points

*Note: AI-assisted content. Review and validate before use.*
```

---

---

## Transparency Note Outline (Draft)

### System Purpose

HVE Core is a Microsoft repository that distributes prompt-engineering scaffolding (custom agents, prompts, instructions, skills, collections, and a VS Code extension) so engineering teams can build AI-assisted workflows on top of GitHub Copilot Chat, Visual Studio Code, and Microsoft Foundry models.
The system targets Microsoft engineers, ISE field teams, customer engineering teams, and downstream community contributors who want a curated, governance-aware starting point for AI-assisted software work.

### Capabilities

HVE Core ships planning agents (Security, RAI, SSSC), code-review agents, backlog-management agents, design-thinking facilitation agents, experimental media-generation skills (PowerPoint, voice-over, video-to-GIF), and language-specific coding-standards instructions.
Capabilities are described per-agent in the agents directory and per-skill in SKILL.md files.
Capability documentation should be aligned per RAI-TEMP-3 (Capabilities subsection) and per-agent Transparency Notes per RAI-TEMP-2 (Transparency Note authoring).

### Limitations

The Customer Card Render skill produces marketing-style customer slides and was flagged for redaction-step gaps and persona stereotyping concerns; mitigation is tracked in RAI-TEMP-16. AI-authored workflow files were called out for needing a human review gate before merge (RAI-TEMP-18). Generated content carries the standard "Note: Reviewed and validated by a qualified human reviewer" footer per RAI-TEMP-2 author requirements; downstream consumers should not assume independent validation has occurred.

### Data Usage

HVE Core does not bundle training data. Runtime inputs are user-authored prompts, attached repository files, and tool outputs that the operator chooses to share with the configured model. Memory subsystems used by some agents store transient state on the operator's local machine; retention, consent, and redaction policies are tracked in RAI-TEMP-14 (Memory layer specification). Sensitive customer data handling guidance is tracked in RAI-TEMP-15.

### Decision Process

Agents produce suggested actions and considerations. They do not autonomously commit code, file work items, or send messages without operator confirmation. Multi-agent orchestration audit trail work is tracked in RAI-TEMP-6. AI-disclosure markers on agent-produced artifacts are tracked in RAI-TEMP-7.

### Human Oversight

The operator is the primary human-in-the-loop. Custom agents include explicit confirmation gates before destructive or external-effect actions (issue creation, PR submission, file deletion). Per-agent Impact Assessments tracked in RAI-TEMP-5 capture oversight requirements per agent. Customer-handoff governance is tracked in RAI-TEMP-8.

### Contact and Feedback

GitHub issues on the microsoft/hve-core repository are the primary feedback channel. Agent discoverability into user-facing docs (so consumers know which agent is appropriate for which scenario, and how to escalate concerns) is tracked in RAI-TEMP-20.

*Note: AI-assisted content. Review and validate before use.*

---

## Monitoring Summary

| Work Item   | Metric                                               | Threshold/Criteria                                                                 | Alert Mechanism                                         | Review Cadence   |
|-------------|------------------------------------------------------|------------------------------------------------------------------------------------|---------------------------------------------------------|------------------|
| RAI-TEMP-9  | Drift in agent behavior vs. intended scope           | Material divergence from agent.md or instructions.md detected                      | Telemetry-driven dashboard + RAI re-assessment trigger  | Quarterly        |
| RAI-TEMP-7  | AI-disclosure marker presence on generated artifacts | 100% of agent-produced files include the standard footer                           | CI lint (lint:ai-artifacts)                             | Per pull request |
| RAI-TEMP-17 | Prompt-injection patterns in instruction content     | Zero occurrences of detected injection markers in committed instructions           | CI lint job (instruction-content prompt-injection lint) | Per pull request |
| RAI-TEMP-19 | Secrets in cloud agent CI execution                  | Zero secrets/tokens detected by gitleaks across .github/workflows and agent runs   | gitleaks GitHub Action; failure blocks merge            | Per pull request |
| RAI-TEMP-18 | AI-authored workflow files merged without review     | Zero workflow files authored or modified by an agent merged without human approval | CI gate + CODEOWNERS enforcement on .github/workflows   | Per pull request |
| RAI-TEMP-12 | Accessibility regressions in user-facing docs        | Zero new WCAG 2.1 AA violations in docs/ tree                                      | axe-core or pa11y CI run on docs build                  | Per pull request |

*Note: AI-assisted content. Review and validate before use.*

---

## Disclaimer

This agent is an assistive tool only. It does not provide legal, regulatory, or compliance advice and does not replace Responsible AI review boards, ethics committees, legal counsel, compliance teams, or other qualified human reviewers.

The output consists of suggested actions and considerations to support a user's own internal review and decision-making. All RAI assessments, risk classification screenings, security models, and mitigation recommendations generated by this tool must be independently reviewed and validated by appropriate legal and compliance reviewers before use.

Outputs from this tool do not constitute legal approval, compliance certification, or regulatory sign-off.

---

🤖 *Crafted with precision by ✨Copilot following brilliant human instruction, then carefully refined by our team of discerning human reviewers.*
