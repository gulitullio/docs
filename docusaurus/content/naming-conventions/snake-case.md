---
title: snake_case
sidebar_position: 3
---

Tutte le lettere sono minuscole, le parole sono separate da un underscore (`_`).

### Linguaggi comuni

Python, Ruby, C, PHP

### Utilizzo

Variabili, Funzioni/metodi, Nomi di file

### Note

In Python è convenzione usare `snake_case` per nomi di funzioni, metodi e variabili, mentre le classi usano `PascalCase`. Anche in altri linguaggi (es. C, Ruby) questo stile è comune per nomi identificatori.

### Esempio

```py
from typing import Optional

class user_profile:
    def __init__(self, user_id: int, user_name: str, is_active: bool):
        self.user_id = user_id
        self.user_name = user_name
        self.is_active = is_active

class user_service:
    def __init__(self):
        self.users: list[user_profile] = []

    def add_user(self, user_profile: user_profile) -> None:
        self.users.append(user_profile)

    def get_user_by_id(self, user_id: int) -> Optional[user_profile]:
        for user in self.users:
            if user.user_id == user_id:
                return user
        return None
```
