# Guardrails and Validation

A guardrail, in this workflow, is a rule I've added *after* an AI tool got something wrong — not a theoretical best practice, but a scar turned into a checklist item. The list grows over time; that's the point.

## Standing guardrails

- **Never accept AI-suggested removal of error handling "for clarity."** Models will sometimes simplify code by quietly dropping try/catch blocks or null checks. Every removal gets reviewed line by line.
- **Treat AI-generated tests with suspicion if they were written by the same tool that wrote the code.** A model that misunderstands a requirement will often write a test that confirms its own misunderstanding rather than catching it.
- **Anything touching Azure cost or scaling (queue triggers, autoscale rules, SQL DTU/vCore settings) gets a manual sanity check against actual pricing/limits**, because AI training data skews toward generic cloud advice, not current Azure specifics.
- **Don't let AI tools introduce new third-party packages without an explicit decision.** It's easy for a draft to quietly add a dependency to solve a problem that didn't need one.

## Validation checklist (used every loop)

- [ ] Code runs locally against real (or realistic) data, not just the happy-path example
- [ ] Existing test suite still passes — not just new tests
- [ ] Logic matches the original scope from stage 1, not a "helpful" reinterpretation of it
- [ ] No new dependencies or architectural patterns without a deliberate decision
- [ ] A human (me, or another reviewer) has read every line, not just skimmed the diff summary

## Why this matters for engineering leadership, not just individual output

The reason I treat this as a process worth documenting, rather than a personal habit, is that this is exactly the kind of discipline a team needs as AI-assisted development becomes the default. The risk isn't that AI writes bad code occasionally — it's that teams stop reviewing AI output with the same rigor they'd apply to a junior developer's PR, because it "looks" more polished. A documented loop with guardrails is how you keep velocity gains without quietly eroding code quality.
