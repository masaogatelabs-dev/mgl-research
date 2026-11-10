# 数学証明の独立検証

**日本語** · [English](README.en.md)

Masao Gate Labs · AI査読・検証

## AI査読について

MGLのAI査読は、AIを用いて論文の主張・仮定・論証・参照する根拠を確認し、その過程と結果を記録する取り組みです。対象とする論文の全体を査読し、各主張と証明の妥当性を確認することを最終目標としています。

検証の途中でも、現時点で確認できた範囲、未確認・未判定の範囲、判定を保留した理由を明示して公開します。人間の査読者が根拠をたどり、追加の確認や追試が必要な箇所を判断できるよう支援します。

[引用目録](../../citations/README.md)では、検証記録を書誌ID・版・固定URLで参照できます。査読目録と各記録にある元論文へのリンクも併せて、どの原稿のどの版について、何が確認され、何が未判定なのかを理解しやすくします。

ここではOpenAIの公開数学原稿を対象とした、MGLによる独立研究の記録を掲載します。

案内更新日 2026-11-11 JST

## 査読目録

| MGL査読ID | OpenAI Family | 原稿名・固定版 | 検証範囲 | 状態 | 記録 |
| --- | --- | --- | --- | --- | --- |
| MGL-MATH-001 | 088 | [A product counterexample to the simplex maximum for projection-body volume](https://github.com/openai/math/blob/adc7f1241b42e322a6451854ab7e4b4c146bf78a/preprints/A-product-counterexample-to-the-simplex-maximum-for-projection-body-volume-September-24-2026/paper.pdf) | 有理数比較・取込み試験 | 限定記録公開済み | [T01 v0.1.1](T01.md#mgl-math-001-の確認範囲) |
| MGL-MATH-002 | 353 | [A Smooth Nonquadratic Entire Affine Maximal Graph in Dimension Ten](https://github.com/openai/math/blob/adc7f1241b42e322a6451854ab7e4b4c146bf78a/preprints/Smooth-Nonquadratic-Affine-Maximal-Graph-in-Dimension-Ten-October-5-2026/affine-maximal-dimension-ten.pdf) | 取込み試験。全証明は未評価 | 限定記録公開済み | [T01 v0.1.1](T01.md#mgl-math-002-の確認範囲) |

初回公開日 2026-11-11 JST · 更新日 2026-11-11 JST · v0.1.1

[MGL-REF-001 / 引用目録](../../citations/README.md)

## 原典の記録方法

- [OpenAIの原稿目録](https://github.com/openai/math/blob/main/CONTENTS.md)でFamily番号と原稿名を確認します。同じFamilyに複数の原稿がある場合は、査読対象の原稿を個別に指定します。
- 原稿へのリンクは対象のコミットSHAで固定します。同じ原稿の改訂版を検証するときは別行に登録し、旧版との関係を記録します。
- MGL査読IDは `MGL-MATH-001` の形式で付けます。状態は「予定」「検証中」「記録公開済み」など、作業の進み具合を示します。数学的な判定と保留点は検証記録に記載します。

**原典の記載例（査読対象の登録前）**  
Family 002 · [Exact Birch–Swinnerton-Dyer Formula from Low Selmer Corank](https://github.com/openai/math/blob/4eaee87548250b2682affda7d05d947c05554bae/preprints/Exact-Birch-Swinnerton-Dyer-Formula-from-Low-Selmer-Corank-October-7-2026/exact-bsd-low-selmer-corank.pdf) · [同じ版の原稿目録](https://github.com/openai/math/blob/4eaee87548250b2682affda7d05d947c05554bae/CONTENTS.md)

## 各検証記録に載せること

1. 対象の定理・補題・節と、原稿で使われている仮定。
2. 確認した論証、参照した補題、独立に再検算できた箇所とその根拠。
3. 未確認・保留の箇所と、確認を再開するために必要なこと。
4. Leanで確認した場合は、形式化の対象、対応する定理、確認した版。自然言語の原稿との対応を分けて記載します。

[研究テーマ一覧](../README.md) · [公開トップ](../../README.md)


