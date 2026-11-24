# [Benchmark] DGX Spark: Qwen3.6 Q8_0 and Flash-Next UD-Q2_K_XL, custom API + Hermes comparison

Single GB10, 128 GB nominal unified memory. Strata Control 0.2.21 / engine 0.1.67 previously reported. Qwen3.6 MTP2, four/two slots; Flash-Next DFlash2, one slot, 256K. Flash-Next direct 4K/16K/32K decode: 61.5/53.4/51.9 tok/s. Qwen3.6 32K decode was about 10.5 tok/s in both slot configurations. Could maintainers advise on the long-context behavior and best way to contribute this adapted suite? This is not a claim of compliance with the full upstream protocol.

Reports, measurements and available evidence: REPOSITORY_URL

Limitations: n=1 per case, differing output lengths, cache and acceleration. Both Flash-Next exports are included in v1.0, with redactions.
