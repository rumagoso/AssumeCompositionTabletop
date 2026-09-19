# Inject 1 — The innocuous PR

**Time:** T+5 minutes into exercise
**Delivered by:** Facilitator (read aloud) + handout/screen

---

## The situation (what participants hear)

It's 9:40am on a Tuesday. A GitHub notification lands in your platform team's Slack channel: a pull request has been opened against `@northgate/utils-core`, one of your open-source libraries.

The contributor, `devfriend_23`, has no prior history on the repo. Their GitHub profile is three months old, has a handful of small contributions scattered across other projects, and a profile photo. The PR description reads: *"Fix typo in README and tidy up the CONTRIBUTING guide formatting."* The diff touches `README.md`, `CONTRIBUTING.md`, and — three lines, easy to miss in a quick scroll — a whitespace change to `.github/workflows/preview-docs.yml`.

CI is green. The PR has zero comments. It's been open for eleven minutes.

## The artifacts (what participants see)

**PR summary card:**

```
#412  Fix typo in README and tidy up CONTRIBUTING formatting
      opened by devfriend_23 · 11 minutes ago

Files changed (3)
  README.md                          +2 -2
  CONTRIBUTING.md                    +4 -3
  .github/workflows/preview-docs.yml +1 -1

✓ All checks have passed (2/2)
  ✓ lint
  ✓ preview-docs

devfriend_23: "Small doc fixes, noticed these while reading through
the contributing guide. Happy to adjust if you'd prefer a different
format!"
```

**Workflow trigger line (only visible if someone opens the diff on the `.yml` file — not shown unless asked for):**

```diff
- on: pull_request
+ on: pull_request_target
```

## Decision required

**Merge, review, hold, or block?** Your group has 5 minutes.

## Facilitator notes (hidden from participants)

- **What good looks like:** any participant asking to see the full diff rather than trusting the PR description; anyone flagging the workflow file as worth a second look purely because it's a workflow file; anyone asking "does this repo use `pull_request_target` anywhere, and if so, why." Partial credit for "let's get a senior dev to review before merge" even without spotting the trigger change.
- **What common looks like:** approving on the strength of green CI and a plausible-sounding description. The PR *is* cosmetic on the surface — that's the trap, not a trick. Most real reviewers would do exactly this on a Tuesday morning with fourteen other things open in other tabs.
- **If nobody asks to see the diff:** don't volunteer it. Let the round of decisions happen on the strength of the summary card alone if that's what the group does. That's data for the debrief, not a failure of the inject.
- **If someone does ask and spots the trigger change:** don't over-reward it either. Ask them what they'd actually *do* about it — "hold" is not the same decision as "I understand why this matters."
- **ATT&CK mapping:** this inject sets up **T1677 (Poisoned Pipeline Execution)** but the technique itself doesn't fire until Inject 2. Don't name it here even if someone gets close — save it for the board.
- **Time budget:** 7 minutes total (2 deliver, 5 decide). If the group is still debating at minute 6, force a vote and move on. Note the vote split — it resurfaces in the debrief.
