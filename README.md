# Prompt Skill Pack

A practical skill pack for coding agents to write, revise, normalize, and evaluate prompts with a structured, test-driven workflow.

## Overview

This repository provides a small set of agent skills for prompt engineering in real-world coding-agent environments.

It is designed for agents that need to:

- write prompts from scratch
- revise existing prompts with minimal, targeted edits
- normalize vague prompt requests into a clear specification
- generate evaluation cases for prompt regression testing

The pack treats prompt engineering as an engineering workflow rather than a writing exercise.  
Instead of optimizing for "nice wording," it focuses on:

- clear task contracts
- explicit constraints
- output guarantees
- failure-mode analysis
- evaluation-driven iteration

## Why this exists

When prompt work is handled ad hoc, several problems appear quickly:

- goals are underspecified
- constraints are mixed with background context
- output format is not truly enforced
- edits become full rewrites even when small fixes would be better
- prompt changes are made without regression tests

This pack breaks the process into reusable skills so an agent can make prompt work more systematic and more reliable.

## Included skills

### 1. `prompt-brief-normalizer`

Turns a vague request, scattered notes, or an existing prompt into a normalized brief.

It extracts and organizes:

- goal
- context
- constraints
- output contract
- definition of done
- likely failure modes

Use this first when the request is ambiguous or the existing prompt is messy.

---

### 2. `prompt-author`

Creates a new prompt from scratch using a structured template.

It is intended for cases where the agent needs to generate a fresh prompt rather than patch an existing one.

Typical output structure includes:

- role or task framing
- objective
- context handling rules
- constraints
- output requirements
- tool-use rules
- completion criteria

---

### 3. `prompt-editor`

Improves an existing prompt with minimal, targeted edits.

It is designed to avoid unnecessary rewrites and instead focuses on diagnosing issues such as:

- contradictory instructions
- missing output requirements
- weak completion criteria
- unclear tool-use rules
- overlong or decorative wording
- examples that do not match the intended behavior

Use this when preserving the original intent matters.

---

### 4. `prompt-eval`

Creates evaluation cases for prompt testing and regression checks.

It helps define test cases across dimensions such as:

- outcome quality
- process compliance
- format correctness
- edge-case handling
- efficiency or unnecessary verbosity

Use this whenever a prompt will be reused, versioned, or deployed.

## Repository structure

```text
skills/
  prompt-brief-normalizer/
    SKILL.md
  prompt-author/
    SKILL.md
    assets/
      prompt-template.md
  prompt-editor/
    SKILL.md
    assets/
      edit-checklist.md
  prompt-eval/
    SKILL.md
    assets/
      eval-template.md
