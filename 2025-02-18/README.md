# 2025-02-18

## **UEK-210**

### **Semantic Versioning (SemVer)**

Entwickler und auch Systemadministratoren stehen vor der Frage, nach welchem Schema sie eine eigenentwickelte Software, Konfigurationsdateien oder Hardware-Releases versionieren. Eine insbesondere im Unix- und Webumfeld verbreitete Variante stellt das sogenannte **"Semantic Versioning"** dar, häufig als **SemVer** abgekürzt.

Das Verfahren definiert eine Versionsnummer in der einfachsten Variante als Kombination dreier Zahlen: einer **Hauptversions-**, einer **Nebenversions-** und einer **Revisionsnummer**, die jeweils einer nichtnegativen Ganzzahl entsprechen.

**Struktur einer Versionsnummer**

Die Zählung beginnt zunächst bei der Versionsnummer **0.0.1**. Anschließend werden die einzelnen Nummern nach vordefinierten Kriterien hochgezählt, wobei eine Veränderung der Hauptversion die Nebenversion und eine Veränderung der Nebenversion die Revision jeweils auf den Wert **0** zurücksetzt.

Wichtig ist, dass eine einzelne Nummer nicht zwingend einstellig sein muss:  
Auf die Versionsnummer **0.9.x** folgt also nicht zwingend **1.0.0**, sondern gegebenenfalls zunächst die Version **0.10.0**.

### Regeln zur Versionsänderung

Auf Grundlage einer Versionsnummer von **MAJOR.MINOR.PATCH** werden die einzelnen Elemente folgendermaßen erhöht:

-   **MAJOR** wird erhöht, wenn API-inkompatible Änderungen veröffentlicht werden.
-   **MINOR** wird erhöht, wenn neue Funktionalitäten, welche kompatibel zur bisherigen API sind, veröffentlicht werden.
-   **PATCH** wird erhöht, wenn die Änderungen ausschließlich API-kompatible Bugfixes umfassen.

Zusätzlich sind Bezeichner für Vorveröffentlichungen und **Build-Metadaten** als Erweiterungen zum **MAJOR.MINOR.PATCH**-Format verfügbar.

### Vorabversionen kennzeichnen

Optional kann eine Versionsnummer um ein **Suffix** ergänzt werden, um Vorabversionen zu kennzeichnen.  
Ein solches Suffix wird durch einen **Trennstrich (`-`)** eingeleitet und besteht danach aus beliebigen alphanumerischen Zeichen.

**Beispiel:**  
`1.0.0-beta1`

---

### **Was ist Cloud?**

-   **Entstehung des Begriffs Cloud:**

    -   Symbol der Wolke als Darstellung von Netzwerken
    -   Ursprünglich aus der Telekommunikation

-   **Definition Cloud (z. B. nach NIST):**

    -   On-Demand-Netzwerkzugriff auf gemeinsam genutzte IT-Ressourcen
    -   Skalierbar, flexibel, ortsunabhängig

-   **5 Merkmale einer Cloud:**

    1. On-Demand Self-Service
    2. Breiter Netzwerkkonnektivität
    3. Ressourcenzusammenlegung (Multi-Tenancy)
    4. Schnelle Skalierbarkeit
    5. Messbare Services

-   **Cloud-Dienstleistungen:**

    -   Speicher (z. B. Google Drive, OneDrive)
    -   Computing (z. B. AWS EC2, Azure VM)
    -   Datenbanken (z. B. AWS RDS, Firebase)
    -   KI/ML-Dienste (z. B. Azure AI, Google Vertex AI)

-   **Cloud-Anbieter:**

    -   Amazon Web Services (AWS)
    -   Microsoft Azure
    -   Google Cloud Platform (GCP)
    -   IBM Cloud
    -   Oracle Cloud

-   **Cloud-Deployment-Modelle:**

    1. Public Cloud
    2. Private Cloud
    3. Hybrid Cloud
    4. Community Cloud

-   **Cloud-Service-Modelle:**

    1. Infrastructure as a Service (IaaS)
    2. Platform as a Service (PaaS)
    3. Software as a Service (SaaS)

-   **Vorteile der Cloud:**

    -   Skalierbarkeit
    -   Kosteneffizienz (Pay-as-you-use)
    -   Flexibilität & Verfügbarkeit
    -   Automatische Updates & Wartung
    -   Globale Zugänglichkeit

-   **Nachteile der Cloud:**

    -   Abhängigkeit vom Anbieter (Vendor Lock-in)
    -   Sicherheits- & Datenschutzrisiken
    -   Internetabhängigkeit
    -   Begrenzte Kontrolle über Infrastruktur

-   **On-Premise-Dienste im Betrieb:**

        -   Lokale Server für interne Anwendungen

    s - Datenbanken mit sensiblen Daten - Spezialisierte Anwendungen (z. B. Produktionssteuerung)

-   **Technologietransfer in der Cloud:**
    -   Bereitstellung über APIs & Webservices
    -   Nutzung von Container-Technologien (Docker, Kubernetes)
    -   Open-Source-Plattformen & Code-Repositories (GitHub, GitLab)
    -   Cloud-basierte Marktplätze für Software & Services


docker run -d -p 8080:80 -v \\wsl.localhost\Ubuntu\home\hug\Website:/usr/share/nginx/html --name Website nginx

docker cp Website:/usr/share/nginx/html/. \\wsl.localhost\Ubuntu\home\hug\Website