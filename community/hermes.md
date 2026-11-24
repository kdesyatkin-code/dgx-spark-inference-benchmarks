# Local Hermes performance on DGX Spark: why decode speed is not task latency

I compared Ollama and Strata with Qwen3.6 and Flash-Next using the same three Hermes fixtures. Flash-Next direct API latency favored Strata, but two of three agent wall-time tasks favored Ollama. Ollama used one model request per agent task; Strata made multiple requests and one 4K measurement overlapped an earlier canceled request. Short tasks received roughly 14.5K system-context tokens. Which supported provider/cache/toolset configuration would best preserve full agent functionality while improving end-to-end performance?

Reports, measurements and available evidence: REPOSITORY_URL

Limitations: n=1 per case, differing output lengths, cache and acceleration. Both Flash-Next exports are included in v1.0, with redactions.
