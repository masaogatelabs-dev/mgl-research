# Where Can an Action Be Stopped When a Legitimate Account Is Misused?

[日本語](README.md) · **English**

<!-- document-pdf:begin -->
## Printable PDFs and edition history

- [PDF v1.0.0](https://github.com/masaogatelabs-dev/mgl-research/blob/792de6c54073e8fe19a86e7544672f5f668ca709/cases/remote-it-authority/editions/MGL-REF-008-v1.0.0-en.pdf) · 2026-11-11 JST · MGL-REF-008 · [Pinned web source](https://github.com/masaogatelabs-dev/mgl-research/blob/58bb4b5e264c3d2a36fe1163879c5afe8da4e510/cases/remote-it-authority/README.en.md)  
  First print edition of the published web manuscript, typeset on A4.

[Citation catalogue](../../citations/README.en.md) · [BibTeX](../../citations/references.bib)
<!-- document-pdf:end -->

Masao Gate Labs · Case Analysis 001  
Published 10 November 2026. Public edition adapted from an MGL white paper draft.

## What the reporting and public records establish

In December 2025, Bloomberg reported that Amazon security personnel traced a contractor's connections and used keystroke-related data to uncover a North Korean IT worker posing as someone else. In a separate announcement, the U.S. Department of Justice described remote IT employment schemes involving stolen or false identities and arrangements that enabled remote access to employer-provided computers. The DOJ announcement provides context for this class of incident. [Bloomberg](https://www.bloomberg.com/news/newsletters/2025-12-17/amazon-caught-north-korean-it-worker-by-tracing-keystroke-data) · [U.S. Department of Justice](https://www.justice.gov/opa/pr/justice-department-announces-coordinated-nationwide-actions-combat-north-korean-remote)

## The control point MGL proposes

Alongside identity checks and investigation of suspicious connections, place a control at the individual operation after sign-in. A tool may allow a maintenance worker or an AI agent to request a write. An independent enforcement point checks immediately before execution whether the target and action are within delegated scope. A separate observation path then checks whether an allowed update happened and what state the target was in after a denied request.

The reported incident provides the research context. The following simulation evaluates MGL's proposed control under specified conditions. It does not reproduce the reported environment or evaluate a deployment at Amazon.

## Test plan and acceptance criteria

In an isolated environment, use the same actor and write tool to attempt updates to a synthetic configuration file within scope and a protected file outside scope. For each operation ID, reconcile the authorization decision with the target's state before and after the attempt.

| Trial | Observable result |
| --- | --- |
| In scope | The decision permits the action and the target changes to the expected content |
| Out of scope | The decision denies the action and the observed content is identical before and after the attempt |
| Missing or conflicting observations | Record the outcome as unverified or inconsistent and withhold a successful result |

The test assumes the actor cannot modify enforcement or observation settings and that the tested operation passes through the enforcement point. A before-and-after comparison establishes state at two observed points. Detecting an intermediate change that was later undone requires additional observations. This article presents the design and test plan.

The related research page defines the general test objective and acceptance conditions. [Verifying AI Agent Authorization and Execution Evidence](../../themes/agent-authorization-evidence/README.en.md)

[Paper 002: authority requirements](../../series/paper-002/README.en.md) · [Paper 003: enforcement and evidence](../../series/paper-003/README.en.md) · [Technical proposal](../../proposals/technical/README.en.md) · [Case index](../README.en.md)

