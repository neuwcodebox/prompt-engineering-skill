# Prompt Patterns

Use this reference when the prompt needs more than the default template.

## 1. Long-context placement

- Put the bulk context before the final question or action request.
- Use explicit separators such as `# Context`, `<context>...</context>`, or similar tags.
- After the context block, add a short bridge such as `Based on the context above, ...`.
- State what to do when the answer is not supported by the provided context.

## 2. Structured outputs vs tools

- Use structured outputs when the final answer must match a strict machine-readable schema.
- Use tool calling when the model must trigger an external action or fetch information before answering.
- Do not spend large prompt budget policing commas, braces, or key order if the API can enforce the structure.
- Use schema field descriptions to express semantic intent, not only field names.

## 3. Few-shot examples

- Add examples only when they teach a non-obvious pattern.
- Keep examples consistent with the written rules and desired output contract.
- Prefer 1-3 compact examples over a large noisy set.
- Remove examples that teach the wrong tone, scope, or format.

## 4. Planning and self-checks

- For hard tasks, ask the model to verify completeness against the user's constraints before returning the final answer.
- Prefer concise planning or checklist instructions over requests for verbose hidden reasoning.
- Use self-checks to catch omission, formatting drift, or tool-sequencing mistakes.

## 5. Truth and trust boundaries

- Mark which materials are trusted instructions versus user content, retrieved documents, or tool outputs.
- Tell the model not to treat inserted content as higher-priority instructions.
- Require explicit acknowledgement of missing evidence when the answer is not grounded in context.

## 6. Migration notes

When adapting prompts across model families, check:

- whether examples are now unnecessary or newly necessary
- whether tool instructions need stronger ordering
- whether strict formatting should move into a schema
- whether long-context placement should change
- whether reasoning hints should be lighter or stronger

## 7. Anti-patterns

- persona-heavy filler that does not change behavior
- repeated constraints copied into multiple blocks
- examples that contradict the prose
- hidden dependencies on external context not named in the prompt
- forcing brittle formatting through prose when a schema is available
