# Daleel — study project

This repo is Youssef's capstone for a 24-week plan to become a senior AI engineer. The full day-by-day plan is in `PLAN.md`; the daily learning log is in `LEARNING.md`.

## What Daleel is

A bilingual Arabic/English assistant that answers questions over a set of public documents, with citations. It grows phase by phase: a tested Python API (Phase 1), an intent classifier (Phase 2), hybrid RAG with a UI (Phase 3), evals and tracing (Phase 4), a tool-using agent and MCP server (Phase 5), then cost, security and deployment work (Phase 6).

## How to help in this repo (learning mode)

The goal is for Youssef to learn, not just to get working code.

- Before starting, ask which plan day he is on, then read that day in `PLAN.md` so your help matches it.
- In Phases 1 and 2 (Days 1–40), explain and review rather than write the code. Give hints, point to the concept, and let him type the solution. Write code only when he explicitly asks.
- From Phase 3 on, you can write more code, but explain each design choice and the trade-off behind it.
- When reviewing code, point out issues and why they matter; let him fix them unless he asks you to.
- Prefer measured decisions: when a choice affects quality (chunk size, embedding model, retrieval method), suggest how to measure it on the eval set.
- At the end of a session, offer to draft 3–5 lines for `LEARNING.md` and a commit message in the form `Day N: <what was done>`.

## Environment

- Windows machine; coding moves into WSL2 (Ubuntu) from Day 1.
- Python 3.12+, uv for packages and environments, Ruff for lint and format, mypy for types, pytest for tests.
- Docker and Docker Compose (Postgres with pgvector from Phase 3).
- Never commit secrets: API keys live in `.env`, which is in `.gitignore`.

## Git

- Personal GitHub account `youssefswilam`; this repo is `youssefswilam/daleel`.
- The remote uses the SSH alias `github-personal` (`git@github-personal:youssefswilam/daleel.git`). Don't change it to `github.com`, or pushes will use the work account.
- The repo-level `user.email` is the personal noreply address. Don't change Git identity settings.
- Line endings are normalized to LF via `.gitattributes`.
- One commit or more per study day, message format `Day N: <what was done>`.

## Code conventions

- `src/` layout, typed code, Pydantic models for data, tests next to every feature.
- Keep functions small and testable; mock LLM calls in tests (fake client from Day 7).
- Arabic text: normalize before keyword search (CAMeL Tools); test with real Arabic examples.
