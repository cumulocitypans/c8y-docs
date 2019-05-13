---
weight: 50
title: Anwenden von Geschäftsregeln
layout: redirect
---

<a name="event-processing"></a>
### Echtzeitverarbeitung

Mittels Echtzeitverarbeitung können Geschäftsregeln definiert werden, die automatisch in Echtzeit ausgeführt werden, sobald neue Daten eingehen oder bestehende Daten geändert werden. Die Logik wird in sogenannten Modulen implementiert, die aus einer Menge von CEP-Anweisungen bestehen.

> **Info:** Eine benutzerfreundliche Methode, Echtzeitregeln zu definieren, wird in der Cockpit-Anwendung mit den sogenannten [Smart Rules](/guides/benutzerhandbuch/cockpit#rules) bereitgestellt. Smart Rules sind ebenfalls CEP-Anweisungen, die in der Liste der Echtzeitregeln angezeigt werden, hier jedoch nicht bearbeitet werden können.

Klicken Sie **Echtzeitverarbeitung** im Menü **Geschäftsregeln**, um die vorhandenen Module anzuzeigen oder neue Module zu erstellen.

![Echtzeitverarbeitung](/guides/images/benutzerhandbuch/admin_event-processing.png)

Für jedes Modul wird in der Liste der Status (bereitgestellt = grünes Häkchen / nicht bereitgestellt = Ausrufungszeichen), der Name und das Datum der letzten Aktualisierung angezeigt.

Klicken Sie auf eine Anwendung, um diese zu bearbeiten oder klicken Sie auf das Menüsymbol und wählen Sie **Bearbeiten** im Kontextmenü.

Um ein Modul zu löschen, klicken Sie **Löschen** im Kontextmenü.

Anstatt ein Modul zu löschen, können Sie es auch zeitweise deaktivieren, indem Sie den Status auf "Nicht bereitgestellt" setzen.

**Erstellen neuer Module**

Um ein neues Modul zu erstellen, klicken Sie **Neues Modul** in der oberen Menüleiste.

<img src="/guides/images/benutzerhandbuch/admin-event-processing-new-module.png" alt="Neues Modul" style="max-width: 50%">

1.  Geben Sie oben einen Namen für das neue Modul ein. Es sind nur alphanumerische Zeichen ohne Leerzeichen zulässig.
2.  Standardmäßig ist der Status "Bereitgestellt" voreingestellt, so dass die Anweisungen, die Sie erstellen, unmittelbar ausgeführt werden. Um dies zu verhindern, schieben Sie den Regler auf "Nicht bereitgestellt".
3.  Geben Sie Ihre CEP-Anweisungen in das Textfeld **Quellcode** ein. Als Hilfe finden Sie einige Beispiele. Klicken Sie **Beispiele** und wählen Sie ein passendes Beispiel aus der Auswahlliste. Klicken Sie **Übernehmen**, um das Beispiel an der Position des Mauszeigers in das Textfeld zu kopieren.
4.  Klicken Sie **Speichern**, um Ihre Einstellungen zu speichern.

Das Beispielmodul erzeugt einen Alarm, wenn die Temperatur unter 0 Grad sinkt.

<img src="/guides/images/benutzerhandbuch/admin-event-processing-module-example.png" alt="Beispielmodul" style="max-width: 50%">

Wenn der Status eines Moduls auf "Bereitgestellt" steht, wird dies durch eine grünes Häkchen in der Modulliste angezeigt. Immer wenn eine Anweisung eine Ausgabe generiert, wird diese unter dem Häkchen angezeigt. Klicken Sie auf eine Ausgabezeile, um die detaillierte Ausgabe der Anweisung anzuzeigen. Klicken Sie **Alles löschen**, um die Ausgabe zu entfernen.

### <a name="reprio-alarms"></a>Alarmregeln

Alarmregeln ermöglichen es, den Schweregrad und Text von Alarmen zu ändern, um diese den Prioritäten Ihres Unternehmens anzupassen. Der Abbruch einer Verbindung wird beispielsweise standardmäßig als WICHTIG eingestuft, kann aber in Ihrem Fall KRITISCH sein. Daher können Sie eine Alarmregel definieren, die Alarme im Zusammenhang mit Verbindungsabbrüchen als KRITISCH einstuft.

Klicken Sie **Alarmregeln** im Menü **Geschäftsregeln**, um eine Liste aller Alarmregeln anzuzeigen.

<img src="/guides/images/benutzerhandbuch/admin-alarm-mapping.png" alt="Alarmregeln" style="max-width: 100%">

Für jede Alarmregel wird der Schweregrad und der Name der Regel angezeigt.

Klicken Sie auf einen Eintrag, um diesen zu bearbeiten.

Zum Löschen einer Alarmregel bewegen Sie den Mauszeiger darüber und klicken Sie auf die Schaltfläche **Löschen**.

**Hinzufügen einer Alarmregel**

Um eine Alarmregel hinzuzufügen, klicken Sie **Alarmregel hinzufügen** in der oberen Menüleiste.

<img src="/guides/images/benutzerhandbuch/Admin_AlarmMappingAdd.png" alt="Alarmregel hinzufügen" style="max-width: 50%">

1.  Geben Sie den Alarmtypen ein, den Sie ändern möchten.
2.  Geben Sie optional einen neuen Text für den Alarm ein. Wenn Sie keinen Text eingeben, wird der Ursprungstext beibehalten.
3.  Wählen Sie den gewünschten neuen Schweregrad aus, oder wählen Sie "Ignorieren", um den Alarm ganz zu unterdrücken.
4.  Klicken Sie **Speichern**, um Ihre Einstellungen zu speichern.
