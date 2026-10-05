# Git Guide for Manual Module Development

Git records your implementation history. The plan and ledger explain what that history was intended to deliver.

These are command examples for you to run in your actual repository. Replace every ALL_CAPS placeholder first. This pack has not executed them against a module repository.

## 1. Establish the starting point — inspection

```text
git status --short --branch --untracked-files=all
git rev-parse HEAD
git log -5 --oneline
```

Record the actual repository, branch, full starting SHA, and pre-existing changes. Do not assign unrelated existing changes to this module.

If you want a separate branch, create it manually from the agreed starting state:

```text
git switch -c module/MODULE_ID
```

This changes your active branch. A separate branch is a convention, not evidence that the checkout has no pre-existing changes.

## 2. Commit the approved plan — changes made by you

After approving the plan, stage only its intended documents:

```text
git add -- "docs/modules/MODULE_ID/plans/implementation-plan.v1.md"
git diff --cached
git commit -m "docs(MODULE_ID): approve implementation plan v1"
git rev-parse HEAD
```

Staging selects content for the next commit; committing records it. Review all staged content, including anything staged earlier, before committing. Add shared rules or other documents explicitly if they belong in this commit.

Record the resulting plan commit in the ledger afterward. A plan file does not need to contain its own commit SHA.

## 3. Commit coherent pieces of a phase — changes made by you

Review the working and staged changes:

```text
git diff
git diff --cached
git status --short --untracked-files=all
```

Select the actual files you want to include, then commit:

```text
git add -- "path/to/changed-file" "path/to/another-file"
git diff --cached
git commit -m "feat(MODULE_ID): P-01 define module contracts [plan v1]"
git rev-parse HEAD
```

Commit titles should name the phase and intent. They help navigation; reviewers inspect the contents.

One phase may have several commits. When a commit affects several phases, the tracker maps it to each affected requirement and records any work outside the current review. Closing one phase does not close all phases named by that commit.

Prefer separate commits for unrelated changes. Suggested correction title:

```text
fix(MODULE_ID): P-02 address F-001 duplicate handling [plan v2]
```

## 4. Identify the exact review target — inspection

Record full commit IDs for the phase base and reviewed head. Verify the history relationship:

```text
git merge-base --is-ancestor PHASE_BASE REVIEW_HEAD
git log --reverse --format="%H %s" PHASE_BASE..REVIEW_HEAD
git diff --name-status PHASE_BASE REVIEW_HEAD --
git diff PHASE_BASE REVIEW_HEAD --
git diff MODULE_BASE REVIEW_HEAD --
```

The ancestry check returns 0 when the base is an ancestor; otherwise resolve the intended comparison before treating it as a simple phase progression.

The log selects commits reachable from the head but not the base. The two-endpoint diff compares the resulting snapshots; it does not list every intermediate change. Use both history and snapshot inspection, plus relevant source at the reviewed head. Inspect cumulative module behavior as well as phase changes.

Start with repository-wide changed paths to detect work outside expected files. Narrow the review only after assessing callers, shared configuration, dependencies, and other affected boundaries.

## 5. Separate committed and local work — inspection

```text
git status --short --untracked-files=all
git diff
git diff --cached
git diff HEAD --
```

Plain diff shows unstaged tracked changes; cached diff shows staged changes. Diff against HEAD shows the net tracked local changes. Untracked file contents are absent from those diffs; inspect relevant files separately.

A review of REVIEW_HEAD must not silently use newer local implementation. Human-supplied runtime results must identify which snapshot and environment were tested.

To inspect the committed plan rather than a later local edit:

```text
git show PLAN_COMMIT:docs/modules/MODULE_ID/plans/implementation-plan.v1.md
```

## 6. Track and accept

After each implementation commit, record its actual SHA, phase and requirement IDs, applicable plan version, and observed change in the ledger.

After verification, record the exact plan/code pair, report, open findings, and your acceptance. Keep the implementation SHA distinct from a later ledger-only documentation commit.

## 7. Revise without erasing history

Approve the revision and save the new plan in a new file. Commit the new plan and approved change record manually. Record their actual SHAs, then make new implementation commits for adaptation, replacement, or removal.

The tracker never rewrites history to make the implementation appear to have followed a newer plan from the beginning. Branch renames, squashes, rebases, or cherry-picks require remapping affected IDs and verifying the resulting snapshots; old reports retain their historical references.

## 8. Recovery guidance

If a change proves wrong, first inspect the work and decide how to correct it. Prefer a new corrective commit when preserving this workflow's audit trail. Do not treat destructive reset, clean, or force-push as routine recovery steps.

For each proposed Git mutation, the tracking agent should state: purpose, affected files/history, expected change, and the inspection that will confirm it.

## Sources for command semantics

The distinction between commit selection and snapshot comparison follows the official [git-log](https://git-scm.com/docs/git-log) and [git-diff](https://git-scm.com/docs/git-diff) documentation. The phase IDs, commit-title convention, ledger, and acceptance rules are design choices in this workflow.

