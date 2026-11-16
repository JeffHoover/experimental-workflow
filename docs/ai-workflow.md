# Provisional AI software development workflow

Status: Draft for user review. This document consolidates the agreed workflow; creating it does not approve any software change.

## Purpose and limits

The user remains accountable for the software. This workflow provides a provisional basis for accepting outcomes without supervising every development step. It addresses behavioral correctness, implementation quality, affordable maintenance, and diagnosis. It is not an experimentally validated replacement for human review. Agent assessment does not provide independent assurance; agents may share blind spots. No productivity improvement is assumed. Evaluate total effort, including preparation, implementation, verification, human review, and rework.

## Repository setup

Keep this document at `docs/ai-workflow.md`. Create one change record per task from `docs/changes/TEMPLATE.md`. The record grows throughout the task; separate documents for each stage are unnecessary. Tool-specific instruction files must direct the agent to this workflow and the active change record before work begins.

Before implementation, establish the following in the change record or reference existing repository documentation:

- Development setup and required executable check commands, derived from repository instructions, CI configuration, and existing scripts.
- The change's base revision and active change-record path.
- Available development permissions and relevant restrictions or enforcement gaps.
- The applicable release process.

An unavailable command or missing configuration must be reported rather than invented. Resolve missing information when it becomes necessary for the affected work.

## 1. Investigate and authorize

Before drafting the change brief, the agent must investigate the request and the relevant parts of the existing system. Sources include the user request or issue, supplied examples, repository instructions and documentation, existing tests, relevant implementation and callers, and targeted execution when useful and permitted. Investigation must be proportional to the change.

The agent must draft a short brief covering:

- Intended behavior and representative input/output examples.
- Boundaries, exceptions, invalid inputs, and error behavior.
- Existing behavior and regression expectations to preserve.
- Exclusions.
- Consequential uncertainties affecting behavior, scope, or the need for human implementation review.

The brief must distinguish established behavior, proposed behavior, and assumptions. It must reference sources supporting consequential behavioral claims and surface consequential source conflicts. Current implementation demonstrates existing behavior; it does not alone establish intended behavior. Business decisions missing from the sources must be brought to the user. Executable tests are not required for brief approval.

The agent must not begin implementation until the user explicitly approves an identified version of the change brief. The agent must record who approved it, the approved version, and a reference to the approval. A short quotation of the approval message is sufficient; include a conversation reference where available. This is an agent-maintained continuity record, not independently verified proof of approval.

The agent must preserve the approved brief. Proposed amendments must be distinguishable from approved content. If an authorized behavior or boundary changes, the agent must record the proposed amendment and obtain user approval before proceeding with the affected work.

## 2. Implement autonomously within scope

Once the brief is approved, the agent must implement within its authorized scope. Routine implementation choices, debugging, regression checks, and behavior-preserving refactoring do not require user approval.

The agent must write behavioral tests before implementing the behavior they cover and run them to confirm that they fail for the expected reason. It may write several related tests before implementation. The agent must then implement the behavior, run relevant regression checks, and refactor while preserving behavior. Strict red-green-refactor cycles are not required.

Existing regression expectations remain acceptance constraints unless a change is authorized. Behavior-preserving test refactoring is permitted. If a meaningful test-first failure cannot be demonstrated, the agent must report the limitation and obtain a user decision before treating an alternative as satisfying this requirement.

## 3. Stop and ask

The agent must pause the affected work and ask the user when it:

- Encounters business ambiguity affecting observable behavior.
- Needs to change a test's expected behavior beyond what the approved brief authorizes.
- Needs to weaken or disable a check.
- Needs a materially broader change, including an unapproved public API, schema, or dependency change.

The agent must describe the issue, its consequence, and a recommended resolution. It may continue unaffected work within the approved scope. Record approved amendments and their approval references in the change record.

## 4. Assess and verify the finished revision

### Fresh assessment

A fresh agent session must receive the approved brief and amendments, the base and finished revision identifiers, relevant repository instructions and verification commands, and significant design decisions and known limitations. It must inspect the diff and relevant surrounding code for behavioral correctness, readability, design, complexity, error handling, and diagnostic usefulness.

The reviewer must report concrete findings and unresolved concerns with code references and identify the revision reviewed. It must not treat implementation-agent claims or passing checks as sufficient evidence of correctness. A fresh session reduces dependence on the implementation conversation; it does not establish independent assurance.

Record each finding's disposition: fixed, remaining for user decision, or addressed with an explanation. If implementation changes after assessment, the affected changes must be assessed again before acceptance.

### Executable verification

The agent must run required executable checks against the finished revision and record the revision, commands, results, and any failures or checks not run. Required checks must include established project checks and relevant behavioral and regression tests. Additional targeted checks must address a concrete concern.

After subsequent code changes, the agent must rerun checks affected by those changes. Before acceptance, recorded results must apply to the revision presented to the user. The agent must not describe verification as complete while required checks remain failed or unrun.

Use a compact results table with links to longer logs where useful. Retaining every development test run is unnecessary. Clearly distinguish observed results from statements about checks that were not executed.

For a Git repository, a commit hash with no uncommitted code changes is the recommended way to identify the acceptance candidate. If another convention is used, it must unambiguously identify the code assessed and checked, including any uncommitted changes. Later updates solely to the change record must distinguish their own revision from the verified code revision; they do not alone require rerunning code checks.

## 5. Present for acceptance

The agent must present an acceptance summary and wait for the user's acceptance decision. It must contain:

- Approved behavior mapped to test names or locations, including relevant preserved behavior and any approved behavior without executable coverage.
- Verification results and the revision to which they apply.
- Significant design decisions and their maintenance implications.
- Reviewer findings, their dispositions, and unresolved concerns.
- Remaining uncertainties and limitations.
- Whether qualified human implementation review is required, the reason, and its outcome when performed.

The user personally reviews the behavioral tests, behavior-to-test mapping, verification results, significant design decisions, reviewer findings, and remaining uncertainties.

Personal implementation examination is optional for bounded changes following established patterns. Higher-consequence changes, including authorization, sensitive data, irreversible migrations, concurrency, or unfamiliar architecture, require implementation review by the user or another qualified person. The agent must surface uncertain classification to the user. Unresolved reviewer concerns must be brought to the user.

Record the user's acceptance decision and the candidate it concerns. Acceptance does not authorize merging or deployment.

## 6. Prepare and release

The agent may prepare a commit or pull request containing the assessed changes. Merging and deployment require explicit user approval or authorization through the team's existing release process. Acceptance alone does not grant release authorization.

The revision submitted for release must be the accepted revision. Subsequent changes must receive the assessment and verification appropriate to those changes before release. If the release process creates a different combined revision, follow that process's validation requirements and do not claim the earlier checks ran against the combined revision.

## Operating permissions and enforcement

The agent must operate with permissions limited to the authorized development work. Standing permissions must exclude production changes, access to production credentials, and destructive operations outside disposable development resources. When an authorized task requires additional permissions, the agent must explain the specific operation and obtain user approval or follow the team's existing approval process.

These are portable rules. Tool-specific enforcement is configured separately through sandboxing, credential availability, command permissions, branch protection, required checks, merge permissions, and deployment gates. Instructions express boundaries; permissions constrain capabilities. Document actual restrictions and gaps rather than treating written rules as technical enforcement.

## Handoffs and effort

The active change record must make the current stage, approved scope, completed work, and next action clear enough for another session to continue. Do not rely on chat history as the sole source of authorization or task state.

An optional rough effort entry can capture preparation, implementation, verification/review, and rework, including human time and agent elapsed time separately when known. Mark estimates and unknowns. This is a proposed lightweight aid for assessing total effort, not a required timesheet or evidence of productivity gains.
