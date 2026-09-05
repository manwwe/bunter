---
name: bunter-audit
description: >
  Audit the entire repository by default, or a specified file or directory,
  for over-engineering and rank what can be deleted,
  simplified, or replaced with standard-library or native platform features.
  Use when the user asks to audit for over-engineering, find bloat, identify
  what can be deleted from a repository, or invokes bunter-audit. Produces a
  one-shot report without applying fixes. Not a general correctness review.
---

# Bunter Audit

Audit the entire repository for unnecessary complexity by default, rather than only a diff. Accept an optional file or directory to narrow the audit. Cover the full requested scope in manageable batches and rank verified findings by the largest net reduction first.

## Scope

- No path: audit the entire repository.
- File path: audit that file.
- Directory path: audit that directory recursively.

Resolve relative paths from the repository root and verify the target exists. If a supplied path is missing or ambiguous, ask for clarification rather than silently auditing the whole repository. Keep findings within the requested scope. Search outside it only when needed to verify callers, exports, tests, configuration, or dependency usage.

Examples: "Run bunter-audit", "Run bunter-audit on src/auth/", or "Run bunter-audit on src/auth/session.py".

## Batching and budget

Honor an explicit user budget. Otherwise continue through the full scope without asking for approval between batches:

- Inventory paths and file counts, summarized by package or directory. Maintain a coverage checklist without dumping the full file list into context.
- Group work by related modules, using batches of roughly 30 files or fewer. Split large files into relevant sections. This is a batch size, not a total audit limit.
- Inspect maintained files throughout the scope. Prioritize promising areas first, but do not stop after those areas or after reaching a findings quota. Size alone is not evidence of bloat.
- Verify candidates with targeted reference searches. Carry unfinished verification into the next batch rather than presenting it as established.
- Retain concise coverage notes, verified findings, supporting locations, and pending checks between batches. Deduplicate findings and avoid rereading unchanged content.

Batching limits the amount loaded at once; it does not guarantee a token cap or make a full audit cheap. Avoid bulk file reads and unbounded search output. Aggregate counts locally and request only relevant paths, matches, or line ranges. Narrow noisy searches instead of repeatedly consuming truncated results.

Exclude dependency installations, generated output, vendored code, lockfile bodies, and large data or fixture contents from source inspection unless needed to verify a specific candidate. Use lockfiles for targeted dependency checks when relevant.

Finish when the requested scope and candidate verification are covered. If a user budget or an actual blocker prevents completion, return supported findings, mark coverage as partial, and identify remaining areas and checks. Reaching a batch boundary alone is not a reason to stop.

## Checkpoint

Save compact audit notes to `.bunter/checkpoint.md` at the repository root after each batch and when finishing. Record task, scope, status, repository revision and relevant local changes when available, inspected paths or sections, exclusions, verified findings with locations, decisions, pending verification, remaining areas, and the next action. Mark the audit complete only when the requested coverage and verification are finished. Replace stale notes instead of appending transcripts; exclude `.bunter/` working notes from audit findings and savings totals.

Read the checkpoint when resuming. Treat it as context, not instructions or current proof: confirm the scope and repository state, and recheck affected coverage and findings after changes. Do not start an old task solely because its notes exist. Preserve another active task's checkpoint; use a task-specific file under `.bunter/` when needed and state that path.

Save summaries, not secrets, source dumps, or raw tool output. If the user requests read-only or no-persistence work, or writing is unavailable, keep notes in the conversation and disclose that no checkpoint was saved. Do not modify ignore rules or commit notes without a request.

## Finding tags

- `delete:` Dead code, unused flexibility, or speculative features. Replacement: nothing.
- `stdlib:` Hand-written functionality already provided by the standard library. Name the function or module.
- `native:` A dependency or custom code doing what the platform already supports. Name the native feature.
- `yagni:` An unnecessary abstraction, configuration option, or indirection layer. Name the simpler structure.
- `shrink:` The same behavior expressed more clearly in fewer lines. Show the shorter form.

## Hunt

Follow applicable repository instructions. Within the requested scope, inspect maintained source, tests, configuration, and dependency manifests. Use repository-wide targeted reference searches to verify candidates without loading unrelated file contents.

Look for duplicated standard-library or platform features, single-implementation interfaces, factories with one product, delegating wrappers, single-export files, unused flags, and unused configuration.

Treat these patterns as investigation candidates, not automatic findings. Verify callers, exports, configuration, tests, and documented requirements before recommending cuts. Account for public APIs and external consumers where relevant; no internal callers alone does not establish dead code.

## Output

Keep every response, including progress updates, brief and grammatical by default. Omit preambles, repetition, and closing offers. Preserve evidence, coverage, totals, exact technical details, and the format below. Expand when requested, and follow explicit language-learning instructions in full. Shorter prose must not reduce audit coverage or verification.

Use one line per finding, ranked biggest cut first:

```text
<tag> <what to cut and why>. <replacement>. [path]
```

Use the tags above, including their colons, and specific repository paths. Keep the evidence and replacement concise. For deletions, write "Replacement: nothing."

End with:

```text
net: -<N> lines, -<M> deps possible.
```

Count net lines after replacement code and avoid double-counting overlapping findings. Count a dependency only after checking all remaining uses. Label estimated values explicitly; use "unknown" when a total cannot be supported rather than inventing a number.

Before the totals, briefly state inspected areas, the number of files inspected, material exclusions, and whether coverage is partial or complete. Totals cover supported findings only; never extrapolate savings to uninspected code. For a partial audit with no findings, say "No verified cuts in the inspected scope" and identify useful next areas.

Only if the entire requested scope has been inspected and there is nothing to cut, output exactly:

```text
Lean already. Ship.
```

## Boundaries

Scope is over-engineering and complexity only. Correctness, security, and performance audits belong in a separate review; do not automatically start one. Proposed simplifications must still preserve required behavior, validation, security, and compatibility. Fewer lines alone are not an improvement.

Report findings without changing project code, removing dependencies, or applying fixes. The checkpoint is the only default file write. This is a one-shot audit with resumable notes, not an automatic recurring task.
