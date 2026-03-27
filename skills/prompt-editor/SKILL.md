---
name: prompt-editor
description: Diagnose and revise an existing prompt artifact for clarity, reliability, model fit, tool behavior, format compliance, or reduced ambiguity. Use when a prompt already exists and should be improved rather than replaced. Do not use for blank-slate prompt creation unless the original prompt is unsalvageable, and do not use for performing the downstream business task itself.
---

## Purpose

Improve an existing prompt without losing valid constraints, domain language, or proven behaviors.

## Artifact boundary

- Edit the prompt artifact, not the task output the prompt would later produce.
- If the prompt is for a task such as news classification, preserve the label policy and system behavior unless the requested change explicitly alters that contract.
- Prefer the smallest diff that fixes the real reliability problem.

## Editing policy

Default to minimal, high-leverage edits first. Escalate to structural rewrite only when the current prompt is contradictory, underspecified, or misaligned with the target model family.

## Diagnosis checklist

Inspect the prompt for:

- contradictory instructions
- instructions hidden after long background context
- unclear or missing output format
- vague success criteria
- examples that conflict with the written rules
- examples that overfit to a narrow case or teach the wrong pattern
- missing tool-use prerequisites or verification rules
- tool instructions that fail to say whether tool use is optional, required, or forbidden
- prompt blocks in the wrong order
- verbosity or persona instructions that interfere with the task
- reasoning instructions that do not fit the target model family
- hard format requirements that should be schema-enforced instead
- mixed trusted instructions and untrusted inserted content
- missing handling for prompt injection or hostile retrieved content
- missing ambiguity handling
- missing definition of done

## Rewrite policy

1. Preserve good constraints and task-specific language.
2. Remove contradictions, hedging, and mixed signals.
3. Tighten output requirements so compliance is testable.
4. Make action order explicit when tool use or side effects matter.
5. Add examples only if they solve a measured failure mode.
6. When revising for a new model family, state what changed because of the target model's behavior.
7. If the original prompt is too bloated, compress repeated rules into a smaller number of stronger blocks.
8. If the prompt mixes instructions with injected documents or user content, separate them with headings or tags.
9. If format compliance is the real issue, move brittle prose rules into a schema or tool interface recommendation.
10. Keep edits local when possible so the downstream diff is easy to review.
11. If the real gap is missing evaluation coverage rather than prompt wording, say so and hand off concrete cases for `prompt-eval`.

Use [assets/edit-checklist.md](assets/edit-checklist.md) when you need a compact inspection pass before rewriting.

## Output contract

Return exactly these sections:

### Diagnosis
List the most important failure modes in priority order.

### Revised prompt
Provide the improved prompt in full.

### Delta summary
For each major change, show:
- `change`
- `reason`
- `expected effect`

### Regression risks
What might get worse after the rewrite.

### Eval additions
New tests that should be added before shipping the rewrite.

## Definition of done

The revised prompt is measurably clearer, internally consistent, and easier to evaluate than the original.
