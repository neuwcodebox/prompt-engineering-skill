---
name: prompt-brief-normalizer
description: Normalize a vague prompt request or prompt-related task into a reusable brief. Use when the user wants to create a new prompt, improve an existing prompt, migrate prompts between model families, or diagnose why a prompt is failing. Do not use for executing the underlying business task when no reusable prompt artifact is needed.
---

## Purpose

Turn scattered requirements into a compact, explicit brief that downstream prompt-writing or prompt-editing skills can use reliably.

## What to extract

Produce a normalized brief with these fields:

- `task_type`: one of `new_prompt`, `revise_prompt`, `migrate_prompt`, `debug_prompt`, `agent_prompt`, `tool_prompt`, `structured_output_prompt`
- `target_model_or_family`
- `provider`
- `primary_goal`
- `user_intent`
- `available_context`
- `inputs`
- `constraints`
- `output_contract`
- `tooling_or_schema_requirements`
- `definition_of_done`
- `known_failure_modes`
- `assumptions`
- `open_questions`
- `recommended_next_skill`

## Operating rules

1. Prefer explicit extraction over paraphrase-heavy rewriting.
2. Preserve user language when it encodes constraints or product semantics.
3. Infer missing fields only when the next skill can safely proceed; mark every inference under `assumptions`.
4. Separate facts from assumptions.
5. If the user supplied an existing prompt, parse it into blocks and record which blocks should likely be preserved.
6. If the request implies hard formatting guarantees, note that this likely needs structured outputs or a tool schema rather than prompt-only wording.
7. If the issue sounds like model choice, retrieval quality, tool design, or missing evals rather than prompt wording, say so clearly.

## Output contract

Return exactly these sections:

### Brief
A concise normalized brief in YAML or bullet form.

### Assumptions
Only the assumptions that were necessary to proceed.

### Risks
The top failure risks or missing information.

### Recommended next skill
One of:
- `prompt-author`
- `prompt-editor`
- `prompt-eval`
- `none`

## Definition of done

The result is done when another agent can write or revise the prompt without rereading the original request.
