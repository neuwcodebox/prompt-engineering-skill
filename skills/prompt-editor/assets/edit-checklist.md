# Prompt Edit Checklist

- What is the exact task?
- Which instructions are actually highest priority?
- What should the model return?
- What is forbidden?
- What should happen on ambiguity?
- Which instructions are global vs task-local?
- Are instructions separated from inserted context or retrieved data?
- Are examples aligned with the rules?
- Are examples still necessary?
- Is the prompt forcing unnecessary reasoning style?
- Are output guarantees actually schema or tool problems?
- Are tool rules explicit about prerequisites and ordering?
- Is there any prompt-injection risk from untrusted content?
- Is there a definition of done?
- What test would fail if this prompt regressed?
