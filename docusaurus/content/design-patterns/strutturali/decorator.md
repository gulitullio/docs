---
title: Decorator
sidebar_position: 1
---

E' un pattern **strutturale** che permette di aggiungere dinamicamente comportamenti o responsabilità a un oggetto **senza modificare il codice della sua classe originale**.

Si ottiene avvolgendo (wrapping) l'oggetto in un altro oggetto che implementa la stessa interfaccia.  
L'idea è simile alle **matrioske**: ogni decoratore può aggiungere logica extra e passare le chiamate all'oggetto "interno".

La struttura è la seguente:

- **Component**: interfaccia o classe astratta base.
- **ConcreteComponent**: implementazione concreta del componente.
- **Decorator**: classe astratta che implementa `Component` e contiene un riferimento a un `Component`.
- **ConcreteDecorator**: aggiunge nuove funzionalità.

---

### Quando usarlo ✅

- Vuoi aggiungere responsabilità a un oggetto senza modificare il suo codice.
- Vuoi combinare comportamenti in modo flessibile e dinamico.
- Vuoi evitare una gerarchia di classi troppo complessa a causa di estensioni multiple.

---

### Quando NON usarlo ❌

- La logica extra può essere gestita più semplicemente con _composition_ o _strategy_.
- Il sistema ha già molte istanze annidate e il debugging diventerebbe difficile.
- Le performance sono critiche e il wrapping aggiungerebbe overhead inutile.

---

## Esempio

Supponiamo di avere un personaggio in un gioco che può subire danni.  
Con il Decorator possiamo aggiungere dinamicamente effetti (scudi, potenziamenti, ecc.) senza modificare il codice di base.

#### Interfaccia componente

```csharp
public interface IDamageable
{
    void TakeDamage(int amount);
}
```

#### Componente concreto

```csharp
public class Player : MonoBehaviour, IDamageable
{
    public int Health = 100;

    public void TakeDamage(int amount)
    {
        Health -= amount;
        Debug.Log($"Player ha {Health} HP rimanenti.");
    }
}
```

#### Decoratore astratto

```csharp
public abstract class DamageableDecorator : IDamageable
{
    protected IDamageable _wrapped;

    public DamageableDecorator(IDamageable wrapped)
    {
        _wrapped = wrapped;
    }

    public virtual void TakeDamage(int amount)
    {
        _wrapped.TakeDamage(amount);
    }
}
```

#### Decoratore concreto: Scudo

```csharp
public class ShieldDecorator : DamageableDecorator
{
    private int _shieldStrength;

    public ShieldDecorator(IDamageable wrapped, int shieldStrength) : base(wrapped)
    {
        _shieldStrength = shieldStrength;
    }

    public override void TakeDamage(int amount)
    {
        if (_shieldStrength > 0)
        {
            int absorbed = Mathf.Min(amount, _shieldStrength);
            _shieldStrength -= absorbed;
            amount -= absorbed;
            Debug.Log($"Scudo assorbe {absorbed} danni. Scudo rimanente: {_shieldStrength}");
        }

        if (amount > 0)
        {
            base.TakeDamage(amount);
        }
    }
}
```

#### Utilizzo

```csharp
public class GameController : MonoBehaviour
{
    void Start()
    {
        Player player = new Player();
        IDamageable decoratedPlayer = new ShieldDecorator(player, 20);

        decoratedPlayer.TakeDamage(10); // Scudo assorbe 10
        decoratedPlayer.TakeDamage(15); // Scudo assorbe 10, player prende 5
    }
}
```
