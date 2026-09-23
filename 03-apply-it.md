# Lesson 3. Apply it

## The change

This lesson walks one ordinary GRC engineering change through the method. The stack stays unnamed on purpose. The same shape fits a policy check, a scheduled monitor, a workflow tool, or a service you build. Swap the requirement for one from your catalog and keep the artifacts.

**Change:** a written requirement says privileged access is reviewed on a fixed interval, and access that misses the review is not allowed to stand. Today that sentence lives in a policy. The engineering work is to make it a control: a check that fails when a review is missing or stale, an evidence record an assessor can read, and a catalog entry that points at that same check.

This is a BMad Method change with a light enterprise overlay. The meaning of the control is new, the work crosses a check, a run, evidence, and a mapping, and the output is something you would show as assurance. It is not a new product. Analysis stays short.

## Phase 1. Analysis, kept small

Write a product brief only long enough to stop the agent from absorbing the neighboring requirements.

```markdown
# Product brief: privileged-access review control

## Gap
The policy requires a review of privileged access on a fixed interval.
Nothing fails when the review is missing, late, or incomplete,
and nothing produces evidence an assessor can trace to the requirement.

## In scope
Privileged accounts already listed in the system of record.
A check that compares the latest review date to the interval.
A fail result when the review is missing or older than the interval.
An evidence record. A catalog entry for this requirement only.

## Out of scope
Deciding who is privileged. Granting or removing access.
Multi-factor authentication. Manager identity proof.
Those are separate requirements and separate stories.

## Done
A population with a current review passes.
A missing or stale review fails, and the result names the account.
The evidence record names the requirement, the population, and the result.
The catalog entry describes the same check in the same words.
```

The out-of-scope lines are the part agents skip. "Automate access reviews" will happily expand into provisioning, ticketing, and authentication if you do not close the door.

## Phase 2. Planning

The PRD splits what the control must do from the qualities the evidence must have. Write requirements as conditions, not as tasks.

**Functional**

- FR1. Given a privileged account whose latest review falls inside the interval, the check returns pass.
- FR2. Given a privileged account with no review, or a review older than the interval, the check returns fail and names the account.
- FR3. Accounts outside the privileged population do not affect the result.
- FR4. The catalog entry names this requirement and points at the same check that FR1 and FR2 describe.

**Non-functional**

- NFR1. The evidence record includes the requirement, the account identifier you already agreed to store, the result, and the time. It includes no credentials, no tokens, and no full export of the identity system.
- NFR2. A reviewer can see pass and fail without reading the implementation.
- NFR3. The check runs on the agreed cadence, or in the delivery path if the requirement is preventive. A fail is visible and blocks the step you said it blocks.
- NFR4. Wording of the requirement is identical in the check, the evidence, and the catalog entry.

NFR4 is the GRC-specific one. Agents will paraphrase one requirement three different ways across three files. The requirement forbids that.

Skip a UX spec if the only consumer is a result file whose fields are already in NFR1. Add one when a person must accept the record: an assessor, a control owner, or a dashboard reader. In that case the spec is the record layout and the pass/fail presentation, not a visual design.

## Phase 3. Solutioning

The architecture note records the expensive choices. One decision record is enough for this change.

```markdown
# ADR: One check, one evidence path

## Decision
Implement the review-interval check in the control automation
you already operate, writing one evidence record per run.

## Why
A second path, such as a spreadsheet macro or a separate script
with its own file format, will disagree with the first path
the moment a review date is interpreted differently.

## Consequences
The control proves that a review record exists and is current
for the privileged population in the system of record.
It does not prove the review was a good judgment, that access
was removed, or that the list of privileged accounts is correct.
Those stay out of scope, as written in the brief.
```

Then slice stories so each one is reviewable on its own. Order them so a failure exists before a success looks meaningful.

| Story | Acceptance criteria | Why this order |
|-------|---------------------|----------------|
| S1. Fail case | A fixture has a privileged account with a stale review, and a test expects a fail that names the account. The test may fail until S2. | You can see the miss before the check exists. |
| S2. The check | The check fails the S1 fixture and passes a fixture with a current review. The result includes the requirement name. | Implementation meets tests that were specified first. |
| S3. The run | The check runs on the agreed cadence or in the agreed delivery step. A fail is visible where you said it would be. | The control is now an operating fact. |
| S4. Evidence | A pass run writes a record that satisfies NFR1 and NFR4. | Proof is a record you keep, not a log line you scroll past. |
| S5. Catalog | The catalog entry cites the requirement with the statement used in S2 and S4. | The catalog and the check cannot drift in the same change. |

Run the readiness check before S2, once the brief, PRD, ADR, and story list exist.

| Result | Meaning on this change |
|--------|------------------------|
| PASS | Requirement, out-of-scope list, pass case, fail case, evidence fields, and owner are all written down. |
| CONCERNS | Proceed, and record the concern in the story. Example: "interval" is specified loosely, so S2 must name the number of days and the timezone. |
| FAIL | Stop. Typical causes: no owner for an exception, no fail case, or "access" used in place of a named requirement. |

`project-context.md` is written once for the effort, and then every later control inherits it:

```markdown
# Project context

## Requirements
Use requirement names and IDs from the catalog.
Do not invent them. If the name is uncertain, stop and ask.

## Evidence
Every new check writes the requirement, the subject, the result, and the time.
Never write secrets, tokens, or full system exports into evidence.

## Behavior
Checks fail closed. A missing input is a fail, not a skip.
Do not weaken an existing check to make a new test pass.

## Scope
A story implements its acceptance criteria only.
A new population, system, or requirement is a planning change.
```

That file is the constitution the method describes. It is also the instruction you most want loaded into every coding session on this work.

## Phase 4. Implementation

For each story, in a fresh session:

1. Create the story file from the epic. Copy the acceptance criteria and the ADR consequence into it. Do not make the agent re-derive them.
2. Implement only that story.
3. Review against the story, the ADR, and the project context. A review that only checks style is the wrong review. Ask whether the diff preserved the requirement name, the fail case, and the out-of-scope line.

The BMad Loop, if you use it, is this phase unattended: take the next story, implement, require tests to pass, review, commit, continue. Hand it the story queue from the table above. Do not hand it the sentence "automate access reviews" with no stories.

When S5 is done, the retrospective is short and specific. What did the agent assume? Did the requirement statement stay identical across files? Did any stop belong to someone other than the implementer? Feed those answers into `project-context.md` or the next brief. That is the learn-and-adjust loop.

## What you can drop

A one-line fix inside the check, after this change exists, is Quick Flow. The tech spec cites the PRD requirement it still satisfies and names the fixture that must still fail. It does not reopen the ADR unless the meaning of the control changes.

## Likely-tested distinctions

| Pair | How to tell them apart |
|------|------------------------|
| Brief vs. PRD | The brief bounds the gap and the non-goals. The PRD states the pass condition, the fail condition, and the evidence qualities. |
| ADR vs. story | The ADR is the choice you do not want re-litigated per story. The story is one step that must honor that choice. |
| Fail case first vs. check first | The fixture records the intended failure before the implementation can pass by accident. |
| Evidence vs. run log | Evidence is the record you keep. A run log is how you noticed it. NFR1 defines the record. |
| Catalog vs. check | The check enforces. The catalog claims the check satisfies a requirement. NFR4 keeps the claim and the enforcement in the same words. |

## Self-check

1. Why does the brief put granting and removing access out of scope, and what would an agent likely build if that section were missing?
2. Rewrite "add a check for access reviews" as one functional requirement in the given/when style used above. Include the fail.
3. You are tempted to start with S2, the check, because you already know how you would code it. What do you lose by skipping S1?
4. The readiness check finds no named owner for an exception if a break-glass account cannot show a review. PASS, CONCERNS, or FAIL, and why?
5. Name three lines you would put in `project-context.md` that should apply to the next control, not only to access reviews.
