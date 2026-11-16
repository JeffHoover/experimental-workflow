# Change record: <short title>

<!-- Copy this file for a task. Keep entries proportional to the change.
Use "Not applicable" with a short reason where appropriate. Empty sections
are unfinished, not evidence of completion. Use "the user" in rules.
Preserve approved brief versions and append proposed amendments separately.
Reference durable existing evidence instead of duplicating it. -->

## Task and handoff

- Change ID:
- Request or issue:
- Workflow: [AI development workflow](../ai-workflow.md)
- Stage: Investigating / Awaiting brief approval / Implementing / Awaiting decision / Assessing / Awaiting acceptance / Accepted / Released
- Active record path:
- Base revision:
- Candidate revision (including any uncommitted code):
- Completed work:
- Next action:
- Pending user decisions or blockers:

## Repository setup

Reference existing documentation where available.

- Development setup:
- Relevant repository instructions:
- Development permissions and restrictions:
- Known enforcement gaps:
- Release process and approval boundary:

| Required check | Exact command and working directory | Source or purpose |
| --- | --- | --- |
| <test, regression, lint, type check, build, etc.> | <command; directory> | <CI configuration, repository instruction, or change-specific reason> |

## Change brief, version <N>

Status: Draft / Awaiting approval / Approved

### Intended behavior and examples

<Describe what should change. Give representative inputs, conditions, and expected observable outcomes. Use stable behavior labels such as B1 where they make the later mapping easier.>

### Boundaries and failures

<Relevant limits, exceptions, invalid inputs, error behavior, and boundary examples.>

### Behavior to preserve

<Existing behavior and regression expectations that constrain this change. Reference relevant tests and interfaces.>

### Exclusions

<What this change deliberately leaves out.>

### Consequential uncertainties

<Unresolved questions, assumptions, source conflicts, and missing business decisions. Identify behavior or work blocked by each. Include any reason qualified human implementation review may be needed.>

### Investigation sources

| Source | Relevant observation or requirement | Established, proposed, or assumed; conflicts or limits |
| --- | --- | --- |
| <request, documentation, test, code/caller, or targeted execution reference> | <supports which consequential claim> | <classification and limitation> |

### Approval

- Approved by:
- Approved brief version:
- Approval quotation and conversation reference, where available:

The agent must not begin implementation until the user explicitly approves an identified version of the change brief.

## Amendments and stop decisions

<Append only as needed. Do not silently edit the approved brief.>

### Amendment or decision <ID>

- Status: Proposed / Approved / Declined
- Affected approved brief version and behavior:
- Trigger, consequence, and recommended resolution:
- Proposed change to behavior, scope, test expectation, check, or permissions:
- Work paused; unaffected work that may continue:
- User decision, approver, and approval reference:

## Implementation notes

### Test-first evidence

<Briefly identify the behavioral tests run before implementation and the observed expected failures. A compact account is sufficient; no per-cycle log is required. Record any limitation and user-approved alternative.>

### Significant design decisions

<Record consequential choices, their reasons, and maintenance or diagnostic implications. Omit routine implementation details.>

### Known limitations

<Include unresolved problems, existing failures discovered during investigation, and environmental constraints.>

## Fresh assessment

- Fresh reviewer session reference or description:
- Base revision:
- Reviewed candidate revision:
- Review scope and relevant surrounding code:
- Assessment summary and limitations:

| Finding | Code reference | Concrete concern and consequence | Disposition and evidence |
| --- | --- | --- | --- |
| <ID> | <file/location> | <finding> | <fixed; remaining for user decision; or addressed with explanation> |

<If no findings, state that explicitly with the scope examined. This does not establish correctness. Record reassessment of changes made after review.>

## Finished-revision verification

- Verified candidate revision:
- Any uncommitted code included and how identified:
- Environment details relevant to interpreting the results:

| Check | Exact command and working directory | Revision | Result | Evidence or reason not run |
| --- | --- | --- | --- | --- |
| <required check> | <command; directory> | <identifier> | <pass, fail, or not run> | <concise observed result or log reference> |

- Subsequent changes and affected checks rerun:
- Failed or unrun required checks and their consequences:

Recorded results must apply to the candidate presented for acceptance. Verification is incomplete while required checks remain failed or unrun.

## Acceptance summary

### Approved behavior mapped to tests

| Approved behavior or preserved expectation | Behavioral test name and location | Coverage limitation or gap |
| --- | --- | --- |
| <brief/amendment reference> | <test reference> | <none known, or explicit gap> |

### Decision material

- Candidate presented for acceptance:
- Verification summary and reference to results above:
- Significant design decisions and maintenance implications:
- Reviewer findings and unresolved concerns requiring user decision:
- Remaining uncertainties and behavior without executable coverage:
- Qualified human implementation review: Required / Optional / Needs user decision
- Classification reason:
- Human implementation reviewer and outcome, if required:

### User acceptance

- Decision: Pending / Accepted / Changes requested / Declined
- Candidate accepted:
- User decision quotation and reference:
- Explicit decisions on remaining concerns or limitations:

The agent must wait for the user's acceptance decision. Acceptance does not authorize merging or deployment.

## Release handoff

- Prepared commit or PR:
- Accepted revision and revision submitted for release:
- Release authorization: Pending / Explicit user approval / Existing team process
- Approval reference or applicable process evidence:
- Subsequent code changes and assessment/verification references:
- Release outcome, when known:

## Optional rough effort

<!-- Proposed aid, not a required control. Avoid double counting rework under
other stages. Agent elapsed time can overlap human time and is not labor saved. -->

| Activity | Human time | Agent elapsed time | Estimate, measurement, or unknown |
| --- | --- | --- | --- |
| Preparation and brief approval | | | |
| Initial implementation | | | |
| Verification, assessment, and acceptance review | | | |
| Rework | | | |

- Relevant coordination or tool costs, if known:
- Practical observations about burden, diagnosis, or maintenance:
