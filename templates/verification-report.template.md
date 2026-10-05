# <Module> — <Phase or Final Module> Verification <review ID>

> Copy to reviews/<phase>-review-<number>.md. Evaluate actual evidence. A report never creates plan approval or phase acceptance.

## 1. Verdict

**Verdict:** <Verified / Changes required / Incomplete>

**Reason:** <one or two sentences identifying the obligations satisfied or outstanding>

**Human acceptance:** <Pending / explicit acceptance record, date, exact scope and residual issues>

Verified requires all required criteria due for this review to have their specified evidence, no unresolved findings against those obligations, and no unapproved behavior deviation. Advisory findings may remain with recorded disposition. Missing required access or evidence yields Incomplete when no required due failure has been established. An observed failure of a required due obligation or an unapproved behavior deviation yields Changes required even when other evidence is also missing.

Nonblocking issues may remain with explicit disposition. A missing required criterion cannot be waived by calling it nonblocking in this report; changing an obligation requires an approved plan revision.

## 2. Exact review target

| Field | Value |
|---|---|
| Repository / branch | <verified context> |
| Phase IDs / requirement scope | <IDs and why this scope> |
| Original approved plan | <v1 commit:path> |
| Currently approved plan | <version and commit:path> |
| Approved revisions | <CR IDs and commit:path; None if none> |
| Module starting commit | <full SHA> |
| Phase comparison base | <full SHA> |
| Reviewed code head | <full SHA> |
| Relevant commits included | <actual full SHA list / ledger references> |
| Working tree at review | <staged / unstaged / untracked / clean; related files> |
| Source of execution evidence | <human-supplied / agent-executed with authorization / None> |
| Review date / reviewer role | <facts> |

State explicitly whether uncommitted work is excluded. If reviewed, label it separately as a working-tree snapshot with captured evidence; do not attribute it to a commit.

## 3. Plan alignment

### A. Current approved obligations

| Requirement / criterion | Required or advisory / due point | Expected behavior | Evidence at reviewed snapshot | Result | Finding / reason |
|---|---|---|---|---|---|
| <IDs> | <classification and due point from plan> | <behavior> | <actual paths, lines, tests, demonstrations> | <Pass / Fail / Not verified / Not yet due / Approved N/A> | <F-ID / reason> |

“Not yet due” is valid only for a later scheduled obligation that is not a current prerequisite. “Approved N/A” cites its plan rationale.

### B. Departures from original intent

| Original obligation / design | Current behavior or obligation | Change record | Approved? | Reconciliation complete? |
|---|---|---|---|---|
| <v1 ID and behavior> | <what changed> | <CR or None> | <Yes / No / Unknown> | <evidence or outstanding work> |

Evaluate the current plan as effective. Do not fail code merely for an approved change from v1; do fail or flag an unapproved departure.

## 4. Findings — repeat for each actionable issue

### F-<ID>: <specific missing building block or behavior difference>

- **Priority:** <Critical / High / Medium / Low>
- **Blocks:** <phase closure / named downstream phase / final acceptance / advisory only>
- **Obligation:** <requirement ID, criterion ID, plan version>
- **Expected behavior:** <what the plan requires>
- **Observed behavior / omission:** <what the code and evidence establish>
- **Location and evidence:** <actual path, verified lines, commit SHA, and relevant results>
- **Why it matters:** <the design or behavioral reason>
- **If left unresolved:** <concrete failure or limitation>
- **Causal impact chain:** <trigger → behavior → affected state or caller → consequence>
- **Affected area:** <specific callers, records, jobs, interfaces, configuration, or operations>
- **Impact confidence:** <Demonstrated / Inferred with named assumptions / Unknown>
- **Finding confidence:** <High / Medium / Low and why>
- **Manual correction direction:** <what the human should change and why; no implementation patch>
- **How to verify the correction:** <observable scenario and expected result>
- **Status / owner:** <Open / human owner>

Distinguish evidence that a building block is absent from evidence that an adverse event has occurred. Do not invent incidents or quantify impact without a basis.

Priority reflects plausible impact; blocking follows the approved classification and due point. Every required due criterion blocks acceptance if unmet, even if its impact is not Critical.

## 5. Evidence and coverage limits

| Check | Expected result | Actual result | Evidence origin / date | Code and environment covered | Limitation |
|---|---|---|---|---|---|
| <inspection or runtime scenario> | <result> | <observed result / Not run> | <source> | <SHA / configuration / fixtures> | <limits> |

Check relevant happy paths, invalid input, dependency failure, duplicates, partial effects, and integration boundaries according to the plan. Mark irrelevant checks Not applicable with a reason.

Human-supplied logs or test results need a stated code snapshot and environment. If those are unclear, label their coverage uncertain.

**Cumulative behavior assessed:** <earlier phases plus this phase; integration with relevant callers>

**Missing access / evidence:** <what is unavailable and what input would resolve it>

**Unreviewed future work:** <due-later criteria, kept separate from current findings>

## 6. Carry-forward and next steps

| Finding / decision | Present status | Required human action | Recheck target |
|---|---|---|---|
| <existing F-ID> | <open / corrected / resolved / accepted residual> | <task> | <criterion and snapshot> |

**Recommended next manual task:** <smallest useful correction or next phase task>

**Ledger update proposed:** <phase verdict, report pointer, findings, reopening if relevant>

**Freshness condition:** This report covers the recorded plan and code snapshot. Reassess relevant subsequent changes before accepting a newer state. Preserve this report in the history.

