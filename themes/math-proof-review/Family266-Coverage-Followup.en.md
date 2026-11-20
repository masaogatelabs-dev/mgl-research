# Family 266 follow-up — tracing six cases and covering their Hadamard points

Masao Gate Labs | Supplement to the Family 266 technical review v0.2.0 | Verification date 20 November 2026 JST

[日本語](Family266-Coverage-Followup.md) · **English**

We examined six balls from the published computation that entered fallback. Each ball contained a point outside all of the independent implementation's initial Stage C balls. **Under the local bounds of the published Root certificates, every point satisfying the Hadamard condition in any of the six balls is covered by the independent implementation's initial Stage C balls.** All six points found outside the cover failed row orthogonality. [Initial comparison](https://github.com/masaogatelabs-dev/mgl-research/blob/634e42c75b827087b06da528c435e74c0bdb604c/themes/math-proof-review/Family266-Independent-Implementation.en.md) · [Local bounds in the paper](https://github.com/openai/math/blob/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026/build/sections/phase-cover.tex)

## 01 Six remaining cases in the initial comparison

We compared the 163 records sent to fallback by the initial Stage C of OpenAI's published computation with the 43 records from the independent implementation built from the paper by maximusrufus and colleagues. Allowing row and column permutations, transpose, conjugation and phase alignment, we found that all 43 independent centers lay in published balls. Of the published balls, 157 overlapped an independent fallback ball. The search found no fallback overlap for six balls. One possibility at that point was that the independent implementation had handled the six cases earlier. [Independent data and discussion](https://github.com/google-deepmind/formal-conjectures/issues/6918#issuecomment-7016254568) · [Initial comparison and list of six](https://github.com/masaogatelabs-dev/mgl-research/blob/634e42c75b827087b06da528c435e74c0bdb604c/themes/math-proof-review/Family266-Independent-Implementation.en.md)

## 02 Exact rational checks of the correspondences

The independent team identified the six correspondences in the Stage B refinement output <code>fine.bin</code>. The batch writer splits that file's insertion order into groups of 256, so the quotient and remainder gave the Stage C input file and position. The batch writer sets the Stage C input radius to 0.016. We read the stored binary64 values as exact dyadic rationals and compared squared distances after phase alignment. All six published centers lay inside the indicated Stage C balls. Distances agreed with the independent team's report to six decimal places. [Independent team's follow-up](https://github.com/google-deepmind/formal-conjectures/issues/6918#issuecomment-7030043886) · [Batch writer](https://github.com/maximusrufus/mub6-certified-rerun/blob/ad961ac581c92eb3186f8c2fcb10af61223a7173/impl/stageBC/brun.cpp)

| Published record (zero-based) | Independent fine.bin index | First Stage C input and index | Center distance (approx.) |
| --- | --- | --- | --- |
| bad6.bin, #0 | 9142 | f35.bin, #182 | 0.007663919 |
| bad6.bin, #2 | 7552 | f29.bin, #128 | 0.001926635 |
| bad7.bin, #1 | 9142 | f35.bin, #182 | 0.006776854 |
| bad7.bin, #3 | 10217 | f39.bin, #233 | 0.006347020 |
| bad8.bin, #1 | 9130 | f35.bin, #170 | 0.002127197 |
| bad10.bin, #0 | 9142 | f35.bin, #182 | 0.008265086 |

The six correspondences use four distinct records. All four were marked <code>NEGATIVE(graph)</code> in the public logs of the initial Stage C pass. This established that the centers lay inside balls eliminated by the graph check. The next question was whether the union of the independent balls covered each entire published ball. [c29.log](https://github.com/maximusrufus/mub6-certified-rerun/blob/ad961ac581c92eb3186f8c2fcb10af61223a7173/certificates/batches/c29.log) · [c35.log](https://github.com/maximusrufus/mub6-certified-rerun/blob/ad961ac581c92eb3186f8c2fcb10af61223a7173/certificates/batches/c35.log) · [c39.log](https://github.com/maximusrufus/mub6-certified-rerun/blob/ad961ac581c92eb3186f8c2fcb10af61223a7173/certificates/batches/c39.log)

## 03 Geometric coverage of the full balls

We checked the SHA-256 manifest for all 61 initial Stage C batches and compared all 15,595 balls. Let $R$ be the exact rational value of the stored binary64 radius 0.016. We measured horizontal phase displacements after dephasing and subtracting integer turns. We considered row and column permutations, transpose and complex conjugation. [Stage C inputs](https://github.com/maximusrufus/mub6-certified-rerun/tree/ad961ac581c92eb3186f8c2fcb10af61223a7173/certificates/batches) · [SHA-256 manifest](https://github.com/maximusrufus/mub6-certified-rerun/blob/ad961ac581c92eb3186f8c2fcb10af61223a7173/certificates/MANIFEST.txt) · [Phase displacement](https://github.com/maximusrufus/mub6-certified-rerun/blob/ad961ac581c92eb3186f8c2fcb10af61223a7173/impl/stageBC/common.hpp) · [Symmetry maps](https://github.com/maximusrufus/mub6-certified-rerun/blob/ad961ac581c92eb3186f8c2fcb10af61223a7173/impl/stageBC/phi.hpp)

A center that can reach a published ball must be at most $2R$ away. Horizontal projection preserves each anchored $2\times2$ alternating sum, whose absolute value is at most twice the center distance. Since $4R<1/2$ turn, the nearest integer turn is unique in each entry for every nearby alignment. We scaled phases by $D=2^{40}$ and rounded them to integers for the screening comparisons. We allowed $4/D$ for error in the anchored $2\times2$ alternating sums and $24/D$ for error in the projected norm. We checked all 3,856 nearby alignments using the exact stored values. We found a point strictly inside each published ball and outside every independent ball.

To obtain each point, displace the four indicated entries, with alternating signs and magnitude $9999R/20000$ per entry. The top-left sign is shown below. The indices are zero-based. All other entries have zero displacement, so the full displacement has length $9999R/10000$. The last column gives the least excess of the point's squared distance to a nearby center over $R^2$.

| Published record (zero-based) | Rows | Columns | Top-left sign | Nearby balls | Nearby alignments | Smallest squared distance minus squared radius (approx.) |
| --- | --- | --- | --- | --- | --- | --- |
| bad6.bin, #0 | [0, 3] | [1, 2] | + | 141 | 621 | 6.24484392e-05 |
| bad6.bin, #2 | [4, 5] | [0, 4] | − | 109 | 658 | 2.02411209e-05 |
| bad7.bin, #1 | [3, 5] | [3, 5] | + | 98 | 650 | 6.66963372e-05 |
| bad7.bin, #3 | [2, 5] | [3, 5] | + | 103 | 616 | 5.31183035e-05 |
| bad8.bin, #1 | [2, 5] | [3, 4] | + | 66 | 669 | 1.85826762e-05 |
| bad10.bin, #0 | [2, 5] | [0, 4] | + | 104 | 642 | 8.35263307e-05 |

This left the question of whether the uncovered part contained a point satisfying the Hadamard condition.

## 04 Row orthogonality at the six uncovered points

For a phase matrix $p$, put $H_{ij}=\exp(2\pi\mathrm{i}p_{ij})$. The Hadamard condition requires the real and imaginary parts of every inner product of distinct rows to vanish. We bounded $\pi$ using Machin's formula and alternating arctangent series, then used Taylor polynomials with rational remainder bounds for sine and cosine. For each of the six points, at least one component had an enclosure excluding zero.

| Published record (zero-based) | Row pair | Inner product component | Rational enclosure (rounded outward) |
| --- | --- | --- | --- |
| bad6.bin, #0 | (0, 3) | imaginary | [-0.200677786860, -0.200677786859] |
| bad6.bin, #2 | (4, 5) | imaginary | [0.173349277514, 0.173349277515] |
| bad7.bin, #1 | (3, 5) | imaginary | [0.147461199995, 0.147461199996] |
| bad7.bin, #3 | (2, 5) | real | [-0.126229290581, -0.126229290580] |
| bad8.bin, #1 | (2, 5) | imaginary | [0.181614668218, 0.181614668219] |
| bad10.bin, #0 | (2, 5) | real | [-0.174375895661, -0.174375895660] |

None of the six points satisfies row orthogonality. We next checked coverage on a region that contains all points satisfying the Hadamard condition in each published ball.

## 05 From a tangent-space sample to a check of all cells

A stored Root certificate has a center $P$ and a $36\times4$ tangent matrix $T$. For a horizontal displacement $\delta$ with $\|\delta\|\le R$ satisfying $F(P+\delta)=0$, the paper sets $\eta=T^\top\delta$ and gives the following bound. [Root certificates in the paper](https://github.com/openai/math/blob/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026/build/sections/phase-cover.tex)

$$
\|\delta-T\eta\|\le \mathtt{n0}+\mathtt{id}\,R+\mathtt C R^2.
$$

An exploratory sample used 30,000 directions on each tangent sphere. The maximum distance from a sample point to its nearest independent center ranged from about 0.00973 to 0.01069 across the six cases. This suggested that coverage could hold even after allowing a displacement away from the tangent space. The final check covered all applicable cells, including the regions between sample points.

## 06 Coverage of points satisfying the Hadamard condition

For all six stored certificates, the right-hand side of the Root bound was less than the rational value $n=0.001121$. An exact Frobenius norm check of $T^\top T-I$ gave $\|T\|<\beta=1.00001$, hence $\|\eta\|<0.016001$. We subdivided $[-1/32,1/32]^4$, which contains all such $\eta$. For a cell with midpoint $m$ and coordinate half-width $h$, $\|\eta-m\|\le 2h$ throughout the cell. [MGL's review of the stored certificates](https://github.com/masaogatelabs-dev/mgl-research/blob/41bd45f6d3697cf864198d39e646b8ff4eca8ace/themes/math-proof-review/Family266.en.md#review-08)

For a phase-aligned independent center with displacement $v$, we checked $R-n-2\beta h>0$ and the following inequality in exact rational arithmetic.

$$
\|Tm-v\|^2 \le (R-n-2\beta h)^2.
$$

The triangle inequality then gives $\|\delta-v\|\le R$. We discarded cells whose minimum distance from the origin exceeded 0.016001. Floating point selected a ball to try for a cell. Exact rational comparisons determined the result for each cell.

| Published record (zero-based) | Covered terminal cubes | Terminal cubes outside the bound | Distinct independent records used | Smallest squared slack (approx.) |
| --- | --- | --- | --- | --- |
| bad6.bin, #0 | 746 | 1,490 | 68 | 1.71101083e-07 |
| bad6.bin, #2 | 645 | 1,606 | 53 | 6.63215623e-08 |
| bad7.bin, #1 | 718 | 1,653 | 50 | 1.81726140e-07 |
| bad7.bin, #3 | 823 | 1,788 | 55 | 1.38092367e-07 |
| bad8.bin, #1 | 651 | 1,675 | 42 | 1.48349693e-07 |
| bad10.bin, #0 | 736 | 1,515 | 55 | 3.36353594e-07 |

Across the six cases, 4,319 terminal cells were covered and 9,727 lay outside the required region. No undecided cells remained. The maximum subdivision depth was four. The conclusion, under the published local certificate bounds, covers all Hadamard points in these six balls by the independent implementation's initial Stage C inputs. The existence of additional mutually unbiased bases and a rerun of the graph checks for every covering record are outside this computation's scope. [Published fallback data](https://github.com/openai/math/tree/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026/verification/saved-run/execution/data/batches)

We thank maximusrufus and colleagues for releasing their implementation and intermediate data and for locating the six correspondences. [Initial comparison](https://github.com/masaogatelabs-dev/mgl-research/blob/634e42c75b827087b06da528c435e74c0bdb604c/themes/math-proof-review/Family266-Independent-Implementation.en.md) · [GitHub discussion](https://github.com/google-deepmind/formal-conjectures/issues/6918)
