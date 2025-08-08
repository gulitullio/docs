---
title: Strategy
sidebar_position: 2
---

Il **Strategy Pattern** è un pattern **comportamentale** che permette di definire una famiglia di algoritmi, incapsularli e renderli intercambiabili a runtime.  
Invece di avere una singola classe con tanti `if` o `switch` per decidere il comportamento, ogni strategia viene implementata come classe separata.  
L’oggetto che le utilizza non conosce i dettagli interni della strategia.

**Obiettivo:** separare l’algoritmo dalla logica che lo usa, migliorando estendibilità e manutenibilità.

---

### Struttura

- **Strategy (Interfaccia)**: definisce il contratto dell’algoritmo.
- **Concrete Strategies**: implementazioni specifiche del comportamento.
- **Context**: classe che usa la strategia e può cambiarla a runtime.

---

### Quando usarlo ✅

- Quando hai **più varianti dello stesso algoritmo** e vuoi evitare `if`/`switch` annidati.
- Quando il comportamento deve poter **cambiare a runtime**.
- Quando vuoi **separare il "cosa" dal "come"** per migliorare la leggibilità.
- Quando vuoi poter **aggiungere nuove varianti senza modificare il codice esistente** (Open/Closed Principle).

---

### Quando NON usarlo ❌

- Se il numero di varianti è **molto basso e stabile** → introdurre un pattern potrebbe complicare inutilmente.
- Se le strategie **non condividono un’interfaccia comune** → forzare il pattern porterebbe a design artificiale.
- Se la strategia non cambierà mai a runtime e il comportamento è semplice → meglio mantenere il codice diretto.

---

### Esempio

In questo esempio creeremo un sistema per muovere un personaggio con diverse strategie di movimento.

#### Interfaccia della strategia

```csharp
public interface IMovementStrategy
{
    void Move(Transform character, float speed);
}
```

#### Strategie concrete

```csharp
public class WalkMovement : IMovementStrategy
{
    public void Move(Transform character, float speed)
    {
        character.Translate(Vector3.forward * speed * Time.deltaTime);
    }
}
```

```csharp
public class FlyMovement : IMovementStrategy
{
    public void Move(Transform character, float speed)
    {
        character.Translate(Vector3.up * Mathf.Sin(Time.time) * speed * Time.deltaTime);
    }
}
```

#### Context (il personaggio)

```csharp
public class CharacterControllerStrategy : MonoBehaviour
{
    [SerializeField] private float speed = 5f;
    private IMovementStrategy movementStrategy;

    void Start()
    {
        // Strategia iniziale
        movementStrategy = new WalkMovement();
    }

    void Update()
    {
        movementStrategy.Move(transform, speed);

        // Cambio strategia a runtime
        if (Input.GetKeyDown(KeyCode.Space))
        {
            movementStrategy = new FlyMovement();
        }
    }

    public void SetMovementStrategy(IMovementStrategy newStrategy)
    {
        movementStrategy = newStrategy;
    }
}
```
