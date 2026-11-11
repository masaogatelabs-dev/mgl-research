# T01 v0.1.1 — 有理数比較の追試 / Reproduce the rational comparison

[日本語](#日本語) · [English](#english) · [T01 の討論 / Discussion](https://github.com/masaogatelabs-dev/mgl-research/discussions/2)

## 日本語

**MGL-MATH-001（OpenAI Family 088）** の定理1と「The counterexample and exponential excess」節に示された数値比較を追試します。固定版の原稿は比を $121\binom{20}{10}/(21\cdot 2^{20})$ としています。この式を入力とし、二項係数、分子・分母、差、および比が1を上回ることを整数・有理数の演算で確認します。

この追試の範囲は、提示された比の数値評価です。体積比の式の幾何学的導出、証明全体、Family 353 の数学的主張は対象外です。

Python 3.8以上で、下のコードを `t01_rational_check.py` として保存し、`python3 t01_rational_check.py` を実行します。Windowsでは `py -3 t01_rational_check.py` も使えます。外部ライブラリは不要です。

[OpenAIの固定版PDF](https://github.com/openai/math/blob/adc7f1241b42e322a6451854ab7e4b4c146bf78a/preprints/A-product-counterexample-to-the-simplex-maximum-for-projection-body-volume-September-24-2026/paper.pdf) · [固定版TeXの該当箇所](https://github.com/openai/math/blob/adc7f1241b42e322a6451854ab7e4b4c146bf78a/preprints/A-product-counterexample-to-the-simplex-maximum-for-projection-body-volume-September-24-2026/build/main.tex#L383-L408) · [MGLの固定版PDF](https://github.com/masaogatelabs-dev/mgl-research/blob/17ae9cb70ba781d99969a92ba46c7009a3f761f5/themes/math-proof-review/editions/T01-v0.1.1-ja.pdf)

## English

This check reproduces the numerical comparison in Theorem 1 and the section “The counterexample and exponential excess” of **MGL-MATH-001 (OpenAI Family 088)**. The pinned manuscript gives the ratio $121\binom{20}{10}/(21\cdot 2^{20})$. Starting from that expression, the script checks the binomial coefficient, numerator, denominator, difference, and strict inequality using exact integer and rational arithmetic.

The scope is the numerical evaluation of the stated ratio. The geometric derivation of the volume ratio, the complete proof, and the mathematical claims of Family 353 are outside this check.

Save the following code as `t01_rational_check.py` and run `python3 t01_rational_check.py` with Python 3.8 or newer. On Windows, `py -3 t01_rational_check.py` is another option. Only the standard library is used.

[Pinned OpenAI manuscript](https://github.com/openai/math/blob/adc7f1241b42e322a6451854ab7e4b4c146bf78a/preprints/A-product-counterexample-to-the-simplex-maximum-for-projection-body-volume-September-24-2026/paper.pdf) · [Pinned TeX passage](https://github.com/openai/math/blob/adc7f1241b42e322a6451854ab7e4b4c146bf78a/preprints/A-product-counterexample-to-the-simplex-maximum-for-projection-body-volume-September-24-2026/build/main.tex#L383-L408) · [Pinned MGL PDF](https://github.com/masaogatelabs-dev/mgl-research/blob/17ae9cb70ba781d99969a92ba46c7009a3f761f5/themes/math-proof-review/editions/T01-v0.1.1-en.pdf)

## コード / Code

```python
from fractions import Fraction
from math import comb

choose = comb(20, 10)
numerator = 121 * choose
denominator = 21 * 2**20
difference = numerator - denominator
ratio = Fraction(numerator, denominator)

assert choose == 184_756
assert (numerator, denominator) == (22_355_476, 22_020_096)
assert difference == 335_380
assert ratio > 1

print(f"C(20, 10) = {choose}")
print(f"Ratio (before reduction) = {numerator}/{denominator}")
print(f"Difference = {difference}")
print("Ratio > 1")
```

## 期待する出力 / Expected output

```text
C(20, 10) = 184756
Ratio (before reduction) = 22355476/22020096
Difference = 335380
Ratio > 1
```

[追試結果を共有する / Share an independent check](https://github.com/masaogatelabs-dev/mgl-research/discussions/2) · [訂正を報告する / Report a correction](https://github.com/masaogatelabs-dev/mgl-research/issues/new?template=publication-correction.yml)
