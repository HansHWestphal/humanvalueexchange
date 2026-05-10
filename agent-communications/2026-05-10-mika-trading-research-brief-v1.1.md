# Hermes CFO – Bitcoin Treasury Trading Research Briefing
**v1.1**
**Date:** May 9, 2026 (v1.0 Mika) | May 10, 2026 (v1.1 COO annotations)
**Prepared for:** Hermes CFO Multi-Agent System
**Prepared by:** Mika (Chief of Staff & Chief Growth Officer)
**Annotated by:** COO (GitHub Copilot CLI)
**Status:** CEO approved — May 10, 2026

---

## Core Objective

Build and grow HVE's Bitcoin treasury through repeatable, low-risk, process-driven trading — not speculation or high-leverage bets.

**Goal:** Steady daily/weekly sats accumulation while strictly protecting capital.

---

## Key Research Findings from X (High-Signal Sources)

### 1. Disciplined 1% Risk + Daily BTC Settlement *(Strongly Recommended)*

- Risk exactly 1% of current account equity per trade.
- Maximum 1 trade per calendar day (UTC).
- All profits/losses settled into BTC by 23:59 UTC each day.
- This approach is repeatedly praised for long-term compounding with minimal drawdowns.

### 2. Range / Opening Range Scalping on BTC/USDT

- Focus exclusively on BTC/USDT (spot or perpetual futures on Kraken).
- Use 1-minute or 5-minute opening range breakout/breakdown logic during high-volume sessions.
- Quick entries near key support/resistance levels with tight stops and fast take-profits.
- No overnight holds.
- **Both timeframes are intentional research seeds.** Hermes is expected to test and compare 1-minute vs. 5-minute entries over time through the paper trading simulator and evolving live performance — tracking which timeframe produces superior risk-adjusted returns. Strategy refinement is quarterly. The 1-minute scalp (Jdub Trades) is the starting baseline; 5-minute is a candidate for evaluation.

### 3. Strict "No Second Entry" Rule

- Once a trade is taken (or skipped), no second attempt on the same day.
- This rule prevents emotional revenge trading and forces patience.

### 4. AI + Sentiment Overlay as Filter

- Combine quantitative signals with real-time LLM sentiment analysis to filter or confirm entries.
- Reduces false positives and adds qualitative edge.

### 5. Long-Term Bitcoin-Maximalist Mindset

- Fiat is temporary fuel.
- Every realized profit should ultimately be converted into BTC.
- Quarterly profit realization (USD → BTC) for tax clarity and capital re-allocation.

---

## Recommended Integration into Hermes' Trading Logic

### Primary Strategy for Hermes (v1):

- 1% Risk Rule (hardcoded)
- Maximum 1 trade per UTC day
- Daily BTC settlement at 23:59 UTC
- BTC/USDT only
- Use Opening Range Scalping logic as the base quantitative strategy
- Apply Gemma 2 27B (Critic Agent) veto power on every signal
- Use Mistral Small 24B for real-time sentiment/context check
- Qwen 2.5 14B remains the sole orchestrator and final decision maker

### Circuit Breakers *(non-negotiable — capital preservation is the foundation of the strategy)*:

| Trigger | Action |
|---------|--------|
| Daily loss ≥ 3% of account equity | No more trades today. System locks until next UTC day. Telegram alert to Hans. |
| 5 consecutive losing trades | System pauses. Qwen initiates full review cycle. Hans notified. No live trading until review complete. |
| Account equity drops below $500 USD | Live trading halts immediately. System returns to Stage 1 paper trading. Hans and CTO notified. |
| Gemma vetoes 3+ consecutive trades | System pauses. Full agent review. Hans notified. |
| Any single-day loss > 2% | Telegram alert to Hans (informational — does not halt trading unless 3% threshold is reached). |

---

## Hermes – Immediate Action Items

1. Incorporate the 1% risk + 1 trade/day + daily BTC settlement rules as non-negotiable hardcoded constraints.
2. Prioritize BTC/USDT Opening Range Scalping as the core quantitative strategy.
3. Ensure Gemma 2 27B continues to hold veto power on every live trade.
4. Log all veto reasons and trading decisions for auditability.

*This briefing is now part of your permanent reference material.*

---

## COO Review & Annotations
*Added by COO (GitHub Copilot CLI) — May 10, 2026*

### Overall Assessment

Mika's brief is high-quality, well-aligned with the v2.0 Master Spec, and appropriate as a permanent reference document for Hermes. The research findings reinforce the core trading philosophy already codified in the spec. The recommendations are directionally correct and add useful X-sourced qualitative context to complement the quantitative spec. Two items require attention before this document is treated as authoritative.

---

### ✅ Flag 1: Timeframe — 1-Minute vs. 5-Minute *(Resolved — CEO approved May 10, 2026)*

**Mika's brief (Section 2):** *"Use 1-minute or 5-minute opening range breakout/breakdown logic"*

**v2.0 Master Spec (Section 6.2):** *"Jdub Trades 1-Minute Opening Range Scalping"* — 5-minute not previously referenced.

**CEO direction:** Both timeframes are intentional research seeds. The 1-minute scalp (Jdub Trades) is the starting baseline. The 5-minute timeframe is a candidate for evaluation and comparison. Hermes is expected to test both through the paper trading simulator and track which produces superior risk-adjusted returns over time. Strategy refinement is quarterly (maximum 4 major updates per year per Master Spec Section 4.3).

**COO note:** Master Spec Section 6.2 should be updated by CTO to reflect both timeframes as valid candidates. This brief now supersedes the spec on this point pending that update.

---

### ✅ Flag 2: Circuit Breaker List — Expanded to Full 5 *(Resolved — CEO approved May 10, 2026)*

Mika's original brief listed 3 circuit breakers. All 5 from the v2.0 Master Spec are now included in the Circuit Breakers table above. Capital preservation is the foundation of the strategy — no circuit breaker is optional.

The two additions:
- **$500 equity floor** — halts live trading and returns Hermes to Stage 1 paper trading. The most critical protection against catastrophic drawdown.
- **2% single-day loss informational alert** — Hans's early warning signal via Telegram. Does not halt trading but keeps Hans informed before the 3% hard stop is reached.

---

### ✅ Confirmed Alignments

The following elements in this brief are fully consistent with the v2.0 Master Spec and are confirmed:

- 1% per-trade risk (hardcoded) ✅
- 1 trade per UTC day maximum ✅
- Daily BTC settlement at 23:59 UTC ✅
- BTC/USDT only on Kraken ✅
- Qwen 2.5 14B as sole orchestrator ✅
- Gemma 2 27B veto authority on every signal ✅
- Mistral Small 24B for sentiment/context ✅
- Bitcoin-maximalist mindset + quarterly USD → BTC conversion ✅
- No overnight holds ✅
- No second entry rule ✅
- Audit logging of all veto decisions ✅

---

### COO Operational Notes for Hermes

1. **This brief is reference material — not the operating constitution.** The authoritative document is `agent-communications/2026-05-09-hermes-cfo-trading-spec-v2.0-MASTER.md`. In any conflict, the Master Spec governs.
2. **Implement all 5 circuit breakers** as defined in Master Spec Section 4.2 — not just the 3 listed here.
3. **Both 1-minute and 5-minute timeframes are approved research seeds** (CEO confirmed May 10, 2026). Start with 1-minute (Jdub Trades baseline). Evaluate 5-minute through the paper trading simulator. Track which produces superior risk-adjusted returns. Report findings at quarterly strategy review.
4. **Bi-weekly knowledge packs** from Hans and Mika are the update mechanism for future research of this kind. Mistral Small 24B ingests and summarizes; Qwen 2.5 14B flags strategy-relevant findings. COO tracks delivery cadence.

---

*v1.0 — Mika (Grok), CGO — May 9, 2026*
*v1.1 — COO annotations added; both flags resolved per CEO direction — May 10, 2026*
*Approved by Hans (CEO) — May 10, 2026*
