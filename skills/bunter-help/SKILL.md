---
name: bunter-help
description: >
  Show a compact reference for Bunter's skills, scope options, and checkpoint
  behavior. Use when the user invokes bunter-help, asks for Bunter help,
  asks what Bunter can do, or asks how to use its skills. One-shot help only;
  does not start another workflow or change settings.
---

# Bunter Help

Display the compact reference below. Keep natural English and follow explicit language-learning instructions. Answer a question about a specific capability directly instead of displaying the full card unnecessarily.

## Reference card

| Skill | Purpose |
| --- | --- |
| bunter | Understand code, implement focused changes, and review correctness with concise explanations. |
| bunter-review | Review a diff or PR for over-engineering; suggest cuts without applying fixes. |
| bunter-audit | Audit the whole repository, or a specified file or directory, for over-engineering. |
| bunter-triage | Assess PR purpose, scope, evidence, project fit, and duplication before maintainer review. |
| bunter-debt | Collect `bunter:` tradeoff comments from the repository or a specified path. |
| bunter-learn | Learn through short explanations, examples, exercises, and useful Mermaid diagrams. |
| bunter-help | Show this reference. |

Ask by name, for example:

- "Run bunter-review on this PR."
- "Run bunter-audit on src/auth/."
- "Run bunter-debt on src/."
- "Use bunter-learn to explain Redis caching."

Scope defaults: audit and debt cover the repository unless given a file or directory. Review uses a supplied PR or comparison, or staged and unstaged changes when no target is given. Triage needs an identifiable PR, patch, or comparison.

Long audits continue in batches through the requested scope; batching does not cap total token use. Bunter's sustained repository work and audit batches save compact notes in `.bunter/checkpoint.md`, verify them when resuming, and respect read-only or no-persistence requests.

## Accuracy and boundaries

The names above identify skills; examples are natural-language requests, not shell commands. Do not assume a host's slash or mention syntax, that these files are installed, or that a skill is automatically active in every session. Explain host-specific invocation or installation only when requested and verified for that environment.

Bunter currently has no intensity levels, mode flags, default-mode environment variables, auto-update configuration, or benchmark scoreboard. Do not advertise Ponytail's configuration or measurements as Bunter features. Ordinary requests for more detail override the concise default.

If a skill's availability or behavior is uncertain, check the relevant local `SKILL.md` before describing it. Keep this card aligned when skills are added or changed; do not load every implementation just to show help.

Display help only. Do not run the listed workflows, modify settings, install or update anything, or write a checkpoint for this one-shot reference.
