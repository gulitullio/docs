---
title: Dependency Inversion Principle (DIP)
sidebar_position: 5
---

E' il quinto e ultimo principio SOLID.

È fondamentale per scrivere codice disaccoppiato, flessibile e facile da testare.

> **"Una classe non dovrebbe dipendere direttamente da classi concrete, ma da interfacce o astrazioni"**

I moduli di alto livello non dovrebbero dipendere da moduli di basso livello, dovrebbero dipendere dalle astrazioni.  
Le astrazioni non dovrebbero dipendere dai dettagli ma, viceversa, i dettagli dovrebbero dipendere dalle astrazioni.

---

### ❌ Esempio che viola il principio ❌

In questo esempio, una classe `GameManager` dipende direttamente da una classe concreta `FileLogger`.

Non puoi facilmente sostituire `FileLogger` con un altro sistema (es. `ConsoleLogger`, `DatabaseLogger`, `MockLogger`)

```csharp
public class FileLogger
{
    public void Log(string message) {
        File.AppendAllText("log.txt", message + Environment.NewLine);
    }
}
```

```csharp
public class GameManager
{
    private FileLogger logger;

    public GameManager() {
        logger = new FileLogger(); // Tight coupling
    }

    public void StartGame() {
        logger.Log("Game started.");
    }
}
```

---

### ✅ Esempio corretto ✅

Definiamo un’interfaccia `ILogger` e usiamo l’inversione delle dipendenze:

```csharp
public interface ILogger
{
    void Log(string message);
}
```

```csharp
public class FileLogger : ILogger
{
    public void Log(string message) {
        File.AppendAllText("log.txt", message + Environment.NewLine);
    }
}
```

```csharp
public class ConsoleLogger : ILogger
{
    public void Log(string message) {
        Console.WriteLine(message);
    }
}
```

```csharp
public class GameManager
{
    private readonly ILogger logger;

    public GameManager(ILogger logger) {
        this.logger = logger;
    }

    public void StartGame() {
        logger.Log("Game started.");
    }
}
```

```csharp
var logger = new FileLogger();
var gameManager = new GameManager(logger);
gameManager.StartGame();
```
