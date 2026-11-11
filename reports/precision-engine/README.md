# MGL高精度演算機 - 実証結果と処理性能

**日本語** · [English](README.en.md)

<!-- document-pdf:begin -->
## 印刷用PDFと版履歴

- [PDF v1.0.0](https://github.com/masaogatelabs-dev/mgl-research/blob/363b550db2815ae9d18281dce185aa588d9aa4cd/reports/precision-engine/editions/MGL-REF-009-v1.0.0-ja.pdf) · 2026-11-11 JST · MGL-REF-009 · [固定版Web原稿](https://github.com/masaogatelabs-dev/mgl-research/blob/80a14879c11e83a6bb5c6ba1d4e447d835b700a7/reports/precision-engine/README.md)  
  初回公開。開発・検証報告をWeb版とA4 PDFで掲載。
- [PDF v1.1.0](https://github.com/masaogatelabs-dev/mgl-research/blob/891d6f6fe4495f7a697a76aeac2cd3c4e4db54ee/reports/precision-engine/editions/MGL-REF-009-v1.1.0-ja.pdf) · 2026-11-11 JST · MGL-REF-009 · [固定版Web原稿](https://github.com/masaogatelabs-dev/mgl-research/blob/ab2afb4baa945665ee18a9553d0b4b148e3d8efb/reports/precision-engine/README.md)  
  検算・監査の範囲を明記し、対象版と測定条件を示す実証根拠表を追加。

[引用目録](../../citations/README.md) · [引用データ（BibTeX）](../../citations/references.bib)
<!-- document-pdf:end -->

Masao Gate Labsの開発・検証報告です。実証はCPU開発版 v1.1.0-dev.2、処理時間は v1.1.0-dev.1 の記録に基づきます。

## 本体・アダプター・今回の追加例

| 機能 | 確認した内容 |
| --- | --- |
| 本体 | 80有効桁の演算と検算。旧版 v1.0.0 で固定した200要求の計算結果が開発版でも一致。 |
| アダプター | ローカルの研究ツールから、従来の80桁演算と追加した数学機能の両方を呼び出せる。 |
| 数学機能の拡張 | 16・32・80・160・320有効桁の指定と、最大8×8の行列積・行列式・逆行列・連立方程式を追加。 |
| 係数検算の追加例 | HJO有限多項式は3プロファイル×5ランクの15組で、全係数が2つの計算経路で一致。 |

## 検算と監査の範囲

指定可能な桁数と確認した精度を区別します。表の回帰比較と係数照合は、それぞれ記載の対象に限ります。監査では実行版と入出力を対応づけ、保存記録の整合性を確認します。計算の成否は別に記録します。

Linux x86-64で自己試験66メソッド、連携試験43ケースが成功し、有理数行列積61件を検査しました。Windows実測は80桁の基準版 v1.0.0 が対象で、行列機能を含む開発版のWindows実行は未確認です。

## 8要求の一括処理実測

dev.1を同じLinux環境で実行し、同じ8要求を各方式で交互に30回ずつ測定しました。起動・計算・検算・保存・監査を含みます。一括実行の中央値は個別起動の約21%でした。 [実証根拠表 v1.1.0](evidence/v1.1.0-ja.md)

| 実行形態 | 中央値 | 95パーセンタイル |
| --- | --- | --- |
| 8件を個別起動 | 1.498秒 | 1.610秒 |
| 8件を一括実行 | 0.312秒 | 0.343秒 |

## NVIDIA cuBLAS・尾崎方式IIとの対比

NVIDIAはCUDA Toolkit 13.4のcuBLASで、性能上有利な条件に尾崎方式IIを用いると説明しています。 [NVIDIA リリースノート](https://docs.nvidia.com/cuda/archive/13.4.1/cuda-toolkit-release-notes/index.html#cublas-release-13-4)

| 項目 | MGL高精度演算機 | NVIDIA cuBLAS |
| --- | --- | --- |
| 対象 | CPUでの小規模行列・多倍長演算と検算 | GPUでの倍精度（FP64）行列積 |
| 性能指標 | 8要求の一括処理に要した時間。中央値0.312秒 | NVIDIA公表の実数DGEMM処理量。B200で最大175 TFLOPS、RTX PRO 6000 Blackwell Server Editionで最大45 TFLOPS |

MGLの秒数は検算・保存も含む所要時間で、NVIDIAのTFLOPSは行列積の処理量です。速度を直接比較するには、入力・精度・計測区間をそろえた測定が必要です。

参照資料 [尾崎方式IIの論文（arXiv v4）](https://arxiv.org/abs/2504.08009v4) · [理研R-CCSの公開実装 GEMMul8](https://github.com/RIKEN-RCCS/GEMMul8) · [開発・検証報告一覧](../README.md)
