# RulMiner

**Pearl (PRL) GPU miner for NVIDIA RTX 50-series (Blackwell) cards. 0.5% dev fee. Built-in card tuning.**

![Windows](https://img.shields.io/badge/Windows-10%2F11-blue) ![NVIDIA](https://img.shields.io/badge/NVIDIA-RTX%2050--series-76b900) ![Fee](https://img.shields.io/badge/dev%20fee-0.5%25-red)

## Download

Get the latest `RulMiner-x.y.z-windows.zip` from the **[Releases](../../releases)** page. **Only download from this page.** Modified "no fee" copies often contain malware, and official builds refuse to run if they have been changed.

## Quick start

1. Install a current NVIDIA driver.
2. Unzip anywhere and run **RulMiner.exe**. Click **Yes** when Windows asks for permission (only needed for card tuning).
3. Paste your **Pearl wallet** (or Kryptex account) and a worker name, pick a mode, done.

Modes: **Kryptex PPS+ (Pearl or Bitcoin payout)**, **HeroMiners / LuckyPool**, or **Solo** (you get the whole block, but only when your cards find one).

## Why RulMiner

- **0.5% fee**, lower than SRBMiner-Multi, BzMiner, PeakMiner and Kobold (2%) and OneZeroMiner (1%); some Pearl miners charge 0%. You mine 49 minutes 45 seconds, then 15 seconds for the developer on the same pool. A badge shows during those 15 seconds. You keep 100% of any block you find on your own time.
- **Card tuning built in.** Per-card clock offset, clock lock, power limit and fans, with safe limits. Every card goes back to stock when you close RulMiner. No Afterburner needed.
- **Find my best settings.** Tests a few settings on each card (about 70 s each: a speed run, then a check that every result is still correct at that setting) and shows the fastest and the most efficient.
- **One window dashboard.** Speed, accepted shares, temps, power, efficiency, luck, earnings estimate.
- **Safety first.** Stops a card at its temperature limit (80 °C default).

## New in 3.2

- **Dev fee cut in half to 0.5%**, taken as 15 seconds every 50 minutes.
- **Pause while gaming** (one-card PCs, off by default): mining pauses when a game uses your card, and comes back 60 s after it closes.
- **Back to stock**: one button puts every card on stock clocks and keeps mining.
- **Ready for Pearl's FP8 fork**: when FP8 jobs arrive, RulMiner stops cleanly and puts your cards back to stock instead of reconnecting forever.

## New in 3.1

A new hand-written kernel for RTX 50-series cards: **+4.6% to +5.4% on our RTX 5070 Ti** (about +4% on our 5060 Ti / 5060 rig) at the same clock and power as 3.0 (based on llmjob's open-source sm_120 fold, MIT license). Every result is still checked against Pearl's official verifier before a share is sent. Nothing to set up: it's on by default.

**What's next:** ⚡ more hashes per watt (closing the power gap to the most efficient miner) and 🧪 the FP8 version for Pearl's PIP-3 fork, which has already mined blocks accepted on Pearl's FP8 testnet.

## Measured speeds (miner-reported, our own cards, RulMiner 3.1)

| Card | Speed | Power | Settings |
|---|---|---|---|
| RTX 5070 Ti | ~197 TH/s | 270 W | stock clocks, 270 W limit |
| RTX 5070 Ti | ~212.5 TH/s | ~245 W | lock 3000, +499 MHz, memory 810 |
| RTX 5060 Ti | ~110 TH/s | ~147 W | lock 3100, +400 MHz |
| RTX 5060 | ~94.5 TH/s | 145 W | lock 3100, +400 MHz |

The tuned rows are our own cards; offsets this high aren't safe on every chip. Start lower, or let **Find my best settings** test yours.

**Versus other miners** (RTX 5070 Ti, same clocks, back-to-back runs): RulMiner 212.5 TH/s, SRBMiner 3.8.9 213.6 TH/s, PeakMiner 2.2.08rc3 211.7 TH/s. Those runs were with RulMiner 3.1's 1% fee against SRBMiner's 2% (about even after fees); with 3.2's 0.5% fee RulMiner comes out ahead, and RulMiner is level with PeakMiner. SRBMiner draws about 14 W less (6.4% more TH/s per watt). One card, short back-to-back runs; details in BENCHMARKS.md.

Full results, power tests and long runs: **[BENCHMARKS.md](BENCHMARKS.md)**. Your numbers depend on card, cooling, driver and settings. Compare miners with your pool's credited hashrate over an hour or more, not the first few minutes (early share counts are mostly luck).

## FAQ

**Windows says "Windows protected your PC".** RulMiner isn't signed with a paid certificate yet. Click **More info → Run anyway**. Official builds check their own signature and refuse to run if modified.

**My antivirus flags it.** Every GPU miner gets flagged at some point because malware sometimes hides miners. Download only from this page; if you trust it, add an exclusion for the RulMiner folder.

**Where are my settings?** `%LOCALAPPDATA%\RulMiner` on your PC.

**What does RulMiner connect to?**
- **The pool you pick**, to mine. LuckyPool's connection is unencrypted (its encrypted port uses a certificate Windows doesn't trust, and RulMiner never turns certificate checks off); the others use TLS.
- **That same pool's stats page** (Kryptex, HeroMiners or LuckyPool), for the dashboard's "pool credited" numbers. It sends your wallet or account address, which that pool already has from your login. Turn it off with `RULMINER_NO_POOL_STATS=1`.
- **The Pearl price** from Coinbase (CoinGecko as backup), every 2 minutes, for the earnings estimate. Nothing about you is sent. Turn it off with `RULMINER_NO_PRICE=1`.

Nothing else: no telemetry, no update checks, no web fonts.

**Does the fee connect to anything of mine?** No. During the 15-second fee window your miner sends work to the same pool, credited to the developer's wallet address. Nothing else.

**AMD / older NVIDIA?** No. RulMiner targets RTX 50-series (Blackwell) only. On a PC with other cards too, RulMiner logs the cards it can't use and keeps mining on the rest.

**Can I leave a card out?** Yes: add `set "RULMINER_EXCLUDE_GPUS=1"` (comma-separated card numbers, e.g. `1,3`) near the top of `start-rulminer.bat`. If one card stops (too hot, a wrong result, or it can't start), the other cards keep mining.

**Which NVIDIA driver?** A current one (we test on 621.x). The 3.1 kernel is built with a recent CUDA toolkit; on a driver too old to load it, the card keeps mining with a built-in fallback kernel that's about 3% slower than 3.0. RulMiner's log (%LOCALAPPDATA%\RulMiner\logs) shows "rotation_fold_refused" when that happens. Updating the driver fixes it.

**Pearl FP8 fork (PIP-3)?** Pearl plans a mining change (FP8). When it activates, every miner needs an update. From 3.2, RulMiner notices FP8 jobs, stops cleanly and puts your cards back to stock. The FP8 version of RulMiner will ship here once the fork date is set.

## License

RulMiner is free to use under the terms in `LICENSE.txt` (no modified or redistributed builds). Third-party notices: `THIRD-PARTY-LICENSES.txt`.
