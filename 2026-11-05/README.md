## 2026-11-05

### **DevOps: Modul 324 im Überblick**

Seit dem letzten Lernjournal-Eintrag habe ich mich mit dem Modulbeschrieb von Modul 324 «DevOps-Prozesse mit Tools unterstützen» beschäftigt. Auf den ersten Blick war das Dokument wegen der vielen Fachbegriffe schwer verständlich. Nachdem ich es Schritt für Schritt durchgegangen bin, ist mir die Grundidee klar geworden: Wiederkehrende Schritte wie Bauen, Testen und Ausliefern werden nicht mehr von Hand erledigt, sondern laufen automatisch wie an einem Fliessband ab. Das nennt man **CI/CD** (Continuous Integration / Continuous Deployment).

#### **1. Die Ziele des Moduls**

Das Modul hat fünf Handlungsziele:

1. **Aufgaben erfassen**: Anforderungen werden als Stories oder Issues mit Akzeptanzkriterien beschrieben, und jeder Commit wird mit der passenden Story verknüpft.
2. **Entwicklungsumgebung ausbauen**: Linter, Build, Tests, Git und Paketverwaltung werden direkt in die Entwicklungsumgebung integriert.
3. **Git professionell nutzen**: Feature-Branches, Pull Requests mit Code-Review, Semantic Versioning (`MAJOR.MINOR.PATCH`) und Abhängigkeiten über npm oder Maven.
4. **Continuous Integration**: Bei jedem Push baut eine Pipeline die Anwendung und führt die Tests aus.
5. **Continuous Deployment**: Die Anwendung wird automatisch in eine Abnahmeumgebung ausgeliefert, unterstützt durch Infrastructure as Code, YAML-Konfigurationen, SSH-Keys und eine sichere Verwaltung von Secrets.

#### **2. Wichtige Begriffe**

- **Pipeline**: automatische Abfolge von Schritten (bauen → testen → ausliefern)
- **Artefakt**: das Ergebnis eines Builds, z. B. ein Paket oder ein Docker-Image
- **MVP** (Minimum Viable Product): die kleinste Version eines Produkts, die bereits einen Nutzen bringt
- **Infrastructure as Code**: Server und Umgebungen werden in Textdateien beschrieben statt von Hand eingerichtet
- **Linter**: ein Werkzeug, das Code automatisch auf Fehler und Stilprobleme prüft

#### **3. Erkenntnis**

Ich habe gemerkt, dass ich Teile davon schon aus der Praxis kenne. Bei meiner VS-Code-Extension könnte zum Beispiel eine GitHub Action bei jedem Push die Tests ausführen und automatisch die `.vsix`-Datei bauen – das wäre genau die Continuous Integration aus Ziel 4. DevOps ist für mich dadurch weniger ein abstraktes Schlagwort, sondern eine Arbeitsweise, die manuelle und fehleranfällige Schritte durch zuverlässige Automatisierung ersetzt.
