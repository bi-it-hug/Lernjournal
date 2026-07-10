## 2026-07-10

### **Custom Theme in MudBlazor**

In MudBlazor steuert ein zentrales `MudTheme`-Objekt Farben, Typografie und Layout. Statt der Standardpalette habe ich eigene Light- und Dark-Paletten aufgebaut und die Farben an die Tailwind-Skalen angelehnt (z. B. `Blue._500`, `Neutral._900`). Das Theme wird über `MudThemeProvider` eingebunden; den Dark-Mode-Zustand speichere ich im `localStorage` und stelle ihn beim Start wieder her – so bleibt die Einstellung über Seitenwechsel hinweg erhalten.
