---
title: Copy Constructor
---

È un costruttore che crea un nuovo oggetto copiando i dati da un oggetto esistente.

```cpp
MyClass(const MyClass& other); // Firma tipica
```

Quando viene chiamato:

- Quando inizializzi un oggetto da un altro passato per reference costante.
- Quando ritorni un oggetto per valore (anche se spesso l’ottimizzazione RVO lo evita).
- Quando passi un oggetto per valore a una funzione.

### Esempio

Qui copiamo il valore puntato, non solo il puntatore, per evitare shallow copy e double delete.

```cpp
class MyClass {
    int* data;
public:
    MyClass(int val) : data(new int(val)) {}

    // Copy constructor
    MyClass(const MyClass& other) : data(new int(*other.data)) {
        std::cout << "Copy constructor\n";
    }

    ~MyClass() { delete data; }
};
```
