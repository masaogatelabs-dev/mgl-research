# Technical review of Seymour’s second-neighborhood conjecture

Masao Gate Labs · OpenAI Math Family 173 · Published version v0.1.0 · 2026-11-14 JST · MGL-REF-010

## Review scope

This review covers the pinned version of OpenAI’s preprint dated September 23, 2026. Page numbers refer to the source paper.

| Source location | What MGL checked |
| --- | --- |
| Theorem 1.1 (p. 1, proof on p. 12) | In any nonempty finite oriented graph, with no loops, multiple arcs, or opposite arcs, some vertex has at least as many vertices at directed distance exactly two as at distance one. The count at distance two excludes the starting vertex and its direct out-neighbors. |
| Corollary 5.1 (pp. 12–13) | For any nonnegative vertex weights, some vertex satisfies the inequality. There also exist nonnegative vertex weights totaling one for which every vertex satisfies it. The statement for nonnegative arc weights relies on Seacrest’s Proposition 2. A zero-weight arc can still belong to a two-step path. |
| Corollary 6.1 (pp. 13–14) | The non-neighbor and degree inequalities in the absence of directed triangles, the existence of a directed triangle when both minimum degrees are at least n/3, and the bound n ≥ 3r + 1 when every vertex has in- and outdegree r and the directed girth is four. |

MGL completed its internal technical review within the stated scope. Independent third-party review or replication, human peer review, and Lean re-verification by MGL have yet to be performed. OpenAI’s Lean scope note covers the exact-distance-two statement corresponding to the main theorem.

## A three-vertex counterexample to the shortcut for Lemma 3.1

In Lemma 3.1 (pp. 6–10), equation (8) bounds the number of deletions needed to remove conflicts by **|H| + q**. Here q counts the points of Z, the set defined by the conflicts, that no surviving member covers. During the review, MGL tested a simplification that drops q and uses **|H|** alone as the bound.

Take vertices 0, 1, and 2, with just the arcs 0 → 1 and 0 → 2. Set the left family R = {(0,1), (0,2)} and the right family C = {(1,0), (2,0)}. Each left member conflicts with both right members, so removing all conflicts requires at least two deletions. The paper’s definition gives H = {(0,0)}. Thus the shortcut bound |H| = 1 fails.

All four points of Z = {1,2} × {1,2} are initially covered. Deleting just the two members on either side leaves all four points covered by the other side, so q = 0 and 2 ≤ 1 fails. Deleting all four members leaves q = 4, and 4 ≤ 1 + 4 holds. This pruning satisfies the paper’s equation (8).

## Finite checks

| Target | Inputs and results |
| --- | --- |
| Theorem 1.1 | Exhaustively checked all 59,809 labeled oriented graphs on one to five vertices under the paper’s assumptions. Zero counterexamples. Counting endpoints of any two-step path changed the truth of the inequality in 43,218 graph–vertex pairs compared with counting vertices at distance exactly two. |
| Lemma 3.1, two-element set | Checked all 4,096 combinations of the binary relation and the left and right families. Zero counterexamples to equation (8) and 40 to the shortcut. On the same inputs, direct enumeration and the augmented bipartite graph calculation agreed on the minimum of “deletions − q” in every case. |
| Lemma 3.1, three-element set | Checked a fixed sample of 1,600 configurations. Zero counterexamples to equation (8) or to the augmented bipartite graph matching bound, and 22 counterexamples to the shortcut. |

## Checks of the general argument

For the main theorem, MGL checked how Proposition 2.1 (pp. 3–5) obtains a graph with the required expansion property from a minimal counterexample and how Proposition 4.1 (pp. 10–12) rules out such a graph. The review also checked why diagonal members are conflict-free and retained when Proposition 4.1 applies the pruning lemma.

For Lemma 3.1, MGL checked the rank argument for the augmented bipartite graph’s matching bound |Z| + |H|, including Lemma 3.2, and how its vertex cover yields equation (8). Each of the |Z| − q points still covered after pruning requires a distinct auxiliary vertex in the cover. Subtracting these vertices from the cover bound leaves at most |H| + q deletions of original members, as in equation (9). The construction also retains every initially conflict-free member.

For Corollary 5.1, MGL checked Seacrest’s Proposition 2, the specialization from arc weights to vertex weights, and the separation argument using transposition under arc reversal. For Corollary 6.1, MGL checked how all three conclusions follow from the fact that exact second out-neighbors are non-neighbors when the graph has no directed triangle.

## Sources and citation

- [OpenAI’s pinned source paper (PDF)](https://github.com/openai/math/blob/4eaee87548250b2682affda7d05d947c05554bae/preprints/A-proof-of-Seymours-second-neighborhood-conjecture-September-23-2026/paper.pdf) · *A proof of Seymour’s second-neighborhood conjecture* (2026-09-23)
- [OpenAI’s Lean scope note at the same commit](https://github.com/openai/math/blob/4eaee87548250b2682affda7d05d947c05554bae/lean/docs/173.md)
- [Tyler Seacrest, arXiv:1212.1883v1, Proposition 2](https://arxiv.org/abs/1212.1883v1)

Suggested citation. Masao Gate Labs (2026). Technical review of Seymour’s second-neighborhood conjecture. OpenAI Math Family 173, published version v0.1.0, MGL-REF-010.
