# SHAGA: The First Neural Content Delivery Network

**Distributed Data Collection + Distributed Compute = Neural Content Delivery Networks**

## The Core Insight

Traditional video codecs predict the next frame from previous frames. In games, you have something more powerful: the player input that caused each frame change. 

Every W,A,S,D keystroke, every mouse movement is the causal signal that generated the visual change. Instead of compressing the pixels, you can compress the causality itself.

**Neural Game Codecs**: AI models that generate game frames from player inputs, trained on synchronized gameplay data at massive scale.

Games have unique properties that make this revolutionary approach possible:

**Predictable Physics**: Player inputs produce more predictable visual outcomes than natural video. W+A+mouse_delta → constrained camera trajectory → learnable pixel transformations.

**Finite Asset Space**: Games use limited textures, models, and animations. Neural auto-encoders can learn compressed representations of these recurring visual patterns.

**Causal Structure**: Unlike natural video, game frames have explicit causality. Frame N+1 is deterministically generated from Frame N + Control Input N. Critically, frames encode most of all hidden states from the game executable/engine - the visual output contains all the information that matters to the gamer.

## The Opportunity

**What makes this possible now:**
- SHAGA has operational gaming network (data source)
- Mobile NPUs improving rapidly, though still power-intensive
- Neural video generation breakthroughs (GameNGen, Diffusion models)
- Geographic constraints create defensible market positions

**What makes this urgent:**
- First comprehensive gameplay dataset wins
- Google lost direct cloud gaming data collection (no Stadia)
- Mobile hardware efficiency improving rapidly
- Neural video generation advancing quickly

**The Business Case**: CDNs like Twitch spend most bandwidth on top 5 games. Optimizing compression for individual games creates immediate value while building toward the full causal streaming vision.

## Technical Solution

**The Physics of Self-Improving Networks**

Traditional CDN: Moves video bits from servers to clients
**Neural CDN**: Uses distributed compute to train AI models that reduce bandwidth requirements for recurrent traffic

**Control-Conditioned Compression**
```
Standard: Predict frame N+1 from previous frames
Neural: Predict frame N+1 from previous frames + controller input
```

**Bandwidth Reduction Potential** (1080p@60fps)
- Traditional stream: 6-8 Mbps
- Neural codec: 1.55 Mbps anchor frames + 50 Kbps control data
- Target: 20% reduction (conservative), 75% theoretical maximum

**Power Consumption Projections**
- Current mobile hardware: ~15-35W for neural processing
- Optimized NPU: ~3-7W (next-generation)
- Custom ASIC: ~1-2W (theoretical limit with dedicated hardware)

## Implementation Strategy

**Phase 1: Game-Specific Neural Compression (Proof of Concept)**

Before building full control-conditioned codecs, prove the concept with game-specific compression that exploits visual constraints:

**Game-Specific Advantages:**
- **Constrained Color Palettes**: Fortnite may only need 26 bits instead of 32 for colors
- **Repetitive Assets**: Same textures, animations, and effects appear constantly
- **Predictable Rendering**: Game-specific lighting and shading patterns

**"PNG for Fortnite" Approach:**
- Train neural codecs on single-game video streams (no controller inputs needed)
- Exploit game-specific visual patterns that H.264 can't optimize for - similar to content-specific specialization validated in academic CDN research
- Prove 20-30% bandwidth reduction on major games
- Use existing SHAGA stream data to validate compression gains

**Phase 2: Full Control-Conditioned Generation**

Once game-specific compression is proven, integrate controller inputs for the revolutionary "compress causality" approach described above.

## SHAGA Network Infrastructure

**Current Network Resources** (July 2025):
- **4.19 PFLOPS** total GPU compute (FP32)
- **39.51 Gbps** total network throughput
- **333 nodes** across 76 GPU models with full hardware profiling

**Training Approach**: Federated learning across gaming hardware during idle periods. Each node trains on locally-generated data, with model updates aggregated across the network.

**Network Effects and Model Convergence**:
- **Self-Improving Properties**: As more users play through the network, the models improve. Each gaming session provides additional training signal for the neural codecs.
- **Game-Specific Convergence**: Different games have different physics and visual patterns. Models trained on Rocket League learn different representations than those trained on Skyrim. Academic research confirms content-specific models reduce performance variation.
- **Federated Optimization**: Distributed training allows models to learn from diverse hardware configurations and network conditions, improving robustness.

The SHAGA network serves a dual purpose:
- **Gaming infrastructure**: Provides low-latency gaming to users
- **Data collection**: Generates training data for neural game codecs
- **Distributed training**: Uses idle gaming hardware to train models

## The Star Atlas Campaign (Phase 0)

**Why Star Atlas?**
- Predictable physics engine (learnable patterns)
- Consistent visual style (learnable by AI)
- Active player base (data generation)
- High bandwidth requirements (strong incentive to optimize)

**Phase 1 Target**: Game-specific neural compression using Star Atlas video streams
**Phase 2 Target**: Full control-conditioned generation with synchronized frame+control pairs
**Timeline**: Q3 2025 data collection, Q4 2025 neural codec prototype
**Strategic Value**: Prove the concept on one game, then expand to the full causal streaming vision

## Research Foundation

**Current State-of-the-Art Research**

**DCVC-FM (2024)**: 29.7% bitrate reduction with infinite sequence handling. Features dual quantization and 32-frame refresh cycles for temporal stability.

**VFIMamba (NeurIPS 2024)**: O(n) linear complexity temporal modeling using State Space Models. Mixed-SSM blocks enable control token injection.

**MobileNVC (Qualcomm)**: 38.9 FPS 1080p neural video decode on Snapdragon 8 Gen 2. Block-based motion with 8-bit quantization.

**GameNGen (Google)**: Neural DOOM execution at 20 FPS. Noise augmentation prevents drift, 4-step sampling for real-time performance.

**Hunyuan-GameCraft (2025)**: W,A,S,D,mouse → continuous camera parameters. Model distillation achieves 6.6 FPS real-time with 20x speedup.

**Current Architecture Stack**:
```
VFIMamba temporal modeling + DCVC-FM stability + MobileNVC deployment
+ GameNGen control conditioning + Hunyuan-GameCraft parameter mapping
= Control-conditioned video generation framework
```

The technical foundation is proven in academic literature. Neural enhancement in content delivery systems is an established research field with multiple deployed systems. **The missing piece is gameplay data at scale.**

**Technical Challenges & Solutions**

**Temporal Stability**: Neural models drift over long sequences
*Solution*: Feature refresh every 32 frames, noise augmentation

**Mobile Power**: Must match video decoder energy consumption  
*Solution*: 8-bit quantization, tiled execution patterns

**Real-time Latency**: Gaming requires <80ms end-to-end
*Solution*: Lightweight models, predictive generation with corrections. Academic literature shows similar latency targets across multiple neural CDN systems.

**Data Quality**: Training requires frame-perfect synchronization
*Solution*: SHAGA's existing network infrastructure handles this

**Current Limitations**: Neural codecs are 10-20x slower to encode than H.264 and consume significantly more power than traditional decoders. Mobile deployment requires substantial optimization and maybe dedicated hardware.

## Current Status

- **Network**: Operational with real users
- **Star Atlas Partnership**: Phase 0 data collection launching Q3 2025
- **Literature Review**: Complete technical analysis
- **Prototype**: Client-side interpolation in development

## The Vision

Neural Game Codecs transform content delivery from moving pixels to generating experiences. SHAGA's distributed network provides both the data to train these models and the infrastructure to deploy them.

**Success means**: Games that generate locally with minimal bandwidth, powered by AI trained on SHAGA's unique gameplay dataset & compute network.

**The race**: Build the training dataset before competitors realize what's possible.

## Documentation

- [Literature Review](research/literature_review/README.md) - Current state-of-the-art research analysis
- [SHAGA Technical Blueprint](https://zenodo.org/records/15778429) - Engineering blueprint 
- [Experimental Research](research/experiments/README.md) - Research methodology and validation approaches
- [Baseline Analysis](research/baselines/README.md) - Traditional codec performance analysis

---

*Time-sensitive: The window for collecting foundational neural gaming data is now. Google lost this capability with Stadia. SHAGA won't.* 