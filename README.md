# APEX-KV
**Attention Pointer EXtraction for KV Cache**

Fuzzy KV cache reuse for transformer inference.
Fingerprints attention head pointer sets with SimHash + MinHash,
performs O(1) fuzzy lookup via LSH band indexing.

## Measured Results (N=10 runs, Welch t-test, CPU)
| Metric | Exact Match | APEX-KV | Δ |
|---|---|---|---|
| Hit rate | 91.0% | 98.3% | +7.3pp |
| Collisions | 0 | 0 | — |
| Lookup at 8K entries | 3,693μs | 1.9μs | 1979× |
| Throughput | 3,663 tok/s | 2,920 tok/s | −20.3% |

## Files
- `apex_kv_core.py` — transformer + attention extraction
- `lsh_index.py` — O(1) LSH band index
- `benchmark_v2.py` — benchmark harness

## Known Limitations
- Throughput gap vs exact match not yet resolved
- Tested on scratch-trained model, not GPT-2/Llama
- Stale LSH entries need compaction at production scale

## Next Step
Run on GPT-2 via HuggingFace to validate domain-routing
hypothesis on a model with documented head specialisation.
