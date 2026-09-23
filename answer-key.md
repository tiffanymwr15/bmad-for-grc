# Answer key

Grade yourself strictly. A partial answer on a decision-owner question is wrong, because that is the mistake the course is about. After you grade, mark the domain in `study-tracker.md` as `strong` or `shaky`, and copy any miss into the weak-items log.

## Lesson 1

1. At least four, often all five. "Encryption at rest" does not name the requirement or the system boundary. "Make the check pass" does not say what must fail. Evidence location, exception owner, and the forbidden list (do not weaken an existing check, do not invent an ID) are unstated. Any one of those left blank will be filled by the agent.
2. In the artifact, the decision changes a document the next phase loads. Once the run is green, the decision is already evidence, a catalog entry, and a history someone may rely on. Changing it means explaining why yesterday's proof is void.
3. A scope decision. A data store the spec never mentioned is a capability the obligation did not include. It can change what the system reads, what it stores, and who owns the new exposure. Branch naming would be the implementation-detail version of a stop.
4. The control lives only in a document. The control lives only in the pipeline, with no recorded decision. BMAD directly prevents the second: unstated assumptions becoming code. It also stops you from "fixing" the first by generating an unowned check.
5. A strong answer says that agents implement implied decisions, that a GRC decision has to carry obligation, fail case, evidence, and owner, and that writing those down before the diff is what makes the later gate defensible. Quoting the acronym is not required.

## Lesson 2

1. Quick Flow. Write a tech spec that cites the existing control decision and names the case that must still fail. Do not open a PRD unless the meaning of the interval is actually disputed.
2. BMad Method, with a light enterprise overlay if you will show the result as assurance. The control's meaning does not exist in an artifact yet, and the change crosses the check, the run, the evidence, and the catalog. Quick Flow would let the agent choose the interpretation in code.
3. Evidence layout: the evidence consumer (UX perspective), when a person must accept the record. Where the check runs: the architect, as an architecture decision. Which requirement is in scope: the product / obligation owner.
4. PRD, architecture, epics and stories, and a readiness result. (A brief is optional.) FAIL means an artifact required to implement without guessing is missing, so you stop before coding. It does not mean the code is defective.
5. The architecture session should load the PRD as context, not inherit a chat that already wandered through options, rejected ideas, and half-decided them. Fresh context keeps the written artifact as the source of truth.

## Lesson 3

1. Those are different requirements with different proof. Left unstated, an agent asked to "automate access reviews" will often build provisioning, removal, and ticketing because that is a plausible completion of the phrase. The brief's non-goals are what keep this exercise a review-interval claim.
2. One acceptable answer: Given a privileged account with no review or a review older than the interval, when the check runs, then the result is fail and the message names that account. A pass-only sentence is incomplete.
3. You lose a recorded picture of the failure that does not depend on the check you are about to write. Without it, a check can pass by reading the wrong date, or by not checking at all, and you have no fixture that shows the miss.
4. FAIL. An exception with no owner is an authorization to deviate that nobody holds. CONCERNS would fit a narrower ambiguity you can resolve inside a story, such as which timezone defines "current." Lack of an owner is not narrow.
5. Any three that generalize, for example: do not invent requirement names, fail closed when input is missing, never write secrets into evidence, do not weaken an existing check to make a new test pass, and do not expand scope beyond the story. Lines that only make sense for access reviews do not count.

## Lesson 4

1. The implementer. The run does not need to pause. Branch naming is an implementation detail.
2. Class: capability the spec never mentioned, and it also exposes a new system, so security or architecture is involved along with the obligation owner. Pause the story. Write a log row whose answer states whether that system is in scope, which fields may be read, and what may be stored. Resume only after those owners answer. "We need it to finish the story" is not an answer.
3. The loop would commit guesses about scope, evidence, and exposure, and those commits become the proof you later show. A stop is the point where that guess would have entered the record.
4. One acceptable row: Story S4 (or whichever evidence story), stop is "full account export in the evidence file," class is security or architecture, owner is the security or architecture owner, answer stays blank until they write it. The right substantive answer, given lesson 3's NFR1, is to keep only the agreed fields. Filling the answer as the implementer, without an owner, is the miss.
5. Credit any GRC change that names a track consistent with lesson 2, an artifact that matches that track, and a stop whose class is obligation, evidence consumer, or security. "I would answer every stop myself" does not pass.
