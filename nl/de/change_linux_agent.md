---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, customize, linux agent

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

# Linux-Sysdig-Agenten anpassen
{: #change_linux_agent}

Der Sysdig-Agent erfasst standardmäßig Daten aus einer Reihe von Plattformen und Anwendungen. Sie können die Agentenkonfigurationsdatei bearbeiten, um ihr Standardverhalten zu ändern und Daten ein- oder auszuschließen. Sie können die Sysdig-Agentenkonfigurationsdatei anpassen, um angepasste Metriken einzuschließen, wie z. B. JMX, StatsD und Prometheus. Sie können Metriken und Container auch herausfiltern.
{:shortdesc}

Der Sysdig-Agent verwendet zwei Konfigurationsdateien, die angeben, welche Daten automatisch erfasst werden sollen:

| Datei                   | Beschreibung                                                     | Position                                |
|------------------------|-----------------------------------------------------------------|-----------------------------------------|
| `dragent.default.yaml` | Hauptkonfigurationsdatei </br>**Hinweis:**** Bearbeiten Sie diese Datei nicht. | `/opt/draios/etc/dragent.default.yaml`  |
| `dragent.yaml`         | Die Konfigurationsdatei, die Sie bearbeiten, um den Sysdig-Agenten anzupassen. | `/opt/draios/etc/dragent.yaml`          |
{: caption="Tabelle 1. Sysdig-Agentenkonfigurationsdateien" caption-side="top"} 

Sie können die Datei *dragent.yaml* bearbeiten, um die erfassten Daten anzupassen. Die Änderungen werden sofort wirksam, nachdem Sie die Datei gespeichert haben. Der Agent erkennt die Änderung und wird automatisch erneut gestartet. Die Häufigkeit und die Dateien, die ein Sysdig-Agent überprüft, finden Sie in der Datei *dragent.default.yaml*.

Die Datei *dragent.default.yaml* enthält zum Beispiel die folgenden Informationen:

```
check_frequency_s: 5
files:
- /opt/draios/etc/dragent.yaml
- /opt/draios/etc/kubernetes/config/dragent.yaml
- /opt/draios/etc/kubernetes/secrets/access-key
```
{: screen}



## Die Dragent-YAML-Datei bearbeiten
{: #change_linux_agent_edit_agent}

Die yaml-Datei befindet sich im Verzeichnis */opt/draios/etc/*.

Führen Sie die folgenden Schritte aus, um die Datei zu bearbeiten und die Änderungen anzuwenden:

1. Greifen Sie direkt auf die *dragent.yaml* zu. Die Datei befindet sich im Verzeichnis `/opt/draios/etc/dragent.yaml`.
2. Bearbeiten Sie die Datei. Verwenden Sie die gültige YAML-Syntax.
3. Starten Sie den Agenten neu. Führen Sie den folgenden Befehl aus:

    ```
    service dragent restart
    ```
    {: codeblock}


## Ports blockieren
{: #change_linux_agent_block_ports}

Um den Netzverkehr und die Metriken von Netzports zu blockieren, müssen Sie den Abschnitt **blacklisted_ports** in der Datei *dragent.yaml* anpassen. Sie müssen die Ports auflisten, aus denen Sie Daten herausfiltern möchten.

**Hinweis:** Port 53 (DNS) ist immer in der Blacklist aufgeführt. 

Das folgende Beispiel zeigt, wie der Abschnitt *blacklisted_ports* eines Sysdig-Agenten festgelegt wird, um Daten aus den Ports 6666 und 6379 auszuschließen:

```
blacklisted_ports:
    - 6666
    - 6379
```
{: screen}

## Metriken einschließen und ausschließen
{: #change_linux_agent_inc_exc_metrics}

Zum Filtern angepasster Metriken müssen Sie den Abschnitt **metrics_filter** in der Datei *dragent.yaml* anpassen. Sie können angeben, welche Metriken eingeschlossen und welche herausgefiltert werden sollen, indem Sie die Filterparameter **include** und **exclude** konfigurieren.

**Hinweis:** Die Reihenfolge der Filterregeln wird wie folgt festgelegt: Die erste Regel, die mit einer Metrik übereinstimmt, wird angewendet.

Wenn der Abschnitt *metrics_filter* eines Sysdig-Agenten z. B. wie folgt aussieht:

```
metrics_filter:
  - include: metricA.*
  - exclude: metricA.*
  - include: metricB.*
  - include: haproxy.backend.*
  - exclude: haproxy.*
  - exclude: metricC.*
```
{: screen}

* Sie konfigurieren den Sysdig-Agenten, um alle Daten von Metriken zu erfassen, die mit *metricA*, *metricB* und *haproxy.backend* beginnen. 
* Sie filtern Metriken heraus, die mit *metricC* beginnen, und andere Metriken, die mit *haproxy* beginnen. 
* Der Eintrag `exclude: metricA.*` wird ignoriert.


## Die Protokollebene ändern
{: #change_linux_agent_log_level}

Um die Protokollebene zu konfigurieren, müssen Sie den Abschnitt **log** in der Datei *dragent.yaml* anpassen. 

Der Sysdig-Agent generiert Protokolleinträge in */opt/draios/logs/draios.log*. 
* Die Protokolldatei wird gewechselt, wenn sie 10 MB groß ist.
* Die 10 letzten Protokolldateien werden beibehalten. Die Datumszeitmarke, die an den Dateinamen angehängt wird, wird verwendet, um zu bestimmen, welche Dateien beibehalten werden sollen.
* Gültige Protokollebenen sind: *Keine*, *Fehler*, *Warnung*, *Info*, *Debug*, *Trace*.
* Die Standardprotokollebene ist *Info*, wobei ein Eintrag für jede zusammengefasste Metrikübertragung zu den Back-End-Servern einmal pro Sekunde zusätzlich zu den Einträgen für Warnungen und Fehler erstellt wird.
* Sie können den Typ des Protokolls und die Einträge anpassen, die durch die Konfiguration der Sysdig-Agentenkonfigurationsdatei **/opt/draios/etc/dragent.yaml** erfasst werden. Nachdem Sie die Datei bearbeitet haben, müssen Sie den Agenten in der Shell mit `service dragent restart` neu starten, um die Änderungen zu aktivieren.

| Anwendungsfälle                                     | Protokollabschnittseintrag           |
|-----------------------------------------------|-----------------------------|
| Fehlerbehebung beim Agentenverhalten                   | `file_priority: debug`      |
| Container-Konsolenausgabe reduzieren               | `console_priority: warning` |
| Ereignisse nach Priorität filtern                  | `event_priority: warning`   |
| Überprüfung, welche Metriken eingeschlossen oder ausgeschlossen sind  | `metrics_excess_log: true`  |
{: caption="Tabelle 2. Protokollabschnittseinträge" caption-side="top"} 
