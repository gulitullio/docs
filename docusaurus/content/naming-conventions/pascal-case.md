---
title: PascalCase
sidebar_position: 1
---

Ogni parola inizia con la lettera maiuscola, inclusa la prima.

### Linguaggi comuni

C#, JavaScript, Java, TypeScript, Swift

### Utilizzo

Classi, Interfacce, Enum, Tipi personalizzati

### Note

In molti linguaggi (es. Java, TypeScript) è convenzione usare PascalCase per nomi di classi e interfacce, mentre si usa CamelCase per variabili e metodi.  
Alcuni sviluppatori preferiscono usare camelCase per le proprietà anche all'interno di interfacce/classi. Lo stile può variare a seconda del team o delle linee guida del progetto.

### Esempio

```ts
interface UserProfile {
  UserId: number;
  UserName: string;
  IsActive: boolean;
}

class UserService {
  private Users: UserProfile[] = [];

  constructor() {}

  AddUser(userProfile: UserProfile): void {
    this.Users.push(userProfile);
  }

  GetUserById(userId: number): UserProfile | null {
    for (let user of this.Users) {
      if (user.UserId === userId) {
        return user;
      }
    }
    return null;
  }
}
```
