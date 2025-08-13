---
title: Move Constructor
---

È un costruttore che trasferisce le risorse da un oggetto temporaneo (o comunque trasferibile) a un nuovo oggetto, senza fare una copia completa.

```cpp
MyClass(MyClass&& other) noexcept; // Firma tipica
```

Quando viene chiamato:

- Quando inizializzi un oggetto da un rvalue (oggetto temporaneo).
- Quando usi std::move su un oggetto.
- Nei ritorni di funzione, se l’oggetto è temporaneo.

### Esempio

Qui non allochiamo memoria nuova:

- Prendiamo il puntatore dell’altro oggetto.
- Lo "azzeriamo" per evitare doppia deallocazione.

```cpp
class MyClass {
    int* data;
public:
    MyClass(int val) : data(new int(val)) {}

    // Move constructor
    MyClass(MyClass&& other) noexcept : data(other.data) {
        other.data = nullptr; // svuotiamo l’originale
        std::cout << "Move constructor\n";
    }

    ~MyClass() { delete data; }
};
```
