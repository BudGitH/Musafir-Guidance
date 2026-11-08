# Changelog

All notable changes to Musafir Guidance are recorded here. Each released version is kept side by side in the repository so it can be opened and compared.

| Version | File | Status |
|---|---|---|
| v2.0.0 | [`Musafir-Guidance.html`](Musafir-Guidance.html) | Current (redesign) — pending review |
| v1.0.0 | [`v1/Musafir-Guidance.html`](v1/Musafir-Guidance.html) | Original — archived and marked outdated (banner + `noindex`), not maintained |

The current version always lives at `Musafir-Guidance.html`, so existing links and bookmarks open the latest release. Older versions live in `vN/` folders.

---

## v2.0.0 — Modern refresh

### Design and usability
- Card-based layout replaces the 6-column table, popups and loading modal.
- Mobile-first: large tap targets, no iOS zoom on inputs, sticky "Check my journey" button on phones.
- Automatic dark mode (follows the device setting).
- Madhhab selector (single madhhab or compare all four); choice is remembered.
- Arrive / leave dates instead of typed day counts, so nights are calculated exactly.
- Keyboard-friendly place search (Photon, falling back to Nominatim).
- Inline field errors and a visible banner for network problems (previously console-only).
- Trip saved in the browser between visits.
- Leaflet 1.7.1 → 1.9.4, CARTO tiles, numbered map pins.

### Accuracy fixes
- Whole-trip logic: short hops between stops count as one journey; a long stay makes you resident and the next departure starts a new journey.
- Each journey is judged by the farthest straight-line point it reaches from where it began. Hops are never added up, so a zig-zag trip can't qualify by accident; when the hops do add up past the distance, the leg is flagged "road distance may qualify".
- Out-and-back trips are judged by how far you get, not the sum of both halves.
- Per-madhhab thresholds: Hanafi ~77 km and 15+ nights; Maliki and Shafiʿi ~81 km and 4+ full days (arrival/departure days excluded); Hanbali ~81 km and more than 4 nights, with exactly 4 nights shown as borderline (it depends on arrival and departure times).
- Legs slightly under the distance are flagged "borderline" (distances are straight-line).
- Maliki: combining allowed while on the road (v1 said never); the "on the road only" note also shows when comparing all four.
- Niyyah text: Maghrib is never shortened; *jamʿ* (combining) replaces *jamāʿah* (congregation); early/late combining no longer swapped; late combining includes the intention to delay.
- Place-search text is escaped before display.

### Review fixes (PR #1)
- Farthest-point distance rule for multi-stop journeys (see above). The old "two 50 km hops qualify" test now uses stops in a straight line, and a zig-zag test was added.
- Hanbali: a 4-night stay is marked Borderline instead of silently "traveller".
- Hanafi residence label corrected to "15+ nights".
- Editing the trip (return home, adding or removing a stop, dates, places) hides the old results and shows "Out of date — check again".
- Saved trips are checked on load: unknown madhhab values fall back to "All four", missing fields are filled in, unsafe stop ids are replaced, and stop ids are escaped in the form.
- Typed places: the full matched name is shown, and when several places match you are asked to choose from the list instead of the first result being used silently.
- Self-tests: 19 → 28 (Hanbali 4 nights, zig-zag trip, long stay at the last stop on a return trip, Maliki "no jamʿ while staying", saved-data checks).
- v1 page marked outdated with a banner and `noindex`.

### Rule verification (8 Nov)
Every threshold and ruling was checked against published sources; see [`docs/FIQH-RULE-VERIFICATION.md`](docs/FIQH-RULE-VERIFICATION.md) for the findings and full links. Wording changes that came out of it:
- Hanafi residence: "15 days or more" (sources say days; the app counts nights between your dates).
- Hanafi distance note: 48 English miles ≈ 77 km is the majority view; up to ≈ 95 km with the sharʿi mile. Range shown as 77–95 km.
- Distance is measured one way along the route, never as a round trip.
- Maliki combining: on the road, or when there is a need such as illness or rain; not during an ordinary stay.
- New note on undecided stays (Shafiʿi up to 18 days when departure could come any moment; Hanafi until 15 days in one place is firmly intended).
- Thresholds, residence tests and the 28 self-tests are unchanged.

Implementation plan for this and the UI refresh: [`docs/IMPLEMENTATION-PLAN.md`](docs/IMPLEMENTATION-PLAN.md).

### Before release
- [ ] Open the page with `#selftest` and confirm all 28 rule checks pass.
- [ ] Check layout on a real phone and a desktop.
- [ ] Qualified review of the open items in `docs/FIQH-RULE-VERIFICATION.md` §6:
  - the Arabic niyyah wording (no source found yet);
  - how multi-stop journeys are measured (farthest straight-line point from the start);
  - whether the Maliki "20 prayers" and Shafiʿi "4 full days" counts start and end the same way.
- [ ] Already source-confirmed, still worth a scholar's glance: Hanbali more-than-20-prayers rule with 4 nights as borderline; Hanafi ~77 km and 15 days.

### Known follow-ups
- Selected-option highlight relies on CSS `:has()`; not visible on older browsers (e.g. Firefox < 121).

---

## v1.0.0 — Original
- Single-page table layout with multi-leg entry, Nominatim autocomplete, Leaflet map, madhhab summary cards and niat generator with text-to-speech.
- Archived at `v1/Musafir-Guidance.html` for reference, with an "Outdated" banner and `noindex`. Known issues are listed under v2.0.0 "Accuracy fixes".
