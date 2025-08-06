---
title: Incapsulamento
sidebar_position: 1
---

Consiste nel **nascondere i dettagli interni di un oggetto** e nell'esporre solo ciò che è necessario tramite metodi o proprietà.  
Questo permette di proteggere lo stato interno dell'oggetto e di controllarne l'accesso e la modifica.

Nei videogames, ad esempio, gli oggetti come personaggi, nemici o oggetti di gioco spesso hanno stati interni che non devono essere modificati arbitrariamente (es. salute, energia, munizioni). L'incapsulamento permette di garantire che queste variabili vengano modificate solo in modi controllati, mantenendo la coerenza dello stato di gioco.

---

## Esempio in C# - Personaggio di un gioco

```cs
public class Character
{
    // Qui vediamo che il campo è privato
    // Questo perché vogliamo accedervi solo con i metodi TakeDamage o Heal
    private int health;

    public int Health {
        get { return health; }
        private set {
            if (value < 0) health = 0;
            else if (value > MaxHealth) health = MaxHealth;
            else health = value;
        }
    }

    public int MaxHealth { get; private set; }

    public Character(int initialHealth, int maxHealth) {
        MaxHealth = maxHealth;
        Health = initialHealth;
    }

    public void TakeDamage(int damage) {
        if (damage < 0) throw new ArgumentException("Damage cannot be negative.");

        Health -= damage;
        if (Health == 0) Console.WriteLine("Character is dead!");
    }

    public void Heal(int amount) {
        if (amount < 0) throw new ArgumentException("Healing amount cannot be negative.");

        Health += amount;
    }
}
```
