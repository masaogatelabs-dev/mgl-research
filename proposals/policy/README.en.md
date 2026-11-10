# Policy and Institutional Proposal for an AI-Native Society

[日本語](README.md) · **English**

Author: Masao Takeuchi (Masao Gate Labs). Document ID **MGL-ASP-POL-001**. Source version v1.1, dated 29 October 2026.  
Public edition. Microsoft Copilot and ChatGPT supported the original research and writing. ChatGPT assisted with public editing and translation.

This is independent research. The acknowledgments indicate assistance and do not imply collaboration, review, approval, or endorsement by the AI providers.

## Scope

When AI can act on external systems and redelegate work, product safety is one part of the task. Institutions also need conditions for granting authority, oversight of operations, and procedures for investigation and remedy. This proposal draws on the development of road transport institutions to examine which functions transfer to AI, including common rules, ongoing assessment, and revision in light of evidence. It presents MGL's proposed arrangements for discussion.

## Eight policy proposals

### P-01 Responsibilities and delegation origin

Record who requested, delegated, executed, and oversaw the action. Identify gaps, overlaps, and handoff conditions.

### P-02 Separate capability and authority

Set purpose, target, action, expiration, limits, and redelegation conditions. Finding a new tool does not automatically expand authority.

### P-03 Reassess after change

When a model, tool, data source, purpose, or configuration changes, check the validity of prior evaluation and restrict operation as needed.

### P-04 Evidence and independent investigation

Connect requests, authority, decisions, and outcomes. Reconcile them with external receipts or target state and define investigation access and preservation rules.

### P-05 Limits on administrators

Separate responsibility for rule changes, grants, suspension, reinstatement, and evidence access. Require reasons, expiration, notice, and review for temporary measures.

### P-06 Suspension, review, and remedy

Distinguish blocking new actions from safely interrupting work in progress. Provide for appeals, phased reinstatement after reassessment, and remedies for affected parties.

### P-07 Proportionality of burden and privacy

Scale controls by impact, reversibility, autonomy, and reach. Minimize evidence collection and evaluate the burden on smaller adopters.

### P-08 Cross-organizational interoperability

Verify the meaning and validity of external identities, authority, and evidence. Progress from simulation to independent evaluation and limited operation.

## Allocate responsibilities

Developers and providers communicate evaluation scope, updates, and conditions of use. Deploying organizations set purposes, delegation boundaries, oversight arrangements, and incident procedures. Standard setters, evaluators, and independent investigators need defined responsibilities for common conditions, verification, and appropriate access to evidence. Infrastructure operators are themselves subject to oversight when they change grants, suspend access, or restore it. Identify AI as a technical actor and address legal responsibility in a separate process that accounts for the circumstances.

Effective oversight requires information, time, authority, and backup arrangements. Keep evidence collection and disclosure proportionate to oversight and remedy needs.

## Shared example and link to the technical proposal

In a fictional procurement workflow, a purchasing agent delegates quotations and ordering to child agents. Each order could be within its individual limit while the aggregate exceeds the budget. Check the shared limit at execution time. If a response is lost and the order outcome is unknown, reconcile against the external receipt before retrying.

| Shared ID | Policy area | Technical requirements | Tests in the technical proposal |
| --- | --- | --- | --- |
| P-01 | Responsibilities and delegation origin | ID / ACC / DEL | V-04, V-14 |
| P-02 | Separate capability and authority | AUTH / PUR / DEL | V-01, V-02, V-09, V-15 |
| P-03 | Reassess after change | CON / OPS-02 | V-05 |
| P-04 | Evidence and independent investigation | EVD / ACC / OPS-03 | V-04, V-10, V-14 |
| P-05 | Limits on administrators | HUM / GOV-01 / GOV-02 | V-06, V-12 |
| P-06 | Suspension, review, and remedy | INC / REV / REC / GOV-03 | V-03, V-07, V-12 |
| P-07 | Proportionality of burden and privacy | ID-05 / EVD-05 / GOV-04 | V-13, V-16 |
| P-08 | Cross-organizational interoperability | INT / OPS-01 / OPS-04 | V-08, V-11, V-16 |

Progress through design, simulation, independent evaluation, and limited deployment. Evaluate unauthorized actions, time to reflect revocation, false stops, recovery, oversight workload, operating cost, and access to remedy. Define acceptance criteria before testing, according to the impact of the use case.

Related public sources: [Paper 001 references](../../series/paper-001/README.en.md) · [Japan National Police Agency: History of traffic safety measures](https://www.npa.go.jp/hakusyo/h29/honbun/html/tf120000.html) · [NIST AI RMF](https://www.nist.gov/itl/ai-risk-management-framework) · [NIST AI Agent Standards Initiative](https://www.nist.gov/artificial-intelligence/ai-agent-standards-initiative)

[Technical proposal](../technical/README.en.md) · [Proposal index](../README.en.md) · [Research series](../../series/README.en.md)
