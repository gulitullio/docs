---
title: Collision resolution
sidebar_position: 2
---

In ambito gaming e simulazioni, quando due o più oggetti si scontrano (collision detection), serve una logica per gestire cosa succede dopo: questo processo si chiama collision resolution.

In pratica, la collision resolution risponde a domande tipo:

- Come devo spostare gli oggetti per evitare che restino incastrati?
- Come calcolo la risposta fisica (rimbalzo, attrito, ecc)?
- Quale comportamento devo applicare in base al tipo di oggetto (muro, nemico, power-up)?

Senza un’adeguata collision resolution, le collisioni sarebbero solo rilevate ma non risolte, quindi:

- Oggetti potrebbero sovrapporsi (clipping)
- Personaggi potrebbero passare attraverso muri
- L’esperienza di gioco sarebbe incoerente o frustrante

---

### Tipi comuni di Collision Resolution

- **Separazione Posizionale**: Spostare gli oggetti fuori dalla collisione
- **Impulse-based**: Applicare un impulso per simulare rimbalzi
- **Penetration Depth**: Calcolare la profondità di sovrapposizione e correggerla
- **Continuous Collision Resolution**: Usata per oggetti veloci per evitare di “saltare” attraverso collider

---

### Esempio

Supponiamo di voler gestire la collisione di un player con un muro usando un semplice metodo di separazione posizionale.

- Alla collisione, otteniamo il punto di contatto e la normale della superficie del muro
- Calcoliamo la penetrazione come proiezione del punto di contatto sulla normale
- Spostiamo il player lungo quella direzione per risolvere la sovrapposizione
- Cambiamo la velocità riflettendola sulla normale per simulare un piccolo rimbalzo

```csharp
public class SimpleCollisionResolution : MonoBehaviour
{
    public Rigidbody2D rb;
    public Collider2D playerCollider;

    void OnCollisionEnter2D(Collision2D collision)
    {
        // Prendiamo il primo punto di contatto
        ContactPoint2D contact = collision.contacts[0];

        // Direzione di separazione: il normale al punto di contatto
        Vector2 separationDirection = contact.normal;

        // Profondità di penetrazione (stimata)
        float penetrationDepth = Mathf.Abs(Vector2.Dot(contact.point - (Vector2)rb.position, separationDirection));

        // Spostiamo il player fuori dal muro
        rb.position += separationDirection * penetrationDepth;

        // Facciamo rimbalzare leggermente il player all'indietro
        Vector2 velocity = rb.velocity;
        velocity = Vector2.Reflect(velocity, separationDirection) * 0.5f; // dimezziamo la velocità per simulare attrito
        rb.velocity = velocity;
    }
}
```
