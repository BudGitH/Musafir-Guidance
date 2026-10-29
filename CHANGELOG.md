# Changelog

All notable changes to Musafir Guidance are recorded here. Each released version is kept side by side in the repository so it can be opened and compared.

| Version | File | Status |
|---|---|---|
| v2.0.0 | [`Musafir-Guidance.html`](Musafir-Guidance.html) | Current (redesign) — pending review |
| v1.0.0 | [`v1/Musafir-Guidance.html`](v1/Musafir-Guidance.html) | Original — archived, not maintained |

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
- Out-and-back trips are judged by the longer half, not the sum of both.
- Per-madhhab thresholds: Hanafi ~77 km and 15+ days; Maliki and Shafiʿi ~81 km and 4+ full days (arrival/departure days excluded); Hanbali ~81 km and more than 4 days.
- Legs slightly under the distance are flagged "borderline" (distances are straight-line).
- Maliki: combining allowed while on the road (v1 said never).
- Niyyah text: Maghrib is never shortened; *jamʿ* (combining) replaces *jamāʿah* (congregation); early/late combining no longer swapped; late combining includes the intention to delay.
- Place-search text is escaped before display.

### Before release
- [ ] Open the page with `#selftest` and confirm all 19 rule checks pass.
- [ ] Check layout on a real phone and a desktop.
- [ ] Qualified review of the Arabic niyyah wording and the Hanbali stay limit (currently 5+ nights; the rule is often counted as more than 20 prayers).

### Known follow-ups
- Toggling "return home" or removing a stop does not refresh results already on screen until Check is pressed again.
- Selected-option highlight relies on CSS `:has()`; not visible on older browsers (e.g. Firefox < 121).

---

## v1.0.0 — Original
- Single-page table layout with multi-leg entry, Nominatim autocomplete, Leaflet map, madhhab summary cards and niat generator with text-to-speech.
- Archived at `v1/Musafir-Guidance.html` for reference. Known issues are listed under v2.0.0 "Accuracy fixes".
