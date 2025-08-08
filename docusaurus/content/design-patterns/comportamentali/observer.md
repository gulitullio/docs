---
title: Observer
sidebar_position: 1
---

E' un pattern **comportamentale** che definisce una **relazione uno-a-molti** tra oggetti, in modo che quando uno stato dell’oggetto osservato (_subject_) cambia, tutti gli osservatori (_observers_) vengano notificati automaticamente.

In termini semplici: il Subject "avvisa" tutti gli iscritti (Observers) quando succede qualcosa di interessante, senza sapere chi sono o cosa fanno.

**Obiettivi principali**

- Disaccoppiare chi **emette eventi** (Subject) da chi **li riceve** (Observers).
- Rendere il sistema **estensibile** senza modificare il codice esistente.
- Favorire la **comunicazione asincrona** e la **modularità**.

---

### Quando usarlo ✅

- Più oggetti devono reagire a cambiamenti di stato di un altro oggetto.
- Vuoi evitare **dipendenze dirette** tra componenti.
- L’evento può avere **più listener** e questi listener possono cambiare dinamicamente.
- Vuoi seguire il **principio Open/Closed**: aggiungere nuovi osservatori senza modificare il Subject.

---

### Quando NON usarlo ❌

- C’è un solo destinatario dell’evento (in quel caso un callback diretto è più semplice).
- Le dipendenze sono statiche e non cambieranno mai.
- Il flusso degli eventi è **semplice** e non richiede un meccanismo centralizzato.
- Vuoi evitare **complessità di debugging** dovuta a eventi che si propagano in modo implicito.

---

### Esempio

Immaginiamo un sistema in cui un oggetto (`Player`) notifica altri sistemi (UI, Audio, Achievements) quando cambia la salute.

#### Interfaccia Observer

```csharp
public interface IHealthObserver
{
    void OnHealthChanged(int newHealth);
}
```

#### Observer: UI

```csharp
public class HealthUI : MonoBehaviour, IHealthObserver
{
    public void OnHealthChanged(int newHealth)
    {
        Debug.Log($"[UI] Aggiorna barra salute a {newHealth}");
    }
}
```

#### Observer: Audio

```csharp
public class HealthAudio : MonoBehaviour, IHealthObserver
{
    public void OnHealthChanged(int newHealth)
    {
        if (newHealth <= 30)
            Debug.Log("[Audio] Riproduci suono di bassa salute");
    }
}
```

#### Subject

```csharp
public class Player : MonoBehaviour
{
    private List<IHealthObserver> observers = new List<IHealthObserver>();
    private int health = 100;

    public void AddObserver(IHealthObserver observer)
    {
        if (!observers.Contains(observer))
            observers.Add(observer);
    }

    public void RemoveObserver(IHealthObserver observer)
    {
        observers.Remove(observer);
    }

    public void TakeDamage(int amount)
    {
        health = Mathf.Max(health - amount, 0);
        Debug.Log($"Player health: {health}");
        NotifyObservers();
    }

    private void NotifyObservers()
    {
        foreach (var observer in observers)
            observer.OnHealthChanged(health);
    }
}
```

#### Utilizzo

```csharp
public class GameSetup : MonoBehaviour
{
    public Player player;
    public HealthUI healthUI;
    public HealthAudio healthAudio;

    void Start()
    {
        player.AddObserver(healthUI);
        player.AddObserver(healthAudio);

        player.TakeDamage(20);
        player.TakeDamage(60);
    }
}
```
