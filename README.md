# Common Model Library (CML) 
![Logo of Stadt Freiburg i. Br.](/img/logo_freiburg.gif) 

## Inhaltsverzeichnis
- [1 - Einführung und Vorteile](#1---einführung-und-vorteile)
- [2 - Quickstart](#2---quickstart)
  * [2a - In 60 Sekunden zum eigenen Prozess](#2a---in-60-sekunden-zum-eigenen-prozess)
  * [2b - Texte individuell anpassen](#2b---texte-individuell-anpassen)
  * [2c - Hintergrund und Funktionsweise](#2c---hintergrund-und-funktionsweise)
- [3 - Voraussetzungen an die Formulare](#3---voraussetzungen-an-die-formulare)
- [4 - Komplexe Prozesse designen](#4---komplexe-prozesse-designen)
  * [4a - Modul: Konfiguration](#4a---modul-konfiguration)
  * [4b - Modul: Antrag](#4b---modul-antrag)
  * [4c - Modul: Sachbearbeitung](#4c---modul-sachbearbeitung)
- [5 - Funktionen](#5---funktionen)
  * [5a - Funktion: AttachmentProcessor](#5a---funktion-attachmentprocessor)
- [6 Lizenz, Vorschläge etc.](#6-lizenz-vorschläge-etc)

## 1 - Einführung und Vorteile
Der Service-BW-Prozessdesigner ist ein mächtiges Tool, mit dem Kommunen beliebig komplexe Online-Anträge umsetzen können.
Selbst Details wie "Wann wird der Bürger benachrichtigt?" können frei gestaltet werden.\
\
Die Grundlage dafür bildet das sog. Prozessmodell, indem alle Aktivitäten des Prozesses definiert sind.\
Aufgrund der vielfältigen Möglichkeiten ist die Entwicklung eines solchen Prozessmodells jedoch enorm komplex.\
Die Entwicklung eines Prozessmodells von "0 auf 100" kostet somit sehr viel Zeit.\
\
Dabei ist es jedoch gar nicht nötig jeden Prozess von "0 auf 100" neu zu entwickeln.\
Schließlich folgen die meisten Anträge eigentlich einem einheitlichen Ablaufschema:

1. Antragstellung durch Bürger
2. Prüfung durch zuständige Stelle
3. Entscheidung durch zuständige Stelle
4. Erbringung der beantragten Leistung (z.B. Zustellung einer Erlaubnis)

Die **CML** greift genau diesen Gedanken auf und hilft die dabei die **Entwicklungszeit für Service-BW-Prozesse drastisch zu verkürzen.**\
Prozessmodelle, die dem obigen Ablaufschema entsprechen, sind in wenigen Klicks erstellt:

Es muss nur der Prozess konfiguriert ggf. Hinweistexte eingepflegt werden.\
Den Rest erledigt die CML!

Aber auch komplexe Anträge, die sich nicht einfach so in ein abtraktes Schema pressen lassen, können mithilfe der CML umgesetzt werden.
Jedes Modul und jede Funktion kann völlig unabhängig eingesetzt werden und ist dadurch wiederverwendbar.\
(Siehe Anleitungen ab Abschnitt 3)
\
\
**Die wichtigsten Vorteile der CML auf einen Blick:**
- Einfache Prozesse sind mit wenigen Klicks erstellt
- Auch komplexe Prozesse können relativ einfach umgesetzt werden
- Best-Practices (der Stadt Freiburg) sind direkt in die CML integriert
- Konform zu den aktuellen Qualitätskriterien des Innenministerium BW
- Automatische Benachrichtung der Bürger und Sachbearbeiter
- Der Bürger erhält vor dem Absenden des Antrags eine Zusammenfassung des Antrags


## 2 - Quickstart

### 2a - In 60 Sekunden zum eigenen Prozess

**Wichtig:** Damit der Prozess anschließend gleich startet, sollten bei der Formularerstellung gleich die [Voraussetzungen an die Formulare](#3---voraussetzungen-an-die-formulare) beachtet werden!

1. Auf der [Testumgebung von Service-BW](actest.service-bw.de/) ein neues Prozessmodell anlegen.

![Neues Prozessmodell anlegen](/img/001.jpg) 


2. Dem Prozessmodell einen Namen geben und speichern.

![Prozessmodell benennen und speichern](/img/002.jpg) 


3. Service-BW generiert nun die sog. "Prozessmodell-ID."\
Diese brauchen Sie in Schritt 8 noch...\
(Am besten also kurz notieren.)

![Prozessmodell-ID merken](/img/003.jpg) 


4. In einem Editor der Wahl (z.B. Visual Studio Code oder Notepad++) das [Prozessparameter-Template](/Templates/Prozessparameter%20-%20Template.json) öffnen und dort unter `defaultValue` die Formular-IDs eintragen.\
Format: `{Mandant}:{Formular-ID}:{Versions-ID}` \
**Hinweis:** Vor der Zertifizierung muss der Parameter 'defaultValue' natürlich wieder entfernt werden.\
Sie brauchen diesen Paramter nur, um den Prozess vor der Zertifizierung testen zu können.

![Formular-IDs eintragen](/img/004.jpg)
    
**Tipp:** Am einfachsten gelangen Sie an die Formular-ID, wenn Sie das entsprechende Formular öffnen und diesen Teil aus der URL herauskopieren:

![Formular-IDs herausfinden](/img/005.jpg)

5. Das Prozessparameter-Template unter **Prozessparamter-Definitionen** hochladen und speichern

![Prozessmodellparameter-Definition hochladen](/img/006.jpg) 
   
   
6. In die **Fachliche Modellierung** wechseln und das [Prozessmodell-Template](/Templates/CML%20-%20Template.bpmn20.xml) hochladen.

![Prozessmodell-Template hochladen](/img/007.jpg) 
   
   
7. Die Prozessmodell-Datei bearbeiten.

![Prozessmodell-Template bearbeiten](/img/008.jpg)


8. Bei `Process identifier`die ID des Prozesses wie folgt ändern:\
`m{Mandanten-ID}.p{Prozessmodell-ID}` \
Unter `Name` muss der Name des Prozesses eingetragen werden, z.B. \"Wildunfall bescheinigen lassen\".

![Prozessmodell-Template bearbeiten](/img/009.jpg)


9. Anschließend die Prozessmodell-Datei speichern.\
Unter `Name`muss wieder der Name des Prozesses eingetragen werden.\
Bei `Description`können Sie einen kurzen Erklärungstext formulieren.

![Prozessmodell-Template speichern](/img/010.jpg)


10. Wieder zurück im Admincenter können Sie jetzt die Datei freigeben.

![Prozessmodell-Template freigeben](/img/011.jpg)


11. Wechseln Sie anschließend wieder in die **Fachliche Modellierung**.\
Schließen Sie dort diese Entwicklungsphase ab, indem Sie auf \"Stufe abschließen\" klicken.

![Stufe abschließen](/img/012.jpg)


12. Wechseln Sie nun in die **Technische Modellierung**.\
Deployen Sie dort das Prozessmodell.

![Prozess Deployen](/img/013.jpg)

Der Prozess ist nun voll funktionsfähig.\
Um das Ganze jetzt noch zu testen, können Sie den Prozess wie gwohnt einer Leistung zuweisen.\
Z.B. `Zuständigkeitsfinder > Leistung > Prozesse`


### 2b - Texte individuell anpassen


### 2c - Hintergrund und Funktionsweise
Die CML basiert auf einem modularen Ansatz:

Das Ziel war es häufig genutzte Features in wiederverwendbare und unabhängige Module zu vereinen.\
Dadurch soll es möglich sein, auch sehr komplexe Prozesse mit wenig Aufwand zu realiseren.\
Anstatt alles von \"0 auf 100\" zu entwickeln, können Sie z.B. einfach mehrere \"Sachbearbeiter\"-Module aneinandereihen und schon haben Sie mehrstufige Genehmigungsläufe realisiert.

Des Weiteren soll die CML unbegübten Entwicklern die komplizierte Konfiguration abnehmen.\
(Beispiel: Zuständiges Behördenkonto ermitteln)

**Das passiert bei der CML im Hintergrund:** \
Zunächst liest das in [2a eingefügte Template](#2a---in-60-Sekunden-zum-eigenen-Prozess) die sog. Prozessparameter aus und erstellt daraus sog. Prozessinstanz-Variablen. Diese Prozessinstanz-Variablen konfigurieren später die einzelnen Module, z.B.: \
- `formularAS` bestimmt, welches Formular dem Bürger angezeigt werden soll.
- `eIdLogin` legt fest, ob der Bürger sich Online ausweisen muss, um den Antrag aufzurufen.

Die eigentliche Arbeit verrichtet die CML später im Hintergrund, ohne dass Sie in Ihrem Prozessmodell jemans etwas einstellen mussten.

Ist diesem Task (Arbeitsschritt) abgeschlossen, erstellt die CML aus dem gleichen Grund auch für die in [2b definierten Texte](#2b---Texte-individuell-anpassen) entsprechende Prozessinstanz-Variablen.

Der nächste Task startet daraufhin die CML.\
Dazu ruft das Template den sog. Starter-Prozess auf. \
Der Starter-Prozess koordiniert daraufhin die einzelnen Module und sorgt dafür, dass jedes Modul richtig konfiguriert ist.

![Konfiguration](/img/Starter-BPMN.jpg)

Wenn Sie einen komplexeren Prozess designen möchten, können Sie theoretisch auch einen eigenen Starter-Prozess designen. \
Am einfachsten wird es jedoch sein, Sie rufen die benötigten CML-Module direkt in Ihrem Haupt-Prozess-Modell (Template) auf.

Näheres dazu finden Sie in [4 - Komplexe Prozesse designen](#4---komplexe-prozesse-designen).


## 3 - Voraussetzungen an die Formulare 

## 4 - Komplexe Prozesse designen

### 4a - Modul: Konfiguration
**Key:** m3.1201.cml.konfiguration

**BPMN-Diagramm:**
![Konfiguration](/img/Konfiguration-BPMN.jpg)

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

**BPMN-Diagramm:**
![Antrag](/img/Antrag-BPMN.jpg)

**Input-Parameter:** (Pflichtparameter  mit \*)
| Name                     | Erläuterung                                                                                                                          |
| -----------              | -----------                                                                                                                          |
| eIdLogin                 | Falls "true" muss der Bürger sich mithilfe der Online-Ausweis-Funktion des Personalausweis anmelden.                                 |
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

**BPMN-Diagramm:**
![Sachbearbeitung](/img/Sachbearbeitung-BPMN.jpg)

**Input-Parameter:** (Pflichtparameter  mit \*)
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
**Key:** m3.1201.cml.attachmentProcessor

**BPMN-Diagramm:**
![AttachmentProcessor](/img/AttachmentProcessor-BPMN.jpg)

**Input-Parameter:** (Pflichtparameter  mit \*)
| Name                     | Erläuterung                                                                                    |
| -----------              | -----------                                                                                    |
| form (\*)                | Das Formular, aus dem die PDF-Zusammenfassung generiert werden soll. (als FormContent-Objekt)  |
| onlySummary              | Falls "true" wird nur die Zusammenfassung erstellt. Weitere Anhänge bleiben unberücksichtigt.  |
| processName (\*)         | Name des Prozesses (z.B. "Geburtsurkunde beantragen").                                         |


**Output-Parameter:**
| Name                     | Wert (falls bekannt)   | Erläuterung                                                                                    |
| -----------              | -----------            | -----------                                                                                    |
| attachments              | (BinaryContent-Array)  | Objekt aller beigefügten Dateien (+ Zusammenfassung). In Servicekonto-Nachrichten verwendbar.  |


## 6 Lizenz, Vorschläge etc.
