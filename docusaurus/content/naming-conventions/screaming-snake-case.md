---
title: SCREAMING_SNAKE_CASE
sidebar_position: 4
---

Tutte le lettere sono maiuscole, le parole sono separate da un underscore (`_`).

### Linguaggi comuni

C, C++, Java, Python, JavaScript, TypeScript

### Utilizzo

Costanti, Valori immutabili, Flag di configurazione

### Note

Questo stile è spesso utilizzato per identificare **costanti globali** o **valori statici** che non cambiano mai durante l'esecuzione del programma.

In molti linguaggi è una convenzione comune per distinguere facilmente valori costanti da variabili normali.

### Esempio

```ts
const MAX_RETRY_COUNT = 5;
const API_BASE_URL = "https://api.example.com";
const DEFAULT_TIMEOUT_MS = 3000;

function fetchData(url: string, retries: number = MAX_RETRY_COUNT): void {
  console.log(`Fetching ${url} with max ${retries} retries...`);
}

fetchData(API_BASE_URL);
```
