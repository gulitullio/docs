---
title: Move assignment operator
---

Il move assignment operator (operatore di assegnazione per spostamento) è un costrutto speciale che permette di trasferire le risorse da un oggetto temporaneo o trasferibile (un rvalue) a un altro oggetto già esistente, evitando copie inutili.

Quando assegni un oggetto a un altro, in genere si fa una copia dei dati (copy assignment operator).
Ma se l’oggetto sorgente è temporaneo (per esempio il risultato di una funzione o un std::move), non ha senso duplicare i dati: possiamo trasferire le risorse interne invece di copiarle.

### Forma tipica

```cpp
ClassName& operator=(ClassName&& other) noexcept;
```

- `ClassName&&` → accetta un `rvalue` reference (oggetto temporaneo o passato tramite `std::move`).
- `noexcept` → buona pratica, così container STL come `std::vector` possono ottimizzare.
- Ritorna `*this` per consentire le assegnazioni concatenate `(a = b = c).`

### Esempio semplificato

```cpp
T a;
T b;
b = std::move(a); // qui entra in gioco il move assignment
```

### Funzionamento interno

Il corpo tipico di un move assignment operator:

- Autocheck: se stai assegnando l’oggetto a se stesso, non fare nulla
- Dealloca eventuali risorse dell’oggetto di destinazione (per evitare memory leak)
- Trasferisci i puntatori o le risorse dal other a `*this `
- Resetta l’oggetto other in uno stato “valido ma vuoto”
- Ritorna `*this `

### Quando viene chiamato

Il move assignment viene usato quando:

- Stai assegnando un rvalue (obj = MyClass(10);)
- Oppure stai forzando lo spostamento con std::move (obj = std::move(other);).
- Se la classe non definisce un move assignment personalizzato, il compilatore può generarne uno automaticamente (dal C++11 in poi), a patto che sia possibile spostare i membri.

### Differenza con il copy assignment

| Copy assignment (`T& operator=(const T&)`) | Move assignment (`T& operator=(T&&)`) |
| ------------------------------------------ | ------------------------------------- |
| Duplica le risorse                         | Trasferisce le risorse                |
| Potenzialmente costoso                     | Più veloce (no allocazioni inutili)   |
| Usa l'oggetto sorgente senza modificarlo   | Svuota l'oggetto sorgente             |
