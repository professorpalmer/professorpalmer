# Cary Palmer

Senior machine learning engineer working on durable agent infrastructure, orchestration, retrieval, computer vision, and applied ML.

[LinkedIn](https://www.linkedin.com/in/cary-palmer-a30557175) · [Portfolio](https://dugoutfantasy.com/portfolio) · [Portable LLM Wiki](https://portablellm.wiki/professorpalmer)

Everything is open source, so feel free to steal anything useful. Happy to discuss any of it, anytime.

## Projects

### [Puppetmaster](https://github.com/professorpalmer/Puppetmaster)

A provider-neutral control plane for agent swarms: subprocess workers, model routing, leases, artifacts, memory, CodeGraph context, and deterministic result stitching.

This is Redis + Gunicorn + Git + SQLite in an agentic layer. It is the foundation of everything I do in work, research, and my own harnesses. I install it everywhere and make it the default agent runtime. No more subagents. No more transcripts as the source of truth.

- Durable SQLite-backed jobs, leases, retries, artifacts, receipts, and memory
- Provider-neutral routing across local, subscription, and API-backed models
- Parallel workers with isolated execution and deterministic stitching
- Shared CodeGraph context for repository navigation
- Replayable results and zero-model-call artifact recall

- **SWE-bench Lite:** 47–48% token-matched savings and 29% lower actual spend with cost routing and durable retries in a controlled, single-seed study. [Study and frozen predictions](https://github.com/professorpalmer/swebench-pm)
- **NL2Repo-Bench:** 91.1% mean upstream test-pass rate, about 2.28 times the published approximately 40% state of the art; 53% of libraries reached a fully green upstream suite. [Paper and methodology](https://professorpalmer.github.io/durable-state-vs-context/)
- **Agent storms:** coordinated 1,000 concurrent agents in a public demonstration, then reached 1,493 concurrent agents with Puppetmaster + Hermes in one storm, without subagents.

<details>
<summary>More measured results and caveats</summary>

- **Full-repository migration:** the durable arm repaired a 364-module strict JavaScript-to-TypeScript migration to zero type errors. The one-shot monolith retained 16 strict errors, while stateless retrieval produced approximately 290 errors at the 120-module scope.
- **Resumability:** after a hard interruption, the durable arm preserved 17 of 24 completed modules and resumed to a full oracle pass; the monolith preserved none.
- **Parallel headroom:** the full-scale dependency critical path fell to 4.6% of total work, exposing 21.6 times theoretical dataflow headroom. The measured serving ceiling was approximately 10–12 concurrent Cursor sessions; the same orchestrator sustained 100% worker success through 32 concurrent Claude Code sessions.

The papers and studies publish their caveats, machine-readable ledgers, frozen predictions, and reproduction commands. These are measured workflows, not guarantees for every repository or model.

</details>

### [Portable LLM Wiki](https://github.com/professorpalmer/portable-llm-wiki)

A vendor-neutral personal context layer for LLMs. Knowledge lives as structured Markdown in git and can be queried from any client through HTTP or MCP.

The wiki supports provenance, typed pages, graph-aware retrieval, linting, access tiers, selective sharing, and QR handoff. It lets people and models share specific context, rules, skills, hooks, and project history without locking that knowledge inside one chat product.

[Open the hosted wiki](https://portablellm.wiki/)

### [Marionette](https://github.com/professorpalmer/marionette)

A desktop agentic coding harness built around durable state, multi-agent work, and Puppetmaster orchestration.

Marionette integrates Portable LLM Wiki into its backend and can inject the relevant rules, skills, hooks, project context, and retrieved history at runtime. It is my largest project and daily driver, and it remains an active work in progress.

[Project site](https://professorpalmer.github.io/marionette/)

### [Automaton](https://github.com/professorpalmer/Automaton)

A native GPUI, GrokBot-style staff interface built on Puppetmaster. Named automata speak, dispatch work, and query durable state instead of stuffing permanent staff history into an ever-growing transcript.

The measured query-first path reduced inference calls by 95% on repeated work: one paid miss followed by 19 zero-call recalls. A 400-turn workday replay with 5% novel tasks avoided 376 calls, or 94%; its late window reached 98%. A separate 330-turn hostile safety mix recorded 83 valid recalls with zero false hits and zero stale hits.

[Architecture, ledgers, and reproduction](https://github.com/professorpalmer/automaton-durable-state)

### [Discord OS](https://github.com/professorpalmer/discord-os)

A poor man's AWS stack for local agent work. Discord becomes the phone UI, identity and permission layer, notification system, job-thread manager, and blob store while your own Mac or PC supplies the compute.

Each channel can bind to a git checkout. Asks become durable, steerable jobs; analysis can run concurrently while writes serialize safely per repository. Puppetmaster handles orchestration, and the host can expose GitHub, AWS, Portable LLM Wiki, or arbitrary CLI and HTTP tools to workers. No hosted fleet is required.

<details>
<summary>What is already in the harness</summary>

- On, Off, Ask, Pair, Halt, Gate, Roles, GitHub, Files, Terminal, Browser, and recent-job controls
- Approval, cancellation, retry, spend caps, and remote halt/resume
- Live progress cards, durable thread history, completion summaries, and in-thread steering
- Concurrent jobs with per-checkout write serialization
- Channel-to-checkout realms and repository-aware routing
- Recurring SQLite-backed jobs and voice-memo task intake
- Durable think-tank channels and Portable LLM Wiki retrieval
- GitHub, AWS CLI, and arbitrary CLI/HTTP host tools
- OpenRouter, Cursor, Puppetmaster, and optional Marionette compute paths
- Local key vault, short-lived pairing tickets, secret shredding, and subprocess-only key injection
- Discord attachment storage addressed by channel, message, attachment, and SHA-256
- SQLite persistence for tasks, runs, events, memory, artifacts, schedules, spend, permissions, and intake watermarks
- Path-confined terminal and file actions plus allowlisted browser targets
- macOS and Windows background-host support

</details>

### [Cursor Buddy](https://github.com/professorpalmer/cursor-buddy)

A Cursor and harness plugin that ingests archived chats into a local SQLite vault and makes them searchable over MCP through catalog-residual retrieval. Export is ingest; pruning is an explicit separate action. Archived conversations remain durable and queryable without being written back into Cursor's live renderer database.

## Research papers and experiments

### [State, Not Tokens](https://professorpalmer.github.io/durable-state-vs-context/)

A controlled study of repository-scale agent reasoning. The results argue that durable state, retrieval, and navigation matter more than simply increasing the nominal context window.

The durable architecture reached a 91.1% mean test-pass rate on NL2Repo-Bench, about 2.28 times the published approximately 40% state of the art. The controlled migration study also found that durable accumulation produced repairable, consistent shared state where stateless retrieval produced structural cross-file conflicts.

[Paper, source, and data](https://github.com/professorpalmer/durable-state-vs-context) · [PDF v12](https://professorpalmer.github.io/durable-state-vs-context/paper.pdf?v=12) · [Zenodo](https://doi.org/10.5281/zenodo.20709565)

### [Subtraction](https://professorpalmer.github.io/subtraction/)

Research into why coding agents tend to add code instead of removing it, and which interventions can produce smaller patches without breaking behavior.

[Source and experiments](https://github.com/professorpalmer/subtraction)

### [Durable Autoresearch](https://github.com/professorpalmer/durable-autoresearch)

A paper and experiment suite for running durable autonomous research on medium-sized GPUs using persistent research memory, verification, remembered negative results, and reproducible evaluation.

In the live A/B, the durable arm used approximately 20% fewer GPU-seconds than the soft-memory arm. At publication, Puppetmaster's Stitch was the number-one medium-GPU agent with a 0.947135 beat on a 24 GB RTX 3090 at approximately $0.24 per hour. The project does not claim the global XL-GPU lead.

[Contemporaneous result post](https://x.com/CaryPalmerr/status/2086068849598726211)

### [Automaton Durable State](https://github.com/professorpalmer/automaton-durable-state)

Research on how query-first retrieval, bounded context, durable state, and artifact reuse reduce the amount of live conversational context required by a persistent staff system.

Published ledgers measure 95% inference avoidance on repeated work, 94% across a 400-turn workday replay with 5% novel tasks, and 25.15% on a hostile mixed workload with zero false or stale hits.

### [Catalog Residual](https://professorpalmer.github.io/catalog-residual/)

My Codex-style compaction method: extractive handles, last-wins retrieval, and a compact catalog of dropped context. The production seam is integrated into Marionette, while the independent repository contains the lab, evaluation battery, and paper. A compatible version has also been contributed upstream to Hermes.

[Source and experiments](https://github.com/professorpalmer/catalog-residual)

### [StrongOrc](https://github.com/professorpalmer/strongorc)

My benchmark for evaluating models both as durable orchestrators and as workers inside an orchestrated system. It separates orchestration quality from raw worker capability and tests both under confined, reproducible conditions. Strong work in progress. Expensive as hell.

## Other work

My earlier and parallel work includes computer-vision systems, pitch-level baseball ML, fantasy sports tooling, and long-running FFXI open-source projects. Selected work is collected in my [portfolio](https://dugoutfantasy.com/portfolio).
