---
name: prompt-author
description: Write a reusable prompt from scratch for an assistant, coding agent, tool-using agent, or structured-output workflow. Use when the user has no existing prompt or when the current prompt is too weak to salvage. Do not use for small edits to an existing prompt when a targeted rewrite is more appropriate.
---

## Purpose

Generate a production-usable prompt artifact from a normalized brief or raw request.

## Core principle

Write the shortest prompt that still makes the model reliable. Do not add decorative prose, redundant constraints, or generic "be smart" filler.

## Reliability rules

1. Put the highest-priority instructions, constraints, and output rules before lower-priority guidance.
2. Separate instructions from bulk context, examples, and user-provided data with explicit headings or tags.
3. State what counts as trusted context, what counts as untrusted input, and what to do when the answer is missing from the provided material.
4. Use structured outputs or tool schemas for hard guarantees; use prompt prose for semantics, prioritization, and ambiguity handling.
5. Add examples only when zero-shot instructions are insufficient or when format or style drift is a known failure mode.
6. Keep the prompt modular enough that later editors can modify one block without rewriting the rest.

## Workflow

1. Identify the prompt class:
   - direct answering
   - extraction/classification
   - long-context synthesis
   - coding agent
   - tool-using agent
   - structured-output generation
2. Decide the control surface:
   - no tools, optional tools, or required tools
   - freeform answer, reusable template, JSON schema, or tool call
   - zero-shot or few-shot
3. Build the prompt in ordered blocks:
   - role / identity
   - objective
   - truth boundary / context handling rules
   - task instructions
   - constraints
   - output contract
   - tool-use rules (only if relevant)
   - verification / completeness loop (only if relevant)
   - examples (only if zero-shot is insufficient)
4. Prefer explicit contracts over vibes:
   - define what success looks like
   - define what counts as insufficient information
   - define how ambiguity should be handled
   - define the exact output structure
5. Keep examples tightly aligned with the written instructions. Every example should either teach a pattern or be removed.
6. If the task needs guaranteed JSON or tool arguments, recommend structured outputs or a tool schema instead of relying only on prose.
7. If the target model family is a reasoning family, prefer lightweight planning or self-check instructions over requests for full hidden reasoning transcripts.
8. If the task is long-context, place the bulk context before the final action request and use a clear transition such as `Based on the context above`.
9. If the prompt will be reused across providers or model families, keep provider-specific tactics isolated in notes rather than mixing them into universal instructions.

Read [references/prompt-patterns.md](references/prompt-patterns.md) when the task involves long context, structured outputs, few-shot examples, or model-family migration.

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
Provide 5-10 high-value test cases covering happy path, edge cases, ambiguous input, missing data, and format compliance.

## Quality gates

Before finalizing, check:

- Is the scope explicit?
- Are critical instructions placed before examples or background context?
- Is trusted vs untrusted context separated?
- Is the output contract precise?
- Are contradictions removed?
- Are examples consistent with the rules?
- Is the prompt shorter than it was before abstraction or filler was added?
- Are tool rules explicit about when tools are optional, required, or forbidden?
- Does the prompt specify what to do when data is missing or incompatible?
- If hard structure matters, should a schema or tool interface carry more of the burden?

## Definition of done

The prompt is ready to paste into a real agent or application with only placeholder substitution.
