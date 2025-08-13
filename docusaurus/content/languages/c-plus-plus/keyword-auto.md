---
title: Keyword Auto
---

La parola chiave auto serve per dedurre automaticamente il tipo di una variabile in fase di compilazione, senza che tu debba scriverlo esplicitamente.

Non significa che la variabile diventa “dinamica” come in Python o JavaScript.  
Il tipo è sempre fisso e forte (statically typed), solo che è il compilatore a indovinarlo al posto tuo

### Esempi pratici

Il compilatore guarda l’inizializzazione e deduce il tipo più corretto

```cpp
auto x = 5;        // x è int
auto y = 3.14;     // y è double
auto s = "ciao";   // s è const char*
```

#### Tipi complessi

**auto** è utilissimo quando il tipo è lungo o complesso, per esempio con iteratori:

```cpp
int main() {
    vector<int> v = {1, 2, 3};

    // Senza auto:
    vector<int>::iterator it = v.begin();

    // Con auto:
    auto it2 = v.begin();

    cout << *it2; // 1
}
```

#### Const e riferimenti

**auto** non mantiene automaticamente const e & dal valore iniziale (a meno che non lo scrivi):

- Se vuoi che sia riferimento, metti & o && esplicitamente
- Se vuoi mantenere const, aggiungilo

```cpp
const int n = 42;

auto a = n;   // a è int (const rimosso)
auto& b = n;  // b è const int& (qui const rimane)
```

#### Funzioni

Molto comodo per dedurre il tipo di ritorno di una funzione.

```cpp
auto somma(int a, int b) {
    return a + b; // tipo dedotto: int
}
```

#### Lambda

Oppure per memorizzare lambdas (dove il tipo è impronunciabile)

```cpp
auto f = [](int x) { return x * 2; };
```
