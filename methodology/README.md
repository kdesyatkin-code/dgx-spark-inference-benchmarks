# Methodology

15 cases per configuration, one measured run each: Hermes 4K/16K/Short, direct 4K/16K/32K, retrieval R1–R3, tool T1–T3, instructions I1–I3. The 13 original fixture files are in `test-prompts/`; Hermes uses first message content for its three tasks, direct API uses full messages and tools. No enforced output cap or JSON mode; thinking enabled. Sequential warm model requests; cache reuse recorded when available. Wall time includes client/agent overhead. Prefill rate uses newly processed tokens where available. Decode includes reasoning where counted. Functional checks require exact retrieval, one expected structured tool call without execution, or strict JSON values/types. Agent exit status is not a quality score.

Hardware: one GB10, Linux ARM64, nominal 128 GB unified memory. No concurrent throughput claim. Different sampling/formatting, caching and engine optimizations not controlled. Direct API routes differ (native Ollama vs OpenAI-compatible Strata), Hermes uses compatible endpoint. 4K/16K labels describe fixture lengths, not actual total agent context. Resource snapshots are not peaks. No matched CPU/GPU energy sampling. No pooled statistics across model versions.

Fixtures are adapted synthetic workloads; not a certified upstream standard benchmark. See upstream [Strata protocol](https://github.com/Niko1221/Strata/blob/main/docs/BENCHMARK_PROTOCOL.md) for submission requirements.

Next study (not yet measured): UD-IQ4_XS, 15 cases × 3 repeats × 2 engines; record load, continuous resource sampling and cache state, median and range; check quality and Hermes overhead.
