# 数学証明の独立検証

**日本語** · [English](README.en.md)

Masao Gate Labs · AI査読・検証

## AI査読について

MGLのAI査読は、AIを用いて論文の主張・仮定・論証・参照する根拠を確認し、その過程と結果を記録する取り組みです。対象とする論文の全体を査読し、各主張と証明の妥当性を確認することを最終目標としています。

検証の途中でも、現時点で確認できた範囲、未確認・未判定の範囲、判定を保留した理由を明示して公開します。人間の査読者が根拠をたどり、追加の確認や追試が必要な箇所を判断できるよう支援します。

[引用目録](../../citations/README.md)では、検証記録を書誌ID・版・固定URLで参照できます。査読目録と各記録にある元論文へのリンクも併せて、どの原稿のどの版について、何が確認され、何が未判定なのかを理解しやすくします。

ここではOpenAIの公開数学原稿を対象とした、MGLによる独立研究の記録を掲載します。

検証記録の本文は、版ごとに印刷用のA4 PDFで掲載します。査読目録から原典、確認範囲、更新履歴、引用情報、原稿に対応するLean資料をたどれます。

案内更新日 2026-11-11 JST

## 質問・提案する

[T01 v0.1.1 の公開討論（MGL-MATH-001・002）](https://github.com/masaogatelabs-dev/mgl-research/discussions/2)で、質問や追試結果を共有できます。[査読希望・共同研究の提案](https://github.com/masaogatelabs-dev/mgl-research/discussions/categories/research-proposals)も受け付けています。どちらも日本語・英語で投稿できます。

[Family 088の有理数比較を追試する](T01-rational-check.md) · [資料の訂正を報告する](https://github.com/masaogatelabs-dev/mgl-research/issues/new?template=publication-correction.yml)

## 査読目録

| MGL査読ID | OpenAI Family | 原稿名・固定版 | 検証範囲 | 状態 | Lean資料 | 検証記録 |
| --- | --- | --- | --- | --- | --- | --- |
| MGL-MATH-001 | 088 | [A product counterexample to the simplex maximum for projection-body volume](https://github.com/openai/math/blob/adc7f1241b42e322a6451854ab7e4b4c146bf78a/preprints/A-product-counterexample-to-the-simplex-maximum-for-projection-body-volume-September-24-2026/paper.pdf) | 有理数比較・取込み試験 | 限定記録公開済み | [形式化の範囲](https://github.com/openai/math/blob/adc7f1241b42e322a6451854ab7e4b4c146bf78a/lean/docs/088.md) | [T01 PDF v0.1.1](https://github.com/masaogatelabs-dev/mgl-research/blob/17ae9cb70ba781d99969a92ba46c7009a3f761f5/themes/math-proof-review/editions/T01-v0.1.1-ja.pdf) · [確認範囲・履歴](T01.md#mgl-math-001-の確認範囲) |
| MGL-MATH-002 | 353 | [A Smooth Nonquadratic Entire Affine Maximal Graph in Dimension Ten](https://github.com/openai/math/blob/adc7f1241b42e322a6451854ab7e4b4c146bf78a/preprints/Smooth-Nonquadratic-Affine-Maximal-Graph-in-Dimension-Ten-October-5-2026/affine-maximal-dimension-ten.pdf) | 取込み試験。全証明は未評価 | 限定記録公開済み | 対応確認保留 | [T01 PDF v0.1.1](https://github.com/masaogatelabs-dev/mgl-research/blob/17ae9cb70ba781d99969a92ba46c7009a3f761f5/themes/math-proof-review/editions/T01-v0.1.1-ja.pdf) · [確認範囲・履歴](T01.md#mgl-math-002-の確認範囲) |
| MGL-MATH-003 | 173 | [A proof of Seymour’s second-neighborhood conjecture](https://github.com/openai/math/blob/4eaee87548250b2682affda7d05d947c05554bae/preprints/A-proof-of-Seymours-second-neighborhood-conjecture-September-23-2026/paper.pdf) | 主定理1.1・系5.1・系6.1の技術査読 | 技術査読記録公開済み | [OpenAIの形式化範囲](https://github.com/openai/math/blob/4eaee87548250b2682affda7d05d947c05554bae/lean/docs/173.md) | [Web v0.1.0](https://github.com/masaogatelabs-dev/mgl-research/blob/140574b7c4bc1c54be98ce3c8443c48370b7790d/themes/math-proof-review/Family173.md) · [A4 PDF v0.1.0](https://github.com/masaogatelabs-dev/mgl-research/blob/140574b7c4bc1c54be98ce3c8443c48370b7790d/themes/math-proof-review/editions/Family173-v0.1.0-ja.pdf) · [引用情報](../../citations/README.md#mgl-ref-010) |
| MGL-MATH-004 | 156 | [A nine-dimensional counterexample to Borsuk’s covering assertion](https://github.com/openai/math/blob/4eaee87548250b2682affda7d05d947c05554bae/preprints/A-nine-dimensional-counterexample-to-Borsuks-covering-assertion-September-23-2026/paper.pdf) | 主定理1.1・系7.1、4・5ラベルの復元境界 | 技術査読記録公開済み | [OpenAIの形式化範囲](https://github.com/openai/math/blob/4eaee87548250b2682affda7d05d947c05554bae/lean/docs/156.md) | [Web v0.1.0](https://github.com/masaogatelabs-dev/mgl-research/blob/beb2caa3f4a7c8e3ce7ead43496f43597578d688/themes/math-proof-review/Family156.md) · [A4 PDF v0.1.0](https://github.com/masaogatelabs-dev/mgl-research/blob/beb2caa3f4a7c8e3ce7ead43496f43597578d688/themes/math-proof-review/editions/Family156-v0.1.0-ja.pdf) · [引用情報](../../citations/README.md#mgl-ref-011) |
| MGL-MATH-005 | 161 | [A counterexample to Sidorenko’s conjecture](https://github.com/openai/math/blob/4eaee87548250b2682affda7d05d947c05554bae/preprints/A-counterexample-to-Sidorenkos-conjecture-September-23-2026/paper.pdf) | 主定理1.1・系1.2・系1.3の技術査読 | 技術査読記録公開済み | [OpenAIの形式化範囲](https://github.com/openai/math/blob/4eaee87548250b2682affda7d05d947c05554bae/lean/docs/161.md) | [Web v0.1.0](https://github.com/masaogatelabs-dev/mgl-research/blob/beb2caa3f4a7c8e3ce7ead43496f43597578d688/themes/math-proof-review/Family161.md) · [A4 PDF v0.1.0](https://github.com/masaogatelabs-dev/mgl-research/blob/beb2caa3f4a7c8e3ce7ead43496f43597578d688/themes/math-proof-review/editions/Family161-v0.1.0-ja.pdf) · [引用情報](../../citations/README.md#mgl-ref-012) |
| MGL-MATH-006 | 162 | [Balanced counterexamples to Ryser’s conjecture at prime orders](https://github.com/openai/math/blob/4eaee87548250b2682affda7d05d947c05554bae/preprints/Balanced-Counterexamples-to-Rysers-Conjecture-at-Prime-Orders-September-27-2026/paper.pdf) | 主定理1.1・系1.2、有限検算と一般論証 | 技術査読記録公開済み | [OpenAIの形式化範囲](https://github.com/openai/math/blob/4eaee87548250b2682affda7d05d947c05554bae/lean/docs/162.md) | [Web v0.1.0](https://github.com/masaogatelabs-dev/mgl-research/blob/beb2caa3f4a7c8e3ce7ead43496f43597578d688/themes/math-proof-review/Family162.md) · [A4 PDF v0.1.0](https://github.com/masaogatelabs-dev/mgl-research/blob/beb2caa3f4a7c8e3ce7ead43496f43597578d688/themes/math-proof-review/editions/Family162-v0.1.0-ja.pdf) · [引用情報](../../citations/README.md#mgl-ref-013) |
| MGL-MATH-007 | 181 | [A linear cycle-and-edge decomposition of every graph](https://github.com/openai/math/blob/4eaee87548250b2682affda7d05d947c05554bae/preprints/A-linear-cycle-and-edge-decomposition-of-every-graph-September-24-2026/main.pdf) | 補題3.1の式(3.6)、MGLの修正案と本文の二つの適用 | 途中報告公開済み・固定原稿の査読は保留 | [OpenAIの形式化範囲](https://github.com/openai/math/blob/4eaee87548250b2682affda7d05d947c05554bae/lean/docs/181.md) | [Web v0.1.0](https://github.com/masaogatelabs-dev/mgl-research/blob/beb2caa3f4a7c8e3ce7ead43496f43597578d688/themes/math-proof-review/Family181.md) · [A4 PDF v0.1.0](https://github.com/masaogatelabs-dev/mgl-research/blob/beb2caa3f4a7c8e3ce7ead43496f43597578d688/themes/math-proof-review/editions/Family181-v0.1.0-ja.pdf) · [引用情報](../../citations/README.md#mgl-ref-014) |
| MGL-MATH-008 | 266 | [The maximum number of mutually unbiased bases in dimension six](https://github.com/openai/math/blob/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026.pdf) | 主定理1.1の公開計算を論文指定の演算条件で再現、最終未解決0件 | 技術査読記録公開済み | [上限5組までの形式化](https://github.com/openai/math/blob/42907c9e999cc00d6abe7a50bfc1023250edd1b9/lean/docs/266.md) | [Web v0.1.0](https://github.com/masaogatelabs-dev/mgl-research/blob/df333e12c9f43b1f402c61902d7da7c2681fdaf4/themes/math-proof-review/Family266.md) · [A4 PDF v0.1.0](https://github.com/masaogatelabs-dev/mgl-research/blob/df333e12c9f43b1f402c61902d7da7c2681fdaf4/themes/math-proof-review/editions/Family266-v0.1.0-ja.pdf) · [引用情報](../../citations/README.md#mgl-ref-015) · [演算機の実運用評価](../../reports/README.md#mgl-high-precision-engine-family-266) |

初回公開日 2026-11-11 JST · 更新日 2026-11-11 JST · v0.1.1

PDF公開日 2026-11-11 JST

[MGL-REF-001 / 引用目録](../../citations/README.md)

Lean欄は対象原稿に対応する原典の付属資料を示します。対象の固定版では、Family 088の形式化は今回の原稿の20次元の反例を含みます。Family 353の形式化は3〜9次元を扱う別原稿が対象です。

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


