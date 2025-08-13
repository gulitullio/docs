---
title: LValue & Rvalue
---

### LValue (Locator Value)

- Un **lvalue** rappresenta un oggetto che ha un indirizzo in memoria e quindi può stare sul lato sinistro di un’assegnazione.
- Gli **lvalue** persistono oltre l’espressione corrente.

```cpp
int x = 5;   // x è un lvalue
x = 10;      // ok, x può stare a sinistra dell'assegnazione
```

### RValue (Read Value / Right Value)

- Un **rvalue** è un valore temporaneo senza un nome stabile, tipicamente generato da un’espressione.
- Gli **rvalue** non hanno un indirizzo persistente e non possono stare da soli sul lato sinistro di un’assegnazione.

```cpp
int y = 10;
int z = y + 5; // (y + 5) è un rvalue temporaneo
```

### Overview

- Lvalue: ha un nome o un indirizzo, può essere modificato (se non è const).
- Rvalue: è temporaneo, spesso un risultato intermedio di un calcolo.
- Un lvalue può diventare rvalue se lo usi come valore.
- Alcuni tipi di espressioni generano rvalue: letterali numerici (42), il risultato di una funzione che ritorna per valore, espressioni aritmetiche (a+b).

### Esempi

```cpp
int a = 5;     // 'a' è un lvalue
int b = a;     // 'a' qui è usato come rvalue (il suo valore viene letto)
int c = a + b; // (a + b) è un rvalue temporaneo
(a + b) = 10;  // Errore: (a + b) è un rvalue, non ha memoria assegnabile
```

#### Funzioni e ritorni

```cpp
int getValue() { return 42; }

int main() {
    int x = getValue();  // getValue() ritorna un rvalue
}
```

Se una funzione ritorna per riferimento, invece, può produrre un lvalue:

```cpp
int global;
int& getRef() { return global; }

int main() {
    getRef() = 10; // ok, getRef() è un lvalue
}
```

#### std::move

std::move non sposta veramente nulla ma trasforma un lvalue in un rvalue (più precisamente in un xvalue, eXtended value), permettendo di usare il move constructor o il move assignment invece di una copia.

Questo è utile con oggetti pesanti come std::string, std::vector, ecc.

```cpp
// Senza std:move
// Qui viene chiamato il copy constructor, che copia tutto il contenuto di a in b.
int main() {
    std::string a = "Ciao mondo";
    std::string b = a; // COPIA: a rimane invariata
    std::cout << "a: " << a << "\n";
    std::cout << "b: " << b << "\n";
}

// Con std:move
// std::move(a) trasforma a (lvalue) in un rvalue.
// Nessuna copia di memoria pesante, solo un trasferimento di puntatori.
int main() {
    std::string a = "Ciao mondo";
    std::string b = std::move(a); // MOVE: a viene "svuotata"
    std::cout << "a: " << a << "\n"; // a ora è in stato valido ma indefinito (spesso vuota)
    std::cout << "b: " << b << "\n";
}

```
