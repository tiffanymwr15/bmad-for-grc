# Lesson 1. Why BMAD matters for GRC engineering

Read this after the opening of the visual course, or start here if you are reading. The definition comes first. The claim comes after you know what the method is.

## What BMAD is

BMAD is the Breakthrough Method for Agile AI-Driven Development. It is an open-source way to build software with AI agents. The work covers the whole effort: what to build, how it holds together, and how it changes as you learn.

A coding agent is usually handed a goal and asked to implement it. BMAD puts a method in front of that. Specialized perspectives weigh in, in order: product, architecture, the person who will use the result, development, and testing. Each one leaves a document. The next step loads that document instead of guessing. The amount of planning matches the size of the change. A small, already-decided edit goes straight to build. A larger change gets a fuller plan.

A later part of the method, the BMad Loop, can take the stories that planning produced and run the build without someone pasting the next command. It implements a story, checks that the tests pass, reviews the change, and commits it. When it cannot decide, it stops and asks.

## Why that matters for GRC engineering

GRC engineering turns an obligation into something a system can enforce and an assessor can trace. The pieces are a named requirement, a check that can fail, a record of the result, and a catalog entry that uses the same words as the check.

That work is now often done with a coding agent. The agent is good at writing the check. It is careless about the decision the check depends on. "Add the control" also invites it to invent which requirement applies, what a failure looks like, what gets stored as evidence, and who may accept an exception.

In a product feature, that guess becomes rework. In GRC engineering, the guess becomes proof. Someone later treats a green run as evidence that a requirement is met. If the requirement was never named, the evidence does not hold.

BMAD matters here because it keeps the decision in front of the code. You name the obligation, the fail case, the evidence, and the owner while they are still cheap to change. The agent builds against those words. When the loop stops, the question goes to the person who owns it.

## The claim

BMAD matters in GRC engineering because an agent will implement whatever decision you left implicit, and an implicit control decision does not survive an audit.

The method's trade is deliberate: spend more time, and more tokens, making product, architecture, and design decisions explicit before code exists. A wrong decision is cheap in a planning artifact and expensive once it ships. In this field, "ships" means the gate is green, the evidence is filed, and someone later treats that evidence as proof.

## Two failures you already know

**The control lives in a document and not in the system.** The obligation is real. No check enforces it, and no evidence record is produced when it holds or fails. An assessment finds the gap by reading the system, not the policy.

**The control lives in the system and not in a decision.** An agent, or a hurried engineer, wrote a check that passes. Nobody recorded which obligation it satisfies, who owns the exception path, what a false pass looks like, or where the evidence goes. The run is green. The story is missing.

BMAD is aimed at the second failure, and it keeps the first one from being "fixed" by generating code with no owner. Coding assistants are effective at implementation. They turn unstated assumptions into code. The method keeps you in control by making the important decisions explicit and preserving them as context for the work that follows.

## What "explicit" means here

A GRC change is explicit when a later reader, human or agent, can answer these without guessing:

1. **Obligation.** Which control or requirement, in which framework, and which system is in scope.
2. **Intent.** What condition must be true, and what condition must fail the gate.
3. **Evidence.** What artifact proves it, where it is stored, and who can read it.
4. **Owner.** Who accepts a scope change, an exception, or a residual risk.
5. **Boundary.** What the agent is forbidden to do in order to get a green build. Inventing a control ID, weakening a rule, logging a secret, and widening scope are the usual list.

If any of those five is missing, the agent fills it in. That fill-in is the defect.

## Why the order matters

BMAD's suggested order is clarify the idea, plan it, then build and verify, with learning fed back into planning. Specialized perspectives weigh in before the code exists: product, architecture, UX, development, and testing.

Translated, that means the control owner, the person who designs where the check lives, the person who consumes the evidence, and the person who will test pass and fail cases all leave a mark in an artifact before implementation starts. Catching a scope or design question at that point is the whole point. After the check is running and evidence is filed, changing it means re-issuing evidence and explaining a moving control to an assessor.

## Where the Port article fits

Port's explainer describes a later piece of the method, the BMad Loop: an unattended run that takes a queue of stories, implements each one, reviews it, and commits it when tests and linters pass. The loop works with agents such as Claude Code and Codex.

The article's useful warning is about what happens when the loop stops. It stops on decisions it cannot make. Some stops are implementation details. Some are product questions. Some are architecture and security questions. If every stop lands on the developer at the keyboard, that person answers for roles they do not hold.

For GRC, that is the moment an exception gets invented. Lesson 4 covers how to route those stops. The course does not treat "stop less often" as a goal. A stop is a decision that still needs a human. Skipping it means shipping a guess, and a guess in a control is an undocumented exception.

## The scale clue

The same method sizes itself to the work. A false-positive fix in a rule you already decided does not need a product requirements document. A new control family, a new system in scope, or an AI-risk workflow does. Lesson 2 names the tracks. The reason to care now: under-planning a compliance change and over-planning a one-line fix are both ways the method fails.

## Likely-tested distinctions

| Pair | How to tell them apart |
|------|------------------------|
| Documented control vs. implemented control | The first is an obligation someone can cite. The second is a check, a test, and an evidence record. |
| Explicit decision vs. agent assumption | An explicit decision is written in an artifact the next session loads. An assumption appears for the first time inside the diff. |
| Cheap decision vs. shipped decision | Cheap means the PRD, architecture note, or story can still change. Shipped means the gate, evidence, and mapping already treat it as fact. |
| Autonomy vs. reach | Autonomy is the loop doing the next story without you pasting a command. Reach is the stop arriving at the person who owns that decision. |

## Self-check

1. A teammate asks an agent to "add encryption at rest and make the check pass." Which of the five explicit-decision questions are still unanswered?
2. Why is a wrong control decision cheaper in a planning artifact than in a green pipeline?
3. The BMad Loop stops because a new check would need to read a data store the spec never mentioned. Is that an implementation detail or a scope decision, and why?
4. Name the two failure modes in this lesson, and say which one BMAD is built to prevent directly.
5. Explain, in two or three sentences you could say to another GRC engineer, why this method matters even if you never install it.
