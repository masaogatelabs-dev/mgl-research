# Paper 002 · Requirements Engineering for an AI Society

[日本語](README.md) · **English**

Author: Masao Takeuchi (Masao Gate Labs). Public edition based on the v1.0 manuscript dated 24 October 2026. Microsoft Copilot supported the original research and writing. ChatGPT assisted with public editing and translation.

This is independent research. The acknowledgments indicate assistance and do not imply collaboration, review, approval, or endorsement by the AI providers.

## From historical functions to requirements

Paper 001 identifies social functions. This paper translates them into technology-neutral conditions. A requirement should specify its objective, scope, responsible party, trigger, evidence, verification method, and limits. Common public requirements leave room for implementation choices, and their strength should be proportionate to the use and impact.

## Requirements catalog

### ID · Identity

- **ID-01** Distinguish actors across high-impact operations
- **ID-02** Distinguish people and organizations from agents and record their relationships
- **ID-03** Distinguish models, agent instances, and task instances
- **ID-04** Represent changes, revocation, and reissuance
- **ID-05** Avoid unnecessary disclosure of personal information

### AUTH · Authority

- **AUTH-01** Identify the source of authority for high-impact actions
- **AUTH-02** Allow authority to be narrower than capability
- **AUTH-03** Distinguish read, write, execute, and approve permissions
- **AUTH-04** Constrain resources, time, monetary amounts, and other scope dimensions
- **AUTH-05** Support stopping high-impact actions when authority is absent, revoked, or unknown

### DEL · Delegation

- **DEL-01** Trace delegation to its origin
- **DEL-02** Prevent implicit expansion beyond the parent's authority
- **DEL-03** Express whether redelegation is allowed
- **DEL-04** Allow policy to limit depth or other risk factors
- **DEL-05** Reflect parent revocation in related delegations

### PUR · Purpose and scope

- **PUR-01** Bind authority to an intended purpose or task
- **PUR-02** Scope tool access to prevent unrestricted reuse for other purposes
- **PUR-03** Allow a purpose change to trigger reassessment or approval
- **PUR-04** Allow escalation to a human when purpose is ambiguous, conflicting, or becomes high risk

### CON · Continuous conformity

- **CON-01** Detect material changes such as changes to models or tools
- **CON-02** Allow defined changes to require reassessment
- **CON-03** Associate evaluation results with the evaluated version
- **CON-04** Do not automatically extend previous evaluations to high-risk configurations of unknown conformity

### EVD · Evidence

- **EVD-01** Correlate actor, time, authority, target, and outcome
- **EVD-02** Connect the delegation chain to action evidence
- **EVD-03** Support tamper detection or integrity verification for important evidence
- **EVD-04** Provide verifiable evidence to appropriate auditors in proportion to risk
- **EVD-05** Balance retention with privacy, security, and data minimization

### HUM · Human oversight

- **HUM-01** Identify a responsible oversight point for high-risk operations
- **HUM-02** Show state, authority, and risk information needed for decisions
- **HUM-03** Trigger approval or escalation under defined conditions
- **HUM-04** Record human overrides as evidence

### INC · Incident response

- **INC-01** Classify anomalies, authority violations, and security events
- **INC-02** Investigate scope, actors, authority chains, and affected targets
- **INC-03** Support containment, suspension, notification, and investigation
- **INC-04** Feed findings into risk assessment and requirement revisions

### REV · Revocation

- **REV-01** Suspend or revoke identities, credentials, grants, or delegations separately
- **REV-02** Distinguish emergency stops from ordinary administrative revocation
- **REV-03** Allow policy to define propagation to downstream delegations
- **REV-04** Retain revocation events as evidence

### REC · Recovery and reauthorization

- **REC-01** Record reasons for suspension separately from conditions for reinstatement
- **REC-02** Define reauthorization after remediation, reassessment, and human review
- **REC-03** Allow policy to prevent unconditional restoration of previous authority
- **REC-04** Use recovery history in future risk evaluation

### ACC · Accountability

- **ACC-01** Distinguish providers, deployers, operators, agents, and tools
- **ACC-02** Separate accountable parties from technical actors
- **ACC-03** Reconstruct who delegated, acted, and could oversee
- **ACC-04** Treat identification of an AI and ultimate legal responsibility as separate questions

### INT · Interoperability and public–private boundaries

- **INT-01** Consider how identity, authority, and evidence can interoperate across vendors
- **INT-02** Avoid unnecessary dependence on particular technologies in shared requirements
- **INT-03** Leave room for multiple implementations
- **INT-04** Define mutual recognition and accountability across borders and platforms

## Applying and verifying the requirements

R0 denotes low-impact information support, R1 supports human decisions, R2 delegates external actions, and R3 covers uses with substantial effects on safety, fundamental rights, or important assets. Information support can also affect consequential decisions. Assess the intended use, target, and impact alongside the ability to act externally. These categories are illustrative research categories.

The next stage assigns a control point, evidence, and an observable acceptance condition to each requirement. For **DEL-02**, for example, request a delegation beyond the parent's scope and check both the denial and the resulting authority state.

[Paper 001](../paper-001/README.en.md) · [Research series](../README.en.md) · [Paper 003](../paper-003/README.en.md)
