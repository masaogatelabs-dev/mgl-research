# Technical review of the nine-dimensional Borsuk counterexample

Masao Gate Labs · OpenAI Math Family 156 · Published version v0.1.0 · 2026-11-14 JST · MGL-REF-011

## Scope and review result

MGL reviewed the pinned OpenAI manuscript dated September 23, 2026, covering Theorem 1.1 (p. 2, proof on p. 16), Corollary 7.1 (p. 17), and their proof dependencies. The theorem uses the rank-one orthogonal projectors onto lines in real four-dimensional space. They lie in the nine-dimensional affine space of trace-one symmetric matrices and have Frobenius diameter √2. Ten sets of diameter strictly smaller than √2 cannot cover this set. Corollary 7.1 extends the construction to all integer dimensions d ≥ 9.

MGL completed its internal technical review and found no defect overturning the conclusions within the reviewed scope.

## Reconstruction from four and five labels

A six-label triangle system selects exactly one triple from each complementary pair, with each pair of labels occurring in exactly two selected triangles (Definition 5.1, p. 12). **MGL tested a shortcut during the review** that would reconstruct the whole system uniquely from the triangles on four labels.

Both systems below satisfy the definition. Each three-digit string denotes a triangle.

| System | Selected triangles |
| --- | --- |
| System I | 123, 124, 135, 146, 156, 236, 245, 256, 345, 346 |
| System II | 123, 124, 136, 145, 156, 235, 246, 256, 345, 346 |

Both restrict to just 123 and 124 on {1,2,3,4}. They differ on triangles involving labels 5 and 6, so four labels do not determine the system. With five labels, the complement of every triple containing the omitted label lies entirely among the five retained labels. Membership of each missing triple follows from the complementary-triple rule, giving unique reconstruction under the paper’s conditions (Lemma 5.3(4), pp. 12–13).

## Finite checks and general argument

| Check | What MGL checked |
| --- | --- |
| Finite | Enumerated all 1,024 ways of choosing from the ten complementary pairs and obtained 12 labeled systems satisfying the conditions. Each realized restriction to a fixed four-label set had two extensions. Each restriction to a fixed five-label set had one. A separate rational-arithmetic check covered 3,160 pairs of projectors. |
| General | Checked the reduction from a cover to a smooth partition of unity, the mod-2 degree of the odd map and its constraint on maximal supports, and the deduction of the ten-label obstruction from the six-label systems. Complements of adjacent tetrahedra share five labels, as needed for the transport in Lemma 6.2 (pp. 13–14). For the extension to higher dimensions, MGL checked that each added point is at diameter distance from every other added point and every point in the original set. |

## Open scope

Independent third-party review or replication, human peer review, Lean execution by MGL, and a comprehensive literature review remain unperformed. OpenAI separately documents formalization of the nine-dimensional counterexample. The smallest dimension admitting a counterexample and the exact covering number of this set are outside the manuscript’s claims.

## Sources and citation

- [OpenAI’s pinned source paper (PDF)](https://github.com/openai/math/blob/4eaee87548250b2682affda7d05d947c05554bae/preprints/A-nine-dimensional-counterexample-to-Borsuks-covering-assertion-September-23-2026/paper.pdf)
- [OpenAI’s Lean scope note at the same commit](https://github.com/openai/math/blob/4eaee87548250b2682affda7d05d947c05554bae/lean/docs/156.md)

Suggested citation. Masao Gate Labs (2026). Technical review of the nine-dimensional Borsuk counterexample. OpenAI Math Family 156, published version v0.1.0, MGL-REF-011.
