---
title: MVVM (Model-View-ViewModel)
sidebar_position: 2
---

E' un pattern di progettazione che separa un'applicazione in tre parti:

- **Model**: Contiene i dati e la logica di gioco
- **View**: si occupa della rappresentazione visiva e dell'interfaccia utente
- **ViewModel**: agisce come ponte tra il Model e la View, gestendo lo stato e la logica di visualizzazione. Spesso implementa il **data binding** per aggiornare automaticamente la UI quando i dati cambiano.

Questo pattern è molto usato nelle applicazioni con interfacce reattive.

---

### Perché usarlo

- **Separazione chiara** tra dati, interfaccia e logica di visualizzazione
- **Aggiornamenti automatici della UI** con il data binding
- **Testabilità**: la logica di presentazione (ViewModel) può essere testata senza la View
- **Mantenibilità**: modificare la UI senza toccare la logica

---

## Quando usarlo

- Giochi con interfacce complesse e dinamiche (es. HUD dinamici, inventari, menu).
- Progetti in cui la UI cambia frequentemente in base allo stato di gioco.

---

## Esempio

Un gioco in cui il giocatore ha una barra della vita (HP) che si aggiorna automaticamente quando subisce danni.

- Il giocatore subisce danno → `playerViewModel.TakeDamage()`
- Il `ViewModel` aggiorna il `Model` e invia un evento.
- La `View` riceve l'evento e aggiorna la barra della vita.

#### Model

```csharp
public class PlayerModel
{
    public int MaxHealth { get; private set; }
    public int CurrentHealth { get; private set; }

    public PlayerModel(int maxHealth)
    {
        MaxHealth = maxHealth;
        CurrentHealth = maxHealth;
    }

    public void TakeDamage(int amount)
    {
        CurrentHealth = Mathf.Max(CurrentHealth - amount, 0);
    }
}
```

#### ViewModel

```csharp
public class PlayerViewModel
{
    private PlayerModel playerModel;
    public event Action<int, int> OnHealthChanged;

    public PlayerViewModel(PlayerModel model)
    {
        playerModel = model;
    }

    public void TakeDamage(int amount)
    {
        playerModel.TakeDamage(amount);
        OnHealthChanged?.Invoke(playerModel.CurrentHealth, playerModel.MaxHealth);
    }
}
```

#### View

```csharp
public class HealthBarView : MonoBehaviour
{
    public Slider healthSlider;

    public void UpdateHealth(int current, int max)
    {
        healthSlider.maxValue = max;
        healthSlider.value = current;
    }
}
```

#### GameManager

```csharp
public class GameManager : MonoBehaviour
{
    public HealthBarView healthBarView;
    private PlayerViewModel playerViewModel;

    private void Start()
    {
        var playerModel = new PlayerModel(100);
        playerViewModel = new PlayerViewModel(playerModel);

        playerViewModel.OnHealthChanged += healthBarView.UpdateHealth;
        healthBarView.UpdateHealth(playerModel.CurrentHealth, playerModel.MaxHealth);
    }

    private void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space))
        {
            playerViewModel.TakeDamage(10);
        }
    }
}
```
