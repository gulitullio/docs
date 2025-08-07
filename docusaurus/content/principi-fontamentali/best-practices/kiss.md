---
title: KISS - Keep It Simple, Stupid
sidebar_position: 2
---

E' un principio fondamentale della programmazione e dell'ingegneria del software

> **Rendi il codice il più semplice possibile**

Significa che dovresti evitare di scrivere codice inutilmente complesso, durante la scrittura di nuove funzionalità dovresti chiederti "sto complicando troppo?"

N.B. Non significa sacrificare l'architettura ma trovare il modo più semplice per risolvere un problema senza over-engineering, è facile cadere nella trappola di creare strutture complesse anche per problemi semplici.

---

### Vantaggi

- **Leggibilità**: il codice è comprensibile anche da altri sviluppatori (o da te stesso in futuro).
- **Sviluppo più veloce**: quando il codice è semplice, aggiungere nuove funzionalità è più immediato.
- **Mantenibilità**: meno complessità = meno bug.
- **Testing**: meno rami di esecuzione = test più semplici.

---

### ❌ Esempio errato ❌

In questo esempio, la classe `ComplexPlayerMovement` presenta funzioni inutili per operazioni semplici (GetAxis, CalculateMovement, GetSpeedFactor).  
Il codice è difficile da leggere e mantenere per qualsiasi altro sviluppatore del team.

```csharp
public class ComplexPlayerMovement : MonoBehaviour
{
    private Vector3 movement;
    private Rigidbody rb;

    void Start() {
        rb = GetComponent<Rigidbody>();
    }

    void Update() {
        float horizontalInput = GetAxis("Horizontal");
        float verticalInput = GetAxis("Vertical");
        movement = CalculateMovement(horizontalInput, verticalInput);
    }

    void FixedUpdate() {
        MovePlayer(movement);
    }

    float GetAxis(string axisName) {
        return Mathf.Clamp(Input.GetAxis(axisName), -1f, 1f);
    }

    Vector3 CalculateMovement(float x, float z) {
        Vector3 move = new Vector3(x * GetSpeedFactor(), 0f, z * GetSpeedFactor());
        return move;
    }

    float GetSpeedFactor() {
        return Mathf.Pow(2f, 1f);
    }

    void MovePlayer(Vector3 direction) {
        if (direction != Vector3.zero) {
            rb.MovePosition(transform.position + direction * Time.fixedDeltaTime);
        }
    }
}
```

---

### ✅ Esempio corretto ✅

Codice chiaro, diretto, leggibile. Fa esattamente ciò che serve, senza complicazioni inutili.

```csharp
public class SimplePlayerMovement : MonoBehaviour
{
    public float speed = 5f;
    private Rigidbody rb;

    void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    void FixedUpdate()
    {
        float moveX = Input.GetAxis("Horizontal");
        float moveZ = Input.GetAxis("Vertical");

        Vector3 movement = new Vector3(moveX, 0f, moveZ) * speed * Time.fixedDeltaTime;
        rb.MovePosition(transform.position + movement);
    }
}
```
