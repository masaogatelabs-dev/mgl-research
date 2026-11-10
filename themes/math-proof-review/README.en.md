# Independent Verification of Mathematical Proofs

[日本語](README.md) · **English**

Masao Gate Labs · AI-assisted review and verification

## About AI-assisted review

MGL's AI-assisted review uses AI to examine a manuscript's claims, assumptions, arguments, and supporting references, and to record the process and findings. Its ultimate goal is to review the entire target manuscript and assess the validity of each claim and proof.

While verification is in progress, we publish the scope checked so far, the parts still unchecked or undecided, and the reasons for holding a judgment open. These records support human reviewers in tracing the evidence and deciding where further examination or replication is needed.

The [citation catalogue](../../citations/README.en.md) identifies verification records by bibliographic ID, version, and pinned URL. Together with the review index and links to the original manuscripts in each record, it helps readers understand which manuscript and revision were examined, what was established within the checked scope, and what remains undecided.

This page presents records from MGL's independent research on mathematical manuscripts publicly released by OpenAI.

Introduction updated 2026-11-11 JST

## Review index

| MGL review ID | OpenAI Family | Manuscript / pinned revision | Scope | Status | Record |
| --- | --- | --- | --- | --- | --- |
| MGL-MATH-001 | 088 | [A product counterexample to the simplex maximum for projection-body volume](https://github.com/openai/math/blob/adc7f1241b42e322a6451854ab7e4b4c146bf78a/preprints/A-product-counterexample-to-the-simplex-maximum-for-projection-body-volume-September-24-2026/paper.pdf) | Rational comparison and extraction tests | Limited record published | [T01 v0.1.1](T01.en.md#mgl-math-001) |
| MGL-MATH-002 | 353 | [A Smooth Nonquadratic Entire Affine Maximal Graph in Dimension Ten](https://github.com/openai/math/blob/adc7f1241b42e322a6451854ab7e4b4c146bf78a/preprints/Smooth-Nonquadratic-Affine-Maximal-Graph-in-Dimension-Ten-October-5-2026/affine-maximal-dimension-ten.pdf) | Extraction tests; whole proof unevaluated | Limited record published | [T01 v0.1.1](T01.en.md#mgl-math-002) |

First published 2026-11-11 JST · Updated 2026-11-11 JST · v0.1.1

[MGL-REF-001 / Citation catalogue](../../citations/README.en.md)

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


