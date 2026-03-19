# trustworks-kiro-power

Et Kiro Power der hjælper Trustworks-medarbejdere med at bygge fungerende prototyper ud fra idéer — uden teknisk erfaring.

## Installation (for brugere)

1. Åbn Kiro
2. Find **"Powers"** i venstre panel
3. Klik **"Add power from GitHub"**
4. Indsæt: `github.com/trustworks/trustworks-kiro-power`
5. Klik **Install**

Det er alt. Næste gang du åbner et projekt og beskriver din idé, aktiverer poweret automatisk.

---

## Hvad poweret gør

Når du nævner ord som "idé", "prototype", "bygge", "app", "automatisere", "telefon" eller "dashboard", aktiverer Kiro automatisk Trustworks-konteksten og guider dig gennem processen.

**Poweret styrer:**
- Hvordan Kiro interviewer dig om din idé
- Hvilken teknologi Kiro vælger (uden at spørge dig)
- Hvornår Kiro anbefaler at involvere en udvikler
- Hvad der sker hvis du vil bygge en mobilapp (PWA i stedet for React Native)

---

## Indhold

```
trustworks-kiro-power/
├── POWER.md                      ← Entry point — onboarding og keyword-triggers
├── mcp.json                      ← Context7 til opdateret dokumentation
├── hooks/
│   └── readme-updater.kiro.hook  ← Holder README opdateret automatisk
└── steering/
    ├── 00-trustworks.md          ← Hvem er Trustworks og brugerne
    ├── 01-interaction.md         ← Interaktionsstil og tone
    ├── 02-tech-decision.md       ← Beslutningstræ for teknologivalg
    ├── 03-pwa-patterns.md        ← Mønstre til mobilapps (auto-indlæst)
    ├── 04-handoff.md             ← Overdragelse til teknisk kollega (auto-indlæst)
    └── 05-prototype-review.md    ← Gennemgang af færdig prototype (/prototype-review)
```

---

## Vedligeholdelse (for IT-teamet)

**Opdater steering-filer** ved at redigere `.md`-filerne og pushe til main. Brugere får opdateringen næste gang de bruger Kiro — ingen geninstallation nødvendig.

**Tilføj en ny teknologi-type:** Rediger `steering/02-tech-decision.md` og tilføj en ny sektion i beslutningstræet.

**Tilføj et nyt use case-specifikt mønster** (som `03-pwa-patterns.md`): Opret en ny `.md`-fil i `steering/` med `inclusion: auto` og en god `description` — Kiro indlæser den automatisk når det er relevant.

**Test af ændringer:** Klon repo'et lokalt, åbn mappen i Kiro, og test med en ny samtale.

---

## Teknologier poweret kender til

| Scenarie | Valg |
|---|---|
| Mobilapp (iPhone/Android) | Progressive Web App |
| Intern desktop-app | Python + Streamlit |
| Team-deling på lokalnetværk | Streamlit med `--server.address 0.0.0.0` |
| Databehandling / Excel-automatisering | Python-script |
| Simpel informationsside | Statisk HTML |

Poweret vælger **aldrig** React, React Native, Flutter, Firebase, Docker eller andre teknologier der kræver cloud-konti eller kompleks opsætning.

---

*Vedligeholdes af Trustworks IT-teamet*
