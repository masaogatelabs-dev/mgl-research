# Interim review of the Erdős–Gallai cycle-decomposition manuscript

Masao Gate Labs · OpenAI Math Family 181 · Published interim report v0.1.0 · 2026-11-14 JST · MGL-REF-014

## Scope and current status

MGL examined the pinned OpenAI manuscript dated September 24, 2026. Theorem 1.1 (p. 1) claims that the edges of a finite simple undirected graph on n vertices can be partitioned into at most Cn simple cycles and single edges, with an absolute constant C. **The technical review of the pinned manuscript remains on hold.** The open point is equation (3.6) in Lemma 3.1 (pp. 5–8), on which Theorem 1.1 and Corollary 1.2 depend.

## The inference at issue in equation (3.6)

In Lemma 3.1, h is a lower bound on cut expansion. The parameters ℓ, k, b, and z bound path length, endpoint load, team size, and forbidden vertices per demand, respectively. The printed assumption (3.2) is h ≥ 64ℓ²(k + b) + z. Equation (3.6) uses 4[z + (k + b)ℓ²] ≤ h/16. When z is large, the printed assumption also fails to give |Wₚ| ≤ h/4, the bound used in the growth step (3.8). Here Wₚ is the set of deleted vertices for demand p, with its two endpoints excluded.

MGL checked a complete graph with r = 2⁴⁰ vertices, h = r/2, k = b = 1, and ℓ = 53,792, giving z = 179,377,668,096. Equation (3.2) holds with equality, yet z exceeds h/4 = 137,438,953,472. A forbidden set disjoint from the endpoints gives |Wₚ| ≥ z. This example refutes the inference to the bound in the proof. The existence of the routing paths in the example was left unevaluated.

## MGL’s proposed amendment and the two applications

MGL examined replacing z with 4z in (3.2) and replacing (3.6) with |Wₚ| ≤ z + 4bℓ² ≤ h/4. The second inequality follows from 4z + 16bℓ² ≤ 4z + 64(k + b)ℓ². This gives the bound h/4 for the growth estimate (3.8) and preserves h ≥ 64kℓ² for the bound on deleted edges.

| Application in the paper | What MGL checked for the amendment |
| --- | --- |
| Lemma 4.3 (pp. 12–13) | With z = 0, the change in its coefficient leaves the assumption unchanged. |
| Lemma 6.2 (p. 21, application on p. 24) | Here z = 2B₀, B₀ = D⁰·³⁰, and h = D⁰·⁹⁰/4. Both the amended term 4z = 8D⁰·³⁰ and the remaining term 64ℓ²(k + b) = O(D⁰·⁵⁴(log D)⁴) are o(h). Thus the strengthened assumption holds for sufficiently large D. |

## Checked and open scope

The strengthened condition suffices at the two application sites examined. In the strong induction, MGL also checked that each recursive input is smaller and checked how repeated vertices are counted in the total. The general statement of Lemma 3.1 as printed remains unverified in this review. Author confirmation, independent third-party review or replication, and Lean execution by MGL remain outstanding. OpenAI separately documents formalization of the main theorem.

## Sources and citation

- [OpenAI’s pinned source paper (PDF)](https://github.com/openai/math/blob/4eaee87548250b2682affda7d05d947c05554bae/preprints/A-linear-cycle-and-edge-decomposition-of-every-graph-September-24-2026/main.pdf)
- [OpenAI’s Lean scope note at the same commit](https://github.com/openai/math/blob/4eaee87548250b2682affda7d05d947c05554bae/lean/docs/181.md)

Suggested citation. Masao Gate Labs (2026). Interim review of the Erdős–Gallai cycle-decomposition manuscript. OpenAI Math Family 181, published interim report v0.1.0, MGL-REF-014.
