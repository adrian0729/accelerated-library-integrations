# CUDA-Q QEC Result Summary

## Steane Code-Capacity Demo

| p | raw errors | decoded errors | raw rate | decoded rate |
| --- | ---: | ---: | ---: | ---: |
| 0.0010 | 3 | 0 | 0.003 | 0 |
| 0.0030 | 7 | 1 | 0.007 | 0.001 |
| 0.0100 | 32 | 0 | 0.032 | 0 |
| 0.0300 | 96 | 20 | 0.096 | 0.02 |
| 0.0500 | 136 | 46 | 0.136 | 0.046 |
| 0.1000 | 254 | 143 | 0.254 | 0.143 |

## Surface-Code Logical Error Results

| decoder | distance | p | shots | without decoding | with decoding |
| --- | ---: | ---: | ---: | ---: | ---: |
| nv-qldpc-decoder | 3 | 0.0010 | 1000 | 0.015 | 0.008 |
| nv-qldpc-decoder | 3 | 0.0030 | 1000 | 0.045 | 0.027 |
| nv-qldpc-decoder | 3 | 0.0050 | 1000 | 0.062 | 0.032 |
| nv-qldpc-decoder | 3 | 0.0100 | 1000 | 0.106 | 0.061 |
| nv-qldpc-decoder | 3 | 0.0300 | 1000 | 0.261 | 0.222 |
| nv-qldpc-decoder | 3 | 0.0500 | 1000 | 0.378 | 0.349 |
| nv-qldpc-decoder | 3 | 0.1000 | 1000 | 0.493 | 0.496 |
| nv-qldpc-decoder | 5 | 0.0010 | 1000 | 0.045 | 0.009 |
| nv-qldpc-decoder | 5 | 0.0030 | 1000 | 0.111 | 0.044 |
| nv-qldpc-decoder | 5 | 0.0050 | 1000 | 0.174 | 0.08 |
| nv-qldpc-decoder | 5 | 0.0100 | 1000 | 0.304 | 0.172 |
| nv-qldpc-decoder | 5 | 0.0300 | 1000 | 0.447 | 0.433 |
| nv-qldpc-decoder | 5 | 0.0500 | 1000 | 0.515 | 0.52 |
| nv-qldpc-decoder | 5 | 0.1000 | 1000 | 0.501 | 0.504 |
| single_error_lut | 3 | 0.0010 | 1000 | 0.011 | 0.007 |
| single_error_lut | 3 | 0.0010 | 1000 | 0.006 | 0.008 |
| single_error_lut | 3 | 0.0030 | 1000 | 0.034 | 0.019 |
| single_error_lut | 3 | 0.0050 | 1000 | 0.054 | 0.024 |
| single_error_lut | 3 | 0.0100 | 1000 | 0.106 | 0.07 |
| single_error_lut | 3 | 0.0300 | 1000 | 0.271 | 0.236 |
| single_error_lut | 3 | 0.0500 | 1000 | 0.385 | 0.357 |
| single_error_lut | 3 | 0.1000 | 1000 | 0.468 | 0.453 |
| single_error_lut | 5 | 0.0010 | 1000 | 0.022 | 0.011 |
| single_error_lut | 5 | 0.0030 | 1000 | 0.104 | 0.061 |
| single_error_lut | 5 | 0.0050 | 1000 | 0.16 | 0.11 |
| single_error_lut | 5 | 0.0100 | 1000 | 0.272 | 0.256 |
| single_error_lut | 5 | 0.0300 | 1000 | 0.445 | 0.445 |
| single_error_lut | 5 | 0.0500 | 1000 | 0.456 | 0.456 |
| single_error_lut | 5 | 0.1000 | 1000 | 0.529 | 0.529 |

## CPU vs GPU Syndrome Benchmark

| backend | median ms | syndromes/s | speedup vs CPU | scope |
| --- | ---: | ---: | ---: | --- |
| cpu_numpy | 321.459 | 311,082 | 1.00x | compute_only |
| gpu_cupy | 2.901 | 34,473,712 | 110.82x | compute_only |

## Decoder Benchmark Results

| decoder | path | distance | GPU | median ms | syndromes/s | speed vs LUT | raw errors | decoded errors | decoded rate | gain vs raw | rate vs LUT |
| --- | --- | ---: | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| nv-qldpc-decoder |  | 7 | NVIDIA L4 | 178.375 | 56,062 | 1.00x | 765/10000 | 167/10000 | 0.0167 |  |  |
| nv-qldpc-decoder | decode_batch | 7 | NVIDIA L4 | 48.153 | 41,534 | 0.55x | 153/2000 | 28/2000 | 0.014 | 5.46x | 0.32x |
| single_error_lut |  | 7 | NVIDIA L4 | 136.920 | 73,035 | 1.00x | 805/10000 | 480/10000 | 0.048 |  |  |
| single_error_lut | decode_batch | 7 | NVIDIA L4 | 26.274 | 76,121 | 1.00x | 153/2000 | 88/2000 | 0.044 | 1.74x | 1.00x |
| nv-qldpc-decoder |  | 9 | NVIDIA L4 | 516.585 | 19,358 | 1.00x | 1285/10000 | 207/10000 | 0.0207 |  |  |
| single_error_lut |  | 9 | NVIDIA L4 | 281.636 | 35,507 | 1.00x | 1192/10000 | 1013/10000 | 0.1013 |  |  |

## Decoder Comparison Takeaway

- d=7: QLDPC ran at 0.74x the LUT throughput with 0.38x the LUT logical error rate on the same sampled workload.
- d=9: QLDPC ran at 0.55x the LUT throughput with 0.20x the LUT logical error rate on the same sampled workload.
