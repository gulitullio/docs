---
title: Convenzioni in Unreal
sidebar_position: 5
---

Unreal Engine utilizza convenzioni di scrittura particolari, definite da **Epic Games**, per garantire coerenza e chiarezza nel codice.  
Ecco una panoramica dei principali stili usati:

---

## Prefissi Speciali

Unreal Engine utilizza prefissi specifici per indicare il tipo o il ruolo delle entità:

- `U` → Classi derivate da `UObject` (es. `UTexture`, `UWidget`)
- `A` → Classi derivate da `AActor` (es. `ACharacter`, `AEnemy`)
- `F` → Struct (es. `FVector`, `FRotator`, `FTransform`)
- `I` → Interfacce (es. `IInteractable`)
- `b` → Variabili booleane (`bIsAlive`, `bHasKey`)
- `E` → Enum (`EWeaponType`, `EGameState`)

---

## Convenzioni Generali

| Elemento             | Stile                         | Esempio                             |
| -------------------- | ----------------------------- | ----------------------------------- |
| **Classi UE**        | `UPascalCase` / `APascalCase` | `UUserWidget`, `APlayerController`  |
| **Variabili membro** | `PascalCase` con prefisso     | `Health`, `bIsAlive`, `MyComponent` |
| **Variabili locali** | `camelCase`                   | `enemyCount`, `deltaTime`           |
| **Metodi**           | `PascalCase`                  | `TakeDamage()`                      |
| **Costanti**         | `SCREAMING_SNAKE_CASE`        | `MAX_PLAYER_COUNT`                  |

---

## Esempi

```cpp
UCLASS()
class AMyCharacter : public ACharacter
{
    GENERATED_BODY()

public:
    AMyCharacter();

    virtual void Tick(float DeltaTime) override;

    void TakeDamage(float DamageAmount);

private:
    float Health;
    bool bIsAlive;
    FVector CurrentLocation;
};
```

---

## 🔗 Riferimenti

- [Unreal Engine Coding Standard](https://dev.epicgames.com/documentation/en-us/unreal-engine/epic-cplusplus-coding-standard-for-unreal-engine/)
