---
name: prompt-author
description: Write a reusable prompt from scratch for an assistant, coding agent, tool-using agent, or structured-output workflow. Use when the user has no existing prompt or when the current prompt is too weak to salvage. Do not use for small edits to an existing prompt when a targeted rewrite is more appropriate.
---

## Purpose

Generate a production-usable prompt artifact from a normalized brief or raw request.

## Core principle

Write the shortest prompt that still makes the model reliable. Do not add decorative prose, redundant constraints, or generic "be smart" filler.

## Workflow

1. Identify the prompt class:
   - direct answering
   - extraction/classification
   - long-context synthesis
   - coding agent
   - tool-using agent
   - structured-output generation
2. Build the prompt in ordered blocks:
   - role / identity
   - objective
   - context handling rules
   - task instructions
   - constraints
   - output contract
   - tool-use rules (only if relevant)
   - verification / completeness loop (only if relevant)
   - examples (only if zero-shot is insufficient)
3. Prefer explicit contracts over vibes:
   - define what success looks like
   - define what counts as insufficient information
   - define how ambiguity should be handled
   - define the exact output structure
4. Keep examples tightly aligned with the written instructions.
5. If the task needs guaranteed JSON or tool arguments, recommend structured outputs / tool schema instead of relying only on prose.
6. If the target model family is a reasoning family, avoid unnecessary chain-of-thought instructions unless the provider specifically benefits from them.
7. If the task is long-context, separate context from instructions cleanly and place the question / action request after the bulk context.

## Output contract

Return exactly these sections:

### Final prompt
Provide the prompt artifact in the most useful form for the task:
- single system/developer prompt, or
- layered `system` / `developer` / `user` blocks, or
- a reusable template with placeholders.

### Design notes
Briefly explain the design choices block by block.

### Assumptions
List only assumptions that materially shaped the prompt.

### Suggested eval cases
Provide 5–10 high-value test cases covering happy path, edge cases, ambiguous input, and format compliance.

## Quality gates

Before finalizing, check:

- Is the scope explicit?
- Is the output contract precise?
- Are contradictions removed?
- Are examples consistent with the rules?
- Is the prompt shorter than it was before abstraction/filler was added?
- Does the prompt specify what to do when data is missing or incompatible?

## Definition of done

The prompt is ready to paste into a real agent or application with only placeholder substitution.
