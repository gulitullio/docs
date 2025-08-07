---
title: YAGNI - You Aren’t Gonna Need It
sidebar_position: 3
---

E' un acronimo che sta per:

> **Non ne avrai bisogno**

È un principio nato nel contesto dello sviluppo Agile e promuove l'idea che **non bisogna scrivere codice o funzionalità che non servono oggi**, anche se pensiamo che **potrebbero** servire in futuro.

---

### Vantaggi

- **Velocità**: evita sprechi di tempo nello scrivere codice non richiesto
- **Semplicità**: riduce la complessità del progetto, rende più semplice un eventuale refactoring o manutenzione
- **Meno bug**: meno codice vuol dire meno bug da gestire o testare

---

### ❌ Esempio errato ❌

In questo esempio ci sono funzioni inutilizzate e premature, tempo sprecato per cose non richieste.

```csharp
public class InventorySystem : MonoBehaviour
{
    public void AddItem(string itemName) {
        Debug.Log("Item added: " + itemName);
        SaveToCloud(itemName);       // Not needed now
        SendAnalytics(itemName);     // Not required yet
        CheckAchievements(itemName); // Future feature
    }

    void SaveToCloud(string item) {
        Debug.Log("Saving to cloud..."); // Not implemented
    }

    void SendAnalytics(string item) {
        Debug.Log("Sending analytics..."); // Not used yet
    }

    void CheckAchievements(string item) {
        Debug.Log("Checking achievements..."); // Feature not planned
    }
}
```

---

### ✅ Esempio corretto ✅

E' presente solo il codice necessario, quando sarà il momento di aggiungere altre funzionalità (cloud, analytics...), lo farai con requisiti chiari e concreti.

```csharp
public class InventorySystem : MonoBehaviour
{
    public void AddItem(string itemName) {
        Debug.Log("Item added: " + itemName);
    }
}
```
