---
title: Factory
sidebar_position: 2
---

Il **Factory Pattern** è un pattern **creazionale** che fornisce un’interfaccia per creare oggetti in una superclasse, lasciando alle sottoclassi la decisione su quale classe concreta istanziare.  
In parole semplici: invece di usare direttamente `new` nel codice, demandi a un metodo/funzione dedicata la logica di creazione dell’oggetto.

**Obiettivi principali**

- **Disaccoppiare** la logica di creazione dal resto del codice.
- Rendere il codice **più flessibile** quando si aggiungono nuovi tipi di oggetti.
- **Centralizzare** la logica di creazione per facilitare modifiche future.

---

### Quando usarlo ✅

- Hai una logica di creazione complessa o ripetitiva.
- Vuoi poter aggiungere nuovi tipi di oggetti senza modificare il codice esistente.
- Non vuoi che il codice client conosca i dettagli delle classi concrete.
- Vuoi seguire il **principio Open/Closed** (_open for extension, closed for modification_).

---

### Quando NON usarlo ❌

- La creazione è semplice (un singolo `new` senza logica aggiuntiva).
- Non prevedi cambiamenti futuri nei tipi di oggetti.
- Il pattern aggiungerebbe solo **complessità inutile**.
- Puoi ottenere lo stesso risultato con **Dependency Injection** o **ScriptableObjects** (in Unity) senza aumentare l’overhead.

---

### Esempio

Immaginiamo un gioco in cui vogliamo creare diversi tipi di nemici (`Orc`, `Goblin`, `Troll`) senza che il codice client sappia quale classe usare.

#### Interfaccia

```csharp
public interface IEnemy
{
    void Attack();
}
```

#### Classi concrete

```csharp
public class Orc : IEnemy
{
    public void Attack() => Debug.Log("Orc attacca con l'ascia!");
}

public class Goblin : IEnemy
{
    public void Attack() => Debug.Log("Goblin lancia una pietra!");
}

public class Troll : IEnemy
{
    public void Attack() => Debug.Log("Troll colpisce con un masso!");
}
```

#### Enum per i tipi di nemico

```csharp
public enum EnemyType
{
    Orc,
    Goblin,
    Troll
}
```

#### Factory

```csharp
public static class EnemyFactory
{
    public static IEnemy CreateEnemy(EnemyType type)
    {
        switch (type)
        {
            case EnemyType.Orc:
                return new Orc();
            case EnemyType.Goblin:
                return new Goblin();
            case EnemyType.Troll:
                return new Troll();
            default:
                throw new System.ArgumentException("Tipo di nemico non supportato");
        }
    }
}
```

#### Utilizzo

```csharp
public class GameManager : MonoBehaviour
{
    void Start()
    {
        IEnemy enemy1 = EnemyFactory.CreateEnemy(EnemyType.Orc);
        enemy1.Attack();

        IEnemy enemy2 = EnemyFactory.CreateEnemy(EnemyType.Goblin);
        enemy2.Attack();
    }
}
```
