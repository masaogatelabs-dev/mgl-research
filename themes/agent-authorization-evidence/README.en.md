# Verifying AI Agent Authorization and Execution Evidence

[日本語](README.md) · **English**

Masao Gate Labs · Ongoing research · Research objective and test plan

## Research objective

When an AI agent is delegated a file update, can we verify that **an authorized action completes as expected and an out-of-scope action is denied**? This research compares the authorization record with the actual file state. Evidence from an observation path separate from execution allows a third party to reconcile the request, decision, and outcome for the same operation.

## Research questions

1. Can the system evaluate the action and target against delegated scope immediately before execution and enforce the decision at the point of execution?
2. For both allow and deny decisions, can an observer verify that the target state matches the expected outcome?
3. Can a third party distinguish verified outcomes from outcomes with missing or conflicting evidence?

## Test plan

Use synthetic files in an isolated environment. Start each trial from the same initial state and compare the same update request under allow and deny conditions. Use an operation ID to associate the request, authorization decision, and before-and-after observations. The observation path is separate from execution. The test assumes the execution identity cannot change enforcement or observation settings, or alter evidence collected by the observer.

| Trial | Acceptance or reporting condition |
| --- | --- |
| Allow | The record permits the action and the observed contents change to the expected value |
| Deny | The record denies the action and the observed contents match before and after the attempt |
| Missing evidence | Mark the outcome unverified if the decision or target state cannot be associated with the same operation |
| Decision and observation disagree | Record the mismatch when the observed outcome conflicts with the allow or deny record |

A before-and-after comparison establishes content at two observed points. Detecting intermediate changes that were reversed, or evaluating paths outside the test scope, requires additional observations. This page presents the test plan. Results available for public release will be published separately with their test conditions and observation limits.

## Related research

- [Paper 002](../../series/paper-002/README.en.md) on authority (AUTH) and evidence (EVD) requirements
- [Paper 003](../../series/paper-003/README.en.md) on enforcement points and evidence design
- [Case Analysis 001](../../cases/remote-it-authority/README.en.md) on applying these ideas to misuse of legitimate access

[Research themes](../README.en.md) · [Public research results](../../results/README.en.md)
