# MGL High-Precision Compute Engine

[日本語](README.md) · **English**

Masao Gate Labs development report. Validation results are from CPU release v1.1.0-dev.2. Timing measurements are from v1.1.0-dev.1.

## Core, adapter, and extensions

| Function | Demonstrated capability |
| --- | --- |
| Core | 80-significant-digit arithmetic and verification. All 200 requests matched their v1.0.0 results. |
| Adapter | Local research tools can invoke the 80-digit arithmetic and the added mathematical functions. |
| Extensions | 16, 32, 80, 160, or 320 significant digits. Matrix products, determinants, inverses, and linear solves up to 8 by 8. |
| Coefficient checks | Two computation paths matched every coefficient in 15 HJO finite-polynomial cases. |

## Scope of verification and audit

Selectable precision and verified accuracy are distinct. The regression and coefficient checks cover the cases listed above. The audit checks saved records linking the engine version, inputs, and outputs. Computation status is recorded separately.

Linux x86-64 tests passed 66 self-test methods and 43 integration cases and covered 61 rational matrix products. Windows tests cover the 80-digit v1.0.0 baseline. Windows execution of the development release with matrix functions remains unverified.

## Timing for eight requests

On the same Linux system, each mode processed the same eight requests 30 times in alternating order. Timing included startup, computation, verification, saving, and audit. The batch median was about 21% of the separate-launch median. [Validation evidence](evidence/v1.1.0-en.md)

| Mode | Median | 95th percentile |
| --- | --- | --- |
| Eight separate launches | 1.498 s | 1.610 s |
| One batch of eight | 0.312 s | 0.343 s |

## NVIDIA cuBLAS and Ozaki Scheme II

CUDA Toolkit 13.4 uses Ozaki Scheme II for cuBLAS FP64 matrix multiplication when it improves performance. [NVIDIA release notes](https://docs.nvidia.com/cuda/archive/13.4.1/cuda-toolkit-release-notes/index.html#cublas-release-13-4)

| Aspect | MGL engine | NVIDIA cuBLAS |
| --- | --- | --- |
| Workload | CPU multiprecision arithmetic and verification, including small matrices | GPU matrix multiplication with FP64 emulation |
| Metric | 0.312 s median for eight requests, including verification and saving | Published real DGEMM throughput of up to 175 TFLOPS on B200 and 45 TFLOPS on RTX PRO 6000 Blackwell Server Edition |

A speed comparison requires matched inputs, precision, and timing boundaries.

References [Ozaki Scheme II paper (arXiv v4)](https://arxiv.org/abs/2504.08009v4) · [RIKEN R-CCS GEMMul8 implementation](https://github.com/RIKEN-RCCS/GEMMul8) · [Development and validation reports](../README.en.md)
