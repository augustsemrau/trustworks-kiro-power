---
inclusion: auto
name: pwa-patterns
description: Use when building a Progressive Web App or a mobile app
---

# PWA Patterns and Best Practices

Use these patterns when building a Progressive Web App for Trustworks users.

---

## Manifest (manifest.json)

Always use this as a starting point — customise name and colours:

```json
{
  "name": "App name here",
  "short_name": "Short name",
  "description": "What the app does",
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

Icons: Always generate a simple inline SVG icon — no image files to download.

---

## Service Worker (service-worker.js)

Minimal service worker that caches the app for offline use:

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

## Data storage with localStorage

For simple apps: store data as JSON in localStorage. No server, no account, works offline.

```javascript
function saveData(key, data) {
  localStorage.setItem(key, JSON.stringify(data));
}

function loadData(key, defaultValue = []) {
  const stored = localStorage.getItem(key);
  return stored ? JSON.parse(stored) : defaultValue;
}
```

**Limitation:** localStorage is tied to the browser and device being used. Data is not automatically shared across devices. Always inform the user of this.

**Export function:** Always include a button that exports data as CSV or JSON, so the user cannot lose their data.

---

## Mobile-friendly design — always

```css
* { box-sizing: border-box; margin: 0; padding: 0; }

body {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  font-size: 16px;           /* Never below 16px — prevents zoom on iOS */
  padding: env(safe-area-inset-top) env(safe-area-inset-right)
           env(safe-area-inset-bottom) env(safe-area-inset-left);
}

/* Touch targets must be at least 48px tall */
button, input, select {
  min-height: 48px;
  font-size: 16px;           /* Prevents auto-zoom on iOS */
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

## Danish number and date formatting

Even when the steering files are in English, apps built for Danish users should format numbers and dates correctly:

```javascript
// Danish date format
const date = new Date().toLocaleDateString('da-DK', {
  weekday: 'long', year: 'numeric', month: 'long', day: 'numeric'
});

// Danish number formatting (comma as decimal separator)
const km = (12.5).toLocaleString('da-DK');  // "12,5"

// Danish currency
const amount = (1234.5).toLocaleString('da-DK', {
  style: 'currency', currency: 'DKK'
});  // "1.234,50 kr."
```

---

## Work mileage log — specific pattern

For mileage apps used for Danish tax deductions:

**Data to store per trip:**
- Date
- From (address or description)
- To (address or description)
- Kilometres (manual entry)
- Purpose (dropdown: client visit, meeting, training, other)
- Notes (optional)

**Danish tax rules:**
- State reimbursement rate 2024: DKK 3.79/km (first 20,000 km), DKK 2.23/km thereafter
- The app should export an annual summary as CSV that an accountant can use
- Show running totals: total km and calculated deduction amount

**Export format (CSV):**
```
Date,From,To,Kilometres,Purpose,Amount (DKK),Notes
```

---

## How to test on a real phone

Always include these instructions in README.md for PWA projects:

```markdown
## Testing on your phone

1. Start the server: `python3 -m http.server 8080`
2. Find your computer's IP address:
   - Mac: System Settings → Network → IP address
   - Windows: Run `ipconfig` in terminal → IPv4 Address
3. Open `http://[your-ip]:8080` on your phone (same WiFi)
4. Install as an app:
   - iPhone: Tap the share button → "Add to Home Screen"
   - Android: Tap the menu button → "Install app" or "Add to Home Screen"
```

---

## GitHub Pages (free hosting, optional)

If the user wants to share the app with others without requiring them to run a server:

1. Create a free account at github.com
2. Create a new repository and upload the files
3. Go to Settings → Pages → select "main branch"
4. The app is available at `https://[username].github.io/[repo-name]`

Always inform the user that the app will be publicly accessible — not suitable for confidential data.
