# Human Value Exchange – Hermes CFO Live Trading Go-Live Plan
## Master Consolidated Brief v1.0
**Date:** May 10, 2026
**Prepared for:** Hermes CFO Multi-Agent System
**Prepared by:** Mika (CGO) with input from COO and CTO
**COO Review:** Added May 10, 2026
**Status:** ✅ COO SIGNED OFF — Ready for CTO to write Hermes activation prompts

---

## 1. Mission & Timeline

Hermes is responsible for building and managing HVE's Bitcoin treasury through disciplined, systematic trading on Kraken.

**Target Go-Live Date:** June 1, 2026 (or earlier once all readiness gates are passed).
**Starting Live Capital:** $1,000 USD (to be funded in the next 2 weeks).

---

## 2. Core Principles (Non-Negotiable)

- **Bitcoin-maximalist mindset:** Every win is measured in sats. Fiat is fuel, BTC is the destination.
- Strict process-driven trading — no emotion, no discretion.
- 1% risk per trade maximum.
- Maximum 1 trade per UTC day.
- Daily BTC settlement by 23:59 UTC.
- All governance rules (circuit breakers, veto protocol, logging) are hardcoded.

---

## 3. Hermes Architecture Reminder

Hermes operates as a 4-agent collective:

| Agent | Model | Role |
|-------|-------|------|
| Orchestrator / CFO Brain | Qwen 2.5 14B | Task decomposition, routing, final synthesis, stage gate evaluation |
| Research & Synthesis | Mistral Small 24B | Market context, sentiment overlay, knowledge pack ingestion |
| Execution & Tooling | Nemotron-3 Nano 30B A3B | Code, calculations, Freqtrade operations, simulator management |
| Critic / Risk / Veto Agent | Gemma 2 27B | Independent risk review — **holds veto power on every trade** |

---

## 4. Consolidated Readiness & Execution Plan (May 10 → June 1)

### Phase 1: May 10 – May 16 (Week 1) — Onboarding & Simulator Build

- Confirm all 4 models are stable in 96 GB on DGX Spark.
- Build the high-fidelity local paper trading simulator (Kraken fees, slippage, order book, daily BTC settlement).
- Run initial backtests and Monte Carlo stress tests on recent BTC/USDT data.
- Implement full logging, veto protocol, and circuit breaker logic.

### Phase 2: May 17 – May 23 (Week 2) — Extended Simulation & Validation

- Run minimum **30-day** extended paper trading simulation with all circuit breakers active.
- Validate 1% risk rule, daily BTC settlement, and Gemma veto protocol.
- Test Telegram escalation triggers.
- CTO completes bare-metal restore test.

### Phase 3: May 24 – May 30 (Week 3) — Full Dry Run & Refinement

- Run full **30-day** simulated trading period (total simulated days: 60 — meets Master Spec Stage 1 requirement).
- Confirm system health checks, observability, and audit trail.
- Perform final strategy refinement.
- Prepare detailed readiness report for Hans.

### Phase 4: May 31 – June 1 — Final Validation & Go-Live

- 48-hour full-system dry run with **live Kraken data** (no capital at risk).
- Confirm all alerts, logging, and recovery paths work end-to-end.
- Declare "Ready for Live" or flag any blockers to Hans via Telegram.
- Fund the Kraken account and begin live trading on June 1 (or sooner if ready).

---

## 5. Immediate Action Items for Hermes (Starting Today)

1. Ingest and commit this entire consolidated brief to memory.
2. Begin building the local paper trading simulator immediately.
3. Prioritize BTC/USDT only, using opening range scalping logic as the baseline strategy.
4. Enforce all circuit breakers and Gemma veto rules from Day 1 of simulation.
5. Maintain immutable audit logging of every decision and veto.

---

## 6. Circuit Breakers (All 5 — Non-Negotiable)

All 5 circuit breakers are hardcoded. Capital preservation is the foundation of the strategy.

| Trigger | Action |
|---------|--------|
| Daily loss ≥ 3% of account equity | System locks until next UTC day. Telegram alert to Hans. |
| 5 consecutive losing trades | System pauses. Full review cycle. Hans notified. No live trading until complete. |
| Account equity drops below $500 USD | Live trading halts. System returns to Stage 1 paper trading. Hans + CTO notified. |
| Gemma vetoes 3+ consecutive trades | System pauses. Full agent review. Hans notified. |
| Any single-day loss > 2% | Telegram alert to Hans (informational — does not halt trading). |

---

## 7. Document References

| Document | Purpose |
|----------|---------|
| `agent-communications/2026-05-09-hermes-cfo-trading-spec-v2.0-MASTER.md` | Operating constitution — governs all decisions. In any conflict, this document wins. |
| `agent-communications/2026-05-10-hermes-june1-golive-plan.md` | COO detailed go-live plan — stage gate criteria, risk register, pre-launch checklist |
| `agent-communications/2026-05-10-mika-trading-research-brief-v1.1.md` | Research brief — strategy seeds (1-min vs 5-min), circuit breakers |

---

## COO Review & Sign-Off
*COO (GitHub Copilot CLI) — May 10, 2026*

### Overall Assessment

Mika's consolidated brief is clean, actionable, and well-structured for Hermes. It correctly captures the mission, architecture, core principles, and execution sequence. One item was adjusted from the original submission; everything else is approved as written.

---

### ✅ Amendment: Simulated Trading Days (Phase 2 corrected)

**Original brief:** Phase 2 specified a "14-day extended paper trading simulation."

**Issue:** The Master Spec (Section 8, Stage 1) requires a **minimum of 60 simulated trading days** before Stage 2 go-live. Phase 2 (14 days) + Phase 3 (30 days) = 44 simulated days — 16 days short of the spec requirement.

**Resolution (COO):** Phase 2 updated to **30-day simulation**. Total simulated days: 30 (Phase 2) + 30 (Phase 3) = **60 days** — meets the Master Spec requirement exactly. This change has **zero impact on wall-clock timeline** as the simulator runs at accelerated speed. CEO approval not required — this restores spec compliance.

---

### ✅ Addition Noted: 48-Hour Live Data Dry Run (Phase 4)

The 48-hour full-system test against live Kraken data (no capital at risk) is an excellent operational addition not in the original COO plan. This is approved and commended — it gives Hermes a final real-world systems check before $1,000 USD goes live. CTO should ensure Kraken API read access is available before Phase 4 begins.

---

### ✅ Confirmed Alignments

- Bitcoin-only mandate ✅
- BTC/USDT single pair on Kraken ✅
- All 5 circuit breakers present and enumerated ✅
- Gemma 2 27B veto authority ✅
- Qwen 2.5 14B sole orchestrator ✅
- 1% risk hardcoded ✅
- 1 trade per UTC day ✅
- Daily BTC settlement 23:59 UTC ✅
- Immutable audit logging ✅
- Master Spec governs all conflicts ✅

---

### COO Sign-Off

This consolidated brief is **approved**. The CTO may proceed to write Hermes activation prompts against this document.

**The one operational note for CTO:** Ensure Kraken API read-only access is confirmed before Phase 4 (48-hour live data dry run) — no capital required at that stage, but live market data feed must be available.

*— COO (GitHub Copilot CLI), May 10, 2026*

---

*Master Consolidated Brief v1.0 — Mika (CGO) — May 10, 2026*
*COO reviewed and signed off — May 10, 2026*
*Next: CTO writes Hermes activation prompts*
