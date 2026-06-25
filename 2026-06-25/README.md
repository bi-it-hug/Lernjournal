# React Native

## Technologie-Stack

- **Framework**: React Native mit [Expo](https://docs.expo.dev/)
- **Routing**: [Expo Router](https://docs.expo.dev/router/introduction/) (file-based Routing)
- **Styling**: [NativeWind](https://www.nativewind.dev/) (Tailwind CSS für React Native)
- **UI-Komponenten**: [React Native Reusables](https://reactnativereusables.com/)
- **State Management**: React Context API
- **Persistenz**: AsyncStorage
- **Sensoren**: expo-sensors (Magnetometer)
- **Sprache**: TypeScript

## 1. Was ist React Native?

### Definition

React Native ist ein Framework von Meta, mit dem man mobile Apps für **iOS** und **Android** mit JavaScript/TypeScript und React entwickelt. Statt einer Webseite im Browser rendert React Native native UI-Komponenten (`View`, `Text`, `Pressable` usw.) auf dem Gerät.

### Unterschied zu einer Web-App

| Aspekt | Web (React) | React Native |
|--------|-------------|--------------|
| DOM-Elemente | `<div>`, `<p>`, `<button>` | `<View>`, `<Text>`, `<Pressable>` |
| Styling | CSS-Dateien | StyleSheet oder Utility-Klassen (NativeWind) |
| Plattform | Browser | iOS, Android (optional Web) |
| Gerätezugriff | Eingeschränkt | Kamera, Sensoren, Speicher usw. |

### Warum Expo?

Expo baut auf React Native auf und vereinfacht den Einstieg: Kein Xcode/Android Studio nötig für den Start, vorgefertigte APIs (`expo-camera`, `expo-sensors`) und ein Dev-Server mit Hot Reload. Die App kann direkt auf dem Handy mit **Expo Go** getestet werden.

## 2. Expo Router – Navigation über Dateistruktur

### Definition

Expo Router nutzt **file-based Routing**: Jede Datei im `src/app/`-Ordner wird automatisch zu einer Route. Das funktioniert ähnlich wie Next.js im Web.

### Routing-Hierarchie im Projekt

```
src/app/
├── _layout.tsx          → Root-Layout (Provider, Stack-Navigation)
├── (tabs)/              → Tab-Gruppe (Klammern = unsichtbar in der URL)
│   ├── _layout.tsx      → Tab-Navigation
│   ├── index/           → Home-Tab
│   ├── anomaly/         → Anomalies-Tab
│   └── settings/        → Settings-Tab
├── create-anomaly.tsx   → Modal-Screen
└── edit-anomaly.tsx     → Modal-Screen
```

### Root-Layout mit Stack-Navigation

Das Root-Layout umschliesst die gesamte App mit Providern und definiert den Stack für Modals:

```tsx
export default function RootLayout() {
    const { colorScheme } = useColorScheme()

    return (
        <SensorProvider>
            <ThemeProvider value={NAV_THEME[colorScheme ?? "light"]}>
                <SafeAreaProvider>
                    <AnomalyProvider>
                        <StatusBar style={colorScheme === "dark" ? "light" : "dark"} />
                        <Stack>
                            <Stack.Screen name="(tabs)" options={{ headerShown: false }} />
                            <Stack.Screen name="edit-anomaly" options={MODAL_OPTIONS} />
                            <Stack.Screen name="create-anomaly" options={MODAL_OPTIONS} />
                        </Stack>
                        <PortalHost />
                    </AnomalyProvider>
                </SafeAreaProvider>
            </ThemeProvider>
        </SensorProvider>
    )
}
```

**Wichtige Konzepte:**

- **Provider nesting**: Context-Provider werden von aussen nach innen geschachtelt, damit alle Screens darauf zugreifen können.
- **Stack.Screen**: Registriert Screens und deren Optionen (z. B. `presentation: "modal"`).
- **SafeAreaProvider**: Berücksichtigt Notch und Statusleiste auf modernen Geräten.

### Tab-Navigation

Für die untere Tab-Leiste werden native Tabs von Expo Router verwendet:

```tsx
export default function TabLayout() {
    return (
        <NativeTabs tintColor={PlatformColor("systemRed")} minimizeBehavior="onScrollDown">
            <NativeTabs.Trigger name="index">
                <Label>Home</Label>
                <Icon sf={{ default: "house", selected: "house.fill" }} />
            </NativeTabs.Trigger>
            <NativeTabs.Trigger name="anomaly">
                <Label>Anomalies</Label>
                <Icon sf={{ default: "eye", selected: "eye.fill" }} />
            </NativeTabs.Trigger>
            <NativeTabs.Trigger name="settings">
                <Label>Settings</Label>
                <Icon sf={{ default: "gear", selected: "gear" }} />
            </NativeTabs.Trigger>
        </NativeTabs>
    )
}
```

### Screen-Konfiguration inline

Jeder Screen kann seine Header-Optionen direkt setzen:

```tsx
export default function HomeScreen() {
    const { magnetometerData } = useSensors()

    return (
        <>
            <Stack.Screen options={{ title: "Home", headerTransparent: true }} />
            <View className="flex-1 items-center justify-center gap-8 p-4">
                <Text>{magnetometerData?.x.toFixed(2)}</Text>
            </View>
        </>
    )
}
```

## 3. React Context – Globaler State

### Definition

Context ermöglicht es, Daten ohne Prop-Drilling (durch viele Zwischenkomponenten) an beliebige Kind-Komponenten weiterzugeben. Das Muster besteht aus drei Teilen: **Context erstellen → Provider → Custom Hook**.

### Beispiel: SensorContext

```tsx
const SensorContext = createContext<SensorContextProps | undefined>(undefined)

function SensorProvider({ children }: { children: ReactNode }) {
    const [magnetometerData, setMagnetometerData] = useState<MagnetometerProps | null>(null)

    useEffect(() => {
        Magnetometer.setUpdateInterval(50)
        const subscription = Magnetometer.addListener((data) => setMagnetometerData(data))
        return () => subscription.remove()
    }, [])

    return <SensorContext.Provider value={{ magnetometerData }}>{children}</SensorContext.Provider>
}

function useSensors() {
    const context = useContext(SensorContext)
    if (!context) throw new Error("useSensors must be used within a SensorProvider")
    return context
}
```

**Wichtige Punkte:**

- `useEffect` mit **Cleanup-Funktion** (`subscription.remove()`): Verhindert Memory Leaks, wenn die Komponente unmountet.
- Der Custom Hook `useSensors()` wirft einen Fehler, wenn er ausserhalb des Providers verwendet wird – das hilft beim Debuggen.

### Beispiel: AnomalyContext mit Persistenz

Für Anomalie-Daten wird zusätzlich **AsyncStorage** genutzt, um Daten lokal auf dem Gerät zu speichern:

```tsx
useEffect(() => {
    async function saveAnomalies() {
        try {
            await AsyncStorage.setItem("anomalies", JSON.stringify(anomalies))
        } catch (error) {
            console.error(`Error while saving Anomalies: ${error}`)
        }
    }
    saveAnomalies()
}, [anomalies])
```

AsyncStorage ist das React-Native-Äquivalent zu `localStorage` im Browser – ideal für kleine Datenmengen wie Einstellungen oder Listen.

## 4. Styling mit NativeWind

### Definition

[NativeWind](https://www.nativewind.dev/) bringt Tailwind-CSS-Utility-Klassen nach React Native. Statt `StyleSheet.create()` schreibt man `className="flex-1 items-center p-4"`.

### Verwendung

```tsx
<View className="flex-1 items-center justify-center gap-8 p-4">
    <Text className="text-lg font-bold">Anomalie erkannt</Text>
</View>
```

### UI-Komponenten mit Varianten

React Native Reusables nutzt **class-variance-authority (cva)** für wiederverwendbare Komponenten mit Varianten – ähnlich wie bei shadcn/ui im Web:

```tsx
const buttonVariants = cva(
    'group shrink-0 flex-row items-center justify-center gap-2 rounded-md',
    {
        variants: {
            variant: {
                default: 'bg-primary active:bg-primary/90',
                destructive: 'bg-destructive active:bg-destructive/90',
                outline: 'border-border bg-background active:bg-accent border',
            },
            size: {
                default: 'h-10 px-4 py-2',
                sm: 'h-9 px-3',
                lg: 'h-11 px-8',
            },
        },
        defaultVariants: { variant: 'default', size: 'default' },
    }
)
```

Die Hilfsfunktion `cn()` (aus `clsx` + `tailwind-merge`) kombiniert Klassen und löst Konflikte auf.

## 5. Geräte-APIs

### Magnetometer (expo-sensors)

Das Projekt liest Echtzeit-Magnetometerdaten für die Anomalie-Erkennung:

```tsx
Magnetometer.setUpdateInterval(50)  // Update alle 50ms
const subscription = Magnetometer.addListener((data) => setMagnetometerData(data))
```

Expo kapselt die nativen Sensor-APIs von iOS und Android hinter einer einheitlichen JavaScript-Schnittstelle.

### Weitere Expo-Module im Projekt

| Modul | Zweck |
|-------|-------|
| `expo-camera` | Kamerazugriff |
| `expo-image-picker` | Bilder aus Galerie wählen |
| `expo-status-bar` | Statusleisten-Styling |
| `@react-native-async-storage/async-storage` | Lokale Datenspeicherung |

## 6. Projektstruktur

```
anomaly-detector/
├── app.json                 # Expo-Konfiguration
├── src/
│   ├── app/                 # Screens & Navigation (Expo Router)
│   ├── components/          # Wiederverwendbare UI-Komponenten
│   │   └── ui/              # Basis-Komponenten (Button, Card, Input, …)
│   ├── context/             # React Context Provider
│   ├── data/                # Standarddaten & Defaults
│   ├── lib/                 # Hilfsfunktionen (Theme, utils)
│   └── types/               # TypeScript-Typdefinitionen
├── tailwind.config.js       # Tailwind-Konfiguration
└── global.css               # Globale Styles für NativeWind
```

### Best Practices

- **Separation of Concerns**: Screens in `app/`, Logik in `context/`, UI in `components/`
- **TypeScript-Typen** in eigenem `types/`-Ordner für Wiederverwendbarkeit
- **Path Aliases** (`@/components/...`) für saubere Imports
- **Provider im Root-Layout** statt in einzelnen Screens

## 7. Entwicklungsworkflow

```bash
npm run dev        # Dev-Server starten (Port 8082)
# Dann im Terminal:
#   i → iOS Simulator (nur Mac)
#   a → Android Emulator
#   w → Web-Browser
# Oder QR-Code mit Expo Go scannen
```

Der Dev-Server unterstützt **Hot Reload**: Änderungen am Code erscheinen sofort auf dem Gerät, ohne die App neu zu starten.

## 8. Lernerkenntnisse

### Technische Konzepte

1. **React Native Grundlagen**: Native UI-Komponenten statt HTML, plattformübergreifende Entwicklung
2. **Expo-Ökosystem**: Vereinfachter Einstieg, vorgefertigte native APIs, Expo Go zum Testen
3. **File-based Routing**: Navigation über Ordnerstruktur mit Expo Router
4. **Context API**: Globaler State ohne externe Bibliothek (Redux, Zustand)
5. **NativeWind**: Tailwind-ähnliches Styling in React Native
6. **Geräteintegration**: Sensoren und lokaler Speicher über Expo-Module

### Architektur-Patterns

- **Provider Pattern**: Globale Daten und Services über React Context
- **Compound Components**: UI-Bibliothek mit Varianten (cva)
- **Layout Routes**: Verschachtelte `_layout.tsx`-Dateien für Navigation

### Unterschiede zu Web-Entwicklung

- Kein DOM – stattdessen native Views
- `Platform.select()` für plattformspezifisches Verhalten
- `SafeAreaProvider` für Geräte mit Notch
- AsyncStorage statt localStorage
- Sensoren und Kamera direkt über Expo-Module

## Weiterführende Links

- [React Native Dokumentation](https://reactnative.dev/docs/getting-started)
- [Expo Dokumentation](https://docs.expo.dev/)
- [Expo Router](https://docs.expo.dev/router/introduction/)
- [NativeWind](https://www.nativewind.dev/)
- [React Native Reusables](https://reactnativereusables.com/)
