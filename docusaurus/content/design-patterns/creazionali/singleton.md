---
title: Singleton
sidebar_position: 1
---

E' un design pattern **creazionale** che garantisce l’esistenza di **una sola istanza** di una classe durante l’esecuzione dell’applicazione e fornisce un **punto di accesso globale** a questa istanza.

**Caratteristiche principali:**

1. **Istanza unica** → Solo un oggetto può esistere.
2. **Accesso globale** → L’istanza è accessibile ovunque.
3. **Creazione controllata** → L’oggetto viene creato solo quando serve.

E' quindi usato spesso per:

- Gestire **managers** (es. GameManager, AudioManager, UIManager)
- Mantenere **dati persistenti** tra scene
- **Evitare duplicazioni** di oggetti di servizio

---

### Quando usarlo ✅

Il Singleton è utile quando:

- Un oggetto deve coordinare operazioni a livello globale (es. sistema di salvataggio, configurazione globale, log).
- Si deve evitare la creazione multipla dello stesso servizio.
- Serve un **punto di accesso centralizzato**.

---

### Quando NON usarlo ❌

Abusare del Singleton può rendere il codice difficile da testare, fortemente accoppiato e meno flessibile.

Da evitare quando:

- Si può passare l’oggetto tramite **dependency injection**.
- Si vuole favorire la modularità e il riuso.

---

### Esempio

- GameManager.Instance è accessibile ovunque.
- Solo una istanza vive durante tutta l’applicazione.
- Persistente tra scene.

```csharp
public class GameManager : MonoBehaviour
{
    public static GameManager Instance { get; private set; }
    public int score;

    void Awake()
    {
        if (Instance != null && Instance != this)
        {
            Destroy(gameObject); // Evita duplicati
            return;
        }

        Instance = this;
        DontDestroyOnLoad(gameObject); // Persiste tra scene
    }

    public void AddScore(int points)
    {
        score += points;
    }
}
```
