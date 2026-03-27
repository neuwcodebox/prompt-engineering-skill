---
name: prompt-eval
description: Create eval cases, scoring rules, and regression tests for a prompt or prompt-based skill. Use after writing or revising prompts, especially before publishing, changing models, or comparing prompt versions. Do not use when the user only wants the prompt text and no quality harness.
---

## Purpose

Turn prompt quality from opinion into measurable checks.

## Evaluation framework

Split checks into five categories:

- task fidelity: did the result solve the real task correctly?
- process compliance: did the model follow required steps or tool rules?
- format or schema compliance: did it return the requested shape exactly?
- robustness: did it handle ambiguity, missing data, conflicts, and hostile context safely?
- efficiency: did it avoid unnecessary steps, verbosity, or retries?

## What to generate

1. Success criteria
2. A compact test set
3. Deterministic checks where possible
4. Rubric-based checks where necessary
5. Regression cases for previously observed failures
6. Notes on what should be checked automatically versus manually

## Test case design rules

Include:
- happy path
- edge case
- ambiguous input
- adversarial or conflicting instruction case
- incomplete or incompatible input case
- strict output-format compliance case
- tool-use prerequisite case (if tools are involved)
- prompt-injection or untrusted-context boundary case (if external content is involved)
- long-context placement case (if the prompt relies on large context windows)
- migration case when comparing model families or prompt versions

Prefer small, focused, must-pass checks over giant impressionistic rubrics.

Read [references/eval-patterns.md](references/eval-patterns.md) when the prompt uses tools, long context, strict schemas, or judge-model scoring.

## Output contract

Return exactly these sections:

### Success criteria
A short, measurable definition of success.

### Eval set
Provide a table or structured list with:
- `id`
- `input`
- `expected_behavior`
- `check_type` (`deterministic`, `rubric`, `human_review`)
- `priority` (`must_pass`, `important`, `nice_to_have`)

### Scoring rules
How each case is graded.

### Regression watchlist
The 3-5 most likely ways this prompt will fail again.

## Definition of done

A teammate can compare two prompt versions and tell which one is better without relying on gut feel alone.
