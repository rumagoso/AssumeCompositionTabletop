# Reference — The Real Attack Timeline

*Assume Composition — Tabletop Scenario Pack v1.0*

The scenario in this pack is fictional (NorthGate Services doesn't exist). The attack pattern it's built on is not. This is the real-world evidence base, for facilitators who want the ATT&CK IDs to feel grounded rather than memorised, and for anyone who wants to check the pack's premises against primary sources rather than take the pack's word for it.

---

## The TanStack compromise (the pack's primary reference case)

- **10 May 2026** — Attacker stages the payload: a fork repository under the account `voicproducoes`, carrying a `package.json` with a malicious `prepare` lifecycle hook and a ~2.3 MB obfuscated JavaScript payload designed to exit cleanly and leave minimal trace.
- **11 May 2026** — Malicious versions published across 42+ `@tanstack` packages. Compromised tarballs ran roughly 3.7x larger than their clean counterparts. Detected within minutes by automated package-analysis tooling; the compromise itself had already executed.
- **Attack chain, in sequence:**
  1. A `pull_request_target`-triggered workflow gave a fork-originated run access to base-repository context.
  2. GitHub Actions cache poisoning let content written during that run be trusted by a later, legitimately-triggered run.
  3. An OIDC token was extracted from runner process memory during that later run.
  4. The stolen token was used to generate a validly-attested **SLSA Build Level 3** provenance record for a malicious publish — meaning the published package looked cryptographically legitimate, because the pipeline that built it *was* legitimate. What wasn't legitimate was what had been fed into it upstream.
  5. Autonomous propagation: the payload located npm tokens with `bypass_2fa` enabled, enumerated every package under the compromised maintainer, exchanged OIDC tokens for per-package publish credentials, and republished itself across the maintainer's other packages without further human action.
- **Scope:** 84+ malicious versions documented across 42+ packages, spanning TanStack and at least two other maintainers (UiPath, DraftLab) caught in the same wave. Collectively, packages in this family see weekly downloads in the millions.
- **The provenance lesson, stated plainly by the researchers who caught it:** SLSA provenance confirms *which pipeline* produced an artifact. It does not confirm the pipeline was behaving as its owners intended. This is the exact tension Inject 3 in this pack is built to dramatise.

## Same family, earlier and later incidents

The TanStack compromise wasn't an isolated event — it's one documented instance in an ongoing campaign pattern, with related compromises reported against other CI/CD-dependent open-source projects across 2026. Facilitators wanting more texture for the debrief or for Q&A after the exercise should look at reporting from the vendors and researchers who tracked the broader campaign (see `further-reading.md`) rather than treat TanStack as a one-off.

## Where this pack's numbers come from

Every figure above is drawn from public post-incident reporting, not from the pack author's own investigation — this pack's author was not involved in responding to the TanStack compromise. Treat this file as a pointer to primary sources, not as the primary source itself; if you're citing specifics in a talk or a report, go read the original writeups linked in `further-reading.md` and cite those directly.

## The framing gap this pack is built around

MITRE ATT&CK catalogues the individual techniques used in this chain — see `mitre-mapping.md` for the specific IDs — but does not yet have a first-class object representing the *composition* of techniques across a trust boundary into a single named attack pattern. That gap is the thesis this pack exists to make participants feel, not just read about.
