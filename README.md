# <img src="skills/italian-weather-alerts/assets/flag-it.svg" width="28" height="19" alt="Bandiera Italiana" style="vertical-align: middle;"> Italian Weather Alerts for Google AI Edge Gallery

> A Google AI Edge Gallery skill for querying official Italian Civil Protection weather alerts and presenting the results in a clear, visual mobile dashboard.

![Status](https://img.shields.io/badge/status-prototype-orange)
![Platform](https://img.shields.io/badge/platform-Google%20AI%20Edge%20Gallery-blue)
![Coverage](https://img.shields.io/badge/coverage-Italy-green)

## ✨ Overview

This project is an Agent Skill built according to the official [Google AI Edge Gallery Skills Specification](https://github.com/google-ai-edge/gallery/tree/main/skills). It is designed to answer questions such as:

- “Are there any weather alerts tomorrow in Bologna?”
- “What risks affect my area today?”
- “Show me the current Civil Protection alerts for my location.”

The skill covers the whole of Italy, resolves locations to official alert zones, and returns both a concise AI answer and an interactive visual dashboard rendered directly on-device.

## 🖼️ UI Preview

The following screenshot illustrates the live on-device response experience inside a Google AI Edge Gallery chat for the municipality of **Segrate (Milano, Lombardia)**:

<p align="center">
  <img src="docs/mockups/italian-weather-alerts-preview.png" width="50%" alt="Italian Weather Alerts UI (Segrate Demo)">
</p>

> ℹ️ Captured directly from the app interface showing decentralized on-device fetching of official DPC critical alert bulletins, interactive day toggle (Oggi/Domani), and national alert maps.

## 🎯 Main goals

- <img src="skills/italian-weather-alerts/assets/flag-it.svg" width="18" height="12" alt="Italia" style="vertical-align: middle;"> Support all Italian regions and autonomous provinces.
- 🗺️ Map municipalities and locations to official Civil Protection alert zones.
- 🚦 Clearly display yellow, orange, and red alert levels.
- 🌧️ Separate hydrogeological, hydraulic, thunderstorm, and other supported risks.
- 📅 Support at least today and tomorrow.
- 🔎 Show bulletin issue time, retrieval time, source, and data freshness.
- 📱 Provide a mobile-friendly inline visual dashboard.
- ♿ Use text, labels, icons, and patterns in addition to colors.
- 🛡️ Never infer an official alert from a generic weather forecast.

## 🧱 Architecture & Official Standards

This skill is engineered strictly adhering to the [AI Edge Gallery Agent Skills Guide](https://github.com/google-ai-edge/gallery/tree/main/skills):

- **Declarative Contract (`SKILL.md`)**: Configured with frontmatter metadata (`name`, `description`, `metadata.homepage`) and prompt instructions with JSON schemas for LLM tool invocation.
- **Headless Logic Runner (`scripts/index.html`)**: Implements the globally exposed `window.ai_edge_gallery_get_result(data)` asynchronous entry point. It runs silently in a hidden mobile webview to fetch live Civil Protection bulletins, resolve Italian municipalities to alert zones, and handle caching.
- **Interactive Inline WebView (`assets/webview.html`)**: Employs the official `webview` response schema (`url` and `aspectRatio`) to stream a dynamic, touch-friendly dashboard directly into the chat interface.
- **Direct Client-Side Query**: Queries the official Open Data repository of the Italian Civil Protection ([`pcm-dpc/DPC-Bollettini-Criticita-Idrogeologica-Idraulica`](https://github.com/pcm-dpc/DPC-Bollettini-Criticita-Idrogeologica-Idraulica)) directly from the device.
- **Zero Backend Dependency**: 100% decentralized and autonomous on-device execution. Does not require any external proxies, backends, or API keys.

```text
skills/italian-weather-alerts/
├── SKILL.md                 # Agent instructions & tool schema
├── scripts/
│   └── index.html           # Headless background logic runner (DPC Open Data query & cache)
└── assets/
    ├── webview.html         # Interactive mobile chat UI dashboard
    └── flag-it.svg          # Local asset icons
```

## 📚 Data principles

- Official Civil Protection alert levels are authoritative.
- Weather forecasts and official alerts are displayed as different data types.
- Missing, stale, ambiguous, or unavailable data must be reported explicitly.
- The AI must not invent alert zones, levels, dates, issue times, or risk categories.

## 🚧 Project status

The core skill implementation, DPC bulletin ingestion logic, national zone resolution, and responsive inline mobile dashboard are fully implemented and verified on physical devices (see preview above).

For further roadmap items and deep dives, see [Implementation evolution](docs/implementation-evolution.md).

## ⚠️ Disclaimer

This project is a personal technical prototype and is not an emergency notification service. Always consult official Civil Protection and regional authorities for current information and follow official emergency instructions.
