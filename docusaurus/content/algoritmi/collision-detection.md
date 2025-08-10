---
title: Collision detection
sidebar_position: 1
---

Gli algoritmi di collision detection servono a determinare se due o più oggetti in un ambiente virtuale si intersecano o entrano in contatto.  
Sono fondamentali nei videogiochi, simulazioni fisiche, realtà virtuale, CAD e robotica.

In pratica, senza collision detection:

- I personaggi passerebbero attraverso i muri
- I proiettili attraverserebbero i nemici senza colpirli
- Gli oggetti non reagirebbero realisticamente alla fisica

---

### Perché usarli

- **Prestazioni**: gli algoritmi ben implementati evitano sprechi di calcolo, rilevando collisioni solo quando serve.
- **Fisica**: consentire a Unity (o altri motori) di calcolare reazioni (rimbalzi, attriti, ecc.).
- **Gameplay**: rilevare eventi come “colpito da un proiettile”, “entrato in una zona”, “raccolto un oggetto”.

---

### Come funzionano

Generalmente, il processo ha due fasi:

**Broad Phase** (fase larga)

- Filtra velocemente coppie di oggetti che potrebbero collidere.
- Usa bounding boxes semplici (AABB - Axis-Aligned Bounding Box, o Sphere Bounds).

Algoritmi tipici: Spatial Partitioning (QuadTree, Octree, BSP trees, Grid).

**Narrow Phase** (fase ristretta)

- Calcola con più precisione la collisione solo per le coppie candidate.
- Usa formule geometriche complesse (intersezione tra poligoni, mesh, capsule, ecc.).

---

### Tipi comuni di Collision Detection

- AABB vs AABB: collisione tra due rettangoli/cubi allineati agli assi
- Sphere vs Sphere: controllo rapido basato su raggio
- Raycasting: utile per linee di vista, proiettili, selezioni
- OBB (Oriented Bounding Box): bounding box ruotata
- Mesh vs Mesh: più costosa, usata solo se serve estrema precisione

---

### In Unity

Unity ha già un sistema di collision detection integrato nel Physics Engine:

- Collider: componenti che definiscono la forma per la collisione (BoxCollider, SphereCollider, MeshCollider, ecc.).
- Rigidbody: per consentire alla fisica di muovere l’oggetto.
- Trigger: colliders che non bloccano ma segnalano il passaggio di un oggetto.

Eventi principali:

- OnCollisionEnter, OnCollisionStay, OnCollisionExit
- OnTriggerEnter, OnTriggerStay, OnTriggerExit
