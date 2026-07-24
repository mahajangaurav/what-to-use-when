# Contributing to What to Use When

Thanks for helping improve this skill! The goal is **consistent, correct routing** between the free
Microsoft 1P Copilot agents and Cowork.

## Ways to contribute

- **New trigger scenarios** — the most valuable contribution. Open an issue with:
  - the user phrasing,
  - the tool it *should* route to (or "should NOT fire — this is a direct action / multi-output job"),
  - why.
- **Routing corrections** — cases where the skill recommends the wrong tool.
- **Docs & screenshots** — clearer deployment steps, real screenshots for `docs/screenshots/`.

## Editing the skill

The skill is a single file: [`skill/what-to-use-when/SKILL.md`](skill/what-to-use-when/SKILL.md).

Please keep these invariants:

1. **Triggers live in the `description`.** That is what the router reads. Add trigger *phrases* there;
   keep long explanation in the body.
2. **Stay under the description limit.** Cowork enforces a **1,024-character** limit on the JSON-escaped
   description. Keep it a folded scalar (`>-`) and plain ASCII; target ≤ ~1,000 escaped characters for
   headroom.
3. **No pricing in user-facing output.** Never add credit counts, dollar amounts, or cost estimates.
4. **Keep the precedence rule intact** — the skill must fire *before* retrieval, task creation, or file
   generation.
5. **Don't gate direct actions** (send email, schedule meeting, post to Teams, create event) and don't
   block genuinely multi-output Cowork jobs.

## Testing a change

Before opening a PR, sanity-check triggering with a small labeled set: 3–5 prompts that **should** fire
and 2–3 that **should not** (the negatives are the valuable part). Confirm the should-not cases stay
silent. Include your results in the PR description.

## Pull requests

- One logical change per PR.
- Update `CHANGELOG.md` with a short entry.
- Describe the trigger/behavior impact and any test results.
