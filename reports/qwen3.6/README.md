# Strata vs Ollama on NVIDIA DGX Spark — Qwen3.6-35B-A3B Q8_0

**Report v1.0 (historical measurements) | 2026-11-24 | Independent community comparison**

## Executive summary

45 measured runs: 15 per configuration. Strata won 9 of 15 individual latency comparisons against Ollama in each series, but Ollama completed the whole sequential workload in less time and won all three Hermes workloads. Reducing Strata from four to two slots saved about 19–23 GiB of system RAM without materially improving decode speed. On direct API tests, Strata decode fell from ~68 to ~10.5 tokens/s as prompt length increased from 4K to 32K; Ollama fell from 54.49 to 45.58. All nine functional fixtures passed in each configuration. A planned fourth series was not run: Ollama requested four slots but initialized one, as it had in the baseline. This is not a measured concurrent-throughput comparison.

## Hardware and software

NVIDIA DGX Spark, GB10, Linux aarch64, 128 GB nominal unified memory (121 GiB visible in `free`). Strata Control 0.2.21, native CUDA engine 0.1.67; Ollama 0.32.15; Hermes Agent 0.22.5 (previously reported). Local storage; no additional GPU. Exact driver/OS build and native pack checksum not recorded here.

| Setting | Ollama V1 | Strata V1 | Strata V2 |
|---|---|---|---|
| Requested/effective slots | 2/1 | 4/4 | 2/2 |
| Configured context | 262144 | 262144 | 262144 |
| KV cache | F16 default, actual type not captured | FP32 | FP32 |
| Speculative decoding | No implementation in later load log | MTP 2 | MTP 2 |
| Vision | Available | On | On |
| Model | Ollama GGUF | Strata native pack | Same native pack |
| RAM snapshots | 48–53 GiB | ~89–93 GiB | ~70 GiB |

Ollama model `qwen3.6:35b-a3b-q8_0`, architecture `qwen35moe`, manifest digest `0218f872e86baa9c7610509f27db36a7bc52eea7afee24688f81ca74ffcb6c77`; model blob manifest digest `7d8298ddcbce81ae5b237e42cd551db8352cf362564caa826b5ded02041fdfeb` (38,696,955,136 bytes). Strata rejected this GGUF due to a tensor shape mismatch [2048,1] vs [2048]; its own Q8_0 pack was used. Thus identical quantization labels do not imply identical weights. Ollama Modelfile: temperature 1, top_k 20, top_p 0.95, min_p 0, presence_penalty 1.5, repeat_penalty 1. Full equivalence of Strata sampling was not verified. FP16 requested via Strata launcher was not applied by the native Qwen engine.

## Method

Same synthetic fixture inputs, sequential requests, direct API and Hermes end-to-end paths separated. Three Hermes performance tasks, three direct context tasks, three retrieval, three tool-call construction and three strict JSON instruction tests. Thinking enabled; no deliberate output cap. Engine-specific optimizations retained. The nominal Hermes 4K/16K/Short labels refer to fixture size, not actual total agent context (about 18.5K/30.8K/14.5K input tokens for Strata). Direct tests used approximately 4K/16K/32K. Functional success required exact retrieval answers, expected structured tool calls (no execution), or valid JSON with strict expected values/types. One observation per fixture/configuration. Adapted synthetic workloads, not an official upstream benchmark suite. Background containers stopped for measured clean runs; not all ancillary service states independently recorded. Initial unsuccessful deployment/hybrid load excluded.


## Wall time (s)

| Case | ollama-v1 | strata-v1 | strata-v2 |
|---|---:|---:|---:|
| hermes-4k | 15.360 | 37.170 | 29.320 |
| hermes-16k | 22.168 | 79.148 | 69.628 |
| hermes-short | 14.646 | 23.197 | 23.194 |
| dgx-4k | 37.773 | 25.682 | 26.055 |
| dgx-16k | 33.960 | 49.488 | 49.409 |
| dgx-32k | 49.359 | 174.314 | 174.328 |
| retrieval-r1 | 6.104 | 3.861 | 3.881 |
| retrieval-r2 | 5.469 | 4.083 | 4.153 |
| retrieval-r3 | 9.815 | 14.280 | 14.283 |
| tool-t1 | 3.782 | 1.934 | 1.930 |
| tool-t2 | 2.746 | 2.484 | 2.522 |
| tool-t3 | 2.540 | 1.680 | 1.682 |
| instructions-i1 | 6.154 | 3.608 | 3.601 |
| instructions-i2 | 12.910 | 10.895 | 11.061 |
| instructions-i3 | 11.696 | 4.163 | 4.153 |

## Subtotals (s)

| Workload | ollama-v1 | strata-v1 | strata-v2 |
|---|---:|---:|---:|
| Hermes | 52.174 | 139.515 | 122.142 |
| DGX | 121.092 | 249.484 | 249.793 |
| Retrieval | 21.388 | 22.224 | 22.318 |
| Tools | 9.068 | 6.098 | 6.133 |
| Instructions | 30.760 | 18.666 | 18.815 |
| Direct API | 182.307 | 296.472 | 297.059 |
| All | 234.482 | 435.987 | 419.201 |

## Decode (tokens/s)

| Case | ollama-v1 | strata-v1 | strata-v2 |
|---|---:|---:|---:|
| hermes-4k | 50.260 | 27.310 | 27.595 |
| hermes-16k | — | — | 11.739 |
| hermes-short | — | — | 36.906 |
| dgx-4k | 54.494 | 68.743 | 67.850 |
| dgx-16k | 50.452 | 32.186 | 32.053 |
| dgx-32k | 45.585 | 10.487 | 10.484 |
| retrieval-r1 | 53.911 | 70.351 | 69.549 |
| retrieval-r2 | 53.100 | 76.470 | 75.425 |
| retrieval-r3 | 49.572 | 35.556 | 35.396 |
| tool-t1 | 55.843 | 85.906 | 84.546 |
| tool-t2 | 55.918 | 84.947 | 83.715 |
| tool-t3 | 55.880 | 87.446 | 86.317 |
| instructions-i1 | 55.027 | 89.612 | 88.232 |
| instructions-i2 | 54.781 | 85.123 | 83.849 |
| instructions-i3 | 55.248 | 85.834 | 86.045 |

## Prefill (new tokens/s, where available)

| Case | ollama-v1 | strata-v1 | strata-v2 |
|---|---:|---:|---:|
| hermes-4k | 2334.330 | 1661.500 | 1717.765 |
| hermes-16k | — | — | 1215.360 |
| hermes-short | — | — | 1798.548 |
| dgx-4k | 2524.291 | 2248.432 | 2237.133 |
| dgx-16k | 2509.916 | 1818.637 | 1870.137 |
| dgx-32k | 2356.292 | 1403.592 | 1402.524 |
| retrieval-r1 | 2502.328 | 2252.337 | 2244.717 |
| retrieval-r2 | 2508.338 | 2256.482 | 2226.930 |
| retrieval-r3 | 2505.449 | 1883.725 | 1882.163 |
| tool-t1 | 1046.282 | 923.423 | 944.079 |
| tool-t2 | 1107.068 | 941.661 | 947.066 |
| tool-t3 | 1147.736 | 1001.914 | 996.509 |
| instructions-i1 | 299.956 | 217.273 | 227.661 |
| instructions-i2 | 333.816 | 265.047 | 262.009 |
| instructions-i3 | 310.442 | 241.981 | 242.390 |

For Flash-Next Hermes, Strata rate/token columns describe the first attributable model request, not the full multi-request task. For Qwen3.6 the first Hermes 4K rates are previously reported, not normalized source metrics.

## Key observations

- On direct DGX 4K, Strata V2 was faster in end-to-end latency (26.05 vs 37.77 s). At 32K it was 3.53 times slower (174.33 vs 49.36 s).
- Strata V2 reserved 22.12 GiB for two sessions versus 44.23 GiB for four, with every routed expert in VRAM (32.67 GiB), prompt chunk 1024, 57.02 GiB free before expert placement. No packed-copy release message in V2 startup; actual use not independently confirmed. V1 launch logs differed in available memory and packed-copy release, so slot count is not the only possible difference.
- The strong long-context slowdown persisted even with ~51 GiB available system RAM after loading V2. Its exact cause is unestablished; do not attribute it solely to KV precision, attention, MTP or memory bandwidth without profiling.
- Ollama V2 attempt: configured `OLLAMA_NUM_PARALLEL=4`, recreated same container image, loaded same model and 262144 context. Runner logged `initializing, n_slots = 1, n_ctx_slot = 262144, kv_unified = 'false'`; `warmup: flash attention is enabled`; `no implementations specified for speculative decoding`. RAM 48 GiB. No additional timed series: requested setting did not change effective slots. This establishes behavior of the tested build/model, not all Ollama models or versions.


## Limitations

See [methodology](../../methodology/README.md). Different GGUF packs, cache and sampling, one run per case. Exact driver and clean V2 startup evidence missing. The 45-run historical archive contains 43 normalized wall metrics plus two successful Hermes 4K logs.
