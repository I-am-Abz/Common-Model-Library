# Common Model Library (CML) 
![Logo of Stadt Freiburg i. Br.](/img/logo_freiburg.gif) 

## Inhaltsverzeichnis
- [1 - Warum CML?](#1---warum-cml)
- [2 - Quickstart-Anleitung](#2---quickstart-anleitung)
- [4 - Komplexe Prozesse designen](#4---komplexe-prozesse-designen)
   - [4a - Modul: Konfiguration](#4a---modul--konfiguration)
   - [4b - Modul: Antrag](#4b---modul--antrag)
   - [4c - Modul: Sachbearbeitung](#4c---modul--sachbearbeitung)
- [5 - Funktionen](#5---funktionen)
   - [5a - Funktion: AttachmentProcessor](#5a---funktion--attachmentprocessor)
- [6 Lizenz, Vorschläge etc.](#6---Lizenz-Vorschläge-etc)

## 1 - Warum CML?
Der Service-BW-Prozessdesigner ist ein mächtiges Tool, mit dem Kommunen beliebig komplexe Online-Anträge umsetzen können.
Selbst Details wie "Wann wird der Bürger benachrichtigt?" können frei gestaltet werden.\
\
Die Grundlage dafür bildet das sog. Prozessmodell, indem alle Aktivitäten des Prozesses definiert sind.\
Auf Grund der vielfältigen Möglichkeiten ist die Entwicklung eines solchen Prozessmodells jedoch enorm komplex.\
Die Entwicklung eines Prozessmodells von "0 auf 100" kostet somit sehr viel Zeit.\
\
Dabei ist es jedoch gar nicht nötig jeden Prozess von "0 auf 100" neu zu entwickeln.\
Schließlich folgen die meisten Anträge eigentlich einem einheitlichen Ablaufschema:

1. Antragstellung durch Bürger
2. Prüfung durch zuständige Stelle
3. Entscheidung durch zuständige Stelle
4. Erbringung der beantragten Leistung (z.B. Zustellung einer Erlaubnis)

Die **CML** greift genau diesen Gedanken auf und hilft die dabei die **Entwicklungszeit für Service-BW-Prozesse drastisch zu verkürzen.**
Prozessmodelle, die dem obigen Ablaufschema entsprechen, sind in wenigen Klicks erstellt:

Es muss nur der Prozess konfiguriert ggf. Hinweistexte eingepflegt werden.\
Den Rest erledigt die CML!

Aber auch komplexe Anträge, die sich nicht einfach so in ein abtraktes Schema pressen lassen, können mithilfe der CML umgesetzt werden.\
Jedes Modul und jede Funktion kann völlig unabhängig eingesetzt werden und ist dadurch wiederverwendbar...\
(Siehe Anleitungen ab Abschnitt 3)

**Die wichtigsten Vorteile der CML auf einen Blick:**
- Einfache Prozesse sind mit wenigen Klicks erstellt
- Auch komplexe Prozesse können relativ einfach umgesetzt werden
- Best-Practices (der Stadt Freiburg) sind direkt in die CML integriert
- Konform zu den aktuellen Qualitätskriterien des Innenministerium BW
- Automatische Benachrichtung der Bürger und Sachbearbeiter
- Der Bürger erhält vor dem Absenden des Antrags eine übersichtliche Zusammenfassung
- Unterstützung bei der Einrichtung durch integrierte Fehlerbehandlung


## 2 - Quickstart-Anleitung

## 3 - Voraussetzungen an die Formulare 

## 4 - Komplexe Prozesse designen

### 4a - Modul: Konfiguration
**Key:** m3.1201.cml.konfiguration


**Input-Parameter:** (Pflichtparameter  mit \*)
| Name                     | Erläuterung                                                                                                                             |
| -----------              | -----------                                                                                                                             |
| leistung (\*)            | ID der Leistung, aus der derProzess gestartet wurde. Wird benötigt, um das zuständige Behördenkonto zu ermitteln.                       |
| region (\*)              | ID der Leistung, aus der derProzess gestartet wurde. Wird benötigt, um das zuständige Behördenkonto zu ermitteln.                       |
| sbServicekontoId         | ID des Behördenkontos, falls das zuständige Behördenkonto nicht ausgelesen werden kann.                                                 |
| startedBy (\*)           | User-ID des Antragstellers. Dieser bekommt eventuell Fehlermeldungen angezeigt, falls dieser keine Region oder Leistung ausgewählt hat  |


**Output-Parameter:**
| Name                     | Wert (falls bekannt) | Erläuterung                                                                |
| -----------              | -----------          | -----------                                                                |
| sbServicekontoId         |                      | ID des Behördenkontos, das für die spätere Sachbearbeitung zuständig ist.  |
| killable                 | "true"               | Falls "true", kann der Antrag durch z.B. den Bürger gelöscht werden.       |


### 4b - Modul: Antrag
**Key:** m3.1201.cml.antrag

| Name                     | Erläuterung                                                                                                                          |
| -----------              | -----------                                                                                                                          |
| eIdLogin                 | Falls "true" muss der Bürger sich mithilfe der Online-Ausweis-Funktion des Personalausweis anmelden                                  |
| formularAS (\*)          | ID des Formulars, das dem Bürger angezeigt werden soll. (Format: '{Mandanten-ID}:{Formular-ID}:{Version}')                           |
| hinweiseAntragstellung   | Wird dem Bürger vor dem Formular angezeigt ("Was muss der Bürger für den Antrag beachten?" Welche Nachweise muss er bereithalten?)   |
| hinweiseWeitererAblauf   | Wird dem Bürger nachdem Absenden des Formulars angezeigt. ("Wie geht es mit dem Antrag weiter?")                                     |
| killable                 | Falls "true", kann der Antrag durch z.B. den Bürger gelöscht werden.                                                                 |
| logo                     | Logo der Behörde. (Am besten als Link. Auch Base64-Codierte Grafiken sind möglich.)                                                  |
| nameZustaendigeStelle    | Name der zuständigen Behörde (Falls nicht gesetzt, wird "Serviceportal Baden-Württemberg" an den entsprechenden Stellen angezeigt.)  |
| processInstanceId (\*)   | Vorgangsnummer.                                                                                                                      |
| processName (\*)         | Name des Prozesses (z.B. "Geburtsurkunde beantragen").                                                                               |
| sbServicekontoId (\*)    | ID des Behördenkontos, das für die spätere Sachbearbeitung zuständig ist.                                                            |
| startedBy (\*)           | User-ID des Antragstellers.                                                                                                          |
| startedByName (\*)       | Name des Antragstellers.                                                                                                             |


**Output-Parameter:**
| Name                     | Wert (falls bekannt) | Erläuterung                                                           |
| -----------              | -----------          | -----------                                                           |
| Form                     |                      | Das vom Bürger ausgefüllte Formular als FormContent-Objekt.           |
| killable                 | "false"              | Falls "true", kann der Antrag durch z.B. den Bürger gelöscht werden.  |


### 4c - Modul: Sachbearbeitung

**Key:** m3.1201.cml.sachbearbeitung

| Name                     | Erläuterung                                                                                                                          |
| -----------              | -----------                                                                                                                          |
| Form (\*)                | Das vom Bürger ausgefüllte Formular als FormContent-Objekt.                                                                          |
| formularSB (\*)          | ID des Formulars, das der Sachbearbeitung angezeigt werden soll. (Format: '{Mandanten-ID}:{Formular-ID}:{Version}')                  |
| formularRueckfragen (\*) | ID des Formulars, das dem Bürger bei Rückfragen angezeigt werden soll. (Format: '{Mandanten-ID}:{Formular-ID}:{Version}')            |
| hinweiseAbholung         | Wird dem Bürger in der abschließenden Servicekonto-Nachricht angezeigt.  (z.B. Link auf OE mit Öffnungszeiten)                       |
| hinweiseAbschluss        | Wird dem Bürger in der abschließenden Servicekonto-Nachricht angezeigt.                                                              |
| hinweiseWeitererAblauf   | Wird dem Bürger nachdem Absenden des Formulars (Rückfragen) angezeigt. ("Wie geht es mit dem Antrag weiter?")                        |
| killable                 | Falls "true", kann der Antrag durch z.B. den Bürger gelöscht werden.                                                                 |
| logo                     | Logo der Behörde. (Am besten als Link. Auch Base64-Codierte Grafiken sind möglich.)                                                  |
| nameZustaendigeStelle    | Name der zuständigen Behörde (Falls nicht gesetzt, wird "Serviceportal Baden-Württemberg" an den entsprechenden Stellen angezeigt.)  |
| processInstanceId (\*)   | Vorgangsnummer.                                                                                                                      |
| processName (\*)         | Name des Prozesses (z.B. "Geburtsurkunde beantragen").                                                                               |
| sbServicekontoId (\*)    | ID des Behördenkontos, das für die spätere Sachbearbeitung zuständig ist.                                                            |
| startedBy (\*)           | User-ID des Antragstellers.                                                                                                          |
| startedByName (\*)       | Name des Antragstellers.                                                                                                             |


## 5 - Funktionen

### 5a - Funktion: AttachmentProcessor

## 6 Lizenz, Vorschläge etc.
