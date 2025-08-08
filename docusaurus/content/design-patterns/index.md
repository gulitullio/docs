---
title: Design Patterns
---

Un **Design Pattern** è una soluzione riutilizzabile e testata per un problema ricorrente nello sviluppo software.  
Non è un pezzo di codice pronto da copiare e incollare, ma un _modello concettuale_ o una _linea guida_ che aiuta a risolvere problemi di progettazione in modo efficace e standardizzato.

I design patterns sono nati dall’esperienza di sviluppatori che hanno individuato soluzioni comuni a sfide frequenti nella progettazione di software.

---

## Tipi principali di Design Patterns

Secondo la classificazione del _Gang of Four_ (GoF), esistono tre categorie principali:

1. **Creazionali**  
   Gestiscono la creazione degli oggetti in modo flessibile e controllato.  
   _Esempi:_ Singleton, Factory Method, Abstract Factory, Builder, Prototype.

2. **Strutturali**  
   Si concentrano sulla composizione delle classi e degli oggetti.  
   _Esempi:_ Adapter, Decorator, Composite, Proxy, Facade, Bridge, Flyweight.

3. **Comportamentali**  
   Definiscono come gli oggetti interagiscono e comunicano tra loro.  
   _Esempi:_ Observer, Strategy, Command, State, Mediator, Iterator, Memento.

---

## Vantaggi

- **Standardizzazione**: facilita la collaborazione tra team.
- **Riutilizzo**: soluzioni pronte e collaudate.
- **Manutenibilità**: codice più leggibile e facilmente estendibile.
- **Flessibilità**: semplifica modifiche ed estensioni.
- **Documentazione implicita**: il nome del pattern racconta già parte della logica.

---

## Svantaggi

- **Overengineering**: rischio di complicare il codice usando pattern non necessari.
- **Curva di apprendimento**: serve esperienza per capire quando e come applicarli.
- **Rigidità**: un uso improprio può rendere il sistema meno flessibile.
- **Performance**: alcuni pattern (es. Decorator, Proxy) introducono un overhead.

---

## Buone pratiche

- **Usali come guida, non come regola**.
- **Scegli il pattern solo se risolve davvero un problema reale**.
- **Mantieni il codice leggibile**: il pattern deve chiarire, non confondere.
- **Conosci più pattern possibili**, ma applicali con criterio.
