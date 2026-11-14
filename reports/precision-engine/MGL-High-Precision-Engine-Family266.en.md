# The MGL High-Precision Engine in a technical review

Masao Gate Labs | Case study from OpenAI’s Family 266 preprint | v0.1.0 | 14 November 2026

**All 640 cross-checked comparisons near the public double-precision code’s rejection threshold gave the same decisions.** MGL used its High-Precision Engine as part of a technical review of OpenAI’s *The maximum number of mutually unbiased bases in dimension six*, pinned to commit `42907c9e999cc00d6abe7a50bfc1023250edd1b9`. [Preprint and verification materials](https://github.com/openai/math/tree/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026)

## Where we used it

The public code rejects a candidate when a numerical test rules out a necessary condition. We took the same inputs and enclosed the decision gap between a lower and an upper bound. When the entire interval lies on the same side of the threshold, we can check the decision while accounting for rounding. We read each saved double-precision value as its exact rational equivalent.

| Workload | Observed result |
| --- | --- |
| Two measurements on 600 public intermediate records | We compared the phase residual and the deviation from orthogonality of tangent columns. Maximum absolute differences between double and high precision were 1.281 × 10⁻¹⁶ and 4.631 × 10⁻¹⁶, respectively. Both paths met the corresponding saved bound for every record. |
| Near-threshold comparisons in stage C | We checked 144 comparisons from equation (6.7), 48 from equation (6.11), and 448 from equation (6.12) and vector-pair conditions. Both paths agreed on all 640, including 320 rejections and 320 comparisons that retained the candidate. |
| Phase residuals for saved candidate balls | We checked 3,083 stage A records, 600 intermediate records, 22,379 refined records and 1,127 further-refined records. In all 27,189 cases, the upper endpoint of the residual interval was below the saved bound. |

For the 600-record comparison, the MGL engine computed exact rational matrix products, evaluated pi to 320 significant digits, and computed square roots to 80 significant digits. We compared complex exponentials using MPC/MPFR at 384 and 512 bits. This comparison did not enclose the entire phase residual in an interval.

## A case where the numerical margin retained a candidate

For equation (6.23), we examined balls 159 and 156 from record 204 of `f84.bin`, using zero-based indexing for the record. A positive gap means the comparison rejects the candidate. With the public code’s margin included, the interval lay entirely below zero, near −2.1220 × 10⁻⁹. Removing only that comparison margin, while keeping both ball centers and radii fixed, moved the entire interval above zero, near +3.1851 × 10⁻⁷. The margin kept this candidate from being rejected at that comparison. [Pinned stage C source](https://github.com/openai/math/blob/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026/verification/saved-run/compiled-build/source/stageC.cpp)

## What the engine handled

We used the MGL High-Precision Engine `1.1.0-dev.2` with math extension `0.1.0-dev.2` on Linux. For stage C, the engine supplied enclosing intervals for pi and selected square roots, and exact rational subtraction for the decision gap. For candidate-ball residuals, it supplied the interval for pi. MPFR handled trigonometry and intermediate interval operations with 320-bit directed rounding. Separate GMP integer and rational checks verified the candidate-ball matrix conditions.

This case study shows how a second arithmetic path checked recorded bounds and near-threshold decisions on real review data. The 640 comparisons were selected for proximity to their thresholds. The Family 266 technical review covers the full public replay and uniform error bounds. Runtime and comparisons with other products were outside the scope of this evaluation.
