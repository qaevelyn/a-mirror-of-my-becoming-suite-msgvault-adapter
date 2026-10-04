# A Mirror of My Becoming™ Suite: msgvault Adapter

**The ship that reads mail in its own native tongue.**

Ship 7 of A Mirror of My Becoming™. Built October 2026 on an 8 GB Intel MacBook Air. Reads msgvault.db (SQLite mail archive), normalizes RFC822 message-ids, preserves full metadata, and feeds the canonical Chroma store with nomic-embed-text vectors — the fleet's model. The embed_gen watermark is built into msgvault's own schema: progress lives in the data itself. Crash, restart, curfew, resume — never re-ingest, never duplicate.

**Author:** Evelyn Caro

---

## What it does

Bridges a SQLite mail archive into the canonical Chroma vector store. Replace-mode: stale chunks deleted batch-wise before fresh replacements land. Idempotent upserts. Deterministic IDs derived from normalized message-ids. Every chunk carries full metadata — sender, timestamp, subject, thread position, message type.

---

## Why it exists

The prior-art search (three passes: GitHub, Reddit/HN/PyPI, and unweighted problem-space) found the pieces scattered across repositories and tutorials — normalization in one PR, deterministic Chroma IDs in another — but nobody publishes the resilience-engineered bridge between a SQLite mail archive and a Chroma vector store. Ship 7 is that bridge, with the fleet's crash-survival engineering behind it. First published of its kind.

---

## Curfew schedule

| Night | Curfew |
|-------|--------|
| Mon / Tue / Thu / Fri | `--curfew 08:00` (stop cleanly, stamp, resume on relaunch) |
| Wed / weekend | No curfew — runs 24 hours |

Never self-restarts. The owner decides when to relaunch.

---

## Requirements

- Python 3 with: `chromadb`, `langchain`, `langchain-ollama`
- [Ollama](https://ollama.com) running locally, with `nomic-embed-text` pulled
- A msgvault.db SQLite archive

---

## Quickstart

Dry run (10 messages, no writes):
python3 ingest_msgvault.py --db ~/.msgvault/msgvault.db
--store /tmp/test-store --collection mirror_food_emails --dry-run

Real run (overnight, curfew at 8 AM):
nohup python3 -u ingest_msgvault.py
--db ~/.msgvault/msgvault.db
--store /path/to/vector-store
--collection mirror_food_emails
--embed-model nomic-embed-text
--heartbeats --curfew 08:00 &
---

## The fleet

- **[Ship 1](https://github.com/qaevelyn/a-mirror-of-my-becoming-rag-ship1-deepseek-rag-local)** — DeepSeek RAG, rebuilt local
- **[Ship 2](https://github.com/qaevelyn/a-mirror-of-my-becoming-rag-ship2-ibm-granite-agentic)** — IBM Granite Agentic RAG
- **[Ship 3](https://github.com/qaevelyn/a-mirror-of-my-becoming-rag-ship3-ibm-granite)** — IBM Granite Standard RAG
- **[Ship 4](https://github.com/qaevelyn/a-mirror-of-my-becoming-rag-ship4-ibm-granite-agentic)** — IBM Granite Agentic RAG
- **[Ship 5](https://github.com/qaevelyn/a-mirror-of-my-becoming-rag-ship5-ibm-granite-agentic-evidenceflow)** — IBM Granite Agentic RAG with EvidenceFlow
- **[Ship 6 — Suite: Ingestion Tools](https://github.com/qaevelyn/a-mirror-of-my-becoming-suite-ingestion-tools)** — the suite that feeds the fleet
- **[Ship 7](https://github.com/qaevelyn/a-mirror-of-my-becoming-suite-msgvault-adapter)** — this repo — msgvault adapter
**[A Mirror of My Becoming™](https://github.com/qaevelyn/a-mirror-of-my-becoming)** — the parent index.

---

## License

Dual-licensed:

- **AGPL-3.0** — free to use, modify, and redistribute under the terms of the license. Full text in [LICENSE](LICENSE).
- **Commercial license** — available for organizations that need to use the code without the AGPL-3.0 obligations. Contact the author for pricing.

Free does not mean free to exploit. If you build a product on this work, the author expects to be paid.

---

## Author

**Evelyn Caro** — Sovereign AI Builder.

**[qaevelyn.github.io](https://qaevelyn.github.io)** · Commercial licensing: **evelyn.caro.cloud@gmail.com**

---

© 2026 Evelyn Caro. All rights reserved.
