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

# Den Sysdig-Agenten anpassen, um Daten zu steuern
{: #customize_agent}

Der Sysdig-Agent erfasst standardmäßig Daten aus einer Reihe von Plattformen und Anwendungen. Sie können die Agentenkonfigurationsdatei bearbeiten, um ihr Standardverhalten zu ändern und Daten ein- oder auszuschließen. Sie können die Sysdig-Agentenkonfigurationsdatei anpassen, um angepasste Metriken einzuschließen, wie z. B. JMX, StatsD und Prometheus. Sie können Metriken, Ereignisdaten und Container auch herausfiltern.
{:shortdesc}

## Den Kubernetes-Sysdig-Agenten anpassen
{: #kube}

Der Kubernetes-Sysdig-Agent verwendet zwei Konfigurationsdateien, die angeben, welche Daten automatisch erfasst werden sollen:

| Dateiname                        | Aktionen           |
|----------------------------------|-------------------|
| `sysdig-agent-daemonset-v2.yaml` | Ändern Sie die Protokollebene. |
| `sysdig-agent-configmap.yaml`    | Blockieren Sie Ports. </br>Schließen Sie Metrikdaten ein oder aus. </br>Fügen Sie Ereignisse hinzu oder entfernen Sie sie. </br>Filtern Sie Container heraus. |
{: caption="Tabelle 1. Kubernetes-Sysdig-Agentenkonfigurationsdateien" caption-side="top"} 

Wenn Sie einen Kubernetes-Sysdig-Agenten bearbeiten möchten, müssen Sie möglicherweise die Datei *sysdig-agent-configmap.yaml* oder *sysdig-agent-daemonset-v2.yaml* oder beide Dateien bearbeiten.

Es gibt zwei Methoden, mit denen Sie eine Konfigurationsdatei ändern können:
* Methode 1: Ändern Sie die Datei direkt in dem Cluster, in dem der Agent ausgeführt wird. Weitere Informationen hierzu finden Sie im Abschnitt [Konfiguration des Kubernetes-Sysdig-Agenten durch Verwendung von "kubectl edit" bearbeiten](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_edit_kube_agent_method1).
* Methode 2: Ändern Sie die Datei lokal und wenden Sie die Änderungen auf den Cluster an. Weitere Informationen hierzu finden Sie im Abschnitt [Konfiguration des Kubernetes-Sysdig-Agenten durch Verwendung von "kubectl apply" bearbeiten](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_edit_kube_agent_method2).

Sie können den Daten, die vom Agenten erfasst werden, Tags hinzufügen. 
* Verwenden Sie diese Tags, um die Daten zu verwalten, die Sie überwachen. 

    * Verwenden Sie Bezeichnungen, um Infrastrukturressourcen in logische Hierarchien zu gruppieren, Daten herauszufiltern und zusammengefasste Daten in Segmente aufzuteilen. 
    
    * Passen Sie an, wie Daten aggregiert werden, wenn Sie ein Diagramm konfigurieren oder einen Alert für eine Metrik erstellen. 
    
    * Legen Sie den Geltungsbereich eines Dashboards, einer Anzeige oder eines Alerts fest, um Datenpunkte zu filtern. 
    
    * Beschränkten Sie den Zugriff auf Daten, indem der Datenzugriff der Benutzer durch die Teams verwaltet wird. 
    
    * Weitere Informationen zum Verwalten von Daten finden Sie im Abschnitt [Daten verwalten](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-manage#manage).

* Weitere Informationen zum Hinzufügen von Tags finden Sie unter [Weitere Tags zu Daten hinzufügen, die von einem Kubernetes-Sysdig-Agenten erfasst werden](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_add_tags). 


**Sie können die Daten anpassen, die vom Sysdig-Agenten erfasst werden.** 

Wenn Sie Ereignisse, Metriken und Container ausschließen, beachten Sie die folgenden Informationen:
* Sie reduzieren die Agent- und Back-End-Auslastung.
* Es werden nur Daten aus Containern erfasst, die Sie überwachen wollen.
* Sie können die Kosten steuern, indem Sie Berichte über wichtige Container erstellen und nicht benötigte oder unkritische Container herausfiltern.
* Sie können die Kubernetes-Ereignisse konfigurieren, die Sie überwachen wollen. Weitere Informationen finden Sie im Abschnitt [Eine Gruppe von Kubernetes-Ereignissen erfassen](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_collect_events).

In der folgenden Liste werden Aktionen aufgeführt, die Sie ausführen können, um die Daten zu steuern, die vom Sysdig-Agenten erfasst werden:
* [Sammlung von Ereignissen inaktivieren](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_disable_events)
* [Metriken einschließen und ausschließen](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_inc_exc_metrics)
* [Kubernetes-Objekte und -Container filtern, aus denen Daten erfasst werden](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_filter_data)
* [Ports blockieren](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_block_ports)
* [Kubernetes-Ereignisse nach Priorität filtern](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_filterby_severity)

Sie können den Typ des Protokolls und die Einträge, die ebenfalls erfasst werden, anpassen. Weitere Informationen finden Sie in [Protokollebene ändern](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_log_level).

Sie können auch die Liste der Metriken protokollieren, für die der Agent Daten aufzeichnet. Weitere Informationen finden Sie im Abschnitt [Protokollierung in einer Datei, welche Metriken eingeschlossen oder ausgeschlossen sind](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_log_metrics).

Der Sysdig-Agent generiert Protokolleinträge in */opt/draios/logs/draios.log*. 
* Die Protokolldatei wird gewechselt, wenn sie 10 MB groß ist.
* Die 10 letzten Protokolldateien werden beibehalten. Die Datumszeitmarke, die an den Dateinamen angehängt wird, wird verwendet, um zu bestimmen, welche Dateien beibehalten werden sollen.
* Gültige Protokollebenen sind: *Keine*, *Fehler*, *Warnung*, *Info*, *Debug*, *Trace*.
* Die Standardprotokollebene ist *Info*, wobei ein Eintrag für jede zusammengefasste Metrikübertragung zu den Back-End-Servern einmal pro Sekunde zusätzlich zu den Einträgen für Warnungen und Fehler erstellt wird.

In der folgenden Tabelle werden einige allgemeine Szenarios und der Wert aufgeführt, den Sie in den einzelnen Tabellen festlegen müssen:

| Anwendungsfälle                                     | Protokollabschnittseintrag           |
|-----------------------------------------------|-----------------------------|
| Fehlerbehebung beim Agentenverhalten                   | `file_priority: debug`      |
| Container-Konsolenausgabe reduzieren               | `console_priority: warning` |
| Ereignisse nach Priorität filtern                  | `event_priority: warning`   |
| Überprüfung, welche Metriken eingeschlossen oder ausgeschlossen sind  | `metrics_excess_log: true`  |

## Container-Sysdig-Agent
{: #container}


In der folgenden Liste werden Aktionen aufgeführt, die Sie ausführen können, um die Daten zu steuern, die vom Sysdig-Agenten erfasst werden:
* [Sammlung von Ereignissen inaktivieren](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_disable_events)
* [Metriken einschließen und ausschließen](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_inc_exc_metrics)
* [Container filtern, aus denen Daten erfasst werden](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_collect_docker_events)
* [Ports blockieren](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_block_ports)
* [Ereignisse nach Priorität filtern](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_filterby_severity)

Sie können den Typ des Protokolls und die Einträge, die ebenfalls erfasst werden, anpassen. Weitere Informationen finden Sie in [Protokollebene ändern](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_log_level).



## Linux-Sysdig-Agent
{: #linux}

Der Linux-Sysdig-Agent verwendet zwei Konfigurationsdateien, die angeben, welche Daten automatisch erfasst werden sollen:

| Datei                   | Beschreibung                                                     | Standort                                |
|------------------------|-----------------------------------------------------------------|-----------------------------------------|
| `dragent.default.yaml` | Hauptkonfigurationsdatei </br>**Hinweis:****Bearbeiten Sie diese Datei nicht.  | `/opt/draios/etc/dragent.default.yaml`  |
| `dragent.yaml`         | Die Konfigurationsdatei, die Sie bearbeiten, um den Sysdig-Agenten anzupassen. | `/opt/draios/etc/dragent.yaml`          |
{: caption="Tabelle 1. Sysdig-Agentenkonfigurationsdateien" caption-side="top"} 

Sie können die Datei *dragent.yaml* bearbeiten, um die erfassten Daten anzupassen. Die Änderungen werden sofort wirksam, nachdem Sie die Datei gespeichert haben. Der Agent erkennt die Änderung und wird automatisch erneut gestartet. Die Häufigkeit und die Dateien, die ein Sysdig-Agent überprüft, finden Sie in der Datei *dragent.default.yaml*. Weitere Informationen hierzu finden Sie im Abschnitt [Die Dragent-YAML-Datei bearbeiten](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_linux_agent#change_linux_agent_edit_agent).

Die Datei *dragent.default.yaml* enthält zum Beispiel die folgenden Informationen:

```
check_frequency_s: 5
files:
- /opt/draios/etc/dragent.yaml
- /opt/draios/etc/kubernetes/config/dragent.yaml
- /opt/draios/etc/kubernetes/secrets/access-key
```
{: screen}

In der folgenden Liste werden Aktionen aufgeführt, die Sie ausführen können, um die Daten zu steuern, die vom Sysdig-Agenten erfasst werden:
* [Metriken einschließen und ausschließen](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_linux_agent#change_linux_agent_inc_exc_metrics)
* [Ports blockieren](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_linux_agent#change_linux_agent_block_ports)

Sie können den Typ des Protokolls und die Einträge, die ebenfalls erfasst werden, anpassen. Weitere Informationen finden Sie in [Protokollebene ändern](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_linux_agent#change_linux_agent_log_level).


