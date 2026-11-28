# RulMiner

**Pearl (PRL) GPU miner for NVIDIA RTX 50-series (Blackwell) cards. Windows and HiveOS/Linux. 0.5% dev fee. Built-in card tuning.**

![Windows](https://img.shields.io/badge/Windows-10%2F11-blue) ![HiveOS](https://img.shields.io/badge/HiveOS%20%2F%20Linux-Ubuntu%2022.04%2B-orange) ![NVIDIA](https://img.shields.io/badge/NVIDIA-RTX%2050--series-76b900) ![Fee](https://img.shields.io/badge/dev%20fee-0.5%25-red)

## Download

Get the latest `RulMiner-x.y.z-windows.zip` (Windows) or `rulminer-x.y.z.tar.gz` (HiveOS / Linux) from the **[Releases](../../releases)** page. **Only download from this page.** Modified "no fee" copies often contain malware. Official builds check their own signature at start.

## Quick start

1. Install a current NVIDIA driver.
2. Unzip anywhere and run **RulMiner.exe**. Click **Yes** when Windows asks for permission (only needed for card tuning).
3. Paste your **Pearl wallet** (or Kryptex account) and a worker name, pick a mode, done.

Modes: **Kryptex PPS+ (Pearl or Bitcoin payout)**, **HeroMiners / LuckyPool**, **Solo** (you get the whole block, but only when your cards find one), or **Quantus** (second coin on Kryptex, paid in Bitcoin).

**HiveOS:** flight sheet with Miner = Custom, installation URL = the `rulminer-x.y.z.tar.gz` link from Releases, hash algorithm `pearlhash`, your wallet and pool as usual. Needs NVIDIA driver 570+ with the open kernel modules (`nvidia-driver-update`). Full steps in the README inside the archive. Built and tested on HiveOS; mmpOS and plain Ubuntu 22.04+ should work (untested, reports welcome).

## Why RulMiner

- **0.5% fee**, lower than SRBMiner-Multi, BzMiner, PeakMiner and Kobold (2%) and OneZeroMiner (1%); some Pearl miners charge 0%. You mine 49 minutes 45 seconds, then 15 seconds for the developer on the same pool. A badge shows during those 15 seconds. You keep 100% of any block you find on your own time.
- **Card tuning built in** (Windows). Per-card clock offset, clock lock, memory clock, power limit and fans, with safe limits. Every card goes back to stock when you close RulMiner. No Afterburner needed.
- **Freeze protection.** If a too-high offset freezes a card, RulMiner notices within seconds and restarts. On Windows it comes back at stock clocks and keeps mining on its own; on HiveOS the restart uses your OC profile.
- **Find my best settings.** Tests a few settings on each card (about 70 s each: a speed run, then a check that every result is still correct at that setting) and shows the fastest and the most efficient.
- **One window dashboard.** Speed, accepted shares, temps, power, efficiency, luck, earnings estimate.
- **Safety first.** Stops a card at its temperature limit (80 °C default).

## New in 3.3

- **Freeze protection**: a frozen card (100% busy, no work finished, no error) is caught within seconds and RulMiner restarts. On Windows it comes back at stock clocks, resumes your mode, and keeps that card's saved tune off until you save a lower one; on HiveOS the restart uses your OC profile. 3 freezes in 5 minutes and it stops and tells you. Frozen cards show "Stalled" and 0 TH/s, never an old number. (Tested with forced freezes; a real driver-level freeze wasn't reproduced.)
- **Tune cards fixed**: memory clock set first and only while not mining (it could reset the driver on some cards), offsets checked after writing, a blank power field leaves your limit alone.
- **HiveOS / Linux build**: HiveOS custom miner, same speed as Windows on our 4-card rig (~431 TH/s).
- **Quantus (QTC)** as a second coin on Kryptex, same 0.5% fee.
- Easier-to-read amber dashboard numbers.

## New in 3.2

- **Dev fee cut in half to 0.5%**, taken as 15 seconds every 50 minutes.
- **Pause while gaming** (one-card PCs, off by default): mining pauses when a game uses your card, and comes back 60 s after it closes.
- **Back to stock**: one button puts every card on stock clocks and keeps mining.
- **Ready for Pearl's FP8 fork**: when FP8 jobs arrive, RulMiner stops cleanly and puts your cards back to stock instead of reconnecting forever.

## New in 3.1

A new hand-written kernel for RTX 50-series cards: **+4.6% to +5.4% on our RTX 5070 Ti** (about +4% on our 5060 Ti / 5060 rig) at the same clock and power as 3.0 (based on llmjob's open-source sm_120 fold, MIT license). Every result is still checked against Pearl's official verifier before a share is sent. Nothing to set up: it's on by default.

**What's next:** ⚡ more hashes per watt (closing the power gap to the most efficient miner) and 🧪 the FP8 version for Pearl's PIP-3 fork, which has already mined blocks accepted on Pearl's FP8 testnet2 (blocks 150,516 and 150,521).

## Measured speeds (miner-reported, our own cards, RulMiner 3.1)

| Card | Speed | Power | Settings |
|---|---|---|---|
| RTX 5070 Ti | ~197 TH/s | 270 W | stock clocks, 270 W limit |
| RTX 5070 Ti | ~212.5 TH/s | ~245 W | lock 3000, +499 MHz, memory 810 |
| RTX 5060 Ti | ~110 TH/s | ~147 W | lock 3100, +400 MHz |
| RTX 5060 | ~94.5 TH/s | 145 W | lock 3100, +400 MHz |

The tuned rows are our own cards; offsets this high aren't safe on every chip. Start lower, or let **Find my best settings** test yours.

**Versus other miners** (RTX 5070 Ti, same clocks, back-to-back runs): RulMiner 212.5 TH/s, SRBMiner 3.8.9 213.6 TH/s, PeakMiner 2.2.08rc3 211.7 TH/s. Those runs were with RulMiner 3.1. After fees (RulMiner now 0.5%, SRBMiner and PeakMiner 2%) that works out to about 1% more net hashrate than SRBMiner and about 2% more than PeakMiner on that card; this is fee math on the same runs, not a new measurement. SRBMiner draws about 14 W less (6.4% more TH/s per watt). One card, short back-to-back runs; details in BENCHMARKS.md.

Full results, power tests and long runs: **[BENCHMARKS.md](BENCHMARKS.md)**. Your numbers depend on card, cooling, driver and settings. Compare miners with your pool's credited hashrate over an hour or more, not the first few minutes (early share counts are mostly luck).

## FAQ

**Windows says "Windows protected your PC".** RulMiner isn't signed with a paid certificate yet. Click **More info → Run anyway**. Official builds check their own signature at start; only download from this page.

**My antivirus flags it.** Every GPU miner gets flagged at some point because malware sometimes hides miners. Download only from this page; if you trust it, add an exclusion for the RulMiner folder.

**Where are my settings?** `%LOCALAPPDATA%\RulMiner` on Windows, `~/.local/state/RulMiner` on Linux (never inside the HiveOS miner folder, which HiveOS wipes on reinstall).

**What does RulMiner connect to?**
- **The pool you pick**, to mine (for Quantus: Kryptex's Quantus pool). LuckyPool's connection is unencrypted (its encrypted port uses a certificate Windows doesn't trust, and RulMiner never turns certificate checks off); the others use TLS.
- **That same pool's stats page** (Kryptex, HeroMiners or LuckyPool), for the dashboard's "pool credited" numbers. It sends your wallet or account address, which that pool already has from your login. Turn it off with `RULMINER_NO_POOL_STATS=1`.
- **The Pearl price** from Coinbase (CoinGecko as backup), every 2 minutes, for the earnings estimate. Nothing about you is sent. Turn it off with `RULMINER_NO_PRICE=1`.

Nothing else: no telemetry, no update checks, no web fonts.

**Does the fee connect to anything of mine?** No. During the 15-second fee window your miner sends work to the same pool, credited to the developer's wallet address. Nothing else.

**Does RulMiner tune my cards on HiveOS?** No. On Linux RulMiner never changes clocks, power or fans: HiveOS applies your OC profile and would overwrite it. The README in the archive lists the settings we run on our own rig as a starting point. Freeze protection still works there: HiveOS restarts the miner (on the same OC profile, so lower the offset), and after 3 freezes in 5 minutes RulMiner stays stopped until you restart it.

**AMD / older NVIDIA?** No. RulMiner targets RTX 50-series (Blackwell) only. On a PC with other cards too, RulMiner logs the cards it can't use and keeps mining on the rest.

**Can I leave a card out?** Yes: add `set "RULMINER_EXCLUDE_GPUS=1"` (comma-separated card numbers, e.g. `1,3`) near the top of `start-rulminer.bat`. If one card stops (too hot, a wrong result, or it can't start), the other cards keep mining.

**Which NVIDIA driver?** Windows: a current one (we test on 621.x). Linux/HiveOS: 570 or newer with the open kernel modules. The 3.1 kernel is built with a recent CUDA toolkit; on a driver too old to load it, the card keeps mining with a built-in fallback kernel that's about 3% slower than 3.0. RulMiner's log (%LOCALAPPDATA%\RulMiner\logs) shows "rotation_fold_refused" when that happens. Updating the driver fixes it.

**Pearl FP8 fork (PIP-3)?** Pearl plans a mining change (FP8). When it activates, every miner needs an update. From 3.2, RulMiner notices FP8 jobs, stops cleanly and puts your cards back to stock. The FP8 version of RulMiner will ship here once the fork date is set.

## License

RulMiner is free to use under the terms in `LICENSE.txt` (no modified or redistributed builds). Third-party notices: `THIRD-PARTY-LICENSES.txt`.
