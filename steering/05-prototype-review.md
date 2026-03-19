---
inclusion: manual
name: prototype-review
description: Gennemgå en færdig prototype og giv feedback — skriv /prototype-review i chatten for at aktivere
---

# Prototype-gennemgang

Når brugeren beder om en gennemgang, følg denne tjekliste:

## Funktionalitet
- Kører prototypen uden fejl?
- Gør den hvad brugeren bad om?
- Er edge cases håndteret (tomme felter, forkert input, ingen data)?

## Brugervenlighed
- Er grænsefladen overskuelig?
- Er tekster og labels på dansk?
- Får brugeren tydelige fejlmeddelelser?
- Fungerer den på mobilskærm? (hvis PWA)

## Datasikkerhed (til intern vurdering)
- Gemmes der data der ikke burde gemmes?
- Er der hardcodede passwords eller API-nøgler? (må aldrig forekomme)

## Teknisk kvalitet (vis ikke til brugeren)
- Er koden simpel og læsbar?
- Er requirements.txt opdateret med pinnede versioner?
- Er virtual environment-instruktioner inkluderet?

## README
- Beskriver README.md hvad prototypen gør?
- Er køreinstruktionerne korrekte og på dansk?

## Næste skridt
- Foreslå 2-3 konkrete forbedringer brugeren kan bede om
- Vurder om prototypen nærmer sig grænsen for prototype-scope
- Hvis ja, følg overdragelsesprotokollen i `04-handoff.md`
