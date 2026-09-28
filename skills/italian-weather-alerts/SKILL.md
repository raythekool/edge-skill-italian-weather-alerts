---
name: italian-weather-alerts
description: Queries official Italian Civil Protection weather alert bulletins and presents location-based risks for municipalities across Italy in a visual dashboard. Use when the user asks about Italian weather alerts, Civil Protection warnings, alert levels, hydrogeological or hydraulic risk, thunderstorms, or risks affecting an Italian location.
compatibility: Designed for Google AI Edge Gallery JavaScript skills. Requires internet access for current official data. Read-only; no destructive device actions.
license: MIT
metadata:
  author: Marco Dodaro
  version: "0.1.0"
  homepage: https://github.com/raythekool/edge-skill-italian-weather-alerts
  data-scope: Italy
---

# Italian Weather Alerts

Use this skill to answer questions about official Italian Civil Protection weather alerts and related risks.

## Required execution

Call the `run_js` tool using:

- script name: `index.html`
- data: a JSON string with:
  - `location`: the Italian municipality, province, region, or alert zone requested by the user. String.
  - `date`: `today`, `tomorrow`, or an ISO date (`YYYY-MM-DD`). Default to `today`.
  - `includeForecast`: Boolean. Default to `false`. Only include this when the user explicitly asks for a normal weather forecast as well as official alerts.

Example:

```json
{"location":"Bologna (BO)","date":"tomorrow","includeForecast":false}
```

## Response requirements

1. Use the returned structured result as the source of truth for alert levels, risks, dates, timestamps, and source links.
2. Clearly distinguish official Civil Protection alerts from ordinary weather forecasts.
3. State the resolved municipality, province, region, and alert zone when available.
4. Report every relevant risk separately. Do not collapse all risks into one color if the data contains multiple risk types.
5. Mention bulletin issue time, data retrieval time, validity period, and freshness status.
6. If the location is ambiguous, ask the user for the province or region instead of guessing.
7. If data is unavailable, stale, incomplete, or only demo data is available, say so prominently.
8. Never invent an alert level, risk, location-to-zone mapping, date, timestamp, or official source.
9. Never describe a generic forecast as an official alert.
10. Include the returned webview when present.

## Data and safety rules

- This skill is read-only.
- It must not delete files, change phone settings, send messages, create emergency reports, or perform destructive actions.
- Current data must come from official sources configured in the script or normalized dataset.
- During development, the script may use clearly labeled demo data when live data is not configured; it must never present demo values as live alerts.
- In an emergency, direct the user to official Civil Protection and regional authority channels.

## Examples

- “Are there any alerts tomorrow in Bologna?”
- “What is the Civil Protection risk in Vaiano, Prato?”
- “Show Italian orange and red alerts today.”
- “What is the difference between the alert and tomorrow’s forecast in Milan?”
