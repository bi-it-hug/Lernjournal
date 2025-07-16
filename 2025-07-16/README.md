# Backend

## Technologie-Stack

- **Backend**: Node.js mit Express.js
- **Datenbank**: MongoDB mit Mongoose ODM
- **Authentifizierung**: JWT (JSON Web Tokens)
- **Architektur**: RESTful API mit modularem Aufbau

## 1. Was sind Routes?

### Definition

Routes sind definierte Endpunkte in einer Web-Anwendung, die bestimmen, wie HTTP-Anfragen (GET, POST, PUT, DELETE) verarbeitet werden. Sie bilden die Schnittstelle zwischen Client und Server.

### Implementierung in diesem Projekt

#### Route-Struktur

```javascript
// app.js - Hauptanwendung
app.use("/tasks", tasks); // Alle Task-bezogenen Endpunkte
app.use("/login", login); // Authentifizierung
app.use("/logout", logout); // Abmeldung
app.use("/verify", verify); // Token-Validierung
```

#### Beispiel: Tasks-Route (`routes/tasks.js`)

```javascript
// GET /tasks - Alle Aufgaben abrufen
router.get("/", verifyToken, async (request, response) => {
    const tasks = await Task.find();
    response.json(tasks);
});

// POST /tasks - Neue Aufgabe erstellen
router.post("/", verifyToken, validateTask, async (request, response) => {
    const task = new Task(request.body);
    const savedTask = await task.save();
    response.status(201).json(savedTask);
});

// GET /tasks/:id - Einzelne Aufgabe abrufen
router.get("/:id", verifyToken, async (request, response) => {
    const task = await Task.findById(request.params.id);
    response.json(task);
});
```

### Vorteile der Route-Struktur

- **Modularität**: Jede Funktionalität hat ihre eigene Route-Datei
- **Wartbarkeit**: Einfache Erweiterung und Änderung von Endpunkten
- **Übersichtlichkeit**: Klare Trennung der Verantwortlichkeiten
- **Wiederverwendbarkeit**: Routes können in anderen Projekten wiederverwendet werden

## 2. Was ist Middleware?

### Definition

Middleware sind Funktionen, die zwischen der HTTP-Anfrage und der endgültigen Antwort ausgeführt werden. Sie können die Anfrage verarbeiten, validieren, modifizieren oder die Ausführung beenden.

### Middleware-Pipeline

```
Client Request → Middleware 1 → Middleware 2 → Route Handler → Response
```

### Implementierte Middleware in diesem Projekt

#### 1. verifyToken Middleware (`middleware/verifyToken.js`)

```javascript
export default function verifyToken(request, response, next) {
    try {
        const authHeader = request.headers.authorization;
        if (!authHeader) return response.status(401).json({ error: "No Token provided" });

        const token = authHeader.startsWith("Bearer ") ? authHeader.substring(7) : authHeader;
        const decoded = jwt.verify(token, config.session.secret);
        request.user = decoded; // User-Informationen zur Request hinzufügen
        next(); // Zur nächsten Middleware/Route weiterleiten
    } catch (error) {
        response.status(401).json({ error: "Invalid Token" });
    }
}
```

**Funktion**: Überprüft JWT-Tokens und fügt Benutzerinformationen zur Request hinzu.

#### 2. validateLogin Middleware (`middleware/validateLogin.js`)

```javascript
export default function validateLogin(request, response, next) {
    const authHeader = request.headers.authorization;
    if (!authHeader || !authHeader.startsWith("Basic ")) return response.status(400).json({ error: "Authorization header required" });

    try {
        const credentials = Buffer.from(authHeader.split(" ")[1], "base64").toString();
        const [email, password] = credentials.split(":");

        if (!email || !password) return response.status(400).json({ error: "Email and password required" });

        request.credentials = { email: email.trim(), password: password.trim() };
        next();
    } catch (error) {
        return response.status(400).json({ error: "Invalid authorization format" });
    }
}
```

**Funktion**: Validiert Basic Authentication Header und extrahiert Credentials.

#### 3. validateTask Middleware (`middleware/validateTask.js`)

```javascript
export default function validateTask(request, response, next) {
    const { title } = request.body;
    if (!title || title.trim().length === 0) return response.status(422).json({ error: "Title is required" });
    next();
}
```

**Funktion**: Überprüft, ob Task-Daten gültig sind.

### Middleware-Verwendung in Routes

```javascript
// Mehrere Middleware in einer Route
router.post("/", verifyToken, validateTask, async (request, response) => {
    // Route-Handler wird nur ausgeführt, wenn alle Middleware erfolgreich sind
});
```

## 3. Authorization-System

### Authentifizierung vs. Autorisierung

- **Authentifizierung**: "Wer bist du?" (Login-Prozess)
- **Autorisierung**: "Was darfst du?" (Berechtigungen)

### Implementiertes Authorization-System

#### 1. JWT-basierte Authentifizierung

**Token-Generierung beim Login** (`routes/login.js`):

```javascript
router.post("/", validateLogin, async (request, response) => {
    const { email, password } = request.credentials;
    const user = await User.findOne({ email });

    if (!user || password !== user.password) return response.status(401).json({ error: "Invalid credentials" });

    // JWT-Token erstellen
    const token = jwt.sign(user.toObject(), config.session.secret, { expiresIn: "24h" });
    response.json({ token });
});
```

**Token-Validierung** (`middleware/verifyToken.js`):

```javascript
const decoded = jwt.verify(token, config.session.secret);
request.user = decoded; // Benutzerinformationen zur Request hinzufügen
```

#### 2. Authorization-Flow

```
1. Client sendet Login-Request mit Basic Auth
2. Server validiert Credentials
3. Server generiert JWT-Token
4. Client speichert Token
5. Client sendet Token bei jeder API-Anfrage
6. Server validiert Token bei geschützten Endpunkten
```

#### 3. Geschützte Endpunkte

Alle Task-Endpunkte sind durch `verifyToken` Middleware geschützt:

```javascript
router.get("/", verifyToken, async (request, response) => {
    // Nur authentifizierte Benutzer können Tasks abrufen
});
```

### Sicherheitsaspekte

#### Vorteile von JWT

- **Stateless**: Server speichert keine Session-Daten
- **Skalierbar**: Funktioniert über mehrere Server hinweg
- **Selbstbeschreibend**: Token enthält alle notwendigen Informationen

#### Implementierte Sicherheitsmassnahmen

- **Token-Expiration**: 24 Stunden Gültigkeit
- **Secret Key**: Sichere Token-Signierung
- **Input-Validierung**: Überprüfung aller Eingabedaten
- **Error Handling**: Sichere Fehlerbehandlung ohne Informationslecks

## 4. Datenbank-Architektur

### Mongoose-Schemas

#### User-Schema (`db/schemas/user.js`)

```javascript
export const userSchema = new mongoose.Schema({
    email: String,
    password: String,
});
```

#### Task-Schema (`db/schemas/task.js`)

```javascript
export const taskSchema = new mongoose.Schema(
    {
        title: String,
        description: String,
        completed: Boolean,
        dueDate: Date,
    },
    { versionKey: false }
);
```

### Model-Verwendung

```javascript
// User-Model
import { User } from "../db/models/user.js";
const user = await User.findOne({ email });

// Task-Model
import { Task } from "../db/models/task.js";
const task = new Task(request.body);
```

## 5. Projektstruktur und Best Practices

### Ordnerstruktur

```
├── app.js              # Hauptanwendung
├── config.js           # Konfiguration
├── routes/             # Route-Definitionen
├── middleware/         # Middleware-Funktionen
├── db/                 # Datenbank-Layer
│   ├── models/        # Mongoose-Modelle
│   └── schemas/       # Datenbankschemas
└── public/            # Statische Dateien
```

### Code-Organisation

- **Separation of Concerns**: Jede Datei hat eine spezifische Verantwortlichkeit
- **Modularität**: Wiederverwendbare Komponenten
- **Middleware-Chaining**: Flexible Kombination von Middleware
- **Error Handling**: Konsistente Fehlerbehandlung

## 6. Lernerkenntnisse

### Technische Konzepte

1. **RESTful API-Design**: Standardisierte HTTP-Endpunkte
2. **Middleware-Architektur**: Modulare Request-Verarbeitung
3. **JWT-Authentifizierung**: Sichere, stateless Authentifizierung
4. **MongoDB mit Mongoose**: Objekt-Dokument-Mapping
5. **Express.js Routing**: Flexible URL-Behandlung

### Architektur-Patterns

- **MVC-Pattern**: Model-View-Controller (ohne View in API)
- **Middleware-Pattern**: Request-Pipeline-Verarbeitung
- **Repository-Pattern**: Datenbankzugriff über Modelle

### Sicherheitsaspekte

- **Input-Validierung**: Schutz vor ungültigen Daten
- **Token-basierte Auth**: Sichere Benutzerauthentifizierung
- **Error Handling**: Sichere Fehlerbehandlung
- **CORS-Konfiguration**: Cross-Origin-Request-Handling
