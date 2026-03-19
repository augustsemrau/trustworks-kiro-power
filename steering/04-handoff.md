---
inclusion: auto
name: handoff-protocol
description: Brug når brugeren nærmer sig grænserne for hvad der kan bygges uden en udvikler, eller spørger om næste skridt
---

# Overdragelsesprotokol

## Signaler på at en teknisk kollega bør involveres

**Tekniske grænser:**
- Integration med eksisterende systemer (SAP, Dynamics 365, SharePoint, interne API'er)
- Data skal deles på tværs af enheder eller brugere i realtid
- Mange samtidige brugere (mere end et lille team)
- Data kræver særlig sikkerhed eller GDPR-behandling
- Deployment til rigtig server eller cloud
- Automatisk kørsel uden brugerinteraktion (schedulerede jobs)
- Login og adgangskontrol

**Kompleksitetssignaler:**
- Brugeren har bedt om det samme ændret tre eller flere gange uden tilfredsstillende resultat
- Opgaven kræver forståelse af eksisterende kodebase eller systemer
- Prototypen skal erstatte et produktionssystem

## Hvad du siger

> *"Det vi er nået til nu kræver hjælp fra en teknisk kollega — ikke fordi idéen er dårlig, men fordi [konkret årsag på dansk]. Jeg laver en opsummering til dig nu, som du kan sende videre."*

## Overdragelsesdokument (gem som HANDOFF.md)

```markdown
# Prototype-overdragelse: [Projektets navn]

## Hvad er bygget
[2-3 sætninger — hvad gør prototypen, hvad er ikke implementeret]

## Hvad brugeren vil opnå
[Det forretningsmæssige mål, ikke det tekniske]

## Teknisk tilstand
- Teknologi: [PWA / Streamlit / Python-script]
- Koden ligger i: [mappenavn]
- Start med: [kommando]
- Pakker: se requirements.txt (hvis relevant)

## Datamodel
[Beskriv hvad der gemmes, hvordan og hvor]

## Hvad der mangler
[Prioriteret liste over næste skridt der kræver teknisk arbejde]

## Spørgsmål til den tekniske kollega
[2-4 specifikke spørgsmål]
```

## Hvad du ikke gør

- Forsøg ikke at implementere cloud-integrationer for at undgå overdragelsen
- Sig aldrig "det kan ikke lade sig gøre" — sig "det kræver en teknisk kollega"
- Vent ikke til brugeren selv beder om hjælp — vær proaktiv
