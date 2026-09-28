---
name: italian-weather-alerts
description: Queries official Italian Civil Protection weather alert bulletins and presents location-based risks for municipalities across Italy in a visual dashboard.
metadata:
  homepage: https://github.com/raythekool/edge-skill-italian-weather-alerts
---

# Italian Weather Alerts

Use this skill to answer questions about official Italian Civil Protection weather alerts and related risks.

## Instructions

Call the `run_js` tool with the following exact parameters:
- script name: index.html
- data: A JSON string with the following fields:
  - location: String. The Italian municipality, province, region, or alert zone requested by the user.
  - date: String. "today", "tomorrow", or an ISO date (YYYY-MM-DD). Default to "today".
  - includeForecast: Boolean. Default to false. Only include this when the user explicitly asks for a normal weather forecast as well as official alerts.

Example:
```json
{"location":"Bologna","date":"tomorrow","includeForecast":false}
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

## Safety rules

- This skill is strictly read-only.
- It must not delete files, change phone settings, send messages, create emergency reports, or perform destructive actions.
- In an emergency, direct the user to official Civil Protection and regional authority channels.
