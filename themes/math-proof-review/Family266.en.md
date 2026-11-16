# At most three mutually unbiased bases in complex dimension six — Family 266 technical review

Masao Gate Labs | Family 266 | English edition v0.2.0 | MGL-MATH-008 · MGL-REF-015  
Overall assessment 14 November 2026 (JST) · Revised edition published 16 November 2026 (JST)

## Review verdict

**MGL’s technical review supports Theorem 1.1, which states that there are at most 3 mutually unbiased bases in complex dimension 6.** We verified the existence of 3 bases using exact arithmetic and reproduced the published computation that rules out a 4th, from the initial cover to the final decision, under the paper’s stated double-precision conditions.

| Review record | Details |
| --- | --- |
| Reviewer | Chappie 3 (MGL AI technical reviewer) |
| Model used | GPT-6.1-Sol (as recorded by Masao) |

Two orthonormal bases are mutually unbiased if the squared magnitude of the inner product of any vector from one basis with any vector from the other is $1/6$. We separately verified the construction of 3 bases and the paper’s computation that covers the candidate region and rules out a 4th basis.

**163 cases remained after the initial search.** Of the 22,379 records processed in the initial run of stage C, 163 reached the search cap and remained unresolved. The region represented by those 163 records was covered again with 1,127 smaller candidate balls. The final run of C processed all of them, leaving 0 unresolved cases. [Refinement and final stage C](#review-04) · [Reproduction instructions and output hashes](#reproduce)

**Meaning of “supports”**  MGL found no issue that overturns the conclusion within the review scope and verification methods described here. We reviewed the 24 September 2026 OpenAI preprint *The maximum number of mutually unbiased bases in dimension six* and its public computational materials at commit <code>42907c9e999cc00d6abe7a50bfc1023250edd1b9</code>. The manuscript PDF’s SHA-256 is <code>b4cc74c840c902494d589b51c8e9706490f37cf2735e69a0486122131c6b7446</code>. [Original manuscript PDF](https://github.com/openai/math/blob/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026.pdf) · [Pinned replay instructions](https://github.com/openai/math/blob/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026/verification/saved-run/VERIFY.md)

**OpenAI’s public materials**  Along with the paper, OpenAI published the numerical source code, saved data from each stage, and replay instructions. These materials let readers trace the inputs and see how candidates that reached the search cap were passed on to the next stage. The same public materials were the starting point for MGL’s replay and its separate high-precision cross-checks. [OpenAI’s paper and computational materials](https://github.com/openai/math/tree/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026)

**Scope of review**  We reran the pinned C++ implementation on Linux x86-64 with GCC 14.2.0. The arithmetic assumptions were IEEE 754 binary64 round-to-nearest, correctly rounded square roots, and no fused multiply-add (FMA). Separate calculations checked the phase residuals and matrix conditions that certify the saved candidate balls. For candidate balls used only during execution, we relied on the code’s acceptance conditions and uniform error bounds. A full formal proof of the main theorem was outside the review scope. The public Lean material we consulted establishes an upper bound of 5 bases. MGL’s verdict on the upper bound of 3 bases rests on the mathematical checks and numerical replay described below. [Scope of the Lean verification](https://github.com/openai/math/blob/42907c9e999cc00d6abe7a50bfc1023250edd1b9/lean/docs/266.md)

**Publication scope**  To let readers follow up from the original sources, we report the assumptions, formulas, conditions, observations, and grounds for the verdict. MGL maintains its internal search and verification-order algorithms and work logs internally.

## Order of the review and who did what

Masao requested review of papers discussed on the forum. For Family 266 he directed a comparison of the paper’s double-precision results with cross-checks using the MGL High-Precision Engine and asked that verification continue. The account below reconstructs the checks, assessments, and next tasks in the order they were reported. Opening remarks for individual steps and the origin of each question are given where the record establishes them. Interpretive notes are retrospective and draw on the reports and results from the time.

**Decisions within the review and how it was completed**  The reports show that after 640 comparisons agreed with the stage C decisions, verification extended to uniform error bounds and upstream coverage. The full replay of stage A then connected the stages required by Theorem 7.1 through the final run of C using the same numerical records. That connection supported the overall assessment. [Step 05](#review-05) · [Step 06](#review-06) · [Step 08](#review-08)

| Report order | Scope checked | Assessment at the time and open work |
| --- | --- | --- |
| [01](#review-01) | Existence of 3 bases, initial cover, and a sampled replay of stage C | Lower bound of 3 confirmed. Upper bound of 3 pending. |
| [02](#review-02) | Coverage in stages A and B, search-cap handling, and a report of non-finite values | Coverage handoff checked on a sample. An end-to-end replay of all cases remained. |
| [03](#review-03) | 600 numerical records and 144 near-threshold comparisons for Equation (6.7) | Comparisons agreed. Later shards and error bounds remained open. |
| [04](#review-04) | All shards of the initial run of C, further refinement, and 48 comparisons for Equation (6.11) | Replayed from the intermediate records through final C. Regenerating the intermediate records remained open. |
| [05](#review-05) | 448 comparisons for Equation (6.12) and vector pairs, and complex exponential error | 640 near-threshold comparisons in total. Uniform error bounds came next. |
| [06](#review-06) | Uniform error bounds for 10 types of stage C rejection comparisons and for ball radii | The errors were within the margins under the stated input conditions. Coverage in stages A and B remained open. |
| [07](#review-07) | Initial refinement in stage B and 3,683 certificates | Connected stage A output through final C. The full stage A replay remained open. |
| [08](#review-08) | All of stage A, the full set of saved certificates, and the overall assessment | Connected the initial cover through final C and supported Theorem 1.1. |

In the proof, the upper-bound computation proceeds alongside the construction of 3 bases, from the initial cover to stage A, stage B, initial C, further refinement of unresolved cases, and final C. The review checked the downstream stages first using published intermediate outputs, then replayed the upstream stages and matched them to those same data.

<a name="review-01"></a>

## 01 Existence of 3 bases and the initial cover

**Task and assumptions.** We examined the construction in Lemma 1.2 and the initial cover in Section 2 of the paper. With the first basis fixed as the standard basis, the second can be represented by a normalized complex Hadamard matrix. Starting from $I,U$, apply $U^*$ to all bases, swap the first two, and take entrywise conjugates to obtain $I,U^{\mathsf T}$. The magnitudes of inner products are preserved, so transposition preserves extendibility to 4 bases.

**Checks and results.** We constructed 3 bases each in dimensions 2 and 3 and took tensor products of corresponding bases. In dimension 3, $\omega^3=1$ and $1+\omega+\omega^2=0$ give $|1+2\omega|^2=|2+\omega^2|^2=3$. The squared magnitudes of cross-basis inner products are then $(1/2)(1/3)=1/6$. For the initial cover we checked the phase ordering and closed-interval endpoints in Lemma 2.4 and verified the distance bounds for the 9-dimensional boxes in Lemma 2.9 using rational arithmetic. The initial-cover program produced 249,878 centers from 151,744,086 pairs of intervals. The saved file matched the public copy. [Paper, Lemmas 1.2, 2.2, 2.4 and 2.9 and Proposition 2.10](https://github.com/openai/math/blob/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026.pdf)

**Assessment at the time and next task.** The existence of 3 bases was confirmed. The upper bound of 3 remained open. The next task was to check whether stages A and B carry over every candidate in the initial cover. [Continue to step 02](#review-02)

<a name="review-02"></a>

## 02 Preserving coverage and handling the search cap

**Task and assumptions.** From each center, stage A covers possible completions with closed cells in $U(2)$. Stage B reuses a parent ball’s result for later coverage only when the parent was successfully covered. For a merged ball to contain the original ball, a sufficient radius is the sum $r+d$ of the original radius $r$ and the upper bound $d$ on the distance between the centers under the equivalence transformation actually used.

**Checks and results.** A 64-case sample from stage A produced 315 balls and 0 unresolved cases. Passing 12 of those balls to a stage B sample produced 330 balls and 0 unresolved cases. We also examined a report of non-finite values in the public code. At 3 sites we checked the input ranges and nonnegativity of the quantities involved in taking square roots for squared box distances, cluster distances, and edge comparisons. Within the public runs examined we did not reproduce NaNs reaching these 3 sites. [Paper, Lemma 4.15, Propositions 4.16 and 5.7, and Appendix A.9–A.12](https://github.com/openai/math/blob/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026.pdf) · [External code review](https://github.com/kusasyu36/openai-math-audit)

**Assessment at the time and next task.** The sampled cases preserved coverage. The upper bound of 3 remained open. We planned to check how rounding affects rejection decisions and replay the remaining shards. [Continue to step 03](#review-03)

<a name="review-03"></a>

## 03 Public intermediate records and 144 comparisons for Equation (6.7)

**Task and assumptions.** We checked double-precision rejection decisions near the threshold using a separate high-precision calculation. Saved binary64 values were read as exactly equivalent rationals. Comparison differences were oriented so that a positive value meant rejection.

**Checks and results.** In the 600 public intermediate records, the phase residual and the deviation from orthogonality of the tangent columns both stayed within their saved bounds. The maximum absolute differences between the double-precision and high-precision calculations were $1.281\times10^{-16}$ and $4.631\times10^{-16}$, respectively. We selected 6 records each from 2 shards of initial C and from the further-refinement output, and extracted near-threshold comparisons on both sides of rejection for the 3 variants of Equation (6.7). All 144 comparisons gave matching decisions. In the closest case, the first record of the further-refinement output, the high-precision enclosure for the comparison difference was $[1.664563697533116274232730,1.664563697533116274232731]\times10^{-10}$, entirely on the rejection side. [Paper, Equation (6.7) and Appendix A.10](https://github.com/openai/math/blob/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026.pdf) · [Case study of the MGL High-Precision Engine](https://github.com/masaogatelabs-dev/mgl-research/blob/df333e12c9f43b1f402c61902d7da7c2681fdaf4/reports/precision-engine/MGL-High-Precision-Engine-Family266.en.md)

**Assessment at the time and next task.** The intermediate records and the sampled comparisons checked out. The next tasks were to finish replaying initial C and to cross-check its directional necessary condition. [Continue to step 04](#review-04)

<a name="review-04"></a>

## 04 All shards of initial C and 48 directional comparisons

**Task and assumptions.** Starting with the public intermediate records, we checked output counts, order, and bytes to see whether every candidate that reached the search cap in initial C was carried forward. For the directional test in Equation (6.11), we held fixed the finite direction vectors selected by the public code.

**Checks and results.** We added the remaining 14 shards to the 74 reported earlier, processing all 22,379 records in 88 shards. The 163 capped cases came from 15 shards and appeared in the unresolved output with the same bytes and relative order as in the input. Refining these 163 output records produced 1,127 records. The 4 shards of final C ended with 0 unresolved cases. All 48 near-threshold comparisons for Equation (6.11) gave the same decisions at high precision and double precision. [Paper, Equation (6.11) and Section 7](https://github.com/openai/math/blob/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026.pdf) · [Pinned replay instructions](https://github.com/openai/math/blob/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026/verification/saved-run/VERIFY.md)

**Assessment at the time and next task.** We reproduced the chain from the public intermediate records through final C. The upper bound of 3 remained open while we worked on regenerating the intermediate records and establishing general error bounds. [Continue to step 05](#review-05) · [Step 07 on regenerating the intermediate records](#review-07)

<a name="review-05"></a>

## 05 A further 448 comparisons and how a margin can retain a candidate

**Task and assumptions.** We added the single-vector comparison in Equation (6.12) and the vector-pair comparisons in Equations (6.16), (6.20), (6.21), and (6.23). In addition to the 3 input groups reported earlier, we selected unresolved records from the 15 initial C shards containing cases that reached the search cap and sampled near-threshold cases on both sides of rejection.

**Checks and results.** All 448 additional high-precision comparisons agreed. Together with the earlier 144 and 48, this brought the total to 640. The separate calculation used rational arithmetic and enclosing intervals for pi and some square roots from the MGL High-Precision Engine. Trigonometric and intermediate interval operations used MPFR with directed rounding at 320-bit precision.

**Analysis and targeted cross-check.** For the mutual-unbiasedness condition in Equation (6.23), we examined the comparison between balls 159 and 156 at index 204 (zero-based) of <code>f84.bin</code>. With the margin included, the difference was $[-2.12200308140,-2.12200308139]\times10^{-9}$, so the candidate was retained. Keeping the same centers and radii and removing only that comparison margin gives $[3.18507737692,3.18507737693]\times10^{-7}$, on the rejection side. This isolated the reason the comparison retained the candidate. A rational-arithmetic bound for the complex exponential approximation, including formation of its argument in stage C, was below $2\times10^{-14}$. [Paper, Equations (6.12), (6.16) and (6.20)–(6.23), and Appendix A.2](https://github.com/openai/math/blob/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026.pdf) · [Pinned stage C code](https://github.com/openai/math/blob/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026/verification/saved-run/compiled-build/source/stageC.cpp)

**Assessment at the time and next task.** No rounding-related decision reversals were found in the 640 comparisons. The next task was to establish error bounds for safe rejection over the specified input range. [Continue to step 06](#review-06)

<a name="review-06"></a>

## 06 Uniform error bounds for stage C

**Task and assumptions.** We bounded arithmetic errors for the code ranges examined, using valid candidate-ball certificates as input. The conditions included grid subdivision count $6\le M\le1024$, saved phases $|P_{ji}|\le4$, Hadamard-side radius $r\le0.03$, and candidate-vector ball radius $s<0.1$.

**Checks and results.** We allocated $2\times10^{-16}|z|+10^{-300}$ for rounding in one elementary operation. Given magnitude bounds $A,B$ and respective error bounds $e_A,e_B$, we bounded the error in their product by $Ae_B+Be_A+e_Ae_B$ plus rounding in the product itself. For 10 types of rejection comparisons, following Appendices A.10 and A.11 and the code, the largest error bound was below $8\times10^{-12}$. The code’s comparison margins were $2\times10^{-7}$ or $3\times10^{-7}$. For a ball radius used to group candidates, the error bound was below $3\times10^{-13}$ and within the additive margin of $10^{-9}$. [Paper, Appendices A.10 and A.11](https://github.com/openai/math/blob/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026.pdf) · [Pinned stage C code](https://github.com/openai/math/blob/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026/verification/saved-run/compiled-build/source/stageC.cpp)

**Why the comparison margin works.** Let $d$ be the exact real comparison difference before subtracting the margin, $m$ the specified margin, and $\widehat{\Delta}$ the difference computed by the code with the margin included. Our error bound $E$ gives $|\widehat{\Delta}-(d-m)|\le E$. When the code rejects, $\widehat{\Delta}>0$ and hence $d>m-E$. Since $E<m$, the exact real difference is positive.

**Assessment at the time and next task.** Under the specified inputs and arithmetic conditions, the margins checked suffice to prevent false rejection due to rounding in the comparisons examined. We next returned to stages A and B to check the validity of the certificates used as input to stage C. [Continue to step 07](#review-07)

<a name="review-07"></a>

## 07 Initial refinement in stage B and 3,683 certificates

**Task and assumptions.** We checked whether the stage B intermediate records could be regenerated from the saved stage A outputs. A candidate-ball certificate (Root) contains a center $P$, tangent-space columns $T$ for local displacement, and their error bounds. For auxiliary matrices omitted from the public records, we constructed candidates and checked the paper’s sufficient conditions separately.

**Checks and results.** With all 3,083 stage A balls as input, we regenerated 600 intermediate records and obtained 0 unresolved cases. The intermediate file matched the input of step 04 byte for byte. For the saved 3,083 and 600 records, 3,683 in all, we checked phase residuals using directed rounding and used dyadic rational and multiprecision integer arithmetic to check the tangent-column conditions and auxiliary-matrix bounds. All passed. For 97 cases in which the initial auxiliary-matrix candidate did not satisfy the remainder-constant condition, we used transposition, as permitted by Lemma 4.7, to propose another candidate and verify the sufficient condition. [Paper, Lemmas 4.4 and 4.7 and Propositions 4.5 and 5.7](https://github.com/openai/math/blob/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026.pdf)

**Assessment at the time and next task.** The replay connected the saved stage A output through final C. The upper bound of 3 remained open while we prepared to replay all of stage A with the 249,878 initial centers and check the error bounds used for coverage of candidate cells. [Continue to step 08](#review-08)

<a name="review-08"></a>

## 08 Full stage A replay and overall assessment of the main theorem

**Task and assumptions.** We replayed the 4 stage A shards from the initial cover and checked whether candidates were rejected, covered, or left unresolved. We also checked the bytes passed to the next stage.

**Checks and results.** All 249,878 initial centers were processed. The shards produced 764, 774, 757, and 788 records, for a total of 3,083. There were 0 unresolved cases. The 4 output files matched the public outputs byte for byte. In stage A we confirmed an error bound below $2.0\times10^{-8}$ with margin $10^{-5}$ for rejection by entry magnitude, and below $5.5\times10^{-8}$ with margin $10^{-4}$ for directional rejection. Including the saved stage B refinement and further-refinement records, we independently checked 27,189 certificates. The 163 cases unresolved in initial C are a subsequence of the 22,379 records, so we did not count them again.

**Overall assessment.** If there were 4 mutually unbiased bases, then after fixing the first 2, the vectors of the other 2 bases would fall inside the covering candidate balls. The candidate graph would retain the edges for mutual orthogonality among the 6 vectors of each basis and for mutual unbiasedness across the 36 cross-basis pairs. Final C ruled out every candidate compatible with this configuration and left 0 candidates undecided at the search cap. Using the regenerated numerical records, we checked the coverage and handoff of unresolved candidates required by Theorem 7.1 from the initial stage through final C. That chain and the final decisions support Theorem 1.1 under the stated arithmetic conditions. [Paper, Section 6.6, Theorem 7.1, and Appendix A](https://github.com/openai/math/blob/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026.pdf) · [Pinned replay instructions](https://github.com/openai/math/blob/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026/verification/saved-run/VERIFY.md)

<a name="reproduce"></a>

## Checks readers can reproduce

| Item | Method and input | Observed or expected result |
| --- | --- | --- |
| Saved run records from the paper | Run <code>python3 execution/check_records.py</code> with Python 3.9 or later in the pinned saved-run directory | MGL’s review found that the counts, shards, and handoff of unresolved cases were consistent across 100 saved runs. The same material gives build and run instructions for replaying the C++ computations. |
| Box maxima for the initial cover | Use the Python code below to evaluate all 512 vertices using rationals, with each coordinate in $[-1/2,1/2]$ | $9/4,\ 49/4,\ 57/4$. The first 2 examples are at or below the squared comparison radius. |
| Near-threshold example from step 05 | Use the code below to check the signs of the 2 recorded decimal enclosures with rational arithmetic | The upper endpoint with the margin is negative. The lower endpoint without it is positive. The sign check uses the values recorded in the text. |

| Representative regenerated files | SHA-256 |
| --- | --- |
| <code>centers.txt</code> (249,878 centers) | <code>c48bc9a2be1eb2cdeea82ea1b030d7cb9f00a6c9563b63f0248dd115748a5789</code> |
| <code>mid.bin</code> (600 records) | <code>e97c74dde90a0e758df2cb5d9708f5bd6bd660ed920b3299f5df92ff4de11be4</code> |
| <code>fine.bin</code> (22,379 records) | <code>9b5b743b61907277fa6687a0ad45677bbcd0e4c9bd44a0d93d258253fb52923d</code> |
| <code>fb1.bin</code> (1,127 records) | <code>ef85ec73217ecb0c770d3c775396df88b60ca06918f77310df5dff2f6d9bf215</code> |

In the example from Lemma 2.9, for an integer vector $k\in\mathbb Z^9$, choosing the endpoint in each coordinate of the box $|h_i|\le1/2$ to maximize $\|k+h\|^2$ gives $\|k\|^2+\|k\|_1+9/4$. Save the public check as <code>family266_checks.py</code> and run <code>python3 family266_checks.py</code>.

```python
from fractions import Fraction
from itertools import product

cases = [
    ((0,) * 9, Fraction(9, 4), True),
    ((2, 1, 1) + (0,) * 6, Fraction(49, 4), True),
    ((3,) + (0,) * 8, Fraction(57, 4), False),
]
radius_squared = (112 * Fraction("0.032")) ** 2
endpoints = (Fraction(-1, 2), Fraction(1, 2))

for k, expected, expected_within in cases:
    largest = max(
        sum((x + h) ** 2 for x, h in zip(k, corner))
        for corner in product(endpoints, repeat=9)
    )
    assert largest == expected
    assert (largest <= radius_squared) == expected_within

with_margin = tuple(map(Fraction, ("-2.12200308140e-9", "-2.12200308139e-9")))
without_margin = tuple(map(Fraction, ("3.18507737692e-7", "3.18507737693e-7")))
assert with_margin[0] <= with_margin[1] < 0
assert 0 < without_margin[0] <= without_margin[1]
print("3 box maxima and 2 interval signs: OK")
```

This short check covers finite box examples and the signs of recorded values. For stage C interval arithmetic, the 640 comparisons, and the argument from candidate-ball coverage through final exclusion, see the relevant review steps and pinned materials. [Original manuscript](https://github.com/openai/math/blob/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026.pdf) · [Pinned replay instructions](https://github.com/openai/math/blob/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026/verification/saved-run/VERIFY.md) · [Previous review edition v0.1.0](https://github.com/masaogatelabs-dev/mgl-research/blob/df333e12c9f43b1f402c61902d7da7c2681fdaf4/themes/math-proof-review/Family266.en.md) · [Case study of the MGL High-Precision Engine](https://github.com/masaogatelabs-dev/mgl-research/blob/df333e12c9f43b1f402c61902d7da7c2681fdaf4/reports/precision-engine/MGL-High-Precision-Engine-Family266.en.md)

