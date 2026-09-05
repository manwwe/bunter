---
name: bunter-debt
description: >
  Collect bunter: code comments into a ledger of deliberate tradeoffs,
  limitations, and revisit triggers. Use when the user invokes bunter-debt,
  asks what Bunter deferred, or requests its shortcut or debt ledger.
  Accept an optional file or directory; otherwise scan the repository.
  Reports recorded markers, not all technical debt or benchmark savings.
---

# Bunter Debt

Collect documented tradeoffs without modifying code. Keep responses brief and grammatical; preserve exact locations and meaningful details. Expand when requested and follow explicit language-learning instructions in full.

## Scope and scan

Follow applicable repository instructions. Scan the whole repository by default, a supplied file alone, or a supplied directory recursively. Resolve relative paths from the repository root. Ask for clarification if the supplied target is missing or ambiguous; do not silently broaden it.

Start with `rg -n -F 'bunter:'` against the resolved target. Respect ignore rules and exclude `.git`, dependency installations, generated output, and vendored code. If relevant maintained files are ignored, inspect them explicitly and disclose any coverage limits. Narrow or paginate large result sets rather than loading the repository into context.

Inspect enough surrounding syntax to confirm each match is an actual code comment, including block or markup comments where supported. Exclude string literals, documentation examples, and prose merely describing the convention. A text match is only a candidate. Group a multi-line marker into one entry and count each marker once.

The convention is `bunter: <known limitation>; <upgrade path and trigger>`. Preserve the comment's meaning even when an older marker uses a different format. Do not infer missing limits, triggers, or upgrade paths. Do not execute the scanned code.

## Output

Group entries by file, using one line per marker:

```text
<file>:<line>: <tradeoff>. ceiling: <stated limit>. upgrade: <stated action and trigger>. <missing-field tags, if any>
```

Use `not specified` for missing information. Add `no-trigger` when no condition for revisiting is stated, `no-upgrade` when no upgrade action is named, and `no-ceiling` when the limitation is absent. A qualitative condition can be a trigger; do not require an invented numeric threshold.

End with:

```text
<N> markers, <M> with no trigger.
```

If no confirmed markers are found, say "No bunter: markers found in the scanned scope. No recorded debt." This does not establish that the codebase is debt-free. Disclose exclusions or incomplete coverage when material; counts cover confirmed markers only.

If the user explicitly requests authorship, use targeted `git blame` and label it as last-touch authorship, not ownership or responsibility. Leave it out otherwise.

## Boundaries

This is a one-shot ledger, not a persistent mode or a complexity audit. Do not add markers, apply fixes, or calculate hypothetical savings. Report in the response by default. If the user requests a saved ledger, write it to the requested path, or `BUNTER-DEBT.md` in the repository root when no destination is specified. Preserve unrelated content in an existing file.
