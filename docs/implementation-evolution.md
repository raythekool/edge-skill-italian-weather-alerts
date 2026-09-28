# 🧭 Implementation evolution proposal

This document describes a staged evolution from the current visual concept to a reliable Google AI Edge Gallery skill covering Italy.

## Phase 0 — Concept and UI validation

- Reproduce the attached mobile mockup as a responsive HTML/CSS dashboard.
- Validate inline webview rendering in Google AI Edge Gallery on iPhone.
- Test Italian text, long risk descriptions, accessibility, dark mode, and narrow screens.
- Keep all displayed alert values clearly marked as fictional until the data pipeline exists.

## Phase 1 — National data contract

Define a small, stable normalized JSON contract independent from the original source formats.

Suggested fields:

- `schemaVersion`
- `generatedAt`
- `sourceUrls`
- `bulletinIssuedAt`
- `validFrom`
- `validTo`
- `zones[]`
- `zones[].id`
- `zones[].name`
- `zones[].region`
- `zones[].geometry`
- `zones[].risks[]`
- `zones[].risks[].type`
- `zones[].risks[].level`
- `zones[].risks[].description`
- `dataQuality.status`
- `dataQuality.warnings[]`

Use explicit levels such as `none`, `yellow`, `orange`, and `red`; do not encode severity only as a color.

## Phase 2 — Decentralized on-demand data ingestion

- Query the national Civil Protection repository (`pcm-dpc/DPC-Bollettini-Criticita-Idrogeologica-Idraulica`) directly from the client JS runtime.
- Fetch the daily lightweight summary JSON (~3 KB) on-demand without intermediate servers or private GitHub Actions.
- Parse `html_descrition` to extract risks, severity levels (none, yellow, orange, red), and affected regions/zones.
- Retrieve the official daily national criticality map preview image (`files/preview/YYYYMMDD_HHMM_oggi.png` and `domani.png`).
- Implement client-side `sessionStorage`/`localStorage` caching so multiple queries in a session do not repeat network calls.
- Maintain a graceful fallback to local fixtures when offline or if network limits are reached.

## Phase 3 — Italy-wide geographic resolution

- Build or import a maintained municipality-to-alert-zone mapping for all Italian regions and autonomous provinces.
- Store municipality name, province, region, coordinates, and zone identifier.
- Require province or region when a municipality name is ambiguous.
- Add tests for border municipalities and special administrative cases.
- Never silently map a municipality when the match is uncertain.

## Phase 4 — Edge Gallery skill

Implement the skill using the Edge Gallery conventions:

- `SKILL.md` describes when the skill should activate and its safety rules.
- `scripts/index.html` performs the minimal data retrieval and filtering.
- Return concise structured JSON to the local model.
- Return an inline webview dashboard for visual output.
- Pass only small identifiers or query parameters to the dashboard URL.
- Keep the model responsible for explanation, not for calculating alert severity.

## Phase 5 — Visual dashboard

Implement the mockup as a responsive, dependency-light interface:

- High-visibility alert summary banner.
- Separate risk cards for each risk type.
- Today/tomorrow selector.
- Municipality and alert-zone labels.
- Italy-wide map with selectable zones.
- Details and map tabs.
- Bulletin issue time, retrieval time, freshness badge, and source link.
- Explicit states for no alert, unavailable data, stale data, ambiguous location, and partial coverage.
- Text and icons in addition to color for accessibility.

The interface should not present a forecast as an official alert and should always show a fictional/demo state in development builds.

## Phase 6 — Quality, resilience, and security

- Validate all downloaded JSON before publishing it.
- Use schema validation and fail closed when required fields are missing.
- Add automated tests for dates, severity ordering, risk grouping, and location filtering.
- Add a freshness threshold and visible stale-data warnings.
- Minimize downloaded payload size for mobile use.
- Avoid third-party analytics and unnecessary network requests.
- Do not store precise user location unless the user explicitly chooses to do so.
- Keep the skill read-only: it must not send messages, create emergency reports, or modify phone files.

## Phase 7 — Operational improvements

- Add monitoring for failed ingestion runs.
- Publish a small status document with last successful update and source health.
- Add a manual refresh action.
- Cache the last known dataset and label it clearly when offline.
- Consider optional weather forecasts as a separate section, never mixed with official alert levels.
- Add regional source links for deeper explanations without making them mandatory for national coverage.

## Definition of done for the first usable release

- All Italian alert zones are represented.
- A municipality can be resolved deterministically or the user is asked to clarify.
- The latest valid official bulletin is selected reproducibly.
- Today and tomorrow queries return source-backed results.
- The dashboard renders inside Edge Gallery on iOS.
- No-alert, stale-data, unavailable-data, and ambiguous-location states are tested.
- Documentation includes installation, limitations, sources, and the emergency-information disclaimer.
