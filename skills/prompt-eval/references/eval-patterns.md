# Eval Patterns

Use this reference when building a reusable prompt test set.

## 1. Prefer deterministic checks first

- Exact match for labels, enum values, and required fields
- String or regex checks for mandatory phrases
- JSON parsing and schema validation for structured outputs
- Tool-call presence or absence checks when tool behavior is part of the contract

Use rubric or human review only for criteria that cannot be captured reliably in code.

## 2. Cover the real task distribution

Build cases that reflect:

- common production inputs
- edge cases that still matter in practice
- failure cases already observed
- intentionally ambiguous or underspecified requests
- malformed, partial, or conflicting inputs

Do not rely only on polished happy paths.

## 3. Evaluate robustness

If the prompt consumes external or retrieved content, include cases for:

- prompt injection attempts inside the context
- irrelevant but plausible distractors
- missing evidence for the requested answer
- conflicting evidence across multiple sources

## 4. Evaluate long-context behavior

When the prompt depends on large context:

- place key facts deep in the context, not only near the end
- test whether the model follows the final task request instead of earlier distractors
- verify that unsupported claims are rejected when the context does not contain the answer

## 5. Judge-model scoring rules

- Use judge models for coherence, completeness, or style only when deterministic checks are insufficient.
- Give the judge a precise rubric and a constrained output scale.
- Grade the visible answer, not hidden reasoning.
- Spot-check judge reliability before scaling.

## 6. Regression watchlist prompts

Typical recurring failures:

- output shape drifts even when content is mostly correct
- the model answers from prior knowledge instead of provided context
- tool prerequisites are skipped
- ambiguity is resolved by guessing instead of asking or flagging missing data
- examples dominate the task and cause pattern overfitting
