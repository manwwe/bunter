---
name: bunter-triage
description: >
  Triage a pull request for contribution value, scope, evidence, project fit,
  and duplication. Use when the user invokes bunter-triage, asks to screen PRs
  for low-quality contributions or PR slop, or wants to assess readiness for
  maintainer review. Recommends next steps without posting comments or closing
  PRs. Not an AI-authorship detector or a full correctness review.
---

# Bunter Triage

Assess the contribution, not the contributor. Keep responses short, grammatical, specific, and respectful. Follow explicit language-learning instructions in full. Do not infer quality from suspected AI authorship, writing style, contributor experience, or PR size alone.

## Gather context

Use the supplied PR, patch, or comparison. If no target is identifiable from context, ask for it. Read applicable repository instructions and contribution guidelines, the PR description and linked issue when available, the diff, relevant surrounding code and tests, and available CI results for the reviewed revision.

Use targeted searches and bounded reads. Check related implementations and accessible issues or PRs when duplication is plausible. If remote context, CI, or search access is unavailable, disclose the limitation rather than guessing. Distinguish checks actually run from results reported by the author or CI. Do not run untrusted PR-provided automation merely to triage it.

## Assess

- Purpose: Identify the problem, expected benefit, and evidence that the change addresses it. A missing issue is not a defect unless the project requires one; documentation and maintenance work can have clear value without a bug report.
- Scope: Identify unrelated churn, unnecessary dependencies, speculative features, or abstractions that materially obscure the change. Verify concerns against project needs rather than flagging patterns automatically.
- Evidence: Compare the claimed behavior with the implementation and relevant tests, reproductions, or documentation checks. Request verification proportional to the change; neither a green CI badge nor a test count proves adequacy. Pending or unavailable checks are not failed checks.
- Fit: Check contribution requirements, compatibility expectations, public interfaces, and established patterns. Cite specific requirements for blockers; keep personal preferences out of the verdict.
- Duplication: Look for existing functionality or overlapping work. Cite the matching code, issue, or PR and explain the overlap. Similar titles alone do not establish duplication; do not claim an exhaustive search unless performed.

Verify each concern against concrete evidence. Do not invent findings to fill categories. Triage is an initial readiness assessment, not a full correctness, security, or performance audit. Mention an obvious consequential defect encountered in scope, but do not silently expand into separate reviews.

## Verdict and output

Lead with one verdict:

- Ready for review: No material triage blockers found; the purpose and supporting evidence are clear enough for substantive maintainer review. This is not approval to merge.
- Needs clarification: Missing or conflicting information prevents a supported assessment. Name the smallest question or evidence request that would resolve it.
- Needs changes: Verified problems with the contribution require a concrete revision. Explain the impact and smallest reasonable next step.

Follow with only the findings needed to support the verdict. For each, include the evidence or location, why it matters, and an actionable next step. Order by impact. If both revisions and questions are needed, use Needs changes and include the unresolved questions.

Finish with a brief coverage or verification limitation only when material. Do not produce a numerical quality score or call a contribution slop in feedback to its author. If no blockers were found, a short verdict with relevant evidence is enough.

## Boundaries

Read and report by default. Do not edit the contribution, publish feedback, submit a review, label or close the PR, or merge it without explicit authorization for that action. Draft feedback in the response when requested. Do not automatically launch bunter-review or a repository-wide audit; recommend a focused follow-up when warranted.
