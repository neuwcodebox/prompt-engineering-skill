---
name: prompt-brief-normalizer
description: Normalize a vague request, notes dump, or existing prompt into a reusable prompt brief. Use when the user wants to create a new prompt, improve an existing prompt, migrate prompts between model families, or diagnose why a prompt is failing. Do not use for executing the underlying business task when no reusable prompt artifact is needed.
---

## Purpose

Turn scattered requirements into a compact, explicit brief that downstream prompt-writing or prompt-editing skills can use reliably.

## Artifact boundary

- Produce a prompt brief, not the business-task result.
- If the user mentions a domain task such as news classification, define the prompt contract for that task instead of classifying the news.
- Prefer reusable prompt-design language over one-off task advice.

## What to extract

Produce a normalized brief with these fields:

- `task_type`: one of `new_prompt`, `revise_prompt`, `migrate_prompt`, `debug_prompt`, `agent_prompt`, `tool_prompt`, `structured_output_prompt`
- `interaction_pattern`: one of `direct_answer`, `classification`, `extraction`, `tool_using_agent`, `coding_agent`, `long_context_synthesis`, `workflow_orchestrator`
- `prompt_artifact_type`: one of `system_prompt`, `developer_prompt`, `layered_prompt`, `prompt_template`, `tool_schema`, `eval_plan`, `mixed`
- `target_model_or_family`
- `provider`
- `response_mode`: one of `freeform`, `template`, `json_schema`, `tool_call`, `mixed`
- `primary_goal`
- `user_intent`
- `available_context`
- `inputs`
- `trusted_inputs`
- `untrusted_inputs`
- `context_boundaries`
- `constraints`
- `output_contract`
- `tooling_or_schema_requirements`
- `example_strategy`
- `model_fit_notes`
- `preserve_blocks`
- `definition_of_done`
- `known_failure_modes`
- `non_prompt_causes_to_check`
- `eval_need`
- `assumptions`
- `open_questions`

## Operating rules

1. Prefer explicit extraction over paraphrase-heavy rewriting.
2. Preserve user language when it encodes constraints or product semantics.
3. Infer missing fields only when the next skill can safely proceed; mark every inference under `assumptions`.
4. Separate facts from assumptions.
5. If the user supplied an existing prompt, parse it into blocks and record which blocks should likely be preserved.
6. If the request implies hard formatting guarantees, note that this likely needs structured outputs or a tool schema rather than prompt-only wording.
7. Distinguish prompt problems from model choice, retrieval quality, tool design, data quality, or missing evals. If the prompt is not the primary bottleneck, say so clearly.
8. Record where long context should appear relative to the instructions and final task request.
9. Mark whether the prompt must defend against prompt injection or untrusted retrieved content.
10. Flag examples that should be preserved, removed, or rewritten because they no longer match the intended behavior.
11. If the request implies a model-family migration, capture the reason for migration and the behaviors that must remain invariant.

Use [assets/brief-template.md](assets/brief-template.md) when a structured brief template will help the next skill move faster.

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
