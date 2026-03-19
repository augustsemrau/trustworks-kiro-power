---
inclusion: always
---

# Teknologivalg — Beslutningstræ

Brugeren skal **aldrig** vælge teknologi selv. Du vælger baseret på disse kriterier. Det afgørende spørgsmål er altid:

> **Kan brugeren køre, teste og dele dette med nul konti, nul abonnementer og nul serveropsætning?**

---

## Beslutningstræ

### Bruges det primært på en telefon?

**→ Progressive Web App (PWA)**

En PWA er en hjemmeside der opfører sig som en app på telefonen. Brugeren åbner den i sin browser og kan tilføje den til sin startskærm — præcis som en rigtig app. Den virker offline, gemmer data lokalt, og kræver ingen App Store, ingen Google Play, ingen udviklerkonto.

**Teknisk stack:**
- Rent HTML, CSS og JavaScript — ingen frameworks, ingen build-trin
- Data gemmes i `localStorage` (indbygget i alle mobilbrowsere)
- Kører fra en simpel lokal server: `python3 -m http.server 8080`
- Deles ved at køre serveren og åbne IP-adressen på telefonen, ELLER via GitHub Pages (gratis hosting)

**Typiske eksempler:**
- Kørselsregistrering til skat (Dittes mands app)
- Tidsregistrering på farten
- Simpel tjekliste eller logbog
- Udgiftsregistrering

**PWA-krav du altid inkluderer:**
```
manifest.json        ← gør den installerbar på telefonen
service-worker.js    ← gør den offline-kapabel
index.html           ← hoved-applikationen
style.css            ← mobilvenligt design (touch-targets, stor tekst)
app.js               ← logik og datahåndtering
```

Manifestet skal altid have: `name`, `short_name`, `display: standalone`, `start_url`, `icons` (brug emoji-baserede SVG-ikoner så der ikke kræves billedfiler).

Design altid mobile-first: store knapper (min. 48px touch target), tydelig kontrast, simpelt layout. Test ved at åbne på telefon.

---

### Bruges det på én computer — kun af brugeren selv?

**→ Python + Streamlit**

Kører lokalt, åbner automatisk i browser, ingen installation udover Python.

**Teknisk stack:**
- Python 3.10+
- Streamlit til UI
- SQLite til data (lokal fil, ingen server)
- `pip install -r requirements.txt` + `streamlit run app.py`

**Projektstruktur:**
```
projekt/
├── app.py
├── requirements.txt    ← med pinnede versioner (fx streamlit==1.45.1)
├── data/
└── README.md           ← dansk, uden jargon
```

---

### Bruges det af et lille team (2-10 personer) på samme netværk?

**→ Python + Streamlit med netværksdeling**

Samme stack som ovenfor. Streamlit kan køres så det er tilgængeligt på lokalnetværket:

```bash
streamlit run app.py --server.address 0.0.0.0
```

Andre på samme WiFi kan tilgå det via computerens IP-adresse. Ingen server eller cloud nødvendigt.

---

### Er det ren databehandling — ingen brugergrænseflade?

**→ Python-script**

Simpelt script der læser inputfiler (CSV, Excel) og skriver outputfiler.

**Teknisk stack:**
- Python 3.10+
- pandas eller polars til databehandling
- openpyxl til Excel-filer
- Kører med: `python process.py`

Inkluder altid en kort beskrivelse øverst i scriptet om hvad det gør og hvilke filer det forventer.

---

### Er det en simpel informationsside eller opslagstavle?

**→ Statisk HTML**

En enkelt HTML-fil der kan åbnes direkte i en browser. Ingen server nødvendig.

Kan deles ved at sende filen, eller hostes gratis på GitHub Pages.

---

## Hvad du aldrig vælger (og hvorfor)

| Teknologi | Hvorfor ikke |
|---|---|
| React / Vue / Angular | Kræver Node.js, npm, build-pipeline — for komplekst at sætte op |
| React Native / Flutter | Kræver Xcode, Android Studio, app store-konto |
| Django / FastAPI med database | Kræver server, deployment, vedligeholdelse |
| Firebase / Supabase / AWS | Kræver konto, kreditkort, cloud-konfiguration |
| Docker | Kræver teknisk opsætning, ikke egnet til prototyper |
| Electron | Tung, kompleks, overkill til prototyper |

**Undtagelse:** Hvis en teknisk kollega er med i samtalen og eksplicit beder om en af ovenstående, følg deres anvisning.

---

## Virtual environment — altid til Python-projekter

Inkluder altid disse instruktioner i README.md for Python-projekter:

```bash
python3 -m venv venv
source venv/bin/activate      # Mac/Linux
venv\Scripts\activate          # Windows
pip install -r requirements.txt
```

Pin altid versioner i requirements.txt. Brug `pip freeze > requirements.txt` efter installation.

---

## Fejlhåndtering i prototyper

- Wrap filoperationer og databehandling i `try/except`
- Vis fejl på dansk med `st.error()` (Streamlit) eller `alert()` / synlig tekst (PWA)
- Lad aldrig prototypen crashe med en uforståelig fejl
- Simple, forståelige fejlmeddelelser er bedre end avanceret fejlhåndtering
