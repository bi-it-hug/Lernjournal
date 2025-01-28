# Lernjournal

## Übersicht:

-   **[2025-01-28](#2025-01-28)**
-   **[2025-01-21](#2025-01-21)**

---

## 2025-01-28

### Override Annotation

```java
// Oberklasse
class Tier {
    String name;

    // Methode in der Oberklasse
    void essen() {
        System.out.println(name + " isst.");
    }
}

// Unterklasse
class Hund extends Tier {
    // Methode in der Unterklasse, die die Methode der Oberklasse überschreibt
    @Override
    void essen() {
        System.out.println(name + " isst Hundefutter.");
    }

    // Zusätzliche Methode in der Unterklasse
    void bellen() {
        System.out.println(name + " bellt: Wuff!");
    }
}

// Hauptprogramm
public class VererbungBeispiel {
    public static void main(String[] args) {
        Hund hund = new Hund();
        hund.name = "Bello";  // Attribut der Oberklasse
        hund.essen();         // Methode der Unterklasse (überschreibt die Methode der Oberklasse)
        hund.bellen();        // Methode der Unterklasse
    }
}
```

### **Ausgabe:**

```
Bello isst Hundefutter.
Bello bellt: Wuff!
```

---

### **Erklärung:**

1. **`@Override`**: In der Unterklasse `Hund` überschreiben wir die Methode `essen()`, die in der Oberklasse `Tier` definiert ist. Die Annotation `@Override` zeigt an, dass eine Methode der Oberklasse bewusst überschrieben wird.
2. Die Methode `essen()` in der Klasse `Hund` ersetzt die Implementierung von `essen()` in der Klasse `Tier`, sodass die Ausgabe `Bello isst Hundefutter.` erscheint, anstelle der ursprünglichen Ausgabe `Bello isst.`.

3. Im Hauptprogramm (`main`) wird das Objekt `hund` erstellt, und die überschreibene Methode `essen()` aus der Unterklasse wird aufgerufen.

Mit der `@Override`-Annotation wird außerdem sichergestellt, dass die Methode korrekt überschrieben wird – falls sie in der Oberklasse nicht existiert oder anders benannt ist, wird ein Fehler ausgelöst. Dies hilft, Fehler zu vermeiden!

---

## 2025-01-21

### Java Vererbung

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

---
