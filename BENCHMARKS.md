# RulMiner benchmarks

Real numbers from our own cards, mining Pearl on the Kryptex pool (November 2026, RulMiner 3.1.0, Windows 11, NVIDIA 621.x drivers). Your results depend on the card model, cooling, room temperature, driver and settings.

## What changed in 3.1

RulMiner 3.1 runs a new hand-written kernel on RTX 50-series cards (based on llmjob's open-source sm_120 fold, MIT license; see THIRD-PARTY-LICENSES.txt). Every result it produces is still checked against Pearl's official verifier before a share is sent. Same card, same settings, 60-second benchmarks:

| RTX 5070 Ti setting | 3.0 kernel | 3.1 kernel | Gain |
|---|---|---|---|
| No clock lock, 300 W | 191.7 TH/s | 200.5 TH/s | +4.6% |
| No clock lock, 275 W | 187.5 TH/s | 196.8 TH/s | +5.0% |
| No clock lock, 250 W | 183.5 TH/s | 192.4 TH/s | +4.9% |
| Lock 3000 MHz, +499 MHz, memory 810 MHz | 201.9 TH/s | 212.7 TH/s | +5.4% |

The new kernel reaches about 99% of the card's INT8 tensor throughput at its clock (tensor operations per clock × number of SMs; the 3.0 kernel reached 94%), so speed now follows the core clock almost exactly. On our 3-card 5060 Ti / 5060 rig the gain was about +4%.

## Summary (miner-reported speed, RulMiner 3.1)

| Card | Settings | Speed | Board power | Efficiency |
|---|---|---|---|---|
| RTX 5070 Ti | stock clocks, 270 W limit | ~197 TH/s | 270 W | ~730 GH/W |
| RTX 5070 Ti | lock 3000 MHz, +499 MHz, memory 810 MHz | **212.5 TH/s** | ~245 W | **~870 GH/W** |
| RTX 5060 Ti | stock clocks, 180 W limit | ~104 TH/s | ~156 W | ~660 GH/W |
| RTX 5060 Ti | lock 3100 MHz, +400 MHz | **~110 TH/s** | ~147 W | ~750 GH/W |
| RTX 5060 | lock 3100 MHz, +400 MHz, 145 W limit | **94.5 TH/s** | 145 W | ~650 GH/W |
| RTX 5060 | lock 3100 MHz, +400 MHz, 125 W limit | 90.5 TH/s | 125 W | ~720 GH/W |

The tuned rows are our own cards. Offsets of +400 to +500 MHz are not safe on every chip: start lower, or let **Find my best settings** test your card (it checks every setting against the official verifier before showing it). The tuner's built-in suggestions stay at the more conservative settings from 3.0.

With a clock lock and a high offset the 5070 Ti only draws ~245 W, so its power limit (250-300 W) no longer changes the speed. On the 5060 the 145 W limit is the ceiling: 150 W added nothing, and 125 W gives up 4% speed for 14% less power.

## Versus other miners (RTX 5070 Ti, same settings)

One card (our RTX 5070 Ti), lock 3000 MHz, +499 MHz, memory 810 MHz, 270 W limit, mining on Kryptex. Each miner ran 7 minutes twice, in alternating order (A B C A B C), miner-reported hashrate averaged from minute 2 on. A single small sample, not a full benchmark suite:

| Miner | Run 1 | Run 2 | Board power | Efficiency | Dev fee |
|---|---|---|---|---|---|
| RulMiner 3.1.0 | 212.45 TH/s | 212.53 TH/s | 244.9 W | 867.7 GH/W | 1% |
| SRBMiner-Multi 3.8.9 | 213.65 TH/s | 213.47 TH/s | 231.3 W | 923.3 GH/W | 2% |
| PeakMiner 2.2.08rc3 | 211.70 TH/s | 211.74 TH/s | 247.4 W | 855.7 GH/W | see its docs |

- **Speed:** within 0.5% of each other at the same clock. After dev fees (RulMiner 1%, SRBMiner 2%), RulMiner and SRBMiner come out about even, and RulMiner is level with PeakMiner.
- **Efficiency:** SRBMiner uses about 14 W less on this card (6.4% more TH/s per watt). Under a power limit that matters. Stock clocks, 270 W limit (short runs, about 30 s of samples each): SRBMiner 200.0 TH/s at 2808 MHz, RulMiner 197.0 at 2773 MHz, PeakMiner ~196 at ~2765 MHz.
- These are each miner's own reported speeds over short runs, not pool-credited hashrate. BzMiner and WildRig were not tested (Windows Defender blocked both downloads on our test PC).

Compare miners over **at least an hour**, using your pool's credited hashrate. The first few minutes swing a lot with luck.

## Long runs

**3-card rig** (2× RTX 5060 Ti + RTX 5060) on **RulMiner 3.0.0**, one continuous run:

| | |
|---|---|
| Duration | 22.4 hours |
| Average speed | 282 TH/s (pool 3-hour average 289 TH/s) |
| Shares | 2,576 accepted / 5 rejected (**99.8% of sent shares accepted**); 7 more were stale (found for a job that had already changed, dropped before sending) |
| Power (sum of the 3 cards' board power) | ~423 W |
| Luck | 101% |

The same rig on 3.1 (lock 3100 MHz, +400 MHz) runs about 318-320 TH/s at ~437 W. Long 3.1 runs will be added here.

## How we tune (and how to start)

1. Start at **stock**, then add core offset in +25 MHz steps until speed stops rising or errors appear.
2. **Lock the core clock** a little under the card's boost clock. With the offset this runs the same speed at lower voltage (an undervolt).
3. **Lower the power limit** to 85-90% and check that speed holds.
4. Keep the card **under ~72 °C** for long runs. Raise fans before raising power.

Or just click **Find my best settings** in RulMiner's tuner: it tests a few combinations on each card and shows the fastest and the most efficient.

## Method

- Kernel comparisons and power tests: RulMiner's built-in 60-second benchmark, clocks and power sampled with nvidia-smi from second 20 on; the official-verifier self-test passed at every tuned point.
- Miner comparison and summary speeds: real pool mining, miner-reported hashrate; power is the card's reported board power (nvidia-smi / NVML), not wall power.
- Pool-credited hashrate swings with luck over short windows; at the end of the 22.4-hour rig run Kryptex's 3-hour average was 289 TH/s, against 282 TH/s reported by the miner over the whole run.
