# <Module name> — Phase and Commit Ledger

> Copy to phase-ledger.md. Replace placeholders with observed facts. Keep earlier verification targets and report history.

## Module pointers

| Field | Value |
|---|---|
| Module ID / repository | <ID / path> |
| Branch | <actual branch> |
| Module starting commit | <full SHA> |
| Original approved plan | <v1 path and full plan commit SHA> |
| Current approved plan | <version, path, full plan commit SHA> |
| Approved change records | <CR IDs, paths, committed snapshots> |
| Current working-tree status | <clean / staged / unstaged / untracked; checked at date> |
| Next finding ID | <F-001; allocate IDs across this module> |
| Last updated by / date | <role or human / date> |

## Plan versions

| Version | File | Commit containing approved plan | Approval record | Effective obligations |
|---|---|---|---|---|
| v1 | plans/implementation-plan.v1.md | <full SHA after commit> | <explicit approval / date> | Original baseline |
| <v2> | <path> | <full SHA> | <approval / CR> | <summary of changes> |

## Phase summary

| Phase | Applicable plan | Status | Phase base | Reviewed code head | Commit records | Latest report | Blocking findings / prerequisites | Human acceptance |
|---|---|---|---|---|---|---|---|---|
| P-01 | v1 | <Ready / In progress / ...> | <full SHA> | <full SHA or Not reviewed> | <record IDs> | <path or None> | <IDs or None> | <Pending / reference and date> |

Statuses: Draft, Ready, In progress, Ready for verification, Changes required, Incomplete, Verified, Closed, Reopened.

## Commit records

Record every relevant commit. A phase may have several commits; a commit affecting several phases maps to all of them.

| Record ID | Actual full commit SHA | Phase IDs | Requirement / finding IDs | Plan used while coding | What changed | Scope drift / unrelated changes |
|---|---|---|---|---|---|---|
| C-001 | <actual SHA> | P-01 | R-001 | v1 | <observed change> | <None / explanation> |

Include corrective and integration commits. Do not infer their content from the commit message alone.

## Requirement-to-evidence map

| Requirement / criterion | Current plan version | Implementation locations at reviewed SHA | Commit records | Evidence / report | Result |
|---|---|---|---|---|---|
| R-001 / P-01-AC-01 | v1 | <paths and actual lines / SHA> | C-001 | <report or check> | <Pass / Fail / Not verified / Not yet due / Approved N/A> |

## Verification history

| Report ID / path | Phase / module scope | Plan version + committed path | Code base → head | Verdict | Evidence source | Superseded for current acceptance? |
|---|---|---|---|---|---|---|
| <P-01-review-01> | P-01 | <v1 / SHA:path> | <full SHAs> | <Verified / Changes required / Incomplete> | <inspection / human results / executed checks> | <No / Yes and reason> |

Historical reports remain valid descriptions of their own snapshots. They cannot silently justify a later relevant change.

## Findings carried forward

| Finding | Obligation | Priority / blocks what | Status | Owner | Correction commit | Recheck evidence | Closure / accepted residual record |
|---|---|---|---|---|---|---|---|
| F-001 | <IDs> | <priority / phase> | <Open / Fix committed / Resolved / Residual accepted> | <human> | <SHA or None> | <report or Not yet rechecked> | <Pending / exact record> |

Do not erase findings when a phase advances. “Fix committed” is distinct from “Resolved.”

## Revision reconciliation

| Change record | Affected old commits / phases | Disposition | Follow-up commits | Required rechecks | State |
|---|---|---|---|---|---|
| CR-001 | <actual IDs / P IDs> | <retain / adapt / replace / remove> | <actual IDs or Pending> | <criteria / reports> | <Pending approval / Approved / Reconciled> |

A phase closed under v1 may be reopened under v2. Preserve its original acceptance and record the new obligations.

## Documentation timing

Record a code commit's SHA in a later documentation commit, or keep the ledger draft until you make that commit. A commit cannot reliably contain its own final SHA.

If a ledger-only commit follows a reviewed code commit, record both when useful. Confirm the documentation commit did not change code, configuration, tests, dependencies, or approved criteria before carrying acceptance forward.

## Resume note

**Current phase:** <ID and status>

**Next manual task:** <one concrete task>

**What must be resolved first:** <decisions / findings / evidence>

**Latest reviewed code snapshot and plan:** <full references>

**Unreviewed relevant changes:** <details or None observed>

