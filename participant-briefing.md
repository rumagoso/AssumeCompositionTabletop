# Participant Briefing

*Assume Composition — Tabletop Scenario Pack v1.0*

**Read this before the exercise starts. Do not read ahead into the injects.**

---

## Where you work

You work at **NorthGate Services**, a managed service provider based in the EU. Roughly 200 people. You hold ISO 27001 certification and you are classified as a NIS2 **Important Entity**.

Alongside your managed services business, your platform team maintains a handful of **open-source utility libraries** — the kind of small, widely-depended-on packages that show up three levels deep in other people's `package-lock.json` without anyone quite remembering why. Combined, they see a meaningful number of weekly downloads. You didn't set out to become critical infrastructure. You became critical infrastructure anyway.

Your CI/CD runs on **GitHub Actions**. Publishing to npm is **OIDC-federated** — no long-lived npm tokens sitting in secrets, publishing is authenticated per-run via a short-lived OIDC token exchanged with npm's registry. This was a deliberate hardening decision, made two years ago, and the team is quietly proud of it.

*(Running the SME variant instead? Your org is a 30-person shop with a small, overlapping platform/security team. See `variants/sme-mode.md` — the same morning, smaller headcount.)*

---

## What's about to happen

You will receive four **injects** — short scenario updates, delivered by your facilitator — spread across roughly 35 minutes. Each inject presents a situation and asks your group to make a decision within a time limit.

This is not a quiz. There are no hidden "correct" answers being scored. What's being observed is **how your group reasons under partial information and time pressure**, and — this matters — **what nobody in the room raises**. That second part is not a gotcha. It's the point of the whole exercise, and it will be named explicitly in the debrief.

---

## Your role

Your facilitator will assign you one of the following. If the group is small, some roles are collapsed — the facilitator will tell you which.

| Role | You own |
|------|---------|
| **CISO / Security Lead** | Escalation calls, disclosure decisions, external notification |
| **Dev / Platform Lead** | The CI/CD pipeline — you're the one who actually understands how the build works |
| **IR / SOC** | Triage, scoping, evidence preservation |
| **Communications** | Customer-facing messaging, media, community |
| **Legal / Compliance** | NIS2 / GDPR clocks, regulator notification |

Play your role's priorities honestly, even when they create friction with someone else's. That friction is realistic and it's useful.

---

## Ground rules

1. **No side research.** No phones, no Google, no asking an AI assistant what `pull_request_target` means. You are working with what your organisation would actually know in the moment, not what a search engine could tell you.
2. **The facilitator will not clarify "what really happened."** If a detail isn't in the inject, your group decides how to interpret it — the same way a real incident never arrives with a helpful narrator filling in the gaps.
3. **Every decision your group makes is fair game in the debrief**, including ones that turn out to look bad in hindsight. There are no wrong answers here, only visible ones. Nobody is graded. Everybody learns something about how their own team reasons together — that's the entire product.

---

## One honest note before you start

You will, at some point in the next hour, feel like you're missing information that would make the decision obvious. Sit with that feeling rather than trying to resolve it by guessing what the facilitator "wants." Real incidents feel exactly like this. The discomfort is the exercise working.

See you at the whiteboard.
