# DGX Spark inference benchmarks

Independent, single-device comparison of local Qwen inference through Ollama and Strata, with direct API and Hermes end-to-end workloads. Measurements dated 2026-11-24.

| Study | Configurations | Runs |
|---|---|---:|
| [Qwen3.6 Q8_0](reports/qwen3.6/README.md) | Ollama 0.32.15; Strata 4/2 slots | 45 |
| [Flash-Next UD-Q2_K_XL](reports/flash-next/README.md) | Ollama 0.40.18; Strata DFlash2 | 30 |

Key finding: faster direct decode does not necessarily yield faster agent task completion. Qwen3.6 and Flash-Next are separate studies; do not pool results as an engine ranking.

[Russian overview](README_RU.md) · [Methodology](methodology/README.md) · [All 75 measurements](measurements.csv) · [Evidence status](EVIDENCE.md) · [Publication drafts](community/README.md)

**v1.0:** both Flash-Next exports included; all 15 Ollama wall measurements and fixture hashes verified against the original export. No statistical significance claim. The planned IQ4 series is not included.
