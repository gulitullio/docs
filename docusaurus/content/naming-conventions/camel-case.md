---
title: camelCase
sidebar_position: 2
---

La prima parola in minuscolo, le successive con l'iniziale maiuscola.

### Linguaggi comuni

JavaScript, Java, TypeScript, Swift

### Utilizzo

Variabili, Funzioni/metodi

### Note

In TypeScript, Java e JavaScript è normale combinare PascalCase per classi/interfacce e CamelCase per tutto il resto.

### Esempio

```ts
interface UserProfile {
  userId: number;
  userName: string;
  isActive: boolean;
}

class UserService {
  private users: UserProfile[] = [];

  constructor() {}

  addUser(userProfile: UserProfile): void {
    this.users.push(userProfile);
  }

  getUserById(userId: number): UserProfile | null {
    for (let user of this.users) {
      if (user.userId === userId) {
        return user;
      }
    }
    return null;
  }
}
```
