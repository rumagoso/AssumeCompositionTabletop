# Debrief Script

*Assume Composition — Tabletop Scenario Pack v1.0*

**Read this document twice before facilitating.** This is where the pedagogical payload lives. Everything before this point — four injects, thirty-four minutes, four roles arguing under time pressure — exists to set up these thirteen minutes. If you cut this short to save time, you have run a fun exercise with no point.

**0:39–0:52. Thirteen minutes. Three passes.**

---

## Before you start: what you're aiming for

Not: "here's what you should have known about `pull_request_target`."

Instead: **the group sees, on the board, in their own words, that they reasoned correctly inside each individual moment and still missed the thing that connected all four.** That recognition has to land as their own realisation, prompted by what's on the board — not as a lecture from you. Your job in this debrief is almost entirely to draw, ask, and get out of the way.

---

## Pass 1 — What did you do? (3 minutes)

**Mechanics:** Fast round-the-room. Each participant states **one** decision they personally pushed for or made, in one sentence, and why. No arguing, no rebuttal, no "well actually." You are populating the board, not adjudicating it.

**Script:**

> "Thirty seconds each. One decision you made or pushed for, and the one-line reason. I'm just writing these down — we're not debating them yet."

Write each on the board as a short label: *"Merged on green CI"* / *"Wanted to hold, got overruled"* / *"Cleared the cache without investigating"* / *"Started the NIS2 clock"* / *"Held comms until certain"* — whatever actually came out of your room. Use their language, not the inject's language.

**Facilitator note:** if someone tries to justify or defend a decision at length, gently cut back to the format: *"Got it — one line, keep it moving, we'll come back to the why in a minute."* You will come back to it. Pass 2 is where the why gets its answer.

---

## Pass 2 — The composition map (5 minutes)

This is the centre of the exercise. Take your time; do not rush this to protect Pass 3's clock — if anything, protect this one first.

**Mechanics:** Draw three boxes on the board, spaced apart, left to right:

```
[ T1677 ]        [ T1552 ]        [ T1195.002 ]
Poisoned         Unsecured        Compromise
Pipeline         Credentials      Software
Execution                         Supply Chain
```

Now draw the chain underneath, connecting them with arrows through the actual sequence of your exercise:

```
PR opens (pull_request_target)
   → workflow runs with base-repo access
      → cache poisoned during that run
         → later run restores poisoned cache
            → OIDC token exposed in runner memory  [T1552]
               → attacker publishes malicious version
                  using that legitimate OIDC identity [T1195.002]
                     → downstream cascade
```

Map the earlier part of the chain — PR through cache poisoning — explicitly to **T1677** as you draw the first arrow. Let the group watch the sequence take shape; don't dump the whole diagram at once.

**Then draw a fourth box, to the right of the other three, and leave it empty:**

```
[ T1677 ]  →  [ T1552 ]  →  [ T1195.002 ]  →  [   ??   ]
                                                the
                                              composition
                                                itself
```

**Say this, close to verbatim, and then stop talking:**

> "MITRE catalogues each of these individually. T1677. T1552. T1195.002. All three are real, documented, named techniques. What MITRE does not have — what nobody's framework has, yet — is a first-class object for *this box*. The composition itself. The chain across the boundary.
>
> And look back at your decisions on the board. Every single one of them was made *inside* one of the first three boxes. Nobody in this room, in the last thirty-five minutes, made a decision that was actually about the fourth box — about the composition, about the fact that a code-review call at 9:40am was quietly connected to a publish-authentication call three weeks later."

**Then stop. Let it sit for a few seconds before moving to Pass 3.** Resist the urge to explain further. Over-explaining here is the single most common facilitation failure — see `facilitator-guide.md`'s pitfalls section. The diagram does the work. Your sentence does the work. Anything more dilutes both.

---

## Pass 3 — What didn't happen (5 minutes)

**Mechanics:** One question, asked once, then genuine silence while the room thinks.

**Script:**

> "Here's the question I actually want an answer to. What signal, if anyone in this room had raised it, would have caught this two weeks earlier — back at Inject 1 or Inject 2? Nobody raised it. Why not?"

Let the silence run longer than feels comfortable. This question is not rhetorical and the room needs a moment to actually search rather than perform an answer.

**Common answers, if the room needs a nudge after ~20 seconds of silence** (offer one, not all three, and only if truly stuck):

- *"Nobody questioned why a first-time contributor's PR could touch a workflow trigger file with write scope at all."*
- *"Nobody asked how cache scoping works between a fork and the base repository — most of us don't actually have a mental model of that boundary."*
- *"Nobody in the room was thinking about the OIDC federation as a credential that could be extracted — we were thinking about it as an identity, a 'this really is us' signal, not as a thing with an attack surface of its own."*

**The point, stated once, plainly, and not repeated:**

> "This isn't about shame — nobody in this room does this job badly. It's about making visible the assumptions we all walked in with. That's the actual output of this exercise: not 'here's a vulnerability,' but 'here's a shape of reasoning we don't currently have, and now we've felt the absence of it.'"

---

## Written record template (optional)

If your organisation wants a documented output from the session — useful for feeding into a risk register or an IR drill report — capture this immediately after the exercise, while it's fresh:

```markdown
## Tabletop Debrief Record — Assume Composition

**Date:**
**Facilitator:**
**Participants & roles:**
**Variant run:** MSP / SME

### Pass 1 — Decisions made
[paste the board]

### Pass 2 — Composition map
Techniques identified: T1677, T1552, T1195.002
Composition-level decisions made during the exercise: [none / describe]

### Pass 3 — What didn't happen
Signal the group identified as missing:
Root cause (in the group's own words, of why it wasn't raised):

### Monday actions committed
1.
2.
3.

### The shift moment
At what point did the room's read on the situation change from
"this is fine" to "this is not fine"? [free text — often diagnostic
of the org's actual risk posture, per `facilitator-guide.md`]

### Control gaps to add to the risk register
-
```

---

## After Pass 3: handing off to the close

Pass 3 flows directly into the facilitator guide's final segment (0:52–1:00 — three Monday actions + close). Don't add a fourth pass or a summary lecture here. The room has done the work; let it land and move to action items. See [`facilitator-guide.md`](facilitator-guide.md) for that closing script.
