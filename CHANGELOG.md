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

### Before release
- [ ] Open the page with `#selftest` and confirm all 28 rule checks pass.
- [ ] Check layout on a real phone and a desktop.
- [ ] Qualified review of:
  - the Arabic niyyah wording;
  - the Hanbali stay limit (more than 4 nights; exactly 4 nights shown as borderline, since the rule is often counted as more than 20 prayers);
  - the Hanafi thresholds (~77 km and 15 nights);
  - how multi-stop journeys are measured (farthest straight-line point from the start).

### Known follow-ups
- Selected-option highlight relies on CSS `:has()`; not visible on older browsers (e.g. Firefox < 121).

---

## v1.0.0 — Original
- Single-page table layout with multi-leg entry, Nominatim autocomplete, Leaflet map, madhhab summary cards and niat generator with text-to-speech.
- Archived at `v1/Musafir-Guidance.html` for reference, with an "Outdated" banner and `noindex`. Known issues are listed under v2.0.0 "Accuracy fixes".
