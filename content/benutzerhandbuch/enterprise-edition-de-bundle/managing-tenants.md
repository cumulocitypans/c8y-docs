---
weight: 10
title: Verwalten von Mandanten
layout: redirect
---

Wenn Sie Service Provider sind oder die Enterprise Edition von Cumulocity nutzen, möchten Sie eventuell eigene Mandanten verwalten.

Die Mandantenverwaltung ermöglicht es Ihnen, eigene Untermandanten zu erstellen und zu verwalten, und ihnen Zugriff auf Ihre Anwendungen zu gewähren.

> Wichtig: Es besteht ein entscheidender Unterschied zwischen mehreren Mandanten einerseits und mehreren Benutzern mit verschiedenen Berechtigungen innerhalb eines Mandanten andererseits. Mandanten sind physikalisch getrennte Datenbereiche mit einer eigenen URL, eigenen Benutzern einer eigenen Anwendungsverwaltung und ohne Datenteilung. Benutzer eines Mandanten teilen sich standardmäßig dieselbe URL und denselben Datenbereich. Sollte es sich bei Ihren Benutzern also etwa um verschiedene Kunden handeln, die streng getrennt gehalten werden müssen, da es sich eventuell sogar um Mitbewerber handelt, empfehlen wir dringend, mit verschiedenen Mandanten zu arbeiten.
> 
> **Info**: Wenn Sie diese Funktion verwenden möchten, wenden Sie sich bitte an sales@cumulocity.com.

Um die Mandantenfunktionalität nutzen zu können, muss Ihr Benutzer über die entsprechenden Berechtigungen verfügen. Informationen zum Bearbeiten von Berechtigungen finden sie unter [Erstellen und Bearbeiten von Rollen](/guides/benutzerhandbuch/administration#managing-permissions) im Abschnitt Verwalten von Berechtigungen. Da es sich bei der Bearbeitung von Mandanten um ein sensibles Verfahren handelt, sind die entsprechenden Berechtigungen granularer:

*   Read: Durchsuchen und Ansehen von Mandanten.
*   Create: Erstellen neuer Mandanten.
*   Update: Bearbeiten von Mandanten (einschließlich Abonnements) und Sperren oder Aktivieren von Mandanten.
*   Change: Erstellen, Bearbeiten und Löschen von Mandanten

### Anzeigen von Untermandanten

Klicken Sie **Untermandanten** im Menü **Mandanten**, um eine Liste aller Untermandanten in Ihrem Konto anzuzeigen.

Die Seite **Mandanten** zeigt die folgenden Informationen für jeden Untermandanten an:

*   Name des Untermandanten, z.B. Name des Unternehmens Ihres Kunden.
*   ID und Domain. Beim Erstellen des Mandanten wird die ID zum ersten Teil der URL. Wenn Sie beispielsweise einen Mandanten mit der ID "acme" auf cumulocity.com erstellen, lautet die URL des Mandanten "acme.cumulocity.com". Beachten Sie, dass Sie, nachdem der Mandant einmal erstellt wurde, zwar die URL später ändern können, nicht aber die ID.
*   Optionaler Kontaktname und Telefonnummer.
*   Das Erstellungsdatum für den Mandanten.
*   Status des Mandanten, entweder aktiv (angezeigt durch ein grünes Häkchen) oder gesperrt (angezeigt durch ein rotes Kreuz).

Wenn Sie den Management-Mandanten verwenden, sehen Sie eine weitere Spalte **Übergeordneter Mandant**. Die Spalte zeigt den Mandanten an, der den aktuellen Mandanten erstellt hat.

![Untermandanten](/guides/images/benutzerhandbuch/ee-subtenants.png)

### <a name="creating-tenants"></a>Anlegen von Untermandanten

Um einen neuen Mandanten zu erstellen, klicken Sie **Mandanten anlegen** rechts oben in der Menüleiste. 

![Mandanten anlegen](/guides/images/benutzerhandbuch/ee-subtenant-create.png)

Geben Sie für den neuen Mandanten folgende Attribute an:

|Feld|Beschreibung
|:--------|:-----
|Domain/ URL|Geben Sie eine eindeutige ID als ersten Teil der URL ein. Wenn Sie beispielsweise "acme" als ID auf cumulocity.com eingeben, lautet die URL des Mandanten "acme.cumulocity.com". Sie können nur eine Subdomain-Ebene verwenden. Sie können zum Beispiel nur "acme.cumulocity.com"auf cumulocity.com verwenden. Sie können aber nicht "mycustomer.acme.cumulocity.com" wählen. Dies wird vom TLS-Standard nicht unterstützt. 
|Name|Name des Mandanten, z. B. Name des Unternehmens.
|E-Mail des Administrators|Sie müssen eine gültige E-Mail-Adresse angeben, damit Benutzer ihr Passwort ändern können.
|Benutzername des Administrators|Benutzername des Administrators dieses Mandanten.
|Kontaktname|Optionaler Name des Ansprechpartners.
|Telefonnummer|Optionale Telefonnummer des Ansprechpartner.
|Link zum Zurücksetzen des Passworts als E-Mail senden|Standardmäßig ausgewählt. Wenn Sie diese Option deaktivieren, müssen Sie eine Passwort bereitstellen und dieses bestätigen (weitere Informationen zur Passwortstärke finden Sie unter [Anmelden](/guides/benutzerhandbuch/overview#login) im Abschnitt Erste Schritte).
|Mandantenregel|Sie können eine Mandantenregel aus der Dropdown-Liste auswählen, die auf den Mandanten angewendet werden soll.

Felder, die mit einem Sternsymbol * gekennzeichnet sind, sind Pflichtfelder.

Klicken Sie **Speichern**, um Ihre Eingaben zu speichern.

Nachdem der Mandant erstellt wurde, wird er automatisch mit einem ersten Administrator-Benutzer ("Benutzername des Administrators") eingerichtet. Dieser Administrator kann andere Benutzer erstellen und Berechtigungen vergeben. Der erste Benutzer kann nicht gelöscht werden, um ein Aussperren zu verhindern.

Vom Management-Mandanten aus können Sie anderen Mandanten erlauben, Untermandanten zu erstellen. Selektieren Sie dazu "Erstellen von Untermandanten zulassen".


### Bearbeitung von Untermandanten-Attributen

Klicken Sie auf einen Untermandanten, um diesen zu bearbeiten oder klicken Sie **Bearbeiten** im Kontextmenü, auf das Sie über das Menüsymbol zugreifen können.

In der Registerkarte **Attribute** können alle Felder außer der ID und des Benutzernamens des Administrators bearbeitet werden. Details zu den einzelnen Feldern finden Sie unter [Erstellen von Untermandanten](#creating-tenants).

### Sperren von Untermandanten

Sie können Mandanten zeitweilig sperren. Das Sperren eines Mandanten verhindert jeglichen Zugriff auf diesen Mandanten, unabhängig davon, ob der Zugriff über eine Gerät, einen Benutzer oder eine andere Anwendung erfolgt.

Um einen Mandanten zu sperren, klicken Sie auf das Menüsymbol und wählen Sie im Kontextmenü **Entfernen**.

![Sperren eines Mandanten](/guides/images/benutzerhandbuch/ee-subtenant-suspend.png)

Bestätigen Sie im folgenden Dialogfenster das Sperren, indem Sie **OK** klicken und Ihr Passwort eingeben Der Mandant wird durch ein rotes Kreuzsymbol als gesperrt gekennzeichnet. Außerdem wird eine E-Mail an den Administrator des Mandanten gesendet, wenn eine entsprechende E-Mail-Adresse konfiguriert ist.

> **Info**: Als Service Provider können Sie diese E-Mail unterdrücken.

Ist ein Mandant gesperrt, bleiben die Daten des Mandanten in der Datenbank und stehen jederzeit wieder zur Verfügung. Klicken Sie **Aktivieren**, um die Daten wiederherzustellen.

### Löschen von Untermandanten

Um einen Untermandanten und alle seine Daten endgültig zu löschen, klicken Sie auf das Menüsymbol und wählen Sie im Kontextmenü **Löschen**.

> **Info**: Dieser Vorgang kann nicht rückgängig gemacht werden. Aus Sicherheitsgründen ist er daher nur im Management-Mandanten möglich.


### <a name="subscribe"></a>Abonnieren und Überwachen von Anwendungen

In der Registerkarte **Anwendungen** können Sie alle für einen Mandanten abonnierten Anwendungen ansehen sowie Anwendungen für einen Mandanten abonnieren oder entfernen. Standardmäßig werden für einen Mandanten die Standardanwendungen von Cumulocity abonniert.

![Anwendung abonnieren](/guides/images/benutzerhandbuch/ee-subtenants-applications.png)

Um eine Anwendung für einen Mandanten zu abonnieren, bewegen Sie den Mauszeiger über die Anwendungen unter **Verfügbare Anwendungen** auf der rechten Seite und klicken Sie bei der gewünschten Anwendung **Abonnieren**.

Um eine Anwendung zu löschen, bewegen Sie den Mauszeiger über die Anwendungen unter **Abonnierte Anwendungen** auf der linken Seite und klicken Sie bei der gewünschten Anwendung **Abbestellen**.

#### Überwachen von Microservices

Für alle Anwendungen, die als Microservices von Cumulocity gehostet werden, wird neben dem Namen der Microservice-Status als Symbol angezeigt:

<img src="/guides/images/benutzerhandbuch/admin-applications-status.png" alt="Anwendungsstatus" style="max-width: 75%">

Der Microservice kann sich in einem der folgenden Status befinden:

* <img src="/guides/images/icons/ok.png" alt="Up" style="max-width: 100%"> Microservice ist in Betrieb
* <img src="/guides/images/icons/warning.png" alt="Up" style="max-width: 100%"> Microservice ist gestört
* <img src="/guides/images/icons/danger.png" alt="Up" style="max-width: 100%"> Microservice ist außer Betrieb

Details zum Status können durch Ausklappen des jeweiligen Eintrags angezeigt werden. 

<img src="/guides/images/users-guide/Administration/admin-application-details.png" alt="Anwendungsdetails" style="max-width: 75%">

Folgende Informationen werden angezeigt:

* Aktiv: Anzahl der aktiven Microservice-Instanzen
* Gestört: Anzahl der inaktiven Microservice-Instanzen
* Erwartet: Anzahl der erwarteten Microservice-Instanzen
* Name: Name der Microservice-Instanz
* Neustarts: Anzahl der Neustarts von Microservice-Instanzen

Weitere Details finden Sie in der Registerkarte **Status** der entsprechenden Anwendung, siehe [Administration > Verwalten von Anwendungen](/guides/users-guide/administration#managing-applications).

### <a name="tenants-custom-properties"></a>Bearbeitung von benutzerdefinierten Attributen

Die Registerkarte **Benutzerdefinierte Attribute** ermöglicht Ihnen das Anzeigen und Ändern von Werten von benutzerdefinierten Attributen, sowohl vordefinierten (wie "Externe Referenz") als auch denen, die in der [Attributsbibliothek](/guides/benutzerhandbuch/administration#properties) definiert sind. Solche Attribute werden auch als Spalten in der [Benutzungsstatistiktabelle](#usage-stats) angezeigt.

![Benutzerdefinierte Attribute](/guides/images/benutzerhandbuch/Admin_SubtenantCustomProperties.png)

**Begrenzen der Geräteanzahl für Untermandanten**

Der Plattformadministrator kann die Anzahl der gleichzeitig registrierten Hauptgeräte oder der registrierten Geräte insgesamt (einschließlich Kindgeräte) begrenzen. Der Plattformadministrator kann außerdem auf der Seite **Nutzungsstatistiken** die Höchstanzahl registrierter Hauptgeräte und Geräte insgesamt sowie den Höchstwert des genutzten Datenspeichers einsehen. 

### <a name="usage-stats"></a>Anzeigen von Nutzungsstatistiken

Die Seite **Nutzungsstatistiken** zeigt statistische Informationen für jeden Untermandanten an.

Die folgenden Informationen werden für jeden Untermandanten angezeigt:

*   ID: ID des Untermandanten
*   API-Anfragen: Gesamtanzahl der API-Anfragen, einschließlich Anfragen von Geräten und Anwendungen
*   Geräte-API-Anfragen: Anzahl der API-Anfragen von Geräten
*   Speicher (MB): Gespeicherte Daten in Ihrem Konto
*   Hauptgeräte: Anzahl der Geräte ohne Kindgeräte
*   Höchstwert Hauptgeräte: Höchstanzahl Hauptgeräte, ohne Kindgeräte
*   Geräte: Die Gesamtanzahl der mit dem Untermandanten verbundenen Geräte
*   Höchstwert Geräte: Höchstanzahl Geräte, einschließlich Kindgeräte
*   Endpunktgeräte: Blattgeräte (ohne Gateways und Kinder)
*   Abonnierte Anwendungen: Anzahl der vom Untermandanten abonnierten Anwendungen
*   Erstellungszeitpunkt: Datum und Zeit der Erstellung des Untermandanten
*   Erzeugte Alarme: Anzahl der erzeugten Alarme
*   Aktualisierte Alarme: Anzahl der aktualisierten Alarme
*   Erstellte Stammdaten: Anzahl der erstellten Managed Objects
*   Aktualisierte Stammdaten: Anzahl der aktualisierten Managed Objects
*   Erstellte Ereignisse: Anzahl der erstellten Ereignisse
*   Aktualisierte Ereignisse: Anzahl der aktualisierten Ereignisse
*   Erstellte Messwerte: Anzahl der erstellten Messwerte
*   Gesamt Inbound-Transfer: Summe aller Inbound-Transfers (erzeugte Alarme, aktualisierte Alarme, erstellte Ereignisse, aktualisierte Ereignisse, erstellte Stammdaten, aktualisierte Stammdaten, erstellte Messwerte). Inbound-Transfer bezeichnet alle Inbound-Anfragen, die ausgeführt werden, um Daten zur Cumulocity IoT-Plattform zu übertragen. Dazu zählen unter anderem Sensormesswerte, Alarme, Ereignisse und Kommandos, die zwischen Geräten und der Cumulocity IoT-Plattform mittels REST- und/oder MQTT-Schnittstellen übertragen werden. Solche Inbound-Anfragen können auch von eigenen Microservices, Webseiten oder anderen Clients stammen.  
*   Übergeordneter Mandant: Name des übergeordneten Mandanten (nur verfügbar für den Management-Mandanten)
*   Externe Referenz: Dieses Feld ist für den individuellen Gebrauch. Sie können hier beispielsweise einen Link zum CRM-System oder eine interne Kundennummer einfügen.

Außerdem werden benutzerdefinierte Attribute angezeigt, falls vorhanden.

Benutzerdefinierte Attribute können in der [Attributsbibliothek](/guides/benutzerhandbuch/administration#properties) definiert werden. Anschließend können entsprechende Werte in der Registerkarte [Benutzerdefinierte Attribute](#tenants-custom-properties) des Mandanten eingestellt werden.

![Nutzungsstatistiken](/guides/images/benutzerhandbuch/Admin_TenantUsageStatistics.png)

Sie können die Liste der Nutzungsstatistiken nach einem bestimmten Zeitraum filtern, indem Sie einen Start- und einen Endzeitpunkt in der oberen Menüleiste eingeben und **Filter** klicken. Sie können außerdem die Liste nach jeder Spalte filtern und und sortieren, indem Sie auf das Filtersymbol neben dem Namen der entsprechenden Spalte klicken und die Filterkriterien eingeben. Weitere Informationen zur Filterfunktionalität finden Sie unter [Filtern](/guides/benutzerhandbuch/overview#filtering) im Abschnitt Erste Schritte.

Klicken Sie **Export CSV** rechts oben in der Menüleiste, um die aktuelle Ansicht der Statistikentabelle als CSV-Datei zu exportieren. Im folgenden Fenster können Sie die CSV-Ausgabe anpassen.

<img src="/guides/images/benutzerhandbuch/Admin_UsageStatisticsExport.png" alt="Export statistics" style="max-width: 50%">

### <a name="tenant-policies"></a>Mandantenregeln

Eine Mandantenregel ist eine Menge von Mandantenoptionen und Datenhaltungsregeln. Mandantenoptionen und Datenhaltungsregeln können während der Erstellung eines Mandanten konfiguriert werden.

Das Erstellen einer Mandantenregel mit bestimmten Optionen und Regeln spart Zeit bei der Erstellung verschiedener Mandanten mit den gleichen Einstellungen.

> **Info**: Die Optionen und Regeln werden in den Mandanten kopiert. Änderungen an der Regel haben keine Auswirkungen auf bereits erstellte Mandanten.

Klicken Sie **Mandantenregeln** im Menü **Mandanten**, um alle verfügbaren Regeln anzuzeigen.

![Mandantenregeln](/guides/images/benutzerhandbuch/ee-tenant-policies.png)

Für jede Mandantenregel wird der Name, eine optionale Beschreibung und die Anzahl der Optionen und Datenerhaltungsregeln angezeigt, wahlweise in Listen- oder Gitteransicht.

#### Hinzufügen einer Mandantenregel

Klicken Sie **Mandantenregel hinzufügen** in der oberen Menüleiste, um eine neue Mandantenregel zu erstellen.

![Neue Regel hinzufügen](/guides/images/benutzerhandbuch/Admin_TenantsAddPolicy.png)

1.  Geben Sie einen Namen und optional eine Beschreibung ein.
2.  Geben Sie mindestens eine Datenerhaltungsregel ein. Weitere Informationen zur Erstellung von Datenerhaltungsregeln finden Sie unter [Datenerhaltungsregeln](/guides/benutzerhandbuch/administration#retention-rules).
3.  Geben Sie optional eine Mandantenoption ein.
4.  Klicken Sie **Speichern**, um Ihre Eingaben zu speichern.

#### Bearbeiten, Duplizieren und Löschen von Regeln

Klicken Sie auf eine Regel, um diese zu bearbeiten oder öffnen Sie das Kontextmenü über das Menüsymbol und klicken Sie **Bearbeiten**.

Um den Namen einer Regel zu ändern, klicken Sie auf den Namen in der oberen Leiste, ändern Sie den Namen und klicken Sie das grüne Häckchen-Symbol, um Ihre Änderungen zu speichern.

Um eine Datenhaltungsregel oder eine Mandantenoption aus einer Regel zu entfernen, bewegen Sie den Mauszeiger darüber und klicken Sie das Löschen-Symbol.

Um eine Regel zu duplizieren, klicken Sie auf das Menüsymbol und wählen Sie im Kontextmenü **Duplizieren**.

Um eine Regel zu löschen, klicken Sie auf das Menüsymbol und wählen Sie im Kontextmenü **Löschen**.

![Manantenregeln Kontextmenü](/guides/images/benutzerhandbuch/ee-tenant-policy-contextmenu.png)