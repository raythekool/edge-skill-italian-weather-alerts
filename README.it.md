# <img src="skills/italian-weather-alerts/assets/flag-it.svg" width="28" height="19" alt="Bandiera Italiana" style="vertical-align: middle;"> Allerte Meteo Protezione Civile per Google AI Edge Gallery

> 🇬🇧 Read the English version: [README.md](README.md)

Un'Agent Skill per **Google AI Edge Gallery** che interroga direttamente i bollettini ufficiali della **Protezione Civile Italiana** e presenta i livelli di allerta e le mappe di criticità su una dashboard visiva interattiva mobile sul dispositivo.

![Status](https://img.shields.io/badge/status-active-brightgreen)
![Platform](https://img.shields.io/badge/platform-Google%20AI%20Edge%20Gallery-blue)
![Coverage](https://img.shields.io/badge/coverage-Italy-green)
![License](https://img.shields.io/badge/license-MIT-lightgrey)

---

## 🖼️ Anteprima dell'Interfaccia Mobile

La seguente schermata mostra l'esperienza reale on-device durante una conversazione in Google AI Edge Gallery per il comune di **Segrate (Milano, Lombardia)**:

<p align="center">
  <img src="docs/mockups/italian-weather-alerts-preview.png" width="50%" alt="Italian Weather Alerts UI (Segrate Demo)">
</p>

> ℹ️ Cattura diretta dall'app: recupero decentralizzato on-device dei bollettini DPC, toggle interattivo Oggi/Domani e mappe nazionali ufficiali di criticità.

---

## 📚 Tutorials (Orientato all'Apprendimento)

### Primi Passi: Prova la Skill
Puoi interrogare la skill per conoscere le allerte di qualsiasi comune italiano direttamente in linguaggio naturale:

1. **Domanda di esempio sul comune**:
   > *"Ci sono allerte meteo domani a Bologna?"*
2. **Domanda sui rischi di zona**:
   > *"Quali rischi di criticità ci sono oggi a Milano?"*
3. **Mappa e quadro regionale**:
   > *"Mostrami le allerte della Protezione Civile per la Toscana oggi e domani."*

L'agente AI Edge identificherà il comune, mapperà la zona di allerta ufficiale e restituirà sia una sintesi testuale sia la **dashboard grafica inline touch-friendly**.

---

## 🛠️ How-To Guides (Orientato ai Task)

### Come installare la Skill su Google AI Edge Gallery

Puoi caricare la skill sulla tua app Android in due modalità:

#### Metodo 1: Importazione Locale via ADB
1. Collega il tuo dispositivo Android con il **Debug USB** abilitato.
2. Invia la cartella della skill sul telefono:
   ```bash
   adb push skills/italian-weather-alerts/ /sdcard/Download/
   ```
3. Nell'app **Google AI Edge Gallery**, tocca **Import local skill** e seleziona la cartella `italian-weather-alerts`.

#### Metodo 2: Importazione via URL (GitHub Pages)
1. Apri la sezione **Skill Manager** nell'app AI Edge Gallery.
2. Inserisci il seguente URL pubblico:
   ```text
   https://raythekool.github.io/edge-skill-italian-weather-alerts/skills/italian-weather-alerts/
   ```

---

## 📖 Reference (Orientato all'Informazione)

### Struttura della Skill

```text
skills/italian-weather-alerts/
├── SKILL.md                 # Contratto dichiarativo, prompt di sistema e schema JSON
├── scripts/
│   └── index.html           # Runner logico headless (fetch Open Data DPC e cache locale)
└── assets/
    ├── webview.html         # Dashboard grafica mobile touch-friendly
    └── flag-it.svg          # Asset grafici
```

### Schema di Invocazione Tool (`run_js`)
L'LLM invoca il runner headless `index.html` tramite `run_js` passando il seguente payload JSON:

| Campo | Tipo | Descrizione | Default |
| :--- | :--- | :--- | :--- |
| `location` | `String` | Comune, provincia, regione o zona di allerta (es. `"Bologna"`) | Obbligatorio |
| `date` | `String` | `"today"`, `"tomorrow"`, o data ISO (`"YYYY-MM-DD"`) | `"today"` |
| `includeForecast` | `Boolean` | Se includere indicazioni meteo generali assieme all'allerta | `false` |

Esempio:
```json
{"location": "Bologna", "date": "tomorrow", "includeForecast": false}
```

### Fonti Dati Ufficiali
- Repository Open Data DPC: [`pcm-dpc/DPC-Bollettini-Criticita-Idrogeologica-Idraulica`](https://github.com/pcm-dpc/DPC-Bollettini-Criticita-Idrogeologica-Idraulica)
- Portale Cartografico Nazionale: [Mappe Rischi Protezione Civile](https://mappe.protezionecivile.gov.it/it/mappe-rischi/bollettino-di-criticita/)

---

## 🧠 Explanation (Orientato alla Comprensione)

### Perché un'Architettura Zero-Backend On-Device?
A differenza delle app meteo convenzionali che richiedono server intermedi, API key a pagamento o database proprietari:
- **Totale Privacy & Decentralizzazione**: Il dispositivo dell'utente effettua la richiesta direttamente ai raw dataset ufficiali della Protezione Civile su GitHub.
- **Resilienza**: Funziona senza server di terze parti; l'elaborazione dei GeoJSON e la risoluzione geografica comune-zona avvengono localmente nel runtime headless webview.

### Bollettini Ufficiali vs Previsioni Meteo
Una delle funzioni cardine della skill è separare le **previsioni meteorologiche ordinarie** (es. "domani piove a Roma") dai **bollettini ufficiali di criticità idrogeologica e idraulica** emessi dallo Stato:
- **Verde**: Assenza di fenomeni significativi prevedibili.
- **Giallo**: Criticità ordinaria (possibili allagamenti localizzati, temporali improvvisi).
- **Arancione**: Criticità moderata (fenomeni diffusi e pericolosi).
- **Rosso**: Criticità elevata (gravi pericoli per l'incolumità pubblica).

### Politica Rigida Anti-Allucinazione
Le istruzioni in `SKILL.md` impediscono categoricamente al modello di inferire o inventare livelli di allerta basandosi su semplici previsioni meteo generiche. Se un dato non è presente o non è aggiornato, la skill lo dichiara esplicitamente.

---

## ⚠️ Disclaimer

Questo progetto è un prototipo tecnico personale e non costituisce un canale ufficiale di allertamento per le emergenze. Per informazioni in tempo reale e disposizioni di evacuazione o sicurezza, fare sempre riferimento ai canali ufficiali della Protezione Civile e dei Comuni di appartenenza.
