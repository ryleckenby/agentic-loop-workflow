# Agentic Loop Workflow

A practical framework for building software with AI tools (Claude, Claude Code, GitHub Copilot, Cursor, Code Rabbit) without losing engineering judgment in the process.

## Why this exists

Most "I use AI to code" stories stop at "the model wrote it and it worked." That's not engineering, that's luck. After 17+ years building C#/.NET and Azure systems and leading engineering teams, the question I care about isn't *can AI write code* — it's *how do you build a repeatable process around AI assistance that produces code you'd actually ship, with the same rigor you'd expect from a human PR.*

This repo documents the loop I use day to day: how a task goes from idea to AI-assisted draft to reviewed, validated, production-ready code. It's written so another engineer or engineering leader could read it and either adopt the process or poke holes in it.

## What's in here

- [`docs/01-workflow-stages.md`](docs/01-workflow-stages.md) — the loop itself, stage by stage
- [`docs/02-prompt-templates.md`](docs/02-prompt-templates.md) — the actual prompt structures I reuse, not just "good prompting tips"
- [`docs/03-guardrails-and-validation.md`](docs/03-guardrails-and-validation.md) — how I catch AI mistakes before they ship
- [`docs/04-case-study.md`](docs/04-case-study.md) — one task walked through start to finish, including a place the AI got it wrong
- [`examples/`](examples/) — sample prompt chains and review notes

## The short version

1. **Scope it like a human would have to do it.** AI is bad at filling in ambiguity you haven't resolved yourself.
2. **Draft with AI, fast.** Let it produce a first pass — code, tests, docs — without precious attachment to the output.
3. **Review like it's a junior engineer's PR.** Because that's what it is. Trust the structure, verify the logic, never trust the edge cases.
4. **Validate against reality**, not against "it looks right" — run it, test it, check it against the actual system constraints (Azure quotas, existing schemas, team conventions).
5. **Capture what you learned** so the next loop is faster and the prompts get better.

This isn't a productivity hack. It's a discipline — and like any engineering discipline, the value is in the parts that are boring and repeatable, not the parts that feel magical.
