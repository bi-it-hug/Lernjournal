# Polymorphismus (2025-01-28)

## Zusammenfassung

In diesem Eintrag beschäftige ich mich mit dem Konzept des Polymorphismus in der objektorientierten Programmierung, seinen verschiedenen Formen und praktischen Anwendungsbeispielen.

## Lernziele

-   Verständnis des Polymorphismus-Konzepts
-   Kenntnis der verschiedenen Arten von Polymorphismus
-   Praktische Anwendungsbeispiele
-   Best Practices für die Implementierung

## Inhaltsverzeichnis

1. [Einführung](#einführung)
2. [Arten von Polymorphismus](#arten-von-polymorphismus)
3. [Praktische Beispiele](#praktische-beispiele)
4. [Vorteile und Anwendungsfälle](#vorteile-und-anwendungsfälle)
5. [Zusammenfassung](#zusammenfassung)

## Einführung

Polymorphismus ist ein grundlegendes Konzept der objektorientierten Programmierung, das es ermöglicht, dass Objekte unterschiedlicher Klassen auf die gleiche Weise behandelt werden können. Das Wort "Polymorphismus" kommt aus dem Griechischen und bedeutet "viele Formen".

## Arten von Polymorphismus

### Ad-hoc Polymorphismus

-   Überladung von Methoden
-   Überladung von Operatoren
-   Beispiel: `+` kann Zahlen addieren oder Strings verketten

### Parametrischer Polymorphismus

-   Generische Typen und Methoden
-   Beispiel: `List<T>` in C# oder Java

### Subtyp-Polymorphismus

-   Vererbung und Interfaces
-   Beispiel: Eine Methode kann mit verschiedenen Unterklassen arbeiten

## Praktische Beispiele

```java
// Beispiel für Subtyp-Polymorphismus
interface Form {
    double berechneFläche();
}

class Kreis implements Form {
    private double radius;

    public Kreis(double radius) {
        this.radius = radius;
    }

    @Override
    public double berechneFläche() {
        return Math.PI * radius * radius;
    }
}

class Rechteck implements Form {
    private double breite, höhe;

    public Rechteck(double breite, double höhe) {
        this.breite = breite;
        this.höhe = höhe;
    }

    @Override
    public double berechneFläche() {
        return breite * höhe;
    }
}
```

## Vorteile und Anwendungsfälle

### Vorteile

-   Wiederverwendbarkeit von Code
-   Flexibilität und Erweiterbarkeit
-   Bessere Wartbarkeit
-   Reduzierung von Code-Duplikation

### Anwendungsfälle

-   GUI-Komponenten
-   Datenbankzugriff
-   Plugin-Systeme
-   Algorithmen mit verschiedenen Implementierungen

## Zusammenfassung

Polymorphismus ist ein mächtiges Konzept, das die Flexibilität und Wartbarkeit von Code verbessert. Durch die verschiedenen Arten von Polymorphismus können Entwickler eleganten und wiederverwendbaren Code schreiben.

## Weiterführende Links

-   [Java Tutorial: Polymorphismus](https://docs.oracle.com/javase/tutorial/java/IandI/polymorphism.html)
-   [C# Polymorphismus](https://docs.microsoft.com/de-de/dotnet/csharp/programming-guide/classes-and-structs/polymorphism)
-   [Design Patterns](https://refactoring.guru/design-patterns)
