---
title: Heap & Stack
sidebar_position: 2
---

---

## Differenze chiave

| Aspetto          | Stack                       | Heap                                             |
| ---------------- | --------------------------- | ------------------------------------------------ |
| **Allocazione**  | Automatica (a compile-time) | Dinamica (a runtime)                             |
| **Gestione**     | Automatica (scope-based)    | Manuale (new/delete)                             |
| **Velocità**     | Molto veloce                | Più lenta                                        |
| **Dimensione**   | Limitata (tipicamente MB)   | Molto grande (dipende dal sistema)               |
| **Tipi di dati** | Variabili locali, parametri | Oggetti di vita variabile, grandi strutture dati |
| **Rischi**       | Stack overflow se esageri   | Memory leak se non gestito                       |

---

## Stack

Lo stack è una porzione di memoria usata per gestire le chiamate di funzione, variabili locali e il controllo del flusso.

Funziona come una pila LIFO (Last In First Out).

### Caratteristiche principali

- **Allocazione automatica**: le variabili locali e i parametri di funzione vengono allocate sullo stack automaticamente quando si entra in una funzione e deallocate quando si esce.

- **Gestione automatica della memoria**: non serve gestire manualmente la memoria, la deallocazione è automatica alla fine del blocco.

- **Accesso molto rapido**: le variabili sono vicine tra loro in memoria, quindi cache-friendly.

- **Velocità**: l'allocazione e deallocazione sono molto veloci perché avvengono in ordine LIFO.

- **Dimensione limitata**: la dimensione dello stack è limitata (tipicamente qualche MB, configurabile), quindi non è adatto per dati grandi o molti dati dinamici.

### Esempio

```cpp
void foo() {
    int a = 10;       // allocato nello stack
    int arr[100];     // allocato nello stack (attenzione alla dimensione!)
}
```

---

## Heap

Lo heap è una porzione di memoria usata per allocazioni dinamiche, cioè quando si crea memoria a runtime e la si gestisce manualmente.

### Caratteristiche principali

- **Allocazione dinamica**: la memoria viene allocata con new (o malloc in C) e deallocata con delete (o free).

- **Gestione manuale**: devi allocare e deallocare tu esplicitamente la memoria per evitare memory leak.

- **Rischio di memory leak**: se non deallochi correttamente, la memoria rimane occupata inutilmente.

- **Accesso più lento**: l'allocazione è più lenta e l'accesso può essere meno efficiente a causa di frammentazione e minor località spaziale.

- **Dimensione molto più grande**: è molto più grande dello stack e permette di allocare grandi blocchi di memoria.

```cpp
void foo() {
    int* p = new int[100];  // allocazione dinamica sull'heap
    // ... uso p
    delete[] p;             // deallocazione manuale
}
```

---
