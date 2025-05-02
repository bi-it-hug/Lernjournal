## 2025-05-02

### **Docker Basics**

#### **Was ist Docker?**

Docker ist eine Plattform, die es ermöglicht, Anwendungen in sogenannten **Containern** zu verpacken und auszuführen. Ein Container enthält alles, was eine Anwendung braucht: Code, Laufzeit, Systemwerkzeuge, Bibliotheken usw. Damit funktioniert die Anwendung unabhängig von der Umgebung – lokal, auf dem Server oder in der Cloud.

---

### **Grundlegende Docker-Komponenten:**

| Komponente     | Beschreibung                                                              |
| -------------- | ------------------------------------------------------------------------- |
| **Image**      | Eine Vorlage (Template), aus der Container erstellt werden.               |
| **Container**  | Eine laufende Instanz eines Images.                                       |
| **Dockerfile** | Eine Datei, die beschreibt, wie ein Image gebaut werden soll.             |
| **Docker Hub** | Eine Online-Plattform zum Teilen von Docker-Images (wie GitHub für Code). |

---

### **Wichtige Befehle, die ich gelernt habe:**

```bash
docker --version               # Version von Docker anzeigen
docker pull nginx              # Image von Docker Hub herunterladen
docker images                  # Alle lokal verfügbaren Images anzeigen
docker run hello-world         # Container aus Image starten (einmalig)
docker ps                      # Aktive Container anzeigen
docker ps -a                   # Alle Container anzeigen (auch gestoppte)
docker stop <container-id>     # Container stoppen
docker rm <container-id>       # Container löschen
docker rmi <image-id>          # Image löschen
```

---

### **Beispiel: Eigenes Image mit Dockerfile bauen**

```dockerfile
# Dockerfile
FROM node:18
WORKDIR /app
COPY . .
RUN npm install
CMD ["node", "index.js"]
```

```bash
docker build -t mein-node-app .
docker run -p 3000:3000 mein-node-app
```

---

### **Was ich verstanden habe:**

-   Container sind leichtgewichtig und isoliert
-   Ein Container ist **kein** virtueller Rechner, sondern nutzt den Kernel des Hosts
-   Mit Docker kann man „es läuft auf meinem Rechner“ wirklich eliminieren

---
