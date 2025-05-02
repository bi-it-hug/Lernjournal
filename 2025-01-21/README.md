# Vererbung (2025-01-21)

## Zusammenfassung

In diesem Eintrag beschäftige ich mich mit dem Konzept der Vererbung in der objektorientierten Programmierung, ihren verschiedenen Formen und praktischen Anwendungsbeispielen.

## Lernziele

-   Verständnis des Vererbungskonzepts
-   Kenntnis der verschiedenen Arten von Vererbung
-   Praktische Anwendungsbeispiele
-   Best Practices für die Implementierung

## Inhaltsverzeichnis

1. [Einführung](#einführung)
2. [Arten von Vererbung](#arten-von-vererbung)
3. [Praktische Beispiele](#praktische-beispiele)
4. [Vorteile und Nachteile](#vorteile-und-nachteile)
5. [Zusammenfassung](#zusammenfassung)

## Einführung

Vererbung ist ein grundlegendes Konzept der objektorientierten Programmierung, das es ermöglicht, Eigenschaften und Methoden einer Klasse (Basisklasse) an eine andere Klasse (abgeleitete Klasse) weiterzugeben. Dies fördert die Wiederverwendbarkeit von Code und ermöglicht hierarchische Beziehungen zwischen Klassen.

## Arten von Vererbung

### Einfache Vererbung

-   Eine Klasse erbt von genau einer Basisklasse
-   Beispiel: `class Hund extends Tier`

### Mehrfachvererbung

-   Eine Klasse erbt von mehreren Basisklassen
-   In Java nicht direkt möglich, aber durch Interfaces simulierbar
-   Beispiel: `class Hund extends Tier implements Haustier`

### Mehrstufige Vererbung

-   Eine Kette von Vererbungen
-   Beispiel: `class Tier -> class Säugetier -> class Hund`

## Praktische Beispiele

```java
// Basisklasse
class Fahrzeug {
    protected String marke;
    protected int baujahr;

    public Fahrzeug(String marke, int baujahr) {
        this.marke = marke;
        this.baujahr = baujahr;
    }

    public void fahren() {
        System.out.println("Das Fahrzeug fährt.");
    }
}

// Abgeleitete Klasse
class Auto extends Fahrzeug {
    private int anzahlTüren;

    public Auto(String marke, int baujahr, int anzahlTüren) {
        super(marke, baujahr);
        this.anzahlTüren = anzahlTüren;
    }

    @Override
    public void fahren() {
        System.out.println("Das Auto fährt auf der Straße.");
    }
}
```

## Vorteile und Nachteile

### Vorteile

-   Code-Wiederverwendung
-   Bessere Strukturierung
-   Erweiterbarkeit
-   Polymorphismus

### Nachteile

-   Starke Kopplung
-   Komplexität bei tiefen Hierarchien
-   Schwierige Wartung bei Änderungen
-   Potenzielle Verletzung des Single-Responsibility-Prinzips

## Zusammenfassung

Vererbung ist ein mächtiges Werkzeug in der objektorientierten Programmierung, das bei richtiger Anwendung zu sauberem und wartbarem Code führen kann. Es ist wichtig, die Vor- und Nachteile abzuwägen und Vererbung nur dort einzusetzen, wo es sinnvoll ist.

## Weiterführende Links

-   [Java Tutorial: Vererbung](https://docs.oracle.com/javase/tutorial/java/IandI/subclasses.html)
-   [C# Vererbung](https://docs.microsoft.com/de-de/dotnet/csharp/programming-guide/classes-and-structs/inheritance)
-   [SOLID Principles](https://www.digitalocean.com/community/conceptual-articles/s-o-l-i-d-the-first-five-principles-of-object-oriented-design)
