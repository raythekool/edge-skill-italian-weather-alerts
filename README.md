# <img src="skills/italian-weather-alerts/assets/flag-it.svg" width="28" height="19" alt="Italian Flag" style="vertical-align: middle;"> Italian Weather Alerts for Google AI Edge Gallery

> 🇮🇹 Leggi la versione in Italiano: [README.it.md](README.it.md)

A Google AI Edge Gallery Agent Skill for querying official **Italian Civil Protection** weather alerts and displaying localized risk bulletins and cartographic maps directly on an interactive on-device mobile dashboard.

![Status](https://img.shields.io/badge/status-active-brightgreen)
![Platform](https://img.shields.io/badge/platform-Google%20AI%20Edge%20Gallery-blue)
![Coverage](https://img.shields.io/badge/coverage-Italy-green)
![License](https://img.shields.io/badge/license-MIT-lightgrey)

---

## 🖼️ Mobile UI Preview

The following screenshot illustrates the live on-device response experience inside a Google AI Edge Gallery chat for the municipality of **Segrate (Milano, Lombardia)**:

<p align="center">
  <img src="docs/mockups/italian-weather-alerts-preview.png" width="50%" alt="Italian Weather Alerts UI (Segrate Demo)">
</p>

> ℹ️ Captured directly from the app interface: decentralized on-device fetching of official DPC critical alert bulletins, interactive day toggle (Today/Tomorrow), and official national alert maps.

---

## 📚 Tutorials (Learning-Oriented)

### Getting Started: Querying Alerts
You can query the skill using natural conversational language for any Italian municipality:

1. **Specific municipality**:
   > *"Are there any weather alerts tomorrow in Bologna?"*
2. **Local risk details**:
   > *"What risk levels affect Milan and Lombardy today?"*
3. **Regional overview & map**:
   > *"Show me Civil Protection alerts and the national map for Tuscany."*

The on-device model resolves the municipality to its official alert zone, queries official Civil Protection datasets, and renders both a concise summary and an **interactive, touch-friendly inline dashboard**.

---

## 🛠️ How-To Guides (Task-Oriented)

### How to Install on Google AI Edge Gallery

You can load this skill onto your Android device using either method:

#### Method 1: Local Import via ADB
1. Connect your Android device with **USB Debugging** enabled.
2. Push the skill directory to your device's Download folder:
   ```bash
   adb push skills/italian-weather-alerts/ /sdcard/Download/
   ```
3. Inside the **Google AI Edge Gallery** app, tap **Import local skill** and select the `italian-weather-alerts` folder.

#### Method 2: Import via URL (GitHub Pages)
1. Open the **Skill Manager** in the AI Edge Gallery app.
2. Enter the public skill URL:
   ```text
   https://raythekool.github.io/edge-skill-italian-weather-alerts/skills/italian-weather-alerts/
   ```

---

## 📖 Reference (Information-Oriented)

### Directory Structure

```text
skills/italian-weather-alerts/
├── SKILL.md                 # Declarative contract, system prompt, and JSON schemas
├── scripts/
│   └── index.html           # Headless logic runner (DPC Open Data querying & client caching)
└── assets/
    ├── webview.html         # Interactive mobile chat UI dashboard
    └── flag-it.svg          # Local visual assets
```

### Tool Invocation Schema (`run_js`)
The LLM invokes the headless runner `index.html` via `run_js` passing the following JSON payload:

| Field | Type | Description | Default |
| :--- | :--- | :--- | :--- |
| `location` | `String` | Municipality, province, region, or alert zone (e.g. `"Bologna"`) | Required |
| `date` | `String` | `"today"`, `"tomorrow"`, or ISO date (`"YYYY-MM-DD"`) | `"today"` |
| `includeForecast` | `Boolean` | Whether to include generic weather forecast info alongside official alerts | `false` |

Example:
```json
{"location": "Bologna", "date": "tomorrow", "includeForecast": false}
```

### Official Open Data Sources
- DPC Open Data Repository: [`pcm-dpc/DPC-Bollettini-Criticita-Idrogeologica-Idraulica`](https://github.com/pcm-dpc/DPC-Bollettini-Criticita-Idrogeologica-Idraulica)
- National Risk Maps Portal: [Civil Protection Criticality Maps](https://mappe.protezionecivile.gov.it/it/mappe-rischi/bollettino-di-criticita/)

---

## 🧠 Explanation (Understanding-Oriented)

### Why a Zero-Backend, On-Device Architecture?
Unlike conventional weather applications that depend on centralized servers, paid API keys, or intermediate databases:
- **100% Privacy & Decentralization**: The user's device requests raw GeoJSON datasets directly from the Civil Protection repository on GitHub.
- **Resilience**: Zero backend proxies. Geographic zone resolution and GeoJSON parsing occur entirely within the headless webview runtime on-device.

### Official Alerts vs Generic Weather Forecasts
A fundamental design pillar is strictly distinguishing **ordinary meteorological predictions** (e.g., "it might rain in Rome tomorrow") from **official civil protection criticality warnings**:
- **Green**: Absence of significant predictable risks.
- **Yellow**: Ordinary criticality (localized flooding, sudden severe thunderstorms).
- **Orange**: Moderate criticality (widespread and hazardous phenomena).
- **Red**: High criticality (severe danger to public safety).

### Anti-Hallucination Principles
System instructions in `SKILL.md` strictly prohibit the AI from guessing or synthesizing unofficial alert levels. If data is stale or unavailable, the skill reports it explicitly.

---

## ⚠️ Disclaimer

This project is a personal technical prototype and is not an emergency notification service. Always consult official Civil Protection and regional authorities for current information and follow official emergency instructions.
