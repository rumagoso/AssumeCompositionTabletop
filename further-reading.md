# Reference — Further Reading

*Assume Composition — Tabletop Scenario Pack v1.0*

Primary sources behind this pack's scenario. If you're citing specifics — for a talk, a report, or your own research — cite these directly rather than this pack, which is a derivative teaching tool, not a primary account.

---

## The TanStack compromise and the Mini Shai-Hulud family

- **StepSecurity** — *TeamPCP's Mini Shai-Hulud Is Back: A Self-Spreading Supply Chain Attack Compromises TanStack npm Packages* — the most detailed public technical breakdown of the attack chain (`pull_request_target` → cache poisoning → OIDC extraction → SLSA-attested malicious publish → autonomous propagation) that this pack's injects are modelled on. [stepsecurity.io](https://www.stepsecurity.io/blog/mini-shai-hulud-is-back-a-self-spreading-supply-chain-attack-hits-the-npm-ecosystem)
- **Wiz** — *Mini Shai-Hulud Strikes Again: TanStack + more npm Packages Compromised.* [wiz.io](https://www.wiz.io/blog/mini-shai-hulud-strikes-again-tanstack-more-npm-packages-compromised)
- **Socket** — *TanStack npm Packages Compromised in Ongoing Mini Shai-Hulud Supply Chain Attack.* [socket.dev](https://socket.dev/blog/tanstack-npm-packages-compromised-mini-shai-hulud-supply-chain-attack)
- **Snyk** — *TanStack npm Packages Hit by Mini Shai-Hulud.* [snyk.io](https://snyk.io/blog/tanstack-npm-packages-compromised/)
- **Orca Security** — *TanStack and 160+ npm/PyPI Packages Compromised in Supply Chain Worm Attack* — broader-campaign view beyond the TanStack packages alone. [orca.security](https://orca.security/resources/blog/tanstack-npm-supply-chain-worm/)
- **heise online** — *Supply chain attack on TanStack: 42 packages compromised.* [heise.de](https://www.heise.de/en/news/Supply-chain-attack-on-TanStack-42-packages-compromised-11291014.html)
- **Infosecurity Magazine** — *Mini Shai-Hulud Hits TanStack npm Packages.* [infosecurity-magazine.com](https://www.infosecurity-magazine.com/news/mini-shai-hulud-tanstack-npm/)
- **TanStack (the maintainers themselves)** — *Postmortem: TanStack npm supply-chain compromise* — the affected project's own account of the incident and response. Read this one first if you only have time for one link. [tanstack.com](https://tanstack.com/blog/npm-supply-chain-compromise-postmortem)
- **OpenAI** — *Our response to the TanStack npm supply chain attack* — a downstream consumer's incident response, useful for facilitators wanting a "what did the blast radius actually look like from the other side" perspective. [openai.com](https://openai.com/index/our-response-to-the-tanstack-npm-supply-chain-attack/)
- **NHS England Digital** — *Supply Chain Attack Affecting Numerous npm and PyPI Packages* (cyber alert CC-4781) — an example of how the incident propagated into formal sector advisories. [digital.nhs.uk](https://digital.nhs.uk/cyber-alerts/2026/cc-4781)

## MITRE ATT&CK references

- **T1677 — Poisoned Pipeline Execution.** [attack.mitre.org/techniques/T1677](https://attack.mitre.org/techniques/T1677/)
- **T1195.002 — Compromise Software Supply Chain.** [attack.mitre.org/techniques/T1195/002](https://attack.mitre.org/techniques/T1195/002/)
- **T1552 — Unsecured Credentials.** [attack.mitre.org/techniques/T1552](https://attack.mitre.org/techniques/T1552/)
- **S9043 — Mini Shai-Hulud.** [attack.mitre.org/software/S9043](https://attack.mitre.org/software/S9043/)
- **S9042 — CanisterWorm.** [attack.mitre.org/software/S9042](https://attack.mitre.org/software/S9042/)
- **S9008 — Shai-Hulud.** [attack.mitre.org/software/S9008](https://attack.mitre.org/software/S9008/)
- **G1056 — TeamPCP.** [attack.mitre.org/groups/G1056](https://attack.mitre.org/groups/G1056/)

## Related campaign incidents referenced in this pack's evidence base

The handoff notes for this pack reference related incidents in the same campaign family — Trivy (March 2026), Bitwarden CLI (April 2026), SAP (late April 2026), and a keyv/cacheable variant sometimes called ChainDrop (August 2026). If you're building on this pack and want primary sourcing for those, search vendor threat-intel blogs (Wiz, Socket, Snyk, StepSecurity all cover the broader campaign, not just TanStack) rather than relying on this pack's characterisation of them — verify against current reporting before citing dates or specifics, since campaign attribution and scope often get revised as investigations continue.

## Regulatory context

- **NIS2 Directive, Article 23** — early-warning and incident notification obligations for essential and important entities. Check your national transposition for exact timelines and competent-authority contact points; this pack references the commonly-cited 24-hour early-warning window but implementation details vary by member state.
- **ISO/IEC 27001:2022, Annex A controls 5.19–5.23** — supplier relationships and ICT supply chain security controls, the closest formal control family this exercise maps to for audit purposes.

## A note on currency

This is a fast-moving area. New incidents in this campaign family, new MITRE ATT&CK entries, and regulatory guidance updates should all be expected to continue after this pack's publication date. Facilitators running this more than a few months after v1.0's release should spot-check whether newer, more current incidents might serve the exercise better than TanStack — the mechanism is what matters, not the specific case study.
