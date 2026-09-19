# Inject 4 — The cascade

**Time:** T+29 minutes into exercise
**Delivered by:** Facilitator (read aloud) + handout/screen

---

## The situation (what participants hear)

It is now 4:00pm on a Friday. Word has travelled faster than your investigation. `@northgate/utils-core` sits somewhere in the dependency tree of a lot of other people's software — combined, the packages your team maintains see several million weekly downloads. You don't fully control who depends on you, and today that stops being an abstract fact.

In the last ninety minutes: three enterprise customers have called your account managers directly, asking whether they need to take action. A security journalist who covers the supply-chain beat has emailed your press inbox with a two-line question and a deadline of "today, ideally." Independent researchers have started comparing notes about `4.2.1`'s behaviour on a public security mailing list — nobody outside has connected it to a CI/CD compromise yet, but the outbound domain has been posted publicly twice now. Your national regulator's incident-reporting contact has sent a query, referencing the NIS2 early-warning notification your Legal/Compliance function may or may not have already filed.

Your investigation is not finished. You know roughly what happened. You do not yet know the full blast radius — how many versions were affected, how long the window was, or what the payload actually did beyond the one outbound call your downstream contact reported.

It is Friday. It is 4pm. Everyone in the room would like to go home.

## The artifacts (what participants see)

**Three messages arriving near-simultaneously:**

```
[Account Manager, internal Slack]
"Client X's CISO is on the phone asking if they need to pull utils-core
from prod TODAY. What do I tell them."

[Journalist, email]
"Following up on reports of anomalous network activity in a recent
utils-core release. Can you confirm whether this was a supply-chain
compromise, and if so, since when? Filing EOD."

[Regulator, secure portal message]
"Reference: your early-warning notification [timestamp / or: 'We note
no early-warning notification has been received regarding this matter
to date.'] Please provide current status and expected timeline for
initial assessment per NIS2 Art. 23."
```

*(Facilitator: use the bracketed regulator variant that matches what your group actually did in Inject 3. If they never started the clock, say so plainly — that's the version that lands.)*

## Decision required

**What is your external comms plan — to customers, to the journalist, to the regulator? And critically: what do you say about scope when you do not yet fully understand it yourself?** Your group has 10 minutes.

## Facilitator notes (hidden from participants)

- **What good looks like:** a clear, explicit three-way separation in whatever the group drafts — what is *known*, what is *unknown*, and what is *being actively investigated with a stated next-update time*. Willingness to say "we don't yet know the full scope" out loud, to a journalist, on the record, rather than either stonewalling or overclaiming a scope they can't yet stand behind. Recognising that the three audiences (customer, journalist, regulator) need different documents, not one message copy-pasted three times.
- **What common looks like:** one of two failure modes, both understandable under Friday-afternoon pressure. Either **total silence** ("we'll comment once we know more" — which reads, correctly, as stonewalling, and burns trust with the journalist and the enterprise customers alike) or **overcommitment** — a confident statement about scope or impact that the investigation hasn't actually earned yet, which will need a walk-back later and costs more credibility than the original incident.
- **A good facilitator prompt if the group is stuck on "we can't say anything yet":** *"The journalist is filing end of day whether you respond or not. What's in the story if you say nothing?"*
- **No new ATT&CK mapping for this inject.** This is deliberate — Inject 4 tests decision-making under public and regulatory pressure, not attack-technique recognition. Don't try to force a technique onto it in the debrief; let it stand as the consequence layer.
- **Time budget:** 10 minutes. This inject tends to run hot emotionally — people have opinions about crisis comms. Let it. Redirect dominant voices ("Comms, what does Legal need to see before this goes out? Legal, what does Comms need from you in the next two minutes, not the next two hours?") rather than cutting the energy short.
