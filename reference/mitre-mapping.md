# Reference — MITRE ATT&CK Mapping

*Assume Composition — Tabletop Scenario Pack v1.0*

The three techniques this pack maps to in the debrief, plus the catalogued threat group and software families the real-world attack chain is associated with. Facilitators: read this once before running the debrief so the IDs feel grounded when you write them on the board — see `debrief.md` for how and when to introduce them.

---

## The three techniques

### T1677 — Poisoned Pipeline Execution
**Created:** 22 May 2025 · **Last modified:** 12 May 2026 (the day after the TanStack compromise)

Covers adversaries injecting malicious code into a CI/CD build process — direct modification of CI configuration, injection via referenced files (makefiles, scripts), or exploitation of pull-request-triggered workflows to reach pipeline secrets. In this pack's scenario, this is the technique underlying Injects 1 and 2: the `pull_request_target` trigger and the subsequent cache poisoning.

**Related technique:** links to T1195 (Supply Chain Compromise), since poisoned pipelines are a mechanism for injecting components that ship downstream — which is exactly the join this pack's composition map is built to draw explicitly.

### T1552 — Unsecured Credentials
Covers adversaries searching for and extracting credentials — including tokens — accessible in memory, files, or other insecure storage on a compromised system. In this pack's scenario, this is the technique underlying the moment inside Inject 3's backstory where the OIDC token is extracted from runner process memory during a later, legitimately-triggered workflow run that unknowingly restores the poisoned cache.

### T1195.002 — Compromise Software Supply Chain
A sub-technique of T1195 (Supply Chain Compromise), covering manipulation of software prior to receipt by the end consumer, including compromise of the source code, build process, or update mechanism of legitimate software. In this pack's scenario, this is the technique underlying the malicious publish in Inject 3 — a real, validly-signed release from the organisation's own legitimate pipeline, carrying a payload nobody on the team authored.

---

## Catalogued threat group and software (real-world context, not part of the fictional scenario)

These are documented by MITRE and referenced in the pack's `README.md` and `HANDOFF` material as the real-world basis for the attack pattern. They are **not** named inside the fictional NorthGate Services scenario itself — the injects deliberately don't reference them, so participants engage with the mechanism rather than pattern-matching to a known incident name.

- **G1056 — TeamPCP.** MITRE-catalogued threat group associated with compromising trusted CI/CD pipelines, including injecting credential-stealing payloads into widely-used security tooling.
- **S9043 — Mini Shai-Hulud.** MITRE-catalogued software, associated with propagation via GitHub Actions-triggered workflows — the family this pack's scenario is modelled on.
- **S9042 — CanisterWorm.** MITRE-catalogued software, associated with autonomous propagation across dozens of npm packages using stolen publish tokens.
- **S9008 — Shai-Hulud.** The earlier, related malware family that created malicious GitHub workflows within compromised accounts — the lineage Mini Shai-Hulud extends.

---

## The gap this pack names

MITRE's catalogue is a catalogue of parts. T1677, T1552, and T1195.002 are each real, well-documented, independently useful entries. What the catalogue does not yet provide is a first-class object for the *chain across them* — the composition itself, as a named, referenceable pattern distinct from its individual links. This pack's fourth box on the debrief board — drawn empty, deliberately — is where that gap becomes visible to participants rather than remaining an abstract argument. See `debrief.md`, Pass 2, for the exact script.

This is also the substance of the companion one-pager referenced in this pack's `README.md` roadmap: a proposal for how ATT&CK-adjacent frameworks might represent chained compositions as first-class objects, using this attack family as the reference implementation. That one-pager is a separate deliverable from this tabletop pack.
