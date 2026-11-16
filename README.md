# AI Thoughts: provisional AI development workflow

A portable process for delegating software development to AI coding tools while retaining human accountability. The process defines what the agent may do autonomously, when it must stop, and what evidence the user examines before accepting a change.

This is a provisional compromise, not a validated replacement for human implementation review. Fresh agent assessment can surface problems but does not provide independent assurance. No productivity gain is assumed; total effort includes preparation, verification, review, and rework.

## Documents

| File | Purpose |
| --- | --- |
| [Workflow](docs/ai-workflow.md) | Portable rules for authorization, implementation, assessment, acceptance, permissions, and release. |
| [Change-record template](docs/changes/TEMPLATE.md) | One growing record per task, carrying approved scope, decisions, evidence, and handoff state. |

The documents are drafts for review. Their presence does not approve a software change or configure a coding tool's permissions. The workflow is the source of the rules; this README explains how to use it.

## Use in a software repository

1. Copy `docs/ai-workflow.md` and `docs/changes/TEMPLATE.md` into the target repository, preserving their relative paths.
2. Add a pointer to the workflow in each coding tool's repository instructions. Preserve existing project instructions. The snippet below can be used in the instruction entry point supported by the tool.
3. Configure development permissions separately. Exclude production changes, production credentials, and destructive operations outside disposable development resources from standing permissions. Record actual restrictions and gaps.
4. Identify the repository's setup and required checks from existing documentation, scripts, and CI configuration. Record them or link to them in the task's change record.
5. Copy the template to a task-specific file, for example `docs/changes/042-retry-timeout.md`, and provide that path when starting a session.

Repository instruction snippet:

```text
Before working on a software change, read docs/ai-workflow.md and the active
change record identified in the task. Follow the workflow and existing project
instructions. If no active change record exists, create one from
docs/changes/TEMPLATE.md during investigation and identify it to the user.
The agent must not begin implementation until the user explicitly approves
an identified version of the change brief. Keep the record current enough
for another session to continue. Do not infer approval from a populated
template or an unapproved proposal.
```

Tool-specific instruction filenames, permission settings, and approval mechanisms are configured for the installed tool. This repository does not yet supply or verify Codex or Claude Code configurations. Written instructions alone do not enforce access restrictions.

## Run a change

| Stage | Agent work | User involvement |
| --- | --- | --- |
| Investigate and authorize | Inspect relevant sources and draft a brief with examples, boundaries, preserved behavior, exclusions, and uncertainties. | Resolve consequential questions and approve an identified brief version. |
| Implement | Write behavioral tests first, observe expected failures, implement, run regression checks, and refactor within scope. | Decide issues that trigger the stop rules. Routine choices need no approval. |
| Assess and verify | Use a fresh reviewer session; run required checks against the finished revision; record findings and results. | Resolve concerns brought back for decision. |
| Accept | Present tests, behavior mapping, verification, design decisions, findings, and uncertainties. | Personally examine that evidence and decide whether to accept. Arrange qualified implementation review where required. |
| Release | Prepare a commit or PR. | Authorize merging and deployment, or use the team's existing release process. |

The agent must stop affected work for business ambiguity affecting observable behavior, unauthorized changes to test expectations, weakening or disabling checks, or materially broader scope. See the workflow for the complete rules.

## Session starting instructions

Replace bracketed placeholders before use. These prompts reference the workflow rather than replacing it.

### Investigation

```text
Read docs/ai-workflow.md and relevant repository instructions.
Request: [task description or issue reference].
Active change record: [path to existing record, or path to create from template].
Investigate the relevant system and draft the change brief. Identify required
checks and consequential uncertainties. Present the brief for user approval.
Do not begin implementation.
```

### Implementation after approval

```text
Read docs/ai-workflow.md, relevant repository instructions, and [change-record path].
Confirm the record identifies the approved brief and its approval reference.
Implement the approved scope using test first with observed expected failure.
Follow the stop rules. Keep decisions, limitations, and handoff state current.
Prepare the candidate and verification evidence for fresh assessment and user
acceptance. Do not merge or deploy without release authorization.
```

### Fresh assessment

Start a fresh session and provide the record and revisions. It need not inherit the implementation conversation.

```text
Read docs/ai-workflow.md, relevant repository instructions, and [change-record path].
Assess the diff from [base revision] to [candidate revision] and relevant
surrounding code against the approved brief and amendments. Examine behavioral
correctness, readability, design, complexity, error handling, and diagnostic
usefulness. Treat implementation claims and check results as claims to assess,
not sufficient assurance. Record concrete findings with code references,
unresolved concerns, review scope, and the revision reviewed in the change record.
Report findings for disposition before implementation is changed.
```

For continuation in another implementation session, provide the workflow and active record, and direct the agent to resume the recorded next action within approved scope. Missing or conflicting authorization must be resolved with the user.

## Keep the record useful

Fill sections as the task progresses. Keep small changes concise, link to existing evidence, and omit routine implementation narration. Preserve approved brief versions and record amendments separately. Empty fields do not establish completion.

Identify the code being assessed, checked, and accepted unambiguously. A commit hash with no uncommitted code changes is the recommended convention. Code changes after assessment or verification require appropriate reassessment and rerunning affected checks. Distinguish later record-only edits from changes to verified code.

Rough effort tracking is optional. If used, distinguish human time from agent elapsed time and include rework; overlapping durations must not be treated as labor saved.

## What still needs configuring

- The target repository's setup and executable check commands.
- Each tool's instruction entry point and effective permissions.
- The team's merge and deployment authorization process.

There is no application runtime, enforcement automation, or test suite in this document set. Add automation only when it addresses a concrete recurring burden or failure.
