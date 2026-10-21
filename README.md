# Sai Harsha Vardhan Mylavarapu

**AI / LLM engineer.** I build tool-using agents (MCP + Claude) and the verification layers that make their output trustworthy.

[Portfolio site](https://msharsha565-create.github.io) · [All repositories](https://github.com/msharsha565-create?tab=repositories)

---

## What I build

LLMs are good at drafting and bad at being right. My projects pair an agent with a deterministic check, so the model's output is validated against real data and fixed in a loop before anyone relies on it.

## Projects

### [k8s-manifest-guardrail](https://github.com/msharsha565-create/k8s-manifest-guardrail)
[![CI](https://github.com/msharsha565-create/k8s-manifest-guardrail/actions/workflows/ci.yml/badge.svg)](https://github.com/msharsha565-create/k8s-manifest-guardrail/actions)

A validation gate for LLM-generated Kubernetes manifests, plus an MCP server and a Claude agent that writes a manifest, checks it through MCP, and repairs it until it passes.

- Catches hallucinated `apiVersion`s, missing selectors/containers, privileged containers, unpinned images, missing resource limits
- CLI, Python library, web demo, Docker image, MCP server, optional Claude repair agent
- 17 tests, ruff, CI on Python 3.10-3.12 and a Docker build

### [depwatch-mcp](https://github.com/msharsha565-create/depwatch-mcp)
[![CI](https://github.com/msharsha565-create/depwatch-mcp/actions/workflows/ci.yml/badge.svg)](https://github.com/msharsha565-create/depwatch-mcp/actions)

An MCP server that gives agents live dependency-health data from PyPI and npm, plus an agent that audits a `requirements.txt` and writes an upgrade report.

- Flags outdated, unpinned, stale (2+ years), yanked and unlicensed packages, and packages that do not exist
- Web demo: paste a `requirements.txt`, get a live table
- 12 tests with mocked registries; verified against the real PyPI and npm APIs

## Stack

Python · Model Context Protocol · Anthropic API (tool use) · Starlette · pytest · ruff · Docker · GitHub Actions

## How I work

- Every claim in a README is something the tests or a live run backs up; limitations are listed in each repo.
- Agent loops are tested against scripted fake models, so CI needs no API key and never flakes on model output.
