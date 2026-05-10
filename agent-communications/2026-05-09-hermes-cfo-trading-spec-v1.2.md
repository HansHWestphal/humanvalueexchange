# HERMES CFO — CRYPTO TREASURY & TRADING SYSTEM
## Master Project Spec (v1.2)

**Project Owner:** Hans Westphal (Toronto)
**Hardware:** NVIDIA DGX Spark (128 GB unified memory, Blackwell GPU)
**Document Owner:** COO (GitHub Copilot CLI)
**Status:** Draft — pending input from Mika (CGO) before master spec finalization
**Version History:** v1.0 → v1.1 (Hans) → v1.2 (COO edits + additions)

---

## Mission Statement

Hermes exists to build HVE's Bitcoin treasury through disciplined, systematic trading — not speculation.
Every decision is governed by process, not emotion.
The fiat system is a game we play to stack SATS. Hermes is the machine that plays it without ego, without fatigue, and without deviation from the rules.

---

## Core Goal

**Target:** $10M BTC treasury value (measured in USD at current spot price).
**Starting capital:** $1,000 USD live capital.
**Path:** Systematic daily compounding via 1% risk per trade, quarterly USD profit realization, continuous BTC accumulation.
**Bitcoin-maximalist mindset:** Every trading win stacks SATS. Fiat is fuel. BTC is the destination.

---

## 1. Core Philosophy & Architecture

- 100% local on DGX Spark — native Linux installation only. No Docker. No containers. Ever.
- Hermes CFO is a multi-agent intelligence fabric following the Hermes CFO Multi-Agent Intelligence System (v1).
- All models run locally via Ollama.
- Cognitive specialization via the 4-agent collective (see Section 2).
- **Qwen 2.5 14B is the sole orchestrator, router, and conductor** for the entire system. No other model routes decisions.
- Bitcoin-maximalist mindset: every trading win stacks SATS. Quarterly USD conversion for profit realization and tax clarity.
- Human/Grok-in-the-Loop bi-weekly knowledge updates (X + YouTube research packs).
- Discipline IS the strategy. Consistency and process beat discretion every time.

---

## 2. Hermes CFO 4-Agent Collective (Exact Model Set)

### 2.1 Qwen 2.5 14B — Orchestrator / CFO Brain
**Role:** Task decomposition, priority setting, agent routing, executive synthesis, stage gate evaluation.
This is the **only** model that decides what happens next. Every request, skill, and trading decision flows through Qwen 2.5 14B first.

### 2.2 Mistral Small 24B — Research & Synthesis Agent
**Role:** Financial research, document summarization, cross-source synthesis, market context, knowledge pack ingestion.
Answers: *"What do we know, and what evidence supports it?"*

### 2.3 Nemotron-3 Nano 30B A3B — Execution & Tooling Agent
**Role:** Code generation, financial calculations, tool invocation, deterministic execution, Freqtrade operations, paper trading simulator management.
Answers: *"How do we execute this, step by step, without ambiguity?"*

### 2.4 Gemma 2 27B — Critic / Risk / Sanity-Check Agent
**Role:** Independent critique, risk assessment, logical consistency checking, second opinion on all trade signals.
Deliberately skeptical. Asks: *"Does this actually make sense, and what could go wrong?"*
**Gemma 2 27B holds veto power on individual trades** (see Section 4).

---

## 3. Trade Execution & Decision Authority

This section defines who decides what. Ambiguity in execution authority is a trading risk.

### 3.1 Trade Signal Flow
```
Market Data / Strategy Signal
        ↓
Qwen 2.5 14B (Orchestrator)
— decomposes signal, routes to research + execution agents
        ↓
Mistral Small 24B (Research)       Nemotron-3 Nano (Execution)
— confirms market context          — calculates position size, fees, slippage
        ↓                                    ↓
        └──────────── Gemma 2 27B (Critic) ──┘
                    — independent risk review
                    — APPROVE or VETO
                        ↓
              Qwen 2.5 14B (Final synthesis)
              — issues approved trade instruction
                        ↓
              Nemotron-3 Nano executes via Freqtrade / Kraken API
```

### 3.2 Veto Protocol
- If Gemma 2 27B vetoes a trade: **trade is skipped, no exceptions.**
- Veto reason is logged to `/logs/vetoes/YYYY-MM-DD.log`.
- Hans is notified via Telegram immediately on any veto.
- If Gemma vetoes **3 or more consecutive trades**: system pauses, Qwen 2.5 14B initiates a full review cycle, Hans is alerted.

### 3.3 Freqtrade vs LLM Authority
- **Freqtrade** (via FreqAI): generates quantitative strategy signals and executes approved orders at the exchange level.
- **LLM Agent Collective:** evaluates all signals before execution — qualitative filter, risk check, and sentiment overlay.
- **Final execution authority:** LLM collective (Qwen → Gemma approved) → Nemotron-3 instructs Freqtrade to execute.
- Freqtrade does **not** execute autonomously without LLM approval.

---

## 4. Risk Governance (Non-Negotiable)

These rules are hardcoded into the system. Qwen 2.5 14B enforces them. Gemma 2 27B audits compliance.

### 4.1 Per-Trade Risk
- **Risk per trade:** Exactly 1% of current account equity (sized in USD at entry time).
- **Maximum 1 trade per calendar day** (UTC). No exceptions, no second entries.
- All profits and losses settled into BTC by 23:59 UTC each day.

### 4.2 Circuit Breakers
| Trigger | Action |
|---------|--------|
| Daily loss ≥ 3% of account equity | No more trades today. System locks until next UTC day. Telegram alert to Hans. |
| 5 consecutive losing trades | System pauses. Qwen initiates full review cycle. Hans notified. No live trading until review complete. |
| Account equity drops below $500 USD | Live trading halts immediately. System returns to Stage 1 paper trading. Hans notified. CTO alerted. |
| Gemma vetoes 3+ consecutive trades | System pauses. Full agent review. Hans notified. |
| Any single-day loss > 2% | Telegram alert to Hans (informational — does not halt trading unless 3% threshold hit). |

### 4.3 Quarterly Review
- Quarterly: Convert accumulated BTC profits to USD on Kraken to realize gains and reset fiat side.
- Full P&L review by Hermes CFO collective, presented to Hans.
- Maximum 4 major strategy updates per year (prevents over-optimization).
- Canadian tax compliance: all realized gains/losses documented for CRA reporting.

---

## 5. Full Layered Stack (Bottom → Top — Native Linux Only)

| Layer | Component | Notes |
|-------|-----------|-------|
| **Hardware** | NVIDIA DGX Spark | DGX OS Ubuntu 24.04 ARM64, 128 GB unified memory |
| **OS & Firmware** | DGX OS (secured) | CTO-managed. COO coordinates update timing. |
| **Runtime** | Native Python + Ollama | No Docker, no containers, no virtualenv overhead |
| **Local LLM Layer** | Ollama — 4 models only | Qwen 2.5 14B, Mistral Small 24B, Nemotron-3 Nano 30B A3B, Gemma 2 27B |
| **Hermes Agent Layer** | Base Hermes + Atlas extensions | camel safety, skill-factory, maestro 24/7 orchestration, icarus self-training. MCP server enabled. |
| **Observability** | Open WebUI | Admin control, model health, session inspection |
| **Trading Engine** | Freqtrade (native) | Kraken perps + FreqAI. Single-pair: BTC/USDT only. |
| **Sentiment Layer** | Adapted LLMAgentCrypto | Nicholas Renotte's sentiment logic, adapted for BTC/USDT |
| **Research Layer** | awesome-systematic-trading + RetroChainer + public-apis | Institutional-grade systematic trading frameworks |
| **Exchange** | Kraken only | Spot + perpetual futures. Official Kraken CLI + MCP bridge. |
| **Human Interface** | Telegram | Hans ↔ Hermes primary operational channel |

---

## 6. Trading Strategy

### 6.1 Single-Pair Focus
**BTC/USDT only** — spot and perpetual futures on Kraken.
No other pairs. No diversification by symbol. Depth of mastery > breadth.

### 6.2 Core Strategy
**Jdub Trades 1-Minute Opening Range Scalping** — adapted for BTC volume windows.
- Entry: 1-minute opening range breakout during high-volume BTC sessions
- Sentiment overlay: LLMAgentCrypto sentiment filter (Mistral Small 24B)
- Confirmation: Nemotron-3 calculates precise entry, stop-loss, and target
- Risk: 1% account equity per trade (hardcoded)
- Settlement: Daily BTC conversion at 23:59 UTC

### 6.3 Strategy Evolution
- Maximum 4 major strategy updates per year (quarterly)
- All strategy changes require Stage 0 backtest before re-deployment
- Bi-weekly knowledge packs from Hans/Grok inform incremental tuning

---

## 7. Paper Trading Simulator (Critical Infrastructure)

Kraken has no testnet. This simulator is mission-critical — **no strategy goes live without passing through it.**

### 7.1 Simulator Requirements
Hermes (via Nemotron-3 Nano + Qwen 2.5 14B orchestration) builds and maintains a high-fidelity local paper trading simulation engine that replicates:
- Kraken maker and taker fee structures (exact)
- Realistic slippage modeling
- Order book depth and fill dynamics
- Execution latency simulation
- Daily BTC settlement mechanics (23:59 UTC)
- All circuit breaker logic active during simulation

### 7.2 Simulator Operations
- All backtests run inside the simulator
- All Stage 0 and Stage 1 operations run inside the simulator
- Historical data: minimum 6–8 weeks of recent BTC/USDT OHLCV data
- Monte Carlo stress testing runs in Stage 0 before any advancement

---

## 8. 3-Phase Quarterly Testing Pipeline

**All stage gate evaluations are performed by Qwen 2.5 14B (orchestrator) and confirmed by Gemma 2 27B (critic).**
No human approval required to advance stages — but all stage gate results reported to Hans via Telegram.

### Stage 0: Backtest (inside simulator)
- Minimum dataset: 6–8 weeks recent BTC/USDT data
- Monte Carlo stress test required
- **Pass criteria to advance to Stage 1:**
  - Sharpe ratio ≥ 1.5
  - Maximum drawdown ≤ 15%
  - Win rate ≥ 52%
  - No single losing streak > 7 consecutive trades

### Stage 1: Extended Paper Trading (inside simulator)
- Duration: Minimum 60 days of simulated daily trading
- Daily BTC settlement active
- All circuit breakers active
- **Pass criteria to advance to Stage 2:**
  - Same thresholds as Stage 0 — maintained over 60-day live simulation
  - No circuit breaker events in final 30 days of Stage 1
  - Gemma 2 27B confirms readiness

### Stage 2: Live Trading
- Starting capital: $1,000 USD
- All governance rules active from Day 1
- **Quarterly review criteria (return to Stage 1 if):**
  - Live drawdown hits 20%
  - 3 circuit breaker events in a single quarter
  - Strategy Sharpe drops below 1.2 over rolling 30 days

### First Action After Build
Build the local Kraken paper trading simulator → run April/May 2026 paper simulation (daily BTC settlement, all circuit breakers active).

---

## 9. Knowledge Repository

**Location:** `knowledge-repo/`

**Structure:**
```
knowledge-repo/
├── x-threads/
├── youtube-summaries/
├── update-packs/
│   └── YYYY-MM-DD/
├── research-notes/
├── paper-simulations/
└── historical-data/
```

**Ingestion SLA:** All research packs ingested within 24 hours of delivery by Hans.
**Ingestion owner:** Mistral Small 24B (research agent) — ingests, summarizes, and tags all new material.
**Review owner:** Qwen 2.5 14B — flags any strategy-relevant findings to Hans via Telegram.
**Cadence:** Bi-weekly updates from Hans + Grok (X + YouTube research packs). All content BTC-focused.

---

## 10. Monitoring, Health & Operational Continuity

### 10.1 System Health Checks
- Hermes self-monitors system health every 6 hours via Qwen 2.5 14B
- Ollama model availability verified before every trading session opens
- If any model is unavailable: trading is suspended, Hans and CTO notified immediately via Telegram

### 10.2 Reporting Cadence
| Report | Frequency | Channel |
|--------|-----------|---------|
| Daily P&L + BTC accumulated | Daily at 08:00 UTC | Telegram → Hans |
| Weekly summary (BTC treasury, USD equivalent, drawdown status) | Every Monday 08:00 UTC | Telegram → Hans |
| Stage gate results | On completion | Telegram → Hans |
| Circuit breaker events | Immediate | Telegram → Hans |
| Quarterly P&L + strategy review | Quarterly | Telegram → Hans (full report) |

### 10.3 Logging & Audit Trail
- All trades logged: entry, exit, size, P&L, BTC settlement amount
- All agent reasoning chains logged (Qwen routing decisions, Gemma veto rationale)
- All critic vetoes logged to `/logs/vetoes/YYYY-MM-DD.log`
- Audit trail is **immutable append-only** — no log modification ever
- Logs retained for minimum 7 years (Canadian tax / regulatory standard)

### 10.4 Failure & Recovery
- If Ollama crashes mid-session: no trades executed, system waits for restart, Hans notified
- If Kraken API becomes unavailable: all pending orders cancelled, no new orders, Hans notified
- Recovery playbook: CTO owns infrastructure recovery; COO coordinates communication to Hans

---

## 11. Telegram Escalation Triggers

All of the following trigger an **immediate Telegram alert to Hans** — no delay, no batching:

| Event | Severity |
|-------|----------|
| Circuit breaker triggered (any type) | 🔴 Critical |
| Account equity below $500 USD | 🔴 Critical |
| Ollama model unavailable | 🔴 Critical |
| Kraken API unavailable | 🔴 Critical |
| Gemma vetoes 3+ consecutive trades | 🔴 Critical |
| Stage gate passed (advancement) | 🟢 Info |
| Stage gate failed | 🟠 High |
| Single-day loss > 2% | 🟠 High |
| Gemma single trade veto | 🟡 Medium |
| Daily P&L report | 🟢 Info |
| Weekly summary | 🟢 Info |
| New knowledge pack ingested | 🟢 Info |

---

## 12. Key Inspirations & Sources

| Source | Role in System |
|--------|---------------|
| Hermes CFO Multi-Agent Intelligence System (v1) | Full agent architecture |
| Jdub Trades — 1-Minute Opening Range Scalping | Core trading strategy |
| Nicholas Renotte — LLMAgentCrypto | Sentiment analysis layer |
| awesome-systematic-trading (wangzhe3224) | Institutional systematic trading frameworks |
| RetroChainer Open-Source AI Stack | Agent chaining patterns |
| public-apis (public-apis/public-apis) | Data feed integrations |

---

## 13. Activation Phrases (How to Use)

| Phrase | Action |
|--------|--------|
| `"Hardware is here"` or `"Build Hermes CFO v1.2"` | Begin full system build |
| `"Run 2-week research pack"` | Trigger bi-weekly knowledge update cycle |
| `"Stage gate report"` | Request current stage status and pass/fail metrics |
| `"Treasury report"` | Full BTC holdings, USD equivalent, P&L summary |
| `"Veto log"` | Review all recent Gemma critic vetoes |
| `"Circuit breaker log"` | Review all circuit breaker events |

---

## 14. Open Items for Mika (CGO) Input

*This section is for Mika's review before master spec finalization:*

- [ ] **Brand voice for Telegram reports** — should daily P&L messages to Hans feel clinical/data-first, or should they reflect HVE's sovereignty/Bitcoin-maximalist brand voice?
- [ ] **Public-facing narrative** — as HVE grows, will the Hermes trading arm ever be part of the public brand story (proof of concept for financial sovereignty)? If so, Mika should shape the messaging framework now.
- [ ] **Bitcoin payment rail** — once live trading generates BTC profits, does this accelerate the Bitcoin payment rail decision for HVE's coaching products? Mika's input on timing and messaging.
- [ ] **Content opportunity** — Hermes trading performance (wins, milestones, BTC accumulated) could be powerful sovereignty/Bitcoin content for X, Substack, LinkedIn. Mika to advise on what to share and when.

---

## 15. Document Routing

| Agent | Action |
|-------|--------|
| **Mika (CGO)** | Review Section 14 open items. Provide brand voice + narrative input. |
| **CTO** | This is the definitive build spec. Section 5 stack is the authoritative reference. |
| **Hans (CEO)** | Final approval before master spec is locked. |
| **COO** | Tracks delivery against this spec. Coordinates all agent inputs into master v2.0. |

---

*v1.2 authored by COO — May 9, 2026*
*Incorporates v1.1 by Hans Westphal + COO operational governance additions*
*Status: Awaiting Mika (CGO) input → then master spec v2.0*
