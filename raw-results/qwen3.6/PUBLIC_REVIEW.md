# Public archive review

This archive contains anonymized copies, not byte-identical original logs.
45 measured runs: 15 Ollama V1, 15 Strata V1, 15 Strata V2.
All 13 source prompt files retain their original SHA-256 hashes; all recorded source hash references match a supplied source file.
44 files named *-metrics.json exist, of which 43 have wall_seconds.
Ollama V1 Hermes 4K: 15.36 s from results/ollama-hermes-4k-r1-direct.log (exit 0); engine timing in results/ollama-server.log.
Strata V1 Hermes 4K: 37.17 s from results/strata-hermes-4k-r1.log (exit 0); the corresponding metrics JSON is a server snapshot, not a normalized metric record.
results/ollama-hermes-4k-r1.log is an unsuccessful HTTP 503 attempt, excluded from the 45 measured runs.
results-v2/engine-log.txt, memory.txt, strata-status.txt and running-containers.txt document the preliminary launch with other services running, not the clean measured launch. Do not infer measured V2 GPU placement from those preliminary artifacts.
27 functional checks are marked passed in the recorded metrics (9 per configuration); this is not a fresh execution of the tests.
The private container inventory was replaced with its count. Local timestamps, request IDs, public model digests and software versions are retained for traceability.
No obvious credentials or private IPv4 addresses remained in the inspected text. Pattern-based review cannot guarantee absence of all private information.
The later Ollama four-slot attempt and the clean Strata V2 startup log are not separately captured in this archive.
