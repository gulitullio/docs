---
title: Preprocessore
---

Il preprocessore viene eseguito prima della compilazione vera e propria, e produce un unico file che viene successivamente passato al compilatore

Utilizza direttive che iniziano con #, ognuna su una riga separata, con nomi definiti dallo standard e relativi argomenti.

Esempi:
`#define`, `#undef`, `#include`, cicli condizionali (`#if`, `#ifdef`, `#ifndef`, `#else`, `#elif`, `#elifdef`, `#elifndef`, `#endif`), `#line`, `#error`, `#warning`, `#pragma`, e nuove direttive come `#embed` (in C23/C++26)

### Capacità

- **Compilazione condizionale**  
  Permette di includere o escludere porzioni di codice in base a condizioni tramite direttive quali #if, #ifdef, #ifndef, #else, #elif, #elifdef, #elifndef, #endif.

- **Espansione di macro**  
  Attraverso #define e #undef, è possibile definire o rimuovere macro, anche con concatenazione o inserimento di virgolette (# e ##).

- **Inclusione di file**  
  Con #include è possibile includere il contenuto di altri file. L’operatore \_\_has_include (introdotto in C++17) consente di verificare se un file esiste prima dell’inclusione.

- **Emissione di errori o avvisi**  
  La direttiva #error provoca un errore di compilazione, bloccando il processo, mentre #warning (dal C++23) emette un avviso ma non invalida il programma.

- **Controllo del comportamento specifico dell’implementazione**  
  Con #pragma o \_Pragma (da C++11) si può gestire comportamenti dipe\*\*ndenti dal compilatore, come disabilitare avvisi o modificare l’allineamento.

- **Gestione delle informazioni su file e linee**  
  La direttiva #line consente di modificare il numero di linea e il nome del file nel contesto del preprocessore—utile soprattutto per strumenti automatici che generano codice.
