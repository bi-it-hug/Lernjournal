## 2025-03-12

### **Vererbung vs. Interface**

#### **1. Einführung**

In C# gibt es zwei wesentliche Konzepte zur Strukturierung von Code und zur Definition von Beziehungen zwischen Klassen: **Interfaces** und **Vererbung**. Beide Konzepte haben ihre spezifischen Anwendungsfälle, und es ist wichtig zu verstehen, wann man welches verwenden sollte.

#### **2. Interface**

Ein **Interface** ist eine Sammlung von Methodendeklarationen ohne Implementierung. Klassen, die ein Interface implementieren, müssen alle darin definierten Methoden implementieren. Interfaces sind besonders nützlich, wenn verschiedene Klassen unterschiedliche Implementierungen einer Methode bereitstellen sollen, aber eine gemeinsame Schnittstelle benötigen.

-   **Vorteile von Interfaces:**

    -   Ermöglichen eine lose Kopplung zwischen Klassen.
    -   Eine Klasse kann mehrere Interfaces implementieren, was mehr Flexibilität bietet.
    -   Sie fördern das Konzept der **Programmiere gegen Schnittstellen, nicht gegen Implementierungen**.

-   **Beispiel:**

    ```csharp
    public interface IBewegbar
    {
        void Bewege();
    }

    public class Auto : IBewegbar
    {
        public void Bewege()
        {
            Console.WriteLine("Auto fährt");
        }
    }

    public class Fahrrad : IBewegbar
    {
        public void Bewege()
        {
            Console.WriteLine("Fahrrad fährt");
        }
    }
    ```

#### **3. Vererbung**

Vererbung ermöglicht es einer Klasse, von einer anderen Klasse zu erben. Die abgeleitete Klasse erbt die Mitglieder der Basisklasse (Methoden, Eigenschaften, Felder) und kann sie entweder unverändert verwenden oder überschreiben. Vererbung bietet eine starke Kopplung zwischen der Basisklasse und der abgeleiteten Klasse, was bedeutet, dass Änderungen an der Basisklasse Auswirkungen auf die abgeleiteten Klassen haben können.

-   **Vorteile von Vererbung:**

    -   Erleichtert die Wiederverwendung von Code.
    -   Eine klare Hierarchie und Struktur zwischen den Klassen.
    -   Ermöglicht es, gemeinsame Funktionalitäten in der Basisklasse zu definieren.

-   **Beispiel:**

    ```csharp
    public class Fahrzeug
    {
        public void Bewege()
        {
            Console.WriteLine("Fahrzeug bewegt sich");
        }
    }

    public class Auto : Fahrzeug
    {
        public void Hupen()
        {
            Console.WriteLine("Auto hupt");
        }
    }
    ```

#### **4. Unterschiede und Wann man Was verwenden sollte**

-   **Vererbung:**

    -   Wird verwendet, wenn es eine **"ist-ein"**-Beziehung zwischen der Basisklasse und der abgeleiteten Klasse gibt. Zum Beispiel ist ein `Auto` ein `Fahrzeug`.
    -   Vererbung eignet sich, wenn es eine **gemeinsame Funktionalität** in einer Basisklasse gibt, die von abgeleiteten Klassen geteilt werden soll.

-   **Interface:**
    -   Wird verwendet, wenn es eine **"hat-ein"**-Beziehung oder eine **Verhaltensbeschreibung** ohne gemeinsame Implementierung gibt. Zum Beispiel implementieren sowohl `Auto` als auch `Fahrrad` das Interface `IBewegbar`, ohne dass sie dieselbe Implementierung haben müssen.
    -   Ein Interface sollte verwendet werden, wenn mehrere Klassen **unabhängig** voneinander das gleiche Verhalten implementieren sollen.

**5. Fazit**

-   **Vererbung** ist nützlich, wenn eine klare Hierarchie und Vererbung von Funktionalitäten erforderlich ist.
-   **Interfaces** sind flexibler und ermöglichen eine lose Kopplung und das Teilen von Verhalten zwischen nicht verwandten Klassen.

In der Praxis wird oft eine Kombination aus beiden verwendet, um sowohl die Wiederverwendbarkeit von Code als auch die Flexibilität in der Struktur zu maximieren.
