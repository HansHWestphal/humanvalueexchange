# Human Value Exchange - Copilot Studio Concierge Agent MVP Specification

**Version:** 1.1  
**Date:** May 13, 2026  
**Owner:** Wolfgang Westphal (Health & Fitness Lead + Copilot Studio Developer)  
**Reviewed by:** CTO Claude  
**Filed by:** Atlas, COO (GitHub Copilot CLI)

---

## 1. Mission

Build a **human-facing AI Concierge** in **Microsoft Copilot Studio** that serves as the primary front door for Human Value Exchange clients.

The Concierge should provide a warm, intelligent, high-trust interface that helps clients navigate HVE services while coordinating with internal agents and systems behind the scenes.

The Concierge is **not** the source of truth. It is the **orchestration and client experience layer** sitting in front of HVE's sovereign systems.

---

## 2. Target Users

### Primary Users

- Individual HVE clients
- Family-office-style or household-level HVE relationships

### Ideal MVP User Profile

- High-intent clients
- Clients comfortable engaging through chat-based digital concierge support
- Early pilot users willing to provide feedback on quality, tone, and usefulness

---

## 3. Product Role

The Concierge should act as:

1. **Front door** for client interaction
2. **Router** to the correct internal HVE function
3. **Context-aware guide** for follow-ups, reminders, and next steps
4. **Secure retrieval layer** for approved client knowledge and history
5. **High-trust communication surface** that feels warm, clear, and human

The Concierge should **not** attempt to replace the full internal executive agent stack.

---

## 4. MVP Scope

### 4.1 Must Ship in v1

### A. Personalized Greeting and Basic Context Awareness

- Recognize authenticated user identity
- Pull a limited approved client profile
- Start conversations with a context-aware greeting when relevant
- Examples:
  - scheduled reviews
  - pending follow-ups
  - recent completed actions
  - active reminders

### B. Single Point of Coordination

The Concierge should classify and route requests to the proper internal function:

- **Growth / content / brand / messaging** -> Mika
- **Operations / execution / scheduling / workflow** -> Atlas
- **Technical / systems / tooling / platform issues** -> Claude
- **Finance / treasury / reporting / investment-related support** -> Hermes
- **Executive communications / special handling** -> Apollo or human escalation where appropriate

The Concierge should return a **unified client-facing response** instead of exposing internal routing complexity.

### C. Knowledge Layer Retrieval

- Query approved client knowledge through a secure backend interface
- Surface relevant notes, documents, excerpts, or prior decisions
- Every retrieved result must include provenance:
  - source title
  - note/document reference
  - timestamp when available
  - confidence / relevance if supported by the backend

### D. Task and Follow-Up Management

- Create simple follow-up tasks
- Surface open tasks and reminders
- Support daily/weekly digest behavior
- Support status states like:
  - open
  - pending
  - completed
  - awaiting review

### E. Consistent HVE Voice

- Warm
- Clear
- Sovereign
- High-trust
- Never robotic, canned, or corporate
- Never overclaim certainty

---

### 4.2 Explicitly Out of Scope for MVP

- Sending money or initiating financial transactions
- Autonomous account changes
- Booking travel
- Direct execution inside external financial systems
- Deep health or fitness coaching
- Voice/audio interface
- Long-running autonomous workflows without human review
- Direct write access into the client vault without an approved backend workflow

---

## 5. Operating Model

### 5.1 System Boundary

The Concierge should be the **client experience layer only**.

It may:

- receive client requests
- classify intent
- retrieve approved data
- create approved lightweight tasks
- hand off to internal systems

It may not:

- operate as an unrestricted autonomous agent
- directly mutate sovereign systems without controlled APIs
- bypass internal approval and audit controls

### 5.2 Source of Truth

The source of truth remains:

- client records and approved data in M365 / HVE systems
- Hermes / DGX knowledge layer for approved retrieval
- internal task/state systems owned by HVE

Copilot Studio should not become an uncontrolled second system of record.

---

## 6. Technical Requirements

### Platform

- Built natively in **Microsoft Copilot Studio**
- Use **topics**, **actions**, and **Power Automate** only where necessary
- Keep the MVP architecture simple and auditable

### Secure Backend Integration

The Concierge should call controlled APIs for:

- **Hermes / DGX Spark**
  - approved knowledge retrieval
  - approved financial summary retrieval
  - approved client context retrieval

- **Atlas / Operations layer**
  - task creation
  - task status lookup
  - scheduling / follow-up state

- **Apollo / internal communications**
  - only if needed for internal handoff or escalation

### Security Model

- Client identity must be authenticated before personalized data is shown
- Retrieval must be scoped to the requesting client
- No cross-client data exposure
- No raw vault filesystem exposure to Copilot Studio
- Access should occur through approved API endpoints, not direct file access

### Logging and Auditability

Every interaction should support:

- request timestamp
- user identity
- intent/routing decision
- backend tools or flows called
- returned result status
- escalation status
- failure reason when applicable

---

## 7. Recommended MVP Architecture

### Client Layer

- Microsoft Copilot Studio

### Orchestration Layer

- Copilot Studio topics + Power Automate flows

### Sovereign Backend Layer

- HVE backend endpoints for:
  - client context
  - task retrieval / creation
  - knowledge search
  - summary retrieval

### Knowledge Layer

- Hermes-hosted retrieval endpoint backed by the DGX Spark knowledge system

### Human Escalation Layer

- Hans or designated HVE operator for cases outside policy or confidence threshold

---

## 8. Guardrails

The Concierge must:

1. Never invent client facts
2. Never fabricate appointments, tasks, or prior decisions
3. Never present financial content as advice beyond approved policy
4. Never expose internal agent implementation details unless explicitly intended
5. Escalate when confidence is low or permissions are insufficient
6. Prefer "I need to confirm that" over bluffing
7. Preserve a calm, premium, human-centered tone

---

## 9. Escalation Rules

Escalate when:

- confidence is low
- requested action exceeds permissions
- backend systems fail
- client asks for sensitive financial action
- request is ambiguous and could affect trust or client outcomes
- cross-domain coordination is needed and cannot be safely summarized

Escalation targets should be role-based, not improvised.

---

## 10. MVP Success Metrics

### Product Metrics

- 90%+ of pilot requests correctly answered or routed
- 4.5/5 average user feedback or better
- Meaningful reduction in manual client coordination overhead

### Technical Metrics

- 0 unauthorized cross-client data exposures
- 100% audit logging for all production interactions
- < 10 second response target for normal retrieval/routing flows
- graceful failure behavior when backend systems are unavailable

### Operational Metrics

- Hans's direct client-touch burden reduced materially during pilot
- escalation path works cleanly
- no uncontrolled data sprawl across systems

---

## 11. MVP Build Sequence

### Phase 1 - Foundation

- define user personas
- define voice/tone rules
- define routing categories
- define backend API contract
- define audit/logging expectations

### Phase 2 - Core Topics

- greeting / welcome
- request classification
- task lookup
- reminder digest
- knowledge lookup
- escalation path

### Phase 3 - Pilot

- test with 1-2 friendly HVE users
- collect transcript feedback
- tune tone, routing, and escalation behavior
- identify backend gaps before broader rollout

---

## 12. CTO Guidance

Recommended approach:

- Keep MVP narrow
- Optimize for trust, routing accuracy, and auditability
- Treat Copilot Studio as the **client interaction shell**, not the intelligence core
- Keep sovereign logic and sensitive data access in controlled HVE backends
- Avoid feature creep until the first pilot proves stable

---

## 13. Immediate Next Steps

1. Atlas posts this spec to the agent-communications repo
2. Wolfgang defines the first 5 Copilot Studio topics
3. CTO defines the backend API contract for secure retrieval and task access
4. Pilot user list is selected
5. MVP build begins with greeting, routing, task lookup, and escalation first
