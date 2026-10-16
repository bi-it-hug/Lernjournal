## 2026-10-16

### **Figma: Textbearbeitung und flexible Komponenten**

Seit Montag, dem 12. Oktober, habe ich mich unter anderem mit der Textbearbeitung und dem Aufbau wiederverwendbarer Komponenten in Figma beschäftigt. Dabei ging es darum, bestehende Designs gezielter zu bearbeiten und Komponenten so aufzubauen, dass sie unterschiedliche Inhalte aufnehmen können.

#### **1. Schrift formatieren und gleiche Schriftarten auswählen**

Ich habe gelernt, wie ich Text in Figma kursiv formatiere. Dazu wähle ich den Text aus und verwende unter Windows `Ctrl + I` oder wähle in den Texteinstellungen den Schriftschnitt `Italic`. Voraussetzung ist, dass die verwendete Schrift einen passenden kursiven Schnitt besitzt. Sollen nur einzelne Wörter kursiv sein, markiere ich diese innerhalb der Textebene.

Ausserdem habe ich gelernt, wie ich Textebenen mit derselben Schriftart gemeinsam auswählen kann. Dafür markiere ich eine passende Textebene und verwende `Edit > Select all with same font`. So lassen sich entsprechende Stellen schneller finden und gemeinsam bearbeiten. Falls ich noch keine passende Ebene gefunden habe, kann ich eine temporäre Textebene mit der gesuchten Schrift erstellen und diese als Ausgangspunkt verwenden.

#### **2. Instance Swap und Slots unterscheiden**

Ein Schwerpunkt war der Unterschied zwischen Instance Swap und Slots. Mit einem Instance Swap ersetze ich eine verschachtelte Komponenteninstanz durch eine andere. Das eignet sich beispielsweise für ein Icon in einem Button oder Dialog, wenn die Struktur gleich bleiben soll.

Ein Slot bietet mehr Freiheit für den Inhalt einer Komponenteninstanz. Darin können verschiedene Ebenen eingefügt, entfernt oder neu angeordnet werden, ohne die Instanz von ihrer Hauptkomponente zu lösen. Das ist beispielsweise für den Inhalt eines Dialogs sinnvoll, wenn dort je nach Verwendung Text, Bilder oder mehrere Eingabefelder benötigt werden.

Beide Möglichkeiten lassen sich kombinieren: Ein Dialog kann einen Instance Swap für das Symbol im Header und einen Slot für den Inhalt verwenden. Ich habe dadurch besser verstanden, dass ich bei Komponenten zwischen festen Alternativen und frei zusammenstellbarem Inhalt unterscheiden muss. Bei Slots können bevorzugte Komponenten vorgeschlagen werden; diese Vorschläge beschränken den möglichen Inhalt jedoch nicht.

#### **3. Offene Fragen bei Bibliotheken und Animationen**

Ich habe mich auch mit der Veröffentlichung von Designsystem-Inhalten beschäftigt. Dabei kamen Fragen dazu auf, warum Inhalte nicht veröffentlicht werden und als `hidden` erscheinen. Die konkrete Ursache ist in den für diesen Eintrag lesbaren Chatverläufen nicht nachvollziehbar geklärt und bleibt deshalb ein offener Punkt.

Eine weitere Frage betraf Figma Slides: Kann ein Frame eine eigene Animation haben, während ein enthaltenes Element separat animiert wird? Die damalige Recherche ergab dafür keine eindeutige Bestätigung. Deshalb halte ich diese Möglichkeit noch nicht als gesicherte Funktion fest. Als nächster Schritt wäre ein direkter Test mit einem Frame und einer darin enthaltenen Ebene sinnvoll.

#### **4. Erkenntnis**

Ich habe diese Woche vor allem gelernt, Figma gezielter zu bedienen und die Flexibilität von Komponenten bewusster zu planen. Bei Texten helfen mir passende Auswahlfunktionen, Änderungen effizienter vorzunehmen. Beim Komponentenaufbau hilft mir die Unterscheidung zwischen Instance Swap und Slots dabei, für den jeweiligen Inhalt die passende Lösung zu wählen.
