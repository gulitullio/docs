---
title: Pathfinding
sidebar_position: 3
---

Il pathfinding è la tecnica usata per trovare il percorso migliore (o uno percorso ottimale) tra due punti in un ambiente, tipicamente rappresentato da una griglia, un grafo o una mappa.
È fondamentale in giochi, robotica, AI, navigazione e simulazioni.

- **Navigazione AI**: per far muovere NPC (non-player characters) in modo intelligente nel mondo di gioco, evitando ostacoli.
- **Ottimizzazione del percorso**: per trovare la strada più breve o più efficiente tra punti.
- **Realismo**: migliora il gameplay rendendo il movimento degli NPC più credibile.
- **Gestione dinamica**: adattarsi a cambiamenti della mappa o ostacoli in tempo reale.

### Algoritmi più usati

- **A\* (A star)**: cerca il percorso più efficiente usando una combinazione di costo già sostenuto (distanza dal punto di partenza) e una stima del costo residuo (euristica) per arrivare alla destinazione. È un best-first search informato.
- **Dijkstra**: trova il percorso più breve da un nodo a tutti gli altri, ma non usa euristica quindi è meno efficiente di A\* in molti casi.
- **BFS (Breadth-First Search)**: trova il percorso più breve in grafi non pesati, ma non è efficiente su grandi mappe.
- **DFS (Depth-First Search)**: non garantisce il percorso più breve, spesso usato in esplorazione.

N.B. Unity ha un sistema built-in di pathfinding chiamato **NavMesh**

### A\* in breve

- Mantiene una open list di nodi da esplorare e una closed list di nodi già esplorati.
- Calcola il costo totale f(n) = g(n) + h(n), dove:
- g(n) = costo dal nodo iniziale al nodo n
- h(n) = stima (euristica) dal nodo n al nodo obiettivo
- Sceglie di espandere il nodo con il costo totale più basso.
- Continua finché non raggiunge il nodo obiettivo.
