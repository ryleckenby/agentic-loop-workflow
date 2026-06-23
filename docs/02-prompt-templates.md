# Prompt Templates

Generic "write good prompts" advice isn't that useful. These are the actual structures I reuse across tasks. Swap in real specifics for your own work.

## Feature implementation

```
Context: [what system/service this touches, e.g. "ASP.NET Core API, Azure SQL backend"]
Existing pattern: [point to a similar piece of code already in the repo to match conventions]
Task: [the single layer you want — e.g. "implement the repository method for X, not the controller yet"]
Constraints: [things it must not break — existing interface, naming conventions, null-handling style]
Required: include unit tests for [specific edge cases you already know matter]
```

Why this works: pointing at an existing pattern stops the model from inventing a new style. Asking for one layer at a time keeps the diff reviewable.

## Bug fix

```
Symptom: [exact observed behavior, including error message/stack trace if there is one]
Expected behavior: [what should happen instead]
Suspected area: [file/class/method, if you have a hypothesis — don't withhold this to "test" the model]
Do not: [anything off-limits, e.g. "don't change the public method signature"]
```

Why this works: AI tools are good at narrow, well-described bugs and bad at "something's wrong somewhere in this service," so the more precisely you can describe the symptom, the less time gets wasted.

## Code review / second opinion

```
Review this diff for:
1. Logic errors against this requirement: [paste the requirement, not just the code]
2. Edge cases: nulls, empty collections, concurrency, [anything specific to this domain]
3. Whether it matches the existing conventions in [reference file/pattern]
Flag anything you're not confident about rather than guessing.
```

I use this as a second pass after my own review, with a different tool than the one that wrote the code (e.g. Code Rabbit reviewing something Cursor drafted) — different tools catch different classes of mistakes.

## Refactor

```
Goal: [what should be true after the refactor that isn't true now]
Preserve: [behavior/tests that must still pass unchanged]
Scope: [explicitly limit — e.g. "this file only, don't touch callers"]
```

Refactors are where I'm most conservative with AI scope, because "improving" code silently expanding into ten files is the single most common way an AI-assisted change turns into a mess.
