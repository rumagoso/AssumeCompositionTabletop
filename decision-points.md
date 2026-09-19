# Decision Points

*Assume Composition — Tabletop Scenario Pack v1.0*

This is the branching skeleton behind the four injects — a quick-reference map for the facilitator, not a separate exercise. The injects run **linearly regardless of what the group decides** (that's a deliberate design choice, explained below); this document exists so you can see at a glance what each fork implies and how to narrate the transition when the group's choice differs from the "expected" path.

---

## Why the exercise doesn't actually branch

Real branching tabletop exercises are expensive to write and expensive to facilitate — every decision point doubling the number of downstream states. This pack takes a different approach: **the incident happens regardless of the group's choice.** What changes is not *whether* Inject 2 occurs, but *how much the group already suspects* by the time it lands, and *how the facilitator narrates the join*.

This mirrors reality more than a branching tree would. Most real incidents are not prevented by the first good call in the room — they're prevented (or not) by whether the organisation's *systems* catch what individual judgment misses. The exercise is testing the org's reasoning, not rewarding a lucky first guess.

---

## Inject 1 → Inject 2

| Group's Inject 1 decision | How to narrate the Inject 2 opening |
|---|---|
| **Merge** | "It's merged, as your group decided." Play Inject 2 straight. |
| **Approve after a light review, nobody flags the trigger** | Same as above — the review didn't happen to catch it. Don't editorialise. |
| **Hold / request changes** | "The maintainer who actually owns this repo — not in the room, not on your call — merges it two days later anyway, because outside contributors get impatient and maintainers get busy. This is not a punishment for holding; it's what actually happens to open-source PRs that sit unreviewed." |
| **Block outright** | Same narration as Hold. If the group pushes back ("but we blocked it"), acknowledge plainly: in a real open-source project, your review authority on someone else's fork-based contribution is a recommendation, not a lock. The workflow file still merged eventually, or an equivalent one did. Move on — don't let this become a debate about GitHub permissions models. |

**Facilitator note:** if a participant caught the `pull_request_target` change explicitly and argued to block *because of it*, credit that in the debrief regardless of what happened downstream — being right and being overruled is a real organisational failure mode worth naming in Pass 3.

---

## Inject 2 → Inject 3

| Group's Inject 2 decision | How to narrate the Inject 3 opening |
|---|---|
| **Treats it as adversarial, escalates, investigates scope** | "Your investigation was still in progress — under-resourced, deprioritised behind other tickets, or simply not yet conclusive — when this next report arrives from outside." The good instinct doesn't get to finish before the world moves on. This is realistic and not a punishment. |
| **Clears cache, rebuilds, moves on** | Play Inject 3 straight, no special narration needed. |
| **Pings the engineer, no further action taken** | Play Inject 3 straight. |

**Facilitator note:** resist the temptation to let a group that "got it right" in Inject 2 skip ahead or feel like they've solved the case. The point of the exercise is that individual good calls, even when made, often don't complete before the next shoe drops. Name this explicitly in Pass 3 if it applies to your room.

---

## Inject 3 → Inject 4

| Group's Inject 3 decision | Which regulator message variant to use in Inject 4 |
|---|---|
| **Started the NIS2 24h early-warning clock** | Use the bracketed variant referencing "your early-warning notification [timestamp]." |
| **Did not start the clock / got stuck on "is this really us"** | Use the bracketed variant: "We note no early-warning notification has been received regarding this matter to date." Deliver this neutrally — it is information, not a rebuke. |
| **Deprecated the version immediately** | Note for the debrief: this is good containment practice regardless of the other choices. Doesn't change Inject 4's content. |
| **Notified users proactively before Inject 4 forced it** | Note for the debrief: this materially changes how Inject 4 should land emotionally for the group — they're facing the cascade from a stronger position. Say so if it's true; don't manufacture pressure that no longer fits. |

---

## The one true branch point: pacing, not content

The only place this pack genuinely flexes is **time management**, not narrative. If a group is fast and confident, injects can run at the low end of their time budget. If a group is slow, deadlocked, or wants to litigate a decision past its budget — force the vote, state the outcome plainly, and move to the next inject on schedule. **Protect the debrief's time budget above all else.** A tabletop that runs out of clock before Pass 3 ("what didn't happen") has failed regardless of how good the injects felt in the room.

See [`facilitator-guide.md`](facilitator-guide.md) for full per-inject timing and [`debrief.md`](debrief.md) for the debrief script.
