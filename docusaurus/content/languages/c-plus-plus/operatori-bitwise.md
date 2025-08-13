---
title: Operatori bitwise
---

Gli operatori bitwise (o "operatori a livello di bit") sono operatori che lavorano direttamente sui singoli bit che compongono i numeri, anziché sul loro valore numerico complessivo.

Si usano molto in programmazione a basso livello, ma anche in situazioni in cui bisogna gestire flag, maschere di bit, ottimizzare spazio o fare operazioni binarie veloci.  
Ogni numero intero in memoria è rappresentato in binario, gli operatori bitwise manipolano questi bit uno per uno.

| Operatore | Nome                 | Effetto sui bit                                                     |
| --------- | -------------------- | ------------------------------------------------------------------- |
| `&`       | AND bit a bit        | 1 se **entrambi** i bit sono 1                                      |
| `\|`      | OR bit a bit         | 1 se **almeno uno** dei bit è 1                                     |
| `^`       | XOR (o OR esclusivo) | 1 se **solo uno** dei bit è 1                                       |
| `~`       | NOT bit a bit        | Inverte tutti i bit                                                 |
| `<<`      | Shift a sinistra     | Sposta i bit verso sinistra (riempiendo con zeri)                   |
| `>>`      | Shift a destra       | Sposta i bit verso destra (riempiendo con zeri o col bit del segno) |

### Esempi pratici

```cpp
a = 6   // 110 in binario
b = 3   // 011 in binario
a & b   // AND => 110 & 011 = 010 (cioè 2)
a | b   // OR => 110 | 011 = 111 (cioè 7)
a ^ b   // XOR => 110 ^ 011 = 101 (cioè 5)
~a      // NOT => ~110 = 011 (cioè 3)
a << 1  // Shift a sx => 110 diventa 1100 (cioè 12, ogni spostamento a sinistra moltiplica per 2)
a >> 1  // Shift a dx => 110 diventa 011 (cioè 3, ogni spostamento a destra divide per 2)
```

### Quando conviene usarli

Immagina di avere variabili booleane in un unico intero:

```cpp
FLAG_READ  = 1 << 0  // 0001
FLAG_WRITE = 1 << 1  // 0010
FLAG_EXEC  = 1 << 2  // 0100

value = FLAG_READ | FLAG_WRITE  // Abilito lettura e scrittura

// Controllo se il flag WRITE è attivo:
if value & FLAG_WRITE:
    print("Scrittura consentita")
```

### Vantaggi

- **Compressione di dati**
  Puoi usare pochi bit per memorizzare più valori compatti.

- **Algoritmi di grafica e crittografia**
  Molti algoritmi lavorano sui bit per performance e ottimizzazione.

- **Ottimizzazione delle performance**
  Operazioni come `x << 1` sono più veloci di `x \* 2` (anche se nei moderni compilatori la differenza è minima).
