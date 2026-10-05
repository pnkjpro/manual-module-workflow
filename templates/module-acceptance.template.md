# <Module> — Final Acceptance Record

**Status:** <Pending / Accepted / Changes required / Incomplete>

Accepted requires every due required criterion to be Pass or Approved N/A, a current Verified cumulative report for the recorded code/plan pair, reconciled approved revisions, no unresolved required failures or unapproved deviations, and explicit human acceptance. Advisory residual findings must have a recorded disposition. Fail, Not verified, and Not yet due cannot satisfy a required criterion at final acceptance.

| Field | Value |
|---|---|
| Final code snapshot | <repository, branch, full SHA> |
| Original approved plan | <v1 commit:path> |
| Final approved plan | <version and commit:path> |
| Approved revisions | <CR IDs and reconciliation evidence> |
| Final cumulative verification report | <report path and committed snapshot if available> |
| Phase closure records | <ledger / report references> |
| Due requirements and criteria | <evidence map; no required Not verified / Not yet due remains> |
| Unresolved findings | <IDs, impact, disposition, owner, and follow-up; None if none> |
| Explicitly accepted residual limitations | <human acceptance reference; not a substitute for unmet required criteria> |
| Relevant local changes after review | <None observed / details and reassessment> |
| Human acceptance | <Pending / record, date, exact scope> |

**Final integration evidence:** <cross-phase contracts, failure paths, affected callers, and regression results>

**Operational or recovery evidence where required:** <checks or approved N/A rationale>

**Next step:** <None for development / remaining work / separate release process>

Module acceptance is a development decision for this snapshot. Deployment and production readiness require their own applicable checks and authorization.

