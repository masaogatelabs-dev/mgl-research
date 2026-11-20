# Comparing fallback candidate balls across independent implementations of Family 266

Masao Gate Labs | Supplement to the Family 266 technical review v0.2.0 | Initial comparison, 20 November 2026 JST

[日本語](Family266-Independent-Implementation.md) · **English**

**Follow-up, 20 November 2026.** We traced the six remaining cases and checked coverage under the Hadamard condition. [Follow-up verification](Family266-Coverage-Followup.en.md)

We compared the 163 unresolved records from the initial Stage C pass in OpenAI's published computation, as reproduced by MGL, with the 43 unresolved records from the implementation that maximusrufus and colleagues built from the paper's text. We allowed row and column permutations, transpose and complex conjugation, and measured distances after removing row and column phase offsets. **All 43 centers from the independent implementation lay inside at least one candidate ball from the published computation.** [MGL's replay](https://github.com/masaogatelabs-dev/mgl-research/blob/41bd45f6d3697cf864198d39e646b8ff4eca8ace/themes/math-proof-review/Family266.en.md#review-04) · [Independent data and discussion](https://github.com/google-deepmind/formal-conjectures/issues/6918#issuecomment-7016254568)

| Item | Published computation | Independent implementation |
| --- | ---: | ---: |
| Records passed from the initial Stage C to fallback | 163 | 43 |
| Batches containing those records | 15 | 5 |
| Balls with a witnessed overlap with a ball from the other run | 157 | 43 |
| Records whose centers fell in a ball from the other run | 134 | 43 |
| Balls with no overlap found in this search | 6 | 0 |

The search examined 7,009 cross-run pairs and found 2,217 pairs with a verified overlap. These measurements concern balls in horizontal phase space. Establishing coverage of entire balls, the outcome of the exclusion tests, or the presence of a common exact solution requires separate checks.

## Inputs and method

We read 20 <code>bad*.bin</code> files from pinned commits, matching their Git blob IDs. We also checked the five files from the independent implementation against the SHA-256 manifest. We checked record counts and boundaries, the bounds on phase values and radii, and end of file. All 206 records stored the same binary64 radius <code>0.016</code> and tangent-space dimension four. [Published batch data](https://github.com/openai/math/tree/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026/verification/saved-run/execution/data/batches) · [Independent batch data](https://github.com/maximusrufus/mub6-certified-rerun/tree/ad961ac581c92eb3186f8c2fcb10af61223a7173/certificates/batches) · [Independent SHA-256 manifest](https://github.com/maximusrufus/mub6-certified-rerun/blob/ad961ac581c92eb3186f8c2fcb10af61223a7173/certificates/MANIFEST.txt)

The 15 nonempty batches from the published computation were 3, 4, 5, 6, 7, 8, 10, 52, 53, 55, 56, 78, 79, 80 and 84. The independent batches were 20, 29, 32, 35 and 60, with 1, 8, 26, 1 and 7 records, respectively.

1. We took the phase centers as $6\times6$ matrices $P,Q$. We applied the row and column permutations, transpose and phase negation for complex conjugation to the independent center $Q$. We dephased both matrices relative to the first row and first column.
2. We aligned the phase differences by integer turns, using one turn as the unit, then projected onto horizontal phase space with $\Pi$. The projection subtracts the row and column means and adds the grand mean.
3. We compared the squared Frobenius norm $\|\Pi(D_0Q-D_0P-N)\|_F^2$ with the squared sum of the two radii. Here $D_0$ is dephasing and $N$ is the chosen matrix of integer turns. For center inclusion we used the square of the receiving ball's radius. We searched for candidate alignments in binary64 and checked the positive results in exact rational arithmetic on the stored values. [Alignment in the published code](https://github.com/openai/math/blob/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026/verification/saved-run/compiled-build/source/atlas.cpp) · [Independent phase displacement](https://github.com/maximusrufus/mub6-certified-rerun/blob/ad961ac581c92eb3186f8c2fcb10af61223a7173/impl/stageBC/common.hpp) · [Independent symmetry maps](https://github.com/maximusrufus/mub6-certified-rerun/blob/ad961ac581c92eb3186f8c2fcb10af61223a7173/impl/stageBC/phi.hpp)

The search pruned alignments using alternating sums on $2\times2$ submatrices. The projection preserves those sums, so a displacement within distance $\rho$ has alternating sums bounded in absolute value by $2\rho$. The floating-point comparisons used a tolerance of $10^{-10}$. Moving the dephasing row and column anchors recovered the same 2,217 pairs.

## Worked example and the six remaining balls

Take record 26 of <code>bad52.bin</code> in the published data and record 6 of <code>bad32.bin</code> in the independent data, both zero-based. Conjugate the independent center, then select rows in order <code>[0,1,3,4,2,5]</code> and columns in order <code>[5,4,3,2,1,0]</code>. With <code>N = [[0,0,0,0,0,0],[0,2,1,1,2,1],[0,1,1,1,2,2],[0,1,0,0,1,1],[0,0,0,0,1,1],[0,1,1,0,1,1]]</code>, the squared distance is exactly

$$
\frac{600065447762334584904721496619163}{255211775190703847597530955573826158592}.
$$

The distance is about 0.001533377, below the radius 0.016 of either ball.

For the six published balls with no overlap found, we extended the search to a center distance of 0.08. The table gives the nearest alignments found by that search. Distances are rounded from squared distances checked with rational arithmetic. The sum of the radii is about 0.032.

| Record in the published data | Record in the independent data | Center distance |
| --- | --- | ---: |
| <code>bad6.bin</code>, index 0 | <code>bad35.bin</code>, index 0 | 0.033615 |
| <code>bad6.bin</code>, index 2 | <code>bad29.bin</code>, index 0 | 0.033647 |
| <code>bad7.bin</code>, index 1 | <code>bad35.bin</code>, index 0 | 0.041242 |
| <code>bad7.bin</code>, index 3 | <code>bad29.bin</code>, index 0 | 0.056786 |
| <code>bad8.bin</code>, index 1 | <code>bad29.bin</code>, index 0 | 0.050027 |
| <code>bad10.bin</code>, index 0 | <code>bad35.bin</code>, index 0 | 0.033047 |

The stage and conditions under which the independent implementation handled the regions of these six balls remain open in this comparison. At the seed stage, the independent team reports that a diagnostic run with the paper's margins recovered the paper's 151,744,086 pairs. [Seed-stage decisions](https://github.com/maximusrufus/mub6-certified-rerun/blob/ad961ac581c92eb3186f8c2fcb10af61223a7173/impl/seed/DECISIONS.md)

[Family 266 technical review v0.2.0](https://github.com/masaogatelabs-dev/mgl-research/blob/41bd45f6d3697cf864198d39e646b8ff4eca8ace/themes/math-proof-review/Family266.en.md)
