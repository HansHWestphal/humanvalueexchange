# Hermes CFO — June 1, 2026 Go-Live Execution Plan (COO Submission)
**v1.1**
**Date:** May 10, 2026
**Prepared by:** COO (GitHub Copilot CLI)
**Approved by:** Hans Westphal (CEO)
**Target:** Hermes CFO live on Kraken — June 1, 2026
**Window:** 22 days (May 10 → June 1)

**Status:** ✅ COO FINAL — Submitted to Mika (CGO) for consolidation with CTO go-live plan

**Workflow:**
1. ✅ COO plan — this document (operational phases, stage gates, risk, checklist)
2. ⏳ CTO plan — to be provided by CTO (infrastructure build, Hermes prompts)
3. ⏳ Mika (CGO) — consolidates COO + CTO plans into unified Hermes master plan
4. ⏳ COO sign-off — reviews and approves consolidated plan before CTO writes Hermes prompts
5. ⏳ CTO — writes activation prompts for Hermes to action the final plan

---

## Situation

- Kraken account validation: ✅ Complete (or imminent)
- Account funding: Hans to fund $1,000 USD within 2 weeks (hard deadline: May 28 preferred, June 1 absolute)
- DGX Spark: Online — CTO build in progress
- Hermes: Not yet activated — awaiting infrastructure completion
- Stage 0/1 testing: Not yet started

**This plan gets Hermes from zero to live trading in 22 days.**

---

## Critical Path Summary

```
May 10–14  │ CTO: Build & verify full infrastructure stack
May 15     │ Hermes: Activation + full onboarding
May 15–18  │ Hermes: Simulator build + historical data acquisition
May 18–22  │ Hermes: Stage 0 backtesting (1-min + 5-min) + Monte Carlo
May 22–28  │ Hermes: Stage 1 — 60-day accelerated paper trading simulation
May 28     │ Stage 1 gate evaluation + Hans funds Kraken account
May 28–31  │ Hermes: Live trading environment configured + final checks
June 1     │ 🚀 Stage 2 — LIVE TRADING BEGINS
```

---

## Phase 1: CTO Infrastructure Build
**Window:** May 10–14 | **Owner:** CTO | **COO role:** Track daily, escalate delays

The Master Spec Section 16 checklist must be fully cleared before Hermes can activate. Every item is a hard dependency.

| # | Item | Owner | Status |
|---|------|-------|--------|
| 1 | DGX OS Ubuntu 24.04 ARM64 — secured and updated | CTO | ⏳ Pending |
| 2 | Ollama installed — all 4 models downloaded and verified | CTO | ⏳ Pending |
| 3 | Freqtrade installed natively — Kraken API keys loaded | CTO | ⏳ Pending |
| 4 | Hermes agent framework (Base + Atlas extensions) installed | CTO | ⏳ Pending |
| 5 | Telegram bot created and connected to Hans | CTO | ⏳ Pending |
| 6 | Open WebUI accessible for Hans + COO observability | CTO | ⏳ Pending |

**COO action:** Daily check-in with CTO. Any item not confirmed by May 14 triggers immediate escalation to Hans. No phase slippage is acceptable — every day of delay compresses the testing window.

**4 models that must be verified responsive before Hermes activates:**
- Qwen 2.5 14B (Orchestrator)
- Mistral Small 24B (Research/Synthesis)
- Nemotron-3 Nano 30B A3B (Execution/Tooling)
- Gemma 2 27B (Critic/Risk)

---

## Phase 2: Hermes Activation & Onboarding
**Window:** May 15 | **Owner:** Hermes + COO | **Duration:** 1 day

On activation, Hermes reads the full onboarding package in this order:

1. `agent-communications/2026-05-09-hermes-cfo-trading-spec-v2.0-MASTER.md` — operating constitution
2. `agent-communications/2026-05-10-coo-hermes-cfo-welcome.md` — COO welcome
3. `agent-communications/2026-05-10-mika-hermes-cfo-welcome.md` — CGO welcome
4. `agent-communications/2026-05-10-cto-hermes-cfo-welcome.md` — CTO welcome
5. `agent-communications/2026-05-10-mika-trading-research-brief-v1.1.md` — research brief

**Hermes confirms onboarding complete via Telegram to Hans.**

**COO confirms:** Open WebUI shows all 4 models healthy. Hermes agent orchestration layer is responding. Telegram bot is delivering messages to Hans.

---

## Phase 3: Simulator Build & Historical Data
**Window:** May 15–18 | **Owner:** Hermes (Nemotron-3 Nano + Mistral Small 24B) | **Duration:** 3 days

Kraken has no testnet. The paper trading simulator is the only safe environment for all pre-live testing. It must be built before any strategy is evaluated.

### 3.1 Historical Data Acquisition (Mistral Small 24B)
- Source minimum 6–8 weeks of recent BTC/USDT OHLCV data from Kraken API
- Store in `knowledge-repo/historical-data/`
- Data quality verified: no gaps, correct timestamps, accurate OHLCV values
- Mistral Small 24B ingests, tags, and summarizes dataset

### 3.2 Simulator Build (Nemotron-3 Nano)
The simulator must replicate:

| Component | Requirement |
|-----------|------------|
| Fee structure | Exact Kraken maker/taker fees — no approximation |
| Slippage | Realistic order book depth and fill dynamics |
| Execution latency | Simulated latency matching Kraken API response times |
| BTC settlement | Daily conversion at 23:59 UTC — exact mechanics |
| Circuit breakers | All 5 triggers — active and enforced |
| Veto protocol | Gemma 2 27B veto on every simulated signal |
| Audit logging | Immutable append-only trade and veto logs |

### 3.3 Simulator Verification (Qwen 2.5 14B + Gemma 2 27B)
- Qwen runs validation test cases: fee calculations, circuit breaker triggers, BTC settlement
- Gemma independently audits: does the simulator accurately represent live trading risk?
- **Gemma must approve the simulator before any backtesting begins — no exceptions**
- COO notified on simulator sign-off

---

## Phase 4: Stage 0 Backtesting
**Window:** May 18–22 | **Owner:** Hermes | **Duration:** 4 days

Two parallel backtests run against the verified historical dataset.

### Pass Criteria (both strategies must meet these to advance)

| Metric | Threshold |
|--------|-----------|
| Sharpe ratio | ≥ 1.5 |
| Maximum drawdown | ≤ 15% |
| Win rate | ≥ 52% |
| Longest losing streak | ≤ 7 consecutive trades |
| Monte Carlo stress test | Must pass |

### Strategy A: 1-Minute Opening Range Scalping (Jdub Trades baseline)
- Entry: 1-minute opening range breakout during high-volume BTC sessions
- Sentiment overlay: Mistral Small 24B filter
- Risk: 1% account equity per trade (hardcoded)

### Strategy B: 5-Minute Opening Range Scalping (evaluation candidate)
- Entry: 5-minute opening range breakout during high-volume BTC sessions
- Same sentiment overlay and risk rules
- Results compared directly against Strategy A

### Stage 0 Gate Evaluation
- **Owner:** Qwen 2.5 14B (evaluation) + Gemma 2 27B (confirmation)
- Both strategies scored and compared
- Best-performing timeframe (or both if both pass) advances to Stage 1
- **Gate result reported to Hans via Telegram immediately**
- **COO logged the result in the repo**

> **If Stage 0 fails:** Qwen initiates root cause analysis. Strategy is adjusted. Re-backtest required before Stage 1 can begin. COO escalates timeline risk to Hans.

---

## Phase 5: Stage 1 — 60-Day Accelerated Paper Trading
**Window:** May 22–28 | **Owner:** Hermes | **Duration:** 6 days wall-clock (60 simulated trading days)

This is the final gate before live capital is deployed. It runs inside the paper trading simulator at accelerated speed — 60 simulated trading days completed within the available window.

### Operating Rules During Stage 1
- All 5 circuit breakers active — any trigger is logged and reported
- Gemma 2 27B veto protocol live on every signal
- Daily BTC settlement at 23:59 UTC (simulated)
- 1% risk per trade — hardcoded
- Maximum 1 trade per simulated UTC day
- Full audit logging: every trade, every veto, every circuit breaker event

### Stage 1 Pass Criteria

| Criterion | Requirement |
|-----------|------------|
| Sharpe ratio | ≥ 1.5 (maintained over full 60 days) |
| Maximum drawdown | ≤ 15% |
| Win rate | ≥ 52% |
| Circuit breaker events (final 30 sim days) | Zero — clean run required |
| Gemma 2 27B readiness confirmation | Required |

### Stage 1 Gate Evaluation
- **Owner:** Qwen 2.5 14B (evaluation) + Gemma 2 27B (confirmation)
- Full 60-day simulation P&L and metrics reviewed
- **Gate result reported to Hans via Telegram immediately**
- **COO logs result and updates Hans**

> **If Stage 1 fails:** Do not proceed to live trading. Identify root cause. Fix. Return to Stage 0 if strategy change required, or re-run Stage 1 if execution issue. COO escalates June 1 deadline risk to Hans immediately — timeline review required.

---

## Phase 6: Kraken Funding & Live Configuration
**Window:** May 28–31 | **Owner:** Hans (funding) + Hermes (config) + COO (coordination)

### Hans Action Required: Fund Kraken Account
- **Target date:** May 28, 2026
- **Hard deadline:** May 31, 2026 (June 1 go-live requires confirmed funds)
- **Amount:** $1,000 USD
- **COO role:** Confirm with Hans when funds are live on Kraken. Notify Hermes.

### Hermes: Live Trading Environment Configuration (Nemotron-3 Nano)
- Switch Freqtrade from simulator to live Kraken API connection
- Verify API key permissions: trade execution, balance read, order management
- Confirm BTC/USDT pair active on Kraken
- Verify all 5 circuit breakers wired to live account equity
- Verify Telegram alerts firing correctly on test events
- Confirm daily BTC settlement mechanics on live account
- **Qwen 2.5 14B + Gemma 2 27B must both approve live configuration before first trade**

### Final Pre-Launch Checklist (COO owns this)
- [ ] Stage 1 gate: PASSED
- [ ] Kraken account: FUNDED ($1,000 USD confirmed)
- [ ] Freqtrade: LIVE API connected and verified
- [ ] All 4 Ollama models: HEALTHY and responding
- [ ] Telegram bot: LIVE — test alert received by Hans
- [ ] Circuit breakers: VERIFIED on live account
- [ ] Audit logging: ACTIVE — append-only, confirmed
- [ ] Qwen + Gemma: APPROVED live configuration

**All 8 items must be checked before first live trade. No exceptions.**

---

## June 1, 2026 — Go-Live 🚀

**Stage 2 live trading begins.**

- First trade eligible: June 1, 2026 (any high-volume BTC session)
- All governance rules active from Day 1 — no grace period
- Daily P&L report: 08:00 UTC via Telegram to Hans
- COO monitors first-week reporting for discipline and circuit breaker compliance

**The machine runs. The SATS stack. The treasury begins.**

---

## Risk Register

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|-----------|
| CTO infrastructure delayed past May 14 | Medium | High — compresses all phases | COO escalates immediately; daily check-ins |
| Stage 0 backtest fails | Low-Medium | Medium — delays Stage 1 | Root cause + re-backtest; COO flags timeline |
| Stage 1 circuit breaker events in final 30 days | Low | High — must re-run Stage 1 | Build and verify simulator thoroughly in Phase 3 |
| Kraken funding delayed past May 31 | Low | Critical — June 1 go-live impossible | Hans funds by May 28 target; COO tracks |
| Model unavailable on activation | Low | High — delays onboarding | CTO verifies all 4 models before COO sign-off |

---

## Communication Cadence (COO-Owned)

| Check-in | Frequency | Parties | Channel |
|----------|-----------|---------|---------|
| CTO infrastructure progress | Daily (May 10–14) | COO → CTO | Repo + direct |
| Stage gate results | On completion | Hermes → Hans + COO | Telegram + repo log |
| Kraken funding confirmation | One-time | Hans → COO → Hermes | Direct |
| Live config approval | Pre-launch | Hermes → Hans | Telegram |
| First week daily P&L | Daily 08:00 UTC | Hermes → Hans | Telegram |

---

## Document References

| Document | Purpose |
|----------|---------|
| `agent-communications/2026-05-09-hermes-cfo-trading-spec-v2.0-MASTER.md` | Operating constitution — governs all decisions |
| `agent-communications/2026-05-10-mika-trading-research-brief-v1.1.md` | Research brief — strategy seeds and circuit breakers |
| `agent-communications/2026-05-10-coo-hermes-cfo-welcome.md` | COO welcome — operational interface |
| `agent-communications/2026-05-10-mika-hermes-cfo-welcome.md` | CGO welcome — brand and growth alignment |
| `agent-communications/2026-05-10-cto-hermes-cfo-welcome.md` | CTO welcome — infrastructure philosophy |

---

*v1.0 — COO (GitHub Copilot CLI) — May 10, 2026 — initial draft*
*v1.1 — COO — May 10, 2026 — submitted to Mika (CGO) for consolidation with CTO plan*
*CEO approved: Hans Westphal — May 10, 2026*
*COO sign-off on consolidated plan: pending Mika consolidation*
