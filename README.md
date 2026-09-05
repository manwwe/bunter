<p align="center">
  <img src="assets/bunter-logo.svg" alt="Bunter, a friendly bulldog wearing a bow tie" width="200" height="200">
</p>

# Bunter

A practical coding companion for understanding code, making focused changes, reviewing contributions, and learning new technology.

Bunter is inspired by **Mervyn Bunter**, Lord Peter Wimsey's valet and assistant in Dorothy L. Sayers's detective stories. His observant, methodical approach is the model for this project's personality: read carefully, check the evidence, and help without making a fuss. [About the character](https://en.wikipedia.org/wiki/Mervyn_Bunter).

**Status: first pass, ready for hands-on testing.** Bunter is a collection of Markdown skills. Metadata checks have passed, but real-world behavior and token savings have not been benchmarked.

## Principles

- Understand the problem before changing code.
- Reuse existing code and built-in features when they meet the requirements.
- Prefer maintainable solutions over the fewest possible lines.
- Keep answers short and natural; expand when asked.
- Ground review findings in evidence and preserve necessary checks.
- Respect the user's scope, language preferences, and existing changes.

## Skills

| Skill | Use it for |
| --- | --- |
| [bunter](skills/bunter/SKILL.md) | Everyday coding, explanations, focused fixes, and correctness reviews. |
| [bunter-review](skills/bunter-review/SKILL.md) | Finding over-engineering in a diff or PR. |
| [bunter-audit](skills/bunter-audit/SKILL.md) | Finding unnecessary complexity across a repository, file, or directory. |
| [bunter-triage](skills/bunter-triage/SKILL.md) | Screening PR purpose, scope, evidence, project fit, and duplication. |
| [bunter-debt](skills/bunter-debt/SKILL.md) | Collecting documented tradeoffs and missing revisit triggers. |
| [bunter-learn](skills/bunter-learn/SKILL.md) | Learning through short explanations, exercises, hints, and useful Mermaid diagrams. |
| [bunter-help](skills/bunter-help/SKILL.md) | A compact reference for the available skills. |

## Try it out

For a local trial, give your coding agent the path to the relevant `SKILL.md` and ask it to read and use it. For example, from this checkout:

```text
Read skills/bunter-review/SKILL.md and use it to review my staged and unstaged changes for over-engineering.
```

This repository does not currently include an installer or plugin package. Automatic discovery and invocation syntax depend on your agent; simply cloning the repository does not guarantee that the skills are installed or always active.

Once a skill is available to your agent, requests can be as simple as:

```text
Use Bunter to trace this bug and fix its root cause.
Run bunter-audit on src/auth/.
Run bunter-triage on this PR: <PR URL>.
Run bunter-debt on src/.
Use bunter-learn to help me understand Redis caching.
Show bunter-help.
```

## Review, audit, or triage?

**Review** examines a supplied diff or PR for over-engineering. Without a target, it checks staged and unstaged changes. Findings include locations, proposed replacements, and potential net line reductions.

**Audit** covers the entire repository by default. Supply a file or directory to narrow it. Large scopes run in batches until the requested coverage is complete or an explicit budget or blocker stops the work. Batching reduces the amount loaded at once, not the total cost of a full audit.

**Triage** recommends **ready for review**, **needs clarification**, or **needs changes**. It evaluates the contribution's evidence and value, not suspected AI authorship. Ready for review does not mean ready to merge.

These workflows report findings without applying fixes or publishing feedback. The audit may save its checkpoint. External actions require an explicit request.

## Context and checkpoints

During sustained work, Bunter and Bunter Audit save compact notes in `.bunter/checkpoint.md` in the target repository. Notes cover scope, decisions, inspected areas, verified findings, remaining work, and the next action.

On resume, Bunter checks those notes against the current repository state. Read-only or no-persistence requests disable checkpoint writes. Notes do not automatically restart tasks, change the model, or enlarge the host's context window.

## Track deliberate tradeoffs

Use a `bunter:` comment only for a meaningful limitation accepted under current requirements:

```python
# bunter: loads the entire file into memory; stream if files exceed 100 MB.
```

Choose limits and triggers based on the actual project. `bunter-debt` collects these comments and flags missing limitations, upgrade paths, or revisit triggers. No markers means no recorded debt, not a debt-free codebase.

## Testing this first pass

Start with a small change whose behavior you already understand. Check whether Bunter follows the intended scope, produces useful findings, preserves requirements, and stays concise. For audits, try a small directory before a full repository. Verify that checkpoint notes match completed work.

Keep examples of missed issues, unsupported findings, or unnecessary output so the instructions can improve through actual use. There are no measured savings claims or `bunter-gain` scoreboard yet.

## Inspiration

[Ponytail](https://github.com/DietrichGebert/ponytail) informed the simplicity, audit, and tradeoff-ledger ideas. [Caveman](https://github.com/juliusbrussee/caveman) inspired concise explanatory prose. Bunter keeps natural English and prioritizes required behavior over line-count reduction.
