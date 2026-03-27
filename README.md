# Prompt Skill Pack

A practical skill pack for coding agents to write, revise, normalize, and evaluate prompts with an explicit, test-driven workflow.

## Overview

This repository packages prompt engineering as a software workflow:

- normalize the request before writing
- author the smallest reliable prompt
- edit existing prompts with minimal deltas
- evaluate every important prompt change

The pack is meant for real agent environments where prompt quality depends on more than wording. It pushes agents to make the contract explicit:

- what the model must do
- what context is trusted
- what is forbidden
- what output is required
- when tools or schemas should replace prose
- how success will be tested

## Design principles

The skills in this repo bias toward the patterns repeated across current official vendor guidance:

- put critical instructions and output rules first
- separate instructions from bulk context and user data
- mark truth boundaries and insufficient-information behavior
- use structured outputs or tool schemas for hard format guarantees
- add examples only when they solve a measured failure mode
- keep prompts short enough to stay legible and debuggable
- treat prompt changes as incomplete until eval coverage exists
- distinguish prompt problems from model, retrieval, tool, or data problems

## Included skills

### 1. `prompt-brief-normalizer`

Turn a vague request, notes dump, or existing prompt into a reusable brief.

It extracts:

- task type and interaction pattern
- model or provider constraints
- trusted vs untrusted context boundaries
- output and tool/schema requirements
- definition of done
- failure modes, assumptions, and next-step recommendation

Use this first when the request is ambiguous or the current prompt is poorly structured.

### 2. `prompt-author`

Write a new prompt from scratch from a normalized brief or raw request.

It emphasizes:

- ordered prompt blocks
- model-fit decisions
- context placement for long inputs
- schema-first thinking for structured outputs
- explicit ambiguity handling and completion criteria

Use this when there is no good existing prompt to preserve.

### 3. `prompt-editor`

Revise an existing prompt with the smallest set of changes that materially improves reliability.

It focuses on:

- contradiction removal
- block ordering
- example alignment
- tool-use and verification rules
- prompt-injection and untrusted-context boundaries
- model-family migration adjustments

Use this when the original prompt has useful intent or domain language worth keeping.

### 4. `prompt-eval`

Create measurable eval cases, scoring rules, and regression checks for prompt changes.

It emphasizes:

- task-distribution coverage
- deterministic checks where possible
- judge-model checks only where needed
- regression cases for known failures
- robustness against ambiguity, missing data, and conflicting instructions

Use this whenever a prompt is reused, shipped, versioned, or migrated.

## Repository structure

```text
skills/
  prompt-brief-normalizer/
    SKILL.md
  prompt-author/
    SKILL.md
    assets/
      prompt-template.md
    references/
      prompt-patterns.md
  prompt-editor/
    SKILL.md
    assets/
      edit-checklist.md
  prompt-eval/
    SKILL.md
    assets/
      eval-template.md
    references/
      eval-patterns.md
```

## References

- OpenAI, Prompt Engineering:
  https://developers.openai.com/api/docs/guides/prompt-engineering
- OpenAI, Structured Outputs:
  https://developers.openai.com/api/docs/guides/structured-outputs
- OpenAI, Using GPT-5.4:
  https://developers.openai.com/api/docs/guides/latest-model
- Anthropic, Claude Prompting Best Practices:
  https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices
- Anthropic, Define Success Criteria and Build Evaluations:
  https://platform.claude.com/docs/en/test-and-evaluate/develop-tests
- Google AI for Developers, Prompt Design Strategies:
  https://ai.google.dev/gemini-api/docs/prompting-strategies
