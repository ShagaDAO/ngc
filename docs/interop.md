# Interop: NGC ↔ GAP ↔ DGN

## Input (from GAP)
- Expect: GAP v0.x shards: 
  - `video/` frames or encoded stream
  - `controls.jsonl` @ 60 Hz with timestamps
- Use: convert into model-ready batches (notebooks/scripts), keep GAP meta intact for reproducibility.

## Output (toward DGN)
- **Research-only samples** (no live streamer):
  - `dgn-semantic-update-0.1.0.jsonl` (control-intent, camera, state deltas)
  - `dgn-residual-chunk-0.1.0.json` (compressed residuals for visual corrections)
- These are **offline artifacts** for analysis & validation against DGN schemas. 