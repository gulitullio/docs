---
title: DRY - Don't Repeat Yourself
sidebar_position: 1
---

E' una linea guida fondamentale nello sviluppo software, introdotta nel libro _The Pragmatic Programmer_.

> **Evita di ripetere porzioni di codice**

Ogni "conoscenza" nel sistema dovrebbe avere una singola rappresentazione non ambigua, autorevole e definitiva.

---

### Vantaggi

- **Semplicità**: codice più pulito e leggibile
- **Riutilizzo**: logiche comuni riutilizzabili
- **Manutenzione**: cambi il codice in un solo punto
- **Meno bug**: riduci il rischio di incoerenze tra duplicati

---

### ❌ Esempio errato ❌

```csharp
public class Enemy : MonoBehaviour
{
    void Die() {
        Debug.Log("Enemy died");
        Destroy(gameObject);
        AudioSource.PlayClipAtPoint(Resources.Load<AudioClip>("EnemyDeath"), transform.position);
    }
}
```

```csharp
public class Player : MonoBehaviour
{
    void Die() {
        Debug.Log("Player died");
        Destroy(gameObject);
        AudioSource.PlayClipAtPoint(Resources.Load<AudioClip>("PlayerDeath"), transform.position);
    }
}
```

---

### ✅ Esempio corretto ✅

```csharp
public class DeathHandler : MonoBehaviour
{
    public void HandleDeath(string deathSoundName) {
        Debug.Log($"{gameObject.name} died");
        Destroy(gameObject);
        AudioSource.PlayClipAtPoint(Resources.Load<AudioClip>(deathSoundName), transform.position);
    }
}
```

```csharp
public class Enemy : MonoBehaviour
{
    DeathHandler deathHandler;

    public void Die() {
        deathHandler.HandleDeath("EnemyDeath");
    }
}
```

```csharp
public class Player : MonoBehaviour
{
    DeathHandler deathHandler;

    public void Die() {
        deathHandler.HandleDeath("PlayerDeath");
    }
}
```
