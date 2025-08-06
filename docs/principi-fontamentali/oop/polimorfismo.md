---
title: Polimorfismo
sidebar_position: 3
---

Il termine polimorfismo deriva dal greco e significa “molte forme”.  
In programmazione, significa che lo stesso metodo può comportarsi in modo diverso a seconda dell’oggetto che lo implementa.

Questo principio consente di utilizzare oggetti di classi diverse attraverso un’interfaccia comune.

Immagina di avere un gioco in cui vari personaggi possono attaccare, ma ogni tipo di personaggio ha un modo diverso di attaccare.  
Usiamo il polimorfismo per chiamare il metodo Attack() su un elenco di personaggi, senza preoccuparci del loro tipo specifico.

### Classe base

```cs
public class Character
{
    public string Name { get; set; }

    public Character(string name) {
        Name = name;
    }

    public virtual void Attack() {
        Console.WriteLine($"{Name} performs a generic attack.");
    }
}
```

### Classi derivate

```cs
public class Archer : Character
{
    public Archer(string name) : base(name) { }

    public override void Attack() {
        Console.WriteLine($"{Name} shoots an arrow!");
    }
}

public class Knight : Character
{
    public Knight(string name) : base(name) { }

    public override void Attack() {
        Console.WriteLine($"{Name} strikes with a sword!");
    }
}
```

### Esempio di polimorfismo

```cs
public class Game
{
    public static void Main() {
        List<Character> party = new List<Character> {
            new Archer("Elena"),
            new Knight("Baldric"),
        };

        foreach (var character in party) {
            character.Attack();
        }
    }
}
```
