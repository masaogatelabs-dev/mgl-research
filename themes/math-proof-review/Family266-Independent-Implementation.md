# Family 266 補足研究 — 独自実装との候補球比較

Masao Gate Labs ｜ Family 266 技術査読 v0.2.0 補足研究 ｜ 初回比較 2026年11月20日（JST）

**日本語** · [English](Family266-Independent-Implementation.en.md)

OpenAIの公開コードをMGLが再実行した際の初回Stage Cの未解決163件と、maximusrufusらが論文の文章から独自に実装した計算の未解決43件を比較した。行・列の置換、転置、複素共役を認め、行・列の位相差を除いた空間で距離を測ると、**独自実装の43件すべての中心が原論文側の候補球のいずれかに入った。** [MGLの再実行記録](https://github.com/masaogatelabs-dev/mgl-research/blob/41bd45f6d3697cf864198d39e646b8ff4eca8ace/themes/math-proof-review/Family266.md#review-04) · [独自実装の中間データ案内](https://github.com/google-deepmind/formal-conjectures/issues/6918#issuecomment-7016254568)

| 確認項目 | 原論文側 | 独自実装側 |
| --- | ---: | ---: |
| 初回Stage Cの未解決記録 | 163 | 43 |
| 未解決記録を収録したバッチ | 15 | 5 |
| 他方の候補球と重なった球 | 157 | 43 |
| 中心が他方の球に入った記録 | 134 | 43 |
| 調べた範囲で重なりが見つからなかった球 | 6 | 0 |

2,217組で球の重なりを確認した。調べた組合せは $163\times43=7,009$ 組。候補球の重なりは、証明に使われる水平位相空間の球の幾何学的な比較である。棄却条件の成立、球全体の被覆関係、共通する真の解の有無は、それぞれ別の判定を要する。

## 入力と計算方法

公開コミットから計20本の <code>bad*.bin</code> を取得し、Gitのblob IDを照合した。独自実装側の5本は公開マニフェストのSHA-256とも照合した。各ファイルの件数、全レコードの境界、位相値と半径の範囲、ファイル終端を確認した。半径は206件すべてで保存されたbinary64の <code>0.016</code>、接空間の次元は全件で4。 [原論文側のバッチ](https://github.com/openai/math/tree/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026/verification/saved-run/execution/data/batches) · [独自実装側のバッチ](https://github.com/maximusrufus/mub6-certified-rerun/tree/ad961ac581c92eb3186f8c2fcb10af61223a7173/certificates/batches) · [独自実装側のSHA-256一覧](https://github.com/maximusrufus/mub6-certified-rerun/blob/ad961ac581c92eb3186f8c2fcb10af61223a7173/certificates/MANIFEST.txt)

原論文側の非空バッチは3、4、5、6、7、8、10、52、53、55、56、78、79、80、84。独自実装側は20、29、32、35、60で、それぞれ1、8、26、1、7件だった。

1. 位相中心を $6\times6$ 行列 $P,Q$ とし、独自実装側の $Q$ に行・列の置換、転置、複素共役に対応する位相の符号反転を適用した。第1行と第1列を基準に位相を正規化した。
2. 各成分に整数回転を加減して位相の差をそろえ、行・列の平均を引いて全体平均を足す直交射影 $\Pi$ を適用した。成分の差は単位を一回転とする。
3. 比較には、距離の二乗 $\|\Pi(D_0Q-D_0P-N)\|_F^2$ と、半径の和の二乗を用いた。ここで $D_0$ は第1行・第1列を基準にした正規化、$N$ は選んだ整数回転の行列。候補の探索は倍精度で、重なりと中心の包含の判定は保存値を二進有理数として読み、分数のまま検証した。片方の中心が他方の球に入る判定には、受け入れ側の半径の二乗を用いた。 [原論文側の位相整列](https://github.com/openai/math/blob/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026/verification/saved-run/compiled-build/source/atlas.cpp) · [独自実装の変位計算](https://github.com/maximusrufus/mub6-certified-rerun/blob/ad961ac581c92eb3186f8c2fcb10af61223a7173/impl/stageBC/common.hpp) · [独自実装の対称変換](https://github.com/maximusrufus/mub6-certified-rerun/blob/ad961ac581c92eb3186f8c2fcb10af61223a7173/impl/stageBC/phi.hpp)

探索で使った枝刈りは、$2\times2$ の位相の交代和が射影で不変であり、距離 $\rho$ の範囲に入る組合せではその差の絶対値が $2\rho$ 以下になることを利用した。二進浮動小数点の比較には $10^{-10}$ の余裕を置いた。基準にする行と列をずらした再計算でも、得られた2,217組は一致した。

## 具体例と追加照合

原論文側 <code>bad52.bin</code> の添字26と独自実装側 <code>bad32.bin</code> の添字6（ともに0始まり）では、独自実装側を複素共役し、行を <code>[0,1,3,4,2,5]</code>、列を <code>[5,4,3,2,1,0]</code> の順に並べると、中心間距離は約0.001533377で、片方の半径0.016より小さかった。整数回転の行列 $N$ は <code>[[0,0,0,0,0,0],[0,2,1,1,2,1],[0,1,1,1,2,2],[0,1,0,0,1,1],[0,0,0,0,1,1],[0,1,1,0,1,1]]</code>。この変換で得た距離の二乗は厳密に次の値だった。

$$
\frac{600065447762334584904721496619163}{255211775190703847597530955573826158592}.
$$

原論文側の6件について、探索する中心間距離を0.08まで広げた。表は探索で得られた最小距離の例であり、表示値は有理数で照合した距離の二乗から計算した近似値。球の半径の和は約0.032。

| 原論文側のファイルと添字 | 独自実装側のファイルと添字 | 中心間距離 |
| --- | --- | ---: |
| <code>bad6.bin</code> の0 | <code>bad35.bin</code> の0 | 0.033615 |
| <code>bad6.bin</code> の2 | <code>bad29.bin</code> の0 | 0.033647 |
| <code>bad7.bin</code> の1 | <code>bad35.bin</code> の0 | 0.041242 |
| <code>bad7.bin</code> の3 | <code>bad29.bin</code> の0 | 0.056786 |
| <code>bad8.bin</code> の1 | <code>bad29.bin</code> の0 | 0.050027 |
| <code>bad10.bin</code> の0 | <code>bad35.bin</code> の0 | 0.033047 |

この6件は原論文側の初回Stage Cで未解決となった領域である。独自実装でどの段階で、どの条件により同じ領域を処理したかは未確認。初期段階の比較については、独自実装側が原論文と同じ余裕を使った診断実行で、原論文の151,744,086組を再現したと報告している。 [初期段階の判断記録](https://github.com/maximusrufus/mub6-certified-rerun/blob/ad961ac581c92eb3186f8c2fcb10af61223a7173/impl/seed/DECISIONS.md)

[Family 266 技術査読 v0.2.0](https://github.com/masaogatelabs-dev/mgl-research/blob/41bd45f6d3697cf864198d39e646b8ff4eca8ace/themes/math-proof-review/Family266.md)
