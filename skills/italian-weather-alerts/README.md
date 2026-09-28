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

## Features & Data Sources

- **Live Official Ingestion**: Queries the official DPC Open Data repository (`pcm-dpc/DPC-Bollettini-Criticita-Idrogeologica-Idraulica`) directly on-demand via client-side fetch.
- **Zero Backend Required**: No private server or cron job needed; users fetch the latest ~3 KB official bulletin directly.
- **Official National Map**: Dynamically embeds the official Civil Protection alert map preview inside the WebView dashboard.
- **Local Fallback**: Automatically falls back to bundled fixtures (`assets/demo-data.json`) if offline or network requests fail.
- **Privacy & Read-Only**: The skill is strictly read-only and does not track personal user location.
