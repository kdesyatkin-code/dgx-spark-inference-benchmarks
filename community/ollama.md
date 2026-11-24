# GB10: Qwen3.6 Q8_0 initializes one slot despite four requested (0.32.15)

On one DGX Spark with Qwen3.6-35B-A3B Q8_0 and 262144 context, setting OLLAMA_NUM_PARALLEL=4 still produced n_slots=1 in the runner log. The fourth timed series was canceled; this is a historical observation, not a confirmed regression in 0.40.18. Is this expected for that architecture/build? The related Flash-Next study uses 0.40.18 and a single requested slot. Please treat the two versions separately. Before opening an issue, confirm current reproducibility and attach exact startup logs; otherwise share only as historical context.

Reports, measurements and available evidence: REPOSITORY_URL

Limitations: n=1 per case, differing output lengths, cache and acceleration. Both Flash-Next exports are included in v1.0, with redactions.
