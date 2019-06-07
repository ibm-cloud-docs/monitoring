---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

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

# Configuration d'un agent Sysdig
{: #config_agent}

Après la mise à disposition d'une instance du service {{site.data.keyword.mon_full_notm}} dans {{site.data.keyword.cloud_notm}}, vous devez configurer un agent Sysdig dans chaque environnement à surveiller. L'agent Sysdig collecte automatiquement des métriques prédéfinies et génère des rapports les concernant. Vous pouvez configurer quelles métriques surveiller dans chaque environnement.
{:shortdesc}

Vous pouvez associer une ou plusieurs étiquettes à chaque agent Sysdig. Les étiquettes sont des valeurs séparées par une virgule qui se présentent sous la forme **TAG_NAME:TAG_VALUE**. Lorsque vous surveillez votre environnement, vous pouvez les utiliser pour identifier les métriques mises à disposition par un agent. Par exemple, vous pouvez inclure des informations sur le nom du service et l'emplacement dans toutes les métriques qui sont collectées par cet agent.
{: tip}

## Configuration d'un agent Sysdig sous Linux
{: #config_agent_linux}

Procédez comme suit pour configurer un agent Sysdig sous Linux pour collecter et transmettre des métriques à une instance du service {{site.data.keyword.mon_full_notm}} :

1. Obtenez la clé d'accès Sysdig. Pour plus d'informations, voir [Obtention de la clé d'accès via l'interface utilisateur {{site.data.keyword.cloud_notm}}](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui).

2. Obtenez l'URL d'ingestion. Pour plus d'informations, voir [Noeuds finaux de collecteur Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion).

3. Déployez l'agent Sysdig. Exécutez la commande suivante à partir d'un terminal.

    ```
    curl -sL https://ibm.biz/install-sysdig-agent | sudo bash -s -- --access_key SYSDIG_ACCESS_KEY --collector COLLECTOR_ENDPOINT --collector_port 6443 --secure true --tags TAG_DATA --additional_conf 'sysdig_capture_enabled: false'
    ```
    {: codeblock}

    où

    * SYSDIG_ACCESS_KEY est la clé d'ingestion pour l'instance.

    * COLLECTOR_ENDPOINT est l'URL d'ingestion pour la région où se trouve l'instance de surveillance.

    * TAG_DATA sont des étiquettes séparées par une virgule qui se présentent sous la forme *TAG_NAME:TAG_VALUE*. Vous pouvez associer une ou plusieurs étiquettes à votre agent Sysdig. Par exemple, *role:serviceX,location:us-south*.  

    * Définissez **sysdig_capture_enabled** sur *false* pour désactiver la fonction de capture Sysdig. La valeur par défaut est *true*. Pour plus d'informations, voir [Utilisation des captures](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures).

    * Définissez **secure** sur *true* pour utiliser la couche SSL avec la communication.

Si l'agent Sysdig ne parvient pas à s'installer correctement, installez les en-têtes de noyau manuellement. Choisissez une distribution et exécutez la commande pour cette distribution. Relancez ensuite le déploiement de l'agent Sysdig.

* **Pour les distributions Debian et Ubuntu Linux**, exécutez la commande suivante :

    ```
    apt-get -y install linux-headers-$(uname -r)
    ```
    {: codeblock}

* **Pour les distributions RHEL, CentOS et Fedora Linux**, exécutez la commande suivante :

    ```
    yum -y install kernel-devel-$(uname -r)
    ```
    {: codeblock}


## Configuration d'un agent Sysdig sur un conteneur Docker
{: #config_agent_docker}

Procédez comme suit pour configurer un agent Sysdig sur un conteneur Docker pour collecter et transmettre des métriques à une instance du service {{site.data.keyword.mon_full_notm}} :

1. Obtenez la clé d'accès Sysdig. Pour plus d'informations, voir [Obtention de la clé d'accès via l'interface utilisateur {{site.data.keyword.cloud_notm}}](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui).

2. Obtenez l'URL d'ingestion. Pour plus d'informations, voir [Noeuds finaux de collecteur Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion).

3. Déployez l'agent Sysdig. Exécutez la commande suivante :

    ```
    docker run -d --name sysdig-agent --restart always --privileged --net host --pid host -e ACCESS_KEY=SYSDIG_ACCESS_KEY -e COLLECTOR=COLLECTOR_ENDPOINT -e COLLECTOR_PORT=6443 -e SECURE=true -e ADDITIONAL_CONF="sysdig_capture_enabled: false" -e TAGS=TAG_DATA  -v /var/run/docker.sock:/host/var/run/docker.sock -v /dev:/host/dev -v /proc:/host/proc:ro -v /boot:/host/boot:ro -v /lib/modules:/host/lib/modules:ro -v /usr:/host/usr:ro --shm-size=350m sysdig/agent
    ```
    {: codeblock}

    où

    * SYSDIG_ACCESS_KEY est la clé d'ingestion pour l'instance.

    * COLLECTOR_ENDPOINT est l'URL d'ingestion pour la région où se trouve l'instance de surveillance.

    * TAG_DATA sont des étiquettes séparées par une virgule qui se présentent sous la forme *TAG_NAME:TAG_VALUE*. Vous pouvez associer une ou plusieurs étiquettes à votre agent Sysdig. Par exemple, *role:serviceX,location:us-south*.  

    * Définissez **sysdig_capture_enabled** sur *false* pour désactiver la fonction de capture Sysdig. La valeur par défaut est *true*. Pour plus d'informations, voir [Utilisation des captures](/docs/services/Monitoring-with-Sysdig/captures.html#captures).

    * Définissez **SECURE** sur *true* pour utiliser la couche SSL avec la communication.

    Le conteneur s'exécute en mode déconnecté. Pour afficher la sortie du conteneur, supprimez *-d*.
    {: note}




## Configuration d'un agent Sysdig sur un cluster Kubernetes à l'aide d'un script
{: #config_agent_kube_script}

Procédez comme suit pour configurer un agent Sysdig sur un cluster Kubernetes qui s'exécute dans {{site.data.keyword.containerlong_notm}} :

1. Obtenez la clé d'accès Sysdig. Pour plus d'informations, voir [Obtention de la clé d'accès via l'interface utilisateur {{site.data.keyword.cloud_notm}}](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui).

2. Obtenez l'URL d'ingestion. Pour plus d'informations, voir [Noeuds finaux de collecteur Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion).

3. Configurez l'environnement de cluster. Exécutez les commandes suivantes :

    Lancez d'abord la commande permettant de définir la variable d'environnement et téléchargez les fichiers de configuration Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Une fois les fichiers de configuration téléchargés, une commande s'affiche ; elle vous permet de définir le chemin vers le fichier de configuration Kubernetes local en tant que variable d'environnement.

    Ensuite, copiez et collez la commande qui s'affiche sur votre terminal pour définir la variable d'environnement KUBECONFIG.

4. Déployez l'agent Sysdig. Exécutez la commande suivante :

    ```
    curl -sL https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/IBMCloud-Kubernetes-Service/install-agent-k8s.sh | bash -s -- -a SYSDIG_ACCESS_KEY -c COLLECTOR_ENDPOINT -t TAG_DATA -ac 'sysdig_capture_enabled: false'
    ```
    {: codeblock}

    où

    * SYSDIG_ACCESS_KEY est la clé d'ingestion pour l'instance.

    * COLLECTOR_ENDPOINT est l'URL d'ingestion pour la région où se trouve l'instance de surveillance.

    * TAG_DATA sont des étiquettes séparées par une virgule qui se présentent sous la forme *TAG_NAME:TAG_VALUE*. Vous pouvez associer une ou plusieurs étiquettes à votre agent Sysdig. Exemple : *role:serviceX,location:us-south*. 

    * Définissez **sysdig_capture_enabled** sur *false* pour désactiver la fonction de capture Sysdig. La valeur par défaut est *true*. Pour plus d'informations, voir [Utilisation des captures](/docs/services/Monitoring-with-Sysdig/captures.html#captures).



## Configuration manuelle d'un agent Sysdig sur un cluster Kubernetes
{: #config_agent_kube_manually}

Procédez comme suit pour configurer un agent Sysdig sur un cluster Kubernetes qui s'exécute dans {{site.data.keyword.containerlong_notm}} :

1. Obtenez la clé d'accès Sysdig. Pour plus d'informations, voir [Obtention de la clé d'accès via l'interface utilisateur {{site.data.keyword.cloud_notm}}](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui).

2. Obtenez l'URL d'ingestion. Pour plus d'informations, voir [Noeuds finaux de collecteur Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion).

3. Configurez l'environnement de cluster. Exécutez les commandes suivantes :

    Lancez d'abord la commande permettant de définir la variable d'environnement et téléchargez les fichiers de configuration Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Une fois les fichiers de configuration téléchargés, une commande s'affiche ; elle vous permet de définir le chemin vers le fichier de configuration Kubernetes local en tant que variable d'environnement.

    Ensuite, copiez et collez la commande qui s'affiche sur votre terminal pour définir la variable d'environnement KUBECONFIG.

4. Créez un compte de service appelé **sysdig-agent** pour surveiller le cluster Kubernetes. Exécutez la commande suivante :

    ```
    kubectl create serviceaccount sysdig-agent -n ibm-observe
    ```
    {: codeblock}

5. Ajoutez une valeur confidentielle à votre cluster Kubernetes. Exécutez la commande suivante :

    ```
    kubectl create secret generic sysdig-agent --from-literal=access-key=SYSDIG_ACCESS_KEY -n ibm-observe
    ```
    {: codeblock}

    SYSDIG_ACCESS_KEY est la clé d'ingestion pour l'instance.

    La valeur confidentielle Kubernetes contient la clé d'ingestion qui est utilisée pour authentifier l'agent Sysdig auprès du service {{site.data.keyword.mon_full_notm}}. Elle permet d'ouvrir un socket Web sécurisé sur le serveur d'ingestion dans le système back end de surveillance.

6. Créez un rôle de cluster et une liaison de rôle de cluster. 

    Téléchargez le fichier [**sysdig-agent-clusterrole.yaml**](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-agent-clusterrole.yaml).
    
    Pour ajouter un rôle de cluster, exécutez la commande suivante :
    
    ```
    kubectl apply -f /tmp/sysdig-agent-clusterrole.yaml
    ```
    {: codeblock}

    Pour ajouter une liaison de rôle de cluster, exécutez la commande suivante :

    ```
    kubectl create clusterrolebinding sysdig-agent --clusterrole=sysdig-agent --serviceaccount=ibm-observe:sysdig-agent -n ibm-observe
    ```
    {: codeblock}

7. Editez le fichier **sysdig-agent-configmap.yaml** et ajoutez les paramètres requis pour la configuration de l'agent à utiliser dans {{site.data.keyword.cloud_notm}}.

    Téléchargez le fichier [**sysdig-agent-configmap.yaml**](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-agent-configmap.yaml).

    Utilisez un éditeur pour ouvrir le fichier sysdig-agent-configmap.yaml. Ajoutez ensuite les paramètres suivants :

    * **k8s_cluster_name**: ce paramètre indique le nom de cluster sous forme de libellé de métrique. Vous pouvez utiliser le libellé *kubernetes.cluster.name* pour naviguer dans les tableaux de bord Kubernetes par nom de fichier et filtrer les métriques associées au cluster.

    * **collector** : ce paramètre indique l'URL d'ingestion pour la région où se trouve l'instance de surveillance. 

    * **collector_port** : ce paramètre indique le port sur lequel le collecteur effectue l'écoute. Sa valeur doit être *6443*.
    
    * **ssl** : ce paramètre doit être défini sur *true*.
    
    * **ssl_verfiy_certificate** : ce paramètre doit être défini sur *true*.
    
    * **new_k8s** : ce paramètre doit être défini sur *true* pour capturer les métriques kube state.

    * **sysdig_capture_enabled** : ce paramètre active ou désactive la fonction de capture Sysdig. La valeur par défaut est *true*. Pour plus d'informations, voir [Utilisation des captures](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures).

    Voici un exemple de fichier Yaml :

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

8. Appliquez la mappe de configuration au cluster. Exécutez la commande suivante :

    ```
    kubectl apply -f sysdig-agent-configmap.yaml
    ```
    {: codeblock}

9. Appliquez le daemonset pour déployer l'agent Sysdig sur le cluster. Exécutez la commande suivante :

    Téléchargez le fichier [**sysdig-agent-daemonset-v2.yaml**](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-agent-daemonset-v2.yaml).

    ```
    kubectl apply -f sysdig-agent-daemonset-v2.yaml
    ```
    {: codeblock}




