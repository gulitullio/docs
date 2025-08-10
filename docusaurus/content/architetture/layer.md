---
title: Layered Architecture (Architettura a livelli)
sidebar_position: 3
---

Il Layered Architecture (o “architettura a strati”) è un modello di progettazione del software dove il codice è organizzato in **livelli distinti**, ognuno con un compito chiaro. Ogni layer **comunica solo con quello immediatamente sottostante** (o, in alcuni casi, tramite interfacce ben definite).

Struttura tipica:

- **Presentation Layer (UI)** → interagisce con l’utente/giocatore
- **Application Layer** → coordina i casi d’uso, applica logica di flusso
- **Domain Layer** → contiene la logica di gioco (regole, validazioni, ecc.)
- **Infrastructure Layer** → si occupa di persistenza, file, rete, database, API

---

### Perché usarlo

- **Mantenibilità** → Ogni parte è separata, modificabile senza toccare il resto
- **Testabilità** → Il dominio e l’applicazione possono essere testati senza caricare dipendenze
- **Riutilizzo** → La logica di gioco può essere riutilizzata in altri progetti
- **Scalabilità** → Il progetto cresce in modo ordinato senza diventare “spaghetti code”

---

### Quando usarlo

- Per evitare che ogni script sia un miscuglio di UI, gameplay e salvataggio.
- Per rendere più semplice cambiare motore grafico o sistema di input.
- Per separare la logica dal rendering e dagli oggetti.

---

### Esempio

Un’architettura a strati di esempio potrebbe essere la seguente:

- I MonoBehaviour vivono solo nel Presentation Layer (UI)
- La logica core del gioco vive nel Domain Layer (classi pure, senza dipendere da Unity).
- La gestione di file, DB o API è delegata all’Infrastructure Layer.
- La coordinazione delle azioni (ad esempio “avvia partita”, “aggiorna punteggio”) avviene nell’Application Layer.

#### Domain

```csharp
public class Player
{
    public string Name { get; private set; }
    public int Score { get; private set; }

    public Player(string name)
    {
        Name = name;
        Score = 0;
    }

    public void AddScore(int points)
    {
        if (points < 0) throw new System.ArgumentException("Points cannot be negative");
        Score += points;
    }
}
```

#### Infrastructure Layer

```csharp
public class PlayerDataRepository
{
    private string _savePath => Path.Combine(Application.persistentDataPath, "player.json");

    public void Save(Player player)
    {
        string json = JsonUtility.ToJson(player);
        File.WriteAllText(_savePath, json);
    }

    public Player Load()
    {
        if (!File.Exists(_savePath))
            return new Player("Guest");

        string json = File.ReadAllText(_savePath);
        return JsonUtility.FromJson<Player>(json);
    }
}

```

#### Application Layer

```csharp
public class GameService
{
    private Player _player;

    public GameService(Player player)
    {
        _player = player;
    }

    public void AddPointsToPlayer(int points)
    {
        _player.AddScore(points);
        // Qui potresti inviare eventi o notifiche alla UI
    }

    public int GetPlayerScore() => _player.Score;
}
```

#### Presentation Layer (Unity)

```csharp
public class GameUIController : MonoBehaviour
{
    [SerializeField] private Text scoreText;
    private GameService _gameService;
    private PlayerDataRepository _repository;

    void Start()
    {
        _repository = new PlayerDataRepository();
        var player = _repository.Load();
        _gameService = new GameService(player);

        UpdateUI();
    }

    public void OnAddPointsButtonClicked()
    {
        _gameService.AddPointsToPlayer(10);
        UpdateUI();
    }

    private void UpdateUI()
    {
        scoreText.text = "Score: " + _gameService.GetPlayerScore();
    }

    private void OnApplicationQuit()
    {
        _repository.Save(new Player("Player") { /* eventualmente recupera i dati */ });
    }
}
```
