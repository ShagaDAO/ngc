# Literature Review: Neural Game Codecs

What actually works for control-conditioned video generation.

## Key Papers

**DCVC-FM (2024)**: Finally handles long sequences without falling apart. 29.7% bitrate reduction, 32-frame refresh cycle prevents drift. Dual quantization works - global scaler for user control, spatial scaler adapts to content.

**MobileNVC (Qualcomm)**: Proves neural codecs work on real phones. 38.9 FPS 1080p on Snapdragon 8 Gen 2. Block-based motion with 8-bit quantization keeps power reasonable. 24.5 kMACs/pixel is actually achievable.

**VFIMamba (NeurIPS 2024)**: O(n) complexity SSMs beat O(n²) transformers for temporal modeling. Mixed-SSM blocks handle bi-directional processing efficiently. Linear complexity means extended gaming sessions won't kill performance.

**GameNGen (Google DeepMind)**: First neural model running DOOM at 20 FPS real-time. Control conditioning works: 64 frames + 64 actions → next frame. 4-step sampling makes diffusion practical. Noise augmentation (0.3-0.7 level) prevents drift.

**Hunyuan-GameCraft (2025)**: Maps W,A,S,D,mouse to continuous camera parameters. Model distillation gets 20x speedup (6.6 FPS real-time). Shows discrete game controls can be embedded effectively.

**MobileCodec (2022)**: Asymmetric architecture - heavy server encoder, light mobile decoder. 31 FPS HD 720p on Snapdragon 8. Flow-agnostic motion (no pixel warping) keeps mobile implementation simple.

## What This Means

**The Stack That Works**:
```
VFIMamba temporal modeling
+ DCVC-FM stability (32-frame refresh)
+ MobileNVC mobile deployment
+ GameNGen control conditioning
+ Hunyuan-GameCraft parameter mapping
```

**Key Insights**:
- Control conditioning actually works (GameNGen proved it)
- Mobile deployment is possible with right architecture choices
- Linear complexity temporal models are essential for long sessions
- 32-frame refresh cycles prevent temporal drift
- Asymmetric server/client architecture makes sense for power constraints

**Engineering Priorities**:
1. Control input mapping (W,A,S,D → continuous parameters)
2. Temporal stability (feature refresh every 32 frames)
3. Mobile optimization (8-bit quantization, block-based motion)
4. Drift prevention (noise augmentation)

**What Doesn't Work**:
- DCVC-RT: GPU-only, not mobile viable
- GameCodec: Requires game engine integration
- EMA-VFI: O(n²) complexity, too slow
- Pure diffusion: Too computationally expensive

The research shows neural game codecs are technically feasible. The bottleneck is operational efficiency - memory bandwidth and thermal management, not raw compute power.