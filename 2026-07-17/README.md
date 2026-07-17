## 2026-07-17

### **Erkenntnisse seit letztem Freitag**

Seit dem letzten Lernjournal-Eintrag habe ich mein Verständnis für den Aufbau einer konsistenten Oberfläche in MudBlazor vertieft. Besonders wichtig war die Erkenntnis, dass ein Theme nicht nur aus einzelnen Farben besteht, sondern als zentrale Grundlage für die gesamte Anwendung dient. Wenn Farben, Typografie und Layout-Regeln an einer Stelle definiert sind, bleibt die UI einheitlicher und spätere Anpassungen werden einfacher.

Ein weiterer Schwerpunkt war der Dark Mode. Dabei wurde mir klar, dass es nicht reicht, nur zwischen zwei Farbpaletten umzuschalten. Die gewählte Einstellung muss auch gespeichert und beim nächsten Start wiederhergestellt werden, damit sich die Anwendung für den Benutzer zuverlässig anfühlt. Durch die Speicherung im `localStorage` bleibt der Modus über Seitenwechsel und neue Sitzungen hinweg erhalten.

Ich habe ausserdem besser verstanden, wie wichtig die richtige Platzierung von Providern ist. Komponenten wie `MudThemeProvider` müssen möglichst weit oben in der Anwendung eingebunden werden, damit alle untergeordneten Komponenten dieselben Theme-Informationen erhalten. Dadurch wird verhindert, dass einzelne Bereiche der Oberfläche anders reagieren als der Rest der Anwendung.

Zusammengefasst habe ich gelernt, dass gutes UI-Styling nicht nur bedeutet, dass etwas optisch passend aussieht. Entscheidend ist auch, dass Design-Entscheidungen zentral verwaltet, wiederverwendbar umgesetzt und für den Benutzer dauerhaft nachvollziehbar gespeichert werden.
