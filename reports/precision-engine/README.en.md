# MGL High-Precision Compute Engine

[日本語](README.md) · **English**

<!-- document-pdf:begin -->
## Printable PDFs and edition history

- [PDF v1.0.0](https://github.com/masaogatelabs-dev/mgl-research/blob/363b550db2815ae9d18281dce185aa588d9aa4cd/reports/precision-engine/editions/MGL-REF-009-v1.0.0-en.pdf) · 2026-11-11 JST · MGL-REF-009 · [Pinned web source](https://github.com/masaogatelabs-dev/mgl-research/blob/80a14879c11e83a6bb5c6ba1d4e447d835b700a7/reports/precision-engine/README.en.md)  
  Initial release of the development and validation report in web and A4 PDF editions.

[Citation catalogue](../../citations/README.en.md) · [BibTeX](../../citations/references.bib)
<!-- document-pdf:end -->

Masao Gate Labs development report. Validation results are from CPU release v1.1.0-dev.2. Timing measurements are from v1.1.0-dev.1.

## Core, adapter, and extensions

| Function | Demonstrated capability |
| --- | --- |
| Core | 80-significant-digit arithmetic and verification. All 200 requests matched their v1.0.0 results. |
| Adapter | Local research tools can invoke the 80-digit arithmetic and the added mathematical functions. |
| Extensions | 16, 32, 80, 160, or 320 significant digits. Matrix products, determinants, inverses, and linear solves up to 8 by 8. |
| Coefficient checks | Two computation paths matched every coefficient in 15 HJO finite-polynomial cases. |

## Validation on Linux

On Linux x86-64, 66 self-test methods and 43 integration cases passed. Regression checks covered 61 rational matrix products. The Windows x64 record covers 80-digit arithmetic in v1.0.0. Windows execution of the development release with matrix functions remains unverified.

## Timing for eight requests

The same eight requests ran on the same Linux system. Each mode ran 30 times in alternating order. Timing included startup, computation, verification, saving, and audit.

| Mode | Median | 95th percentile |
| --- | --- | --- |
| Eight separate launches | 1.498 s | 1.610 s |
| One batch of eight | 0.312 s | 0.343 s |

The batch median was about 21% of the separate-launch median.

## NVIDIA cuBLAS and Ozaki Scheme II

CUDA Toolkit 13.4 uses Ozaki Scheme II for cuBLAS FP64 matrix multiplication when it improves performance. [NVIDIA release notes](https://docs.nvidia.com/cuda/archive/13.4.1/cuda-toolkit-release-notes/index.html#cublas-release-13-4)

| Aspect | MGL engine | NVIDIA cuBLAS |
| --- | --- | --- |
| Workload | CPU multiprecision arithmetic and verification, including small matrices | GPU matrix multiplication with FP64 emulation |
| Metric | 0.312 s median for eight requests, including verification and saving | Published real DGEMM throughput of up to 175 TFLOPS on B200 and 45 TFLOPS on RTX PRO 6000 Blackwell Server Edition |

A speed comparison requires matched inputs, precision, and timing boundaries.

References [Ozaki Scheme II paper (arXiv v4)](https://arxiv.org/abs/2504.08009v4) · [RIKEN R-CCS GEMMul8 implementation](https://github.com/RIKEN-RCCS/GEMMul8) · [Development and validation reports](../README.en.md)
