# Technical review of the balanced Ryser counterexamples

Masao Gate Labs · OpenAI Math Family 162 · Published version v0.1.0 · 2026-11-14 JST · MGL-REF-013

## Scope and review result

MGL reviewed Theorem 1.1 and Corollary 1.2 (p. 2) of the pinned OpenAI manuscript dated September 27, 2026. MGL completed its internal technical review and found no defect overturning the conclusions within the reviewed scope.

| Source location | What MGL checked |
| --- | --- |
| Theorem 1.1 (proof in §7) | For every sufficiently large prime q, the construction gives an intersecting hypergraph with q + 1 parts. Each edge takes one vertex from each part, and each part has exactly q + 1 vertices belonging to edges. The minimum size of a vertex set meeting all edges is q + 1, exceeding the bound q conjectured for the intersecting case. |
| Corollary 1.2 | Take the hyperedges as the vertices of a complete graph and color each pair by the part of a shared vertex. A connected monochromatic subgraph corresponds to one shared hypergraph vertex, giving a lower bound of q + 1 monochromatic trees for a cover. The stars of each color centered at a fixed vertex give the matching upper bound. |

## Finite checks and general argument

| Check | What MGL checked |
| --- | --- |
| Finite | Enumerated points and lines at q = 5, 7, 11 to check the local incidence bound for a pencil with a finite center. Checked 2,950 cases of the integer counting condition. |
| General | Checked how merging and splitting parallel lines balances the parts, and how a merge in another direction preserves intersection for pairs separated by a split (§2). The proof distinguishes centers at infinity from finite centers. MGL checked the concentration bound for deleted lines, joint probabilities for candidate choices, and exclusion of covers at finite centers, which together give positive probability for all conditions (§§3–7). |

## MGL’s local refinement

In §2 (pp. 7–8), suppose the specified merged-partner block through the center is absent. Labels inside the pencil cover at most 1 + B points, and each of the t labels outside it covers at most two. The paper’s conditions ρq > 2(1 + B) and t ≤ ρq/4 make this bound smaller than the required ρq points.

MGL checked that the integer condition ⌈ρq⌉ > 1 + B + 2⌊ρq/4⌋ gives the same contradiction for this step. With q = 11, B = 2, and ρ = 6/11, the upper bound is five points and six are required. This numerical example identifies the boundary of the local count.

## Open scope

The manuscript’s prime threshold is existential. Counterexample constructions at the small primes tested, improvement of the prime threshold using the refinement, independent third-party review or replication, human peer review, a comprehensive literature review, and Lean execution by MGL remain unperformed. OpenAI’s scope note describes the formalization corresponding to the balanced main theorem.

## Sources and citation

- [OpenAI’s pinned source paper (PDF)](https://github.com/openai/math/blob/4eaee87548250b2682affda7d05d947c05554bae/preprints/Balanced-Counterexamples-to-Rysers-Conjecture-at-Prime-Orders-September-27-2026/paper.pdf)
- [OpenAI’s Lean scope note at the same commit](https://github.com/openai/math/blob/4eaee87548250b2682affda7d05d947c05554bae/lean/docs/162.md)
- [Szőnyi and Weiner, Theorem 2.4, cited in the manuscript](https://real.mtak.hu/13831/1/stabprimfinal.pdf)

Suggested citation. Masao Gate Labs (2026). Technical review of the balanced Ryser counterexamples. OpenAI Math Family 162, published version v0.1.0, MGL-REF-013.
