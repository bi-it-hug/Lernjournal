## 2025-01-21

### Vererbung

**Vererbung** in der Programmierung (besonders in objektorientierten Sprachen wie Java) ist ein Konzept, bei dem eine Klasse (Unterklasse) Eigenschaften und Methoden von einer anderen Klasse (Oberklasse) erbt. Dadurch kann Code wiederverwendet und erweitert werden.

Die Oberklasse stellt allgemeine Funktionalitäten bereit, und die Unterklasse kann diese erweitern oder spezialisieren.

---

### **Beispiel: Vererbung in Java**

```java
// Oberklasse
class Tier {
    String name;

    void essen() {
        System.out.println(name + " isst.");
    }
}

// Unterklasse
class Hund extends Tier {
    void bellen() {
        System.out.println(name + " bellt: Wuff!");
    }
}

// Hauptprogramm
public class VererbungBeispiel {
    public static void main(String[] args) {
        Hund hund = new Hund();
        hund.name = "Bello";  // Attribut der Oberklasse
        hund.essen();         // Methode der Oberklasse
        hund.bellen();        // Methode der Unterklasse
    }
}
```

### **Ausgabe:**

```
Bello isst.
Bello bellt: Wuff!
```

---

### **Erklärung:**

1. **`Tier`** ist die Oberklasse, die allgemeine Eigenschaften und Methoden definiert (z. B. `essen()`).
2. **`Hund`** ist die Unterklasse, die die Eigenschaften von `Tier` erbt und neue Methoden hinzufügt (z. B. `bellen()`).
3. Im Hauptprogramm (`main`) wird ein Objekt der Klasse `Hund` erstellt, das auf Methoden und Attribute der Oberklasse sowie der Unterklasse zugreifen kann.

Vererbung ermöglicht eine einfache und saubere Wiederverwendbarkeit des Codes!
