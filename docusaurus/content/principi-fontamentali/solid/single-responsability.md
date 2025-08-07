---
title: Single Responsibility Principle (SRP)
sidebar_position: 1
---

E' il primo principio dei SOLID la cui definizione è:

> **"Una classe dovrebbe avere una, e una sola, responsabilità."**

In pratica dovrebbe esistere una sola ragione per cui quella classe debba essere cambiata.  
Quando una classe ha più responsabilità, può diventare difficile da modificare, testare o estendere senza causare effetti collaterali inaspettati.

---

### Vantaggi

- Le classi sono più semplici da capire e da testare
- I cambiamenti futuri non rischiano di rompere logiche già esistenti

---

### ❌ Esempio che viola il principio ❌

Supponiamo di avere un personaggio in un gioco che:

- gestisce la salute e i danni subiti
- stampa le informazioni su schermo
- salva i dati su file

Tutte queste responsabilità in **una sola classe** violano il principio di singola responsabilità.

```csharp
public class Player
{
    public string Name { get; set; }
    public int Health { get; private set; }

    public Player(string name) {
        Name = name;
        Health = 100;
    }

    public void TakeDamage(int damage) {
        Health = Math.Max(Health - damage, 0);
    }


    public void ShowStats() {
        Console.WriteLine($"{p.Name} has {p.Health} HP.");
    }

    public void Save() {
        File.WriteAllText("player.txt", $"{p.Name},{p.Health}");
    }
}
```

---

### ✅ Esempio corretto ✅

Classe giocatore con la sola gestione della salute

```csharp
public class Player
{
    public string Name { get; set; }
    public int Health { get; private set; }

    public Player(string name) {
        Name = name;
        Health = 100;
    }

    public void TakeDamage(int damage) {
        Health = Math.Max(Health - damage, 0);
    }
}
```

Classe separata per mostrare le statistiche

```csharp
public class StatDisplayer
{
    public void ShowStats(Player p) {
        Console.WriteLine($"{p.Name} has {p.Health} HP.");
    }
}
```

Classe separata per salvare i dati del giocatore

```csharp
public class PlayerSaver
{
    public void Save(Player p) {
        File.WriteAllText("player.txt", $"{p.Name},{p.Health}");
    }
}

```
