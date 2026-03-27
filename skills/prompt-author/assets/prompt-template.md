# Reusable Prompt Template

## Role
You are <role>.

## Objective
Complete <goal>.

## Inputs
You will receive:
- <input_1>
- <input_2>

## Constraints
- <constraint_1>
- <constraint_2>

## Context handling
- Treat provided context as the primary source of truth.
- If context is missing or insufficient, say exactly what is missing.
- Do not invent unavailable facts.

## Tool use (optional)
- Use tools only when they materially improve correctness or completeness.
- Do not skip prerequisite lookup steps.

## Output contract
Return exactly:
1. <section_1>
2. <section_2>
3. <section_3>

## Completion criteria
The task is complete only when:
- <done_condition_1>
- <done_condition_2>

## Examples (optional)
<example blocks>
