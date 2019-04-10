---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, delete agent

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

# Einen Sysdig-Agenten entfernen
{: #remove_agent}

Wenn Sie eine {{site.data.keyword.mon_full_notm}}-Instanz löschen oder wenn Sie die Erfassung von Metriken aus einer Quelle stoppen möchten, müssen Sie den Sysdig-Agenten deinstallieren.
{:shortdesc}


## Einen Sysdig-Agenten aus einem Kubernetes-Cluster entfernen
{: #remove_agent_kube}

Führen Sie die folgenden Schritte aus, um einen Sysdig-Agenten aus einem Kubernetes-Cluster zu entfernen:

1. Richten Sie die Clusterumgebung ein. Führen Sie die folgenden Befehle aus:

    Verwenden Sie zuerst den Befehl zum Festlegen der Umgebungsvariablen und zum Herunterladen der Kubernetes-Konfigurationsdateien.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Wenn der Download der Konfigurationsdateien abgeschlossen ist, wird ein Befehl angezeigt, mit dem Sie den Pfad zur lokalen Kubernetes-Konfigurationsdatei als Umgebungsvariable festlegen können.

    Kopieren Sie dann den in Ihrem Terminal angezeigten Befehl und fügen Sie ihn ein, um die Umgebungsvariable KUBECONFIG festzulegen.

    **Hinweis:** Jedes Mal, wenn Sie sich an der {{site.data.keyword.containerlong}}-CLI für die Arbeit mit Clustern anmelden, müssen Sie diese Befehle ausführen, um den Pfad zur Konfigurationsdatei des Clusters als Sitzungsvariable zu definieren. Die Kubernetes-CLI verwendet diese Variable, um eine lokale Konfigurationsdatei und Zertifikate zu finden, die für die Verbindung mit dem Cluster in {{site.data.keyword.cloud_notm}} erforderlich sind.

2. Entfernen Sie die Bindung der Clusterrolle. Führen Sie den folgenden Befehl aus:

    ```
    kubectl delete clusterrolebinding sysdig-agent
    ```
    {: codeblock}

3. Entfernen Sie das Servicekonto. Führen Sie den folgenden Befehl aus:

    ```
    kubectl delete serviceaccount -n ibm-observe sysdig-agent
    ```
    {: codeblock}

4. Entfernen Sie das Daemonset. Führen Sie den folgenden Befehl aus:

    ```
    kubectl delete daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

5. Entfernen Sie den geheimen Schlüssel. Führen Sie den folgenden Befehl aus:

    ```
    kubectl delete secret sysdig-agent -n ibm-observe
    ```
    {: codeblock}




## Einen Sysdig-Agenten unter Linux entfernen
{: #remove_agent_linux}

Führen Sie die folgenden Schritte aus, um einen Sysdig-Agenten unter Linux zu entfernen:

* Um den Agenten von **Debian- und Ubuntu-Linux-Distributionen** zu deinstallieren, führen Sie in einem Terminal den folgenden Befehl als **sudo**-Benutzer aus:

    ```
    sudo apt-get remove draios-agent
    ```
    {: codeblock}

* Um den Agenten von **RHEL-, CentOS- und Fedora Linux-Distributionen** zu deinstallieren, führen Sie in einem Terminal den folgenden Befehl als **sudo**-Benutzer aus:

    ```
    sudo yum erase draios-agent
    ```
    {: codeblock}


