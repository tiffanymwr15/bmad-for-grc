# Lesson 4. The human loop

## What the loop is

The BMad Loop is the implementation phase running as a queue. You give it stories. It opens a session with the coding agent you already use, implements the story, checks that the change is real and that tests and linters pass, commits, and takes the next story. Separate reviewer agents look for real defects.

It will stop. The project treats stops differently by type: some are logged and the run continues, and some pause the run until a person acts. Published walkthroughs treat those pauses as the correct behavior.

The limit is routing. On a single machine the stop becomes a desktop notification and a local attention file. The person at that machine is the only operator. A story parked there is invisible to everyone else. The control owner never sees the scope question. The evidence consumer never sees the gap in the report. The security reviewer never sees what the tool started returning to other systems.

## Classify the stop before you answer it

Port's explainer sorts example stops by the role that should own them. Here is that table rewritten for GRC engineering.

| The loop asks | Owner | GRC shape of the same question |
|---------------|-------|--------------------------------|
| Branch name, file layout, helper function | Implementer | Where the check lives in the repo, how the test file is named |
| This story needs a capability the spec never mentioned | Obligation owner | The check needs a population, system, or requirement the brief did not include |
| A person will not understand the result | Evidence consumer | The fail message names an internal field and not the requirement, or the record omits pass versus fail |
| The system now exposes something to another system | Security or architecture | Evidence includes a full export, the check calls a new system, or logs contain identifiers you did not agree to store |

Answer the first row and keep going. For the other three, write the question down, name the owner, and pause that story. Continuing with your own best guess is how an exception becomes code.

Turning the loop's gates off so it stops less is the wrong fix. The stop is the method finding a decision. In assurance work, an unanswered decision that still shipped is a finding waiting for a reviewer.

## A local practice that does not need a platform

A shared platform can route each stop to an approval and keep a log the whole team can see. You can get the discipline without one. Keep a short escalation log next to the stories. One row per stop:

```markdown
| Story | Stop | Class | Owner | Answer | Date |
|-------|------|-------|-------|--------|------|
| S2 | Fail message has no requirement name | Evidence consumer | <name> | Must name the requirement | |
| S4 | Evidence writer wants a full system export | Security / architecture | <name> | Fields in NFR1 only | |
```

Rules:

- The implementer may close a row only when the class is implementation detail.
- Any other class stays open until the named owner writes the answer.
- The answer is copied into the story or into `project-context.md` before the loop resumes that story.
- An empty owner cell means the story is blocked. It does not mean the implementer decides.

That log is the GRC version of "reach." The loop can keep moving on stories that are not blocked. It does not get to make the blocked decision itself.

## Playbook for the next change

Use this before you ask an agent to implement a GRC change. If you cannot fill a line, that line is the first workflow you run, not a reason to start coding.

**1. Place the change**

- [ ] Obligation and system named, with a control ID you did not invent
- [ ] Out of scope written in one or two sentences
- [ ] Track chosen: Quick Flow, Method, or Enterprise, using the risk test in lesson 2

**2. Match the artifact to the track**

- [ ] Quick Flow: tech spec cites the existing decision and the test that must still fail
- [ ] Method: brief or PRD, architecture decision, stories, readiness result
- [ ] Enterprise: those, plus the security or compliance note you would hand an auditor, and the quality gate that blocks a story without evidence

**3. Load a constitution**

- [ ] `project-context.md` states evidence fields, fail-closed behavior, and the forbidden list
- [ ] The coding session is pointed at that file and at the single story, not at a vague goal

**4. Slice proof**

- [ ] A fail case exists before the implementation is trusted
- [ ] A pass case exists
- [ ] Evidence location and fields are specified
- [ ] If you catalog the control, the entry uses the same statement as the check

**5. Run, then route**

- [ ] One story per session
- [ ] Review checks the story, the decision record, and the constitution
- [ ] Stops are classified in the escalation log
- [ ] Only implementation-detail stops are answered by the person running the loop

**6. Learn**

- [ ] Retrospective names one assumption the agent made
- [ ] That assumption is either added to `project-context.md` or explicitly rejected in the next brief

## Why this matters after the course

GRC engineering is a sequence of proof: a named requirement, a check that can fail, a record of the result, and a catalog entry that matches the check. BMAD applies that same instinct one step earlier, to the conversation that produces the code. You would not accept a passing run that cannot name its requirement. You should not accept an agent session that cannot name it either.

The loops worth keeping are the ones that get each question to the right person quickly enough that the work continues and the decision stays explicit. Fewer questions is not the target. Unowned answers are.

## Likely-tested distinctions

| Pair | How to tell them apart |
|------|------------------------|
| Logged stop vs. paused stop | A logged stop is an implementation detail the run can live with. A paused stop changes scope, evidence meaning, or exposure, and waits for its owner. |
| Implementer vs. obligation owner | The implementer chooses file layout. The obligation owner chooses whether a new capability or control ID enters scope. |
| Gate off vs. route the stop | Turning gates off ships the guess. Routing records the owner and the answer, then resumes. |
| Escalation log vs. chat scrollback | The log has a class, an owner, and an answer that later sessions load. Scrollback dies with the chat. |
| Story still running vs. story blocked | Other stories may continue. A story with an open non-implementation stop does not. |

## Self-check

1. The loop stops because it wants to name the branch `access-review-check`. Who answers, and does the run pause?
2. The loop stops because the only way to satisfy the story is to query a production system the spec never mentioned. Classify it, name the owner type, and say what you write before implementation resumes.
3. Why is "set gates to none" a poor response when the same loop is generating compliance evidence?
4. Fill one escalation-log row for this stop: the evidence file would include a full export of every account so the reviewer has context.
5. Take any GRC engineering change, real or hypothetical. State the track, the first artifact you would write, and one stop you would refuse to answer yourself.

When you have answered all five, open [answer-key.md](answer-key.md) and update [study-tracker.md](study-tracker.md).
