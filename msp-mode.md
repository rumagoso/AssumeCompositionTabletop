# Variant — MSP Mode (default)

*Assume Composition — Tabletop Scenario Pack v1.0*

This is the **default configuration** of the pack. Every other file — `participant-briefing.md`, the four injects, `debrief.md`, `decision-points.md` — is written to this mode out of the box. This file exists mainly to make the assumptions explicit, so you can see exactly what to change if you're adapting for a different-shaped org rather than running the SME variant.

---

## Assumed organisation

**NorthGate Services** — a mid-sized MSP, ~200 people, EU-based, ISO 27001 certified, NIS2 Important Entity. Maintains open-source utility libraries alongside its managed services business. GitHub Actions CI/CD, OIDC-federated npm publishing.

This is deliberately close to a real, common shape of organisation in the European MSP/ISP mid-market — a company that didn't set out to be an open-source maintainer but ended up as one, with a security function mature enough to have OIDC federation and NIS2 obligations but not so large that "who owns this decision" is obvious.

## Roles (full set)

CISO/Security Lead, Dev/Platform Lead, IR/SOC, Communications, Legal/Compliance, Facilitator. Six people, one per role, is ideal — see `facilitator-guide.md` for the collapse pattern at four.

## Group size

**5–8 people.** Below 5, use SME mode instead of trying to stretch MSP mode thin — collapsing roles awkwardly mid-exercise costs more than switching variants cleanly beforehand.

## What doesn't change if you adapt the org

The underlying attack chain — PR → poisoned cache → OIDC extraction → malicious publish → cascade — is the pedagogical spine of the pack and should stay intact regardless of variant. What flexes is organisational context (headcount, regulatory framing, role count), not the technical narrative.

## Adapting the org context without switching to SME mode

If you want to run MSP mode but reskin NorthGate Services to feel closer to your own organisation:

- Keep the regulatory framing (NIS2 IE) unless your real org sits under a different regime — see the note on DORA below.
- Keep OIDC-federated publishing as the technical setup; it's load-bearing for Inject 3's "signed and legitimate, and also compromised" tension.
- Feel free to rename the org, adjust headcount, and swap "open-source utility libraries" for whatever your org's actual externally-consumed software surface is (an internal SDK distributed to customers works just as well).
- **Financial services / DORA framing:** not yet built as a formal variant (see `README.md` roadmap — planned for v1.2). If you need it now, the swap is mechanical: replace NIS2 Art. 23's 24-hour early-warning clock in Inject 3/4 with DORA's equivalent major-incident classification and initial notification timelines, and adjust the regulator's Inject 4 message accordingly. The rest of the pack needs no other change.

## When to prefer MSP mode over SME mode

Use MSP mode whenever the room has (or can plausibly role-play) separation between security leadership, platform engineering, IR/SOC, communications, and legal/compliance — even if in your real organisation some of those sit with the same two or three people day-to-day. The exercise's value comes partly from the friction *between* roles with different priorities; MSP mode preserves that friction even in a smaller real-world team, as long as participants can hold the role distinction for an hour.
