# Experimental Research Notes

Running experiments on SHAGA's gaming network to validate neural game codec approaches.

## Current Status

Framework ready. Waiting for Star Atlas Phase 0 data collection (Q3 2025) to start experimental validation.

## Questions We Need to Answer

- How much better is control conditioning vs traditional codecs?
- What's the actual energy trade-off: neural processing vs bandwidth savings?
- Can we build game-agnostic codecs or do we need per-game models?

## Experimental Plan

### Baseline Measurements
Test H.264, H.265, AV1 on gaming content from SHAGA nodes. Measure compression ratios, encoding costs, quality metrics. Find out where traditional codecs fail on gaming content.

### Control Signal Analysis
Analyze controller inputs vs frame changes across different games. Quantify how predictable game state transitions are. Measure information content in W,A,S,D,mouse streams.

### Neural Codec Validation
Test literature review approaches (DCVC-FM, MobileNVC, VFIMamba) on real gaming data. Compare compression efficiency vs computational cost. Validate mobile deployment claims.

## Metrics That Matter

- **Quality**: PSNR, SSIM, perceptual metrics
- **Performance**: Encoding/decoding speed, memory usage, power consumption
- **Efficiency**: Compression ratio vs computational cost
- **Real-world**: Network adaptation, thermal throttling, battery life

## Infrastructure Advantages

SHAGA's 333 nodes across 76 GPU models provide:
- Real gaming workloads (not synthetic datasets)
- Distributed testing environment
- Actual network conditions
- Mobile hardware diversity

Testing on operational gaming infrastructure instead of lab conditions. 