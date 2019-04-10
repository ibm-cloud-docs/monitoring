---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, customize, kubernetes agent

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

# Kubernetes-Sysdig-Agenten anpassen
{: #change_kube_agent}

In {{site.data.keyword.mon_full_notm}} können Sie die Konfiguration des Sysdig-Agenten anpassen, um eine Protokollebene festzulegen, Ports zu blockieren, Metrikdaten ein- und auszuschließen, Ereignisse hinzuzufügen oder zu entfernen und Container zu filtern. 
{:shortdesc}

Wenn Sie einen Kubernetes-Sysdig-Agenten anpassen möchten, müssen Sie möglicherweise Abschnitte in einer der folgenden Dateien konfigurieren:

| Dateiname                        | Aktionen       |
|----------------------------------|-------------------|
| `sysdig-agent-daemonset-v2.yaml` | Ändern Sie die Protokollebene. |
| `sysdig-agent-configmap.yaml`    | Blockieren Sie Ports. </br>Schließen Sie Metrikdaten ein oder aus. </br>Fügen Sie Ereignisse hinzu oder entfernen Sie sie. </br>Filtern Sie Container heraus. |
{: caption="Tabelle 1. Kubernetes-Sysdig-Agentenkonfigurationsdateien" caption-side="top"} 

Wenn Sie einen Kubernetes-Sysdig-Agenten bearbeiten möchten, müssen Sie möglicherweise die Datei *sysdig-agent-configmap.yaml* oder *sysdig-agent-daemonset-v2.yaml* oder beide Dateien bearbeiten.
{: tip}

Es gibt zwei Methoden, mit denen Sie eine Konfigurationsdatei ändern können:
* Methode 1: Ändern Sie die Datei direkt in dem Cluster, in dem der Agent ausgeführt wird.
* Methode 2: Ändern Sie die Datei lokal und wenden Sie die Änderungen auf den Cluster an.

## Konfiguration des Kubernetes-Sysdig-Agenten durch Verwendung von "kubectl edit" bearbeiten
{: #change_kube_agent_edit_kube_agent_method1}

Führen Sie die folgenden Schritte aus, um eine Konfiguration des Kubernetes-Sysdig-Agenten zu bearbeiten:

1. Richten Sie die Clusterumgebung ein. Führen Sie die folgenden Befehle aus:

    Verwenden Sie zuerst den Befehl zum Festlegen der Umgebungsvariablen und zum Herunterladen der Kubernetes-Konfigurationsdateien.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Wenn der Download der Konfigurationsdateien abgeschlossen ist, wird ein Befehl angezeigt, mit dem Sie den Pfad zur lokalen Kubernetes-Konfigurationsdatei als Umgebungsvariable festlegen können.

    Kopieren Sie dann den in Ihrem Terminal angezeigten Befehl und fügen Sie ihn ein, um die Umgebungsvariable KUBECONFIG festzulegen.

    **Hinweis:** Jedes Mal, wenn Sie sich an der {{site.data.keyword.containerlong}}-CLI für die Arbeit mit Clustern anmelden, müssen Sie diese Befehle ausführen, um den Pfad zur Konfigurationsdatei des Clusters als Sitzungsvariable zu definieren. Die Kubernetes-CLI verwendet diese Variable, um eine lokale Konfigurationsdatei und Zertifikate zu finden, die für die Verbindung mit dem Cluster in {{site.data.keyword.cloud_notm}} erforderlich sind.

2. Bearbeiten Sie die Datei *sysdig-agent-configmap.yaml*. 

    Führen Sie den folgenden Befehl aus:

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

    Nehmen Sie Änderungen vor. **Hinweis:** Weitere Informationen, wie Sie Änderungen vornehmen können, erhalten Sie in den `vi`-Editor-Anweisungen.

    Speichern Sie die Änderungen. Die Änderungen werden automatisch angewendet. 

3. Bearbeiten Sie die Datei *sysdig-agent-daemonset-v2.yaml*. 

    Führen Sie den folgenden Befehl aus: 

    ```
    kubectl edit daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

    Nehmen Sie Änderungen vor. **Hinweis:** Weitere Informationen, wie Sie Änderungen vornehmen können, erhalten Sie in den `vi`-Editor-Anweisungen.

    Speichern Sie die Änderungen. Die Änderungen werden automatisch angewendet.

## Konfiguration des Kubernetes-Sysdig-Agenten durch Verwendung von "kubectl apply" bearbeiten
{: #change_kube_agent_edit_kube_agent_method2}

Verwenden Sie diese Methode, wenn die yaml-Konfigurationsdateien in einem System zur Quellcodeverwaltung gespeichert und verwaltet werden.

Führen Sie die folgenden Schritte aus, um eine Konfiguration des Kubernetes-Sysdig-Agenten zu bearbeiten:

1. Rufen Sie die neueste Kopie jeder Datei vom Quellencontroller ab. 

    Um eine lokale Datei mit der Konfiguration zu erstellen, die in einem Cluster implementiert ist, können Sie auch den folgenden Befehl ausführen:
    
    ```
    kubectl get configmap sysdig-agent -n=ibm-observe -o=yaml > prod-sysdig-agent-configmap.yaml
    ```
    {: codeblock} 
    
    oder 
    
    ```
    kubectl get daemonset sysdig-agent -n=ibm-observe -o=yaml > prod-sysdig-agent-daemonset-v2.yaml
    ```
    {: codeblock}

2. Bearbeiten Sie die Konfiguration.

3. Wenden Sie die Änderungen mit den folgenden Befehlen an:

    ```
    kubectl apply -f sysdig-agent-configmap.yaml
    ```
    {: codeblock}
    
    oder
    
    ```
    kubectl apply -f sysdig-agent-daemonset-v2.yaml
    ```
    {: codeblock}

Aktive Agenten wählen die neue Konfiguration automatisch aus, nachdem Kubernetes die Änderungen mit einer Push-Operation auf alle Knoten im Cluster übertragen hat.


## Weitere Tags zu Daten hinzufügen, die von einem Kubernetes-Sysdig-Agenten erfasst werden
{: #change_kube_agent_add_tags}

Führen Sie die folgenden Schritte aus, um einer bereits bereitgestellten Konfiguration eines Kubernetes-Sysdig-Agenten weitere Tags hinzuzufügen:

1. Richten Sie die Clusterumgebung ein. Führen Sie die folgenden Befehle aus:

    Verwenden Sie zuerst den Befehl zum Festlegen der Umgebungsvariablen und zum Herunterladen der Kubernetes-Konfigurationsdateien.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Wenn der Download der Konfigurationsdateien abgeschlossen ist, wird ein Befehl angezeigt, mit dem Sie den Pfad zur lokalen Kubernetes-Konfigurationsdatei als Umgebungsvariable festlegen können.

    Kopieren Sie dann den in Ihrem Terminal angezeigten Befehl und fügen Sie ihn ein, um die Umgebungsvariable KUBECONFIG festzulegen.

    **Hinweis:** Jedes Mal, wenn Sie sich an der {{site.data.keyword.containerlong}}-CLI für die Arbeit mit Clustern anmelden, müssen Sie diese Befehle ausführen, um den Pfad zur Konfigurationsdatei des Clusters als Sitzungsvariable zu definieren. Die Kubernetes-CLI verwendet diese Variable, um eine lokale Konfigurationsdatei und Zertifikate zu finden, die für die Verbindung mit dem Cluster in {{site.data.keyword.cloud_notm}} erforderlich sind.

2. Bearbeiten Sie die Datei *sysdig-agent-configmap.yaml*. 

    Führen Sie den folgenden Befehl aus:

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Nehmen Sie Änderungen vor. **Hinweis:** Weitere Informationen, wie Sie Änderungen vornehmen können, erhalten Sie in den `vi`-Editor-Anweisungen.

    ```
    apiVersion: v1
      data:
        dragent.yaml: |
            k8s_cluster_name: marisa-production
            collector: ingest.us-south.monitoring.cloud.ibm.com
            collector_port: 6443
            ssl: true
            sysdig_capture_enabled: false
            new_k8s: true
            tags: department:finance,region:us-south
      ...
    ```
    {: codeblock}

4. Speichern Sie die Änderungen. 

Die Änderungen werden automatisch angewendet. 

In diesem angegebenen Beispiel erhalten Sie die Tags **agent.tag.cluster_version** und **agent.tag.region**. Sie können sie verwenden, um Alerts zu definieren, Geltungsbereich anzupassen usw.



## Eine Gruppe von Kubernetes-Ereignissen erfassen
{: #change_kube_agent_collect_events}

{{site.data.keyword.mon_full_notm}} unterstützt Ereignisintegrationen mit Kubernetes. Sysdig-Agenten erkennen diese Services automatisch und erfassen Ereignisdaten von ihnen. Sie können die Agentenkonfigurationsdatei bearbeiten, um ihr Standardverhalten zu ändern und Ereignisdaten ein- oder auszuschließen. 

Standardmäßig wird nur eine begrenzte Gruppe von Ereignissen erfasst. Weitere Informationen zu den Ereignissen, die standardmäßig erfasst werden, finden Sie unter [Kubernetes-Ereignisse ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://sysdigdocs.atlassian.net/wiki/spaces/Platform/pages/234356795/Enable+Disable+Event+Data#Enable/DisableEventData-KubernetesEvents){:new_window}.

Wenn Sie Ereignisse hinzufügen oder entfernen möchten, müssen Sie die Datei *sysdig-agent-configmap.yaml* anpassen und angeben, welche Ereignisse eingeschlossen und welche herausgefiltert werden sollen. **Hinweis:** Ein Eintrag im Abschnitt *sysdig-agent-configmap.yaml* überschreibt den gesamten Abschnitt in der Standardkonfiguration.
{: tip}

Führen Sie die folgenden Schritte aus, um Ereignisse aus Kubernetes-Pods zu filtern:

1. Richten Sie die Clusterumgebung ein. Führen Sie die folgenden Befehle aus:

    Verwenden Sie zuerst den Befehl zum Festlegen der Umgebungsvariablen und zum Herunterladen der Kubernetes-Konfigurationsdateien.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Wenn der Download der Konfigurationsdateien abgeschlossen ist, wird ein Befehl angezeigt, mit dem Sie den Pfad zur lokalen Kubernetes-Konfigurationsdatei als Umgebungsvariable festlegen können.

    Kopieren Sie dann den in Ihrem Terminal angezeigten Befehl und fügen Sie ihn ein, um die Umgebungsvariable KUBECONFIG festzulegen.

    **Hinweis:** Jedes Mal, wenn Sie sich an der {{site.data.keyword.containerlong}}-CLI für die Arbeit mit Clustern anmelden, müssen Sie diese Befehle ausführen, um den Pfad zur Konfigurationsdatei des Clusters als Sitzungsvariable zu definieren. Die Kubernetes-CLI verwendet diese Variable, um eine lokale Konfigurationsdatei und Zertifikate zu finden, die für die Verbindung mit dem Cluster in {{site.data.keyword.cloud_notm}} erforderlich sind.

2. Bearbeiten Sie die Datei *sysdig-agent-configmap.yaml*. 

    Führen Sie den folgenden Befehl aus:

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Nehmen Sie Änderungen vor. Fügen Sie den Abschnitt *events* hinzu oder aktualisieren Sie den Abschnitt.

    **Hinweis:** Weitere Informationen, wie Sie Änderungen vornehmen können, erhalten Sie in den `vi`-Editor-Anweisungen.

    Beispiel: Sie möchten Kubernetes-Pod-Ereignisse erfassen und andere Pod-Ereignisse herausfiltern, die standardmäßig erfasst werden. Sie möchten aber Standardereignisse für Kubernetes für Knoten und "replicationControllers" erfassen.

    ```
    events:
      kubernetes:
        pod:
          - Pulling
    ```
    {: codeblock}

4. Speichern Sie die Änderungen. 

Die Änderungen werden automatisch angewendet. 


Ein weiteres Beispiel, mit dem Sie erkennen können, wie eine Untergruppe von Kubernetes-Ereignissen erfasst wird: Sie möchten nur die Ereignissen "Pulling", "Pulled" und "Failed" für Pods überwachen.

* Option 1: Definieren Sie die Reihenfolge der Einträge in Form von Listenpunkten:

    ```
    events:
      kubernetes:
        pod: 
          - Pulling
          - Pulled
          - Failed
    ```
    {: codeblock}

* Option 2: Definieren Sie die Reihenfolge der Einträge in einer Zeile in eckigen Klammern:

    ```
    events:
      kubernetes:
        pod: [Pulling, Pulled, Failed]
    ```
    {: codeblock}

Weitere Informationen zum Arbeiten mit angepassten Ereignissen finden Sie im Abschnitt [Mit angepassten Ereignissen arbeiten ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/222822463/Custom+Events){:new_window}.


## Sammlung von Ereignissen inaktivieren
{: #change_kube_agent_disable_events}

Um einen Sysdig-Agenten für die Erfassung von Kubernetes-Ereignissen zu inaktivieren, müssen Sie die Datei *sysdig-agent-configmap.yaml* ändern. Setzen Sie den **Kubernetes**-Eintrag im Abschnitt **events** auf *none*. 

Führen Sie die folgenden Schritte aus:

1. Richten Sie die Clusterumgebung ein. Führen Sie die folgenden Befehle aus:

    Verwenden Sie zuerst den Befehl zum Festlegen der Umgebungsvariablen und zum Herunterladen der Kubernetes-Konfigurationsdateien.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Wenn der Download der Konfigurationsdateien abgeschlossen ist, wird ein Befehl angezeigt, mit dem Sie den Pfad zur lokalen Kubernetes-Konfigurationsdatei als Umgebungsvariable festlegen können.

    Kopieren Sie dann den in Ihrem Terminal angezeigten Befehl und fügen Sie ihn ein, um die Umgebungsvariable KUBECONFIG festzulegen.

    **Hinweis:** Jedes Mal, wenn Sie sich an der {{site.data.keyword.containerlong}}-CLI für die Arbeit mit Clustern anmelden, müssen Sie diese Befehle ausführen, um den Pfad zur Konfigurationsdatei des Clusters als Sitzungsvariable zu definieren. Die Kubernetes-CLI verwendet diese Variable, um eine lokale Konfigurationsdatei und Zertifikate zu finden, die für die Verbindung mit dem Cluster in {{site.data.keyword.cloud_notm}} erforderlich sind.

2. Bearbeiten Sie die Datei *sysdig-agent-configmap.yaml*. 

    Führen Sie den folgenden Befehl aus:

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Nehmen Sie Änderungen vor. Fügen Sie den Abschnitt *events* hinzu oder aktualisieren Sie den Abschnitt.

    ```
    events:
      kubernetes: none
    ```
    {: codeblock}

6. Speichern Sie die Änderungen. 

Die Änderungen werden automatisch angewendet. 






## Metriken einschließen und ausschließen
{: #change_kube_agent_inc_exc_metrics}

Zum Filtern angepasster Metriken müssen Sie den Abschnitt **metrics_filter** in der Datei *sysdig-agent-configmap.yaml* anpassen. Sie können angeben, welche Metriken eingeschlossen und welche herausgefiltert werden sollen, indem Sie die Filterparameter **include** und **exclude** konfigurieren.

<p class="important">Die Reihenfolge der Filterregeln wird wie folgt festgelegt: Die erste Regel, die mit einer Metrik übereinstimmt, wird angewendet. Nachfolgende Regeln für diese Metrik werden ignoriert.</p>

Führen Sie die folgenden Schritte aus:

1. Richten Sie die Clusterumgebung ein. Führen Sie die folgenden Befehle aus:

    Verwenden Sie zuerst den Befehl zum Festlegen der Umgebungsvariablen und zum Herunterladen der Kubernetes-Konfigurationsdateien.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Wenn der Download der Konfigurationsdateien abgeschlossen ist, wird ein Befehl angezeigt, mit dem Sie den Pfad zur lokalen Kubernetes-Konfigurationsdatei als Umgebungsvariable festlegen können.

    Kopieren Sie dann den in Ihrem Terminal angezeigten Befehl und fügen Sie ihn ein, um die Umgebungsvariable KUBECONFIG festzulegen.

    **Hinweis:** Jedes Mal, wenn Sie sich an der {{site.data.keyword.containerlong}}-CLI für die Arbeit mit Clustern anmelden, müssen Sie diese Befehle ausführen, um den Pfad zur Konfigurationsdatei des Clusters als Sitzungsvariable zu definieren. Die Kubernetes-CLI verwendet diese Variable, um eine lokale Konfigurationsdatei und Zertifikate zu finden, die für die Verbindung mit dem Cluster in {{site.data.keyword.cloud_notm}} erforderlich sind.

2. Bearbeiten Sie die Datei *sysdig-agent-configmap.yaml*. 

    Führen Sie den folgenden Befehl aus:

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Nehmen Sie Änderungen vor. Fügen Sie den Abschnitt *metrics_filter* hinzu oder aktualisieren Sie den Abschnitt.

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

4. Speichern Sie die Änderungen. 

Die Änderungen werden automatisch angewendet. 




## Kubernetes-Objekte und -Container filtern, aus denen Daten erfasst werden
{: #change_kube_agent_filter_data}

Ein Kubernetes-Sysdig-Agent erfasst automatisch Metriken von *allen Containern*, die er in einem Cluster erkennt, einschließlich Prometheus, StatsD, JMX, App-Checks und integrierten Metriken.
 
Sie können den Sysdig-Agenten so anpassen, dass Container aus der Metrikerfassung ausgeschlossen werden. 

Wenn Sie Container ausschließen, beachten Sie die folgenden Informationen:
* Sie reduzieren die Agent- und Back-End-Auslastung.
* Es werden nur Daten aus Containern erfasst, die Sie überwachen wollen.
* Sie können die Kosten steuern, indem Sie Berichte über wichtige Container erstellen und nicht benötigte oder unkritische Container herausfiltern.

Um die Funktion zu aktivieren, in der ein Sysdig-Agent Container filtert, müssen Sie die Datei *sysdig-agent-configmap.yaml* anpassen. Legen Sie den Eintrag **use_container_filter** im Abschnitt **containers** auf *true* fest. **Hinweis:** Diese Funktion ist standardmäßig inaktiviert. Definieren Sie anschließend die Regeln, die eine oder mehrere Bedingungen einschließen und die Sie anwenden möchten.

In der folgenden Tabelle sind die Parameter aufgeführt, die Sie definieren können, um die Filterregeln in einem Cluster festzulegen:

| Parameter                          | Bedingung                                      |
|------------------------------------|------------------------------------------------|
| `container.image`                  | Name des Container-Images                           |
| `container.name`                   | Containername                                 |
| `container.label.*`                | Containerbezeichnung                                |
| `kubernetes.object.*`             | Kubernetes-Objekt. Ein Objekt kann ein Pod, ein Namensbereich usw. sein.   |
| `kubernetes.object.annotation.*`  | Hinweis für Kubernetes-Objekt.                   |
| `kubernetes.object.label.*`       | Bezeichnung für Kubernetes-Objekt.                        |
| `all`                              | Standardregel zur Angabe aller Objekte.            |
{: caption="Tabelle 2. Parameter zum Definieren von Bedingungen für Container" caption-side="top"} 

Beachten Sie die folgenden Informationen, wie der Sysdig-Agent die Regeln anwendet, die Sie im Abschnitt **container_filter** definieren:
* Sie definieren Bedingungen, indem Sie sie mit den Filterparametern **include** und **exclude** konfigurieren. 
* Die erste Abgleichsregel in der Liste bestimmt, ob der Container eingeschlossen oder ausgeschlossen ist.
* Die Bedingungen bestehen aus einem Schlüsselnamen und einem Wert. Wenn der angegebene Schlüssel für einen Container mit dem Wert übereinstimmt, wird die Regel angewendet.
* Wenn eine Regel mehrere Bedingungen enthält, müssen `alle Bedingungen` übereinstimmen, damit die Regel angewendet wird.

Führen Sie die folgenden Schritte aus, um Container herauszufiltern, die ein Sysdig-Agent in einem Cluster überwacht:

1. Richten Sie die Clusterumgebung ein. Führen Sie die folgenden Befehle aus:

    Verwenden Sie zuerst den Befehl zum Festlegen der Umgebungsvariablen und zum Herunterladen der Kubernetes-Konfigurationsdateien.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Wenn der Download der Konfigurationsdateien abgeschlossen ist, wird ein Befehl angezeigt, mit dem Sie den Pfad zur lokalen Kubernetes-Konfigurationsdatei als Umgebungsvariable festlegen können.

    Kopieren Sie dann den in Ihrem Terminal angezeigten Befehl und fügen Sie ihn ein, um die Umgebungsvariable KUBECONFIG festzulegen.

    **Hinweis:** Jedes Mal, wenn Sie sich an der {{site.data.keyword.containerlong}}-CLI für die Arbeit mit Clustern anmelden, müssen Sie diese Befehle ausführen, um den Pfad zur Konfigurationsdatei des Clusters als Sitzungsvariable zu definieren. Die Kubernetes-CLI verwendet diese Variable, um eine lokale Konfigurationsdatei und Zertifikate zu finden, die für die Verbindung mit dem Cluster in {{site.data.keyword.cloud_notm}} erforderlich sind.

2. Bearbeiten Sie die Datei *sysdig-agent-configmap.yaml*. 

    Führen Sie den folgenden Befehl aus:

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Nehmen Sie Änderungen vor. Fügen Sie den Abschnitt *metrics_filter* hinzu oder aktualisieren Sie den Abschnitt.

    Sehen Sie sich z. B. den folgenden Auszug einer Konfigurationszuordnung an:

    ```
    containers:
        # Feature aktivieren
        use_container_filter: true
        #
        # Bedingungen einschließen oder ausschließen
        container_filter:
           - include:
                container.image: 
           - include:
                container.name: 
           - exclude:
                kubernetes.namespace.name: kube-system
    ```  
    {: codeblock}

6. Speichern Sie die Änderungen. 

Die Änderungen werden automatisch angewendet. 


## Ports blockieren
{: #change_kube_agent_block_ports}

Um den Netzverkehr und die Metriken von Netzports zu blockieren, müssen Sie den Abschnitt **blacklisted_ports** in der Datei *sysdig-agent-configmap.yaml* anpassen. Sie müssen die Ports auflisten, aus denen Sie Daten herausfiltern möchten.

**Hinweis:** Port 53 (DNS) ist immer in der Blacklist aufgeführt. 

Führen Sie die folgenden Schritte aus:

1. Richten Sie die Clusterumgebung ein. Führen Sie die folgenden Befehle aus:

    Verwenden Sie zuerst den Befehl zum Festlegen der Umgebungsvariablen und zum Herunterladen der Kubernetes-Konfigurationsdateien.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Wenn der Download der Konfigurationsdateien abgeschlossen ist, wird ein Befehl angezeigt, mit dem Sie den Pfad zur lokalen Kubernetes-Konfigurationsdatei als Umgebungsvariable festlegen können.

    Kopieren Sie dann den in Ihrem Terminal angezeigten Befehl und fügen Sie ihn ein, um die Umgebungsvariable KUBECONFIG festzulegen.

    **Hinweis:** Jedes Mal, wenn Sie sich an der {{site.data.keyword.containerlong}}-CLI für die Arbeit mit Clustern anmelden, müssen Sie diese Befehle ausführen, um den Pfad zur Konfigurationsdatei des Clusters als Sitzungsvariable zu definieren. Die Kubernetes-CLI verwendet diese Variable, um eine lokale Konfigurationsdatei und Zertifikate zu finden, die für die Verbindung mit dem Cluster in {{site.data.keyword.cloud_notm}} erforderlich sind.

2. Bearbeiten Sie die Datei *sysdig-agent-configmap.yaml*. 

    Führen Sie den folgenden Befehl aus:

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Nehmen Sie Änderungen vor. Fügen Sie den Abschnitt *metrics_filter* hinzu oder aktualisieren Sie den Abschnitt.

    Das folgende Beispiel zeigt, wie der Abschnitt *blacklisted_ports* eines Sysdig-Agenten festgelegt wird, um Daten aus den Ports 6666 und 6379 auszuschließen:

    ```
    blacklisted_ports:
      - 6666
      - 6379
    ```
    {: screen}

6. Speichern Sie die Änderungen. 

Die Änderungen werden automatisch angewendet. 



## Die Protokollebene ändern
{: #change_kube_agent_log_level}

Um die Protokollebene zu konfigurieren, müssen Sie den Abschnitt **log** in der Datei *sysdig-agent-daemonset-v2.yaml* anpassen. 

Der Sysdig-Agent generiert Protokolleinträge in */opt/draios/logs/draios.log*. 
* Die Protokolldatei wird gewechselt, wenn sie 10 MB groß ist.
* Die 10 letzten Protokolldateien werden beibehalten. Die Datumszeitmarke, die an den Dateinamen angehängt wird, wird verwendet, um zu bestimmen, welche Dateien beibehalten werden sollen.
* Gültige Protokollebenen sind: *Keine*, *Fehler*, *Warnung*, *Info*, *Debug*, *Trace*.
* Die Standardprotokollebene ist *Info*, wobei ein Eintrag für jede zusammengefasste Metrikübertragung zu den Back-End-Servern einmal pro Sekunde zusätzlich zu den Einträgen für Warnungen und Fehler erstellt wird.
* Sie können den Typ des Protokolls und die Einträge anpassen, die durch die Konfiguration der Sysdig-Agentenkonfigurationsdatei **/opt/draios/etc/dragent.yaml** erfasst werden. Nachdem Sie die Datei bearbeitet haben, müssen Sie den Agenten in der Shell mit `service dragent restart` neu starten, um die Änderungen zu aktivieren.

In der folgenden Tabelle werden einige allgemeine Szenarios und der Wert aufgeführt, den Sie in den einzelnen Tabellen festlegen müssen:

| Anwendungsfälle                                     | Protokollabschnittseintrag           |
|-----------------------------------------------|-----------------------------|
| Fehlerbehebung beim Agentenverhalten                   | `file_priority: debug`      |
| Container-Konsolenausgabe reduzieren               | `console_priority: warning` |
| Ereignisse nach Priorität filtern                  | `event_priority: warning`   |
| Überprüfung, welche Metriken eingeschlossen oder ausgeschlossen sind  | `metrics_excess_log: true`  |
{: caption="Tabelle 2. Protokollabschnittseinträge" caption-side="top"} 

Führen Sie die folgenden Schritte aus, um die Protokollebene zu konfigurieren:

1. Richten Sie die Clusterumgebung ein. Führen Sie die folgenden Befehle aus:

    Verwenden Sie zuerst den Befehl zum Festlegen der Umgebungsvariablen und zum Herunterladen der Kubernetes-Konfigurationsdateien.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Wenn der Download der Konfigurationsdateien abgeschlossen ist, wird ein Befehl angezeigt, mit dem Sie den Pfad zur lokalen Kubernetes-Konfigurationsdatei als Umgebungsvariable festlegen können.

    Kopieren Sie dann den in Ihrem Terminal angezeigten Befehl und fügen Sie ihn ein, um die Umgebungsvariable KUBECONFIG festzulegen.

    **Hinweis:** Jedes Mal, wenn Sie sich an der {{site.data.keyword.containerlong}}-CLI für die Arbeit mit Clustern anmelden, müssen Sie diese Befehle ausführen, um den Pfad zur Konfigurationsdatei des Clusters als Sitzungsvariable zu definieren. Die Kubernetes-CLI verwendet diese Variable, um eine lokale Konfigurationsdatei und Zertifikate zu finden, die für die Verbindung mit dem Cluster in {{site.data.keyword.cloud_notm}} erforderlich sind.

2. Bearbeiten Sie die Datei *sysdig-agent-daemonset-v2.yaml*. 

    Führen Sie den folgenden Befehl aus:

    ```
    kubectl edit daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Nehmen Sie Änderungen vor. Fügen Sie den Abschnitt *log* hinzu oder aktualisieren Sie den Abschnitt.

    Wenn Sie z. B. Ereignisse mit niedriger Priorität (*Hinweis*, *Informationen*, *Debug*) herausfiltern möchten, müssen Sie den Eintrag **metrics_excess_log** im Abschnitt **log** auf *true* festlegen:

    ```
    log:
      file_priority: warning
      console_priority: info
      event_priority: warning
      metrics_excess_log: true
    ```
    {: codeblock}

6. Speichern Sie die Änderungen. 

Die Änderungen werden automatisch angewendet. 


## Kubernetes-Ereignisse nach Priorität filtern
{: #change_kube_agent_filterby_severity}

Wenn Sie Ereignisse nach Priorität filtern möchten, müssen Sie die Datei *sysdig-agent-daemonset-v2.yaml* ändern. Legen Sie den Eintrag **event_priority** im Abschnitt **log** auf *none* fest. 

Die Standardprotokollebene ist **Information**. Dies bedeutet, dass nur Warnungen und Ereignisse mit höherer Priorität übertragen werden.

Gültige Werte: *Notfall*, *Alert*, *Kritisch*, *Fehler*, *Warnung*, *Hinweis*, *Information*, *Debug* und *Keine*. **Hinweis**: Die Werte werden in der Reihenfolge von hoher Priorität bis niedriger Priorität aufgelistet.

Führen Sie die folgenden Schritte aus:

1. Richten Sie die Clusterumgebung ein. Führen Sie die folgenden Befehle aus:

    Verwenden Sie zuerst den Befehl zum Festlegen der Umgebungsvariablen und zum Herunterladen der Kubernetes-Konfigurationsdateien.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Wenn der Download der Konfigurationsdateien abgeschlossen ist, wird ein Befehl angezeigt, mit dem Sie den Pfad zur lokalen Kubernetes-Konfigurationsdatei als Umgebungsvariable festlegen können.

    Kopieren Sie dann den in Ihrem Terminal angezeigten Befehl und fügen Sie ihn ein, um die Umgebungsvariable KUBECONFIG festzulegen.

    **Hinweis:** Jedes Mal, wenn Sie sich an der {{site.data.keyword.containerlong}}-CLI für die Arbeit mit Clustern anmelden, müssen Sie diese Befehle ausführen, um den Pfad zur Konfigurationsdatei des Clusters als Sitzungsvariable zu definieren. Die Kubernetes-CLI verwendet diese Variable, um eine lokale Konfigurationsdatei und Zertifikate zu finden, die für die Verbindung mit dem Cluster in {{site.data.keyword.cloud_notm}} erforderlich sind.

2. Bearbeiten Sie die Datei *sysdig-agent-daemonset-v2.yaml*. 

    Führen Sie den folgenden Befehl aus:

    ```
    kubectl edit daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Nehmen Sie Änderungen vor. Fügen Sie den Abschnitt *log* hinzu oder aktualisieren Sie den Abschnitt.

    Wenn Sie z. B. Ereignisse mit niedriger Priorität (*Hinweis*, *Informationen*, *Debug*) herausfiltern möchten, müssen Sie den Protokollabschnitt **event_priority** auf *Warnung* festlegen:

    ```
    log:
      event_priority: warning
    ```
    {: codeblock}

6. Speichern Sie die Änderungen. 

Die Änderungen werden automatisch angewendet. 

## Protokollierung in einer Datei, welche Metriken eingeschlossen oder ausgeschlossen sind
{: #change_kube_agent_log_metrics}

Sie müssen die Datei *sysdig-agent-daemonset-v2.yaml* anpassen, um in einer Datei zu protokollieren, welche angepassten Metriken eingeschlossen und ausgeschlossen sind. Legen Sie den Eintrag **metrics_excess_log** im Abschnitt **Protokoll** auf **true** fest.

* Die Protokollierung ist standardmäßig inaktiviert. 
* Die Protokollierung erfolgt alle 30 Sekunden auf INFO-Ebene und dauert 10 Sekunden. 
* Die Protokolldatei ist in */opt/draios/logs/draios.log* verfügbar.
* Die Protokollierungsdaten werden wie folgt formatiert:

    ```
    +/-[type][metric included/excluded]: metric.name (filter: +/-[metric.filter])
    ```
    {: screen}

    * *+/-* ist ein Symbol, das angibt, ob die Metrik eingeschlossen oder ausgeschlossen ist. Das Pluszeichen (*+*) gibt an, dass eine Metrik eingeschlossen ist. Das Minuszeichen (*-*) gibt an, dass eine Metrik ausgeschlossen ist. 

    * *[ type]* gibt den Metriktyp an, z. B. *statsd*.
    
    * *[metric included/excluded]* gibt auf eine für Menschen lesbare Weise an, ob die Metrik eingeschlossen oder ausgeschlossen ist.

    *  *metric.name* gibt den Metriknamen an.

    * *(filter: +/-[metric.filter])* stellt Informationen zu allen Filtern bereit, die im Abschnitt **metrics_filter** in der Datei *sysdig-agent-daemonset-v2.yaml* definiert sind.

Ein Eintrag kann beispielsweise so aussehen:

```
-[statsd] metric excluded: mongo.statsd.vsize (filter: -[mongo.statsd.*])
+[statsd] metric included: mongo.statsd.netIn (filter: +[mongo.statsd.net*])
```
{: screen}

Führen Sie die folgenden Schritte aus:

1. Richten Sie die Clusterumgebung ein. Führen Sie die folgenden Befehle aus:

    Verwenden Sie zuerst den Befehl zum Festlegen der Umgebungsvariablen und zum Herunterladen der Kubernetes-Konfigurationsdateien.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Wenn der Download der Konfigurationsdateien abgeschlossen ist, wird ein Befehl angezeigt, mit dem Sie den Pfad zur lokalen Kubernetes-Konfigurationsdatei als Umgebungsvariable festlegen können.

    Kopieren Sie dann den in Ihrem Terminal angezeigten Befehl und fügen Sie ihn ein, um die Umgebungsvariable KUBECONFIG festzulegen.

    **Hinweis:** Jedes Mal, wenn Sie sich an der {{site.data.keyword.containerlong}}-CLI für die Arbeit mit Clustern anmelden, müssen Sie diese Befehle ausführen, um den Pfad zur Konfigurationsdatei des Clusters als Sitzungsvariable zu definieren. Die Kubernetes-CLI verwendet diese Variable, um eine lokale Konfigurationsdatei und Zertifikate zu finden, die für die Verbindung mit dem Cluster in {{site.data.keyword.cloud_notm}} erforderlich sind.

2. Bearbeiten Sie die Datei *sysdig-agent-daemonset-v2.yaml*. 

    Führen Sie den folgenden Befehl aus:

    ```
    kubectl edit daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Nehmen Sie Änderungen vor. Fügen Sie den Abschnitt *log* hinzu oder aktualisieren Sie den Abschnitt.

    Wenn Sie z. B. Ereignisse mit niedriger Priorität (*Hinweis*, *Informationen*, *Debug*) herausfiltern möchten, müssen Sie den Eintrag **metrics_excess_log** im Abschnitt **log** auf *true* festlegen:

    ```
    log:
      metrics_excess_log: true
    ```
    {: codeblock}

6. Speichern Sie die Änderungen. 

Die Änderungen werden automatisch angewendet. 


## Beispiel für eine Configmap-YAML-Datei
{: #change_kube_agent_sample_configmap}

```
apiVersion: v1
data:
  dragent.yaml: |
    ### Agent-Tags
    # tags: linux:ubuntu,dept:dev,local:nyc
    #### Konfiguration der Sysdig-Software
    ####
    # Sysdig-Collector-Adresse
    # collector: 192.168.1.1
    # Collector-TCP-Port
    # collector_port: 6666
    # Ob Collector SSL akzeptiert
    # ssl: true
    # Collector-Zertifikatsprüfung
    # ssl_verify_certificate: true
    #######################################
    #
    k8s_cluster_name: cluster12
    collector: ingest.us-south.monitoring.cloud.ibm.com
    collector_port: 6443
    ssl: true
    ssl_verify_certificate: true
    sysdig_capture_enabled: false
    new_k8s: true
    tags: type:mycluster,region:us-south
    blacklisted_ports:
      - 6666
      - 6379
    events:
      kubernetes:
        node:
          - Rebooted
      metrics_filter:
        - include: metricA.*
        - exclude: metricA.*
        - include: metricB.*
      use_container_filter: true
      container_filter:
        - exclude:
          kubernetes.namespace.name: kube-system
kind: ConfigMap
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"v1","data":{"dragent.yaml":"### Agent tags\n# tags: linux:ubuntu,dept:dev,local:nyc\n#### Sysdig Software related config \n####\n# Sysdig collector address\n# collector: xxx.xxx.x.x\n# Collector TCP port\n# collector_port: 6666\n# Whether collector accepts ssl\n# ssl: true\n# collector certificate validation\n# ssl_verify_certificate: true\n#######################################\n#\nk8s_cluster_name: marisa-production\ncollector: ingest.us-south.monitoring.cloud.ibm.com\ncollector_port: 6443\nssl: true\nssl_verify_certificate: true\nsysdig_capture_enabled: true\nnew_k8s: true\ntags: cluster:mycluster,region:us-south\nevents:    \n  kubernetes:\n     node: \n       - Rebooted\nuse_container_filter: true\ncontainer_filter: \n      - exclude:\n         kubernetes.namespace.name: kube-system\n         container.image: \"registry.ng.bluemix.net/*\"\n"},"kind":"ConfigMap","metadata":{"annotations":{},"creationTimestamp":"2018-11-07T10:57:38Z","name":"sysdig-agent","namespace":"default","resourceVersion":"9999999","selfLink":"/api/v1/namespaces/default/configmaps/sysdig-agent","uid":"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"}}
  creationTimestamp: 2018-11-07T10:57:38Z
  name: sysdig-agent
  namespace: default
  resourceVersion: "9999999"
  selfLink: /api/v1/namespaces/default/configmaps/sysdig-agent
  uid: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```
{: codeblock}

## Beispiel für eine Daemonset-YAML-Datei
{: #change_kube_agent_sample_daemonset}

```
 Bearbeiten Sie das unten stehende Objekt. Zeilen, die mit '#' beginnen, werden ignoriert,
# und eine leere Datei bricht die Bearbeitung ab. Wenn beim Speichern dieser Datei ein Fehler auftritt, wird die Datei
# mit den entsprechenden Fehlern erneut geöffnet.
#
apiVersion: extensions/v1beta1
kind: DaemonSet
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"extensions/v1beta1","kind":"DaemonSet","metadata":{"annotations":{},"labels":{"app":"sysdig-agent"},"name":"sysdig-agent","namespace":"default"},"spec":{"template":{"metadata":{"labels":{"app":"sysdig-agent"}},"spec":{"containers":[{"image":"sysdig/agent","imagePullPolicy":"Always","name":"sysdig-agent","readinessProbe":{"exec":{"command":["test","-e","/opt/draios/logs/running"]},"initialDelaySeconds":10},"resources":{"limits":{"memory":"1024Mi"},"requests":{"cpu":"100m","memory":"512Mi"}},"securityContext":{"privileged":true},"volumeMounts":[{"mountPath":"/host/var/run/docker.sock","name":"docker-sock","readOnly":false},{"mountPath":"/host/dev","name":"dev-vol","readOnly":false},{"mountPath":"/host/proc","name":"proc-vol","readOnly":true},{"mountPath":"/host/boot","name":"boot-vol","readOnly":true},{"mountPath":"/host/lib/modules","name":"modules-vol","readOnly":true},{"mountPath":"/host/usr","name":"usr-vol","readOnly":true},{"mountPath":"/dev/shm","name":"dshm"},{"mountPath":"/opt/draios/etc/kubernetes/config","name":"sysdig-agent-config"},{"mountPath":"/opt/draios/etc/kubernetes/secrets","name":"sysdig-agent-secrets"}]}],"dnsPolicy":"ClusterFirstWithHostNet","hostNetwork":true,"hostPID":true,"serviceAccount":"sysdig-agent","terminationGracePeriodSeconds":5,"tolerations":[{"effect":"NoSchedule","key":"node-role.kubernetes.io/master"}],"volumes":[{"emptyDir":{"medium":"Memory"},"name":"dshm"},{"hostPath":{"path":"/var/run/docker.sock"},"name":"docker-sock"},{"hostPath":{"path":"/dev"},"name":"dev-vol"},{"hostPath":{"path":"/proc"},"name":"proc-vol"},{"hostPath":{"path":"/boot"},"name":"boot-vol"},{"hostPath":{"path":"/lib/modules"},"name":"modules-vol"},{"hostPath":{"path":"/usr"},"name":"usr-vol"},{"configMap":{"name":"sysdig-agent","optional":true},"name":"sysdig-agent-config"},{"name":"sysdig-agent-secrets","secret":{"secretName":"sysdig-agent"}}]}},"updateStrategy":{"type":"RollingUpdate"}}}
  creationTimestamp: 2018-11-07T13:39:58Z
  generation: 2
  labels:
    app: sysdig-agent
  name: sysdig-agent
  namespace: default
  resourceVersion: "5980648"
  selfLink: /apis/extensions/v1beta1/namespaces/default/daemonsets/sysdig-agent
  uid: 9ea3353f-e292-11e8-b4b3-260d32136de0
spec:
  revisionHistoryLimit: 10
  selector:
    matchLabels:
      app: sysdig-agent
log:
  event_priority: warning
  file_priority: warning
  console_priority: info
  metrics_excess_log: true
```
{: codeblock}

