## 2026-08-07

### **AppState und ResolvedTheme**

Seit dem letzten Lernjournal-Eintrag habe ich in der DemoApp vor allem daran gearbeitet, den Anwendungszustand klarer zu strukturieren und das Layout zu entlasten. Besonders wichtig war die Erkenntnis, dass der Theme-Zustand aus zwei Ebenen besteht: dem gespeicherten `ThemeMode` (`Light`, `Dark` oder `System`) und dem zur Laufzeit aufgelösten `ResolvedTheme`, das immer nur `Light` oder `Dark` ist. Bei `System` kommt der konkrete Wert vom Betriebssystem bzw. Browser; erst dieser aufgelöste Wert steuert `MudThemeProvider`. Beides an einer Stelle im `AppStateService` zu halten verhindert doppelte Variablen im Layout und macht den State nachvollziehbarer.

Ein weiterer Schwerpunkt war das Auslagern von UI-Logik in eigene Komponenten. Die Breadcrumbs liegen jetzt in einer eigenen Komponente und reagieren selbst auf `NavigationManager.LocationChanged`. Dadurch bleibt im `MainLayout` nur noch die Layout-Logik (z. B. Sidebar und AppBar auf der Not-Found-Seite). Ähnlich habe ich mit `SettingsRow` eine wiederverwendbare Zeile für Einstellungen gebaut: Label, optionale Beschreibung und beliebiger Inhalt über `ChildContent` (`RenderFragment`). So bleibt der Settings-Dialog übersichtlich und neue Schalter oder Selects lassen sich einheitlich ergänzen.

Ich habe ausserdem besser verstanden, wie wichtig saubere Event-Abonnements sind. Ob Benachrichtigungen über `NotificationService.Changed` oder Breadcrumbs über `LocationChanged` – ohne `Dispose` und Abmelden der Handler entstehen schnell Memory Leaks oder veraltete UI-Updates. Naming wie `NotificationService` statt einer zu kurzen Injection-Variable macht den Code zudem lesbarer.

Zusammengefasst habe ich gelernt, dass saubere Blazor-UI nicht nur aus Styling besteht. Entscheidend ist, persistenten und laufzeitabhängigen State zu trennen, wiederkehrende UI-Muster als Komponenten zu kapseln und Events zentral sowie disziplinert zu verwalten.
