---
inclusion: auto
name: pwa-patterns
description: Brug når du bygger en Progressive Web App eller en mobilapp
---

# PWA-mønstre og bedste praksis

Brug disse mønstre når du bygger en Progressive Web App til Trustworks-brugere.

---

## Manifest (manifest.json)

Brug altid dette som udgangspunkt — tilpas navn og farver:

```json
{
  "name": "App-navn her",
  "short_name": "Kort navn",
  "description": "Hvad appen gør",
  "start_url": "/",
  "display": "standalone",
  "background_color": "#ffffff",
  "theme_color": "#1a56db",
  "icons": [
    {
      "src": "icon.svg",
      "sizes": "any",
      "type": "image/svg+xml",
      "purpose": "any maskable"
    }
  ]
}
```

Ikoner: Generer altid et simpelt SVG-ikon inline — ingen billedfiler der skal downloades.

---

## Service Worker (service-worker.js)

Minimal service worker der cacher appen til offline-brug:

```javascript
const CACHE_NAME = 'app-v1';
const ASSETS = ['/', '/index.html', '/style.css', '/app.js', '/manifest.json'];

self.addEventListener('install', e => {
  e.waitUntil(caches.open(CACHE_NAME).then(c => c.addAll(ASSETS)));
});

self.addEventListener('fetch', e => {
  e.respondWith(
    caches.match(e.request).then(r => r || fetch(e.request))
  );
});
```

---

## Datalagring med localStorage

For simple apps: gem data som JSON i localStorage. Ingen server, ingen konto, virker offline.

```javascript
// Gem
function saveData(key, data) {
  localStorage.setItem(key, JSON.stringify(data));
}

// Hent
function loadData(key, defaultValue = []) {
  const stored = localStorage.getItem(key);
  return stored ? JSON.parse(stored) : defaultValue;
}
```

**Begrænsning:** localStorage er bundet til den browser og enhed der bruges. Data deles ikke automatisk på tværs af enheder. Informer brugeren om dette.

**Eksportfunktion:** Inkluder altid en knap der eksporterer data som CSV eller JSON, så brugeren ikke mister sine data.

---

## Mobilvenligt design — altid

```css
/* Grundlæggende mobile-first setup */
* { box-sizing: border-box; margin: 0; padding: 0; }

body {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  font-size: 16px;           /* Aldrig under 16px — undgår zoom på iOS */
  padding: env(safe-area-inset-top) env(safe-area-inset-right)
           env(safe-area-inset-bottom) env(safe-area-inset-left);
}

/* Touch-targets skal være mindst 48px høje */
button, input, select {
  min-height: 48px;
  font-size: 16px;           /* Undgår auto-zoom på iOS */
  border-radius: 8px;
  padding: 12px 16px;
}

button {
  width: 100%;
  background: #1a56db;
  color: white;
  border: none;
  cursor: pointer;
  font-weight: 600;
}
```

---

## Dansk datoformat og tal

```javascript
// Datoer på dansk
const dato = new Date().toLocaleDateString('da-DK', {
  weekday: 'long', year: 'numeric', month: 'long', day: 'numeric'
});

// Tal med dansk formatering (komma som decimal)
const km = (12.5).toLocaleString('da-DK');  // "12,5"

// Valuta (DKK)
const beloeb = (1234.5).toLocaleString('da-DK', {
  style: 'currency', currency: 'DKK'
});  // "1.234,50 kr."
```

---

## Kørselregistrering — specifikt mønster (Dittes use case)

Til kørselsapps der bruges til skattefradrag:

**Data der skal gemmes pr. tur:**
- Dato
- Fra (adresse eller beskrivelse)
- Til (adresse eller beskrivelse)
- Kilometer (manuel indtastning eller beregnet)
- Formål (rullemenu: kundebesøg, møde, kursus, andet)
- Bemærkninger (valgfrit)

**Skattemæssige krav:**
- Statens kilometertakst 2024: 3,79 kr./km (de første 20.000 km), 2,23 kr./km derefter
- Appen skal kunne eksportere en årsopgørelse i CSV-format som revisor kan bruge
- Vis løbende total: antal km og beregnet fradrag

**Eksportformat (CSV):**
```
Dato,Fra,Til,Kilometer,Formål,Beløb (kr.),Bemærkninger
```

---

## Sådan tester du på rigtig telefon

Inkluder altid disse instruktioner i README.md for PWA-projekter:

```markdown
## Test på din telefon

1. Start serveren: `python3 -m http.server 8080`
2. Find din computers IP-adresse:
   - Mac: System Preferences → Network → IP-adresse
   - Windows: Kør `ipconfig` i terminal → IPv4 Address
3. Åbn `http://[din-ip]:8080` på din telefon (samme WiFi)
4. Installer som app:
   - iPhone: Tryk på deleknappen → "Føj til hjemmeskærm"
   - Android: Tryk på menuknappen → "Installer app" eller "Føj til startskærm"
```

---

## GitHub Pages (gratis hosting, valgfrit)

Hvis brugeren vil dele appen med andre uden at de behøver at køre en server:

1. Opret gratis konto på github.com
2. Opret nyt repository og upload filerne
3. Gå til Settings → Pages → vælg "main branch"
4. Appen er tilgængelig på `https://[brugernavn].github.io/[repo-navn]`

Informer brugeren om at appen så er offentligt tilgængelig — ikke egnet til fortrolige data.
