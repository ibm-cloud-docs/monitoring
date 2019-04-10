---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, config sysdig agent

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

# Einen Sysdig-Agenten konfigurieren
{: #config_agent}

Nachdem Sie eine Instanz des {{site.data.keyword.mon_full_notm}}-Service in {{site.data.keyword.cloud_notm}} bereitgestellt haben, müssen Sie in jeder Umgebung, die Sie überwachen möchten, einen Sysdig-Agenten konfigurieren. Der Sysdig-Agent erfasst und berichtet automatisch über vordefinierte Metriken. Sie können konfigurieren, welche Metriken in jeder Umgebung überwacht werden sollen.
{:shortdesc}

Sie können jedem Sysdig-Agenten einen oder mehrere Tags zuordnen. Bei Tags handelt es sich um durch Kommas getrennte Werte, die als **TAG_NAME:TAG_VALUE** formatiert werden. Wenn Sie Ihre Umgebung überwachen, können Sie diese Tags verwenden, um Metriken zu identifizieren, die von einem Agenten zur Verfügung gestellt werden. Sie können beispielsweise Informationen über den Servicenamen und die Position mit allen Metriken, die von diesem Agenten erfasst werden, enthalten.
{: tip}

## Sysdig-Agenten unter Linux konfigurieren
{: #config_agent_linux}

Führen Sie die folgenden Schritte aus, um einen Sysdig-Agenten unter Linux für die Erfassung und Weiterleitung von Metriken an eine Instanz des {{site.data.keyword.mon_full_notm}}-Service zu konfigurieren:

1. Rufen Sie den Sysdig-Zugriffsschlüssel ab. Weitere Informationen finden Sie im Abschnitt [Zugriffsschlüssel über die {{site.data.keyword.cloud_notm}}-Benutzerschnittstelle abrufen](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui).

2. Rufen Sie die Aufnahme-URL ab. Weitere Informationen finden Sie unter [Sysdig-Collector-Endpunkte](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion).

3. Stellen Sie den Sysdig-Agenten bereit. Führen Sie den folgenden Befehl von einem Terminal aus.

    ```
    curl -sL https://ibm.biz/install-sysdig-agent | sudo bash -s -- --access_key SYSDIG_ACCESS_KEY --collector COLLECTOR_ENDPOINT --collector_port 6443 --secure true --tags TAG_DATA --additional_conf 'sysdig_capture_enabled: false'
    ```
    {: codeblock}

    Hierbei gilt Folgendes:

    * SYSDIG_ACCESS_KEY ist der Aufnahmeschlüssel für die Instanz.

    * COLLECTOR_ENDPOINT ist die Aufnahme-URL für die Region, in der die Überwachungsinstanz verfügbar ist.

    * TAG_DATA sind durch Kommas getrennte Tags, die als *TAG_NAME:TAG_VALUE* formatiert sind. Sie können Ihrem Sysdig-Agenten einen oder mehrere Tags zuordnen. Beispiel: *role:serviceX,location:us-south*. 

    * Legen Sie **sysdig_capture_enabled** auf *false* fest, um die Sysdig-Erfassungsfunktion zu inaktivieren. Standardmäßig ist *true* festgelegt. Weitere Informationen finden Sie im Abschnitt [Mit Erfassungen arbeiten](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures).

    * Setzen Sie **secure** auf *true* fest, um SSL mit der Kommunikation zu verwenden.

Wenn der Sysdig-Agent nicht ordnungsgemäß installiert werden kann, installieren Sie die Kernel-Header manuell. Wählen Sie eine Distribution aus und führen Sie den Befehl für diese Distribution aus. Wiederholen Sie anschließend die Bereitstellung des Sysdig-Agenten.

* Für **Debian- und Ubuntu-Linux-Distributionen** führen Sie den folgenden Befehl aus:

    ```
    apt-get -y install linux-headers-$(uname -r)
    ```
    {: codeblock}

* Für **RHEL-, CentOS- und Fedora-Linux-Distributionen** führen Sie den folgenden Befehl aus:

    ```
    yum -y install kernel-devel-$(uname -r)
    ```
    {: codeblock}


## Sysdig-Agenten in einem Docker-Container konfigurieren
{: #config_agent_docker}

Führen Sie die folgenden Schritte aus, um einen Sysdig-Agenten in einem Docker-Container für die Erfassung und Weiterleitung von Metriken an eine Instanz des {{site.data.keyword.mon_full_notm}}-Service zu konfigurieren:

1. Rufen Sie den Sysdig-Zugriffsschlüssel ab. Weitere Informationen finden Sie im Abschnitt [Zugriffsschlüssel über die {{site.data.keyword.cloud_notm}}-Benutzerschnittstelle abrufen](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui).

2. Rufen Sie die Aufnahme-URL ab. Weitere Informationen finden Sie unter [Sysdig-Collector-Endpunkte](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion).

3. Stellen Sie den Sysdig-Agenten bereit. Führen Sie den folgenden Befehl aus:

    ```
    docker run -d --name sysdig-agent --restart always --privileged --net host --pid host -e ACCESS_KEY=SYSDIG_ACCESS_KEY -e COLLECTOR=COLLECTOR_ENDPOINT -e COLLECTOR_PORT=6443 -e SECURE=true -e ADDITIONAL_CONF="sysdig_capture_enabled: false" -e TAGS=TAG_DATA  -v /var/run/docker.sock:/host/var/run/docker.sock -v /dev:/host/dev -v /proc:/host/proc:ro -v /boot:/host/boot:ro -v /lib/modules:/host/lib/modules:ro -v /usr:/host/usr:ro --shm-size=350m sysdig/agent
    ```
    {: codeblock}

    Hierbei gilt Folgendes:

    * SYSDIG_ACCESS_KEY ist der Aufnahmeschlüssel für die Instanz.

    * COLLECTOR_ENDPOINT ist die Aufnahme-URL für die Region, in der die Überwachungsinstanz verfügbar ist.

    * TAG_DATA sind durch Kommas getrennte Tags, die als *TAG_NAME:TAG_VALUE* formatiert sind. Sie können Ihrem Sysdig-Agenten einen oder mehrere Tags zuordnen. Beispiel: *role:serviceX,location:us-south*. 

    * Legen Sie **sysdig_capture_enabled** auf *false* fest, um die Sysdig-Erfassungsfunktion zu inaktivieren. Standardmäßig ist *true* festgelegt. Weitere Informationen finden Sie im Abschnitt [Mit Erfassungen arbeiten](/docs/services/Monitoring-with-Sysdig/captures.html#captures).

    * Setzen Sie **SECURE** auf *true* fest, um SSL mit der Kommunikation zu verwenden.

    **Hinweis:** Der Container wird im getrennten Modus ausgeführt. Wenn Sie die Ausgabe des Containers sehen möchten, entfernen Sie *-d*.




## Sysdig-Agenten in einem Kubernetes-Cluster mithilfe eines Scripts konfigurieren
{: #config_agent_kube_script}

Führen Sie die folgenden Schritte aus, um einen Sysdig-Agenten in einem Kubernetes-Cluster zu konfigurieren, der im {{site.data.keyword.containerlong_notm}} ausgeführt wird:

1. Rufen Sie den Sysdig-Zugriffsschlüssel ab. Weitere Informationen finden Sie im Abschnitt [Zugriffsschlüssel über die {{site.data.keyword.cloud_notm}}-Benutzerschnittstelle abrufen](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui).

2. Rufen Sie die Aufnahme-URL ab. Weitere Informationen finden Sie unter [Sysdig-Collector-Endpunkte](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion).

3. Richten Sie die Clusterumgebung ein. Führen Sie die folgenden Befehle aus:

    Verwenden Sie zuerst den Befehl zum Festlegen der Umgebungsvariablen und zum Herunterladen der Kubernetes-Konfigurationsdateien.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Wenn der Download der Konfigurationsdateien abgeschlossen ist, wird ein Befehl angezeigt, mit dem Sie den Pfad zur lokalen Kubernetes-Konfigurationsdatei als Umgebungsvariable festlegen können.

    Kopieren Sie dann den in Ihrem Terminal angezeigten Befehl und fügen Sie ihn ein, um die Umgebungsvariable KUBECONFIG festzulegen.

    **Hinweis:** Jedes Mal, wenn Sie sich an der {{site.data.keyword.containerlong}}-CLI für die Arbeit mit Clustern anmelden, müssen Sie diese Befehle ausführen, um den Pfad zur Konfigurationsdatei des Clusters als Sitzungsvariable zu definieren. Die Kubernetes-CLI verwendet diese Variable, um eine lokale Konfigurationsdatei und Zertifikate zu finden, die für die Verbindung mit dem Cluster in {{site.data.keyword.cloud_notm}} erforderlich sind.

4. Stellen Sie den Sysdig-Agenten bereit. Führen Sie den folgenden Befehl aus:

    ```
    curl -sL https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/IBMCloud-Kubernetes-Service/install-agent-k8s.sh | bash -s -- -a SYSDIG_ACCESS_KEY -c COLLECTOR_ENDPOINT -t TAG_DATA -ac 'sysdig_capture_enabled: false'
    ```
    {: codeblock}

    Hierbei gilt Folgendes:

    * SYSDIG_ACCESS_KEY ist der Aufnahmeschlüssel für die Instanz.

    * COLLECTOR_ENDPOINT ist die Aufnahme-URL für die Region, in der die Überwachungsinstanz verfügbar ist.

    * TAG_DATA sind durch Kommas getrennte Tags, die als *TAG_NAME:TAG_VALUE* formatiert sind. Sie können Ihrem Sysdig-Agenten einen oder mehrere Tags zuordnen. Beispiel: *role:serviceX,location:us-south*. 

    * Legen Sie **sysdig_capture_enabled** auf *false* fest, um die Sysdig-Erfassungsfunktion zu inaktivieren. Standardmäßig ist *true* festgelegt. Weitere Informationen finden Sie im Abschnitt [Mit Erfassungen arbeiten](/docs/services/Monitoring-with-Sysdig/captures.html#captures).



## Sysdig-Agenten in einem Kubernetes-Cluster manuell konfigurieren
{: #config_agent_kube_manually}

Führen Sie die folgenden Schritte aus, um einen Sysdig-Agenten in einem Kubernetes-Cluster zu konfigurieren, der im {{site.data.keyword.containerlong_notm}} ausgeführt wird:

1. Rufen Sie den Sysdig-Zugriffsschlüssel ab. Weitere Informationen finden Sie im Abschnitt [Zugriffsschlüssel über die {{site.data.keyword.cloud_notm}}-Benutzerschnittstelle abrufen](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui).

2. Rufen Sie die Aufnahme-URL ab. Weitere Informationen finden Sie unter [Sysdig-Collector-Endpunkte](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion).

3. Richten Sie die Clusterumgebung ein. Führen Sie die folgenden Befehle aus:

    Verwenden Sie zuerst den Befehl zum Festlegen der Umgebungsvariablen und zum Herunterladen der Kubernetes-Konfigurationsdateien.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Wenn der Download der Konfigurationsdateien abgeschlossen ist, wird ein Befehl angezeigt, mit dem Sie den Pfad zur lokalen Kubernetes-Konfigurationsdatei als Umgebungsvariable festlegen können.

    Kopieren Sie dann den in Ihrem Terminal angezeigten Befehl und fügen Sie ihn ein, um die Umgebungsvariable KUBECONFIG festzulegen.

    **Hinweis:** Jedes Mal, wenn Sie sich an der {{site.data.keyword.containerlong}}-CLI für die Arbeit mit Clustern anmelden, müssen Sie diese Befehle ausführen, um den Pfad zur Konfigurationsdatei des Clusters als Sitzungsvariable zu definieren. Die Kubernetes-CLI verwendet diese Variable, um eine lokale Konfigurationsdatei und Zertifikate zu finden, die für die Verbindung mit dem Cluster in {{site.data.keyword.cloud_notm}} erforderlich sind.

4. Erstellen Sie ein Servicekonto mit dem Namen **sysdig-agent**, um den Kubernetes-Cluster zu überwachen. Führen Sie den folgenden Befehl aus:

    ```
    kubectl create serviceaccount sysdig-agent -n ibm-observe
    ```
    {: codeblock}

5. Fügen Sie Ihrem Kubernetes-Cluster einen geheimen Schlüssel hinzu. Führen Sie den folgenden Befehl aus:

    ```
    kubectl create secret generic sysdig-agent --from-literal=access-key=SYSDIG_ACCESS_KEY -n ibm-observe
    ```
    {: codeblock}

    SYSDIG_ACCESS_KEY ist der Aufnahmeschlüssel für die Instanz.

    Der geheime Kubernetes-Schlüssel enthält den Aufnahmeschlüssel, der für die Authentifizierung des Sysdig-Agenten mit dem {{site.data.keyword.mon_full_notm}}-Service verwendet wird. Er wird verwendet, um einen sicheren Web-Socket für den Aufnahmeserver auf dem Überwachungs-Back-End-System zu öffnen.

6. Erstellen Sie eine Clusterrolle und eine Clusterrollenbindung. 

    Laden Sie die Datei [**sysdig-agent-clusterrole.yaml**](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-agent-clusterrole.yaml) herunter.
    
    Führen Sie den folgenden Befehl aus, um eine Clusterrolle hinzuzufügen:
    
    ```
    kubectl apply -f /tmp/sysdig-agent-clusterrole.yaml
    ```
    {: codeblock}

    Führen Sie den folgenden Befehl aus, um eine Clusterrollenbindung hinzuzufügen:

    ```
    kubectl create clusterrolebinding sysdig-agent --clusterrole=sysdig-agent --serviceaccount=ibm-observe:sysdig-agent -n ibm-observe
    ```
    {: codeblock}

7. Bearbeiten Sie die Datei **sysdig-agent-configmap.yaml** und fügen Sie die erforderlichen Parameter für die Konfiguration des Agenten hinzu, der in {{site.data.keyword.cloud_notm}} verwendet werden soll.

    Laden Sie die Datei [**sysdig-agent-configmap.yaml**](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-agent-configmap.yaml) herunter.

    Verwenden Sie einen Editor, um die Datei "sysdig-agent-configmap.yaml" zu öffnen. Fügen Sie dann die folgenden Parameter hinzu:

    * **k8s_cluster_name**: Dieser Parameter gibt den Clusternamen als Metrikbezeichnung an. Sie können die Bezeichnung *kubernetes.cluster.name* verwenden, um in den Kubernetes-Dashboards nach Clusternamen zu navigieren und Metriken herauszufiltern, die dem Cluster zugeordnet sind.

    * **collector**: Dieser Parameter gibt die Aufnahme-URL für die Region an, in der die Überwachungsinstanz verfügbar ist. 

    * **collector_port**: Dieser Parameter gibt den Port an, für den der Collektor empfangsbereit ist. Der Wert muss *6443* sein.
    
    * **ssl**: Dieser Parameter muss auf *true* festgelegt sein.
    
    * **ssl_verfiy_certificate**: Dieser Parameter muss auf *true* festgelegt sein.
    
    * **new_k8s**: Dieser Parameter muss auf *true* festgelegt werden, um Kube-Statusmetriken erfassen zu können.

    * **sysdig_capture_enabled**: Dieser Parameter aktiviert oder inaktiviert die Sysdig-Erfassungsfunktion. Standardmäßig ist *true* festgelegt. Weitere Informationen finden Sie im Abschnitt [Mit Erfassungen arbeiten](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures).

    Ein Beispiel für eine yaml-Datei sieht wie folgt aus:

    ```
     apiVersion: v1
     kind: ConfigMap
     metadata:
       name: sysdig-agent
     data:
       dragent.yaml: |
       tags: linux:ubuntu,dept:dev,local:nyc
       collector: ingest.us-south.monitoring.cloud.ibm.com
       collector_port: 6443
       ssl: true
       new_k8s: true
       k8s_cluster_name: my_cluster_name
       sysdig_capture_enabled: false
    ```
    {: screen}

8. Wenden Sie die Konfigurationszuordnung auf den Cluster an. Führen Sie den folgenden Befehl aus:

    ```
    kubectl apply -f sysdig-agent-configmap.yaml
    ```
    {: codeblock}

9. Wenden Sie das Daemonset an, um den Sysdig-Agenten im Cluster bereitzustellen. Führen Sie den folgenden Befehl aus:

    Laden Sie die Datei [**sysdig-agent-daemonset-v2.yaml**](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-agent-daemonset-v2.yaml) herunter.

    ```
    kubectl apply -f sysdig-agent-daemonset-v2.yaml
    ```
    {: codeblock}




