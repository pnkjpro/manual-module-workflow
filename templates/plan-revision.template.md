# <Module> — Plan Change CR-<ID>

> Copy to changes/CR-001.md. Draft the next plan version separately. This record remains Proposed until the human explicitly approves it.

## 1. Identity and approval

| Field | Value |
|---|---|
| Change ID / status | <CR-001 / Proposed, Approved, Rejected, Implementing, Reconciled> |
| Original baseline | <v1 commit:path> |
| Current approved plan | <version and commit:path> |
| Proposed next plan | <v2 path / Draft> |
| Code snapshot assessed | <actual branch and full SHA; uncommitted work separately> |
| Requested by / date | <human / date> |
| Approval | <Pending / explicit human record, date, and scope> |

## 2. Why the plan needs to change

**Trigger / new evidence:** <changed requirement, confirmed contract, failed assumption, simpler design, or new constraint>

**Current obligation:** <what the approved plan says and why>

**Proposed obligation:** <what changes and why>

**Consequence of keeping the current plan:** <concrete limitation or failure>

**Tradeoffs / alternatives:** <options considered, costs, compatibility, and why proposed direction is preferable>

## 3. Requirement and phase differences

| Item ID | Existing version and wording | Proposed wording / replacement | Reason | Acceptance evidence changed |
|---|---|---|---|---|
| R-001 | <v1 behavior> | <v2 behavior> | <reason> | <old → new checks> |
| P-02 | <existing outcome> | <changed outcome> | <reason> | <criteria> |

Keep IDs stable when the same obligation evolves, and cite its version. If an obligation is replaced or removed, preserve it in the old plan and record its replacement or retirement explicitly. Allocate new phase IDs without renumbering historical phases.

## 4. Reconcile previously committed work

Inspect each affected commit and its cumulative result; a commit title is insufficient evidence.

| Actual commit / phase / requirement | Existing behavior | Disposition | Reason | Follow-up manual work | Required recheck |
|---|---|---|---|---|---|
| <full SHA / P-01 / R-001> | <observed implementation> | <retain / adapt / replace / remove> | <why> | <specific task or None> | <criteria / regression> |

Dispositions:

- **Retain:** still satisfies the new obligations; state why.
- **Adapt:** useful structure or behavior remains, but a specified part changes.
- **Replace:** a different implementation direction must supersede it.
- **Remove:** the behavior is no longer required; assess its callers, data, and configuration before removal.

Use new follow-up commits. Changing the plan does not change the code already committed.

## 5. Impact and verification

| Area | Causal path / concrete impact | Evidence or assumption | Manual work / verification |
|---|---|---|---|
| Earlier phases / contracts | <impact> | <basis> | <recheck> |
| Callers / consumers | <impact> | <basis> | <compatibility check> |
| State / stored data | <impact or N/A reason> | <basis> | <migration / recovery evidence> |
| Configuration / operation | <impact or N/A reason> | <basis> | <checks> |

**Phases to reopen:** <IDs; previous verdicts remain historical>

**Unaffected phases retained as accepted:** <IDs and reason their evidence still applies>

**Open findings:** <carry forward / replaced obligation via approved revision / correction still needed; never silently drop>

**Temporary mixed-version behavior:** <can old and new pieces coexist? what must be coordinated?>

## 6. Draft next plan and coding sequence

- <Update the requirements, architecture, phase specs, and acceptance criteria in the next plan>
- <Put new prerequisites before dependent work>
- <Describe follow-up tasks in the order the human should code them>
- <Update final integration and regression checks>

**Next manual task after approval:** <one concrete task>

## 7. Activation and closure

Before activation: the human reviews the proposed behavior, reconciled earlier work, tradeoffs, and acceptance changes.

After explicit approval:
1. Save the next plan as a new version; preserve older approved versions.
2. Manually commit the new plan and this approved change record.
3. Record actual document commits and update the current-plan pointer in the ledger.
4. Reopen affected phases and implement follow-up work manually.
5. Verify the new code against the new plan and required regression evidence.
6. Mark this revision Reconciled only when the dispositions have been realized in actual code, required rechecks pass, and the human accepts the result.

**Reconciliation evidence:** <follow-up commit IDs, reports, and human acceptance>

A revision can be approved before its coding is complete. Approval establishes the new obligations; Reconciled establishes that earlier and new work now satisfy them.

