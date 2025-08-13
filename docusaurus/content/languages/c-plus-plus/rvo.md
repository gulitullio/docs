---
title: Return Value Optimization (RVO)
---

E' un’ottimizzazione molto importante in C++ che riduce copie inutili degli oggetti quando una funzione restituisce un valore per valore.

In C++ tradizionale, se una funzione restituisce un oggetto by value, il **flusso naturale** sarebbe:

- La funzione crea un oggetto locale.
- L’oggetto locale viene copiato nel valore di ritorno temporaneo.
- Il temporaneo viene poi copiato o spostato nella variabile del chiamante.
- Questo comporta fino a due copie/spostamenti, che possono essere costosi se l’oggetto è grande.

L’RVO dice: **"Perché fare copie inutili? Creiamo direttamente l’oggetto nella memoria del chiamante"**.  
In pratica il compilatore:

- Alloca lo spazio di destinazione direttamente dove andrà a vivere l’oggetto finale.
- Costruisce lì l’oggetto, evitando del tutto la copia o lo spostamento.

### Tipi di ottimizzazione

**RVO classico**

Quando ritorni un oggetto creato direttamente nel return, ad esempio:

```cpp
MyClass makeObject() {
    return MyClass(42); // costruito direttamente nello spazio del chiamante
}
```

**NRVO (Named Return Value Optimization)**

Quando ritorni una variabile locale con nome:

```cpp
MyClass makeObject() {
    MyClass obj(42);
    return obj; // NRVO: il compilatore costruisce 'obj' direttamente nello spazio di ritorno
}
```

### Perché è importante

- Migliora le performance evitando costi di copia/spostamento.
- Può essere cruciale per tipi non copiabili ma solo costruibili (per esempio un std::unique_ptr in certi contesti).
- Riduce overhead nascosto, specialmente nei container e nelle API che restituiscono oggetti pesanti.
