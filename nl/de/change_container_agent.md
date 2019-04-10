---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-18"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# Container-Sysdig-Agenten anpassen
{: #change_container_agent}

In {{site.data.keyword.mon_full_notm}} können Sie die Konfiguration des Sysdig-Agenten anpassen, um eine Protokollebene festzulegen, Ports zu blockieren, Metrikdaten ein- und auszuschließen, Ereignisse hinzuzufügen oder zu entfernen und Container zu filtern. 
{:shortdesc}


## Die Dragent-YAML-Datei bearbeiten
{: #change_container_agent_edit_config}

Die yaml-Datei befindet sich im Verzeichnis */opt/draios/etc/*.

Führen Sie die folgenden Schritte aus, um die Datei zu bearbeiten und die Änderungen anzuwenden:

1. Greifen Sie direkt auf *dragent.yaml* unter `/opt/draios/etc/dragent.yaml` zu.
2. Bearbeiten Sie die Datei. Verwenden Sie die gültige YAML-Syntax.
3. Starten Sie den Agenten neu. Führen Sie den folgenden Befehl aus:

    ```
    docker restart sysdig-agent
    ```
    {: codeblock}



## Ports blockieren
{: #change_container_agent_block_ports}

Um den Netzverkehr und die Metriken von Netzports zu blockieren, müssen Sie den Abschnitt **blacklisted_ports** in der Datei *dragent.yaml* anpassen. Sie müssen die Ports auflisten, aus denen Sie Daten herausfiltern möchten.

**Hinweis:** Port 53 (DNS) ist immer in der Blacklist aufgeführt. 

Das folgende Beispiel zeigt, wie der Abschnitt *blacklisted_ports* eines Sysdig-Agenten festgelegt wird, um Daten aus den Ports 6666 und 6379 auszuschließen:

```
blacklisted_ports:
    - 6666
    - 6379
```
{: screen}



## Eine Gruppe von Docker-Ereignissen erfassen
{: #change_container_agent_collect_docker_events}

{{site.data.keyword.mon_full_notm}} unterstützt die Ereignisintegration mit Docker. Sysdig-Agenten erkennen Docker-Quellen automatisch und erfassen ihre Ereignisdaten. Sie können die Agentenkonfigurationsdatei bearbeiten, um ihr Standardverhalten zu ändern und Ereignisdaten ein- oder auszuschließen. 

Standardmäßig wird nur eine begrenzte Gruppe von Ereignissen erfasst. In der Standardkonfigurationsdatei */opt/draios/etc/dragent.default.yaml* sind die Ereignisse enthalten, die erfasst werden. Weitere Informationen zu den Ereignissen, die standardmäßig erfasst werden, finden Sie unter [Docker-Ereignisse ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://sysdigdocs.atlassian.net/wiki/spaces/Platform/pages/234356795/Enable+Disable+Event+Data#Enable/DisableEventData-DockerEvents){:new_window}.

Wenn Sie Ereignisse hinzufügen oder entfernen möchten, müssen Sie die Datei *dragent.yaml* anpassen und angeben, welche Ereignisse eingeschlossen und welche herausgefiltert werden sollen. **Hinweis:** Ein Eintrag im Abschnitt *dragent.yaml* überschreibt den gesamten Abschnitt in der Standardkonfiguration.
{: tip}

Wenn Sie z. B. Docker-Image-Ereignisse herausfiltern und nur Ereignisse für Zuordnungs-, Festschreibungs- und Kopieraktionen erfassen möchten, müssen Sie den Abschnitt *docker* wie folgt festlegen:

* Option 1: Definieren Sie die Reihenfolge der Einträge in Form von Listenpunkten:

    ```
    events:
      docker:
        image: none
        container:
          - attach
          - commit
          - copy
    ```
    {: codeblock}

* Option 2: Definieren Sie die Reihenfolge der Einträge in einer Zeile in eckigen Klammern:

    ```
    events:
      docker:
        image: none
        container: [attach, commit, copy]
    ```
    {: codeblock}


## Sammlung von Ereignissen inaktivieren
{: #change_container_agent_disable_events}

Um einen Sysdig-Agenten für die Erfassung von Ereignissen zu inaktivieren, müssen Sie die Datei *dragent.default.yaml* ändern. Legen Sie den Abschnitt **events** auf *none* in der Datei *dragent.yaml* fest.

Wenn Sie z. B. Docker-Ereignisse herausfiltern möchten, müssen Sie den Abschnitt *events* in der Datei *dragent.yaml* wie folgt festlegen:

```
events:
  docker: none
```
{: codeblock}



## Ereignisse nach Priorität filtern
{: #change_container_agent_filterby_severity}

Wenn Sie Ereignisse nach Priorität filtern möchten, können Sie auch den Protokolleintragstyp für Ereignisse in der Datei *dragent.yaml* ändern. 

Die Standardprotokollebene ist **Information**. Dies bedeutet, dass nur Warnungen und Ereignisse mit höherer Priorität übertragen werden.

Gültige Werte: *Notfall*, *Alert*, *Kritisch*, *Fehler*, *Warnung*, *Hinweis*, *Information*, *Debug* und *Keine*. **Hinweis**: Die Werte werden in der Reihenfolge von hoher Priorität bis niedriger Priorität aufgelistet.

Wenn Sie z. B. Ereignisse mit niedriger Priorität (*Hinweis*, *Informationen*, *Debug*) herausfiltern möchten, müssen Sie den Protokollabschnitt **event_priority** auf *Warnung* festlegen:

```
log:
  event_priority: warning
```
{: codeblock}


Wenn Sie die Erfassung von Ereignissen blockieren möchten, müssen Sie den Protokollabschnitt **event_priority** auf *none* festlegen:

```
log:
  event_priority: none
```
{: codeblock}




## Metriken einschließen und ausschließen
{: #change_container_agent_inc_exc_metrics}

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
{: #change_container_agent_log_level}

Um die Protokollebene zu konfigurieren, müssen Sie den Abschnitt **log** in der Datei *dragent.yaml* anpassen. 

Der Sysdig-Agent generiert Protokolleinträge in */opt/draios/logs/draios.log*. 
* Die Protokolldatei wird gewechselt, wenn sie 10 MB groß ist.
* Die 10 letzten Protokolldateien werden beibehalten. Die Datumszeitmarke, die an den Dateinamen angehängt wird, wird verwendet, um zu bestimmen, welche Dateien beibehalten werden sollen.
* Gültige Protokollebenen sind: *Keine*, *Fehler*, *Warnung*, *Info*, *Debug*, *Trace*.
* Die Standardprotokollebene ist *Info*, wobei ein Eintrag für jede zusammengefasste Metrikübertragung zu den Back-End-Servern einmal pro Sekunde zusätzlich zu den Einträgen für Warnungen und Fehler erstellt wird.
* Sie können den Typ des Protokolls und die Einträge anpassen, die durch die Konfiguration der Sysdig-Agentenkonfigurationsdatei **/opt/draios/etc/dragent.yaml** erfasst werden. Nachdem Sie die Datei bearbeitet haben, müssen Sie den Agenten in der Shell mit `docker restart sysdig-agent` neu starten, um die Änderungen zu aktivieren.

| Anwendungsfälle                                     | Protokollabschnittseintrag           |
|-----------------------------------------------|-----------------------------|
| Fehlerbehebung beim Agentenverhalten                   | `file_priority: debug`      |
| Container-Konsolenausgabe reduzieren               | `console_priority: warning` |
| Ereignisse nach Priorität filtern                  | `event_priority: warning`   |
| Überprüfung, welche Metriken eingeschlossen oder ausgeschlossen sind  | `metrics_excess_log: true`  |
{: caption="Tabelle 2. Protokollabschnittseinträge" caption-side="top"} 


