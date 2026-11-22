# RulMiner

**Pearl (PRL) GPU miner for NVIDIA RTX 50-series (Blackwell) cards. 1% dev fee. Built-in card tuning.**

![Windows](https://img.shields.io/badge/Windows-10%2F11-blue) ![NVIDIA](https://img.shields.io/badge/NVIDIA-RTX%2050--series-76b900) ![Fee](https://img.shields.io/badge/dev%20fee-1%25-red)

## Download

Get the latest `RulMiner-x.y.z-windows.zip` from the **[Releases](../../releases)** page. **Only download from this page.** Modified "no fee" copies often contain malware, and official builds refuse to run if they have been changed.

## Quick start

1. Install a current NVIDIA driver.
2. Unzip anywhere and run **RulMiner.exe**. Click **Yes** when Windows asks for permission (only needed for card tuning).
3. Paste your **Pearl wallet** (or Kryptex account) and a worker name, pick a mode, done.

Modes: **Kryptex PPS+ (Pearl or Bitcoin payout)**, **HeroMiners / LuckyPool**, or **Solo** (you get the whole block, but only when your cards find one).

## Why RulMiner

- **1% fee**, lower than most Pearl miners. You mine 99 minutes, then 1 minute for the developer on the same pool. A badge shows during that minute. You keep 100% of any block you find on your own time.
- **Card tuning built in.** Per-card clock offset, clock lock, power limit and fans, with safe limits. Every card goes back to stock when you close RulMiner. No Afterburner needed.
- **Find my best settings.** Tests a few settings on each card (about 45 s each) and shows the fastest and the most efficient.
- **One window dashboard.** Speed, accepted shares, temps, power, efficiency, luck, earnings estimate.
- **Safety first.** Stops a card at its temperature limit (80 °C default).

## Measured speeds (miner-reported, our own cards)

| Card | Speed | Power | Settings |
|---|---|---|---|
| RTX 5070 Ti | ~189-194 TH/s | 270 W | +175 MHz, lock 2900, 90% power |
| RTX 5060 Ti | ~99 TH/s | 150 W | +215 MHz, lock 3000 |
| RTX 5060 | ~84 TH/s | 145 W | +230 MHz, lock 2940 |

Pool check: over a 22-hour run on the 3-card rig, Kryptex credited **289 TH/s** against **282 TH/s** reported by the miner. Short runs swing more with luck.

Full results, power tests and long runs: **[BENCHMARKS.md](BENCHMARKS.md)**. Your numbers depend on card, cooling, driver and settings. Use the miner's 1-hour average or your pool's numbers to compare miners, not the first few minutes (early share counts are mostly luck).

## FAQ

**Windows says "Windows protected your PC".** RulMiner isn't signed with a paid certificate yet. Click **More info → Run anyway**. Official builds check their own signature and refuse to run if modified.

**My antivirus flags it.** Every GPU miner gets flagged at some point because malware sometimes hides miners. Download only from this page; if you trust it, add an exclusion for the RulMiner folder.

**Where are my settings?** `%LOCALAPPDATA%\RulMiner` on your PC. RulMiner only talks to the pool you pick.

**Does the fee connect to anything of mine?** No. During the fee minute your miner sends work to the same pool, credited to the developer's wallet address. Nothing else.

**AMD / older NVIDIA?** No. RulMiner targets RTX 50-series (Blackwell) only.

**Pearl FP8 fork (PIP-3)?** Pearl plans a mining change (FP8). When it activates, every miner needs an update. An FP8 version of RulMiner is in testing and will ship here.

## License

RulMiner is free to use under the terms in `LICENSE.txt` (no modified or redistributed builds). Third-party notices: `THIRD-PARTY-LICENSES.txt`.
