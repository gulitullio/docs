---
title: Liskov Substitution Principle (LSP)
sidebar_position: 3
---

E' il terzo principio SOLID e riguarda il modo in cui le classi derivate devono comportarsi rispetto alle classi base.

> **"Le classi figlie devono poter essere usate al posto delle classi genitore senza effetti collaterali o comportamenti inattesi"**.

Se S è una sottoclasse di T, allora gli oggetti di tipo T possono essere sostituiti con oggetti di tipo S senza alterare la correttezza del programma.

---

### ❌ Esempio che viola il principio ❌

Immaginiamo di avere una classe base `Bird` con un metodo `Fly()`, e di derivare una classe `Penguin` (che però non può volare).  
Il codice presume che ogni `Bird` possa volare. Ma quando usiamo un `Penguin`, otteniamo un'eccezione.  
Quindi la sostituzione della sottoclasse rompe il comportamento previsto, violando il principio di Liskov.

```csharp
public class Bird
{
    public virtual void Fly() {
        Console.WriteLine("Flying...");
    }
}
```

```csharp
public class Penguin : Bird
{
    public override void Fly() {
        throw new NotImplementedException("Penguins can't fly!");
    }
}
```

```csharp
public class BirdHandler
{
    public void MakeBirdFly(Bird bird) {
        bird.Fly(); // Will crash if bird is a Penguin
    }
}
```

---

### ✅ Esempio corretto ✅

Separiamo il concetto di "uccello che vola" da "uccello che non vola" usando un'interfaccia specifica per il volo.  
Solo le classi che possono veramente volare implementano IFlyingBird, nn questo modo non abbiamo alcuna eccezione.

```csharp
public class Bird
{
    public string Name { get; set; }
}

public interface IFlyingBird
{
    void Fly();
}
```

```csharp
public class Sparrow : Bird, IFlyingBird
{
    public void Fly() {
        Console.WriteLine("Sparrow flying!");
    }
}
```

```csharp
public class Penguin : Bird
{
    // Penguins do not implement IFlyingBird
}
```

```csharp
public class BirdHandler
{
    public void MakeBirdFly(IFlyingBird bird)
    {
        bird.Fly(); // Safe: only birds that can fly are passed
    }
}
```
