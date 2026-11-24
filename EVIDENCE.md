# Evidence status

- Qwen3.6: previously anonymized archive of 190 entries, including fixture files, logs and manifest; 43 wall metrics and two successful Hermes 4K timed logs. Original archive layout split here into raw-results and test-prompts. Original manifest paths refer to the source ZIP layout.
- Flash-Next Strata: 57 exported files, text anonymized; normalized metrics and source references in CSV.
- Flash-Next Ollama: 57 original exported files included under `raw-results/flash-next/ollama/`, with container IP redacted. All 15 wall times, fixture hashes and RAM snapshots agree with the CSV, as do all 12 direct rate/token metrics and nine functional pass flags. Hermes rate/token columns are from the corresponding server logs as previously transcribed, not the wall metrics JSON. Two smoke transcripts are supplementary.
- The included evidence is not a fresh rerun. Original OS/driver details and matching model file hashes are incomplete.
- Usernames, private network addresses and hostnames were removed from new evidence with pattern-based redaction; review before public upload. No credentials intentionally included.
