# AGENTS.md

- This repository is a prompt-engineering skill pack. The default deliverables are prompt artifacts such as system prompts, developer prompts, reusable templates, and prompt eval suites.
- If the user mentions a business task such as news classification, extraction, or summarization, do not treat this repository as the thing that performs that task. Treat it as the thing that helps another agent write, revise, or evaluate the prompt for that task.
- When editing docs, keep the role split aligned with the repository workflow: `prompt-brief-normalizer` normalizes the request, `prompt-author` writes a new prompt, `prompt-editor` revises an existing prompt with minimal deltas, and `prompt-eval` defines eval cases and regression checks.
- Keep artifact boundaries explicit in every skill. Avoid wording that blurs "doing the business task" with "designing the prompt or eval for that task."
- Keep `README.md`, each `SKILL.md`, and the actual files under `assets/` and `references/` consistent with each other.
