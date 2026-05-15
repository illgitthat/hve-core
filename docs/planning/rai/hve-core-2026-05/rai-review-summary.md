---
title: "RAI Review Summary - HVE Core (May 2026)"
description: "Responsible AI assessment summary for HVE Core, evaluated against the NIST AI Risk Management Framework 1.0 trustworthiness characteristics."
author: HVE Core RAI Reviewers
ms.date: 2026-05-14
ms.topic: overview
keywords:
  - responsible-ai
  - rai
  - nist-ai-rmf
  - assessment
  - hve-core
estimated_reading_time: 8
---

## Overview

| Field                | Value                                                                       |
|----------------------|-----------------------------------------------------------------------------|
| System               | HVE Core (microsoft/hve-core)                                               |
| Assessment Date      | 2026-05-14                                                                  |
| Depth Tier           | Comprehensive                                                               |
| Evaluation Framework | NIST AI Risk Management Framework 1.0 (trustworthiness characteristics)     |

## Executive Summary

HVE Core is a static governance and AI-artifact distribution repository (custom agents, prompts, instructions, skills, scripts) shipped to Microsoft engineers and customer engagements via VS Code extensions, Copilot plugins, and direct clones.
It does not train models, does not host inference, and does not call external services at runtime.
The Responsible AI exposure is concentrated in (a) what the artifacts say to and about downstream model invocations, (b) the trust customers and engineers place in artifacts that carry Microsoft branding, and (c) the persistent memory and customer-handoff workflows the agents orchestrate.

The assessment evaluated the system across the seven NIST AI RMF trustworthiness characteristics and flagged one direct generative-AI touchpoint (Customer Card Render concept-image generation).
Maturity reads: Accountable-and-Transparent and Valid-and-Reliable Developing; Fair Developing; Privacy-Enhanced Foundational (evidence-driven); Safe, Secure-and-Resilient, and Explainable-and-Interpretable Foundational (no inference-time runtime; concerns are folded into Valid-and-Reliable, Privacy-Enhanced, and Accountable-and-Transparent in the per-characteristic notes).
Three areas warrant near-term attention before broad customer redistribution: public claims about agent fitness, AI-disclosure markers on agent-produced artifacts, and customer-handoff governance.

### Review Checkpoint Results

| Checkpoint      | Status | Notes                                                                                                                                                                                  |
|-----------------|--------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Threat Coverage | Met    | Each of the 15 RAI threats (T-RAI-001..015) is mapped to at least one control surface entry and at least one evidence row in the evidence register; Coverage and Verification recorded |

### Per-Characteristic Summary

| Characteristic                 | Maturity Level                 | Key Observations                                                                                                                                                                                    | Open Items |
|--------------------------------|--------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| Valid and Reliable             | Developing                     | Strong artifact-quality controls (linting, validation, plugin generation gate); runtime fitness-for-purpose unverifiable; no instruction-content prompt-injection lint                              | 4          |
| Safe                           | Foundational                   | No inference-time runtime; concerns surface as Valid-and-Reliable items (public claims) and downstream-model issues mediated by host platform                                                       | 1          |
| Secure and Resilient           | Foundational                   | No inference-time runtime; security concerns surface as Privacy-Enhanced items (gitleaks, memory layer) and Accountable-and-Transparent items (audit trail); SDL adoption status not yet documented | 1          |
| Accountable and Transparent    | Developing                     | No HVE Core Transparency Note; per-agent capability/limitation statements absent; AI-disclosure marker not enforced on agent-produced artifacts; customer-handoff opaque                            | 4          |
| Explainable and Interpretable  | Foundational                   | No inference-time runtime; per-agent intelligibility footers not standard; concerns surface as Accountable-and-Transparent items                                                                    | 1          |
| Privacy-Enhanced               | Foundational (evidence-driven) | Microsoft Privacy Standard adoption not declared; memory-layer retention/consent/redaction not specified; gitleaks not present in cloud agent CI; DT participant data                               | 4          |
| Fair with Harmful Bias Managed | Developing                     | Persona stereotyping audit not run; accessibility audit absent; language and code-language coverage skewed; agent discoverability unequal                                                           | 4          |

### Key Findings

* The repository contains no model training, no inference runtime, no external service calls at runtime, and no PII processing within its own boundaries. RAI exposure is mediated by downstream models the artifacts instruct and by the trust customers place in Microsoft-branded artifacts.
* The Customer Card Render skill is the only direct generative-AI touchpoint and warrants explicit redaction, persona-template stereotyping review, and human-review gates before customer-facing distribution.
* Customer-handoff distribution channel is the most opaque of six channels (extension, plugin, clone, devcontainer, customer-handoff, fork) and concentrates the highest density of Accountable-and-Transparent gaps.
* Multi-agent orchestration audit trail is partial; subagent execution is captured in session traces but not in a structured, exportable audit format suitable for compliance review.
* AI-disclosure markers on agent-produced artifacts are inconsistent; some artifact types include the standard footer, others do not, and there is no automated check.
* Public-facing materials (README, docs, marketing copy) include safety and fitness language that the static repository alone cannot verify; claims should be scoped to what the repository ships rather than what the agents do at runtime.
* No Security Plan exists for HVE Core. A separate group will run that assessment independently; cross-reference table in this assessment is intentionally empty.

### Review Quality Summary

| Dimension             | Status    | Notes                                                                                                                                                                                                 |
|-----------------------|-----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Standards Alignment   | Addressed | NIST AI RMF 1.0 trustworthiness characteristics used as the per-characteristic structure throughout the assessment                                                                                    |
| Threat Completeness   | Addressed | 15 RAI threats catalogued (T-RAI-001..015) with concern-level reads; cross-reference column intentionally empty pending separate Security Plan                                                        |
| Control Effectiveness | Addressed | Control surface catalog covers Prevent / Detect / Respond per characteristic; Detect and Respond gaps concentrated in customer-handoff and runtime telemetry                                          |
| Evidence Quality      | Addressed | 41 evidence rows; 7 Full / 16 Partial / 18 Gap; 9 Verified / 3 Partially Verified / 11 Unverified / 18 N/A; per-channel coverage notes embedded                                                       |
| Tradeoff Resolution   | Addressed | 8 tradeoffs documented (TO-002 / 005 / 006 / 007 from common catalog plus TO-100..103 HVE Core-specific); TO-001 / 003 / 004 explicitly not catalogued (no model training, no inference-time runtime) |
| Risk Classification   | Addressed | Comprehensive depth tier; risk score 0.63 (mean of 0.55 / 0.80 / 0.55); Phase 5 dimension revisit netted flat (att 0.50, data 0.80, explain 0.60, mean 0.633); baseline kept                          |

### Suggested Remediation Horizon Summary

| Horizon            | Work Item Count | Key Items                                                                                                                                                                                                                                                                                                         |
|--------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Pre-Production     | 10              | Public claims audit, Transparency Note, per-agent capability statements, Microsoft standards adoption (Privacy, SDL, Accessibility, AI Code of Conduct), per-agent IAs, AI-disclosure marker, persona stereotyping audit, Customer Card Render redaction, prompt-injection lint, AI-authored workflow review gate |
| Early Operations   | 4               | Multi-agent orchestration audit trail, production telemetry / drift / re-assessment cadence, memory-layer retention / consent / redaction, gitleaks in cloud agent CI                                                                                                                                             |
| Ongoing Governance | 6               | Customer-handoff governance, language and code-language coverage, accessibility audit, evaluation cohort diversification, sensitive customer data handling guidance, agent discoverability promotion                                                                                                              |

### Suggested Outcome

| Field                 | Value                            |
|-----------------------|----------------------------------|
| Suggested Status      | Additional attention suggested   |
| Remediation Suggested | Yes                              |
| Work Items Generated  | 20                               |

The assessment surfaced concentrated near-term work in Accountable-and-Transparent (Transparency Note, AI-disclosure marker, customer-handoff governance) and in the single direct generative-AI touchpoint (Customer Card Render). With those areas addressed, the suggested review status would shift to "Ready for stakeholder review."

## AI-Assistance Disclosure

The author created this content with assistance from AI. All outputs should be reviewed and validated before use by a qualified human reviewer.

## Disclaimer

This agent is an assistive tool only. It does not provide legal, regulatory, or compliance advice and does not replace Responsible AI review boards, ethics committees, legal counsel, compliance teams, or other qualified human reviewers.

The output consists of suggested actions and considerations to support a user's own internal review and decision-making. All RAI assessments, risk classification screenings, security models, and mitigation recommendations generated by this tool must be independently reviewed and validated by appropriate legal and compliance reviewers before use.

Outputs from this tool do not constitute legal approval, compliance certification, or regulatory sign-off.

---

🤖 *Crafted with precision by ✨Copilot following brilliant human instruction, then carefully refined by our team of discerning human reviewers.*
