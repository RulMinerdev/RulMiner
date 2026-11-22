# RulMiner benchmarks

Real numbers from our own cards, mining Pearl on the Kryptex pool (November 2026, RulMiner 3.0.0, Windows 11, NVIDIA 621.x drivers). Your results depend on the card model, cooling, room temperature, driver and settings.

## Summary (miner-reported speed)

| Card | Speed (TH/s) | Power | Efficiency | Temp | Settings |
|---|---|---|---|---|---|
| RTX 5070 Ti | **189 – 194** | 270 W | ~700 GH/W | 68 – 72 °C | +175 MHz, lock 2900 MHz, 90% power |
| RTX 5060 Ti | **98 – 100** | 150 W | ~660 GH/W | 62 – 68 °C | +215 MHz, lock 3000 MHz, 83% power |
| RTX 5060 | **80 – 87** | 145 W | ~580 GH/W | 60 – 68 °C | +230 MHz, lock 2940 MHz, stock power |

## Power limit test (RTX 5070 Ti)

Same card, same clocks, only the power limit changed:

| Power limit | Speed | Temp |
|---|---|---|
| 300 W (stock) | 189.9 TH/s | 75 °C |
| **270 W (90%)** | **189.6 TH/s** | **68 °C** |

At stock power the card turns the extra 30 W into heat. 90% keeps essentially all the speed, 7 °C cooler. That's the default "Balanced" setting for this card in the tuner.

## Long runs

**3-card rig** (2× RTX 5060 Ti + RTX 5060), one continuous run:

| | |
|---|---|
| Duration | 22.4 hours |
| Average speed | 282 TH/s (pool 3-hour average 289 TH/s) |
| Shares | 2,576 accepted / 5 rejected / 7 stale (**99.5% accepted**) |
| Wall power (GPUs) | ~423 W |
| Luck | 101% |

**RTX 5070 Ti**, multi-hour runs: 190 – 194 TH/s average, about 1 rejected share per 220 accepted.

## Versus other miners

On the same cards and settings, in 4.5-hour back-to-back runs, the work Kryptex actually credited to RulMiner was **equal to or slightly ahead of** the leading Pearl miners, with a **1% fee** instead of 2–3%. Published RTX 5060 Ti numbers for other miners are 89 – 95 TH/s at 180 W; RulMiner does ~99 TH/s at 150 W on our cards.

Compare miners over **at least an hour**, using your pool's credited hashrate. The first few minutes swing a lot with luck: a run can look like 300+ TH/s or 120 TH/s early and settle to the same average.

## How we tune (and how to start)

1. Start at **stock**, then add core offset in +25 MHz steps until speed stops rising or errors appear.
2. **Lock the core clock** a little under the card's boost clock. With the offset this runs the same speed at lower voltage (an undervolt).
3. **Lower the power limit** to 85–90% and check that speed holds.
4. Keep the card **under ~72 °C** for long runs. Raise fans before raising power.

Or just click **Find my best settings** in RulMiner's tuner: it tests a few combinations on each card and shows the fastest and the most efficient.

## Method

- Speeds in the tables are RulMiner's own reported averages (1-hour or 5-minute). Pool-credited hashrate swings with luck over short windows; over the 22.4-hour rig run Kryptex credited 289 TH/s vs 282 TH/s reported.
- Power is the card's reported board power (nvidia-smi / NVML), not wall power.
- Each setting ran for at least 3 minutes after warm-up; long runs as stated.
