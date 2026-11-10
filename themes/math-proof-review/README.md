# 数学証明の独立検証

**日本語** · [English](README.en.md)

Masao Gate Labs · AI査読・検証

OpenAIの公開数学原稿を対象に、AIを用いた独立検証の記録を公開します。定理の主張と仮定を特定し、証明のどこを確認したか、どんな根拠や再検算があるか、どの点が保留かを区別します。この活動はMGLによる独立研究です。

## 査読目録

過去の比較検証報告T01から、原稿2本に対応する限定検証記録を公開しました。2行は同じ比較試験を参照します。論文全体の数学状態はNOT_EVALUATEDです。

| MGL査読ID | OpenAI Family | 原稿名・固定版 | 検証範囲 | 状態 | 記録 |
| --- | --- | --- | --- | --- | --- |
| MGL-MATH-001 | 088 | [A product counterexample to the simplex maximum for projection-body volume](https://github.com/openai/math/blob/adc7f1241b42e322a6451854ab7e4b4c146bf78a/preprints/A-product-counterexample-to-the-simplex-maximum-for-projection-body-volume-September-24-2026/paper.pdf) · `adc7f124` | 有理数比較・取込み試験 | 限定記録公開済み | [T01](T01.md#mgl-math-001-の確認範囲) |
| MGL-MATH-002 | 353 | [A Smooth Nonquadratic Entire Affine Maximal Graph in Dimension Ten](https://github.com/openai/math/blob/adc7f1241b42e322a6451854ab7e4b4c146bf78a/preprints/Smooth-Nonquadratic-Affine-Maximal-Graph-in-Dimension-Ten-October-5-2026/affine-maximal-dimension-ten.pdf) · `adc7f124` | 取込み試験。全証明は未評価 | 限定記録公開済み | [T01](T01.md#mgl-math-002-の確認範囲) |

2件の記録の初回公開日は2026-11-11 JST、公開要約の現行版はv0.1.0、更新日は2026-11-11 JSTです。元の実験報告はT01 v0.1.0（2026-10-08）。[引用目録と固定版](../../citations/README.md)から、書誌ID MGL-REF-001の引用情報と更新履歴を確認できます。

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
