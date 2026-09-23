# Lesson 2. The method, translated

## The delivery loop

BMad treats AI-driven development as the whole effort: what to build, how it holds together, and how it changes as you learn. A vague notion starts at clarify. A large, clear idea starts at plan. A small change starts at build and verify. Learning loops back to plan.

Four phases produce that loop. Each phase writes documents the next phase loads, so the agent is never asked to invent the previous decision.

| Phase | Name | What it decides | Typical output |
|-------|------|-----------------|----------------|
| 1 | Analysis (optional) | Whether the problem is real and worth planning | Product brief, research notes |
| 2 | Planning | What to build, for whom, and what "good" means | PRD, and a UX spec when a person has to use the result |
| 3 | Solutioning | How it will be built, and the stories that implement it | Architecture with decision records, epics and stories, a readiness gate |
| 4 | Implementation | One story at a time, then review | Story file, code, tests, review, retrospective |

Quick Flow sits beside this path for small, well-understood changes: a short tech spec, then implementation. It skips analysis and solutioning because those decisions already exist in the current system.

## Tracks, chosen by risk

BMad calls this scale-adaptive planning. Depth follows complexity. For GRC work, prefer the risk test over the story-count test. A five-line change that alters what a control proves is not a small change.

| Track | Use it when | Planning shape | GRC examples |
|-------|-------------|----------------|--------------|
| Quick Flow | The requirement is clear, the architecture is unchanged, one person can hold the whole change, and the control's meaning stays the same | `tech-spec` then build | Fix a false positive in a check you already specified. Correct a field the rule already requires. Adjust a threshold an owner already approved. |
| BMad Method | Any of these: the requirement still needs alignment, an architecture choice will shape the code, several components are involved, two agents could implement it differently, or a stakeholder needs the documentation | Brief (optional), PRD, architecture, epics, then stories | Add one control: a fail test, the check, a run, an evidence record, and a catalog entry. |
| Enterprise | Any of these: a regulation or attestation is in play, a security review is mandatory, tenants or data classes must stay isolated, several external systems are involved, or more than one team will maintain it | Method artifacts plus security spec, compliance mapping, integration contracts, and quality gates | A new system enters scope. A workflow that assesses a third party. Anything you will show an assessor as a control, not as a script. |

Enterprise is the honest default when the output is assurance. The method's own examples for that track are HIPAA, PCI-DSS, SOC 2, and government systems. The same test applies to any framework you are attesting to.

You can escalate or shrink mid-flight. A tech spec that uncovers a new data store, a new control interpretation, or a second team becomes input to a PRD. The spec is not wasted.

## Artifacts as the audit trail of the build

Context is the point of the documents. The PRD tells the architect which constraints matter. The architecture tells the implementer which patterns to follow. The story file is the focused packet for one change. `project-context.md` is the constitution: stack, conventions, and rules that every later session inherits.

GRC translation of the same chain:

| BMAD artifact | What you put in it for a GRC change |
|---------------|-------------------------------------|
| Product brief | The obligation, the system, the gap, and what "better" means for the consumer of the evidence |
| PRD | Functional requirements (the condition that must pass and the condition that must fail) and non-functional requirements (evidence format, retention, access, false-pass tolerance, what must never be logged) |
| UX spec | Only when a human reads the output: an auditor, a control owner, a dashboard user. What they need on one screen or in one file to accept the evidence |
| Architecture | Where the control lives (policy check, monitor, workflow, or service), the evidence object, and an architecture decision record for each choice that would be expensive to reverse |
| Epics and stories | Slices that each end in something reviewable: a failing test, a passing test, the run, an evidence record, a catalog entry |
| Readiness check | PASS, CONCERNS, or FAIL before implementation. In this course, FAIL means you cannot name the control, the owner, the fail case, or the evidence location |
| Story file | One change, with acceptance criteria and the technical notes copied from the architecture so the coding agent does not re-decide them |
| `project-context.md` | Frameworks in scope, control ID style, evidence standard, and the forbidden list from lesson 1 |

Fresh context per workflow is part of the method. A long chat that planned the PRD is a bad place to also write the architecture. Load the artifact, start the next role clean.

## Roles, mapped to GRC decisions

The named agents are perspectives, not headcount. One person can wear more than one, as long as the decision is written in the artifact that perspective owns. The failure mode is one chat playing all of them and leaving no record.

| Perspective | Method role | The decision they own in GRC engineering |
|-------------|-------------|------------------------------------------|
| Obligation and scope | Analyst / product manager | Which requirement, which system, what is out of scope, what success looks like for the person who will rely on the evidence |
| Evidence consumer | UX, when the output is read by a person | Whether an auditor or control owner can tell pass from fail without reading the implementation |
| Design and trust boundary | Architect | Where the check runs, what it is allowed to see, what it emits, and which choice is an architecture decision record |
| Slice and sequence | Scrum master | Stories small enough to review, ordered so a failing test exists before a green gate |
| Implementation | Developer | Code and tests that satisfy the story file, without widening it |
| Proof | Test / QA | Pass case, fail case, and the edge that would make a broken control look healthy |

Testing is a perspective that arrives before implementation, in the acceptance criteria, and again after, in review. A control story with only a happy path is not ready.

## Minimum path for a real GRC change

When the work is a new or changed control and Quick Flow does not fit:

1. PRD, with the five questions from lesson 1 answered.
2. Architecture, including where evidence is written and what the check is allowed to access.
3. Epics and stories.
4. Readiness gate.
5. For each story: story file, implementation, review.

Quick Flow is the minimum path only when the five questions are already answered in an existing artifact and this change does not revise them.

## Likely-tested distinctions

| Pair | How to tell them apart |
|------|------------------------|
| Quick Flow vs. BMad Method | Quick Flow keeps an existing control decision and changes the implementation. Method is for a decision that does not yet exist in an artifact. |
| Method vs. Enterprise | Method produces a design you can implement. Enterprise adds the security, compliance, integration, and quality-gate artifacts you will have to show someone outside the build. |
| PRD vs. architecture | The PRD says what must be true and for whom. The architecture says where that truth is enforced and records the expensive choices. |
| Story vs. epic | An epic is a control outcome (the check exists and is cataloged). A story is one reviewable step toward it (the fail test, the check, the run, the mapping). |
| Readiness FAIL vs. a code bug | FAIL happens before implementation, because an artifact is missing. A bug happens after, because the code does not meet the story. |

## Self-check

1. A check flags accounts that are supposed to fail only when the review is older than the interval. The requirement, the owner, and the evidence location are already documented. Which track, and what artifact do you write?
2. You are adding a new requirement as a check, a deliberate fail case, a scheduled run, and a catalog entry. Which track, and why is Quick Flow a poor fit?
3. Who owns each decision: the evidence layout an assessor will read, the choice of where the check runs, and the statement of which requirement is in scope?
4. What four artifacts does the minimum Method path require before the first implementation story, and what does a readiness FAIL mean?
5. Why does the method want a fresh session for architecture after the PRD, instead of continuing the same chat?
