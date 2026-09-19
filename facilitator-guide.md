# Facilitator Guide

*Assume Composition — Tabletop Scenario Pack v1.0*

---

## Before you facilitate

Read this document end-to-end once. Read `debrief.md` a second time — it's where the pedagogical payload lives, and it's the part that fails hardest if you improvise.

Skim the [Flashpoint article](https://flashpoint.io/blog/mini-shai-hulud-worm-new-era-ci-cd-exploitation/) and the [MITRE T1677 page](https://attack.mitre.org/techniques/T1677/) so the ATT&CK IDs feel real, not memorised.

You do not need to be a supply-chain expert to run this. You need to be comfortable saying "the group's choice takes us here" and pointing at what happens next.

---

## What you are trying to make happen

Not: "teach participants about pull_request_target."

Instead: **participants feel the synthesis gap in their own thinking.** They spot each individual signal. They miss the composition. In the debrief, they see the composition drawn on the board and recognise what they missed.

If they leave with "we need better tools," you didn't do your job.
If they leave with "we need to reason across trust boundaries, not within them," you did.

---

## The scenario in one paragraph

You are a mid-sized MSP (call it *NorthGate Services* for the exercise) with roughly 200 people, ISO 27001 certified, a NIS2 Important Entity. You maintain several open-source utility libraries used by your customers and the broader ecosystem. Your CI/CD is GitHub Actions with OIDC-federated publishing to npm. This morning, a first-time contributor opened a pull request.

*(Full org context in `participant-briefing.md`. SME variant substitutes a 30-person org with a small platform team — see `variants/sme-mode.md`.)*

---

## Roles

Assign these based on who's in the room. Ideal: 6 participants, one per role. Minimum viable: 4 (collapse Comms + Legal, collapse Dev + SOC).

| Role | Owns | Common blind spot |
|------|------|-------------------|
| **CISO / Security Lead** | Escalation, disclosure, external notification calls | Under-values technical signals early, over-corrects late |
| **Dev / Platform Lead** | The CI/CD, understands the pipeline, reconstructs the chain | Defensive about the build system; slow to admit a workflow was misconfigured |
| **IR / SOC** | Triage, scoping, evidence preservation | Focuses on the endpoint; slow to look at the CI trust boundaries |
| **Communications** | Customer-facing messaging, media, community | Wants to say something too fast, or too slow |
| **Legal / Compliance** | NIS2 / GDPR clocks, regulator notification | May freeze the room by demanding certainty before action |
| **Facilitator** | You. Deliver injects, keep time, do not answer their questions |

**SME mode:** collapse to Owner, Tech Lead, External Comms. See `variants/sme-mode.md`.

---

## The 60-minute run

### 0:00–0:05 — Setup

Distribute the participant briefing (or read the paragraph above aloud). Assign roles. Confirm the timer. State the rules:

- No side research (no phones, no Google, no ChatGPT). The exercise measures what you know and how you reason, not what you can look up.
- The facilitator will not answer clarifying questions about what "really" happens. If it's not in the inject, decide.
- Every decision is fair game in the debrief. There are no wrong answers, only visible ones.

### 0:05–0:12 — Inject 1: The innocuous PR

Deliver [`injects/inject-01-pr-arrives.md`](injects/inject-01-pr-arrives.md).

**Decision required:** merge, review, hold, block?

**What good looks like:** any participant asking about the workflow trigger, the fork's history, or whether `pull_request_target` runs on this repo. Give partial credit for "let's have a senior review it."

**What common looks like:** approve because the PR is small and cosmetic. The trap.

**Time management:** if the group is stuck at 6 minutes, force a vote. Whichever way it goes, you proceed. Note who voted which way — it matters in the debrief.

### 0:12–0:19 — Inject 2: Cache anomaly

Deliver [`injects/inject-02-cache-poisoned.md`](injects/inject-02-cache-poisoned.md).

Two weeks have passed since Inject 1. Your build cache monitoring — or a passing developer noticing something odd — has flagged an anomaly. Something was cached during the workflow run from that PR.

**Decision required:** how do you scope this? Who do you bring in? Do you rebuild without the cache?

**What good looks like:** treating this as potentially adversarial from the outset. Asking who could have written to the cache and under what identity.

**What common looks like:** assuming it's a benign misconfiguration. Rebuilding without investigating.

**MITRE mapping:** T1677 (Poisoned Pipeline Execution). Do not name it aloud yet — it goes on the board at the debrief.

### 0:19–0:29 — Inject 3: The malicious publish

Deliver [`injects/inject-03-npm-publish.md`](injects/inject-03-npm-publish.md).

A downstream user has reported that a recent version of one of your packages is doing something suspicious on install. Your npm audit shows the version came from your legitimate release pipeline, authenticated via your OIDC federation. Signed with valid SLSA provenance.

**Decision required:** is this you or a compromise? Deprecate the version? Notify users? Notify npm? Notify regulators (NIS2 clock)?

**What good looks like:** parallel tracks — technical investigation *and* pre-drafting communications *and* starting the NIS2 24h early-warning clock. Recognising that "we published it" and "we were compromised" can both be true simultaneously.

**What common looks like:** getting stuck on "was it really us?" for too long, missing the 24h clock, or over-notifying before scope is understood.

**MITRE mapping:** T1552 (Unsecured Credentials) for the OIDC memory extraction, T1195.002 (Compromise Software Supply Chain) for the publish. Save for the debrief.

### 0:29–0:39 — Inject 4: The cascade

Deliver [`injects/inject-04-downstream-alert.md`](injects/inject-04-downstream-alert.md).

The package has 12 million weekly downloads. Three enterprise customers are on the phone. A journalist has emailed. Security Twitter is starting to talk. Your regulator has questions. It's now 4pm on a Friday.

**Decision required:** external comms plan, customer notification, regulator response, and — critically — what do you say about the *scope* when you do not yet fully understand it?

**What good looks like:** clear separation of what is known, unknown, and being investigated. Acknowledgment that early honesty about uncertainty is better than late correction.

**What common looks like:** either full silence pending investigation ("we'll comment when we know more") or over-committed statements that will need to be walked back.

**No new MITRE mapping** — this inject tests decision-making under public pressure, not attack technique recognition.

### 0:39–0:52 — Structured debrief

This is the most important segment. See [`debrief.md`](debrief.md) for the full script. In summary, three passes:

**Pass 1 — What did you do?** (3 min)
Fast round-the-room. Each participant states one decision they made and why. No arguing. Facilitator writes them on the board.

**Pass 2 — The composition map** (5 min)
Facilitator draws three boxes on the board: **T1677** (Poisoned Pipeline Execution), **T1552** (Unsecured Credentials), **T1195.002** (Compromise Software Supply Chain). Draws arrows showing the chain: PR → workflow → cache poisoning → OIDC extraction → malicious publish → downstream cascade.

Then adds a fourth box, empty, labelled **"the composition itself."** Says: *"MITRE has techniques for each of these. It does not have a first-class object for the composition. Neither did we in this exercise. Every decision we made was inside one of the boxes, not across them."*

**Pass 3 — What didn't happen** (5 min)
Facilitator asks: *"What signal would have caught this two weeks earlier? Nobody in the room raised it. Why not?"*

Common answers:
- Nobody questioned why a first-time contributor's PR could touch a workflow trigger with write scope
- Nobody asked about cache scoping between fork and base
- Nobody had a mental model of the OIDC federation as a *credential* rather than an *identity*

The point is not to shame. The point is to make visible the assumptions the room brought in.

### 0:52–1:00 — Three Monday actions + close

Ask each participant: **"What is one thing you will change on Monday?"**

Write them on the board. Common examples:

- Audit every `pull_request_target` workflow across our org
- Add cache scoping to our GitHub Actions hardening baseline
- Rebuild the NIS2 early-warning playbook to account for OIDC-federated publish compromise
- Add a supply-chain incident scenario to next quarter's IR drill schedule
- Draft the composition question into our next threat modelling session: *"if two of these three techniques fired here, what would we see?"*

Close by pointing at the repo. Thank the room.

---

## Common facilitation pitfalls

**You answer their questions.** Don't. Their choices under uncertainty are the exercise.

**You let a strong voice dominate.** Explicitly redirect: *"CISO, sit with that. IR/SOC, what do you see?"*

**You get pulled into a technical rabbit hole.** The exercise is about decision-making under composition, not about the mechanics of GHA cache internals. If the group wants that, offer the reference material and move on.

**You skip the "what didn't happen" pass to save time.** It's the part that changes their thinking. Cut Pass 1 short before you cut this.

**You over-explain the ATT&CK mapping in the debrief.** The map does its own work. Draw it, say the sentence about "no first-class object for composition," stop. Don't lecture.

---

## After the exercise

Encourage the group to document three things:

1. Their three Monday actions (before they forget)
2. The single moment in the exercise where the room shifted from "this is fine" to "this is not fine" — this is often diagnostic of the org's own risk posture
3. Any control gap the exercise surfaced that they want to add to the risk register

Optionally, run the debrief report through the debrief template in `debrief.md` for a written record.

---

## When to run this exercise

- New quarter, new IR drill cycle
- After onboarding new platform or SOC staff
- Before signing an OIDC federation with a new registry or cloud
- After any incident where "we didn't see it coming" was a takeaway
- Whenever someone in leadership says "supply chain is on the radar" — this is what "on the radar" should feel like

---

## Feedback

If you run this, please share what worked and what didn't. Open an issue on the repo or reach out directly. Every run makes v1.1 better.
