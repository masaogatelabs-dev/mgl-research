# Paper 003 · Reference Architecture for an AI Society

[日本語](README.md) · **English**

<!-- document-pdf:begin -->
## Printable PDFs and edition history

- [PDF v1.0.0](https://github.com/masaogatelabs-dev/mgl-research/blob/792de6c54073e8fe19a86e7544672f5f668ca709/series/paper-003/editions/MGL-REF-004-v1.0.0-en.pdf) · 2026-11-11 JST · MGL-REF-004 · [Pinned web source](https://github.com/masaogatelabs-dev/mgl-research/blob/58bb4b5e264c3d2a36fe1163879c5afe8da4e510/series/paper-003/README.en.md)  
  First print edition of the published web manuscript, typeset on A4.

[Citation catalogue](../../citations/README.en.md) · [BibTeX](../../citations/references.bib)
<!-- document-pdf:end -->

Author: Masao Takeuchi (Masao Gate Labs). Public edition based on the v1.0 manuscript dated 24 October 2026. Microsoft Copilot supported the original research and writing. ChatGPT assisted with public editing and translation.

This is independent research. The acknowledgments indicate assistance and do not imply collaboration, review, approval, or endorsement by the AI providers.

## Separate policy decisions from execution

An agent proposes an action. A policy decision point (PDP) evaluates identity, delegation, purpose, target, risk, configuration conformity, and revocation. A policy enforcement point (PEP) enforces the decision immediately before the operation. High-impact actions go through an execution adapter. Verification should cover potential paths that bypass the PEP.

Evidence connects intent, delegation and authority, the decision and policy version, the target and observed outcome, human intervention, incident handling, and recovery. Reconcile the authorization record with observations after execution, preserving gaps and discrepancies. Identity, execution, evidence, and oversight have separate logical responsibilities. Their deployment and independence are assessed for each implementation.

## Traceability from requirements to verification

| Paper 002 domain | Main control point | Verification question |
| --- | --- | --- |
| ID | Identity and status resolution | Try a high-impact action with invalid identity and check denial |
| AUTH | Authority and policy decision/enforcement | Block an external action without authority (V-01) |
| DEL | Delegation validation | Test whether a child can exceed its parent's authority (V-02) |
| PUR | Purpose and target policy | Deny or escalate an out-of-purpose action |
| CON | Configuration and continuous conformity | Check that material change triggers reassessment (V-05) |
| EVD | Evidence | Reconstruct delegation, authority, decision, and outcome (V-04) |
| HUM | Human oversight | Test whether oversight can stop execution (V-06) |
| INC | Incident response | Check transition from detection to containment |
| REV | Revocation and pre-execution checks | Test whether parent revocation propagates and stops new operations (V-03) |
| REC | Recovery and reauthorization | Test whether old authority can return before remediation and review (V-07) |
| ACC | Role mapping and evidence | Distinguish who delegated, executed, and oversaw the operation |
| INT | Interoperability gateway | Test whether unknown external credentials can become authority without validation (V-08) |

V-01 through V-08 in this table are verification proposals in this paper. The technical proposal uses test identifiers within its own document.

## Trust boundaries and a minimal proof of concept

Define what to recheck at delegation from a person or organization to an agent, redelegation, transfer of permission to the execution point, action on an external target, exchange of evidence, and acceptance of credentials across organizations. A minimal proof of concept can cover seven logical functions: identity, authority, decision and enforcement, tool access, evidence, oversight, and revocation and recovery.

Check scope, configuration changes, and revocation at runtime. Restrict or suspend operations when needed. After remediation, reassessment, and review, reissue only the authority required for recovery.

## Scope of verification

This is a reference design. A first evaluation would cover allowed and denied actions, missing evidence, material change, revocation, suspension, and recovery in a simulated environment, and report what could be observed. These are proposed tests. This paper presents no measured results for an integrated implementation.

Related research turns enforcement and independent observation into a concrete file-update test plan. [Verifying AI Agent Authorization and Execution Evidence](../../themes/agent-authorization-evidence/README.en.md)

[Paper 002](../paper-002/README.en.md) · [Security annex](../security-annex/README.en.md) · [Research series](../README.en.md)

