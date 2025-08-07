---
title: Interface Segregation Principle (ISP)
sidebar_position: 4
---

E' il quarto principio dei SOLID.

> **"I client non dovrebbero essere costretti a dipendere da interfacce che non usano."**

In altre parole, è meglio avere **interfacce piccole e specifiche** piuttosto che una grande interfaccia generica che obbliga le classi a fornire metodi inutili.

---

### Vantaggi ISP

- Le classi sono più coerenti con il loro comportamento reale
- Il codice è più facile da leggere, testare e mantenere
- Nessuna classe è costretta a implementare metodi inutili

---

### ❌ Esempio che viola il principio ❌

In questo esempio, abbiamo un'interfaccia `ICharacter` troppo generica che include metodi che **non tutti i personaggi possono o devono usare**:
Immagina, ad esempio, di avere una classe Warrior che implementa questa interfaccia: è costretta a implementare metodi che non le servono, violando il principio ISP.
Questo rende il codice fragile e meno leggibile.

```csharp
public interface ICharacter
{
    void Attack();
    void CastSpell();
    void Heal();
}
```

```csharp
public class Warrior : ICharacter
{
    public void Attack() {
        Console.WriteLine("Warrior attacks with sword!");
    }

    public void CastSpell() {
        throw new NotImplementedException("Warrior can't cast spells.");
    }

    public void Heal() {
        throw new NotImplementedException("Warrior can't heal.");
    }
}
```

---

### ✅ Esempio corretto ✅

All'esempio precedente, applichiamo il principio creando interfacce più piccole e specifiche:

```csharp
public interface IAttacker
{
    void Attack();
}

public interface ISpellCaster
{
    void CastSpell();
}

public interface IHealer
{
    void Heal();
}
```

Ora le classi possono implementare solo le funzionalità che servono

```csharp
public class Warrior : IAttacker
{
    public void Attack() {
        Console.WriteLine("Warrior attacks with sword!");
    }
}
```

```csharp
public class Mage : IAttacker, ISpellCaster
{
    public void Attack() {
        Console.WriteLine("Mage attacks with staff!");
    }

    public void CastSpell() {
        Console.WriteLine("Mage casts a fireball!");
    }
}
```

```csharp
public class Priest : IHealer
{
    public void Heal() {
        Console.WriteLine("Priest heals the party!");
    }
}
```
