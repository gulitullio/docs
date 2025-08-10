---
title: Entity-Component-System (ECS)
sidebar_position: 6
---

E' un paradigma architetturale molto usato nei motori di gioco moderni (Unity, Unreal, ecc.), nato per gestire in modo efficiente moltissimi oggetti di gioco e le loro interazioni.

Si basa su tre concetti chiave:

**Entity**

- È un contenitore logico (un ID univoco) che rappresenta un “oggetto” di gioco.
- Non ha logica e non ha dati di per sé.

Esempi: un nemico, un proiettile, un albero.

**Component**

- Sono strutture di dati puri che definiscono caratteristiche dell’entità.
- Niente logica, solo dati.

Esempi: Position (Vector3 value), Health (int current, int max), Velocity (Vector3 value)

**System**

- Contiene la logica che processa entità che hanno specifici componenti.

Esempio: un MovementSystem elabora tutte le entità che hanno Position e Velocity per aggiornarne la posizione.

---

### Perché usarlo

Rispetto al classico approccio OOP con GameObject + MonoBehaviour, ECS offre:

- **Performance**: i componenti sono memorizzati in array contigui in memoria → ottimizzazione della cache CPU (Data-Oriented Design).
- **Scalabilità**: perfetto per gestire decine di migliaia di entità senza crolli di framerate.
- **Separazione chiara**: tra logica nei System, dati nei Component, struttura nelle Entity → evita monoliti di MonoBehaviour di stato e logica.
- **Flessibilità**: cambiare il comportamento di un’entità è facile, aggiungi o rimuovi componenti.

---

### Quando usarlo

- Giochi con tante entità (sparatutto con centinaia di proiettili, RTS con migliaia di unità).
- Quando le performance sono critiche.
- Se vuoi logica fortemente decoupled e orientata ai dati.

---

### Come si usa in Unity

Unity ha introdotto l’ECS tramite il DOTS (Data-Oriented Technology Stack) che include:

- Entities (il core ECS)
- Jobs System (multi-threading)
- Burst Compiler (compilazione ottimizzata)

L’uso tipico:

- Crei Componenti come IComponentData (solo dati).
- Definisci System che filtrano le entità con certi componenti e applicano logica.
- Istanzi Entity aggiungendo componenti.

---

### Esempio

Abbiamo un gioco con proiettili che si muovono in avanti e scompaiono dopo un certo tempo.

#### Components

```csharp
public struct MoveSpeed : IComponentData
{
    public float Value;
}

public struct Lifetime : IComponentData
{
    public float Value;
}

public struct Direction : IComponentData
{
    public float3 Value;
}
```

#### System: movement

```csharp
[BurstCompile]
public partial struct MovementSystem : ISystem
{
    public void OnUpdate(ref SystemState state)
    {
        float deltaTime = SystemAPI.Time.DeltaTime;

        foreach (var (transform, speed, direction) in
                 SystemAPI.Query<RefRW<LocalTransform>, RefRO<MoveSpeed>, RefRO<Direction>>())
        {
            transform.ValueRW.Position += direction.ValueRO.Value * speed.ValueRO.Value * deltaTime;
        }
    }
}
```

#### System: lifetime

```csharp
[BurstCompile]
public partial struct LifetimeSystem : ISystem
{
    public void OnUpdate(ref SystemState state)
    {
        float deltaTime = SystemAPI.Time.DeltaTime;

        var ecb = new EntityCommandBuffer(Unity.Collections.Allocator.Temp);

        foreach (var (lifetime, entity) in SystemAPI.Query<RefRW<Lifetime>>().WithEntityAccess())
        {
            lifetime.ValueRW.Value -= deltaTime;

            if (lifetime.ValueRW.Value <= 0f)
            {
                ecb.DestroyEntity(entity);
            }
        }

        ecb.Playback(state.EntityManager);
    }
}
```

#### Entity

```csharp
public class BulletSpawner : MonoBehaviour
{
    public GameObject bulletPrefab;
    public float speed = 10f;
    public float lifeTime = 3f;

    private EntityManager manager;
    private Entity bulletEntityPrefab;

    void Start()
    {
        manager = World.DefaultGameObjectInjectionWorld.EntityManager;
        var settings = GameObjectConversionSettings.FromWorld(World.DefaultGameObjectInjectionWorld, null);
        bulletEntityPrefab = GameObjectConversionUtility.ConvertGameObjectHierarchy(bulletPrefab, settings);
    }

    void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space))
        {
            var bullet = manager.Instantiate(bulletEntityPrefab);

            manager.SetComponentData(bullet, new MoveSpeed { Value = speed });
            manager.SetComponentData(bullet, new Lifetime { Value = lifeTime });
            manager.SetComponentData(bullet, new Direction { Value = new float3(0, 0, 1) });
        }
    }
}
```
