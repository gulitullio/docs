---
title: Puntatori
---

Un puntatore è una variabile che contiene l’indirizzo di memoria di un’altra variabile.

In altre parole, mentre una variabile “normale” contiene un valore (es. un intero), un puntatore contiene dove quel valore è memorizzato in memoria

```cpp
int var = 10;
int* ptr = &var;         // 'ptr' punta all’indirizzo di 'var'
std::cout << *ptr;       // dereferenzia ptr → stampa 10
```

- `int* ptr`: dichiara un puntatore a int
- `&var`: operatore address-of, restituisce l’indirizzo di var
- `*ptr`: operatore di dereferenziazione, accede al valore puntato

### Puntatori doppi e funzioni

- **Puntatore a puntatore**
  Serve per strutture avanzate: array di puntatori, gestioni dinamiche, etc

`int** pptr = &ptr;` dove `ptr` è `int*`.

- **Funzione puntatore**
  Permette di chiamare funzioni indirettamente o passare callback a funzione:

```cpp
int (*fun)(int,int) = addition;
int result = fun(5,3);
```

Oppure:

```cpp
int operation(int x, int y, int (*pf)(int,int)) {
  return (*pf)(x,y);
}
```

Molto utile anche nella gestione dei callback

### Operazioni aritmetiche sui puntatori

È possibile incrementare/decrementare, sommare o sottrarre interi:

```cpp
int arr[] = {10,20,30};
int* p = arr;     // arr == &arr[0]
p++;              // ora punta a &arr[1]
std::cout << *p;  // stampa 20
```

### Puntatori e memoria

I puntatori permettono operazioni a basso livello:

- allocazione dinamica: new/delete
- strutture dati: linked list, alberi, grafi
- efficienza: non si copiano grandi strutture, ma solo indirizzi

Attenzione però a: memory leak, dangling pointer, wild pointer.

### Tipi speciali di puntatori

- **Puntatore nullo**
  `int* ptr = nullptr`; o `= NULL`; indica che il puntatore non punta ad alcuna locazione valida

- **Wild pointer (non inizializzati)**
  Non puntano a una locazione valida: usare `int* ptr`; senza inizializzazione è pericoloso. Può causare crash

- **Dangling pointer**
  Puntano a memoria già deallocata o a variabili locali fuori scope. Dereferenziare uno di questi dà undefined behavior

- **Void pointer (void\*)**
  È un puntatore generico che può contenere l’indirizzo di qualsiasi tipo, ma non si può dereferenziare direttamente: serve un cast esplicito

### Puntatori vs Riferimenti

- Riferimento (int& r = var;) è un alias, non può essere nullo e non può essere riassegnato.
- Puntatore (int* p) può essere nullo, può cambiare cosa punta, richiede * per la dereferenziazione
