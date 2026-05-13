# Human Value Exchange - Copilot Studio Concierge Agent Specification v2.0

**Version:** 2.0  
**Date:** 2026-05-13  
**Owner:** Wolfgang Westphal (Health & Fitness Lead + Copilot Studio Developer)  
**Reviewed by:** CTO Claude  
**Status:** Ready for Atlas to post  
**Filed by:** Atlas, COO (GitHub Copilot CLI)

---

## 1. Mission

Build a sovereign, MCP-native, AI-first client Concierge for Human Value Exchange inside Microsoft Copilot Studio.

The Concierge is the warm, intelligent, always-available front door for HVE clients. It uses generative orchestration - not rigid decision trees - to reason about client intent and route to the right HVE backend or agent. It is backed directly by Hermes via a native MCP server connection and grounded in real M365 context via Work IQ.

The Concierge is not a chatbot. It is a generative agent with live tool access, multi-agent coordination capability, and a sovereign backend.

---

## 2. Architecture Principles (v2.0 Departure from v1.x)

v1.x assumed a REST Edge API as the intermediary between Copilot Studio and Hermes. v2.0 eliminates that layer based on confirmed native MCP support in Copilot Studio (validated by HVE CEO in live demo). This simplifies the stack and makes the system more agentic from day one.

### v1.x Architecture (deprecated)

`Copilot Studio -> REST -> HVE Edge API -> Hermes (DGX)`

### v2.0 Architecture

```text
Copilot Studio (hveglobal tenant)
        |
        |--- MCP Tool: HVE Hermes MCP Server (over Tailscale tunnel -> DGX)
        |--- MCP Tool: Microsoft Learn (for grounding if needed)
        |--- Work IQ (M365 context: email, calendar, meetings)
        |--- SharePoint Knowledge Source (client vault, approved docs)
        |
        \--- Connected Agents (multi-agent orchestration)
              |--- HVE-Finance child agent (Hermes queries)
              |--- HVE-Knowledge child agent (vault retrieval)
              \--- HVE-Task child agent (task/follow-up)
```

Private tunnel: Tailscale connects the Concierge's MCP tool calls through to the DGX Spark. The DGX stays private. No port forwarding. Same posture as v1.2 - only the integration protocol changes.

---

## 3. Target Users

- HVE client individuals and families
- High-intent users who want a single sovereign point of contact
- MVP pilot: 1-2 friendly users before broader rollout

---

## 4. Technical Foundation

### 4.1 Primary AI Model

**Claude Sonnet 4.6** - GA in Copilot Studio globally.

**Rationale:**

- Aligns with HVE's native model stack (CTO instance runs Claude Sonnet 4.6)
- Best reasoning depth in the Copilot Studio external model catalog
- Consistent voice across HVE's agent ecosystem
- GA status - production appropriate

**Admin requirement:** Enable Anthropic external models in Power Platform admin center and M365 admin center before Wolfgang begins build.

### 4.2 Orchestration Mode

**Generative Orchestration** - enabled.

The agent reasons about intent using the LLM. It does not rely on rigid topic triggers. This means:

- Client can say anything naturally; the agent decides which tool or child agent to invoke
- Routing is dynamic, not pre-programmed per every possible phrase
- Fallback and escalation are LLM-governed, not hardcoded topic branches

### 4.3 Backend Integration - MCP Native

Hermes is integrated as a native MCP Tool in Copilot Studio. Wolfgang adds the HVE Hermes MCP Server in the Tools tab exactly as Hans added the Process Mining MCP server in his demo.

**HVE Hermes MCP Server - required tools:**

```text
hermes_get_btc_forecast()        -> latest BTC forecast + briefing summary
hermes_search_knowledge_vault()  -> semantic search across /hve-library
hermes_get_client_context()      -> profile, pending items, open tasks
hermes_create_task()             -> write a task to the follow-up queue
hermes_get_morning_briefing()    -> latest morning briefing artifact
hermes_escalate()                -> submit escalation to correct role
```

**CTO deliverable (post-MVP confirmation):** Build and expose the HVE Hermes MCP Server on DGX. Tunnel via Tailscale. Register as a Power Platform custom connector for Copilot Studio discovery.

### 4.4 Context Awareness - Work IQ (Preview)

Enable Work IQ on the agent to give the Concierge access to real-time M365 context:

- Hans's calendar (upcoming reviews, scheduled calls)
- Recent emails relevant to active client relationships
- Meeting notes and follow-ups

This powers the personalized greeting without requiring a custom API call. The agent knows "Hans has a call at 2pm" without Hermes needing to provide it.

### 4.5 Multi-Agent Design

The Concierge is the orchestrating parent. Specialized child agents handle focused domains:

| Child Agent | Responsibility | Tools |
| --- | --- | --- |
| HVE-Finance | BTC forecast, briefing, treasury queries | Hermes MCP tools |
| HVE-Knowledge | Vault search, note retrieval, provenance | Hermes MCP search tool |
| HVE-Task | Task creation, status, reminders | Hermes MCP task tools |

**Why child agents, not one monolith:**

- Keeps tool count per agent under the ~30-40 performance degradation threshold (per Microsoft guidance)
- Each domain stays independently maintainable
- Wolfgang can build and test each child agent in isolation

### 4.6 Identity and Security

**Microsoft Entra Agent ID (Preview):** Enable automatic Entra identity assignment for the Concierge. Each agent gets its own identity - auditable, revocable, role-scoped.

**Security posture:**

- Client identity authenticated before any personalized data is shown
- All Hermes tool calls scoped to requesting client identity
- No cross-client data exposure - ever
- Full audit log per interaction (timestamp, user, intent, tools called, result, escalation status)
- DGX remains private - all calls enter via Tailscale tunnel to Hermes MCP Server
- No raw vault filesystem exposure

### 4.7 Knowledge Sources

| Source | Type | Scope |
| --- | --- | --- |
| Work IQ | M365 real-time | Calendar, email, meetings |
| SharePoint | Document grounding | Approved HVE client docs |
| Hermes MCP | Semantic vault search | `/hve-library` knowledge base |
| Bing Custom Search | Optional | Scoped web grounding if needed |

---

## 5. MVP Scope

### Must Ship in v1 (MVP)

### A. Personalized Greeting with Real Context

- Work IQ pulls calendar and recent activity
- Greeting references actual upcoming events, open tasks, recent decisions
- Claude Sonnet 4.6 writes the greeting in HVE voice - warm, sovereign, specific

### B. Generative Intent Routing

- LLM classifies intent and routes to the correct child agent or MCP tool
- No rigid trigger phrases required
- Routing categories: Finance/Treasury -> HVE-Finance | Knowledge -> HVE-Knowledge | Tasks -> HVE-Task | Escalation -> human

### C. Knowledge Retrieval with Provenance

- HVE-Knowledge child agent queries `hermes_search_knowledge_vault()`
- Every result includes: source, note/doc reference, timestamp, relevance confidence
- No fabrication - if not found, say so clearly

### D. Task and Follow-Up

- HVE-Task child agent creates and queries tasks via Hermes MCP
- Daily/weekly digest surface behavior
- Status states: open, pending, completed, awaiting review

### E. HVE Voice

- Claude Sonnet 4.6 system prompt defines the voice: warm, clear, sovereign, high-trust, never robotic
- Mika's voice spec embedded in system instructions
- Prefer "let me confirm that" over overconfident responses

### F. Escalation

- Clean escalation path when: confidence low | permissions exceeded | backend unavailable | financial action requested | cross-domain coordination needed
- Role-based targets: Finance -> Hermes/Hans | Operations -> Atlas | Technical -> Claude | Communications -> Apollo

### Out of Scope for MVP

- Initiating financial transactions
- Autonomous account changes
- Voice/audio interface
- Deep health/fitness coaching (Phase 3 - Wolfgang's domain)
- Computer Use automation (Phase 2)
- A2A protocol deep integration with Atlas/Claude (Phase 2)

---

## 6. MVP Build Sequence

### Phase 1 - Foundation

- Enable Claude Sonnet 4.6 in Power Platform admin center and M365 admin center
- Enable Work IQ on the agent
- CTO builds and exposes HVE Hermes MCP Server via Tailscale
- Wolfgang registers HVE MCP connector in Power Platform
- Wolfgang defines HVE voice system prompt (coordinate with Mika)

### Phase 2 - Core Agent Build

- Create parent Concierge agent with generative orchestration
- Create HVE-Finance child agent with Hermes MCP finance tools
- Create HVE-Knowledge child agent with Hermes MCP search tools
- Create HVE-Task child agent with Hermes MCP task tools
- Wire Work IQ for greeting context
- Wire SharePoint knowledge source

### Phase 3 - Test and Tune

- Enable agent evaluations with multi-turn test sets
- Test greeting, routing, retrieval, task, escalation flows
- Validate audit logging end-to-end
- Tune voice/tone in system prompt

### Phase 4 - Pilot

- 1-2 friendly HVE users
- Collect CSAT feedback (thumbs up/down in chat)
- Identify backend gaps
- Gate: 90%+ correct routing before broader rollout

---

## 7. Future Capabilities (Flagged, Not Scoped)

| Capability | Platform Status | HVE Relevance |
| --- | --- | --- |
| Computer Use (CUA / Claude Sonnet 4.5) | Preview | Automate legacy systems without APIs - future phase |
| A2A Protocol (agent-to-agent) | Preview | Direct Hermes <-> Concierge deep integration without MCP intermediary |
| Microsoft Foundry agent connection | Preview | If Hermes moves to Azure AI Foundry |
| Voice interface | Roadmap | Premium client experience - Phase 3+ |
| Wolfgang health/fitness child agent | Future | Wolfgang's domain - after MVP proves stable |

---

## 8. Success Metrics

### Product

- 90%+ requests correctly routed or answered without escalation
- 4.5/5+ average conversation CSAT
- Material reduction in Hans's direct client-touch overhead during pilot

### Technical

- 0 unauthorized cross-client data exposures
- 100% audit logging in production
- < 10 second response target for normal flows
- Graceful degradation when Hermes/DGX is unavailable

### Operational

- Escalation path works cleanly
- No uncontrolled data sprawl across systems

---

## 9. CTO Pre-Requisites Before Wolfgang Can Start Phase 2

1. Hermes MCP Server built and exposed on DGX (CTO deliverable)
2. Tailscale tunnel active between Edge and DGX
3. MCP connector registered in Power Platform custom connectors
4. Anthropic Claude Sonnet 4.6 enabled in tenant admin settings
5. Work IQ enabled in Power Platform admin center for `HVE-Concierge-Agent-Dev` environment
