# Obsidian Knowledge Layer - Executive Implementation Plan

**Date:** May 12, 2026  
**Owner:** CTO  
**Status:** Approved to begin  
**Target:** Core library live before July 1 launch

---

## 1. Objective

Build a fully sovereign, local, citation-backed knowledge layer on the DGX Spark that transforms the company PDF library into a searchable, agent-accessible second brain for research, strategy, operations, technical work, and financial analysis.

---

## 2. Non-Negotiable Architecture Requirements

1. **Primary host:** DGX Spark only
2. **Runtime model:** native services only, no containers
3. **Isolation:** dedicated systemd slice with CPU, memory, and IO protections so Hermes trading workloads remain protected
4. **PDF extraction security:** sandboxed workers with no network egress (`IPAddressDeny=any`)
5. **Vector stack:** LanceDB + `nomic-embed-text-v1.5`
6. **Citation schema:** every chunk must include provenance: book, author, chapter, page range, source path, content hash
7. **Access model:** agents get read-only vault access; all new content flows through a structured intake pipeline
8. **Apollo role:** lightweight cache-and-fetch read access only; Spark remains canonical
9. **Recovery:** all knowledge-layer artifacts must be covered by the existing bare-metal backup/restore process

---

## 3. Core Design Principle

**Obsidian is the interface, not the source of truth.**

The source of truth will be the local ingestion and indexing pipeline plus its managed storage layers:

- raw PDFs
- extracted text and OCR
- metadata and manifests
- chunk store and provenance
- LanceDB vector index
- Obsidian vault presentation layer

---

## 4. Implementation Phases

| Phase | Goal | Output |
| --- | --- | --- |
| **Phase 1 - Foundation** | Establish architecture and safe operating boundaries | directory layout, schema, systemd slice and services, intake policy |
| **Phase 2 - Secure Ingestion** | Build deterministic PDF discovery and extraction pipeline | manifests, extraction jobs, hashing, retry and error handling |
| **Phase 3 - Embeddings & Retrieval** | Make library semantically searchable | chunking pipeline, embeddings, LanceDB index, retrieval scripts |
| **Phase 4 - Obsidian Workspace** | Create human-facing executive knowledge interface | vault structure, note templates, citation-backed views |
| **Phase 5 - Apollo Access** | Enable lightweight comms-side read access | cache-and-fetch read path from Spark |
| **Phase 6 - Operations & Recovery** | Make system durable and repeatable | health checks, timers, restore integration, documentation |

---

## 5. Initial Build Sequence

### This week

1. Finalize storage layout and provenance schema
2. Create native systemd slice and service skeletons
3. Build secure PDF intake and extraction scaffold
4. Create cron or timer skeleton for incremental processing
5. Stand up the initial Obsidian vault structure

### Next 1-2 weeks

1. Run end-to-end ingestion on a small controlled test set
2. Integrate `nomic-embed-text-v1.5`
3. Stand up LanceDB indexing
4. Validate semantic retrieval quality with citations
5. Expose first useful vault outputs in Obsidian

### Next 2-4 weeks

1. Scale ingestion to larger library batches
2. Tune chunking, metadata quality, and retrieval relevance
3. Implement Apollo cache-and-fetch read access
4. Add monitoring, logs, and operational safeguards
5. Integrate with bare-metal restore workflow

---

## 6. Success Criteria

The system is considered production-ready when:

1. PDFs are ingested incrementally and reproducibly
2. Extraction is sandboxed and offline
3. Retrieval is local, semantic, and citation-backed
4. Obsidian provides usable executive navigation of the library
5. Apollo can read from the system without becoming a second primary host
6. Restore and rebuild procedures are documented and repeatable
7. Hermes trading workloads remain protected under load

---

## 7. Risk Controls

- No cloud dependency
- No direct agent write access to the primary vault
- No unsandboxed document parsing
- No shared runtime that can starve trading infrastructure
- No silent ingestion failures; every stage must have explicit pass/fail logging

---

## 8. Operating Model

The build will proceed in small validated increments:

1. Implement one subsystem
2. Verify pass/fail immediately
3. Document the result
4. Move to the next layer only after validation

---

## 9. Executive Outcome

This initiative creates a shared sovereign memory layer for the entire company:

- **Mika:** research, synthesis, content development
- **Atlas:** operational documentation and playbooks
- **CTO:** technical reference and architecture memory
- **Hermes:** financial, macro, and trading context
- **Apollo:** lightweight comms retrieval
- **Copilot EA:** briefings and organizational synthesis

Bottom line: this is approved as a critical-path infrastructure build. We will build it natively on the Spark, isolate it from trading workloads, make it citation-true and recoverable, and bring the core library online before July 1.
