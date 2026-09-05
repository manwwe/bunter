---
name: bunter-review
description: >
  Review a diff or pull request for over-engineering: unnecessary abstractions,
  dependencies, dead flexibility, and duplicated standard-library or platform
  functionality. Use when the user requests an over-engineering review of
  changes, asks what can be cut from a diff, or invokes bunter-review.
  Reports suggestions without applying fixes. Not a correctness review or
  a repository-wide audit.
---

# Bunter Review

Review changes for unnecessary complexity. Ground findings in the diff and verify proposed simplifications against surrounding code. Keep every response brief and grammatical, including progress updates. Preserve exact technical details and required evidence; expand when requested and follow explicit language-learning instructions in full.

## Scope

Follow applicable repository instructions. Use the supplied diff, PR, or comparison. If no target is supplied, inspect staged and unstaged changes in the current repository. If there are no changes, ask for a PR or comparison target rather than inventing a base branch or auditing the whole repository.

Read relevant callers, tests, configuration, and documented requirements to verify candidates. Findings must concern changed or directly affected code. Existing unrelated complexity belongs in bunter-audit. Use targeted searches and bounded reads; avoid loading the whole repository.

## Tags

- `delete:` Dead code, unused flexibility, or speculative features. Replacement: nothing.
- `stdlib:` Custom functionality already provided by the standard library. Name the function or module.
- `native:` A dependency or custom code doing what the platform supports. Name the feature.
- `yagni:` An unnecessary abstraction, configuration option, or indirection layer. Name the simpler structure.
- `shrink:` Equivalent behavior expressed more clearly in fewer lines. Show the shorter form.

Treat single implementations, thin wrappers, and shortenable code as candidates, not proof of over-engineering. Check public contracts and external consumers before declaring code unused. Recommend standard-library or native replacements only when their behavior meets the actual requirements.

## Output

Use one line per verified finding, ranked by the largest net reduction first:

```text
<file>:L<line>: <tag> <what to cut and why>. <replacement>.
```

Use exact paths and line numbers from the reviewed version, and include the colon in each tag. For deleted lines, explicitly identify the base version. A tight line range may replace a single line when needed. For a single-file diff, the file prefix may be omitted if unambiguous.

End with:

```text
net: -<N> lines possible.
```

Subtract replacement code and avoid double-counting overlapping suggestions. Label estimates explicitly; use "unknown" when a total cannot be supported. Briefly disclose incomplete coverage or verification before the total. Do not present unverified candidates as findings.

If the review is complete and there are no supported cuts, output exactly:

```text
Lean already. Ship.
```

This means no over-engineering findings, not approval of correctness or readiness to merge. For an incomplete review without findings, say "No verified cuts in the reviewed scope" and state the limitation instead.

## Boundaries

Focus on over-engineering and complexity. Correctness, security, and performance audits belong in a separate review; do not automatically launch one. Suggested cuts must preserve required behavior, validation, error handling, security, accessibility, and compatibility. Do not remove meaningful tests or simplify code solely to reduce line count.

List findings only. Do not apply fixes, publish PR comments, or merge changes. This is a one-shot review, not a persistent mode.
