# 2025-01-28

## **Dynamischer Polymorphismus**

### **1. Was ist dynamischer Polymorphismus?**

Polymorphismus bedeutet, dass eine Methode in einer Oberklasse definiert und in Unterklassen unterschiedlich umgesetzt werden kann. Dabei unterscheidet man:

-   **Statischen Polymorphismus (Methodenüberladung)** → entscheidet sich zur **Kompilierungszeit**.
-   **Dynamischen Polymorphismus (Methodenüberschreibung)** → entscheidet sich zur **Laufzeit**.

Dynamischer Polymorphismus tritt auf, wenn eine Methode in einer Oberklasse vorhanden ist, aber von Unterklassen überschrieben wird. Der entscheidende Punkt ist, dass das **Objekt selbst bestimmt, welche Methode aufgerufen wird, nicht der Referenztyp**.

---

### **2. Anwendung im Code**

Schauen wir uns den Code genauer an:

#### **Basisklasse `Animal` (Elternklasse)**

```java
public class Animal {

    String name;
    int age;

    public Animal(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public void speak() {
        System.out.println();
    }
}
```

-   `Animal` besitzt eine Methode `speak()`, die nichts ausgibt.
-   `speak()` ist **nicht abstrakt**, d. h. sie hat eine leere Implementierung.

#### **Unterklassen `Cat` und `Dog` (Kindklassen)**

Diese Klassen erben von `Animal` und überschreiben die Methode `speak()`.

```java
public class Cat extends Animal {

    String claws;

    public Cat(String name, int age, String claws) {
        super(name, age);
        this.claws = claws;
    }

    @Override
    public void speak() {
        System.out.println("Meow");
    }
}
```

-   `Cat` überschreibt `speak()`, sodass bei einer Katze `"Meow"` ausgegeben wird.

```java
public class Dog extends Animal {

    String paws;

    public Dog(String name, int age, String paws) {
        super(name, age);
        this.paws = paws;
    }

    @Override
    public void speak() {
        System.out.println("Woof");
    }
}
```

-   `Dog` überschreibt `speak()`, sodass bei einem Hund `"Woof"` ausgegeben wird.

---

### **3. Dynamischer Polymorphismus in Aktion**

Im Hauptprogramm werden `Cat` und `Dog` Objekte erstellt und in einer `List<Animal>` gespeichert:

```java
public class App {

    public static void main(String[] args) {

        List<Animal> allAnimals = List.of(
                new Cat("Whiskers", 4, "small"),
                new Dog("Bruno", 10, "big")
        );

        for (Animal animal : allAnimals) {
            animal.speak();
        }
    }
}
```

-   Die `List<Animal>` speichert `Cat`- und `Dog`-Objekte.
-   Die **Referenzvariablen** haben den Typ `Animal`, aber die **tatsächlichen Objekte** sind `Cat` oder `Dog`.
-   Beim Aufruf von `animal.speak()` wird **zur Laufzeit entschieden**, welche Methode ausgeführt wird.

### **4. Ablauf zur Laufzeit**

**Schritt für Schritt:**

1. `animal` zeigt zuerst auf das `Cat`-Objekt.
    - `animal.speak();` ruft die `speak()`-Methode von `Cat` auf → `"Meow"` wird ausgegeben.
2. Danach zeigt `animal` auf das `Dog`-Objekt.
    - `animal.speak();` ruft die `speak()`-Methode von `Dog` auf → `"Woof"` wird ausgegeben.

---

### **5. Wichtige Konzepte im Code**

#### **Methodenüberschreibung (`@Override`)**

-   Die Unterklassen definieren die Methode `speak()` neu.
-   `@Override` sorgt dafür, dass Java prüft, ob tatsächlich eine Methode aus der Oberklasse überschrieben wird.

#### **Polymorphe Variablen (`Animal animal = new Cat(...)`)**

-   Eine Variable vom Typ `Animal` kann sowohl eine `Cat` als auch einen `Dog` speichern.
-   Der **tatsächliche Objekttyp** entscheidet, welche Methode aufgerufen wird.

#### **Laufzeitbindung (Late Binding)**

-   Zur **Kompilierungszeit** weiss der Compiler nur, dass `animal.speak()` existiert.
-   Erst zur **Laufzeit** wird entschieden, welche konkrete Methode (`Cat.speak()` oder `Dog.speak()`) aufgerufen wird.

---

### **6. Vorteile von dynamischem Polymorphismus**

✅ **Erweiterbarkeit**: Neue Tierarten (`Bird`, `Fish` etc.) können einfach hinzugefügt werden, ohne den Code in `App` ändern zu müssen.

✅ **Flexibilität**: Die `List<Animal>` kann verschiedene `Animal`-Unterklassen enthalten, ohne dass spezielle Fallunterscheidungen nötig sind.

✅ **Code-Wiederverwendbarkeit**: Die Methode `speak()` wird in der Basisklasse definiert und kann in Unterklassen einfach angepasst werden.

---

### **7. Fazit**

Dynamischer Polymorphismus ermöglicht es, Methodenaufrufe zur Laufzeit je nach Objekttyp unterschiedlich auszuführen. In deinem Code sorgt er dafür, dass eine Katze "Meow" und ein Hund "Woof" sagt, obwohl beide als `Animal` gespeichert sind. Dies macht den Code flexibler, erweiterbar und leicht verständlich.

> [!NOTE]
> [Code](./Polymorphism/src/)
