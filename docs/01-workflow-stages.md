# The Workflow Stages

The loop has five stages. It repeats — output from validation often kicks you back to drafting, and that's by design, not a failure of the process.

## 1. Scope

Before any AI tool sees the task, I write down:
- What the change needs to do, in plain language
- What it must NOT break (existing contracts, schemas, conventions)
- What "done" looks like — tests passing, a specific behavior, a reviewed PR

This step exists because AI tools are confident even when the task is underspecified. If I can't describe the task clearly, the model can't either — it'll just guess, and guess confidently.

## 2. Draft

This is where Claude Code, Copilot, or Cursor actually generates code. A few rules I hold myself to:

- **Small chunks.** I don't ask for an entire feature in one shot. I ask for one layer at a time (data access, then service logic, then API surface) so I can review incrementally instead of facing a 600-line diff.
- **Ask for the boring parts too.** Tests, error handling, logging — these are exactly where AI tools cut corners if you don't explicitly ask.
- **No emotional attachment to the first draft.** If it's wrong, I regenerate or rewrite rather than patching around bad structure.

## 3. Review

I review AI-generated code the same way I'd review a PR from a developer I'm mentoring — with curiosity about their reasoning, not just their syntax. Specifically I check:

- Does the logic match what I scoped, or did the model quietly change the requirements to make its own job easier?
- Are there edge cases (nulls, empty collections, concurrency, Azure throttling/retries) that look handled but aren't actually tested?
- Does it match existing codebase conventions, or does it introduce a new pattern that'll confuse the next person?

## 4. Validate

Review catches things that *look* wrong. Validation catches things that *are* wrong:

- Run it. Every time. AI-generated code that "looks correct" fails more often than code I write myself, because I haven't built the same intuition for its blind spots yet.
- Run the existing test suite, not just new tests for the new code.
- For anything touching Azure resources, check it against real constraints — connection limits, cost, regional behavior — not just the happy path.

## 5. Capture

After the loop closes, I note:
- Where the AI's first draft was wrong, and what kind of prompt would have prevented it
- Any prompt or template worth reusing (see [`02-prompt-templates.md`](02-prompt-templates.md))
- Anything that should become a guardrail (see [`03-guardrails-and-validation.md`](03-guardrails-and-validation.md))

This is the step most people skip, and it's the one that actually makes the next loop faster. Without it you're not building a workflow, you're just chatting with a model every time and starting from zero.
