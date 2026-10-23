# Sai Harsha Vardhan Mylavarapu

**AI / LLM engineer.** I build evaluation and verification tooling for LLM systems: MCP servers, text-to-SQL benchmarks, and regression gates that catch problems before they ship.

[Portfolio site](https://msharsha565-create.github.io) · [All repositories](https://github.com/msharsha565-create?tab=repositories)

**Contact:** [saiharshamylavara@gmail.com](mailto:saiharshamylavara@gmail.com) · 940-290-1769 · [LinkedIn](https://www.linkedin.com/in/sai-vardhan-mylavarapu-722b67388/)

---

## What I build

LLMs are good at drafting and bad at being right. My projects pair a model with a deterministic check, so output is validated against real data, measured, and fixed in a loop before anyone relies on it.

## Featured projects

### [llm-eval-harness](https://github.com/msharsha565-create/llm-eval-harness)
[![CI](https://github.com/msharsha565-create/llm-eval-harness/actions/workflows/ci.yml/badge.svg)](https://github.com/msharsha565-create/llm-eval-harness/actions)

Regression testing for LLM outputs. Runs a model over a categorized suite, records latency, tokens and cost, compares two runs, and exits non-zero on regression so it can gate CI.

- Layered scoring: exact match, JSON Schema, embedding similarity, LLM-as-judge
- Any OpenAI-compatible endpoint (OpenAI, Ollama, vLLM); records temperature, seed, p50/p95 latency, tokens, cost
- Case-level diffs: two runs with the same pass rate can still hide regressions

### [sqlite-mcp-explorer](https://github.com/msharsha565-create/sqlite-mcp-explorer)
[![CI](https://github.com/msharsha565-create/sqlite-mcp-explorer/actions/workflows/ci.yml/badge.svg)](https://github.com/msharsha565-create/sqlite-mcp-explorer/actions)

A sandboxed text-to-SQL stack: read-only SQL over MCP, a natural-language interface, and a 53-question benchmark scoring syntax validity, schema adherence and execution accuracy.

- Defense in depth: read-only connection, authorizer allow-list, one statement per call, row cap, timeout
- Hallucinated columns and generated writes are caught, and the tests attack every safety layer

### [k8s-manifest-guardrail](https://github.com/msharsha565-create/k8s-manifest-guardrail)
[![CI](https://github.com/msharsha565-create/k8s-manifest-guardrail/actions/workflows/ci.yml/badge.svg)](https://github.com/msharsha565-create/k8s-manifest-guardrail/actions)

A validation gate for LLM-generated Kubernetes manifests, plus an MCP server and a Claude agent that writes a manifest, checks it through MCP, and repairs it until it passes.

### [depwatch-mcp](https://github.com/msharsha565-create/depwatch-mcp)
[![CI](https://github.com/msharsha565-create/depwatch-mcp/actions/workflows/ci.yml/badge.svg)](https://github.com/msharsha565-create/depwatch-mcp/actions)

An MCP server giving agents live dependency-health data from PyPI and npm, plus an agent that audits a `requirements.txt` and writes an upgrade report.

Also: [docsearch-mcp](https://github.com/msharsha565-create/docsearch-mcp), local BM25 document search with cited sources as an MCP server.

## Live results (Gemini, `gemini-3.1-flash-lite`, free tier, one run each, 2026-10-22)

| Eval | Result | Caveat |
| --- | --- | --- |
| llm-eval-harness, plain prompt | 41/55 (75%) | Formatting, not ability: "17 + 25 = 42" fails exact match on all 13 arithmetic cases |
| llm-eval-harness, "final answer only" system prompt | 53/55 (96%) | Ran on the suite before two prompts were fixed; rerun pending a quota reset |
| sqlite-mcp-explorer text-to-SQL benchmark | 53/53 (100%) | Small, easy benchmark: shows the pipeline works, does not rank models; one question was reworded after a 98% first run |

The judged cases are graded by the same model. The agents in k8s-manifest-guardrail and depwatch-mcp each ran live once on Gemini (single runs, free tier). The Claude path has not been run live, and in the Kubernetes run the first draft passed, so the repair loop was not observed live. Details are in each repo's README.

## Stack

Python · Model Context Protocol · Anthropic API (tool use) · OpenAI-compatible APIs (Ollama, vLLM) · SQLite · Starlette · pytest · ruff · Docker · GitHub Actions

## How I work

- Every claim in a README is backed by a test or a live run, and each repo lists its limitations.
- Agent loops are tested against scripted fake models, so CI needs no API key and never flakes on model output.
- Demo "models" that are not real LLMs are labelled as such.
