# Manual Module Development Brain
## A reusable workflow for coding every line yourself

You write the implementation and tests. Agents help you design the module, understand each step, track commits, verify behavior, and revise the plan when new information changes the design.

**Working agreement:** “Do not implement this module for me. Help me plan it, understand it, code it manually, and verify it against the approved plan.”

## Start here

1. Copy this folder into your repository under `docs/modules/<module-id>/`. These are ordinary Markdown documents and reusable agent prompts; copying them does not install or start agents.
2. Fill in the module brief in [implementation-plan.template.md](templates/implementation-plan.template.md).
3. Give the planning agent the brief, [agent-rules.md](agent-rules.md), and relevant repository context. Have it draft a module-specific plan.
4. Review the assumptions, boundaries, acceptance criteria, and phases. Once you approve it, save it as `plans/implementation-plan.v1.md` and commit it manually. Record its actual commit in the phase ledger.
5. Copy the ledger template to `phase-ledger.md`. Set its current approved plan to v1 and record the module's starting commit.
6. Code one phase manually. Ask the mentor for explanations one step at a time whenever needed.
7. Commit coherent pieces of the phase. Ask the Git tracker to map the actual commits to requirements and phase IDs.
8. When the phase is ready, ask the verifier to review an explicit base commit, head commit, and approved plan snapshot.
9. Correct findings manually, commit the fixes, and request another review. Accept the phase only when the required evidence is complete.
10. If the plan changes, use a revision record before implementing the changed scope. Preserve v1, approve v2, and reconcile the earlier commits.

Use [kickoff-prompt.md](kickoff-prompt.md) as the first message for a future module.

## The agent roles

| Role | Main responsibility | Output |
|---|---|---|
| [Module planner](agents/module-planner-agent.md) | Convert the brief into architecture, requirements, and small phases | Draft implementation plan |
| [Git tracking agent](agents/git-tracking-agent.md) | Connect actual changes and commits to phases and detect drift | Updated draft ledger and commit guidance |
| [Module verification agent](agents/module-verification-agent.md) | Independently check intended behavior, omissions, deviations, and consequences | Verification report with evidence |
| [Plan revision agent](agents/plan-revision-agent.md) | Assess changes and reconcile them with committed work | Revision proposal and draft next plan |
| [Concept mentor](agents/concept-mentor-agent.md), optional | Explain the next concept and help you reason through your own implementation | One small learning step at a time |

The same assistant can adopt these roles in separate passes. For more independent review, give the verifier a fresh session containing the approved plan, revisions, exact code snapshot, and evidence. Role separation helps avoid rubber-stamping; it does not guarantee correctness.

`git-guide.md` is a shared guide, not an agent. A separate coordinator is unnecessary at first: this document defines the handoffs.

## The central loop

**Approve plan → understand phase → code manually → commit → track → verify → fix → accept phase.**

A phase may need several commits. A commit records work; it does not prove the phase is complete.

Phase states:

- **Draft:** scope or acceptance criteria are still being shaped.
- **Ready:** its applicable plan is approved and prerequisites are satisfied.
- **In progress:** you are implementing it.
- **Ready for verification:** you identify the exact committed snapshot and supply the expected evidence.
- **Changes required:** verification found an unmet obligation or an unapproved deviation.
- **Incomplete:** verification lacks required access, evidence, or resolved decisions.
- **Verified:** the verifier found the applicable criteria satisfied at the recorded snapshot.
- **Closed:** you accepted that result and any explicitly allowed residual issues.
- **Reopened:** a later change affects the phase's contracts, assumptions, or evidence.

An independent phase can continue while another has findings, if the plan's dependencies allow it. A dependent phase waits for its prerequisites.

## What the plan must explain

The plan is both an implementation map and a learning map. Each phase should identify:

- The behavior you intend to create and the requirement IDs it satisfies.
- The concepts you need to understand before writing it.
- The components and responsibilities involved, with reasons for the chosen boundaries.
- Small manual coding tasks, expected interactions, and failure behavior.
- Observable acceptance criteria and how you will demonstrate them.
- What is deliberately scheduled for a later phase.
- The likely consequences of omissions or incorrect behavior.

Avoid arbitrary fixed phase counts. A tiny module might need two phases; a stateful integration might need more. An illustrative sequence is contracts and boundaries, core behavior, integration and failures, then end-to-end and operational validation.

## What verification means

The verifier answers two questions separately:

1. Does the reviewed code satisfy the **currently approved plan** for this phase?
2. Are departures from the **original approved intent** explained by approved revision records?

It compares phase-local changes and the cumulative module behavior, including relevant callers, configuration, persistence, and dependencies. A requirement scheduled for later is recorded as not yet due unless it is already a prerequisite.



Every finding must identify the missing or incorrect building block, expected versus observed behavior, evidence, why it matters, what happens if unresolved, and the causal path to the affected area. Correction advice describes what you should change and why; you still write the code.

Example: “The repeated-request check is absent → a retried request can repeat the write → duplicate records become possible → downstream consumers may act twice.” This is a reasoned impact chain, not a claim that a production incident has occurred.

Use [verification-report.template.md](templates/verification-report.template.md). Static review can support an alignment claim, but runtime behavior remains unverified without suitable evidence.

## Changing direction midway

Preserve the approved v1 plan. Create `changes/CR-001.md` from [plan-revision.template.md](templates/plan-revision.template.md), then draft `plans/implementation-plan.v2.md`.

For every affected requirement, phase, and existing commit, choose a disposition: retain, adapt, replace, or remove. Describe follow-up work and regression evidence. Explicitly identify previously verified phases that need reopening.

After you approve the revision, commit the new plan and revision record manually, update the ledger's current-plan pointer, and code the follow-up changes in new commits. Earlier commits remain historical evidence. Do not amend old history merely to make it resemble the new design.

A proposed revision cannot excuse a failing implementation. An acceptance criterion changes only through an approved revision, with its consequences recorded.

## The documents to keep for each module

Suggested working layout after instantiating the templates:

```text
docs/modules/<module-id>/
  README.md
  agent-rules.md
  git-guide.md
  phase-ledger.md
  plans/
    implementation-plan.v1.md
    implementation-plan.v2.md          (only if an approved revision exists)
  changes/
    CR-001.md
  reviews/
    P-01-review-01.md
    P-01-review-02.md
  agents/
    module-planner-agent.md
    git-tracking-agent.md
    module-verification-agent.md
    plan-revision-agent.md
    concept-mentor-agent.md
```

Use stable IDs: `R-001` for requirements, `P-01` for phases, `P-01-AC-01` for acceptance criteria, `CR-001` for revisions, and `F-001` for findings. Allocate finding IDs across the module ledger so later reports do not collide. Never renumber earlier IDs to hide a change.

## Short handoff prompts

**Plan:** “Act as the module planner. Read the shared rules and my brief. Draft an understandable phased plan with observable acceptance criteria. Explain the design decisions. Do not write implementation code.”

**Track:** “Act as the Git tracking agent. Map the actual commits from <base> to <head> to P-02 and plan v1. Separate unrelated and uncommitted work. Propose ledger updates; do not stage or commit.”

**Verify:** “Act as the module verification agent. Review P-02 against approved plan v1 at <plan-commit:path>, using code base <base> and head <head>. Check cumulative behavior and carry forward open findings. Explain omissions, behavior differences, and their impact. Do not implement fixes.”

**Revise:** “Act as the plan revision agent. Assess this proposed change against v1 and the completed commits. Draft CR-001 and v2. Show what can stay, what needs adaptation, and which phases need another review. Keep the proposal pending until I approve it.”

**Learn:** “Act as the concept mentor. Explain the next task in P-02, why it exists, and how I can check my understanding. Let me write it manually, one step at a time.”

## Completing the module

Use [module-acceptance.template.md](templates/module-acceptance.template.md) to record the final decision.

Close the module only when all due requirements have evidence, blocking findings are resolved, approved revisions are reconciled with actual code, and cumulative integration checks support the final snapshot. Keep any accepted residual limitations explicit, with an owner and follow-up.

This pack defines a workflow. It makes no claims about an existing repository and does not set up automation. See [the worked revision example](examples/revision-example.md) for how the records fit together.

