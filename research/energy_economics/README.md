# Energy Economics of Neural Game Codecs

**A comprehensive analysis of when neural video decoders make economic sense**

## Executive Summary

Neural video decoders consume 20 mJ/frame (phone) to 1 J/frame (GPU) but rarely achieve energy break-even on modern networks. The business case depends on **dollar savings** from expensive bandwidth, not energy efficiency. This analysis examines real-world scenarios where neural codecs can be economically justified.

## The 20 mJ / 1 J Break-Even Analysis

| Device class                                                                                                         | Extra energy a *today‑class* neural **decoder** needs (1080p @ 60 fps) | How much *network* you must save for the trade to break even **in energy terms**                                                                                         | Does that happen in practice?                                                                                                |
| -------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------- |
| **Phone / tablet** running **MobileNVC** on the on‑die NPU (≈ 24 GMAC/frame, 0.5 pJ/MAC on an Edge‑TPU‑class engine) | **≈ 20 mJ / frame** → ≈ 1.2 J / s ([CVF Open Access][1], [Coral][2])   | 1.2 J / s ÷ (1–3 nJ/bit over 5 G/Wi‑Fi) ⇒ **0.4–1.2 Gbit / s of avoided radio traffic** ([ResearchGate][3])                                                              | No. A whole H.264 stream is only 6–8 Mbit / s; the radio itself is already far more energy‑efficient than the extra compute. |
| **Cloud GPU** (RTX 4080 class, 100 W to run a DCVC‑RT decoder)                                                       | **≈ 1.7 J / frame** → 100 W ≈ 0.10 kWh / h                             | Monetary, not energy: at AWS **\$0.045 / GB egress** ([Amazon Web Services][4]). Saving 3 GB / h yields \$0.13 / h – *>10×* the \$0.01 / h electricity the GPU consumes. | Yes – in clouds the *dollar* cost of bandwidth dwarfs electricity, so neural decode can pay for itself.                      |

**Take‑away**: The "20 mJ (phone) or 1 J (GPU) per frame" threshold is almost never met by the **energy** you save on a modern wired or wireless link, but it *can* be met by the **dollars** you save on metered or premium bandwidth (cloud egress, satellite, mobile data).

## Hardware Efficiency Roadmap

| Year / node                        | Best‑in‑class *edge* NPU efficiency                         | Energy to run a MobileNVC‑size decode (24 GMAC) |
| ---------------------------------- | ----------------------------------------------------------- | ----------------------------------------------- |
| 2022 (Edge TPU 28 nm)              | **2 TOPS / W** → 0.5 pJ/MAC ([Coral][2])                    | **12 mJ / frame**                               |
| 2025 (Snapdragon 8 Gen 3 4 nm)     | **\~6 TOPS / W** (40 %/W better than Gen 2) ([Qualcomm][5]) | **4 mJ / frame**                                |
| 2027 road‑mapped NPU (3 nm + INT4) | **≥12 TOPS / W** (industry target)                          | **≤2 mJ / frame**                               |

Even with aggressive efficiency improvements, neural decoding will still cost roughly **the same energy as lighting a frame on a mid‑brightness OLED** (~20 mJ) and remain an order of magnitude more expensive than hardened AV1 or VVC ASICs (<0.5 mJ/frame).

## Economic Justification Scenarios

### Where Neural Codecs Make Economic Sense

| Scenario                                                 | Why neural decode can make economic sense                                                                                                                                                                               |
| -------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Satellite & fixed‑wireless access (Starlink, OneWeb)** | Starlink charges **\$1 / GB** over the 1 TB monthly cap ([Concord Marine Electronics][6]). Compressing 3 GB/h of 4 K gameplay down to 1 GB/h saves \$2/h – far more than the \~\$0.02/h electricity to run an Edge‑GPU. |
| **Mobile‑data pay‑as‑you‑go markets**                    | Pre‑paid 5 GB top‑ups at \$15 (‑‑> \$3/GB) ([Tom's Guide][7]). For commuters on capped plans the *monetary* value of every Mbit dwarfs the battery hit.                                                                 |
| **Cloud‑gaming broom‑closets**                           | In hyperscale DCs, **egress is the #1 operating cost**; labour and power to run extra GPUs is secondary. A 30 % bitrate cut pays off in days at \$0.05/GB egress.                                                       |
| **Bandwidth‑starved rural ISPs**                         | 1–5 Gbit/s microwave back‑haul links price out at \$0.02–0.10 / GB. When the link is saturated, spending rack power on extra inference can defer a six‑figure capacity upgrade.                                         |

### Where Neural Codecs Don't Make Economic Sense

- **Residential fibre, cable or PON** – marginal cost is <\$0.001 / GB
- **Enterprise/LAN streaming** – 10 GBase‑T moves a gigabyte for micro‑joules
- **Battery‑sensitive wearables** (AR glasses) where every milliwatt counts – purpose‑built ASIC video decoders will stay an order of magnitude more frugal than a general NPU for years

## Risk Assessment for SHAGA Project

| Dimension                               | Today (2025)                                                                      | 3‑year outlook                                                 | Risk                                                                     |
| --------------------------------------- | --------------------------------------------------------------------------------- | -------------------------------------------------------------- | ------------------------------------------------------------------------ |
| **Decoder energy**                      | 20 mJ/frame (phone) / 1 J/frame (GPU)                                             | 2–10 mJ / 0.2–0.4 J with 3 nm NPUs & INT4                      | **Medium** – still higher than hardware AV1; depends on ASIC adoption.   |
| **Achievable bitrate cut**              | 20–30 % vs AV1 on mainstream 3‑D games (WACV‑24 MobileNVC) ([CVF Open Access][1]) | Maybe 40 % with control‑conditioned models                     | **High** – diminishing returns; classical VVC/H.266 keeps improving too. |
| **Bandwidth price where payoff starts** | ≳ \$0.05 / GB server‑side or \$1 / GB client‑side                                 | Falls if ASIC NPUs become ubiquitous                           | **Market‑dependent** – cheap fibre kills the thesis.                     |
| **Hardware roadmap**                    | No mass‑market phones yet ship NGC blocks                                         | Flagship SoCs add INT4 tensor units, but still general‑purpose | **Execution** – needs silicon vendor buy‑in.                             |

## Strategic Implications

### For SHAGA Network

**Opportunity**: The Shaga Network's distributed compute model aligns perfectly with scenarios where neural codecs make economic sense:
- **Cloud gaming**: Distributed nodes reduce egress costs
- **Bandwidth-constrained regions**: Rural nodes serve local users efficiently
- **Premium bandwidth markets**: Satellite and mobile data scenarios

**Positioning**: Focus on high-bandwidth-cost scenarios rather than universal deployment:
- Target cloud gaming services with high egress costs
- Prioritize regions with expensive or limited bandwidth
- Develop partnerships with satellite internet providers

### Business Model Implications

**High-risk/high-reward**: The business case depends on two curves crossing:
1. **Hardware efficiency**: Neural decoders reaching <2 mJ/frame
2. **Bandwidth pricing**: Maintaining ≥\$0.50/GB in target markets

**If curves cross**: Massive opportunity (half the traffic bill)
**If curves don't cross**: Niche market in expensive-bandwidth scenarios only

## Conclusion

Neural game codecs are **not a universal win** but can be economically justified in specific scenarios where bandwidth costs dominate compute costs. The SHAGA project should:

1. **Focus on high-bandwidth-cost scenarios** (satellite, mobile data, cloud egress)
2. **Leverage distributed architecture** to reduce data transfer costs
3. **Plan for market-specific deployment** rather than universal adoption
4. **Monitor hardware efficiency curves** and bandwidth pricing trends

The physics favor dedicated video ASICs, but economics can favor neural codecs in the right market conditions.

## References

[1]: https://openaccess.thecvf.com/content/WACV2024/papers/van_Rozendaal_MobileNVC_Real-Time_1080p_Neural_Video_Compression_on_a_Mobile_Device_WACV_2024_paper.pdf "MobileNVC: Real-Time 1080p Neural Video Compression on a Mobile Device"
[2]: https://coral.ai/static/files/Coral-M2-Dual-EdgeTPU-datasheet.pdf "M.2 Accelerator with Dual Edge TPU datasheet - Coral"
[3]: https://www.researchgate.net/figure/Energy-consumption-per-bit-nJ-bit-transmitted-in-different-ways_tbl1_330479275 "Energy consumption per bit (nJ/bit) transmitted in different ways"
[4]: https://aws.amazon.com/vpc/pricing/ "Amazon VPC Pricing"
[5]: https://www.qualcomm.com/products/mobile/snapdragon/smartphones/snapdragon-8-series-mobile-platforms/snapdragon-8-gen-3-mobile-platform "Snapdragon 8 Gen 3 Mobile Platform"
[6]: https://concordelectronics.com/starlink-plans-your-complete-guide-to-2025-starlink-plan-changes-and-starlink-internet-costs/ "Starlink Plans: 2025 Changes and Internet Costs Guide"
[7]: https://www.tomsguide.com/us/best-cheap-cell-phone-plans,review-4504.html "The best cheap cell phone plans 2025" 