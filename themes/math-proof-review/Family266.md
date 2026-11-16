# 複素6次元の相互不偏基底は最大3組 — Family 266 技術査読

Masao Gate Labs ｜ Family 266 ｜ 日本語版 v0.2.0 ｜ MGL-MATH-008・MGL-REF-015  
統合判定 2026年11月14日（JST） · 改訂公開 2026-11-16（JST）

## 査読結果

**MGL技術査読の判定は「支持」。対象は、複素6次元の相互不偏基底は最大3組とする主定理1.1である。** 3組の存在を厳密計算で確認し、4組目を排除する公開計算を、初期被覆から最終判定まで論文所定の倍精度条件のもとで再現した。

| 査読実行記録 | 記載 |
| --- | --- |
| 査読実行者 | チャッピー3号（MGL AI査読担当） |
| 査読実行モデル | GPT-6.1-Sol（政夫による記録） |

二つの正規直交基底は、一方からどのベクトルを、もう一方からどのベクトルを選んでも、内積の絶対値の二乗が $1/6$ なら相互不偏である。本査読では、3組の構成と、候補領域を覆ってから4組目の可能性を排除する原論文の計算を分けて検証した。

**初回探索で残った163件。** 22,379件を調べた初回Cでは、163件が探索上限に達して未解決として残った。そこで、この163件が表す領域を、より小さい1,127個の候補球で覆い直した。最終Cでその全件を処理し、未解決は0件となった。 [再細分化と最終Cの記録](#review-04) · [追試手順と出力ハッシュ](#reproduce)

**「支持」の意味**　記載した査読範囲と検証経路で結論を覆す問題を確認しなかった、というMGLの判定を指す。対象は2026年9月24日付の OpenAI プレプリント *The maximum number of mutually unbiased bases in dimension six* と、その公開計算資料の固定コミット <code>42907c9e999cc00d6abe7a50bfc1023250edd1b9</code> である。原論文PDFのSHA-256は <code>b4cc74c840c902494d589b51c8e9706490f37cf2735e69a0486122131c6b7446</code>。 [原論文PDF](https://github.com/openai/math/blob/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026.pdf) · [固定版の再実行手順](https://github.com/openai/math/blob/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026/verification/saved-run/VERIFY.md)

**OpenAIの公開資料**　OpenAIは論文に加え、数値計算のソースコード、各段階で保存したデータ、再実行の手順を公開している。読者はこれらの資料から、どの入力を使い、探索上限で残った候補をどう次の段階に渡したかを追える。MGLの再実行と高精度の別経路による検算も、この公開資料を出発点とした。 [OpenAIの論文・計算資料](https://github.com/openai/math/tree/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026)

**査読範囲**　固定版C++をLinux x86-64・GCC 14.2.0で再実行した。算術の前提は IEEE 754 binary64の最近接丸め、正しく丸められた平方根、融合積和（FMA）なし。保存された候補球について、位相残差と候補球を正当化する行列条件を別計算で点検した。実行途中だけで使う候補球にはコードの受理条件と一様な誤差上界を用いた。主定理全体の形式証明は査読範囲外である。比較した公開Lean資料の上界は5組で、MGLの「最大3組」の判定は下記の数学的照合と数値再現に基づく。 [Leanの検証範囲](https://github.com/openai/math/blob/42907c9e999cc00d6abe7a50bfc1023250edd1b9/lean/docs/266.md)

**公開原則**　ここでは原典から追査できるよう、検証に使った仮定と数式、条件、観測結果、判定の根拠を示す。MGL内部の探索と検証順序の決定に使うアルゴリズムや作業ログは内部で管理する。

## 工程の順序と担当

政夫はフォーラムで議論された論文の査読を依頼し、Family 266では論文の倍精度結果とMGL高精度演算機の検算との比較、続く検証の実施を指示した。下記は当時の報告順に、実施した検算、当時の判定、次の課題を再構成したもの。工程ごとの開始発言の逐語記録や、個々の問いを誰が最初に提案したかは確認できた範囲で扱う。「着眼点」は当時の報告と結果に基づく振り返りである。

**工程内の自立性と完遂**　当時の報告から追える判断の例は、段階Cの判定が640比較で一致した後も、確認を一様な誤差上界と上流の被覆へ広げたことである。その後、段階Aの全件再現まで終え、定理7.1が求める各段階を、同一の数値記録で最終Cまでつないで統合判定を行った。 [工程05](#review-05) · [工程06](#review-06) · [工程08](#review-08)

| 報告順 | 検証した範囲 | 当時の判定・残件 |
| --- | --- | --- |
| [01](#review-01) | 3組の存在、初期被覆、段階Cの抽出再実行 | 下限3を確認。上限3は保留。 |
| [02](#review-02) | 段階A・Bの被覆と打ち切り経路、非有限値の指摘 | 被覆の引き継ぎを抽出照合。全件連続再現は残る。 |
| [03](#review-03) | 600件の数値記録、式(6.7)の境界付近144比較 | 比較の一致を確認。後続分割・誤差上界は保留。 |
| [04](#review-04) | 初回Cの全分割と再細分化、式(6.11)の48比較 | 中間記録から最終Cまで連続再現。中間記録の生成が残る。 |
| [05](#review-05) | 式(6.12)とベクトル対の448比較、複素指数の誤差 | 境界付近の照合は計640比較。一様評価へ。 |
| [06](#review-06) | 段階Cの10種の棄却比較と半径の一様評価 | 入力条件のもとで誤差が余裕内。段階A・Bの被覆が残る。 |
| [07](#review-07) | 段階Bの最初の細分化と3,683件の証明記録 | 段階A出力から最終Cまでを接続。段階A全件が残る。 |
| [08](#review-08) | 段階Aの全件、保存証明記録の全体、統合判定 | 初期被覆から最終Cまでを接続し、主定理1.1を支持。 |

証明上の順序は、3組の構成と並行して、初期被覆 → 段階A → 段階B → 初回C → 未解決分の再細分化 → 最終Cと進む。査読では、下流を公開の中間出力から先行して検証した後、上流を再実行して同じデータにつないだ。

<a name="review-01"></a>

## 01 3組の存在と初期被覆

**課題と仮定。** 補題1.2の構成と、原論文第2節の初期被覆を調べた。第1基底を標準基底に固定すると、第2基底は規格化した複素Hadamard行列で表せる。第1・第2を $I,U$ とした場合、全基底に $U^*$ を適用し、両者を交換して成分ごとに共役を取ると $I,U^{\mathsf T}$ になる。内積の絶対値が保たれるので、転置も4組への拡張可能性を保つ。

**試行と結果。** 2次元と3次元で各3組を作り、対応する組のテンソル積を取った。3次元の位相計算では、$\omega^3=1$、$1+\omega+\omega^2=0$ より $|1+2\omega|^2=|2+\omega^2|^2=3$。異なる基底の内積絶対値の二乗は $(1/2)(1/3)=1/6$ となる。初期被覆では、補題2.4の位相の順序付けと閉区間の端点を点検し、補題2.9の9次元の箱の距離上界を有理数で確認した。初期被覆プログラムは151,744,086の区間対から249,878中心を生成し、保存ファイルは公開版と一致した。 [原論文 補題1.2、2.2、2.4、2.9、命題2.10](https://github.com/openai/math/blob/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026.pdf)

**当時の判定・次の課題。** 3組の存在は確認した。上限3は保留し、初期被覆の各候補を段階A・Bが漏れなく引き継ぐかを調べることにした。 [工程02へ](#review-02)

<a name="review-02"></a>

## 02 被覆の引き継ぎと探索の打ち切り

**課題と仮定。** 段階Aでは各中心から補完候補を $U(2)$ の閉セルで覆う。段階Bでは被覆に成功した親球の結果だけを後続の被覆に再利用する。統合先に元の球が収まるための十分条件として、元の半径 $r$ と、実際に採用した同値変換のもとでの中心間距離の上界 $d$ の和 $r+d$ を使う。

**試行と結果。** 段階Aの抽出64件で315球、未解決0を確認し、そのうち12球を段階Bの抽出試行に渡すと330球、未解決0だった。公開コードに対する非有限値の指摘も調べ、箱の平方距離、クラスタの距離、辺比較に渡る平方根の3箇所で入力範囲と非負性を確認した。調べた公開実行の範囲では、3箇所へのNaN流入を再現できなかった。 [原論文 補題4.15、命題4.16・5.7、付録A.9–A.12](https://github.com/openai/math/blob/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026.pdf) · [外部コード査読](https://github.com/kusasyu36/openai-math-audit)

**当時の判定・次の課題。** 抽出例で被覆を引き継げた。上限3は保留し、候補を棄却する判定で丸めの影響を照合するとともに、残る分割を再実行することにした。 [工程03へ](#review-03)

<a name="review-03"></a>

## 03 公開中間記録と式(6.7)の144比較

**課題と仮定。** 倍精度で候補を棄却する境目の判断を高精度の別経路で点検した。保存binary64値は、それと等しい有理数として読み直し、比較の差は正が棄却となる向きにそろえた。

**試行と結果。** 公開中間記録600件では、位相残差と接線列の直交性のずれの両方が保存上界内だった。倍精度経路と高精度経路の最大絶対差はそれぞれ $1.281\times10^{-16}$ と $4.631\times10^{-16}$。初回Cの2分割と再細分化出力から各6件を選び、式(6.7)の3種類について棄却側・非棄却側から境界に近い比較を抽出した。144比較すべてで判定が一致した。最接近例は再細分化出力の先頭レコードで、高精度の判定差の包含区間は $[1.664563697533116274232730,1.664563697533116274232731]\times10^{-10}$ にあり、全体が棄却側だった。 [原論文 式(6.7)、付録A.10](https://github.com/openai/math/blob/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026.pdf) · [MGL高精度演算機の実運用評価](https://github.com/masaogatelabs-dev/mgl-research/blob/df333e12c9f43b1f402c61902d7da7c2681fdaf4/reports/precision-engine/MGL-High-Precision-Engine-Family266.md)

**当時の判定・次の課題。** 中間記録と調べた比較を確認した。初回Cの未実行分と、方向付きの必要条件の検算を次に行う。 [工程04へ](#review-04)

<a name="review-04"></a>

## 04 初回Cの全分割と、方向付きの48比較

**課題と仮定。** 公開中間記録から始め、初回Cで探索上限に達した候補をすべて次へ渡せるか、出力の件数・順序・バイト列で確かめた。方向付きの式(6.11)では、公開コードが選んだ有限な方向ベクトルを固定して照合した。

**試行と結果。** 既報で処理済みの74分割に残り14分割を加え、22,379件・88分割をすべて処理した。探索上限に達した163件は15分割にあり、入力中と同じバイト列・相対順で未解決出力に残った。今回の出力163件から1,127件を再細分化し、最終Cの4分割で未解決0を得た。式(6.11)では、境界に近い48比較すべてで高精度と倍精度の判定が一致した。 [原論文 式(6.11)、第7節](https://github.com/openai/math/blob/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026.pdf) · [固定版の再実行手順](https://github.com/openai/math/blob/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026/verification/saved-run/VERIFY.md)

**当時の判定・次の課題。** 公開の中間記録から最終Cまでを連続して再現した。中間記録の生成と一般誤差評価が残るため、上限3の判定は保留した。 [工程05へ](#review-05) · [中間記録の生成を調べた工程07](#review-07)

<a name="review-05"></a>

## 05 448比較の追加と、比較余裕が候補を残す条件

**課題と仮定。** 式(6.12)の単一ベクトルの比較と、式(6.16)、(6.20)、(6.21)、(6.23)のベクトル対の比較を追加した。既報の3入力群に、初回Cで探索上限に達した15分割から選んだ未解決レコードを加え、棄却側と非棄却側の両方から境界例を抽出した。

**試行と結果。** 高精度で照合した448比較がすべて一致し、既報144・48と合わせて計640比較になった。別経路ではMGL高精度演算機の円周率・一部の平方根の包含区間と有理数演算を使い、三角関数と途中の区間演算をMPFRの320ビット上下丸めで行った。

**考察・検算・絞り込み。** 式(6.23)の相互不偏条件について、<code>f84.bin</code> の添字204（0始まり）、球159と156の比較を調べた。比較余裕込みの差は $[-2.12200308140,-2.12200308139]\times10^{-9}$ で候補が残る。同じ球中心と半径を固定し、当該比較式の余裕だけを外すと $[3.18507737692,3.18507737693]\times10^{-7}$ で棄却側に移る。これにより、その比較で候補を残した理由を切り分けた。複素指数の近似誤差も有理数で評価し、段階Cでの引数形成を含む上界が $2\times10^{-14}$ 未満となることを確認した。 [原論文 式(6.12)、(6.16)、(6.20)–(6.23)、付録A.2](https://github.com/openai/math/blob/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026.pdf) · [固定版の段階Cコード](https://github.com/openai/math/blob/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026/verification/saved-run/compiled-build/source/stageC.cpp)

**当時の判定・次の課題。** 640比較では丸めによる判定の反転は見られなかった。次は、抽出例から離れ、規定の入力範囲に対して棄却が安全になる誤差上界を調べる。 [工程06へ](#review-06)

<a name="review-06"></a>

## 06 段階Cの一様な誤差上界

**課題と仮定。** 有効な候補球の証明記録を入力とし、格子分割数 $6\le M\le1024$、保存位相 $|P_{ji}|\le4$、Hadamard側の半径 $r\le0.03$、候補ベクトルの球の半径 $s<0.1$ など、照合したコードの範囲で算術誤差を評価した。

**試行と結果。** 基本演算1回の丸めに $2\times10^{-16}|z|+10^{-300}$ を割り当てた。絶対値の上界が $A,B$、それぞれの誤差上界が $e_A,e_B$ のとき、積の誤差は $Ae_B+Be_A+e_Ae_B$ に積の丸めを加えて評価した。付録A.10・A.11とコードに沿って10種の棄却比較を評価し、最大の誤差上界を $8\times10^{-12}$ 未満と確認した。コードの比較余裕は $2\times10^{-7}$ または $3\times10^{-7}$。候補をまとめる球の半径でも、評価した誤差 $3\times10^{-13}$ 未満が加算余裕 $10^{-9}$ に収まった。 [原論文 付録A.10・A.11](https://github.com/openai/math/blob/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026.pdf) · [固定版の段階Cコード](https://github.com/openai/math/blob/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026/verification/saved-run/compiled-build/source/stageC.cpp)

**比較余裕が効く理由。** 余裕を引く前の実数の判定差を $d$、所定の余裕を $m$、余裕込みでコードが計算した差を $\widehat{\Delta}$ とする。今回の誤差上界 $E$ は $|\widehat{\Delta}-(d-m)|\le E$ を与える。コードが棄却する $\widehat{\Delta}>0$ のとき、$d>m-E$ となり、$E<m$ なので実数の判定差も正になる。

**当時の判定・次の課題。** 指定の入力と算術条件のもとで、調べた棄却比較の丸めによる誤棄却を防ぐ余裕を確認した。段階Cの前提に使った証明記録の有効性を、上流の段階A・Bへ戻って調べる。 [工程07へ](#review-07)

<a name="review-07"></a>

## 07 段階Bの最初の細分化と3,683件の証明記録

**課題と仮定。** 段階Bの公開中間記録を、段階Aの保存出力から再生成できるかを調べた。候補球の証明記録（Root）は、中心 $P$、局所の変位を表す接空間の列 $T$、それらの誤差上界を持つ。公開記録に保存されていない補助行列については、候補を作って原論文の十分条件を別計算で検査した。

**試行と結果。** 段階Aの3,083球を全件入力し、600件の中間記録を未解決0で再生成した。中間ファイルは工程04の入力とバイト単位で一致した。保存された3,083件と600件、計3,683件について、位相残差を方向丸めで、接線列の条件や補助行列の上界を二進有理数・多倍長整数で点検し、全件が通過した。補助行列の初回候補で剰余定数を満たせなかった97件には、原論文の補題4.7が認める転置を使って候補を再提案し、十分条件を確認した。 [原論文 補題4.4・4.7、命題4.5・5.7](https://github.com/openai/math/blob/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026.pdf)

**当時の判定・次の課題。** 段階Aの保存出力から最終Cまでを再実行で接続した。上限3は保留し、初期中心249,878件を入力とする段階A全体の再実行と、候補セルの被覆に使う誤差評価を残した。 [工程08へ](#review-08)

<a name="review-08"></a>

## 08 段階Aの全件と主定理の統合判定

**課題と仮定。** 初期被覆から段階Aの4分割を再実行し、全候補が棄却・被覆・未解決のいずれとして処理されたかと、後段へ渡されたバイト列を確認した。

**試行と結果。** 初期中心249,878件を全件処理し、分割ごとの出力は764、774、757、788の計3,083件。未解決は0件で、4ファイルは公開出力とバイト単位で一致した。段階Aの成分絶対値による棄却では誤差 $2.0\times10^{-8}$ 未満に対して比較余裕 $10^{-5}$、方向付き棄却では $5.5\times10^{-8}$ 未満に対して $10^{-4}$ を確認した。段階Bの細分化と再細分化の保存記録を加えると、独立に点検した証明記録は計27,189件。初回Cで未解決だった163件は22,379件の部分列なので、別件として数えていない。

**統合判定。** もし4組の相互不偏基底が存在するなら、最初の2組を固定した後も、残る2組のベクトルは被覆された候補球の中に入る。候補グラフには、各組の6本を互いに直交で結ぶ辺と、組をまたぐ36対を相互不偏で結ぶ辺が残る。最終Cでは、この組合せが成立し得る候補がすべて排除され、探索上限で判定を持ち越した候補も0件だった。定理7.1が要求する被覆と未解決候補の引き継ぎを、再生成した数値記録で初期段階から最終Cまで照合した。この接続と最終判定を根拠に、規定の算術条件のもとで主定理1.1を支持した。 [原論文 第6.6節、定理7.1、付録A](https://github.com/openai/math/blob/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026.pdf) · [固定版の再実行手順](https://github.com/openai/math/blob/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026/verification/saved-run/VERIFY.md)

<a name="reproduce"></a>

## 読者が手元で追査できる箇所

| 対象 | 方法・入力 | 観測結果または期待値 |
| --- | --- | --- |
| 原論文の保存実行記録 | 固定版の saved-run ディレクトリで Python 3.9以降を使い <code>python3 execution/check_records.py</code> | MGL査読で100実行分の保存記録の件数・分割・未解決の引き継ぎが整合。C++の数値再実行には同じ資料のビルド・実行手順を参照。 |
| 初期被覆の箱の最大値 | 下記のPythonコードで、各座標の区間 $[-1/2,1/2]$ の全512頂点を有理数で計算 | $9/4,\ 49/4,\ 57/4$。前2例が比較半径の二乗以下。 |
| 工程05の境界例 | 下記のコードで、記録された二つの十進包含区間の符号を有理数で照合 | 余裕込みの上端が負、余裕を外した区間の下端が正。符号照合の入力は本文の記録値。 |

| 代表的な再生成ファイル | SHA-256 |
| --- | --- |
| <code>centers.txt</code>（249,878中心） | <code>c48bc9a2be1eb2cdeea82ea1b030d7cb9f00a6c9563b63f0248dd115748a5789</code> |
| <code>mid.bin</code>（600件） | <code>e97c74dde90a0e758df2cb5d9708f5bd6bd660ed920b3299f5df92ff4de11be4</code> |
| <code>fine.bin</code>（22,379件） | <code>9b5b743b61907277fa6687a0ad45677bbcd0e4c9bd44a0d93d258253fb52923d</code> |
| <code>fb1.bin</code>（1,127件） | <code>ef85ec73217ecb0c770d3c775396df88b60ca06918f77310df5dff2f6d9bf215</code> |

補題2.9の例では、整数ベクトル $k\in\mathbb Z^9$ に対し、$|h_i|\le1/2$ の箱全体で $\|k+h\|^2$ が最大になるように各座標の端を選ぶと、$\|k\|^2+\|k\|_1+9/4$ になる。公開用のコードを <code>family266_checks.py</code> として保存し、<code>python3 family266_checks.py</code> で実行できる。

```python
from fractions import Fraction
from itertools import product

cases = [
    ((0,) * 9, Fraction(9, 4), True),
    ((2, 1, 1) + (0,) * 6, Fraction(49, 4), True),
    ((3,) + (0,) * 8, Fraction(57, 4), False),
]
radius_squared = (112 * Fraction("0.032")) ** 2
endpoints = (Fraction(-1, 2), Fraction(1, 2))

for k, expected, expected_within in cases:
    largest = max(
        sum((x + h) ** 2 for x, h in zip(k, corner))
        for corner in product(endpoints, repeat=9)
    )
    assert largest == expected
    assert (largest <= radius_squared) == expected_within

with_margin = tuple(map(Fraction, ("-2.12200308140e-9", "-2.12200308139e-9")))
without_margin = tuple(map(Fraction, ("3.18507737692e-7", "3.18507737693e-7")))
assert with_margin[0] <= with_margin[1] < 0
assert 0 < without_margin[0] <= without_margin[1]
print("3 box maxima and 2 interval signs: OK")
```

この短い検算は、箱の有限例と記録値の符号を確認するためのもの。段階Cの区間算術、640比較、候補球の被覆から最終排除までの論証は、それぞれ該当工程と固定版資料を参照されたい。 [原論文](https://github.com/openai/math/blob/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026.pdf) · [固定版の再実行手順](https://github.com/openai/math/blob/42907c9e999cc00d6abe7a50bfc1023250edd1b9/preprints/The-maximum-number-of-mutually-unbiased-bases-in-dimension-six-September-24-2026/verification/saved-run/VERIFY.md) · [従来の査読記事 v0.1.0](https://github.com/masaogatelabs-dev/mgl-research/blob/df333e12c9f43b1f402c61902d7da7c2681fdaf4/themes/math-proof-review/Family266.md) · [MGL高精度演算機の実運用評価](https://github.com/masaogatelabs-dev/mgl-research/blob/df333e12c9f43b1f402c61902d7da7c2681fdaf4/reports/precision-engine/MGL-High-Precision-Engine-Family266.md)

