# Vererbung vs. Interface (2025-03-12)

## Zusammenfassung

In diesem Eintrag beschäftige ich mich mit den Unterschieden und Anwendungsfällen von Vererbung und Interfaces in der objektorientierten Programmierung.

## Lernziele

-   Verständnis der Konzepte Vererbung und Interface
-   Vergleich der beiden Ansätze
-   Best Practices für die Verwendung
-   Praktische Anwendungsbeispiele

## Inhaltsverzeichnis

1. [Einführung](#einführung)
2. [Vererbung](#vererbung)
3. [Interfaces](#interfaces)
4. [Vergleich](#vergleich)
5. [Zusammenfassung](#zusammenfassung)

## Einführung

Vererbung und Interfaces sind zwei grundlegende Konzepte der objektorientierten Programmierung, die unterschiedliche Ansätze zur Wiederverwendung von Code und zur Strukturierung von Klassen bieten.

## Vererbung

-   **Definition**: Eine Klasse erbt Eigenschaften und Methoden von einer anderen Klasse
-   **Vorteile**:
    -   Code-Wiederverwendung
    -   Polymorphismus
    -   Hierarchische Strukturierung
-   **Nachteile**:
    -   Starke Kopplung
    -   Inflexibilität bei Änderungen

## Interfaces

-   **Definition**: Ein Vertrag, der definiert, welche Methoden eine Klasse implementieren muss
-   **Vorteile**:
    -   Lose Kopplung
    -   Mehrfachimplementierung möglich
    -   Flexibilität
-   **Nachteile**:
    -   Keine Code-Wiederverwendung
    -   Mehr Aufwand bei der Implementierung

## Vergleich

| Aspekt           | Vererbung | Interface              |
| ---------------- | --------- | ---------------------- |
| Kopplung         | Stark     | Lose                   |
| Wiederverwendung | Code      | Nur Methodensignaturen |
| Flexibilität     | Gering    | Hoch                   |
| Implementierung  | Einfach   | Komplexer              |

## Zusammenfassung

Vererbung eignet sich besonders für "ist-ein" Beziehungen und wenn Code-Wiederverwendung im Vordergrund steht. Interfaces sind besser für "kann" Beziehungen und wenn Flexibilität wichtig ist.

## Weiterführende Links

-   [Java Tutorial: Vererbung](https://docs.oracle.com/javase/tutorial/java/IandI/subclasses.html)
-   [Java Tutorial: Interfaces](https://docs.oracle.com/javase/tutorial/java/IandI/createinterface.html)
-   [Design Patterns](https://refactoring.guru/design-patterns)
