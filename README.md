# Shaga: The First Neural Content Delivery Network

> **NGC = research repo.** No production code here.
> - **Data spec + validator:** lives in **GAP** → https://github.com/ShagaDAO/gap  
> - **Wire protocol + validator:** lives in **DGN** → https://github.com/ShagaDAO/dgn  
> - **NGC's job:** explore neural game codecs that *consume GAP data* and *could emit DGN frames* in future.

> **Posture:** Research-only. Performance numbers are **targets**, not guarantees.  
> **Provenance:** AI-assisted for docs/boilerplate with human review (see PROVENANCE.md).  
> **Security:** No runtime code; see SECURITY.md.

## How the repos fit (one view)

GAP (frames+controls spec) ➜ [validated shards] ➜ NGC (research: train/eval codecs) ➜ DGN (protocol: SemanticUpdate + ResidualChunk)

- **GAP → NGC:** NGC experiments assume GAP v0.x shards (video + controls JSONL).
- **NGC → DGN (future):** When we prototype, we'll export "SemanticUpdate/ResidualChunk" *samples* that conform to DGN's schemas for analysis.

**Distributed Data Collection + Distributed Compute = Neural Content Delivery Networks**

> ### Context split (avoid confusion)
> - **Shaga Network usage stats (165k MAU, 200k+ hours)** refer to **classical game streaming** on Shaga – not neural codecs.
> - **NGC** is research toward neural codecs. We do **not** deploy NGC in production.
> - When we say "targets" (e.g., 2–5 Mbps, ≤50 ms): these are **engineering targets**, not measured results. See BENCHMARKS.md.

## The Structure

**Shaga Labs** (company) → built software → run by **Shaga users** → in **The Shaga Network** (infrastructure) → generates data and compute → for **Neural Game Codecs** (research) → that transforms Shaga Network into a **Neural Content Delivery Network**

*This repository documents the Neural Game Codecs research. The [Shaga Network](shaga-network/) is the operational infrastructure built by Shaga Labs and run by Shaga users that provides the training data and distributed compute needed to make NGC a reality.*

## The Core Insight: Compressing Causality

Traditional video codecs predict the next frame from previous frames. In games, player inputs (e.g., W,A,S,D keystrokes, mouse movements) causally drive changes, enabling compression of the causality itself rather than pixels.

**Neural Game Codecs**: AI models trained on synchronized gameplay data to generate frames from inputs at scale.

This shifts content delivery via:
- **Predictable Physics**: Inputs yield constrained, learnable visual outcomes.
- **Finite Asset Space**: Limited textures/models allow compressed representations.
- **Causal Structure**: Frames encode game states; Frame N+1 derives from Frame N + Input N.

## The Opportunity: A Transformative Moment

**Enablers Now**:
- Operational Shaga Network as unique data source.
- Rapid mobile NPU improvements (despite power intensity).
- Breakthroughs like GameNGen proving neural video gen.
- Geographic edges for first-mover advantages.

**Urgency**:
- First comprehensive gameplay dataset dominates.
- Google's Stadia shutdown lost their data edge.
- Hardware efficiency and neural gen advancing fast.

**Business Case**: Optimize for top games (e.g., Twitch's bandwidth hogs) for quick wins, building to full causal streaming.

## Technical Solution: Self-Improving Networks

**Approach**:
```
Traditional CDN: Transmits video bits.
Neural CDN: Trains AI to cut bandwidth for recurring content.

Standard: Predicts from prior frames.
Neural: Predicts from prior frames + inputs.
```

**Bandwidth Potential** (1080p@60fps):
- Traditional: 6-8 Mbps.
- Neural: 1.55 Mbps anchors + 50 Kbps controls.
- Target: 20% reduction (conservative); up to 40-50% theoretically.
- Reality: Varies by game predictability.

**Current Gaps**: Neural encoding 10-20x slower than H.264; decoding 3-7W vs. 0.5W mobile. Closing via hardware.

**Energy Analysis**:
- Transmission: 10-100 nJ/bit (WiFi); 1-3 nJ/bit (5G).
- Neural: 0.1-10 pJ/MAC.
- Trajectory: NPUs/ASICS narrowing gap.
- **Economics**: See [Energy Economics Analysis](research/energy_economics/README.md) for break-even scenarios and market-specific deployment strategies.

**Latency**: <80ms RTT limits to ~500km fiber, favoring regional networks.

## Implementation Strategy

**Phase 1 (2025-2027)**: Game-specific compression.
- Train on streams (no inputs initially).
- Exploit limited visuals for 15-25% savings.
- Validate with Shaga data.

**Phase 2 (2027-2030)**: Add control-conditioned gen.

**Challenges Addressed**:
- Stability: 32-frame refresh (DCVC-FM).
- Power: Quantization/hardware (MobileNVC).
- Performance: Linear models (VFIMamba).
- Multiplayer: Hybrid state management.
- Security: Server validation/anti-cheat.

## Shaga Network Advantage

**Resources**: Detailed in [Shaga Network](shaga-network/).

**Hybrid Setup**:
- Decentralized: P2P data gen with incentives.
- Centralized: AI training/aggregation/deployment.

**Network Effect**: More users → better models → efficiency gains.
**Moat**: Operational data collection beats incumbents.

## Research Foundation

**Components**:
- DCVC-FM: 29.7% bitrate cut, stable.
- VFIMamba: O(n) for sequences.
- MobileNVC: 38.9 FPS 1080p mobile.
- GameNGen: 20 FPS control-conditioned Doom.
- Lee et al.: Content-specific optimization.

**Challenge**: Integrate for real-time modern games—Shaga's focus.

## Star Atlas Proof-of-Concept

**Why**: Predictable physics, consistent style, active base, high bandwidth.
**Timeline**:
- Phase 0 (2025): Data/baseline.
- Phase 1 (2026-2027): Compression prototype.
- Phase 2 (2028-2030): Full gen.

## Current Status

- Network: Operational, generating data.
- Partnership: Star Atlas Phase 0 (Q3 2025).
- Review: SOTA analysis complete.
- Prototype: Compression in dev.

**Assessment**: High-risk/reward; challenges unsolved, but insight sound and infrastructure ready.

## The Vision: Transforming Delivery

Neural Game Codecs shift from pixel-moving to experience-gen:
- 20-50% bandwidth cut.
- New interactive media.
- Advantages for adopters.
- Gaming economics overhaul.

**Approach**: Encode causality rather than pixels.
**Advantage**: Operational data collection infrastructure.
**Goal**: Local generation with minimal bandwidth.

## Toy pass-through (offline)
This repo is **research only**. To make the "GAP → NGC → DGN" flow concrete, we include two **DGN‑shaped sample files**:

- `samples/dgn/semantic_update.jsonl`
- `samples/dgn/residual_chunk.json`

They are schema-only examples (static), so DGN's validator can confirm the wire format:
```bash
# from the DGN repo
python3 tools/validator/cli.py check --schema dgn-semantic-update-0.1.0.json <path>/ngc/samples/dgn/semantic_update.jsonl
python3 tools/validator/cli.py check --schema dgn-residual-chunk-0.1.0.json <path>/ngc/samples/dgn/residual_chunk.json
```

### Compatibility
| Producer | Consumer | Status |
|---|---|---|
| GAP v0.2.x shard | NGC notebooks/tools (research) | ✅ supported (toy) |
| NGC DGN‑shaped samples | DGN validator | ✅ passes schemas |
| DGN 0.1.0 schemas | DGN validator | ✅ CI enforced |

## Documentation

- [Literature Review](research/literature_review/README.md)
- [Energy Economics Analysis](research/energy_economics/README.md)
- [Shaga Blueprint](https://zenodo.org/records/15778429)
- [Experiments](research/experiments/README.md)
- [Baselines](research/baselines/README.md)

---

*Projections based on current trends; actual results may vary. High-risk research with transformative potential.* 