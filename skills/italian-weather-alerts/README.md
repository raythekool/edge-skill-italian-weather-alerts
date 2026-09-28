# 🇮🇹 Italian Weather Alerts Skill

This folder contains the initial Google AI Edge Gallery JavaScript skill.

## Structure

- `SKILL.md` — Agent Skills metadata and instructions.
- `scripts/index.html` — Edge Gallery `run_js` entry point.
- `assets/webview.html` — inline visual dashboard.
- `assets/demo-data.json` — clearly labeled development fixture.

## Loading in Edge Gallery

Host this folder on a true static web host such as GitHub Pages, Cloudflare Pages, or another service that serves Markdown and JavaScript with suitable MIME types. Do not use a normal GitHub repository URL or `raw.githubusercontent.com` as the JS skill host.

Load the URL of the skill folder, for example:

```text
https://<username>.github.io/edge-skill-italian-weather-alerts/skills/italian-weather-alerts/
```

The repository must contain `.nojekyll` so GitHub Pages serves `SKILL.md` without Jekyll conversion.

## Current limitations

- Live official-data ingestion is not configured yet.
- The bundled data is fictional and exists only to validate the UI flow.
- The map is a visual placeholder; production geometry and zone mapping are still required.
- The skill is read-only and does not use device location automatically.
