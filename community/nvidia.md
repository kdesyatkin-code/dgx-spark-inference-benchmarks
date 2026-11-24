# 75 local Qwen inference runs on one DGX Spark: Ollama vs Strata, including Hermes

I measured 75 runs across five configurations on one GB10 system. Qwen3.6 Q8_0 and Flash-Next UD-Q2_K_XL are separate studies. Strata won all 12 direct Flash-Next latency cases, while Ollama won two of three Hermes workloads. Both passed nine functional checks per configuration. Qwen3.6 behaved differently, with a large Strata 32K slowdown. I would appreciate feedback on GB10 memory behavior, cache controls and reproducible agent benchmarking.

Reports, measurements and available evidence: REPOSITORY_URL

Limitations: n=1 per case, differing output lengths, cache and acceleration. Both Flash-Next exports are included in v1.0, with redactions.
