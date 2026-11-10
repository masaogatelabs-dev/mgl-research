# Independent Verification of Mathematical Proofs

[日本語](README.md) · **English**

Masao Gate Labs · AI-assisted review and verification

MGL will publish records of independent, AI-assisted checks of mathematical manuscripts released by OpenAI. Each record identifies the claim and its assumptions, the parts of the proof examined, the supporting checks, and the points still open. This is an independent MGL research project.

## Review index

There are no published verification records yet. Once a target is selected, we will add one row per manuscript and revision.

| MGL review ID | OpenAI family | Manuscript and pinned revision | Scope | Status | Record |
| --- | --- | --- | --- | --- | --- |

## How to record the source

- Use the [OpenAI manuscript catalogue](https://github.com/openai/math/blob/main/CONTENTS.md) to identify the family number and manuscript title. If a family contains several manuscripts, identify the individual manuscript under review.
- Pin the manuscript link to the commit SHA under review. If a revision is checked later, add a separate row and record its relationship to the earlier version.
- Use the format `MGL-MATH-001` for MGL review IDs. Status labels such as Planned, In review, and Record published describe workflow progress. The record gives the mathematical findings and open points.

**Source citation example (not a registered review)**  
Family 002 · [Exact Birch–Swinnerton-Dyer Formula from Low Selmer Corank](https://github.com/openai/math/blob/4eaee87548250b2682affda7d05d947c05554bae/preprints/Exact-Birch-Swinnerton-Dyer-Formula-from-Low-Selmer-Corank-October-7-2026/exact-bsd-low-selmer-corank.pdf) · [Manuscript catalogue at the same revision](https://github.com/openai/math/blob/4eaee87548250b2682affda7d05d947c05554bae/CONTENTS.md)

## What each verification record includes

1. The theorem, lemma, or section examined and the assumptions stated in the manuscript.
2. Arguments examined, dependencies consulted, and independently reproduced checks with supporting evidence.
3. Unverified or open points and what is needed to resume checking them.
4. If Lean is used, the scope of formalization, the corresponding theorem, and the revision checked. Document how that formal statement relates to the prose manuscript.

[Research themes](../README.en.md) · [Home](../../README.en.md)
