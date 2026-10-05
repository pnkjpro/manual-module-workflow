# <Module name> — Implementation Plan <version>

> Copy to plans/implementation-plan.v1.md for the first plan. Replace placeholders. This document starts as Draft. Preserve every approved version when creating the next version.

## 1. Identity and approval

| Field | Value |
|---|---|
| Module ID | <module-id> |
| Plan version / status | <v1 / Draft, Proposed, Approved; supersession is tracked in ledger> |
| Created / last proposed date | <date> |
| Human developer / approver | <name> |
| Approval record | <explicit approval reference and date, or Pending> |
| Supersedes | <none for v1; previous version otherwise> |
| Approved change records | <none or CR IDs and paths> |
| Repository / branch | <verified path and branch> |
| Module starting commit | <actual full SHA before module work, or Not recorded yet> |
| Current approved plan pointer | <phase-ledger.md; populated only after approval> |

Record this plan's committed snapshot in the ledger after committing it. Do not try to put a commit's own hash inside the content of that same commit.

## 2. Problem and success

**Problem:** <concrete behavior or limitation today>

**Desired result:** <observable behavior after this module exists>

**Example scenario:** Given <starting state>, when <trigger>, then <expected result>.

**Users / callers:** <who or what depends on this behavior>

**Success measures:** <observable outcomes; numbers only if justified>

## 3. Boundaries

| Area | In scope | Out of scope / delegated to |
|---|---|---|
| Business behavior | <responsibilities> | <exclusions or owner> |
| Inputs / outputs | <owned interfaces> | <related external interfaces> |
| State / persistence | <owned data and transitions> | <other components' data> |
| Integration / configuration | <required changes> | <separate deployment or modules> |

**Compatibility constraints:** <existing callers, data formats, versions, migrations>

**Operational constraints:** <latency, load, availability, resource limits if relevant>

**Non-goals:** <specific capabilities deliberately excluded>

## 4. Unknowns and design decisions

| ID | Question / assumption | Evidence / options | Decision and reason | Owner / when needed |
|---|---|---|---|---|
| D-001 | <design decision> | <alternatives and tradeoffs> | <decision or Pending> | <owner / phase> |
| U-001 | <unknown external contract> | <what needs checking> | <Pending / verified fact> | <owner / phase> |

A prerequisite uncertainty must be resolved before its dependent phase is Ready. Do not convert an assumption into a confirmed fact.

## 5. Requirements and invariant behavior

An invariant is behavior that must remain true across all relevant paths, such as ownership rules or an allowed state transition.

| Requirement ID | Intended behavior / invariant | Why it matters | Due phase | Acceptance criterion IDs |
|---|---|---|---|---|
| R-001 | <observable obligation> | <reason> | P-01 | P-01-AC-01 |
| R-002 | <observable obligation> | <reason> | P-02 | P-02-AC-01 |
| R-003 | <observable obligation> | <reason> | <phase> | <criterion IDs> |

State required behaviors explicitly. “Robust,” “scalable,” and “production-ready” need concrete criteria.

## 6. Architecture and concepts

| Component / boundary | Responsibility | Inputs → outputs | Collaborators | Concept to understand |
|---|---|---|---|---|
| <component> | <what it owns> | <contract> | <calls / dependencies> | <concept and why used> |

**Main flow:** <trigger → validation → core behavior → state/effect → result>

**Failure flow:** <what happens when an important step fails; who observes or recovers>

**State transitions:** <states and allowed transitions, or Not applicable with reason>

**Dependency direction:** <which components may depend on which; rationale>

**Alternatives rejected:** <important tradeoffs; do not add needless abstractions>

## 7. Phase map

Use the smallest useful phases. Keep IDs stable when adding or reordering phases; record execution order separately.

| Order | Phase ID | Outcome | Requirement IDs | Depends on | Planned verification |
|---|---|---|---|---|---|
| 1 | P-01 | <independently understandable outcome> | R-001 | <none / decision> | <checks> |
| 2 | P-02 | <next outcome> | R-002 | P-01 | <checks> |

The ledger records progress. This plan records intended obligations.

## 8. Phase specification — repeat for each phase

### P-<ID>: <phase name>

**Goal:** <behavior delivered>

**Applicable requirements:** <IDs>

**Prerequisites:** <accepted phases, decisions, contracts, fixtures, environment>

**Concepts before coding:** <concepts, explanations, and design reasons>

**Relevant components / likely locations:** <responsibilities and paths if known; paths are guidance unless the boundary itself is a requirement>

**Manual coding steps:**

1. <One coherent task. Explain what to create and why, without implementation code.>
2. <Next task and its connection to the previous one.>
3. <Next task.>

**Deliberately deferred:** <work scheduled for later phases; identify its due phase>

**Acceptance criteria:**

| Criterion ID | Classification | Due phase / acceptance point | Given / when | Observable expected result | Evidence needed |
|---|---|---|---|---|---|
| P-01-AC-01 | Required | P-01 acceptance | <state / trigger> | <result> | <inspection, test, or demonstration> |
| P-01-AC-02 | Required | P-01 acceptance | <important failure input> | <failure and state/effect behavior> | <evidence> |

Classify criteria as Required or Advisory. Required criteria block acceptance when their due point arrives. Advisory checks can yield nonblocking findings with recorded disposition. Evidence may be deferred to final module acceptance only if the approved plan explicitly assigns that due point and permits earlier phase progression; record the limitation. A verifier cannot change a required due criterion to Advisory or move its due point.

**Likely missing building blocks:**

| Building block | Why needed | If absent / wrong | Affected callers, data, or operations |
|---|---|---|---|
| <phase-specific item> | <causal reason> | <failure path> | <bounded impact> |

**Suggested commit grouping:** <one or more coherent commits mapped to this phase; titles are suggestions, actual IDs go in the ledger>

**Exit criteria:** All required acceptance criteria due for this phase have their specified evidence at the recorded snapshot; related findings and unapproved deviations are resolved; you explicitly accept any residual limitation.

## 9. Cross-cutting behavior

Assess relevance; mark Not applicable with a reason rather than adding every item to every module.

| Concern | Required behavior or justified Not applicable | Due phase / criterion |
|---|---|---|
| Input validation and contract errors | <behavior> | <IDs> |
| Identity / authorization / data ownership | <behavior> | <IDs> |
| Duplicate requests / retries / idempotency | <behavior> | <IDs> |
| Concurrency / atomicity / partial failure | <behavior> | <IDs> |
| Timeout / retry limits / dependency failures | <behavior> | <IDs> |
| Configuration / startup / defaults | <behavior> | <IDs> |
| Logging / metrics / sensitive information | <behavior> | <IDs> |
| Data compatibility / migration / recovery | <behavior> | <IDs> |
| Performance / capacity | <behavior> | <IDs> |
| Integration / end-to-end behavior | <behavior> | <IDs> |

## 10. Final module acceptance

- <Final integration scenarios and expected behavior>
- <Regression checks for affected existing callers and data>
- <Required operational or recovery demonstrations, if relevant>
- <Documentation or interface examples needed by users of the module>
- <Residual limitations that require explicit acceptance>
- <All requirements due at completion; review exact final code and approved plan snapshots>

## 11. Revision history

| Version | Change record | Summary | Approval record | Effect on previous work |
|---|---|---|---|---|
| v1 | None | Original approved baseline | <Pending / reference> | <module starting state> |
| <v2> | <CR-001> | <change> | <Pending / reference> | <affected phases / reconciliation record> |

Preserve every approved plan file unchanged. Record supersession in the ledger and newer plan, not by editing a historical plan's status. Add revision-history rows to the new version only. Use a revision record and a new plan version for changed scope, contracts, architecture obligations, or acceptance criteria.

