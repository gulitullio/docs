---
title: Component-Based Architecture
sidebar_position: 4
---

E' un approccio di progettazione del software in cui le funzionalità di un sistema non vengono organizzate in lunghe gerarchie di classi (come nell’OOP classica), ma vengono composte tramite unità indipendenti chiamate componenti.

Ogni componente:

- È focalizzato su una **singola responsabilità** (principio SRP).
- È **riutilizzabile** in contesti diversi.
- È intercambiabile e **indipendente** dal resto del codice.

Un esempio pratica potrebbero essere i componenti di Unity:

- Ogni GameObject è come un "contenitore" dove i comportamenti sono definiti da componenti (script, renderer, collider, ecc.).
- Invece di ereditare da un’unica mega-classe, il GameObject può avere tanti piccoli script che cooperano.

---

### Perché usarla

Rispetto al classico approccio “eredito da Character e poi specializzo in Enemy o Player”:

- **Maggiore riuso**: lo stesso componente “Health” può essere usato su nemici, giocatori, NPC, torrette...
- **Minore accoppiamento**: i componenti non dipendono dalla struttura gerarchica delle classi.
- **Estendibilità dinamica**: in Unity puoi aggiungere/rimuovere componenti a runtime senza cambiare il codice base.
- **Facile testing**: puoi testare singoli componenti in isolamento.

In generale in giochi complessi (es. RPG), evita classi da 2000 righe e ti permette di evolvere più facilmente il gameplay.

---

### Quando usarlo

- Se il tuo gioco/programma è destinato a evolvere nel tempo, con molte nuove feature o comportamenti,
- Quando vuoi poter riusare lo stesso comportamento su entità diverse senza duplicare codice.
- Ogni componente è “plug-and-play” e può essere applicato a qualunque oggetto compatibile.
- Team diversi possono lavorare su componenti separati senza conflitti sugli stessi file.
- Se il gameplay prevede aggiungere o rimuovere comportamenti a runtime
- L’approccio OOP tradizionale può portare a catene di ereditarietà complesse (Entity → Character → Enemy → FlyingEnemy → BossFlyingEnemy) che diventano fragili

---

### Come usarla

- Identifica i comportamenti indipendenti (movimento, salute, IA, inventario, ecc.).
- Implementa ciascun comportamento come componente autonomo.
- Associa i componenti all'object che li deve avere.
- I componenti comunicano tra loro tramite: eventi o interfacce

---

### Esempio

Supponiamo di avere un giocatore con:

- Movimento (PlayerMovement)
- Sistema di salute (Health)
- Arma (Weapon)

La struttura sarà la seguente:

```
Player (GameObject)
 ├── PlayerMovement (script)
 ├── Health (script)
 ├── Weapon (script)
 ├── SpriteRenderer
 └── Rigidbody2D
```

In pratica crei un GameObject Player, gli aggiungi i componenti PlayerMovement, Health, Weapon (oltre a collider, rigidbody, ecc.).
I componenti non sono gerarchicamente collegati da ereditarietà: sono indipendenti e collaborano.

#### Health

```csharp
public class Health : MonoBehaviour
{
    [SerializeField] private int maxHealth = 100;
    private int currentHealth;

    public System.Action OnDeath;

    private void Awake()
    {
        currentHealth = maxHealth;
    }

    public void TakeDamage(int amount)
    {
        currentHealth -= amount;
        if (currentHealth <= 0)
        {
            currentHealth = 0;
            OnDeath?.Invoke();
        }
    }

    public void Heal(int amount)
    {
        currentHealth = Mathf.Min(currentHealth + amount, maxHealth);
    }
}
```

#### PlayerMovement

```csharp
[RequireComponent(typeof(Rigidbody2D))]
public class PlayerMovement : MonoBehaviour
{
    [SerializeField] private float speed = 5f;
    private Rigidbody2D rb;
    private Vector2 input;

    private void Awake()
    {
        rb = GetComponent<Rigidbody2D>();
    }

    private void Update()
    {
        input = new Vector2(Input.GetAxisRaw("Horizontal"), Input.GetAxisRaw("Vertical")).normalized;
    }

    private void FixedUpdate()
    {
        rb.MovePosition(rb.position + input * speed * Time.fixedDeltaTime);
    }
}
```

#### Weapon

```csharp
public class Weapon : MonoBehaviour
{
    [SerializeField] private GameObject bulletPrefab;
    [SerializeField] private Transform firePoint;

    void Update()
    {
        if (Input.GetButtonDown("Fire1"))
        {
            Shoot();
        }
    }

    private void Shoot()
    {
        Instantiate(bulletPrefab, firePoint.position, firePoint.rotation);
    }
}

```
