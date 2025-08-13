---
title: Ereditarietà
---

In C++, l’ereditarietà può essere pubblica, protetta o privata.  
Questo influisce su come i membri della classe base sono accessibili nella classe derivata e all’esterno.

---

### Ereditarietà pubblica (public)

- I membri **pubblici** della classe base rimangono **pubblici** nella classe derivata
- I membri **protetti** della classe base rimangono **protetti** nella classe derivata
- I membri **privati** della classe base **non sono accessibili** direttamente nella classe derivata (ma ci sono modi per accedervi tramite funzioni pubbliche o protette)

---

### Ereditarietà protetta (protected)

- I membri **pubblici e protetti** della classe base diventano **protetti** nella classe derivata
- I membri **privati** della classe base rimangono **non accessibili** direttamente

---

### Ereditarietà privata (private)

- I membri **pubblici e protetti** della classe base diventano **privati** nella classe derivata
- I membri **privati** della classe base rimangono **non accessibili** direttamente
