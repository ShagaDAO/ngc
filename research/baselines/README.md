# Baseline Analysis

Performance analysis of existing codecs and neural compression approaches.

## Traditional Codecs on Gaming Content

**H.264/AVC**: Still the standard for low-latency streaming. Hardware encoders (NVENC/VCN) hit sub-frame latency with ultrafast presets. CBR keeps network traffic predictable.

**H.265/HEVC**: Better compression but higher latency. Hardware support varies. Most mobile clients decode H.264 more efficiently.

**AV1**: Great compression, but encoding speed and power consumption remain challenging for real-time gaming on mobile hardware.

## Neural Compression Results

**VFIMamba**: O(n) complexity actually works. 33.34 dB PSNR competitive with traditional methods. Mixed-SSM blocks handle temporal modeling efficiently.

**MobileNVC**: Proves neural codecs work on actual phones. 38.9 FPS on Snapdragon 8 Gen 2. Block-based motion estimation keeps power consumption reasonable.

**GameNGen (Google DeepMind)**: Control conditioning works. 20 FPS DOOM execution shows neural models can understand game state. 4-step sampling makes diffusion models practical.

## Performance Targets

**Quality**: Match H.264 PSNR/SSIM while reducing bandwidth
**Latency**: <50ms inference per frame
**Mobile**: <4W system power, <42°C surface temp
**Model size**: <100MB for mobile deployment

## Key Insights

Traditional codecs optimize for general video. Games have structure (predictable physics, limited assets) that neural models can exploit. Control inputs provide causality information that traditional codecs ignore. See [literature review](../literature_review/README.md) for detailed analysis.

The bottleneck isn't computational complexity - it's memory bandwidth and thermal management on mobile hardware. 