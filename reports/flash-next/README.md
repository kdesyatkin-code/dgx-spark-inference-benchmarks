# Qwen3.8-Flash-Next UD-Q2_K_XL: Strata vs Ollama

2026-11-24 | 30 measured runs | v1.0 evidence package

One GB10 DGX Spark, nominal 128 GB unified memory. Both engines used the same four imported base GGUF shards (as reported by the import operation); independent source shard hash comparison not supplied. Context 262144, one slot. Strata DFlash2 and Vision on; Ollama 0.40.18 llamacpp, 100% GPU reported, text-only import, no matched drafter. Hermes 0.22.5 via lmstudio-compatible API configuration. Strata Control 0.2.21 / engine 0.1.67 previously reported.

Strata won all 12 direct latency comparisons. Both passed all nine functional checks. Ollama won two of three Hermes wall-time comparisons; the aggregate difference is small and not a statistical result. Strata Hermes 4K includes overlap with a preceding canceled request, making the aggregate comparison particularly uncertain.

## Wall time (s)

| Case | ollama-0.40.18 | strata-dflash2 |
|---|---:|---:|
| hermes-4k | 67.162 | 85.504 |
| hermes-16k | 68.002 | 52.134 |
| hermes-short | 22.158 | 28.942 |
| dgx-4k | 26.237 | 8.789 |
| dgx-16k | 58.110 | 27.951 |
| dgx-32k | 88.330 | 31.662 |
| retrieval-r1 | 6.732 | 3.552 |
| retrieval-r2 | 6.213 | 3.682 |
| retrieval-r3 | 19.866 | 9.174 |
| tool-t1 | 3.203 | 1.343 |
| tool-t2 | 3.132 | 1.446 |
| tool-t3 | 3.321 | 2.134 |
| instructions-i1 | 2.492 | 1.125 |
| instructions-i2 | 2.894 | 1.481 |
| instructions-i3 | 3.233 | 1.537 |

## Subtotals (s)

| Workload | ollama-0.40.18 | strata-dflash2 |
|---|---:|---:|
| Hermes | 157.323 | 166.579 |
| DGX | 172.677 | 68.402 |
| Retrieval | 32.811 | 16.408 |
| Tools | 9.656 | 4.922 |
| Instructions | 8.618 | 4.144 |
| Direct API | 223.763 | 93.876 |
| All | 381.086 | 260.455 |

## Decode (tokens/s)

| Case | ollama-0.40.18 | strata-dflash2 |
|---|---:|---:|
| hermes-4k | 30.520 | 49.977 |
| hermes-16k | 29.940 | 51.545 |
| hermes-short | 30.980 | 50.752 |
| dgx-4k | 26.924 | 61.500 |
| dgx-16k | 30.663 | 53.400 |
| dgx-32k | 30.045 | 51.900 |
| retrieval-r1 | 31.657 | 55.000 |
| retrieval-r2 | 31.718 | 54.600 |
| retrieval-r3 | 29.458 | 68.800 |
| tool-t1 | 29.282 | 80.500 |
| tool-t2 | 28.721 | 79.000 |
| tool-t3 | 29.416 | 77.700 |
| instructions-i1 | 29.499 | 77.000 |
| instructions-i2 | 29.728 | 69.900 |
| instructions-i3 | 30.978 | 71.700 |

## Prefill (new tokens/s, where available)

| Case | ollama-0.40.18 | strata-dflash2 |
|---|---:|---:|
| hermes-4k | 877.550 | 1888.358 |
| hermes-16k | 872.620 | 1963.623 |
| hermes-short | 146.940 | 83.772 |
| dgx-4k | 890.024 | 1719.800 |
| dgx-16k | 945.315 | 2014.200 |
| dgx-32k | 892.106 | 2085.500 |
| retrieval-r1 | 960.354 | 1651.700 |
| retrieval-r2 | 962.245 | 1667.300 |
| retrieval-r3 | 947.523 | 2011.100 |
| tool-t1 | 480.612 | 527.900 |
| tool-t2 | 549.754 | 544.600 |
| tool-t3 | 562.027 | 556.300 |
| instructions-i1 | 230.509 | 194.700 |
| instructions-i2 | 196.325 | 208.100 |
| instructions-i3 | 180.656 | 192.000 |

For Flash-Next Hermes, Strata rate/token columns describe the first attributable model request, not the full multi-request task. For Qwen3.6 the first Hermes 4K rates are previously reported, not normalized source metrics.

## Resource observations

Ollama post-task RAM rose from 89 to 96 GiB; swap ~187 MiB in direct tests and 177 MiB in final agent tests. Strata ~89–91 GiB system used, swap ~2.4 GiB. These are snapshots, not peaks or equivalent continuous telemetry. Strata status includes GPU power/temperature/utilization snapshots; no matched Ollama telemetry, so no energy-efficiency claim. The Ollama cold smoke run took 196.018 s (55.727 s load, 29.63 tok/s); warm repeated prompt 88.146 s (0.000562 s load, 65/69 cached tokens, 31.17 tok/s). Smoke runs excluded from 30.

## Evidence and limitations

Strata: 57 exported files included, anonymized. Ollama: all 57 original export files included with container IP redacted; the 15 wall times, fixture hashes and RAM snapshots, 12 direct rate/token metrics and nine functional pass flags match the CSV. Supplementary console transcripts retained. All cases n=1; differences in generated length, tool schemas, cache, speculative decoding and agent turns remain. Functional checks are narrow, not general reasoning quality. The two 4K/16K Hermes answers contain incorrect implications about constant-time sequential file scans; exit 0 is not proof of answer correctness.
