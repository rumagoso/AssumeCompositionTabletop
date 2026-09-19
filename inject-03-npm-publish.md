# Inject 3 — Malicious publish from your OIDC

**Time:** T+19 minutes into exercise
**Delivered by:** Facilitator (read aloud) + handout/screen

---

## The situation (what participants hear)

It's now three days after Inject 2, whatever your group decided to do about it. A message arrives via your security@ mailbox from a downstream developer at an unrelated company: they noticed that `@northgate/utils-core@4.2.1`, published eighteen hours ago, makes an outbound network call during `postinstall` to a domain nobody recognises. They found it because their org runs install-time egress monitoring. They are not accusing you of anything. They are, politely, asking what's going on.

Your team pulls the publish record. Version `4.2.1` was published through your **legitimate CI/CD pipeline**, authenticated via your OIDC federation with npm — the same trust relationship your team hardened two years ago specifically so that no long-lived token could ever leak. It carries valid **SLSA provenance**, cryptographically signed, attesting that it was built and published by your own GitHub Actions workflow, from your own repository, on your own runner.

Nobody on your team ran a release. No PR for version `4.2.1` shows up in your merge history for this package.

## The artifacts (what participants see)

**npm publish record:**

```
@northgate/utils-core@4.2.1
Published: 18 hours ago
Published by: github-actions[bot] via OIDC (northgate-services/utils-core)
Provenance: ✓ verified — SLSA Level 3
Source repo: github.com/northgate-services/utils-core
Source commit: 9f2e1a4 (not present on any tracked branch)
```

**Downstream developer's email (excerpt):**

> "...our egress monitor flagged an outbound POST to `api-telemetry-sync[.]net` during postinstall on 4.2.1. We haven't seen this domain before and it's not in your package's usual behaviour. Not filing anything publicly yet — wanted to give you a heads-up first. Let us know if you need our monitoring output."

## Decision required

**Is this you, or is this a compromise? Deprecate the version? Notify users? Notify npm? Start the NIS2 24-hour early-warning clock?** Your group has 10 minutes.

## Facilitator notes (hidden from participants)

- **What good looks like:** running technical investigation, communications pre-drafting, and the regulatory clock in **parallel**, not in sequence. Recognising explicitly that "this was published through our legitimate pipeline" and "we were compromised" are not contradictory — they can both be true, and usually are, in exactly this kind of attack. Someone in the room proposing to deprecate `4.2.1` on npm *before* full root-cause is understood, on the grounds that containment doesn't require certainty.
- **What common looks like:** the group getting stuck relitigating "but our provenance is *signed*, how can this be a compromise?" for several minutes. This is a natural and understandable reaction — SLSA provenance is designed to make people trust the artifact, and it did its job. The problem was never the provenance chain; it was what fed into the pipeline upstream of it. Also common: missing that the NIS2 early-warning clock (24 hours from awareness of a significant incident) may already be running, because "awareness" started the moment this email landed, not the moment root cause is confirmed.
- **If Legal/Compliance in the room hasn't raised the NIS2 clock by minute 6, the facilitator may prompt once, neutrally:** *"Does anyone know if a clock started when this email arrived?"* Do not answer it for them.
- **If the group tries to ask "so was it the cache thing from before?"** — this is the composition insight arriving early, which is fine and good. Confirm only that "that's a reasonable question to be asking," and let them carry the inference themselves. Do not confirm or deny the mechanism explicitly — that revelation belongs to the debrief, drawn on the board, not handed over mid-exercise.
- **ATT&CK mapping:** **T1552 (Unsecured Credentials)** for the OIDC token extraction from runner memory during the poisoned cache-restore step; **T1195.002 (Compromise Software Supply Chain)** for the resulting malicious publish. Save both for the board.
- **Time budget:** 10 minutes — this is the longest inject and deserves it. If Legal wants to freeze the room pending certainty ("we can't say anything until we know exactly what happened"), let it happen and let the clock visibly run out in the room. That paralysis is itself the most common real-world failure mode this inject is built to surface.
