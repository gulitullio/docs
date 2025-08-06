---
title: Ereditarietà
sidebar_position: 2
---

Permette di creare nuove classi che riutilizzano, estendono o modificano il comportamento di una classe esistente.

In termini semplici, una classe derivata (o "figlia") eredita le proprietà e i metodi di una classe base (o "madre"), potendo aggiungere nuove funzionalità o sovrascrivere quelle esistenti.

Immaginiamo di avere un gioco in cui esistono diversi tipi di personaggi: guerrieri, maghi, arcieri.  
Tutti condividono alcune caratteristiche comuni come salute, danni, movimento.  
In questo caso, possiamo creare una classe base Character e poi creare classi derivate come Warrior, Mage, ecc.

### Classe base

```cs
public class Character
{
    public string Name { get; set; }
    public int Health { get; protected set; }

    public Character(string name, int health)
    {
        Name = name;
        Health = health;
    }

    public virtual void Attack()
    {
        Console.WriteLine($"{Name} attacks with a basic strike!");
    }

    public void TakeDamage(int damage)
    {
        Health -= damage;
        Console.WriteLine($"{Name} takes {damage} damage. Remaining health: {Health}");
    }
}
```

### Classe derivata o figlia

```cs
public class Warrior : Character
{
    public Warrior(string name, int health) : base(name, health) {}

    public override void Attack()
    {
        Console.WriteLine($"{Name} swings a mighty sword!");
    }
}

// Derived class
public class Mage : Character
{
    public Mage(string name, int health) : base(name, health) {}

    public override void Attack()
    {
        Console.WriteLine($"{Name} casts a fireball!");
    }
}
```
