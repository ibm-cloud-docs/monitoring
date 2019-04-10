---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, pricing

subcollection: Sysdig

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}
{:important: .important}
{:note: .note}


# Preisstruktur
{: #pricing_plans}

Es sind verschiedene Preisstrukturpläne für eine {{site.data.keyword.mon_full_notm}}-Instanz verfügbar.
{:shortdesc}
 

| Pläne            | Kategorie         | Datenerfassung  |
|------------------|--------------|------------------|
| `Testversion`          |              | Die Daten werden für maximal 20 Container pro Knoten oder für 200 angepasste Metriken pro Knoten nur für 30 Tage erfasst. |
| `Hochgestufte Kategorie` | `Basic`      | Die Daten werden für maximal 20 Container pro Knoten oder für 200 angepasste Metriken pro Knoten erfasst. |
| `Hochgestufte Kategorie` | `Pro`        | Die Daten werden für maximal 50 Container pro Knoten oder für 500 angepasste Metriken pro Knoten erfasst. |
| `Hochgestufte Kategorie` | `Advanced`   | Die Daten werden für maximal 110 Container pro Knoten oder für 1000 angepasste Metriken pro Knoten erfasst. |
{: caption="Tabelle 1. Liste der Servicepläne" caption-side="top"} 


**Hinweis:** Ein Knoten kann ein Host, ein Container, eine virtuelle Maschine, ein Bare Metal oder eine Metrikquelle sein, in der Sie einen Sysdig-Agenten installieren.

Wenn die Anzahl der Container pro Knoten oder die Anzahl der Metriken oberhalb des Schwellenwerts für den hochgestuften Kategorieplan über einen bestimmten Zeitraum liegt, wird die automatische Kategorieerkennung angewendet. Eine Alertbenachrichtigung wird nach Ihrer Benachrichtigungskonfiguration für die Rechnungsverwendung ausgelöst, wenn Sie den folgenden Alert aktivieren: **[{{site.data.keyword.IBM_notm}}]: Usage Kategorie ändern**

Sie können ein **angepasstes Preisangebot** für alle über die Obergrenze des *bezahlten Preisplans für die hochgestufte Kategorie Advanced* hinaus anfordern, indem Sie ein Ticket mit [IBM Cloud Support ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/unifiedsupport/supportcenter){:new_window} öffnen.
{: tip}

Die Daten werden nach den Standardrichtlinien in allen Plänen erfasst und gespeichert. Weitere Informationen finden Sie unter [Datenerfassung](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-about#overview_collection) und [Datenspeicherung](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-about#overview_retention).


## Ihre Nutzung überprüfen
{: #pricing_usage}

Um zu überwachen, wie der {{site.data.keyword.mon_full_notm}}-Service genutzt wird und wie hoch die Kosten für die Nutzung sind, siehe [Ihre Nutzung anzeigen](/docs/billing-usage?topic=billing-usage-viewingusage#viewingusage).



## Alert aktivieren, der Sie über eine Kategorieänderung benachrichtigt
{: #pricing_alert}

Wenn Sie benachrichtigt werden möchten, wenn sich eine Kategorie ändert, müssen Sie den folgenden Alert aktivieren: **[{{site.data.keyword.IBM_notm}}]: Usage Kategorie ändern**

Führen Sie die folgenden Schritte aus, um einen Alert zu aktivieren:

1. Starten Sie die Webbenutzerschnittstelle. Weitere Informationen zum Starten der Webbenutzerschnittstelle finden Sie im Abschnitt [Zur Webbenutzerschnittstelle navigieren](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
2. Erstellen Sie einen Benachrichtigungskanal. Weitere Informationen hierzu finden Sie im Abschnitt [Einen Benachrichtigungskanal konfigurieren](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-notifications#notifications_create). 
3. Klicken Sie auf **ALERTS**, um zum Abschnitt *Alerts* zu navigieren.
2. Suchen Sie nach **Änderung der [IBM]: Usage-Kategorie**.
3. Bearbeiten Sie den Alert, um den Benachrichtigungskanal hinzuzufügen.
4. Klicken Sie auf **Speichern**.



## Wie wird der Serviceplan-Alert generiert?
{: #pricing_how}

Wenn Sie benachrichtigt werden möchten, wenn sich eine Kategorie ändert, müssen Sie den folgenden Alert aktivieren: **[{{site.data.keyword.IBM_notm}}]: Usage Kategorie ändern**

**Hinweis:** Wenn Sie diesen Alert aktivieren, müssen Sie die Benachrichtigungskanäle angeben, über die Sie benachrichtigt werden möchten.

Die Nutzung wird als Durchschnitt der Anzahl der Knoten und Metriken berechnet, die alle 10 Sekunden in der vorhergehenden Stunde erfasst wurden. Kleine, kurzlebige Fluktuationen sind nicht enthalten. Der Unterschied zwischen der vorherigen und der aktuellen Nutzung wird einmal pro Stunde gemessen.

Die definierten Schwellenwerte werden auf folgende Weise festgelegt:

``` 
usageTiers {
  containerDensity {
    Basic = [0, 20]
    Pro = [21, 50]
    Advanced = [51, 100]
  }
  metricDensity {
    Basic = [0, 200]
    Pro = [201, 500]
    Advanced = [501, 1000]
}
```
{: screen}

Die Alertbenachrichtigung wird wie folgt generiert:
1. Jede Stunde, wenn die Anzahl der Container pro Knoten in einer Kategorie zunimmt, wird ein angepasstes Ereignis generiert.
2. Die Alertbedingung prüft alle angepassten Ereignisse, die Informationen zu den Änderungen in der Anzahl der Container pro Knoten enthalten. Wenn ein Ereignis gefunden wird, bei dem die Anzahl der Container in einer Kategorie vom Zeitpunkt der Berechnung der letzten Nutzung zunimmt, wird eine Benachrichtigung gesendet.

Die Häufigkeit des Alerts ist einmal pro Stunde. Bei einem schwankenden Knoten wird die Frequenz des Alerts höchstens alle zwei Stunden angezeigt.

Beachten Sie, dass der Alert nur dann generiert wird, wenn sich ein Knoten von der Kategorie *Basic* zu *Pro* oder zu *Advanced* verschiebt. 



### Beispiele
{: #pricing_examples}

**Beispiel 1** 

Die durchschnittliche Containeranzahl lautet wie folgt: 

| Stunde     | Anzahl der Container | Beschreibung                                                                   | Wird ein Alert generiert? |
|----------|----------------------|-------------------------------------------------------------------------------|------------------------|
| 10:00    | 18                   | Die Kategorie wird auf **Basic** festgelegt.                                                     | Nein                     |
| 11:00    | 21                   | Anzahl der Container befindet sich über der Kategorie *Basic*. Die Kategorie verschiebt sich zu **Pro**.            | Ja                    |
| 12:00    | 19                   | Die Anzahl der Container liegt unter der Kategorie *Basic*. Die Kategorie verschiebt sich wieder zu **Basic**.     | Nein                    |
| 13:00    | 20                   | Keine Kategorieänderung. Die Kategorie wird auf **Basic** festgelegt.                                     | Nein                     |
{: caption="Tabelle 2. Beispiel 1" caption-side="top"} 


**Beispiel 2**

Die durchschnittliche Containeranzahl lautet wie folgt: 

| Stunde     | Anzahl der Container | Beschreibung                                                                   | Wird ein Alert generiert? |
|----------|----------------------|-------------------------------------------------------------------------------|------------------------|
| 10:00    | 15                   | Die Kategorie wird auf **Basic** festgelegt.                                                     | Nein                     |
| 11:00    | 19                   | Die Kategorie wird auf **Basic** festgelegt.                                                     | Nein                     |
| 12:00    | 20                   | Die Kategorie wird auf **Basic** festgelegt.                                                     | Nein                    |
| 13:00    | 21                   | Anzahl der Container befindet sich über der Kategorie *Basic*. Die Kategorie verschiebt sich zu **Pro**.            | Ja                     |
{: caption="Tabelle 3. Beispiel 2" caption-side="top"}


**Beispiel 3**

Die durchschnittliche Containeranzahl lautet wie folgt: 

| Stunde     | Anzahl der Container | Beschreibung                                                                   | Wird ein Alert generiert? |
|----------|----------------------|-------------------------------------------------------------------------------|------------------------|
| 10:00    | 15                   | Die Kategorie wird auf **Basic** festgelegt.                                                     | Nein                     |
| 11:00    | 20                   | Die Kategorie wird auf **Basic** festgelegt.                                                     | Nein                    |
| 12:00    | 21                   | Die Kategorie wird auf **Basic** festgelegt.                                                     | Ja                    |
| 13:00    | 20                   | Die Anzahl der Container befindet sich wieder in der Kategorie *Basic*. Die Kategorie verschiebt sich zu **Pro**.          | Nein                     |
{: caption="Tabelle 3. Beispiel 3" caption-side="top"}



