# Worked Example: A Contract Changes After P-01

This is an illustration, not a review of real code. C-001 and C-002 are ledger record IDs; their corresponding Git SHAs would be actual full hashes in a real module.

## Original approved v1

An import module receives provider events.

- R-001: validate the event contract before changing state.
- R-002: process each provider event once; identity is initially defined as event ID.
- P-01: establish the event contract and persistence boundary.
- P-02: implement processing and repeated-event handling.
- P-03: integrate and demonstrate failure behavior.

The human codes P-01 in C-001 and C-002. The verifier checks its committed snapshot and the approved v1 plan, then the human accepts P-01.

## New evidence before P-02

The provider confirms that event IDs are unique only inside a tenant. The original global event-ID assumption is wrong.

The revision agent drafts CR-001. It explains:

“Two tenants may submit the same event ID → a global identity can treat the second tenant's event as already processed → valid work may be skipped → that tenant's downstream state can remain incomplete.”

This is an inferred consequence of the newly confirmed contract, not evidence that an incident occurred.

## Reconciliation proposal

| Existing record | What was built | Disposition under proposed v2 | Required manual work |
|---|---|---|---|
| C-001 / P-01 / R-001 | Event validation boundary | Adapt | Include the required tenant identity in the contract |
| C-002 / P-01 / R-002 | Persistence identity based on event ID | Adapt | Make the identity represent tenant plus event ID |
| P-02, not implemented | Repeated-event handling | Revise future tasks | Use the updated identity consistently |
| P-03, not implemented | Integration checks | Revise future criteria | Demonstrate isolation across tenants and repeat suppression within one tenant |

v2 preserves R-002's stable ID while recording its changed obligation: identity is now tenant plus event ID. Its original wording remains in v1. P-01 is reopened because its accepted contract no longer satisfies the new effective requirement.

If stored data already exists, the revision also assesses compatibility, backfill or migration needs, uniqueness conflicts, and callers relying on the old identity. It does not assume changing a field is sufficient.

## Approval and follow-up

The human explicitly approves CR-001 and v2, commits those documents, and records the actual document SHAs in the ledger. They code the adaptations in new commits C-003 and C-004.

The verifier checks:
1. A repeat of the same tenant/event identity does not repeat the effect.
2. The same event ID from different tenants is processed independently.
3. Invalid or absent tenant identity produces the approved failure behavior.
4. Related callers and any applicable existing data remain compatible.

The old P-01 report stays in history. A new report covers the new committed snapshot and v2. The human accepts the reopened phase only when the new criteria have evidence.

## A useful finding if the adaptation is incomplete

**F-001 — One caller still passes only event ID**

Expected: all lookups use the tenant plus event identity required by R-002@v2.

Observed: the example assumes a remaining caller supplies only event ID; a real report would cite its actual path, lines, and code SHA.

Why it matters: identity must stay consistent across storage and lookup.

Impact chain: caller drops tenant identity → lookup becomes ambiguous across tenants → the module may skip or associate the wrong event → affected tenant state can diverge.

Manual correction direction: carry the tenant identity through that caller's contract and lookup, then demonstrate both cross-tenant isolation and same-tenant duplicate suppression. The human writes the correction.

The verifier labels the issue Changes required if it fails a due criterion. CR-001 remains unreconciled until the affected code and required checks satisfy v2.

