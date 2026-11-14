# At most three mutually unbiased bases in complex dimension six

Masao Gate Labs | Family 266 technical review | v0.1.0 | 14 November 2026

**MGL’s technical review supports Theorem 1.1 of OpenAI’s preprint under the paper’s stated double-precision arithmetic conditions.** We checked the construction of three bases using exact arithmetic and reproduced the public computation that rules out a fourth, from the initial cover to the final decision. Zero candidates remained unresolved.

We reviewed the 24 September 2026 preprint *The maximum number of mutually unbiased bases in dimension six* and its accompanying materials at commit `42907c9e999cc00d6abe7a50bfc1023250edd1b9`. [Preprint and verification materials](https://github.com/openai/math/tree/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026)

## What we checked

Two orthonormal bases in complex dimension six are mutually unbiased when the squared magnitude of the inner product of any vector from one basis with any vector from the other is one sixth. We verified the existence of three bases by taking tensor products of corresponding bases from triples in dimensions two and three. We checked cross-basis inner products exactly using Gaussian and Eisenstein integers.

Ruling out a fourth basis requires a complete initial cover, preservation of that cover through stages A and B, and exclusion of all remaining candidates in stage C. Stage C checks whether the candidates could form two sets of six mutually orthogonal vectors with all 36 cross-set pairs mutually unbiased. Candidates that reach the search cap are retained for further processing.

## From the initial cover to the final decision

| Step | Result reproduced by MGL |
| --- | --- |
| Initial cover | Checked 151,744,086 interval pairs and regenerated 249,878 seed centers. The saved file matched the public copy. |
| Stage A | Processed all seed centers in four shards. Produced 3,083 candidate balls and zero unresolved cases. All four output files matched the public files byte for byte. |
| Stage B | Refined 3,083 candidate balls to 600 intermediate records, then to 22,379 records. Saved outputs matched the public records. |
| Initial C and further refinement | Of 22,379 records, 163 reached the search cap. Further refinement produced 1,127 records from those 163. |
| Final C | Processed all 1,127 records in four shards. All finished successfully, with zero unresolved cases. |

We ran the pinned public algorithm in stages and passed the same saved numerical records from one stage to the next, following the execution conditions in Theorem 7.1. [Public replay instructions and records](https://github.com/openai/math/tree/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026/verification/saved-run)

## Could rounding cause a candidate to be missed?

An exact replay can repeat the same roundoff and miss the same candidate. We examined the coverage and rejection conditions in the pinned code and separately derived error bounds corresponding to Appendix A. In stage A, for example, the error bound for rejection based on entry magnitudes was below 2.0 × 10⁻⁸, with a code margin of 10⁻⁵. The directional rejection bound was below 5.5 × 10⁻⁸, with a margin of 10⁻⁴.

For 27,189 saved candidate balls, a separate calculation checked that the phase residual stayed below the saved bound and verified the matrix conditions used to certify each ball. The **MGL High-Precision Engine** supplied an enclosing interval for pi. MPFR supplied directed rounding for trigonometric functions and interval arithmetic. Rational and multiprecision integer arithmetic was used for the matrix conditions. All 640 selected near-threshold stage C comparisons also agreed with the public code when cross-checked using the MGL engine and MPFR.

## Scope of the review

This conclusion reflects MGL’s technical review of the pinned version. The replay used Linux x86-64 and GCC 14.2.0, with binary64 round-to-nearest, correctly rounded square roots, and no fused multiply-add. Saved candidate balls were checked independently. For temporary balls, the review relied on uniform error bounds and the code’s acceptance conditions. Formal verification of the full theorem was outside the scope.
