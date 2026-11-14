# Technical review of the Sidorenko counterexample

Masao Gate Labs · OpenAI Math Family 161 · Published version v0.1.0 · 2026-11-14 JST · MGL-REF-012

## Scope and review result

MGL reviewed Theorem 1.1, Corollaries 1.2 and 1.3, and their proof dependencies in the pinned OpenAI manuscript dated September 23, 2026. MGL completed its internal technical review and found no defect overturning the conclusions within the reviewed scope.

| Source location | What MGL checked |
| --- | --- |
| Theorem 1.1 (p. 1, §§3–7) | For the bipartite graph H with 35 vertices and 66 edges, a finite simple host G exists in which the homomorphism density of H is below the 66th power of the edge density. |
| Corollary 1.2 (p. 5, proof on pp. 47–48) | Tensor powers make the normalized density ratio arbitrarily small. Balanced blow-ups and a collision bound preserve a fixed relative deficit of injective copies at a positive limiting edge density. |
| Corollary 1.3 (p. 6, proof on pp. 48–49) | Interpolation between two kernels of edge density p yields a nonconstant graphon with H-density equal to the 66th power of p. Its four-cycle density exceeds the fourth power of p, and one finite graph sequence approximates all three densities simultaneously. |

## General argument for the main theorem

MGL checked how sign correlations over finite fields create a density deficit, and how dilution and symmetrization lead to the existence of a finite simple graph. A small probability of singular matrix differences alone does not control their weighted contribution. MGL traced the move to Lagrangian subspaces, local counting, and the bound for singular configurations in §§4–7. The argument fixes a sufficiently large even dimension D before taking the prime q large.

## Earlier checks and finite computations

| Check | Evidence |
| --- | --- |
| Color refinement in Proposition 2.1(4) (§2) | Direct updates on the incidence graph of 13 points and 22 faces gave 13 point colors and seven face colors after round three. Round four gave 13 point colors and 22 face colors, the first round distinguishing all 35 vertices. |
| Earlier check of Corollary 1.3 (§8) | Taking the main theorem as input, MGL checked the sign kernel with higher H-density at the same edge density, the nonconstancy of the interpolated kernel, and the strict four-cycle excess. The full review then checked the main theorem on which that argument depends. |
| Small singular-case check | At q = 3 and D = 2, MGL counted 40 Lagrangian subspaces and 64,000 ordered triples and checked the distribution after fixing a pair. The general asymptotic bound was examined in the manuscript’s proof. |

## MGL’s refinement and open scope

For the passage to finite graphs in Lemma 3.6, the paper’s absolute error bound is 595/n. MGL examined a one-sided refinement. A collision between adjacent vertices requires a loop and cannot contribute positively to a homomorphism into a simple graph. Only the 529 nonadjacent pairs can contribute collisions on the upper side, giving the bound 529/n for that side.

The finite counterexample was checked as an existence proof. Explicit adjacency data, independent third-party review or replication, human peer review, a comprehensive literature review, and Lean execution by MGL remain unperformed. OpenAI’s formalization scope includes the main counterexample. It excludes the forcing-conjecture consequence in Corollary 1.3.

## Sources and citation

- [OpenAI’s pinned source paper (PDF)](https://github.com/openai/math/blob/4eaee87548250b2682affda7d05d947c05554bae/preprints/A-counterexample-to-Sidorenkos-conjecture-September-23-2026/paper.pdf)
- [OpenAI’s Lean scope note at the same commit](https://github.com/openai/math/blob/4eaee87548250b2682affda7d05d947c05554bae/lean/docs/161.md)

Suggested citation. Masao Gate Labs (2026). Technical review of the Sidorenko counterexample. OpenAI Math Family 161, published version v0.1.0, MGL-REF-012.
