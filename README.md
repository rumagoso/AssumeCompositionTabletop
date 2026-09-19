# Assume Composition — Tabletop Scenario Pack

> A 60-minute tabletop exercise for chained-composition supply-chain attacks against CI/CD pipelines. Built around the Mini Shai-Hulud pattern (TanStack, TeamPCP, and the family).

**Author:** Rui Soares · [itilblues.wordpress.com](https://itilblues.wordpress.com)
**License:** [CC BY 4.0](LICENSE) — use it, adapt it, credit the source.
**Version:** 1.0 (English)
**Companion talk:** *Composition Is the New Zero-Day* — CFP submitted to BSides Lisbon 2026, not selected. Published here regardless.

---

## The thesis

For decades, our real moat wasn't the individual vulnerabilities. It was the *synthesis cost* — reading advisories, understanding trust models, spotting compositions across boundaries.

That cost is falling. LLMs are shockingly good at "find me a chain in these three weaknesses."

We cannot prove any specific attack was LLM-assisted. We *can* prove the economics shifted.

**Assume Composition.**

This pack lets a security team feel that shift in 60 minutes.

---

## What this is

A turnkey tabletop exercise. Four injects, structured decision points, blue-team roles, a debrief that maps the participants' choices to MITRE ATT&CK techniques — and, more importantly, to the **composition across techniques** that the framework doesn't yet represent as a first-class object.

**What's in the pack:**

- Full facilitator guide (`facilitator-guide.md`) — everything you need to run it cold
- Participant briefing (`participant-briefing.md`) — 1-page pre-read
- Four injects (`injects/`) — each with situation, artifacts, decision, facilitator notes
- Decision points (`decision-points.md`) — the branching structure
- Structured debrief (`debrief.md`) — including the "what didn't happen" pass
- Variants (`variants/`) — MSP mode (default) and SME mode
- Reference material (`reference/`) — real attack timeline, MITRE mapping, further reading

**What this is not:**

- Not a training in supply-chain security fundamentals (participants should already have a working mental model of CI/CD, npm, GitHub Actions at concept level)
- Not a red-team exercise (no live tooling, no penetration testing)
- Not a compliance checkbox (though it maps cleanly to NIS2 incident response drills)

---

## Who it's for

**Primary:** Security teams, IR/SOC leads, platform engineers, CISOs at organisations with CI/CD pipelines and open-source dependency exposure. MSP context assumed by default.

**Secondary:** SMEs with a small or shared security function. Use the SME variant (`variants/sme-mode.md`) — collapses roles, adjusts inject complexity, keeps the pedagogical payload.

**Regulatory context:** Directly useful as a supply-chain-specific incident response drill for organisations under NIS2, DORA, or ISO 27001:2022 (Annex A 5.19–5.23).

---

## How to run it

**Time:** 60 minutes.
**Group size:** 5–8 people (MSP mode) or 3–5 (SME mode).
**Materials:** Printed inject sheets (or shared screen), a whiteboard or shared doc for the debrief map, a timer.
**Facilitator:** One person who has read the facilitator guide.

**Sequence:**

| Time | Segment |
|------|---------|
| 0:00–0:05 | Setup and role assignment |
| 0:05–0:12 | Inject 1 — The innocuous PR |
| 0:12–0:19 | Inject 2 — Cache anomaly surfaces |
| 0:19–0:29 | Inject 3 — Malicious publish from your OIDC |
| 0:29–0:39 | Inject 4 — The cascade |
| 0:39–0:52 | Structured debrief |
| 0:52–1:00 | Three "Monday morning" actions + close |

Full detail in [`facilitator-guide.md`](facilitator-guide.md).

---

## Attribution

If you run this pack, please credit:

> *Assume Composition — Tabletop Scenario Pack*, Rui Soares (2026). Available at [github.com/rumagoso/assume-composition-tabletop](https://github.com/rumagoso/assume-composition-tabletop) under CC BY 4.0.

Sharing back what worked, what didn't, and what you'd change is welcome. Open an issue or reach out.

---

## Roadmap

- **v1.0 (this release):** English, MSP + SME variants
- **v1.1:** Portuguese translation
- **v1.2:** Additional variant for financial services (DORA framing)
- **Later:** Companion pack for the *composition-mapping* proposal across T1677 + T1552 + T1195.002

---

## Further reading

- Flashpoint — *The Mini Shai-Hulud Worm and the New Era of CI/CD Exploitation* (May 2026)
- Google Threat Intelligence Group — *AI Threat Tracker: Adversaries Leverage AI for Vulnerability Exploitation* (May 2026)
- FBI — *Cybersecurity Advisory: TeamPCP* (July 2026)
- MITRE ATT&CK: [T1677 Poisoned Pipeline Execution](https://attack.mitre.org/techniques/T1677/), [S9043 Mini Shai-Hulud](https://attack.mitre.org/software/S9043/), [G1056 TeamPCP](https://attack.mitre.org/groups/G1056/)

Full reading list in [`reference/further-reading.md`](reference/further-reading.md).
