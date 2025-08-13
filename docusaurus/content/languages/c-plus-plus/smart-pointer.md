---
title: Smart Pointer
---

Gli smart pointer sono degli oggetti che gestiscono automaticamente la memoria in linguaggi come C++.
Servono per evitare problemi comuni legati alla gestione manuale della memoria, come:

- Memory leak (dimenticare di liberare memoria)
- Doppi delete (liberare due volte la stessa memoria)
- Dangling pointer (puntatori che puntano a memoria già liberata)

Si comportano come normali puntatori, ma quando l’ultimo smart pointer che punta a un certo blocco di memoria viene distrutto o riassegnato, automaticamente libera la memoria.

---

### Perché usare gli smart pointer?

- **Sicurezza**: ti aiutano a evitare errori di gestione della memoria
- **Pulizia del codice**: liberano automaticamente la memoria, quindi meno codice per gestirla
- **Flessibilità**: specialmente i shared_ptr permettono di condividere risorse senza problemi

---

### std::unique_ptr

- Unico proprietario della risorsa
- Non può essere copiato, solo trasferito (con move)
- Quando `unique_ptr` viene distrutto, distrugge anche la risorsa a cui punta

```csharp
std::unique_ptr<int> p1(new int(5));
// p1 è l'unico che "possiede" il puntatore
```

---

### std::shared_ptr

- Permette la condivisione della proprietà della risorsa
- Tiene un conteggio di riferimenti (quanti shared_ptr puntano alla stessa risorsa)
- Quando l’ultimo `shared_ptr` viene distrutto o riassegnato, la risorsa viene liberata.

```csharp
std::shared_ptr<int> p1 = std::make_shared<int>(10);
std::shared_ptr<int> p2 = p1;  // ora ci sono 2 shared_ptr che puntano allo stesso int
```

---

### std::weak_ptr

- Non possiede la risorsa, ma osserva un `shared_ptr` senza aumentarne il conteggio.
- Utile per evitare cicli di riferimento che impedirebbero la distruzione degli oggetti.

```csharp
std::shared_ptr<int> sp = std::make_shared<int>(42);
std::weak_ptr<int> wp = sp;  // wp osserva l'oggetto puntato da sp, ma non ne aumenta il conteggio
```
