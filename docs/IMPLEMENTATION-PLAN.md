# Implementation plan — Musafir Guidance v2.1

Branch: `redesign/modern-refresh` (PR #1). Two commits, then the PR is updated for review.

## Goals
1. Bring every rule in the app in line with the verified sources in
   [`FIQH-RULE-VERIFICATION.md`](FIQH-RULE-VERIFICATION.md), and say plainly what is still unverified.
2. Make the page more elegant: calmer visual hierarchy, clearer results, fewer competing elements,
   without changing the fiqh logic or breaking the 28 self-tests.

## Requirements

### R1 — Rule wording (commit 1; two one-line JS labels carried into commit 2)
| # | Requirement | Where |
|---|---|---|
| R1.1 | Hanafi residence label reads "15 days or more" (the app counts nights as a proxy; the sources say days). | notes (done); `MADHHABS.hanafi.residentShort` (commit 2) |
| R1.2 | Hanafi distance note: 48 English miles ≈ 77 km is the majority view; scholars using the sharʿi mile give up to ≈ 95 km. Overall range shown as 77–95 km. | notes (done) |
| R1.3 | Maliki combining: permitted while actually on the road, or when there is a need such as illness or rain; not during an ordinary stay. | notes (done); `MADHHABS.maliki.jamText` (commit 2) |
| R1.4 | Note on undecided stays: Shafiʿi may keep shortening up to 18 days when departure could come any moment; Hanafi stays a traveller until firmly intending 15 days in one place. | notes (done) |
| R1.5 | Distance is measured one way along the route, never as a round trip; straight-line is a conservative lower bound. | notes (done) |
| R1.6 | Unverified items listed in CHANGELOG "Before release": Arabic niyyah wording; multi-stop "farthest point" rule; Maliki vs Shafiʿi day-count start/end. | CHANGELOG (done) |
| R1.7 | No change to thresholds, residence tests or self-test expectations. | — |

### R2 — UX / UI refresh (commit 2)
| # | Requirement |
|---|---|
| R2.1 | Typography: a display serif for headings (paired with the existing Amiri for Arabic), tighter heading scale, more generous line-height in body copy. |
| R2.2 | Hero header with a short tagline and a subtle gradient; brand mark refined. |
| R2.3 | Stepper: steps numbered with a thin progress rail on desktop; cards get softer shadows and a hairline top accent. |
| R2.4 | Form: resolved-place chip (name + country) under each input; nights shown inline as a pill. |
| R2.5 | Results: per-madhhab summary cards get a coloured left rail by status (ok / partly / full); timeline uses a continuous rail with stay nodes filled and leg nodes outlined. |
| R2.6 | Badges: consistent iconography (✓ qasr, ⇄ jamʿ, ! borderline, ● full); never more than three badges per rule row. |
| R2.7 | Map card: rounded with inset shadow; legend line under it. |
| R2.8 | Niyyah card: Arabic in a bordered panel with larger leading; English below in muted text; speech buttons as icon-first pills. |
| R2.9 | Motion: fade/slide of results on reveal, respecting `prefers-reduced-motion`. |
| R2.10 | Accessibility unchanged or better: focus rings, contrast ≥ 4.5:1 in both themes, all controls ≥ 44 px tall. |
| R2.11 | No change to any JS logic beyond class names, markup and the two R1 labels; 28 self-tests still pass. |

### R3 — Review (after commit 2)
- Update the PR #1 description: commits, rule changes, UI changes, test count, open fiqh items.
- Request review.

## Verification
- Open `Musafir-Guidance.html#selftest` → expect 28/28.
- Check layout at 360 px, 768 px and 1280 px, light and dark.
- Scholar review of the open items in `FIQH-RULE-VERIFICATION.md` §6.

## Out of scope
- Changing the fiqh thresholds or residence tests.
- New madhhabs or the Imami 10-day rule.
- Road-distance routing.
