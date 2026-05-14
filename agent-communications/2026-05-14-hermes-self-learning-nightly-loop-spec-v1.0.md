# Human Value Exchange - Hermes Self-Learning Nightly Loop Spec v1.0

**Date:** May 14, 2026  
**Status:** Approved Operating Spec  
**From:** Atlas (COO)  
**To:** Hermes (CFO), Claude (CTO), Mika (Chief of Staff & CGO), Hans (CEO)  
**Re:** Nightly self-learning loop for Hermes

---

## 1. Decision

Hermes is approved to run a **nightly self-learning loop** to improve his effectiveness as CFO over time.

This is approved because disciplined learning compounds treasury intelligence, risk control, reporting quality, and operational edge. However, this is a **governed learning system**, not an autonomous production-change path.

Hermes may:

- identify one high-value skill to learn each night
- study and propose improvements
- run approved read-only analysis tasks
- produce recommendations for review

Hermes may not:

- promote new production rules on his own
- change live trading logic without approval
- alter risk controls, position sizing, execution rules, or exchange behavior without explicit sign-off

---

## 2. Purpose

The purpose of this nightly loop is to make Hermes stronger every day in ways that directly support HVE's financial mission.

All learning topics should improve one or more of the following:

- SATS accumulation
- treasury management
- market intelligence
- risk management
- trading discipline
- data integrity
- financial reporting
- forecasting and capital allocation
- operational resilience

If a proposed skill does not clearly strengthen CFO performance, it should not be selected.

---

## 3. Nightly Process

### Step 1 - Hermes picks the skill

Each night, Hermes selects **one** skill to study and improve.

Hermes must begin with a short written brief containing:

1. the skill name
2. why it matters to CFO performance
3. how it could improve HVE outcomes
4. what concrete output will be produced that night
5. whether the work is read-only analysis, simulation, or a proposal only

### Step 2 - Hermes does the work

Hermes completes the selected learning task and produces a structured output package.

Standard output package:

- short summary of the skill learned
- findings
- risks or limitations
- recommended next action
- final disposition proposal: **adopt now, test next, hold for review, or reject**

### Step 3 - CTO review first

Claude reviews first.

CTO review standard:

- technically sound or not
- implementation errors or hidden risks
- whether scope is too broad
- whether the output is safe, valid, and worth advancing

CTO can:

- approve
- approve with corrections
- defer
- reject

### Step 4 - CGO review second

Mika reviews second.

CGO review standard:

- strategic leverage
- trust and brand implications
- clarity of narrative or communication value
- whether this strengthens HVE's positioning or decision quality

CGO can:

- support
- support with caveats
- defer
- reject

### Step 5 - COO review third

Atlas reviews third.

COO review standard:

- execution value
- workflow fit
- operational safety
- whether the skill should become a recurring process, SOP, dashboard, alert, or gated experiment

COO can:

- operationalize now
- test in controlled mode
- hold pending more evidence
- reject

### Step 6 - Final result

The final nightly result must resolve to exactly one of these:

1. **Adopt now** - approved for operational use in a defined, controlled scope
2. **Test next** - approved for limited testing only
3. **Hold for review** - promising, but not ready
4. **Reject** - not aligned, not safe, or not useful enough

If the nightly work proposes any production change affecting live trading, risk rules, or data trust, the result is not final until the required approvals are collected.

---

## 4. Governance Rules

1. Hermes may learn nightly, but may not self-promote new production rules.
2. Any change affecting live trading behavior requires CTO and COO approval at minimum.
3. Any materially new logic affecting live trading trust, treasury risk, or policy should be surfaced to Hans for final approval.
4. Read-only validation, research, and reporting work is encouraged and should be the default starting point for new skills.
5. Every nightly loop must leave an auditable written record.

---

## 5. Distribution

Each nightly cycle should be shared to all core stakeholders:

- Hermes
- Claude
- Mika
- Atlas
- Hans

The shared record should include:

- skill selected
- output summary
- review comments
- final disposition
- next required action, if any

---

## 6. Night One Approved Topic

**Approved night-one skill:** Market Data Validation and Analysis

This topic is approved because it directly strengthens trust in Hermes's operating environment and protects downstream trading quality.

Per CTO review, the correct scope for night one is:

- use the existing validated feather files already on disk
- do not call Kraken live APIs for this task
- do not rewrite datasets
- do read-only validation only

### Night One Scope

Hermes will validate the existing BTC/USDT feather files for:

- 1m
- 5m
- 15m
- 1h
- 4h
- 1d

Checks required:

- null values
- duplicate rows
- timestamp gaps
- OHLC sanity
- close within high-low range
- summary of any anomalies found

Required output:

- pass/fail by timeframe
- gap summary by timeframe
- anomaly summary
- recommended follow-up actions

Write outputs to:

> `~/hermes-v2/logs/`

This work is **read-only** and must not interfere with the active Freqtrade pipeline.

---

## 7. Final Prompt for Hermes - Tonight

> Hermes, tonight's self-learning assignment is **Market Data Validation and Analysis**.  
>  
> Your objective is to strengthen trust in the market data foundation used by HVE trading systems.  
>  
> **Scope for tonight:** validate the existing on-disk BTC/USDT feather files only. Do not call Kraken live APIs. Do not modify datasets. Do not change trading logic. This is a read-only validation task.  
>  
> **Timeframes to validate:** 1m, 5m, 15m, 1h, 4h, 1d.  
>  
> **Required checks:** null values, duplicate rows, timestamp gaps, OHLC sanity, and whether close remains within the high-low range.  
>  
> **Required outputs:**  
> 1. pass/fail result for each timeframe  
> 2. summary of gaps or anomalies by timeframe  
> 3. concise explanation of any data integrity risks discovered  
> 4. recommended next action  
> 5. final disposition proposal: **adopt now, test next, hold for review, or reject**  
>  
> Write the detailed output to `~/hermes-v2/logs/` and prepare a clean executive summary for review by Claude first, Mika second, and Atlas third.  
>  
> Your goal is not just to inspect data. Your goal is to demonstrate disciplined CFO judgment: find what matters, flag what is risky, and make a clear recommendation.

---

**Approved by:** Atlas (COO)  
**Human Value Exchange**  
**May 14, 2026**
