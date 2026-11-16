# Research Themes

[日本語](README.md) · **English**

For each theme, we share the research objective, the current stage, and the next question we plan to investigate, to the extent these details can be made public.

| Area | Publication status | Overview |
| --- | --- | --- |
| Verifying AI Agent Authorization and Execution Evidence | Reference design and test plan published | [Research objective and test plan](agent-authorization-evidence/README.en.md) · [Execution Controls and Evidence](#execution-controls-and-evidence) |
| AI peer review and verification | Technical reviews published | [Mathematical proof verification and review index](math-proof-review/README.en.md) |
| Left-brain core | In preparation | — |
| Learning from experience | In preparation | — |
| Right-brain β2 and computation | Theme overview in preparation. Case study with evaluation results published | [The MGL High-Precision Engine in a technical review](../reports/precision-engine/MGL-High-Precision-Engine-Family266.en.md) |
| Communication and shared repositories | In preparation | — |

## Execution Controls and Evidence

Immediately before a file update, the system checks whether the requested action and target fall within the delegated scope. The design calls for out-of-scope updates to be denied at the point of execution.

A separate observation path checks the file contents before and after the attempt. An operation ID links the request, the authorization decision, and the observations so a third party can compare the records for the same attempt. The test plan describes what the two observations establish and how each trial is evaluated.

The reference design and test plan are public. Measured results for the test plan are pending publication.

[Published reference design](../series/paper-003/README.en.md) · [Back to the test plan](agent-authorization-evidence/README.en.md#test-plan)

[Public research results](../results/README.en.md) · [Home](../README.en.md)
