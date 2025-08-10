---
title: MVC (Model-View-Controller)
sidebar_position: 1
---

E' un pattern di progettazione che separa un'applicazione in tre componenti principali:

- **Model**: gestisce i dati e la logica di gioco
- **View**: si occupa della rappresentazione visiva e dell'interfaccia utente
- **Controller**: riceve gli input dell'utente, aggiorna il model e comanda la view

---

### Perché usarlo

- **Separazione chiara** tra logica di gioco, visualizzazione e input
- **Facile manutenzione**: modificare una parte non influisce sulle altre
- **Testabilità**: è possibile testare la logica di gioco senza la grafica
- **Collaborazione**: facilita il lavoro in team (programmatori, artisti, game designer)

---

### Quando usarlo

- Progetti dove si vuole una separazione netta tra UI e logica di gioco.
- Giochi single player o multiplayer con logica di gioco complessa.

---

### Esempio

Un semplice scenario in cui il giocatore raccoglie punti e il punteggio viene mostrato su schermo.

- Il giocatore raccoglie una moneta → Il `GameController` rileva l'evento
- Il `GameController` aggiorna il `PlayerModel` → `playerModel.AddScore(10)`
- La `ScoreView` viene aggiornata → `scoreView.UpdateScore(...)`

#### Model

```csharp
public class PlayerModel
{
    public int Score { get; private set; }

    public void AddScore(int amount)
    {
        Score += amount;
    }
}
```

#### View

```csharp
public class ScoreView : MonoBehaviour
{
    public Text scoreText;

    public void UpdateScore(int score)
    {
        scoreText.text = "Score: " + score;
    }
}
```

#### Controller

```csharp
public class GameController : MonoBehaviour
{
    public PlayerModel playerModel;
    public ScoreView scoreView;

    private void Start()
    {
        playerModel = new PlayerModel();
        scoreView.UpdateScore(playerModel.Score);
    }

    public void OnCoinCollected()
    {
        playerModel.AddScore(10);
        scoreView.UpdateScore(playerModel.Score);
    }
}
```
