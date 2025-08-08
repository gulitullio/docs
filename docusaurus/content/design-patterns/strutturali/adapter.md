---
title: Adapter (o Wrapper)
sidebar_position: 2
---

Permette di adattare l'interfaccia di una classe esistente a un'altra interfaccia attesa dal client, senza modificare il codice originale.

L'idea è quella di incapsulare un oggetto esistente all'interno di una nuova classe che "traduce" le chiamate da un formato all'altro.

**Obiettivo**

- Rendere compatibili classi con interfacce differenti.
- Permettere il riuso di codice esistente senza modificarlo.
- Separare il client dal formato interno di una libreria o classe.

---

### Quando usarlo ✅

- Quando hai **codice legacy** o librerie esterne che non puoi modificare.
- Quando un **client** richiede un'interfaccia specifica ma il servizio ne ha un'altra.
- Quando vuoi creare un **ponte temporaneo** tra due sistemi incompatibili.

---

### Quando NON usarlo ❌

- Se puoi **modificare direttamente** la classe originale per farla aderire all'interfaccia richiesta (Adapter diventerebbe inutile).
- Se le differenze tra le interfacce sono **troppo grandi**: rischi di creare un wrapper complesso e fragile.
- Se la "traduzione" tra interfacce richiede **molta logica** → forse serve un _Facade_ o una _nuova architettura_, non un Adapter.

---

### Esempio

Hai una libreria esterna che muove personaggi con `Move(float x, float y)` ma il tuo codice di gioco usa un'interfaccia `IMovable.Move(Vector2 direction)`.

#### Interfaccia attesa

```csharp
public interface IMovable
{
    void Move(Vector2 direction);
}
```

#### Classe esistente (Adaptee)

Questa classe è di una libreria esterna quindi non modificabile, chiede come parametri 2 float.

```csharp
public class ExternalMover
{
    public void Move(float x, float y)
    {
        Debug.Log($"Muovo verso: X={x}, Y={y}");
    }
}

```

#### Adapter

Nell'adapter vogliamo fare in modo di avere una funzione che prende come parametro un Vector2

```csharp
public class ExternalMoverAdapter : IMovable
{
    private ExternalMover _externalMover;

    public ExternalMoverAdapter(ExternalMover externalMover)
    {
        _externalMover = externalMover;
    }

    public void Move(Vector2 direction)
    {
        // Traduzione da Vector2 a due float separati
        _externalMover.Move(direction.x, direction.y);
    }
}
```

#### Utilizzo

```csharp
public class PlayerController : MonoBehaviour
{
    private IMovable _mover;

    void Start()
    {
        // Creo l'adapter per usare la libreria esterna con la mia interfaccia
        ExternalMover external = new ExternalMover();
        _mover = new ExternalMoverAdapter(external);
    }

    void Update()
    {
        Vector2 input = new Vector2(Input.GetAxis("Horizontal"), Input.GetAxis("Vertical"));
        _mover.Move(input);
    }
}
```
