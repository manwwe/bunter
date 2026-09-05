# Bunter Help

Show this compact card when asked for general help. For a specific question, answer only that question. Shared Bunter rules apply.

| Workflow | Purpose |
| --- | --- |
| Coding | Understand code, implement focused changes, and review correctness. |
| Review | Find over-engineering in a diff or PR. |
| Audit | Find over-engineering across the repository or a specified path. |
| Triage | Assess PR purpose, scope, evidence, fit, and duplication. |
| Debt | Collect `bunter:` tradeoff comments and missing revisit triggers. |
| Learn | Short explanations, examples, practice, and useful Mermaid diagrams. |
| Help | This reference. |

Examples: "Bunter, audit src/auth/", "Bunter, review this PR for over-engineering", "Bunter, list debt in src/", "Bunter, help me learn Redis caching".

Bunter is one skill. Its entrypoint loads only the supporting workflow needed. These are natural-language requests, not shell commands. Do not assume host-specific invocation syntax or automatic activation.

Audit and debt cover the whole repository unless given a file or directory. Review uses the supplied comparison or staged and unstaged changes. Triage needs an identifiable target. Large audits continue in batches; batching does not cap total token use.

Sustained coding work and audit batches save notes in `.bunter/checkpoint.md` in the target project, unless read-only or no-persistence work is requested. Resuming requires checking notes against current code. Other workflows do not write checkpoints by default.

There are no intensity levels, mode flags, auto-update configuration, or measured-savings scoreboard. Requested detail overrides the concise default. Legacy names such as `bunter-audit` refer to workflows, not separate installed skills.

Display help only. Do not run workflows, change settings, install anything, or save a checkpoint. If behavior is uncertain, read the relevant reference, not every reference.
