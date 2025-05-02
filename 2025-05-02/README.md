# Docker Basics (2025-05-02)

## Zusammenfassung

In diesem Eintrag beschäftige ich mich mit den Grundlagen von Docker, einem wichtigen Tool für Containerisierung und Anwendungsentwicklung.

## Lernziele

-   Verständnis der grundlegenden Docker-Konzepte
-   Erstellung und Verwaltung von Docker-Containern
-   Arbeit mit Docker-Images
-   Docker-Compose für Multi-Container-Anwendungen

## Inhaltsverzeichnis

1. [Einführung](#einführung)
2. [Docker-Grundlagen](#docker-grundlagen)
3. [Praktische Beispiele](#praktische-beispiele)
4. [Zusammenfassung](#zusammenfassung)

## Einführung

Docker ist eine Plattform zur Entwicklung, Auslieferung und Ausführung von Anwendungen in Containern. Container ermöglichen es, Anwendungen und ihre Abhängigkeiten in einer isolierten Umgebung zu verpacken.

## Docker-Grundlagen

-   **Container**: Isolierte Umgebungen für Anwendungen
-   **Images**: Vorlagen für Container
-   **Dockerfile**: Anweisungen zum Erstellen von Images
-   **Docker Compose**: Tool für Multi-Container-Anwendungen

## Praktische Beispiele

```dockerfile
# Beispiel Dockerfile
FROM python:3.9
WORKDIR /app
COPY . .
RUN pip install -r requirements.txt
CMD ["python", "app.py"]
```

## Zusammenfassung

Docker bietet eine effiziente Möglichkeit, Anwendungen zu entwickeln und zu deployen. Durch Containerisierung werden Abhängigkeiten isoliert und die Reproduzierbarkeit verbessert.

## Weiterführende Links

-   [Docker Dokumentation](https://docs.docker.com/)
-   [Docker Hub](https://hub.docker.com/)
-   [Docker Compose Dokumentation](https://docs.docker.com/compose/)
