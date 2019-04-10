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

# Configurazione di un agent Sysdig
{: #config_agent}

Dopo aver eseguito il provisioning di un'istanza del servizio {{site.data.keyword.mon_full_notm}} in {{site.data.keyword.cloud_notm}}, devi configurare un agent Sysdig in ogni ambiente che vuoi monitorare. L'agent Sysdig raccoglie e riporta automaticamente le metriche predefinite. Puoi configurare quali metriche monitorare in ogni ambiente.
{:shortdesc}

Puoi associare una o più tag ad ogni agent Sysdig. Le tag sono valori separati da virgole formattate come **TAG_NAME:TAG_VALUE**. Quando monitori il tuo ambiente, puoi utilizzare queste tag per identificare le metriche disponibili da un agent. Ad esempio, puoi includere le informazioni sul nome e l'ubicazione del servizio con tutte le metriche raccolte da questo agent.
{: tip}

## Configurazione di un agent Sysdig su Linux
{: #config_agent_linux}

Completa la seguente procedura per configurare un agent Sysdig su Linux in modo che raccolga e inoltri le metriche a un'istanza del servizio {{site.data.keyword.mon_full_notm}}:

1. Ottieni la chiave di accesso Sysdig. Per ulteriori informazioni, consulta [Ottenimento della chiave di accesso tramite l'IU {{site.data.keyword.cloud_notm}}](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui).

2. Ottieni l'URL di inserimento. Per ulteriori informazioni, consulta [Endpoint raccoglitore Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion).

3. Distribuisci l'agent Sysdig. Immetti il seguente comando da un terminale:

    ```
    curl -sL https://ibm.biz/install-sysdig-agent | sudo bash -s -- --access_key SYSDIG_ACCESS_KEY --collector COLLECTOR_ENDPOINT --collector_port 6443 --secure true --tags TAG_DATA --additional_conf 'sysdig_capture_enabled: false'
    ```
    {: codeblock}

    Dove

    * SYSDIG_ACCESS_KEY è la chiave di inserimento per l'istanza.

    * COLLECTOR_ENDPOINT è l'URL di inserimento per la regione in cui è disponibile l'istanza di monitoraggio.

    * TAG_DATA sono tag separate da virgole formattate come *TAG_NAME:TAG_VALUE*. Puoi associare una o più tag al tuo agent Sysdig. Ad esempio: *role:serviceX,location:us-south*. 

    * Imposta **sysdig_capture_enabled** su *false* per disabilitare la funzione di acquisizione Sysdig. Per impostazione predefinita è impostato su *true*. Per ulteriori informazioni, consulta [Utilizzo delle acquisizioni](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures).

    * Imposta **secure** su *true* per utilizzare SSL con la comunicazione.

Se l'installazione dell'agent Sysdig non viene eseguita correttamente, installa manualmente le intestazioni kernel. Scegli una distribuzione ed esegui il comando per tale distribuzione. Quindi, ritenta la distribuzione dell'agent Sysdig.

* **Per le distribuzioni Debian e Ubuntu Linux**, immetti il seguente comando:

    ```
    apt-get -y install linux-headers-$(uname -r)
    ```
    {: codeblock}

* **Per le distribuzioni RHEL, CentOS e Fedora Linux**, immetti il seguente comando:

    ```
    yum -y install kernel-devel-$(uname -r)
    ```
    {: codeblock}


## Configurazione di un agent Sysdig su un contenitore Docker
{: #config_agent_docker}

Completa la seguente procedura per configurare un agent Sysdig su un contenitore Docker in modo che raccolga e inoltri le metriche a un'istanza del servizio {{site.data.keyword.mon_full_notm}}:

1. Ottieni la chiave di accesso Sysdig. Per ulteriori informazioni, consulta [Ottenimento della chiave di accesso tramite l'IU {{site.data.keyword.cloud_notm}}](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui).

2. Ottieni l'URL di inserimento. Per ulteriori informazioni, consulta [Endpoint raccoglitore Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion).

3. Distribuisci l'agent Sysdig. Immetti il seguente comando:

    ```
    docker run -d --name sysdig-agent --restart always --privileged --net host --pid host -e ACCESS_KEY=SYSDIG_ACCESS_KEY -e COLLECTOR=COLLECTOR_ENDPOINT -e COLLECTOR_PORT=6443 -e SECURE=true -e ADDITIONAL_CONF="sysdig_capture_enabled: false" -e TAGS=TAG_DATA  -v /var/run/docker.sock:/host/var/run/docker.sock -v /dev:/host/dev -v /proc:/host/proc:ro -v /boot:/host/boot:ro -v /lib/modules:/host/lib/modules:ro -v /usr:/host/usr:ro --shm-size=350m sysdig/agent
    ```
    {: codeblock}

    dove

    * SYSDIG_ACCESS_KEY è la chiave di inserimento per l'istanza.

    * COLLECTOR_ENDPOINT è l'URL di inserimento per la regione in cui è disponibile l'istanza di monitoraggio.

    * TAG_DATA sono tag separate da virgole formattate come *TAG_NAME:TAG_VALUE*. Puoi associare una o più tag al tuo agent Sysdig. Ad esempio: *role:serviceX,location:us-south*. 

    * Imposta **sysdig_capture_enabled** su *false* per disabilitare la funzione di acquisizione Sysdig. Per impostazione predefinita è impostato su *true*. Per ulteriori informazioni, consulta [Utilizzo delle acquisizioni](/docs/services/Monitoring-with-Sysdig/captures.html#captures).

    * Imposta **SECURE** su *true* per utilizzare SSL con la comunicazione.

    **Nota:** il contenitore è eseguito in modalità scollegata. Per visualizzare l'output del contenitore, rimuovi *-d*.




## Configurazione di un agent Sysdig su un cluster Kubernetes utilizzando uno script
{: #config_agent_kube_script}

Completa la seguente procedura per configurare un agent Sysdig su un contenitore Kubernetes eseguito in {{site.data.keyword.containerlong_notm}}:

1. Ottieni la chiave di accesso Sysdig. Per ulteriori informazioni, consulta [Ottenimento della chiave di accesso tramite l'IU {{site.data.keyword.cloud_notm}}](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui).

2. Ottieni l'URL di inserimento. Per ulteriori informazioni, consulta [Endpoint raccoglitore Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion).

3. Configura l'ambiente cluster. Immetti i seguenti comandi:

    Per prima cosa, richiama il comando per impostare la variabile di ambiente e scaricare i file di configurazione Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Quando il download dei file di configurazione è terminato, viene visualizzato un comando che puoi utilizzare per impostare il percorso al file di configurazione di Kubernetes locale come una variabile di ambiente.

    Poi, copia e incolla il comando visualizzato nel tuo terminale per impostare la variabile di ambiente KUBECONFIG.

    **Nota:** ogni volta che accedi alla CLI {{site.data.keyword.containerlong}} per utilizzare i cluster, devi eseguire questi comandi per impostare il percorso al file di configurazione del cluster come una variabile di sessione. La CLI Kubernetes utilizza questa variabile per trovare i certificati e un file di configurazione locale necessari per il collegamento con il cluster in {{site.data.keyword.cloud_notm}}.

4. Distribuisci l'agent Sysdig. Immetti il seguente comando:

    ```
    curl -sL https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/IBMCloud-Kubernetes-Service/install-agent-k8s.sh | bash -s -- -a SYSDIG_ACCESS_KEY -c COLLECTOR_ENDPOINT -t TAG_DATA -ac 'sysdig_capture_enabled: false'
    ```
    {: codeblock}

    dove

    * SYSDIG_ACCESS_KEY è la chiave di inserimento per l'istanza.

    * COLLECTOR_ENDPOINT è l'URL di inserimento per la regione in cui è disponibile l'istanza di monitoraggio.

    * TAG_DATA sono tag separate da virgole formattate come *TAG_NAME:TAG_VALUE*. Puoi associare una o più tag al tuo agent Sysdig. Ad esempio: *role:serviceX,location:us-south*. 

    * Imposta **sysdig_capture_enabled** su *false* per disabilitare la funzione di acquisizione Sysdig. Per impostazione predefinita è impostato su *true*. Per ulteriori informazioni, consulta [Utilizzo delle acquisizioni](/docs/services/Monitoring-with-Sysdig/captures.html#captures).



## Configurazione manuale di un agent Sysdig su un cluster Kubernetes
{: #config_agent_kube_manually}

Completa la seguente procedura per configurare un agent Sysdig su un contenitore Kubernetes eseguito in {{site.data.keyword.containerlong_notm}}:

1. Ottieni la chiave di accesso Sysdig. Per ulteriori informazioni, consulta [Ottenimento della chiave di accesso tramite l'IU {{site.data.keyword.cloud_notm}}](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui).

2. Ottieni l'URL di inserimento. Per ulteriori informazioni, consulta [Endpoint raccoglitore Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion).

3. Configura l'ambiente cluster. Immetti i seguenti comandi:

    Per prima cosa, richiama il comando per impostare la variabile di ambiente e scaricare i file di configurazione Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Quando il download dei file di configurazione è terminato, viene visualizzato un comando che puoi utilizzare per impostare il percorso al file di configurazione di Kubernetes locale come una variabile di ambiente.

    Poi, copia e incolla il comando visualizzato nel tuo terminale per impostare la variabile di ambiente KUBECONFIG.

    **Nota:** ogni volta che accedi alla CLI {{site.data.keyword.containerlong}} per utilizzare i cluster, devi eseguire questi comandi per impostare il percorso al file di configurazione del cluster come una variabile di sessione. La CLI Kubernetes utilizza questa variabile per trovare i certificati e un file di configurazione locale necessari per il collegamento con il cluster in {{site.data.keyword.cloud_notm}}.

4. Crea un account del servizio denominato **sysdig-agent** per monitorare il cluster Kubernetes. Immetti il seguente comando:

    ```
    kubectl create serviceaccount sysdig-agent -n ibm-observe
    ```
    {: codeblock}

5. Aggiungi un segreto al tuo cluster Kubernetes. Immetti il seguente comando:

    ```
    kubectl create secret generic sysdig-agent --from-literal=access-key=SYSDIG_ACCESS_KEY -n ibm-observe
    ```
    {: codeblock}

    SYSDIG_ACCESS_KEY è la chiave di inserimento per l'istanza.

    Il segreto Kubernetes contiene la chiave di inserimento che viene utilizzata per autenticare l'agent Sysdig con il servizio {{site.data.keyword.mon_full_notm}}. Viene utilizzata per aprire un socket web sicuro al server di inserimento sul sistema backend di monitoraggio.

6. Crea un ruolo del cluster e un'associazione del ruolo del cluster. 

    Scarica [**sysdig-agent-clusterrole.yaml**](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-agent-clusterrole.yaml).
    
    Per aggiungere un ruolo del cluster, immetti il seguente comando:
    
    ```
    kubectl apply -f /tmp/sysdig-agent-clusterrole.yaml
    ```
    {: codeblock}

    Per aggiungere un'associazione del ruolo del cluster, immetti il seguente comando:

    ```
    kubectl create clusterrolebinding sysdig-agent --clusterrole=sysdig-agent --serviceaccount=ibm-observe:sysdig-agent -n ibm-observe
    ```
    {: codeblock}

7. Modifica **sysdig-agent-configmap.yaml** e aggiungi i parametri richiesti per la configurazione dell'agent in modo che funzioni in {{site.data.keyword.cloud_notm}}.

    Scarica [**sysdig-agent-configmap.yaml**](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-agent-configmap.yaml).

    Utilizza un editor per aprire il file sysdig-agent-configmap.yaml. Poi, aggiungi i seguenti parametri:

    * **k8s_cluster_name**: questo parametro specifica il nome del cluster come un'etichetta della metrica. Puoi utilizzare l'etichetta *kubernetes.cluster.name* per navigare nei dashboard Kubernetes per nome del cluster e filtrare le metriche associate al cluster.

    * **collector**: questo parametro specifica l'URL di inserimento per la regione in cui è disponibile l'istanza di monitoraggio. 

    * **collector_port**: questo parametro indica la porta su cui è in ascolto il raccoglitore. Il valore deve essere *6443*.
    
    * **ssl**: questo parametro deve essere impostato su *true*.
    
    * **ssl_verfiy_certificate**: questo parametro deve essere impostato su *true*.
    
    * **new_k8s**: questo parametro deve essere impostato su *true* per acquisire le metriche kube state.

    * **sysdig_capture_enabled**: questo parametro abilita o disabilita la funzione di acquisizione Sysdig. Per impostazione predefinita è impostato su *true*. Per ulteriori informazioni, consulta [Utilizzo delle acquisizioni](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures).

    Un file yaml di esempio è simile a quanto segue:

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

8. Applica la mappa di configurazione al cluster. Immetti il seguente comando:

    ```
    kubectl apply -f sysdig-agent-configmap.yaml
    ```
    {: codeblock}

9. Applica la serie di daemon per distribuire l'agent Sysdig al cluster. Immetti il seguente comando:

    Scarica [**sysdig-agent-daemonset-v2.yaml**](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-agent-daemonset-v2.yaml).

    ```
    kubectl apply -f sysdig-agent-daemonset-v2.yaml
    ```
    {: codeblock}




