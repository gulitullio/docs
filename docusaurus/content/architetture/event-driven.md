---
title: Event-Driven Architecture (EDA)
sidebar_position: 5
---

L’Event-Driven Architecture (EDA) è un paradigma in cui il flusso dell’applicazione è guidato da eventi.
Un evento è qualsiasi cambiamento di stato o azione significativa che può essere notata dal sistema (es. “il player ha raccolto una moneta”, “un nemico è stato ucciso”, “il timer è scaduto”).

Concetti chiave:

- **Publisher (emettitore)**: genera l’evento (es. Player raccoglie un oggetto)
- **Subscriber (ascoltatore)**: reagisce all’evento (es. UIManager aggiorna il punteggio)
- **Event Bus / Dispatcher**: meccanismo che trasporta gli eventi dai Publisher ai Subscriber senza che conoscano direttamente l’uno l’altro (loose coupling)

---

### Perché usarlo

- **Disaccoppiamento**: i componenti non hanno riferimenti diretti tra loro, riducendo dipendenze rigide.
- **Scalabilità**: è facile aggiungere nuovi comportamenti senza toccare il codice esistente.
- **Manutenibilità**: meno “spaghetti code” e meno rischi di side-effect.
- **Reattività**: si presta a sistemi che devono reagire velocemente a input e cambiamenti.

---

### Svantaggi da considerare

- Difficoltà nel **debugging** (flusso non lineare)
- Rischio di **event storm** (troppe notifiche)
- Necessità di documentare bene **quali eventi esistono** e **chi li ascolta**

---

### Quando usarlo

Per un progetto medio-grande, l’Event Bus è spesso la scelta migliore:

- Evita riferimenti diretti tra oggetti in scena
- Facilita l’aggiunta di listener in qualsiasi punto del codice

---

### Esempio

In Unity, gli eventi possono essere gestiti in diversi modi:

- C# Events / Delegates → nativo, veloce, ma meno dinamico.
- UnityEvent → integrato nell’Inspector, ottimo per designer.
- Event Bus Pattern → centralizza la gestione degli eventi.

Immaginiamo lo scenario un cui il giocatore raccoglie una moneta, la UI aggiorna il punteggio senza che `Player` conosca `UIManager`.
`Player` rileva la collisione con una moneta, incrementa il conteggio e invia un evento con `EventBus.OnCoinCollected`.
`UIManager` ascolta quell’evento e aggiorna il testo in UI.
Non c'è alcun riferimento diretto tra Player e UI, quindi se cambi la UI, il Player non si accorge di nulla.

#### EventBus

```csharp
public static class EventBus
{
    // Passa il numero di monete raccolte come parametro
    public static Action<int> OnCoinCollected;
}
```

#### Player

```csharp
public class Player : MonoBehaviour
{
    private int coins = 0;

    private void OnTriggerEnter(Collider other)
    {
        if (other.CompareTag("Coin"))
        {
            coins++;
            EventBus.OnCoinCollected?.Invoke(coins);
            Destroy(other.gameObject);
        }
    }
}
```

#### UIManager

```csharp
public class UIManager : MonoBehaviour
{
    [SerializeField] private Text coinsText;

    private void OnEnable()
    {
        EventBus.OnCoinCollected += UpdateCoinUI;
    }

    private void OnDisable()
    {
        EventBus.OnCoinCollected -= UpdateCoinUI;
    }

    private void UpdateCoinUI(int totalCoins)
    {
        coinsText.text = "Coins: " + totalCoins;
    }
}
```

### Best practice in Unity

- Definire tutti gli eventi in un unico punto (EventBus o più bus tematici).
- Scollegare sempre i listener (OnDisable) per evitare memory leak.
- Evitare eventi “troppo generici” — mantenere nomi chiari e specifici.
- In progetti grandi, valutare ScriptableObject Event Channels per un flusso più editor-friendly.
