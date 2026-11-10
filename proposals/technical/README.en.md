# Technical Proposal for an AI Management Infrastructure

[日本語](README.md) · **English**

Author: Masao Takeuchi (Masao Gate Labs). Document ID **MGL-ASP-TEC-001**. Source version v1.1, dated 29 October 2026.  
Public edition. Microsoft Copilot and ChatGPT supported the original research and writing. ChatGPT assisted with public editing and translation.

This is independent research. The acknowledgments indicate assistance and do not imply collaboration, review, approval, or endorsement by the AI providers.

## Proposed execution boundary

The proposal addresses workflows that affect external systems across organizations or agents. Logical responsibilities include identity, grants and delegation, decision and enforcement, external tool access, evidence, oversight, continuous conformity, incident response, and recovery. Evaluate potential paths around enforcement in each environment.

1. Identify the request, source of delegation, purpose, target, action, and required authority.
2. Check current grants, conformity, revocation, and shared limits, then decide whether to permit, deny, review, or quarantine the operation.
3. For high-impact operations, establish the pre-action record and any necessary reservation. Bind the permit to the target and action conditions and recheck it immediately before execution.
4. Reconcile the decision with the external receipt or target state. Preserve unknown outcomes and use reconciliation and the external service's properties to decide whether a retry could cause duplicate effects.
5. After material changes or incidents, restrict scope. Reissue only the necessary authority after remediation, reassessment, and review.

Distinguish evidence integrity from agreement with real outcomes. Administrative changes, suspension, reinstatement, and evidence access are themselves subject to authorization and oversight. Verify the meaning, validity, and scope of credentials from external organizations before accepting them.

## Additional cross-cutting requirements

- **GOV-01** Separate administrative powers and address conflicts of interest
- **GOV-02** Require expiry, notice, and review for temporary measures
- **GOV-03** Provide controlled access to evidence for review and remedy
- **GOV-04** Assess proportionality of controls, cost, oversight burden, and privacy
- **OPS-01** Apply aggregate limits and reservations consistently under concurrency
- **OPS-02** Define restrictions and reconciliation for unknown states
- **OPS-03** Bind execution to evidence and handle missing or conflicting records
- **OPS-04** Bind permits to execution conditions and handle revocation, retries, and duplication

## Verification plan

| ID | What to check |
| --- | --- |
| V-01 | Deny absent, expired, or mismatched authority and check external state |
| V-02 | Deny redelegation beyond parent scope and reconstruct its origin |
| V-03 | Propagate parent revocation and distinguish new from in-flight actions |
| V-04 | Independently reconcile request, authority, policy version, execution, and outcome |
| V-05 | Check that material configuration changes trigger reassessment or restrictions |
| V-06 | Test whether a human stop handles new and in-flight actions as defined |
| V-07 | Block reinstatement until remediation and review, then reauthorize a limited scope |
| V-08 | Prevent unknown, expired, or semantically mismatched credentials from granting authority |
| V-09 | Test the shared cap, including reservations, under concurrent execution |
| V-10 | Detect failures in pre-action records, outcome storage, and external receipts |
| V-11 | Exercise races, lost responses, and retries, preventing stale permits and duplicate effects while reconciling unknown outcomes |
| V-12 | Prevent unauthorized administrative changes and self-approval and audit exceptions |
| V-13 | Test overcollection, unauthorized access, retention deadlines, and preservation conditions |
| V-14 | Preserve disagreements between agent reports and external observations and reconstruct responsibilities |
| V-15 | Block out-of-scope operations even under the same stated purpose and escalate ambiguity |
| V-16 | Increase load and concurrency to evaluate latency, false stops, cost, and oversight workload |

Record success conditions, observable state, assumed failures, independence, and residual risks for each use case. Set bounds for revocation and reconciliation before testing. This is a reference design and test plan. It reports neither measured results for the integrated design nor safety certification.

[Policy proposal and P-01 through P-08 mapping](../policy/README.en.md) · [Requirements catalog](../../series/paper-002/README.en.md) · [Case analyses](../../cases/README.en.md)
