## 2026-11-19

### **Figma-Mockups mit shadcn-Komponenten**

Seit dem letzten Lernjournal-Eintrag habe ich im Projekt SmartFarming UI Regeln für die Figma-Mockups festgelegt und dazu eine Anleitung für das Team geschrieben.

#### **1. Komponenten aus den Assets verwenden**

Für alle Mockups gilt: Komponenten werden immer aus dem Assets-Tab der shadcn-Bibliothek in das Design gezogen, statt sie selbst nachzubauen. So arbeitet jede Person mit Instanzen derselben Hauptkomponenten. Da unsere UI-Bibliothek Blazor Blueprint ebenfalls auf dem Design von shadcn/ui basiert, entsprechen die Elemente im Mockup den Komponenten, die später im Code verwendet werden.

#### **2. Nur Farbvariablen statt fixer Farbwerte**

Zusätzlich dürfen im Mockup nur die Farbvariablen von shadcn verwendet werden und keine fix eingetragenen Farbcodes. Dadurch bleiben die Farben im ganzen Design einheitlich, und Änderungen am Theme – zum Beispiel für den Dark Mode – wirken sich zentral auf alle Screens aus. Das knüpft an meine früheren Erkenntnisse zu Themes in MudBlazor an: Design-Entscheidungen gehören an eine zentrale Stelle.

#### **3. Erkenntnis**

Regeln helfen nur, wenn alle sie kennen. Mit der Anleitung kann jedes Teammitglied die Mockups gleich aufbauen, und die Lücke zwischen Design und Umsetzung wird kleiner. Als Product Owner habe ich gemerkt, dass einheitliche Vorgaben am Anfang später viel Abstimmungsaufwand sparen.
