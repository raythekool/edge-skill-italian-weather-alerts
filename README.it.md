# <img src="skills/italian-weather-alerts/assets/flag-it.svg" width="28" height="19" alt="Bandiera Italiana" style="vertical-align: middle;"> Allerte Meteo Protezione Civile per Google AI Edge Gallery

> 🇬🇧 Read the English version: [README.md](README.md)

Un'Agent Skill per l'applicazione mobile **Google AI Edge Gallery** (disponibile su Android e iOS) che consulta direttamente i bollettini ufficiali della **Protezione Civile Italiana** e mostra i livelli di allerta territoriali e le mappe di criticità su una dashboard visiva direttamente nella chat.

![Status](https://img.shields.io/badge/Status-Attivo-brightgreen?style=flat-square)](https://github.com/raythekool/edge-skill-italian-weather-alerts)
![Platform](https://img.shields.io/badge/Platform-Google%20AI%20Edge%20Gallery-blue?style=flat-square)](https://github.com/google-ai-edge/gallery)
![Dispositivi](https://img.shields.io/badge/Dispositivi-Android%20%7C%20iOS-orange?style=flat-square)](https://github.com/raythekool/edge-skill-italian-weather-alerts)
![Copertura](https://img.shields.io/badge/Copertura-Italia%20(Tutti%20i%20Comuni)-green?style=flat-square)](https://github.com/raythekool/edge-skill-italian-weather-alerts)
![Licenza](https://img.shields.io/badge/Licenza-MIT-lightgrey?style=flat-square)](https://github.com/raythekool/edge-skill-italian-weather-alerts)

---

## 🖼️ Anteprima dell'Interfaccia Mobile

Ecco come appare la skill durante una conversazione in **Google AI Edge Gallery** sul tuo smartphone (esempio per il comune di **Segrate, Milano**):

<p align="center">
  <img src="docs/mockups/italian-weather-alerts-preview.png" width="50%" alt="Italian Weather Alerts UI (Segrate Demo)">
</p>

> ℹ️ Cattura diretta dall'app: recupero decentralizzato dei bollettini ufficiali della Protezione Civile, switch interattivo Oggi/Domani e mappe nazionali ufficiali di criticità.

---

## 📚 Tutorials: Primi Passi con le Allerte Meteo

### Fare la tua prima domanda
Una volta abilitata la skill nell'app, basta chiedere normalmente al modello locale:

1. **Domanda su un comune specifico**:
   > *"Ci sono allerte meteo domani a Bologna?"*
2. **Dettaglio sui rischi locali**:
   > *"Quali rischi di criticità ci sono oggi a Milano e in Lombardia?"*
3. **Quadro regionale e mappa**:
   > *"Mostrami le allerte della Protezione Civile e la mappa per la Toscana."*

L'intelligenza artificiale sul dispositivo identifica il comune, mappa automaticamente la zona di allerta ufficiale, recupera il bollettino ufficiale e risponde con una sintesi chiara unita a una **scheda grafica interattiva**.

---

## 🛠️ How-To: Come Installare sullo Smartphone (Android & iOS)

Puoi aggiungere questa skill a **Google AI Edge Gallery** in 3 semplici passaggi:

<p align="left">
  <a href="https://raythekool.github.io/edge-skill-italian-weather-alerts/skills/italian-weather-alerts/">
    <img src="https://img.shields.io/badge/📲%20Aggiunta%20Rapida%20a-Google%20AI%20Edge%20Gallery-0284c7?style=for-the-badge&logo=google" alt="Aggiungi Skill a Google AI Edge Gallery">
  </a>
</p>

1. **Apri Google AI Edge Gallery** sul tuo smartphone Android o iPhone.
2. Nel menu, vai su **Agent Skills** (o **Skill Manager**).
3. Tocca **Add Skill** > **From URL** (o **Remote URL**).
4. Incolla l'indirizzo ufficiale della skill:
   ```text
   https://raythekool.github.io/edge-skill-italian-weather-alerts/skills/italian-weather-alerts/
   ```
5. Tocca **Add / Confirm**. Ora puoi fare domande sulle allerte meteo italiane in qualsiasi chat!

---

## 📖 Reference: Domande, Rischi e Fonti Dati

### Come è Strutturata la Skill
La skill rispetta l'architettura a tre livelli prevista dalle specifiche ufficiali di Google AI Edge Gallery:

```text
skills/italian-weather-alerts/
├── SKILL.md             # Contratto dell'Agente: Prompt di sistema, regole geografiche e schemi JSON
├── scripts/             # Runner Headless: Interrogazione diretta degli Open Data DPC e cache locale
└── assets/              # Dashboard Mobile: Scheda grafica touch-friendly con livelli di criticità e mappe
```

- **`SKILL.md` (Contratto dell'Agente)**: Istruisce il modello locale su come interrogare i dati istituzionali e vieta categoricamente di inventare allerte da previsioni generiche.
- **`scripts/` (Runner Headless)**: Viene eseguito in background sul telefono per scaricare i bollettini GeoJSON della Protezione Civile e mappare i comuni sulle zone di allerta ufficiali.
- **`assets/` (Dashboard Mobile)**: Renderizza la scheda grafica touch-friendly con i codici colore di criticità, il dettaglio dei rischi e le mappe nazionali direttamente nella chat.

### Esempi di domande utili
- *"Ci sono allerte allagamenti o pioggia oggi a Genova?"*
- *"Mostrami le allerte temporali per domani a Roma."*
- *"Qual è il livello di allerta a Firenze in questo momento?"*
- *"Mostrami la mappa nazionale della Protezione Civile per domani."*

### Livelli Ufficiali di Criticità
- 🟢 **Verde**: Assenza di fenomeni significativi prevedibili.
- 🟡 **Giallo**: Criticità ordinaria (possibili allagamenti localizzati, temporali improvvisi, caduta rami).
- 🟠 **Arancione**: Criticità moderata (fenomeni diffusi, persistenti e potenzialmente pericolosi).
- 🔴 **Rosso**: Criticità elevata (gravi pericoli per la sicurezza e l'incolumità pubblica).

### Tipologie di Rischio Monitorate
- **Idrogeologico**: Frane, smottamenti e colate di fango causati da precipitazioni prolungate.
- **Idraulico**: Piene dei fiumi, esondazioni di corsi d'acqua e allagamenti.
- **Temporali Forti**: Fenomeni temporaleschi improvvisi e violenti con grandine e raffiche di vento.

### Fonti Ufficiali e Istituzionali
Tutti i dati vengono acquisiti direttamente dai repository Open Data ufficiali pubblicati quotidianamente dal **Dipartimento della Protezione Civile (DPC)**:
- Repository Open Data DPC: [`pcm-dpc/DPC-Bollettini-Criticita-Idrogeologica-Idraulica`](https://github.com/pcm-dpc/DPC-Bollettini-Criticita-Idrogeologica-Idraulica)
- Portale Cartografico Nazionale: [Mappe Rischi Protezione Civile](https://mappe.protezionecivile.gov.it/it/mappe-rischi/bollettino-di-criticita/)

---

## 🧠 Explanation: Perché Bollettini Ufficiali e Zero-Backend?

### 1. Bollettini Ufficiali di Sicurezza vs Previsioni Meteo
Le classiche app meteo prevedono la probabilità di pioggia, ma non tengono conto del rischio idrogeologico o idraulico del territorio. Questa skill si collega direttamente alle **allerte istituzionali** emanate dagli organi di sicurezza, garantendo dati ufficiali e certificati.

### 2. Zero-Backend e Massima Privacy
Questa skill non si appoggia a server intermedi di tracciamento o API commerciali:
- Le tue ricerche e le tue posizioni geografiche restano private sul tuo smartphone.
- Il telefono interroga direttamente i dati aperti della Protezione Civile senza intermediari.

### 3. Rigida Politica Anti-Allucinazione
Il modello non può inventare livelli di criticità o interpretare arbitrariamente una pioggia come un'allerta rossa. Se i dati del bollettino non sono disponibili per una specifica area, la skill lo dichiara in modo trasparente.

---

## ⚠️ Disclaimer
*Questo progetto è uno strumento tecnico indipendente e non costituisce un canale ufficiale di allertamento per le emergenze. In caso di maltempo severo o emergenze, fare sempre riferimento ai canali ufficiali della Protezione Civile e seguire le istruzioni delle autorità comunali.*
