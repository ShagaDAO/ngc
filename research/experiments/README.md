# Experimental Research Notes

Running experiments on the Shaga Network to validate neural game codec approaches.

## Current Status

Research framework established. Star Atlas Phase 0 data collection in progress (Q3 2025) enabling experimental validation.

## Questions We Need to Answer

- How much better is control conditioning vs traditional codecs?
- What's the actual energy trade-off: neural processing vs bandwidth savings?
- Can we build game-agnostic codecs or do we need per-game models?

## Experimental Plan

### Baseline Measurements
Test H.264, H.265, AV1 on gaming content from Shaga Network nodes. Measure compression ratios, encoding costs, quality metrics. Find out where traditional codecs fail on gaming content.

### Control Signal Analysis
Analyze controller inputs vs frame changes across different games. Quantify how predictable game state transitions are. Measure information content in W,A,S,D,mouse streams.

### Neural Codec Validation
Test approaches from [literature review](../literature_review/README.md) (DCVC-FM, MobileNVC, VFIMamba) on real gaming data. Compare compression efficiency vs computational cost. Validate mobile deployment claims.

## Metrics That Matter

- **Quality**: PSNR, SSIM, perceptual metrics
- **Performance**: Encoding/decoding speed, memory usage, power consumption
- **Efficiency**: Compression ratio vs computational cost
- **Real-world**: Network adaptation, thermal throttling, battery life

## Infrastructure Advantages

The Shaga Network provides:
- **4.19 PFLOPS** distributed GPU compute for neural codec validation
- Real gaming workloads (not synthetic datasets)
- Diverse hardware configurations for mobile deployment testing
- Actual network conditions under load
- Operational gaming infrastructure instead of lab conditions 