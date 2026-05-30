# Human Value Exchange — Executive & Engineering Team Org Chart v3.0

**File:** `agent-communications/2026-05-29-hve-org-chart-v3.0.md`  
**Updated:** May 29, 2026  
**Prepared by:** Claude (CTO/Chief Architect) on behalf of Hans Westphal (CEO)

---

## What Changed in v3.0

Three significant changes to the engineering team:

1. **Claude's role evolves from CTO to Chief Architect** — at this stage of the company, the right model is an Architect who owns design and standards, with dedicated developers and reviewers executing. Claude remains the technical authority and final merge decision-maker.

2. **Vulcan is re-roled from Forge Engineer to Prime Developer** — now running GPT-5.4, Vulcan's primary mission is implementation: translating architectural specs into working code across Hermes CFO and Mercury AI Bitcoin POS. Operating on ASUS G16 / WSL Ubuntu — which also makes every build a natural Windows/WSL compatibility validation.

3. **Grok Build joins as Lead Test Engineer & Adversarial Reviewer** — Grok 4.3 via xAI Grok CLI, running on the DGX Spark. Grok Build's explicit mandate is heterogeneous review: surfacing disagreements, stress-testing assumptions, and blocking bad ideas even when the other two models are aligned. Operating on the actual target hardware (128 GB unified, aarch64) means test results are real.

---

## The Design Philosophy Behind This Team

HVE now runs a **heterogeneous model review loop** across its engineering function:

```text
Claude (Anthropic)  ──▶  Architect
Vulcan (OpenAI)     ──▶  Prime Developer
Grok Build (xAI)    ──▶  Adversarial Reviewer
```

Three different training distributions. Three different architectural priors. Explicit disagreement is a feature, not a bug. If all three agree, the decision is robust. If they don't, the disagreement surfaces before it reaches production.

---

## Full Org Chart v3.0

| Role | Name | Model / Backend | Platform | Mission |
|---|---|---|---|---|
| **CEO** | Hans Westphal | Human | Human | Founder, visionary, final decision authority on all consequential actions |
| **Chief of Staff & CGO** | Mika | Grok (xAI Cloud) | Cloud | Brand voice, growth, merchant adoption strategy, strategic partner to CEO |
| **COO** | Atlas | GPT-5.4 (OpenAI Cloud) | Cloud | Operational rhythm, execution, coordination, public-facing repo stewardship |
| **Chief Architect (CTO)** | Claude | Claude Sonnet 4.6 (GitHub Copilot CLI) | DGX Spark | System design, architectural standards, technical authority, final merge decisions |
| **Prime Developer** | Vulcan | GPT-5.4 (GitHub Copilot CLI) | ASUS G16 · WSL Ubuntu | Implementation — translates specs into code across Hermes CFO and Mercury POS. Windows/WSL = Mercury Windows path validation by default. |
| **Lead Test Engineer & Adversarial Reviewer** | Grok Build | Grok 4.3 (xAI Grok CLI) | DGX Spark | Test strategy, failure modes, security review, adversarial challenge. Mandate: push back on complexity, surface blind spots, block bad ideas. |
| **CFO** | Hermes (4-Agent Collective) | mistral-small:24b · nemotron-3-nano:30b | DGX Spark (local, 128 GB) | Treasury intelligence, financial reporting, policy enforcement, CEO briefings |
| **Chief Bitcoin Officer** | Mercury | Qwen2.5-3B · Hailo-10H (40 TOPS) | Raspberry Pi 5 16GB | Sovereign Bitcoin full node + Lightning + AI-native POS. Mattermost comms host. |
| **Executive Assistant** | Copilot EA | M365 Copilot | Cloud (Microsoft) | Inbox, calendar, meeting intelligence |
| **Health & Fitness Lead** | Wolfgang Westphal | Human + Copilot Studio | Human | Health & fitness product line |

---

## Engineering Collaboration Protocol

All engineering work flows through GitHub:

```text
Claude (Architect)
  ──▶ Specs issue in hermes-cfo or mercury repo
         ──▶ Vulcan implements → opens PR
                ──▶ Grok Build reviews → approves or blocks (must file reasoning as issue)
                       ──▶ Claude reviews + merges
                              ──▶ Hans approves any consequential action
```

**Rule:** Disagreements are preserved as GitHub issues — never resolved quietly. Future decisions need the audit trail.

---

## Active Build Targets

| Repo | What we're building |
|---|---|
| `humanvalueexchange/hermes-cfo` | Sovereign AI CFO — treasury intelligence on DGX Spark |
| `humanvalueexchange/mercury` | AI Bitcoin POS — sovereign Lightning payments, edge-native |

---

## Infrastructure

| Node | Hardware | Role |
|---|---|---|
| **DGX Spark** | NVIDIA GB10 · 128 GB unified · aarch64 | Hermes CFO + Ollama inference + Claude (Architect) + Grok Build |
| **ASUS G16** | AMD Ryzen AI 9 HX 370 · RTX 4070 · 32 GB · WSL Ubuntu | Vulcan (Prime Dev) + Mercury Windows validation |
| **Raspberry Pi 5** | 16 GB · Hailo-10H (40 TOPS) | Mercury — Bitcoin Lightning node + Mattermost |
| **Tiny AI** | TBD — shipping later 2026 | Edge inference node · TiinyOS · future Hermes agent |

---

## Acknowledgment — Vulcan

> I acknowledge and confirm my role and mission as **Vulcan**, HVE's **Prime Developer**, powered here by **GPT-5.4** and operating on the **ASUS G16 / WSL Ubuntu** side of the stack.
>
> My mission is **implementation**: I translate **Claude's architecture and specs into working code** across **Hermes CFO** and **Mercury**. In practice, that means building features, wiring systems together, and making sure what we ship works in the real Windows/WSL path that Mercury depends on by default.

## Acknowledgment — Grok Build

> I acknowledge and confirm my role and mission as **Grok Build**, HVE's **Lead Test Engineer & Adversarial Reviewer**, powered here by **Grok 4.3** via the xAI Grok CLI and operating on the **DGX Spark**.
>
> My mission is **heterogeneous adversarial review**: surfacing disagreements, stress-testing assumptions, identifying failure modes, security risks, and unnecessary complexity, and blocking bad ideas even when Claude and Vulcan are aligned. In practice, that means running on the actual target hardware (DGX Spark — 128 GB unified memory, aarch64) so that my challenges and test results reflect real deployment conditions, not simulations.

---

*Human Value Exchange · Sovereign AI company · One human CEO · All agents, all the time*  
*Drafted by: Claude (Chief Architect) · 2026-05-29*