# Family 266 追加検証記録 — 6件の追跡からアダマール条件付き被覆の判定まで

Masao Gate Labs ｜ Family 266 技術査読 v0.2.0 の補足 ｜ 検証日 2026年11月20日（JST）

**日本語** · [English](Family266-Coverage-Followup.en.md)

**最終判定**　原論文側の未解決候補球6件を調べた。独自実装の初回Stage Cに渡された球を用いると、元の6球それぞれの全体には被覆されない点があった。**原論文の保存証明記録が与える局所上界のもとで、6球それぞれのアダマール条件を満たす点はすべて、独自実装側の球の和集合に覆われる**ことを確認した。最初に見つけた被覆外の6点は、行の直交条件を満たさなかった。 [初回比較](https://github.com/masaogatelabs-dev/mgl-research/blob/634e42c75b827087b06da528c435e74c0bdb604c/themes/math-proof-review/Family266-Independent-Implementation.md) · [原論文の局所上界](https://github.com/openai/math/blob/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026/build/sections/phase-cover.tex)

## 01 初回比較で残った6件

OpenAIが公開した計算で初回Stage Cから再処理に回った163件と、maximusrufusらが原論文から独自に実装した計算の43件を照合した。行・列の置換、転置、複素共役と位相の整列を考慮すると、独自実装側の43中心はすべて原論文側の球に入った。原論文側では157球が独自実装の再処理候補球と重なり、6球の重なりは見つからなかった。この段階では、その6件が独自実装のもっと早い工程で処理された可能性があった。 [独自実装のデータ案内](https://github.com/google-deepmind/formal-conjectures/issues/6918#issuecomment-7016254568) · [初回比較と6件の一覧](https://github.com/masaogatelabs-dev/mgl-research/blob/634e42c75b827087b06da528c435e74c0bdb604c/themes/math-proof-review/Family266-Independent-Implementation.md)

## 02 先方が示した対応を有理数で照合

先方はStage Bの細分化出力 <code>fine.bin</code> から6件の対応先を示した。バッチの出力コードに従い、通し添字を256で割った商と余りを、Stage C入力のバッチ番号とバッチ内添字に使った。入力作成時に保存された半径は0.016である。公開された入力の保存値を二進有理数として読み、位相を整列した後の距離の二乗を比較した。6件とも、元の中心は対応先のStage C入力の球に入った。距離は先方の報告と小数第6位まで一致した。 [先方の追跡結果](https://github.com/google-deepmind/formal-conjectures/issues/6918#issuecomment-7030043886) · [バッチの出力コード](https://github.com/maximusrufus/mub6-certified-rerun/blob/ad961ac581c92eb3186f8c2fcb10af61223a7173/impl/stageBC/brun.cpp)

| 原論文側（0始まり） | 独自実装の fine.bin 通し添字 | 初回Stage C入力と添字 | 中心間距離（近似） |
| --- | --- | --- | --- |
| bad6.bin の 0 | 9142 | f35.bin の 182 | 0.007663919 |
| bad6.bin の 2 | 7552 | f29.bin の 128 | 0.001926635 |
| bad7.bin の 1 | 9142 | f35.bin の 182 | 0.006776854 |
| bad7.bin の 3 | 10217 | f39.bin の 233 | 0.006347020 |
| bad8.bin の 1 | 9130 | f35.bin の 170 | 0.002127197 |
| bad10.bin の 0 | 9142 | f35.bin の 182 | 0.008265086 |

対応先は重複を除くと4レコードで、いずれも初回Stage Cの公開ログで <code>NEGATIVE(graph)</code> を確認した。この結果は、6中心がグラフ判定で除外された球に入ることを示す。次に検証した問いは、中心の周囲を含む元の球全体も、独自実装の球で覆われるかである。 [c29.log](https://github.com/maximusrufus/mub6-certified-rerun/blob/ad961ac581c92eb3186f8c2fcb10af61223a7173/certificates/batches/c29.log) · [c35.log](https://github.com/maximusrufus/mub6-certified-rerun/blob/ad961ac581c92eb3186f8c2fcb10af61223a7173/certificates/batches/c35.log) · [c39.log](https://github.com/maximusrufus/mub6-certified-rerun/blob/ad961ac581c92eb3186f8c2fcb10af61223a7173/certificates/batches/c39.log)

## 03 球全体の幾何学的な被覆

独自実装側の初回Stage C入力61バッチを公開マニフェストのSHA-256と照合し、全15,595球を比較した。$R$ は保存されたbinary64の0.016を正確に有理数へ移した半径である。中心間の水平位相変位は、位相を正規化し、整数回転を差し引いた上で行・列の位相差を取り除いた。行・列の置換、転置、複素共役を探索した。 [独自実装のStage C入力](https://github.com/maximusrufus/mub6-certified-rerun/tree/ad961ac581c92eb3186f8c2fcb10af61223a7173/certificates/batches) · [SHA-256一覧](https://github.com/maximusrufus/mub6-certified-rerun/blob/ad961ac581c92eb3186f8c2fcb10af61223a7173/certificates/MANIFEST.txt) · [位相の変位](https://github.com/maximusrufus/mub6-certified-rerun/blob/ad961ac581c92eb3186f8c2fcb10af61223a7173/impl/stageBC/common.hpp) · [対称変換](https://github.com/maximusrufus/mub6-certified-rerun/blob/ad961ac581c92eb3186f8c2fcb10af61223a7173/impl/stageBC/phi.hpp)

元の球に届く中心間距離は $2R$ 以下である。基準行・列との $2\times2$ の交代和は水平射影で変わらず、その絶対値は中心間距離の2倍以下である。近接する位置合わせでは交代和が $4R<1/2$ 回転に収まるため、整数回転は各成分の最近接値に一意に定まる。位相を $D=2^{40}$ 倍して整数に移し、基準行・列との $2\times2$ の交代和に $4/D$、射影後のノルムに $24/D$ の丸め余裕を加えて、可能な位置合わせを絞った。近接した全3,856通りは元の保存値に戻して有理数で照合した。元の球の内部に、いずれの相手側の球にも入らない点が6件とも見つかった。

下表の点は、元の中心から、指定した2行2列の4成分を交互の符号で動かして得た。各成分の変位の絶対値は $9999R/20000$、全体の長さは $9999R/10000$。添字は0始まりで、その他の成分は0である。表の最後の列は、この点から各近接中心までの距離の二乗が $R^2$ を超えた量の最小値である。

| 原論文側（0始まり） | 行 | 列 | 左上の符号 | 近接した球数 | 近接した位置合わせ | 最小の距離二乗と半径二乗の差（近似） |
| --- | --- | --- | --- | --- | --- | --- |
| bad6.bin の 0 | [0, 3] | [1, 2] | + | 141 | 621 | 6.24484392e-05 |
| bad6.bin の 2 | [4, 5] | [0, 4] | − | 109 | 658 | 2.02411209e-05 |
| bad7.bin の 1 | [3, 5] | [3, 5] | + | 98 | 650 | 6.66963372e-05 |
| bad7.bin の 3 | [2, 5] | [3, 5] | + | 103 | 616 | 5.31183035e-05 |
| bad8.bin の 1 | [2, 5] | [3, 4] | + | 66 | 669 | 1.85826762e-05 |
| bad10.bin の 0 | [2, 5] | [0, 4] | + | 104 | 642 | 8.35263307e-05 |

ここで、被覆から外れた部分にアダマール条件を満たす位相もあるのか、という問いが残った。

## 04 被覆外の6点を行の直交条件で検査

位相行列 $p$ に対して $H_{ij}=\exp(2\pi\mathrm{i}p_{ij})$ と置く。アダマール行列では、異なる2行の内積の実部と虚部が両方とも0になる。円周率をMachinの公式と逆正接の交代級数で挟み、正弦・余弦をTaylor多項式と有理数の剰余上界で評価した。前工程の6点は、いずれも内積の少なくとも一方の成分について0を外す区間が得られた。

| 原論文側（0始まり） | 行の組 | 内積の成分 | 有理数による包含区間（外向き丸め） |
| --- | --- | --- | --- |
| bad6.bin の 0 | (0, 3) | 虚部 | [-0.200677786860, -0.200677786859] |
| bad6.bin の 2 | (4, 5) | 虚部 | [0.173349277514, 0.173349277515] |
| bad7.bin の 1 | (3, 5) | 虚部 | [0.147461199995, 0.147461199996] |
| bad7.bin の 3 | (2, 5) | 実部 | [-0.126229290581, -0.126229290580] |
| bad8.bin の 1 | (2, 5) | 虚部 | [0.181614668218, 0.181614668219] |
| bad10.bin の 0 | (2, 5) | 実部 | [-0.174375895661, -0.174375895660] |

この6点はいずれもアダマール条件から外れていた。そこで次に、条件を満たし得る点の範囲を局所上界で囲み、その範囲の被覆を調べた。

## 05 接空間での試算から全区画の検証へ

原論文の保存証明記録（Root）は中心 $P$ と $36\times4$ の接空間行列 $T$ を持つ。$\|\delta\|\le R$ の水平変位でアダマール条件 $F(P+\delta)=0$ が成立するとき、$\eta=T^\top\delta$ と書けば、原論文は次の上界を与える。 [原論文のRoot証明記録](https://github.com/openai/math/blob/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026/build/sections/phase-cover.tex)

$$
\|\delta-T\eta\|\le \mathtt{n0}+\mathtt{id}\,R+\mathtt C R^2.
$$

各球について接空間の球面を3万方向で試算すると、各試行点から最も近い相手側中心までの距離の最大値は、6球を通じて約0.00973〜0.01069だった。これは、接空間からのずれも含めた全域の被覆を検証できそうだという途中の仮説を支えた。次の工程では、標本点の代わりに全ての適用可能な小区画を検証した。

## 06 有効な点の被覆を確定

保存された6件の上界の右辺が、共通の有理数 $n=0.001121$ 未満であることを確認した。$T^\top T-I$ のフロベニウスノルムを有理数で照合し、$\|T\|<\beta=1.00001$ を確認したので、$\|\eta\|<0.016001$ が従う。$\eta$ を含む $[-1/32,1/32]^4$ を分割し、各区画の中心を $m$、辺の半幅を $h$ とした。区画内では $\|\eta-m\|\le 2h$ となる。 [保存された証明記録の技術査読](https://github.com/masaogatelabs-dev/mgl-research/blob/41bd45f6d3697cf864198d39e646b8ff4eca8ace/themes/math-proof-review/Family266.md#review-08)

位相を整列した独自実装側の球の中心変位を $v$ とする。小区画の被覆は、$R-n-2\beta h>0$ と、次の不等式を有理数で確認して判定した。

$$
\|Tm-v\|^2 \le (R-n-2\beta h)^2.
$$

これらが成立すれば、三角不等式から $\|\delta-v\|\le R$ となる。$\|\eta\|<0.016001$ の範囲に届かない小区画は、原点までの最小距離を有理数で比較して除いた。浮動小数点は照合する球の選択に用い、各区画の判定は有理数で確定した。

| 原論文側（0始まり） | 被覆した区画 | 範囲外の区画 | 被覆に使った異なるレコード | 最小二乗余裕（近似） |
| --- | --- | --- | --- | --- |
| bad6.bin の 0 | 746 | 1,490 | 68 | 1.71101083e-07 |
| bad6.bin の 2 | 645 | 1,606 | 53 | 6.63215623e-08 |
| bad7.bin の 1 | 718 | 1,653 | 50 | 1.81726140e-07 |
| bad7.bin の 3 | 823 | 1,788 | 55 | 1.38092367e-07 |
| bad8.bin の 1 | 651 | 1,675 | 42 | 1.48349693e-07 |
| bad10.bin の 0 | 736 | 1,515 | 55 | 3.36353594e-07 |

6球の合計で4,319区画を被覆し、9,727区画が必要範囲の外にあることを確認した。分割後の未判定区画は0件。最大分割深さは4だった。結論の範囲は、保存証明記録が与える局所上界のもとで、この6球に含まれるアダマール条件を満たす点が、独自実装の初回Stage C入力の球で覆われることまでである。追加の相互不偏基底の存在や、ここで被覆に使った全レコードのグラフ判定を再実行する検証は範囲外である。 [原論文側の再処理データ](https://github.com/openai/math/tree/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026/verification/saved-run/execution/data/batches)

maximusrufusらの独自実装、データ公開と6件の対応への追跡に謝意を表する。 [初回の比較記録](https://github.com/masaogatelabs-dev/mgl-research/blob/634e42c75b827087b06da528c435e74c0bdb604c/themes/math-proof-review/Family266-Independent-Implementation.md) · [GitHubでのやり取り](https://github.com/google-deepmind/formal-conjectures/issues/6918)
