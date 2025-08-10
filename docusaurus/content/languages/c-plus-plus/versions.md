---
title: Versioni
sidebar_position: 1
---

| Versione | Focus principale                                  | Esempi chiave                                                   |
| -------- | ------------------------------------------------- | --------------------------------------------------------------- |
| C++11    | Modernizzazione, move semantics, concurrency      | lambda, smart pointers, auto, nullptr                           |
| C++14    | Raffinamenti e miglioramenti                      | generic lambdas, relaxed constexpr                              |
| C++17    | Produttività, qualità del codice                  | if constexpr, structured bindings, optional/variant, filesystem |
| C++20    | Modernità, sicurezza template, coroutines, moduli | concepts, coroutines, modules, spaceship operator, ranges       |

---

## C++11 (2011)

È stata una rivoluzione nel linguaggio, introdusse molte nuove funzionalità chiave:

- Auto e decltype per deduzione del tipo
- Lambda expressions: funzioni anonime
- Smart pointers (std::unique_ptr, std::shared_ptr)
- Move semantics con rvalue references (&&) e std::move
- Concurrency: thread, mutex, futures, atomics nel thread
- Range-based for loop
- Uniform initialization
- nullptr al posto di NULL
- Static assertions (static_assert)
- Strongly typed enums (enum class)
- Nuove librerie: tuple, chrono, regex
- Variadic templates

## C++14 (2014)

Più che nuove feature radicali, C++14 è stato un raffinamento e una correzione di C++11:

- Generic lambdas (lambda con parametri auto)
- Relaxed constexpr: più funzioni possono essere constexpr
- Return type deduction per funzioni (auto return type)
- Variable templates
- std::make_unique (manca in C++11)
- Miglioramenti a auto e deduzione del tipo

## C++17 (2017)

Ancora più orientato alla semplicità, efficienza e qualità del codice:

- If constexpr: condizionale a compile-time
- Structured bindings: destrutturazione di tuple, pair, struct
- Fold expressions per template variadici
- Nuovo tipo std::optional, std::variant, std::any
- Parallel STL algorithms (esecuzione parallela)
- Filesystem library (filesystem)
- Inline variables (variabili inline a livello di header)
- Miglioramento di constexpr e lambda (lambda constexpr)
- Nuove keyword: [[nodiscard]]
- Eliminazione di alcune feature obsolete
- std::string_view: stringhe “view” senza copia
- Template deduction per classi (deduzione automatica del tipo dei template)

## C++20 (2020)

Una delle versioni più ricche di novità dopo C++11, con molte feature moderne:

- Concepts: constraint per template, più leggibilità e sicurezza
- Ranges library: manipolazione più semplice di sequenze
- Coroutines: supporto nativo per async/await
- Modules: sistema di moduli per compilazione più veloce e migliore gestione dipendenze
- Calendar & timezone nel chrono
- constexpr più potente (quasi tutte le librerie STL possono essere constexpr)
- consteval e constinit per costanti a compile-time
- Immediate functions (consteval)
- New operators (spaceship operator per confronto)
- Designated initializers (come in C99)
- Template parameter lists migliorati (template lambdas, template template parameters migliorati)
- std::span: view non-owning di array e buffer
- Coroutines support per funzioni asincrone
- Miglioramenti a constexpr e lambda (lambda con template parameters)
