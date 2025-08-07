---
title: Open/Closed Principle (OCP)
sidebar_position: 2
---

E' il secondo dei principi SOLID e afferma che:

> **"Il codice dovrebbe essere aperto all’estensione, ma chiuso alla modifica."**

In pratica, una classe, modulo o funzione **può essere estesa** per aggiungere nuove funzionalità, ma **non dovrebbe essere modificata** direttamente ogni volta che serve un cambiamento.

Nel mondo del gaming, sistemi come nemici, armi, poteri speciali o missioni cambiano spesso.  
Con OCP puoi **aggiungere nuovi comportamenti** senza rompere o riscrivere il codice esistente.

---

### ❌ Esempio che viola il principio ❌

Supponiamo di avere un sistema che gestisce danni basati sul tipo di nemico.  
Ogni volta che aggiungiamo un nuovo nemico, dobbiamo modificare questa classe.  
Non è "chiusa alla modifica", quindi viola OCP.

```csharp
public class CalcolatoreDanno
{
    public int CalcolaDanno(string tipoNemico)
    {
        if (tipoNemico == "Zombie")
            return 10;
        else if (tipoNemico == "Robot")
            return 20;
        else if (tipoNemico == "Alieno")
            return 30;

        return 0;
    }
}
```

---

### ✅ Esempio corretto ✅

Creiamo un'interfaccia **IEnemy** con un metodo **CalculateDamage()**, e poi implementiamo vari tipi di nemici.

In seguito, se vorremo aggiungere un nuovo nemico (Drago, Mutaforma, ecc.), possiamo farlo senza toccare il codice esistente ma solo aggiungendo nuove classi.

```csharp
public interface IEnemy
{
    int CalculateDamage();
}
```

```csharp
public class Zombie : IEnemy
{
    public int CalculateDamage() => 10;
}
```

```csharp
public class Robot : IEnemy
{
    public int CalculateDamage() => 20;
}
```

```csharp
public class Alien : IEnemy
{
    public int CalculateDamage() => 30;
}
```

```csharp
public class CombatSystem
{
    public void Attack(IEnemy enemy)
    {
        int damage = enemy.CalculateDamage();
        Console.WriteLine($"You took {damage} damage!");
    }
}
```
