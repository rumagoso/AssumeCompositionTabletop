# Variant — SME Mode

*Assume Composition — Tabletop Scenario Pack v1.0*

Use this variant for a small or medium-sized organisation with a minimal or shared security function — a 10–50 person shop where "the security team" is two people who also do other jobs. Same pedagogical payload as MSP mode, same four injects, same debrief. What changes is org context, role count, and a couple of injects' framing details.

---

## Adjusted organisation

Replace NorthGate Services (~200 people) with a **30-person software shop** — call it whatever fits your room, or keep it generic as "the company." Same shape of exposure: it maintains at least one small, widely-depended-on open-source library or SDK as a side effect of its main product, and publishes via GitHub Actions with OIDC-federated npm publishing. The regulatory framing can stay NIS2-adjacent if participants are EU-based and plausibly in scope as an Important or Essential Entity depending on sector — but don't force NIS2 onto a room where it clearly wouldn't apply. If your SME room isn't under any specific regulatory framework, soften Inject 3/4's regulator thread to "your cyber insurer's incident-notification clause" or "your largest customer's contractual breach-notification SLA" — the mechanic (a clock started by awareness, not by root-cause certainty) is what matters, not which specific regime triggers it.

## Collapsed roles

MSP mode's six roles become **three:**

| SME role | Absorbs |
|---|---|
| **Owner** | CISO/Security Lead + Legal/Compliance — the person who has to decide *and* worry about the regulatory/contractual consequences, because in a 30-person company that's usually the same conversation happening in the same person's head |
| **Tech Lead** | Dev/Platform Lead + IR/SOC — the person who both built the pipeline and has to triage what's wrong with it, because there usually isn't a separate incident-response function to hand off to |
| **External Comms** | Communications, largely unchanged — though in many SMEs this role is played by the Owner too. If your room only has 2–3 people, collapse Comms into Owner as a last resort and say so plainly when assigning roles |

## Group size

**3–5 people.** Three is the practical floor — below that, the role friction that makes the debrief land (Pass 2 and Pass 3 depend on the group having made genuinely different-flavoured decisions to look back on) gets too thin to work with.

## Inject adjustments

The four injects run as written, with two framing notes for the facilitator:

- **Inject 1 (the PR):** unchanged. A small shop maintaining even one open-source library still gets outside contributors; the trap works identically.
- **Inject 3 (the publish) and Inject 4 (the cascade):** dial the *scale* language down if it strains plausibility for your room. "12 million weekly downloads" and "three enterprise customers on the phone" can be read aloud as-is if your group can suspend disbelief for an hour (recommended — the scale is part of what makes the stakes felt), or softened to a number and cast that fits your actual audience's world more closely: fewer downloads, one or two concerned customers rather than three, a local trade-press contact rather than a named security journalist. The *mechanism* of the cascade — customer pressure, press inquiry, regulator or contractual clock, all arriving Friday afternoon before anyone has full scope — is what needs to survive the resize, not the specific numbers.

## What doesn't change

The technical attack chain, the composition map in the debrief, and Pass 3's "what didn't happen" question are identical to MSP mode. The pedagogical payload — that individually reasonable decisions inside each of T1677/T1552/T1195.002 don't add up to a decision about the composition — doesn't depend on org size, and shouldn't be diluted for a smaller room. If anything, it lands harder in a small team, where "we don't have a separate person for that" is a more honest and more common starting condition than in a 200-person MSP.
