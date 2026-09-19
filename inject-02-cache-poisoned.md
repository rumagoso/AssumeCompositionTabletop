# Inject 2 — Cache anomaly surfaces

**Time:** T+12 minutes into exercise
**Delivered by:** Facilitator (read aloud) + handout/screen

---

## The situation (what participants hear)

Two weeks have passed since Inject 1. Whatever your group decided about PR #412, it is now merged — either because your group approved it, or because (say so plainly if this is the case) the maintainer who actually owns the repo merged it independently while your group was still deciding, because that is what maintainers do.

This morning, a platform engineer doing unrelated cleanup on your GitHub Actions cache usage notices something odd: the build cache for `utils-core` is significantly larger than it should be for a small utility library, and a cache key pattern in the logs doesn't match anything your team's workflows are supposed to write. It looks like it was populated during a `pull_request_target`-triggered run — the kind of run that executes with access to base-repo secrets, not fork-scoped ones.

Nobody has reported anything broken. Nothing downstream has changed behaviour. This is a quiet, easy-to-wave-off anomaly, the kind that shows up in fifty tickets a year and is fifty times benign.

## The artifacts (what participants see)

**Cache inspection output (paraphrased from Actions UI):**

```
Cache: utils-core-docs-preview-a3f9e21
Size: 340 MB          (baseline for this workflow: ~4 MB)
Created: 14 days ago, 09:52 UTC
Created by workflow run: preview-docs.yml
Triggered by: pull_request_target (#412)
Last restored: 3 times since creation, most recently 09:15 UTC today
```

**Engineer's Slack message:**

> "hey — not sure if this is a big deal but the docs-preview cache for utils-core is like 80x bigger than it should be? and the key says it came off that PR from a couple weeks back, the typo-fix one. probably nothing but flagging."

## Decision required

**How do you scope this? Who do you bring in? Do you rebuild without the cache, or investigate first?** Your group has 7 minutes.

## Facilitator notes (hidden from participants)

- **What good looks like:** treating an oversized, unexplained cache artifact tied to a `pull_request_target` run as potentially adversarial *by default*, not as a curiosity to resolve later. Asking who — or what identity — had write access to that cache during the run. Asking whether any subsequent workflow run *restored* that cache (it has — three times, including this morning) and what that run had access to.
- **What common looks like:** treating this as a benign misconfiguration or storage bloat issue. "Let's just clear the cache and move on" without asking what the cache may have already fed into. This is the single most consequential decision point in the exercise, and it usually doesn't feel like one.
- **The trap, explicitly:** a `pull_request_target` workflow run from a fork PR executes with base-repo permissions but can be influenced by fork content. If that run's cache step wasn't scoped correctly, a forked contributor's code could have written arbitrary content into a cache key that a *legitimate, secret-bearing* later workflow run then restores and trusts. The size anomaly is the tell. Nobody in the room needs to know this mechanism by name to make the right call — they just need to treat "unexplained + touches a sensitive trigger + already restored three times" as urgent.
- **If the group wants to "just rebuild without the cache":** let them decide that's the fix and move on if that's their call — but note explicitly for the debrief that this treats the *symptom* (bad cache) without answering the *question* (what did the cache already touch, and was anything read from it into a context with real credentials).
- **ATT&CK mapping:** **T1677 — Poisoned Pipeline Execution.** Do not name it aloud. It goes on the board in the debrief, not here.
- **Time budget:** 7 minutes. If the group defaults to "not our department, ping the engineer to sort it," let that stand — it's a realistic and very common outcome, and it's exactly the kind of thing Pass 3 of the debrief exists to surface.
