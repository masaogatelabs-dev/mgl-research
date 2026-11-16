# Technical review of finite-time blowup for Navier–Stokes

Masao Gate Labs (MGL) · English web edition v0.1.5 · Integrated assessment, 14 November 2026

## Review finding

**MGL's technical review supports Theorem 1.1 (whole space) and Corollary 10.6 (periodic domain), which establish finite-time velocity blowup with smooth forcing.**

| Review record | Details |
| --- | --- |
| Reviewer | Chappie No. 3 (MGL AI reviewer) |
| Model used in the review | GPT-6.1-Sol (as recorded by Masao) |

Both results concern positive viscosity and fluid initially at rest. In the whole-space case, the constructed solution has uniformly bounded kinetic energy up to the singular time. The result rules out a global smooth solution with the same initial velocity and forcing whose energy remains uniformly bounded. The periodic result rules out a global smooth periodic solution with the same initial velocity and forcing. The review traced the proof from the background field that produces the stress through the wave corrections, the passage from iteration to a local field, the smooth extension of the forcing, and the comparison with a competing solution. [Theorem 1.1](https://cdn.openai.com/pdf/32d9f210-8b73-45e0-91bc-82a30aef8a9a/navier-stokes.pdf#page=1) · [Corollary 10.6](https://cdn.openai.com/pdf/32d9f210-8b73-45e0-91bc-82a30aef8a9a/navier-stokes.pdf#page=125)

**What MGL means by “supports”.** Within the scope and verification steps documented here, the review found no issue that overturns the conclusions.

**Publication scope.** MGL keeps its internal algorithms for exploration and for selecting the order of checks private. This article presents the assumptions, derivations, calculation conditions, and results so readers can compare them with the paper and check them independently. The assessment rests on the mathematical evidence presented here.

**Edition reviewed.** OpenAI, *Finite Time Blowup for Navier–Stokes*, 166 pages. PDF SHA-256 `0e779481c4da40bd28d1e642e1d8ca57447d129610df28dfa5a11e9af8ae228f`. Equation and section numbers refer to this edition. The Lean code consulted was pinned at commit `f9e8bc5b38b6e212696e8a30e3e91517af887bbd`. [Source PDF](https://cdn.openai.com/pdf/32d9f210-8b73-45e0-91bc-82a30aef8a9a/navier-stokes.pdf) · [Pinned Lean code](https://github.com/openai/NavierStokesAndEuler/tree/f9e8bc5b38b6e212696e8a30e3e91517af887bbd)

**Scope of the assessment.** The forced results correspond to alternatives (C) and (D) in Fefferman's problem statement. MGL's AI technical review rederived estimates analytically, checked calculations symbolically and with rational arithmetic, and traced proof dependencies. The review compared the relevant portions of the published Lean code. An independent Lean rebuild, numerical generation of all profiles, and independent human review remain unperformed. [Fefferman's problem statement](https://www.claymath.org/wp-content/uploads/2022/06/navierstokes.pdf)

## Review sequence and responsibilities

The sections follow **the order in which the review reported its findings**. The proof dependencies run from Theorem 4.6 through Sections 5–8, Propositions 9.5 and 9.6, then Proposition 9.9 and Theorem 3.1, and finally Section 10. The report preserves the status of issues as they stood at each stage and links to the stages that resolved them.

Masao asked for a review of the paper discussed on a forum, then specified that the review resume at the unchecked part of Proposition 9.6. Later rounds followed the next task identified in the preceding report when Masao gave a continuation instruction such as “Please proceed to the next step 🥺👍”. Each section records the checks performed by Chappie No. 3. The public sources below identify where the initial disputes came from. The report flags places where the surviving record does not identify the full early conversation or the origin of a particular proposal. Quoted instructions are excerpts from the conversation, translated here. The notes headed “AI reviewer's observation” were reconstructed from the contemporary reports when preparing the article.

### The AI reviewer's autonomy and completion of the review

Masao selected the paper and where to resume, and gave continuation instructions between stages. The resulting records show that the AI reviewer set specific verification tasks, carried out derivations and calculations, and proposed what to check next based on the results. Autonomy here refers to task selection, verification, and reassessment within a stage as documented in those records. [Stage 07](#stage-07) · [Instruction at the start of stage 08](#stage-08)

In Section 8, the reviewer established that the derivative acts on the entire pressure-correction product $c_\rho P$, then asked whether Section 9 carries that product into the residual estimate. The integrated review checked that connection and traced earlier unresolved points through to the main theorem and its periodic counterpart. MGL then recorded the technical review as complete. [Next task from stage 07](#stage-07) · [Integrated assessment in stage 08](#stage-08)

The account identifies the question, assumptions, equations or calculations compared, scope of each result, and next task. The discussion, calculation, and narrowing-of-scope notes reconstruct the process from the contemporary reports and calculation results.

| Stage | Items checked | Finding at the time and next task |
| --- | --- | --- |
| [01 Published objections](#stage-01) | Equations (8.19) and (10.19) | Finished checking the two objections and moved to Proposition 9.6. |
| [02 Iteration and local field](#stage-02) | Proposition 9.6, Lemmas 9.7–9.8, and Proposition 9.9 | Supported conditional on the preceding construction. Next, check the inputs from Theorem 4.6. |
| [03 Main profile and stress](#stage-03) | Theorem 4.6, Proposition 5.5, and the connection to Section 7 | Left the estimates on the intermediate regions in Appendices A and B open. |
| [04 Intermediate regions in Appendices A and B](#stage-04) | Margin in the cone condition and order of parameter choices | Checked the intermediate regions and moved to the connection with forcing in Section 10. |
| [05 Forcing beyond the singular time](#stage-05) | Proposition 10.1, Lemmas 10.2–10.5, and Corollary 10.6 | Supported using Theorem 3.1 as input. Next, check the connection through Sections 5–7. |
| [06 Background and wave initialization](#stage-06) | Sections 5–7 and Proposition 9.5 | Checked the initial residual conditions and moved to the mean correction in Section 8. |
| [07 Pressure reconstruction and integral defects](#stage-07) | Lemma 8.2, Propositions 8.3–8.4, and Corollary 8.5 | Checked how the mean correction connects to the next step and moved to the integrated assessment. |
| [08 Integrated assessment](#stage-08) | Appendices A–C through Theorem 1.1 and Corollary 10.6 | Completed the MGL technical review and supported both results. |

<a name="stage-01"></a>

## 01 Published objections to equations (8.19) and (10.19)

**Starting instruction and source of the questions.** Masao asked for a review of the paper discussed on a forum. The two issues came from Bastounis, Circelli, and Hansen's comparison of the manuscript and Lean, and Hunt's public report of a counterexample to (10.19). The surviving review record does not establish who made each individual suggestion between the original request and the selection of those issues. [Manuscript and Lean comparison, Sections 3–4](https://arxiv.org/html/2610.08144v1#S3) · [Hunt's report, Sections 4–5](https://falsegreen.com/papers/paperA.pdf)

**Assumptions, checks, and results.** For (8.19), take smooth mean-zero input $F$ on the two-dimensional torus, and write the inverse of $N=v_t\cdot\partial_y$ on each nonzero mode $k$ as the multiplier $\widehat F(k)/(2\pi i v_t\cdot k)$. In (6.7) the reciprocal denominator has order $O(1+|k|)$. Integrating by parts $m+4$ times in the coordinate of largest absolute value and applying the output derivative of order $m$ leaves each term of order $O((1+|k|)^{-3})$. A shell of unit width at radius $n$ contains $O(n)$ lattice points in two dimensions, so the sum converges. The review rederived the manuscript's $C^{m+4}$ estimate. The Lean declaration consulted assumes $m+5$ derivatives, so the two estimates are stated differently. [Source (6.7) and (8.19)](https://cdn.openai.com/pdf/32d9f210-8b73-45e0-91bc-82a30aef8a9a/navier-stokes.pdf#page=95) · [Corresponding Lean declaration](https://github.com/openai/NavierStokesAndEuler/blob/f9e8bc5b38b6e212696e8a30e3e91517af887bbd/NavierStokes/SmoothFamilyTorusInverse.lean#L1059-L1080)

For (10.19), let $\phi_R(x)=\phi(x/R)$, $0\le\phi_R\le1$, $\chi_R=\phi_R^8$, and $B_R=\|\phi_R^4w\|_6$. The public counterexample treated the power as a cutoff at a different radius. Applying the chain rule to the manuscript's definition gives
$$
w\cdot\nabla\chi_R
=\frac{8}{R}\phi_R^3(\phi_R^4w)\cdot(\nabla\phi)(x/R).
$$
Thus when $B_R=0$ the flux factor vanishes. Under the manuscript's definition, the construction in that report cannot have both $B_R=0$ and nonzero flux. The review also rederived the pressure flux estimate. The local term is bounded in $L^{3/2}$ by $C_T(B_R+1)$ and the commutator in $L^{4/3}$ by $C_TR^{-3/4}$. Combining the corresponding bounds for $\phi_R^3w$ in $L^3,L^4$ gives
$$
\left|\int\pi w\cdot\nabla\chi_R\right|
\le C_T R^{-1}(B_R+1)B_R^{1/2}
    +C_TR^{-7/4}B_R^{3/4}.
$$
Here $C_T$ includes a uniform bound on the $L^2$ norm of the velocity difference. [Source (10.17)–(10.19)](https://cdn.openai.com/pdf/32d9f210-8b73-45e0-91bc-82a30eaf8a9a/navier-stokes.pdf#page=122) · [Public counterexample report](https://falsegreen.com/papers/paperA.pdf#page=5)

**Finding at the time and next task.** The two objections had been checked. The assessment of the full paper was still on hold, pending the check of how the inverse enters the iteration in Proposition 9.6 and how that iteration yields the local field. [Stage 02](#stage-02)

**AI reviewer's observation.** Once the cutoff notation matched the paper's, the two conditions required by the counterexample could be checked directly.

<a name="stage-02"></a>

## 02 The iteration in Proposition 9.6 and the local field

**Starting instruction and source of the question.** Masao asked to resume at the unchecked part of Proposition 9.6. Chappie No. 3 identified what each of the four operations updates and which orders it requires, then checked the synthesis after iteration.

**Assumptions, checks, and results.** Set $\varepsilon=Q^h$ and measure orders as powers of $\varepsilon$. At stage $j$, the wave residual has order $B_j=0.7+j/10$, the tangential residual and integral defects have order $C_j^*=B_j+1/2$, and the loss from a radial derivative is $\kappa_s=10^{-5}$. The checks took the initial state from Proposition 9.5, the fixed principal waves, and the inverse for the mean correction as inputs.

| Operation in the paper | What the review checked |
| --- | --- |
| Correction of nonzero angular harmonics | Recover the velocity from the potential. In (7.39) the apparent half-order loss from differentiating the phase cancels. |
| Stress correction for the auxiliary-torus mean | Subtract the weighted total integral and integrate radially. Cross-covariance with the fixed principal waves produces the target stress. The products with the old wave remainder and with the extra curl terms, and the new wave's quadratic term, are retained. |
| Correction of the mean-zero component on the auxiliary torus | Use the inverse in (8.19), recover the axial velocity through the potential, and update the pressure with the cutoff remainder included. |
| Five-variable moment correction | Preserve the two velocity moments and cancel the linear parts of the three defects. Recompute the products after the update using (8.26)–(8.27). |

The lower bounds across the four operations are $0.4-\kappa_s=0.39999$ for improvement in the wave residual, $0.17$ for the tangential residual, and $0.9-4\kappa_s=0.89996$ for the integral defects. Each exceeds the $0.1$ needed for the next stage. The corrections share a domain, and at a fixed order of physical differentiation the exponent of $q$ lost is independent of the iteration index. For synthesis, fix the target derivative and decay orders, then choose one sufficiently advanced finite stage. Estimating its residual and the difference contributed by the tail of the synthesized field gives the arbitrary-order residual estimate in Proposition 9.9. [Proposition 9.6, Lemmas 9.7–9.8, and Proposition 9.9](https://cdn.openai.com/pdf/32d9f210-8b73-45e0-91bc-82a30aef8a9a/navier-stokes.pdf#page=107)

**Finding at the time and next task.** The review supported Proposition 9.6 and the passage to the local field using the preceding construction as input. The next task was to check the inner positivity, stress-direction margin, and integral conditions supplied by Theorem 4.6 and their passage to the background and principal waves. [Stage 03](#stage-03)

**AI reviewer's observation.** Distinguishing the increasing number of input derivatives at successive stages from loss in the decay exponent under physical differentiation clarified how the finite stages yield the synthesized field.

<a name="stage-03"></a>

## 03 Main profile and stress in Theorem 4.6

**Starting instruction and source of the question.** This follow-up checked the prerequisites of Proposition 9.6. The verbatim instruction at the start of this stage was not verified. Chappie No. 3 examined the inner positivity, stress estimates at the annular boundaries, five cumulative integrals, and wave covariance identified in the preceding report.

**Assumptions, checks, and results.** The comparison series near the axis is $f_0(z)=\sum_{n\ge0}(-z/2)^n/[n!(n+1)!]$. With $s=z/2$, for $0\le s\le41/20$ the cubic partial sum of the alternating series is a lower bound. This cubic decreases on the interval, with right endpoint value
$$
1-\frac{s}{2}+\frac{s^2}{12}-\frac{s^3}{144}
=\frac{305719}{1152000}>0.265
\quad (s=41/20).
$$
Combining this with the error $O(\Lambda^{-1})$ in Proposition B.2 yields $E(X_{\mathrm{in}},0)>0$ in the inner region. This supplies the leading coefficient for the later blowup. If the five cumulative integrals $(M,I,J,S,C_p)$ agree at the matching radius as functions of $\eta$, and the profiles agree beyond it, the integrals and their parameter derivatives agree there as well. A common axis pressure matches the pressure. [Theorem 4.6 and Lemma 4.4](https://cdn.openai.com/pdf/32d9f210-8b73-45e0-91bc-82a30aef8a9a/navier-stokes.pdf#page=28) · [Source (B.11)–(B.13)](https://cdn.openai.com/pdf/32d9f210-8b73-45e0-91bc-82a30aef8a9a/navier-stokes.pdf#page=146)

At the inner edge of the annulus the stress vector is nonzero after factoring out the exponential. At the outer edge the azimuthal and axial factors are $e^{-4/y_b^2}y_b^{-3}$ and $e^{-4/y_b^2}y_b^3$, respectively, so the axial-to-azimuthal ratio is $O(y_b^6)$. Writing the unit direction as $(n_\theta,n_z)$, the margin $\kappa>0$ in (4.26) gives
$$
\frac{v_s-2}{2}\left(\frac{n_z-t_sn_\theta}{n_\theta+t_sn_z}\right)^2
\le 1-\frac{\kappa}{2}<1
$$
This supplies the input for choosing positive coefficients for the two wave covariances in Section 7. [Source (4.26)–(4.27) and (7.1)](https://cdn.openai.com/pdf/32d9f210-8b73-45e0-91bc-82a30aef8a9a/navier-stokes.pdf#page=33) · [Source (A.48)–(A.49)](https://cdn.openai.com/pdf/32d9f210-8b73-45e0-91bc-82a30aef8a9a/navier-stokes.pdf#page=142)

**Finding at the time and next task.** The review supported the connection from Theorem 4.6 to the later stages subject to the intermediate-region estimates. The next check was whether the stress condition keeps its margin across the regions in (A.27)–(A.30) and (B.25)–(B.40). [Stage 04](#stage-04)

**AI reviewer's observation.** At the edge where the stress tends to zero, factoring out the vanishing term and checking the direction exposed the margin required for the wave construction.

<a name="stage-04"></a>

## 04 Intermediate regions in Appendices A and B

**Starting instruction and source of the question.** This follow-up addressed the intermediate regions left open in the preceding report. The verbatim instruction at the start of this stage was not verified. Chappie No. 3 checked where the uniform lower bound could become small, the slope on the rising side of the pulse, and the order of parameter choices.

**Assumptions, checks, and results.** In the intermediate region of Appendix A, take $U=0$ and $l=-\lambda$, and use $c_\eta\asymp\eta^2$. The azimuthal coefficient satisfies
$$
Q_s'+(1-\lambda)Q_s
=\lambda-h+c_\eta-\lambda L\bar k(0)e^{-y}.
$$
Solving by an integrating factor adds $-L\bar k(0)e^{-(1-\lambda)y}(1-e^{-\lambda y})$ to the contributions from the constant input and initial value. This checks the sign of the comparison lower bound that uses $L\bar k(0)<1/2$. Within the pulse, retain the stress-direction ratio $w=N_s/(EQ_s)$ and the slope term. With shear coefficients $a,b_s$, sufficient conditions for (A.24) are $a-b_s w>0$ and $2b_s w+b_s^2/a+(a-2)w^2<2$. The two slope-dependent comparison polynomials $-2R^2+2.41R$ and $-3.5R^2+4.82R$ have maxima over the reals of $58081/80000<0.74$ and $58081/35000<1.68$, respectively. The review checked that these margins accommodate the uniform errors from earlier estimates. Here $R$ is the real variable of the comparison polynomials. [Source (A.24)–(A.30)](https://cdn.openai.com/pdf/32d9f210-8b73-45e0-91bc-82a30aef8a9a/navier-stokes.pdf#page=134)

In Appendix B, the review checked the comparison interval near the axis, the change of shear, and the repair of five integrals. In the dimensionless radius for the reconstruction, $X_{\mathrm{sep}}/X_R=e^{T_{\mathrm{sh}}}/(CP_*)^{10}$. Choose the outer data and tolerance first, fix $\Lambda,T_{\mathrm{sh}}$, and then take $C$ to make this ratio small. The shear frequencies for Appendix C are chosen afterward. The preceding lemmas and this parameter order support the conditions throughout the intermediate regions. The inputs and expected values for the exact quadratic check appear at the end of the article. [Source (B.25) and (B.34)–(B.40)](https://cdn.openai.com/pdf/32d9f210-8b73-45e0-91bc-82a30aef8a9a/navier-stokes.pdf#page=150)

**Finding at the time and next task.** The review checked the open regions in Appendices A and B analytically. The next task was to check in Lemmas 10.2 and 10.3 that the forcing derivatives converge as time approaches 1 and extend smoothly past it. [Stage 05](#stage-05)

**AI reviewer's observation.** Specifying what is fixed before increasing the radius made it possible to check that the tolerance was not being changed in the same step.

<a name="stage-05"></a>

## 05 Forcing beyond the singular time

**Starting instruction and source of the question.** Following Masao's continuation instruction, Chappie No. 3 rederived Lemmas 10.2 and 10.3, as identified in the preceding report. The inputs were the regularity of the local field in Theorem 3.1, decay of its residual near the origin, and the exterior heat flow.

**Checks and results.** For $t<1$, localize the field with a space-time cutoff $c$. Write the local velocity as $\nabla\times\boldsymbol A+B e_\theta$. Using $\nabla\times(c\boldsymbol A)+cB e_\theta$ for the localized velocity preserves zero divergence. Define the forcing $f$ as the momentum-equation residual of this velocity and the localized pressure. Near the origin the residual decays to zero to arbitrary order. Where the axial coordinate is nonzero, $q$ has a positive lower bound. Where $z=0$ and the radius is positive, use the integral representation of the exterior heat flow. Combining these regions on the fixed spatial support yields, for each fixed derivative order, the uniform limit
$$
F_j(x)=\lim_{t\uparrow1}\partial_t^j f(x,t)
$$
and uniform limits of its spatial derivatives. [Proposition 10.1 and Lemma 10.2](https://cdn.openai.com/pdf/32d9f210-8b73-45e0-91bc-82a30aef8a9a/navier-stokes.pdf#page=117)

Write the exterior heat flow as $K(r,\tau)=c_\infty(r^2/2)^{-A}H(4\tau/r^2)$, with $\tau=1-t$ and $A=1/2+h$. For $H(Z)$, the derivative of its kernel $e^{-v}v^h(1+Zv)^{-h}$ at each fixed order $j$ is bounded by $C_j e^{-v}v^{h+j}$. For the pressure integral $-\int_r^\infty K(\varrho,\tau)^2\,d\varrho/\varrho$, the integrand of its $j$-th time derivative is bounded by $C_j\varrho^{-3-4h-2j}$. Where the radius has a positive lower bound, this integrable majorant justifies exchanging limits and derivatives. [Source (10.7)–(10.8) and (A.32)](https://cdn.openai.com/pdf/32d9f210-8b73-45e0-91bc-82a30aef8a9a/navier-stokes.pdf#page=119) · [Exterior heat-flow kernel](https://cdn.openai.com/pdf/32d9f210-8b73-45e0-91bc-82a30aef8a9a/navier-stokes.pdf#page=138)

After time 1, set $\sigma=t-1\ge0$ and use $\sum_{j\ge0}\chi_0(b_j\sigma)\sigma^jF_j/j!$. The cutoff $\chi_0$ equals 1 near zero and vanishes for arguments at least 1. On the support of each term, its $m$-th time derivative has a bound proportional to $b_j^{m-j}$. For the finitely many derivatives satisfying $m+|\alpha|\le\lfloor j/2\rfloor$, the bound can be made at most $2^{-j}$ by choosing $b_j$. The differentiated series converges uniformly at each fixed order. At $\sigma=0$, only $j=m$ contributes, so the right-hand derivatives match the left-hand $\partial_x^\alpha F_m$. The forcing has fixed spatial support and vanishes from time 2 onward. The review also checked derivatives of the kernel on the time side and the series coefficients at orders 0 through 8. Uniform convergence gives the result at all orders. [Lemma 10.3 and (10.11)–(10.12)](https://cdn.openai.com/pdf/32d9f210-8b73-45e0-91bc-82a30aef8a9a/navier-stokes.pdf#page=120)

**Finding at the time and next task.** Using the local field as input, the review supported the forcing extension, energy estimate, and passage to the periodic case. The overall verdict remained on hold while the review checked whether the background and waves in Sections 5–7 supply the inputs needed for the iteration. [Stage 06](#stage-06)

**AI reviewer's observation.** Checking separately how the residual vanishes at the origin and how derivatives converge away from it clarified what had to match across the whole space.

<a name="stage-06"></a>

## 06 Background field and wave initialization in Sections 5–7

**Starting instruction and source of the question.** After Masao asked to proceed, Chappie No. 3 checked the passage from the background correction to the principal waves and the initial state of Proposition 9.5.

**Assumptions, checks, and results.** The matrix carrying the $\eta$ derivative in Lemma 5.1 maps the first four components into the last two. The diagonal integral kernel preserves this splitting, so the product of adjacent differentiation operators vanishes. In a nonzero operator string of length $k$ the number of $\eta$ derivatives is at most $\lceil k/2\rceil$. The $(k+1)!$ denominator from ordered radial integration absorbs the growth in the Cauchy estimates, keeping the same radial interval for higher-order corrections. In Lemma 5.2 the background power law splits the five integral conditions into two-row and three-row matrices with distinct weights. The positive-order velocity coefficients and stream function vanish before the mean-correction interval, where the zero axial velocity and the azimuthal power law in (5.44) are preserved. [Lemmas 5.1–5.2 and Proposition 5.5](https://cdn.openai.com/pdf/32d9f210-8b73-45e0-91bc-82a30aef8a9a/navier-stokes.pdf#page=47)

Section 6 separates the wave supports on the auxiliary torus and preserves Haar averages in common covering coordinates. In the Section 7 wave inverse, the propagator for harmonic $m$ has an extra factor $\exp[-(m^2-1)\int d]$ relative to the first harmonic. Since $d\ge0$ and $|m|\ge1$, this factor is at most 1. The value estimate therefore needs no smaller domain. The scale of both principal stress and principal-wave covariance is $Q^{-2A}\varepsilon(Q/q)^{A+1/2}=q^{-A-1/2}$. The review checked the match using the sum of squared cutoffs equal to 1 and the vanishing cross terms between disjoint supports. [Lemmas 6.1–6.2 and equations (7.18)–(7.19), (7.30)](https://cdn.openai.com/pdf/32d9f210-8b73-45e0-91bc-82a30aef8a9a/navier-stokes.pdf#page=65) · [Proposition 7.2](https://cdn.openai.com/pdf/32d9f210-8b73-45e0-91bc-82a30aef8a9a/navier-stokes.pdf#page=78)

| Initial-state check | Rederived lower bound on order | Required at entry to the iteration |
| --- | --- | --- |
| Nonzero angular harmonics of the residual | $1-3\kappa_s=0.99997$ | $0.7$ |
| Auxiliary mean of the tangential residual | $3/2-2\kappa_s=1.49998$, including the principal waves and curl remainder. The time correction handles the auxiliary mean-zero component. | $1.2$ for the full tangential residual after correction |
| Integral defects after the five-variable correction | $1-\kappa_s+0.9-2\kappa_s=1.89997$ | $1.2$ |

**Finding at the time and next task.** The review supported the connection to Proposition 9.5 using Theorem 4.6 and the Section 8 mean correction as inputs. The next check was whether the Section 8 pressure and axial-velocity corrections stay within the annulus and leave the three integral defects in the stated form. [Proposition 9.5 and (9.9)–(9.11)](https://cdn.openai.com/pdf/32d9f210-8b73-45e0-91bc-82a30aef8a9a/navier-stokes.pdf#page=106) · [Stage 07](#stage-07)

**AI reviewer's observation.** The extra decay of the higher harmonics gave an explicit way to judge whether successive iterations require the domain to shrink.

<a name="stage-07"></a>

## 07 Pressure reconstruction and integral defects in Section 8

**Starting instruction and source of the question.** After Masao asked to proceed, Chappie No. 3 rederived (8.6)–(8.9) and (8.12)–(8.17), as identified in the preceding report.

**Assumptions, checks, and results.** Let $R$ denote the normalized radius, $Y$ the auxiliary torus, and $Z$ the normalized axial coordinate. The radial inverse uses the smooth zero extension of the input. For $e=0,1,2$, subtract the total integral $J(R^ef)$ times the truncation function $\chi_m$ from the primitive integrated from the left. Inside the inner edge the primitive vanishes, and outside the outer edge it equals the total integral, so the correction remains supported in the annulus. The integral includes the shift along the auxiliary torus induced by radial motion. With $D_r$ denoting the corresponding derivative,
$$
(D_r+e/R)T_ef=f-R^{-e}(\partial_R\chi_m)J(R^ef).
$$
When $\int R^e\langle f\rangle_Y\,dR=0$, the zero Fourier mode of the total integral vanishes. Integrating by parts $p$ times along the path in Lemma 8.2 gives $M^{-p}$ for the other modes. A fixed output derivative order uses finitely many input derivatives. The bound $M^{-1}\lesssim\varepsilon^{\kappa_s}S_*^{\rho_g}$ then controls the truncation error by an arbitrarily high positive power of $q$. For an input independent of the auxiliary variable, the same weighted integral condition makes the error zero pointwise. [Lemma 8.2 and (8.6)–(8.10)](https://cdn.openai.com/pdf/32d9f210-8b73-45e0-91bc-82a30aef8a9a/navier-stokes.pdf#page=90)

Let $g_r$ be the radial residual source and set $P=\int\langle g_r\rangle_Y\,dR$, $\int\rho\,dR=1$, and $p_m=T_0(g_r-\rho P)$. Equation (8.13) gives $\partial_R\langle p_m\rangle_Y=\langle g_r\rangle_Y-\rho P$. Because the boundary term vanishes at the edge of the support, integration by parts yields
$$
\int R\langle p_m\rangle_Y\,dR
=-\frac12\int R^2\langle g_r\rangle_Y\,dR+c_\rho P,
\qquad c_\rho=\frac12\int R^2\rho\,dR.
$$
Use the paper's assumption that the two velocity moments vanish, and weight the azimuthal equation by $R^2$ and the axial equation by $R$. The time derivatives and axial viscosity terms become derivatives of zero integrals, and the radial divergences vanish at the boundary. Denote the remaining azimuthal and axial integral defects by $J_\theta$ and $J_z$. The axial equation then acquires the pressure contribution $c_\rho P$.
$$
\int R^2\langle E_\theta\rangle_Y\,dR=\varepsilon\partial_ZJ_\theta,
\qquad
\int R\langle E_z\rangle_Y\,dR=\varepsilon\partial_Z(J_z+c_\rho P).
$$
Here $J_\theta=\int R^2\langle Gv+V\gamma+\gamma v+W_{z\theta}\rangle_Y\,dR$ and $J_z=\int R\langle2G\gamma+\gamma^2+W_{zz}\rangle_Y\,dR-\tfrac12\int R^2\langle g_r\rangle_Y\,dR$. The quantities $G,V$ are the background axial and azimuthal velocities, $\gamma,v$ are the corresponding mean corrections, and $W_{ab}$ is the product of wave velocity components averaged over the physical angle. Using $R^e\,dR=Q^{-(e+1)/2}r^e\,dr$ to pass between the physical and chart coordinates shows that both $J_z$ and $c_\rho P$ have the normalization $Q^{2A-1}$. [Source (8.11)–(8.17)](https://cdn.openai.com/pdf/32d9f210-8b73-45e0-91bc-82a30aef8a9a/navier-stokes.pdf#page=92)

**Check.** If $\rho=(q/Q)^{-1/2}\widehat\rho(R/\sqrt{q/Q})$, then $c_\rho=(q/Q)\widehat c_\rho$. The polynomial example at the end uses $q/Q=1+Z$ and $P=1$, with $\langle g_r\rangle_Y$ independent of $Z$. Even though $\partial_ZP=0$, the derivative of the pressure integral is $41/36$. This example detects omission of the product-rule term. The integration by parts above gives the general argument for smooth inputs.

**Discussion, calculation, and scope.** The question was whether the axial derivative retains the variation of $c_\rho$ itself. To compare the derivative of the full product $\partial_Z(c_\rho P)$ with $c_\rho\partial_ZP$, the check fixed $P=1$ and varied only the correction scale $q/Q$. The first gives $P\partial_Zc_\rho=41/36$, while the second gives zero. This identifies when the two formulas differ. Integration by parts retains the full product in the general identity, narrowing the next question to whether Section 9 preserves that product and the axial derivative factor. [Source (8.13) and (8.15)–(8.16)](https://cdn.openai.com/pdf/32d9f210-8b73-45e0-91bc-82a30aef8a9a/navier-stokes.pdf#page=93)

**Finding at the time and next task.** The review checked what the Section 8 correction passes to Propositions 9.5 and 9.6. The main theorem's assessment remained on hold until integration. Next, check how the derivative of the full product in (8.16) enters the weighted residual order in (9.12), and how that estimate feeds into the local field and the forcing. [Source (9.12)](https://cdn.openai.com/pdf/32d9f210-8b73-45e0-91bc-82a30aef8a9a/navier-stokes.pdf#page=108) · [Stage 08](#stage-08)

**AI reviewer's observation.** The example in which the pressure integral changes even with $P$ fixed shows in a short calculation why the full product must be differentiated.

<a name="stage-08"></a>

## 08 Integrated assessment of the main theorem and the periodic case

**Starting instruction and source of the question.** After Masao asked to proceed, Chappie No. 3 checked for remaining unverified assumptions along the route from Theorem 4.6 to Theorem 1.1 and Corollary 10.6.

**Checks and results.** For analyticity near the axis, the review checked the axis pressure in Lemma A.5, the analytic solution in Proposition B.2, and the short inner interval preserved in Corollary B.6. For the stress to vanish outside the annulus, the exterior heat flow satisfies the equation and the total radial moment integrated from the inside vanishes. Positivity and the stress-direction margin from Theorem 4.6 pass to Sections 5–7. Section 9 updates the integral defects from Section 8. The axial integral identity (8.16) keeps the entire product $c_\rho P$ in the term $\varepsilon\partial_Z(J_z+c_\rho P)$. Section 9 uses an integral defect of order $C_* - \kappa_s$ to obtain the weighted residual estimate (9.12) of order $C_*+1-\kappa_s$. In the local field of Proposition 9.9, the inner azimuthal velocity is
$$
u_\theta\bigl(\sqrt{2X_{\mathrm{in}}\tau},0,0,1-\tau\bigr)
=\tau^{-A}\bigl(e_0+O(\tau^{2h})\bigr),
\qquad \tau=1-t,\quad e_0>0,
$$
which diverges along a path approaching the origin. The review checked that the forcing construction in stage 05 takes this same local field as input. [Proposition 9.9 and (9.20)–(9.21)](https://cdn.openai.com/pdf/32d9f210-8b73-45e0-91bc-82a30aef8a9a/navier-stokes.pdf#page=114) · [Source (10.20)–(10.21)](https://cdn.openai.com/pdf/32d9f210-8b73-45e0-91bc-82a30aef8a9a/navier-stokes.pdf#page=124)

In the whole space, Lemma 10.5 gives equality of velocities if a competing solution with the same forcing is smooth on each $[0,T]$ with $T<1$ and has a uniformly bounded spatial $L^2$ norm. Substituting (10.17) on the right of (10.19) yields a highest power of $3/2$ in the dissipation norm. Young's inequality absorbs it into the squared dissipation. Gronwall's inequality and the limit as the cutoff radius tends to infinity then make the difference vanish. Local smoothness of a global competing solution at time 1 is incompatible with the blowup above. For the periodic case, place the spatial support inside a fundamental cube before periodization. The copies have disjoint supports, so their nonlinear cross terms vanish. Agreement with a competing solution follows from the energy estimate for the difference on the periodic domain. [Lemma 10.5 and Corollary 10.6](https://cdn.openai.com/pdf/32d9f210-8b73-45e0-91bc-82a30aef8a9a/navier-stokes.pdf#page=121) · [Comparison in the periodic case](https://cdn.openai.com/pdf/32d9f210-8b73-45e0-91bc-82a30aef8a9a/navier-stokes.pdf#page=126)

**Discussion, calculation, and scope.** The preceding report left two checks. The first was whether the derivative of the full product in (8.16) enters the weighted residual estimate (9.12). The second was whether that estimate leads to synthesis of the local field and extension of the forcing. To check the first, the review compared the right-hand side of (8.16) with the derivation of the weighted integral estimate (9.12) in Section 9. To check the second, it matched residual bounds at fixed derivative orders to the assumptions of Lemma 5.4, then checked that the properties of Theorem 3.1 obtained in Proposition 9.9 supply the inputs of Lemma 10.2. This traced the local result through to the final assessment, in addition to checking the pressure term's sign and coefficient. [Source (9.12) and Proposition 9.9](https://cdn.openai.com/pdf/32d9f210-8b73-45e0-91bc-82a30aef8a9a/navier-stokes.pdf#page=108) · [Lemma 10.2](https://cdn.openai.com/pdf/32d9f210-8b73-45e0-91bc-82a30aef8a9a/navier-stokes.pdf#page=118)

**Integrated finding and remaining verification.** The integrated review record shows that rerunning all six prior calculation scripts passed. The appendix below gives the public checks and results for their respective stages. The review closed the connections previously left on hold, from the construction in Theorem 4.6 to comparison with a competing solution, and supports Theorem 1.1 and Corollary 10.6. Readers can use the pinned edition and equation numbers above to trace the assumptions, derivations, and proposed counterexamples. [Replication instructions and results](#verification)

**AI reviewer's observation.** Resolving the disputes over the two equations still left open whether the local field could be synthesized. The integrated review established which properties pass to each subsequent lemma, providing the basis for a verdict on the paper.

<a name="verification"></a>

## Calculations readers can reproduce

The code below presents representative checks from the six records rerun during the integrated review. It was rewritten for publication. It reproduces the finite calculations in the table. The assumptions and derivations in the article give the general arguments for the lemmas.

Save the [verification code](#verification-code) below as `review_checks.py`. It uses the Python 3.8+ standard library. Run `python3 review_checks.py` for all checks. The results column records runs of the published code under Python 3.12.14.

| Stage and source | Check | Command | Expected | Observed |
| --- | --- | --- | --- | --- |
| [02](#stage-02) · Proposition 9.6 | Lower bounds on improvement in the orders of the wave and tangential residuals and the defects at entry $B=0.7$ | `python3 review_checks.py 02` | $0.39999,\ 0.17,\ 0.89996$ | Matched |
| [03](#stage-03) · Equation (B.11) | Cubic partial sum of the comparison series at $s=41/20$ | `python3 review_checks.py 03` | $305719/1152000$ | Matched |
| [04](#stage-04) · Equations (A.24) and (A.28)–(A.30) | Maxima of the two quadratics used in the stress comparison | `python3 review_checks.py 04` | $58081/80000,\ 58081/35000$ | Matched |
| [05](#stage-05) · Equations (10.11)–(10.12) | Derivative orders 0–8 at which each series term contributes at time 1 | `python3 review_checks.py 05` | 1 only when $m=j$ among all 81 pairs | All 81 matched |
| [06](#stage-06) · Proposition 9.5 | Lower bounds on initial wave residual, auxiliary mean of tangential residual, and corrected defect orders | `python3 review_checks.py 06` | $0.99997,\ 1.49998,\ 1.89997$ | Matched |
| [07](#stage-07) · Equations (8.13), (8.15)–(8.16) | Normalization of the correction and its scale's contribution to the pressure integral | `python3 review_checks.py 07` | $1,\ 41/36$ | Matched |

In stage 07 use $\widehat\rho(x)=140(x-1)^3(2-x)^3$ on $1\le x\le2$ and zero elsewhere. Set $s=x-1$. The two values come from $\int\widehat\rho(x)\,dx$ and $\frac12\int x^2\widehat\rho(x)\,dx$. With $q/Q=1+Z$ and $P=1$ as in stage 07, the second value, $41/36$, appears in the axial derivative of the product.

<a name="verification-code"></a>

### Verification code

```python
import argparse
from fractions import Fraction as F
from math import comb, factorial

KAPPA = F(1, 100_000)


def residual_orders():
    # At the entry B = 0.7. The terms depending on B increase later.
    B = F(7, 10)
    wave = min(F(1, 2) - 4*KAPPA, F(2, 5) - KAPPA,
               F(1, 2) - 2*KAPPA, B - 3*KAPPA)
    mean = min(F(17, 100), 1 - 4*KAPPA)
    defect = F(9, 10) - 4*KAPPA
    result = (wave, mean, defect)
    assert all(gain > F(1, 10) for gain in result)
    return result


def axis_series():
    s = F(41, 20)
    return (sum((-s)**j / (factorial(j) * factorial(j + 1))
                for j in range(4)),)


def transition_quadratics():
    coefficients = ((F(2), F("2.41")), (F("3.5"), F("4.82")))
    return tuple(b*b / (4*a) for a, b in coefficients)


def force_jets():
    # Near zero the cutoff is identically one. Coefficients are padded
    # with zeros so every derivative below can be evaluated at zero.
    matches = 0
    for j in range(9):
        coefficients = [F(0)] * 9
        coefficients[j] = F(1, factorial(j))
        for m in range(9):
            assert coefficients[0] == int(j == m)
            matches += 1
            coefficients = [k * coefficients[k] for k in range(1, len(coefficients))]
    return (matches,)


def initial_orders():
    H0 = 1 - KAPPA
    wave = min(1 - 3*KAPPA, 1 - KAPPA, H0)
    mean = min(F(1, 2) + (1 - KAPPA) - KAPPA, 2 - KAPPA)
    defect = H0 + F(9, 10) - 2*KAPPA
    assert wave > F(7, 10) and min(mean, defect) > F(6, 5)
    return (wave, mean, defect)


def pressure_moment():
    # Integrate x**power * rho_hat(x) using s = x - 1 on [1, 2].
    def moment(power):
        return sum(F(140 * comb(power, i) * (-1)**j * comb(3, j), 4 + i + j)
                   for i in range(power + 1) for j in range(4))
    return (moment(0), moment(2) / 2)


CHECKS = {
    "02": (residual_orders, (F(39999, 100000), F(17, 100), F(22499, 25000))),
    "03": (axis_series, (F(305719, 1152000),)),
    "04": (transition_quadratics, (F(58081, 80000), F(58081, 35000))),
    "05": (force_jets, (81,)),
    "06": (initial_orders, (F(99997, 100000), F(74999, 50000), F(189997, 100000))),
    "07": (pressure_moment, (1, F(41, 36))),
}

parser = argparse.ArgumentParser()
parser.add_argument("stage", nargs="?", choices=CHECKS)
args = parser.parse_args()
for stage in [args.stage] if args.stage else CHECKS:
    check, expected = CHECKS[stage]
    actual = check()
    assert actual == expected, (stage, actual, expected)
    print(f"{stage}: PASS " + ", ".join(map(str, actual)))
```
