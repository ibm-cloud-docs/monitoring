---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-06"

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

# Personnalisation des agents Sysdig Kubernetes
{: #change_kube_agent}

Dans {{site.data.keyword.mon_full_notm}}, vous pouvez personnaliser la configuration de l'agent Sysdig pour définir un niveau de journalisation, des ports de bloc, inclure ou exclure des données de mesure, ajouter ou supprimer des événements, et filtrer des conteneurs. 
{:shortdesc}

Pour personnaliser un agent Sysdig Kubernetes, vous devrez peut-être configurer des sections dans l'un des fichiers suivants :

| Nom de fichier                        | Actions       |
|----------------------------------|-------------------|
| `sysdig-agent-daemonset-v2.yaml` | Modification du niveau de journalisation. |
| `sysdig-agent-configmap.yaml`    | Blocage de ports. </br>Inclusion ou exclusion de données de métriques. </br>Ajout ou suppression d'événements. </br>Filtrage de conteneurs. |
{: caption="Tableau 1. Fichiers de configuration de l'agent Sysdig Kubernetes" caption-side="top"} 

Pour modifier un agent Sysdig Kubernetes, vous devrez peut-être éditer le fichier *sysdig-agent-configmap.yaml* et/ou le
fichier *sysdig-agent-daemonset-v2.yaml*.
{: tip}

Vous pouvez modifier un fichier de configuration de deux façons :
* Méthode 1 : Modification du fichier directement sur le cluster où l'agent est en cours d'exécution.
* Méthode 2 : Modification du fichier localement et application des modifications au cluster.

## Modification de la configuration de l'agent Sysdig Kubernetes à l'aide de kubectl edit
{: #change_kube_agent_edit_kube_agent_method1}

Pour modifier la configuration d'un agent Sysdig Kubernetes, procédez comme suit :

1. Configurez l'environnement de cluster. Exécutez les commandes suivantes :

    Lancez d'abord la commande permettant de définir la variable d'environnement et téléchargez les fichiers de configuration Kubernetes.

    ```
    ibmcloud ks cluster-config <ID_ou_nom_cluster>
    ```
    {: codeblock}

    Une fois les fichiers de configuration téléchargés, une commande s'affiche ; elle vous permet de définir le chemin vers le fichier de configuration Kubernetes local en tant que variable d'environnement.

    Ensuite, copiez et collez la commande qui s'affiche sur votre terminal pour définir la variable d'environnement KUBECONFIG.

    **Remarque :** Chaque fois que vous vous connectez à l'interface CLI {{site.data.keyword.containerlong}} pour utiliser des clusters, vous devez exécuter ces commandes pour définir le chemin d'accès au fichier de configuration du cluster en tant que variable de session. L'interface CLI de Kubernetes utilise cette variable pour localiser un fichier de configuration local et les certificats requis pour connexion au cluster dans {{site.data.keyword.cloud_notm}}.

2. Editez le fichier *sysdig-agent-configmap.yaml*. 

    Exécutez la commande suivante :

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

    Effectuez les modifications. **Remarque :** Reportez-vous aux instructions de l'éditeur `vi` pour savoir comment effectuer des modifications.

    Sauvegardez les modifications. Elles sont appliquées automatiquement. 

3. Editez le fichier *sysdig-agent-daemonset-v2.yaml*. 

    Exécutez la commande suivante : 

    ```
    kubectl edit daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

    Effectuez les modifications. **Remarque :** Reportez-vous aux instructions de l'éditeur `vi` pour savoir comment effectuer des modifications.

    Sauvegardez les modifications. Elles sont appliquées automatiquement.

## Modification de la configuration de l'agent Sysdig Kubernetes à l'aide de kubectl apply
{: #change_kube_agent_edit_kube_agent_method2}

Utilisez cette méthode si les fichiers yaml de configuration sont stockés et gérés dans un système de contrôle des sources.

Pour modifier la configuration d'un agent Sysdig Kubernetes, procédez comme suit :

1. Procurez-vous la copie la plus récente de chaque fichier à partir du contrôleur source. 

    Pour créer un fichier local avec la configuration déployée dans un cluster, vous pouvez également exécuter la commande suivante :
    
    ```
    kubectl get configmap sysdig-agent -n=ibm-observe -o=yaml > prod-sysdig-agent-configmap.yaml
    ```
    {: codeblock} 
    
    ou 
    
    ```
    kubectl get daemonset sysdig-agent -n=ibm-observe -o=yaml > prod-sysdig-agent-daemonset-v2.yaml
    ```
    {: codeblock}

2. Modifiez la configuration.

3. Appliquez les modifications à l'aide des commandes suivantes :

    ```
    kubectl apply -f sysdig-agent-configmap.yaml
    ```
    {: codeblock}
    
    ou
    
    ```
    kubectl apply -f sysdig-agent-daemonset-v2.yaml
    ```
    {: codeblock}

Les agents en cours d'exécution sélectionneront automatiquement la nouvelle configuration une fois que Kubernetes aura propagé les modifications sur tous les noeuds du cluster.


## Ajout d'étiquettes supplémentaires aux données collectées à partir d'un agent Sysdig Kubernetes
{: #change_kube_agent_add_tags}

Procédez comme suit pour ajouter davantage d'étiquettes à une configuration de l'agent Sysdig Kubernetes que vous avez déjà déployée :

1. Configurez l'environnement de cluster. Exécutez les commandes suivantes :

    Lancez d'abord la commande permettant de définir la variable d'environnement et téléchargez les fichiers de configuration Kubernetes.

    ```
    ibmcloud ks cluster-config <ID_ou_nom_cluster>
    ```
    {: codeblock}

    Une fois les fichiers de configuration téléchargés, une commande s'affiche ; elle vous permet de définir le chemin vers le fichier de configuration Kubernetes local en tant que variable d'environnement.

    Ensuite, copiez et collez la commande qui s'affiche sur votre terminal pour définir la variable d'environnement KUBECONFIG.

    **Remarque :** Chaque fois que vous vous connectez à l'interface CLI {{site.data.keyword.containerlong}} pour utiliser des clusters, vous devez exécuter ces commandes pour définir le chemin d'accès au fichier de configuration du cluster en tant que variable de session. L'interface CLI de Kubernetes utilise cette variable pour localiser un fichier de configuration local et les certificats requis pour connexion au cluster dans {{site.data.keyword.cloud_notm}}.

2. Editez le fichier *sysdig-agent-configmap.yaml*. 

    Exécutez la commande suivante :

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Effectuez les modifications. **Remarque :** Reportez-vous aux instructions de l'éditeur `vi` pour savoir comment effectuer des modifications.

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

4. Sauvegardez les modifications. 

Elles sont appliquées automatiquement. 

Dans l'exemple fourni, vous obtenez les étiquettes **agent.tag.cluster_version** et **agent.tag.region**. Vous pouvez les utiliser pour définir des alertes, personnaliser des portées et bien davantage.



## Collecte d'un ensemble d'événements Kubernetes
{: #change_kube_agent_collect_events}

{{site.data.keyword.mon_full_notm}} prend en charge l'intégration d'événement avec Kubernetes. Les agents Sysdig reconnaissent automatiquement ces services et collectent les données d'événement qu'ils contiennent. Vous pouvez éditer le fichier de configuration de l'agent pour modifier son comportement par défaut et inclure ou exclure des données d'événement. 

Par défaut, seul un ensemble limité d'événements est collecté. Pour plus d'informations sur les événements qui sont collectés par défaut, voir [Evénements Kubernetes ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://sysdigdocs.atlassian.net/wiki/spaces/Platform/pages/234356795/Enable+Disable+Event+Data#Enable/DisableEventData-KubernetesEvents){:new_window}.

Pour ajouter ou supprimer des événements, vous devez personnaliser le fichier *sysdig-agent-configmap.yaml* et spécifier les événements à inclure et ceux à filtrer. **Remarque :** Une entrée dans une section du fichier *sysdig-agent-configmap.yaml* remplace la totalité de la section dans la configuration par défaut.
{: tip}

Pour filtrer des événements provenant de pods Kubernetes, procédez comme suit :

1. Configurez l'environnement de cluster. Exécutez les commandes suivantes :

    Lancez d'abord la commande permettant de définir la variable d'environnement et téléchargez les fichiers de configuration Kubernetes.

    ```
    ibmcloud ks cluster-config <ID_ou_nom_cluster>
    ```
    {: codeblock}

    Une fois les fichiers de configuration téléchargés, une commande s'affiche ; elle vous permet de définir le chemin vers le fichier de configuration Kubernetes local en tant que variable d'environnement.

    Ensuite, copiez et collez la commande qui s'affiche sur votre terminal pour définir la variable d'environnement KUBECONFIG.

    **Remarque :** Chaque fois que vous vous connectez à l'interface CLI {{site.data.keyword.containerlong}} pour utiliser des clusters, vous devez exécuter ces commandes pour définir le chemin d'accès au fichier de configuration du cluster en tant que variable de session. L'interface CLI de Kubernetes utilise cette variable pour localiser un fichier de configuration local et les certificats requis pour connexion au cluster dans {{site.data.keyword.cloud_notm}}.

2. Editez le fichier *sysdig-agent-configmap.yaml*. 

    Exécutez la commande suivante :

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Effectuez les modifications. Ajoutez la section *events* ou mettez-la à jour.

    **Remarque :** Reportez-vous aux instructions de l'éditeur `vi` pour savoir comment effectuer des modifications.

    Par exemple, vous voudrez peut-être collecter des événements d'extraction de pod Kubernetes et filtrer d'autres événements de pod qui sont collectés par défaut. Vous souhaitez toujours collecter les événements Kubernetes par défaut pour les noeuds et les contrôleurs de réplication.

    ```
    events:
      kubernetes:
        pod:
          - Pulling
    ```
    {: codeblock}

4. Sauvegardez les modifications. 

Elles sont appliquées automatiquement. 


Un autre exemple vous permet de voir comment collecter un sous-ensemble d'événements Kubernetes : vous voulez uniquement surveiller les événements en cours d'extraction, extraits et en échec pour les pods.

* Option 1 : Définissez la séquence d'entrées sous forme de liste à puces :

    ```
    events:
      kubernetes:
        pod: 
          - Pulling
          - Pulled
          - Failed
    ```
    {: codeblock}

* Option 2 : Définissez la séquence d'entrées sur une seule ligne entre crochets :

    ```
    events:
      kubernetes:
        pod: [Pulling, Pulled, Failed]
    ```
    {: codeblock}

Pour plus d'informations sur l'utilisation d'événements personnalisés, voir [Utilisation des événements personnalisés ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/222822463/Custom+Events){:new_window}.


## Désactivation de la collecte d'événements
{: #change_kube_agent_disable_events}

Pour empêcher un agent Sysdig de collecter des événements Kubernetes, vous devez modifier le fichier *sysdig-agent-configmap.yaml*. Définissez l'entrée **Kubernetes** dans la section **events** sur *none*. 

Procédez comme suit :

1. Configurez l'environnement de cluster. Exécutez les commandes suivantes :

    Lancez d'abord la commande permettant de définir la variable d'environnement et téléchargez les fichiers de configuration Kubernetes.

    ```
    ibmcloud ks cluster-config <ID_ou_nom_cluster>
    ```
    {: codeblock}

    Une fois les fichiers de configuration téléchargés, une commande s'affiche ; elle vous permet de définir le chemin vers le fichier de configuration Kubernetes local en tant que variable d'environnement.

    Ensuite, copiez et collez la commande qui s'affiche sur votre terminal pour définir la variable d'environnement KUBECONFIG.

    **Remarque :** Chaque fois que vous vous connectez à l'interface CLI {{site.data.keyword.containerlong}} pour utiliser des clusters, vous devez exécuter ces commandes pour définir le chemin d'accès au fichier de configuration du cluster en tant que variable de session. L'interface CLI de Kubernetes utilise cette variable pour localiser un fichier de configuration local et les certificats requis pour connexion au cluster dans {{site.data.keyword.cloud_notm}}.

2. Editez le fichier *sysdig-agent-configmap.yaml*. 

    Exécutez la commande suivante :

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Effectuez les modifications. Ajoutez la section *events* ou mettez-la à jour.

    ```
    events:
      kubernetes: none
    ```
    {: codeblock}

6. Sauvegardez les modifications. 

Elles sont appliquées automatiquement. 






## Inclusion et exclusion de métriques
{: #change_kube_agent_inc_exc_metrics}

Pour filtrer des métriques personnalisées, vous devez personnaliser la section **metrics_filter** dans le fichier *sysdig-agent-configmap.yaml*. Vous pouvez indiquer les métriques à inclure et celles à filtrer en configurant les paramètres de filtrage **include** et **exclude**.

<p class="important">L'ordre des règles de filtrage est défini comme suit : la première règle correspondant à une métrique est appliquée. Les règles de suivi pour cette métrique sont ignorées.</p>

Procédez comme suit :

1. Configurez l'environnement de cluster. Exécutez les commandes suivantes :

    Lancez d'abord la commande permettant de définir la variable d'environnement et téléchargez les fichiers de configuration Kubernetes.

    ```
    ibmcloud ks cluster-config <ID_ou_nom_cluster>
    ```
    {: codeblock}

    Une fois les fichiers de configuration téléchargés, une commande s'affiche ; elle vous permet de définir le chemin vers le fichier de configuration Kubernetes local en tant que variable d'environnement.

    Ensuite, copiez et collez la commande qui s'affiche sur votre terminal pour définir la variable d'environnement KUBECONFIG.

    **Remarque :** Chaque fois que vous vous connectez à l'interface CLI {{site.data.keyword.containerlong}} pour utiliser des clusters, vous devez exécuter ces commandes pour définir le chemin d'accès au fichier de configuration du cluster en tant que variable de session. L'interface CLI de Kubernetes utilise cette variable pour localiser un fichier de configuration local et les certificats requis pour connexion au cluster dans {{site.data.keyword.cloud_notm}}.

2. Editez le fichier *sysdig-agent-configmap.yaml*. 

    Exécutez la commande suivante :

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Effectuez les modifications. Ajoutez la section *metrics_filter* ou mettez-la à jour.

    Par exemple, si la section *metrics_filter* d'un agent Sysdig se présente comme suit :

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

    * Vous configurez l'agent Sysdig pour qu'il collecte toutes les données provenant des métriques commençant par *metricA*, *metricB* et *haproxy.backend*. 

    * Vous filtrez les métriques commençant par *metricC* et d'autres métriques commençant par *haproxy*. 

    * L'entrée `exclude: metricA.*` est ignorée.

4. Sauvegardez les modifications. 

Elles sont appliquées automatiquement. 




## Filtrage de conteneurs et d'objets Kubernetes à partir desquels les données sont collectées
{: #change_kube_agent_filter_data}

Un agent Sysdig Kubernetes collecte automatiquement des métriques à partir de *tous les conteneurs* qu'il détecte dans un cluster, notamment Prometheus, StatsD, JMX, app-checks, ainsi que les métriques intégrées.
 
Vous pouvez personnaliser l'agent Sysdig pour exclure des conteneurs de la collecte de métriques. 

Lorsque vous excluez des conteneurs, prenez en compte les informations suivantes :
* Vous réduisez la charge de l'agent et du système de back end.
* Vous collectez uniquement les données provenant des conteneurs que vous souhaitez surveiller.
* Vous pouvez maîtriser les coûts en signalant les conteneurs importants et en filtrant les conteneurs inutiles ou non essentiels.

Pour activer la fonction de filtrage des conteneurs par un agent Sysdig, vous devez personnaliser le fichier *sysdig-agent-configmap.yaml*. Définissez l'entrée **use_container_filter** dans la section **containers** sur *true*. **Remarque :** Par défaut, cette fonction est désactivée. Définissez ensuite les règles incluant une ou plusieurs conditions à appliquer.

Le tableau suivant présente les paramètres permettant de définir les règles de filtrage dans un cluster :

| Paramètre                          | Condition                                      |
|------------------------------------|------------------------------------------------|
| `container.image`                  | Nom de l'image de conteneur                           |
| `container.name`                   | Nom du conteneur                                 |
| `container.label.*`                | Libellé du conteneur                                |
| `kubernetes.object.*`             | Objet Kubernetes. Il peut s'agir d'un pod, d'un espace de nom, etc.   |
| `kubernetes.object.annotation.*`  | Annotation d'objet Kubernetes                   |
| `kubernetes.object.label.*`       | Libellé d'objet Kubernetes                        |
| `all`                              | Règle par défaut pour spécifier tous les objets            |
{: caption="Tableau 2. Paramètres permettant de définir des conditions sur des conteneurs" caption-side="top"} 

Prenez en compte les informations suivantes en ce qui concerne la façon dont l'agent Sysdig applique les règles que vous définissez dans la section **container_filter** :
* Vous définissez des conditions en les configurant avec les paramètres de filtrage **include** et **exclude**. 
* La première règle correspondante dans la liste détermine si le conteneur est inclus ou exclu.
* Les conditions sont constituées d'un nom de clé et d'une valeur. Si la clé donnée pour un conteneur correspond à la valeur, la règle s'applique.
* Lorsqu'une règle contient plusieurs conditions, `toutes les conditions` doivent correspondre pour que la règle s'applique.

Procédez comme suit pour filtrer les conteneurs surveillés par un agent Sysdig dans un cluster :

1. Configurez l'environnement de cluster. Exécutez les commandes suivantes :

    Lancez d'abord la commande permettant de définir la variable d'environnement et téléchargez les fichiers de configuration Kubernetes.

    ```
    ibmcloud ks cluster-config <ID_ou_nom_cluster>
    ```
    {: codeblock}

    Une fois les fichiers de configuration téléchargés, une commande s'affiche ; elle vous permet de définir le chemin vers le fichier de configuration Kubernetes local en tant que variable d'environnement.

    Ensuite, copiez et collez la commande qui s'affiche sur votre terminal pour définir la variable d'environnement KUBECONFIG.

    **Remarque :** Chaque fois que vous vous connectez à l'interface CLI {{site.data.keyword.containerlong}} pour utiliser des clusters, vous devez exécuter ces commandes pour définir le chemin d'accès au fichier de configuration du cluster en tant que variable de session. L'interface CLI de Kubernetes utilise cette variable pour localiser un fichier de configuration local et les certificats requis pour connexion au cluster dans {{site.data.keyword.cloud_notm}}.

2. Editez le fichier *sysdig-agent-configmap.yaml*. 

    Exécutez la commande suivante :

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Effectuez les modifications. Ajoutez la section *metrics_filter* ou mettez-la à jour.

    Par exemple, voici un extrait d'une mappe de configuration :

    ```
    containers:
        # Enable the feature
        use_container_filter: true
        #
        # Include or exclude conditions
        container_filter:
           - include:
                container.image: 
           - include:
                container.name: 
           - exclude:
                kubernetes.namespace.name: kube-system
    ```  
    {: codeblock}

6. Sauvegardez les modifications. 

Elles sont appliquées automatiquement. 


## Blocage de ports
{: #change_kube_agent_block_ports}

Pour bloquer le trafic réseau et les métriques provenant de ports réseau, vous devez personnaliser la section **blacklisted_ports** dans le fichier *sysdig-agent-configmap.yaml*. Vous devez répertorier les ports à partir desquels vous voulez filtrer les données.

**Remarque :** Le port 53 (DNS) se trouve toujours sur liste noire. 

Procédez comme suit :

1. Configurez l'environnement de cluster. Exécutez les commandes suivantes :

    Lancez d'abord la commande permettant de définir la variable d'environnement et téléchargez les fichiers de configuration Kubernetes.

    ```
    ibmcloud ks cluster-config <ID_ou_nom_cluster>
    ```
    {: codeblock}

    Une fois les fichiers de configuration téléchargés, une commande s'affiche ; elle vous permet de définir le chemin vers le fichier de configuration Kubernetes local en tant que variable d'environnement.

    Ensuite, copiez et collez la commande qui s'affiche sur votre terminal pour définir la variable d'environnement KUBECONFIG.

    **Remarque :** Chaque fois que vous vous connectez à l'interface CLI {{site.data.keyword.containerlong}} pour utiliser des clusters, vous devez exécuter ces commandes pour définir le chemin d'accès au fichier de configuration du cluster en tant que variable de session. L'interface CLI de Kubernetes utilise cette variable pour localiser un fichier de configuration local et les certificats requis pour connexion au cluster dans {{site.data.keyword.cloud_notm}}.

2. Editez le fichier *sysdig-agent-configmap.yaml*. 

    Exécutez la commande suivante :

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Effectuez les modifications. Ajoutez la section *metrics_filter* ou mettez-la à jour.

    Par exemple, l'exemple suivant montre comment définir la section *blacklisted_ports* d'un agent Sysdig pour exclure les données provenant des ports 6666 et 6379 :

    ```
    blacklisted_ports:
      - 6666
      - 6379
    ```
    {: screen}

6. Sauvegardez les modifications. 

Elles sont appliquées automatiquement. 



## Modification du niveau de journalisation
{: #change_kube_agent_log_level}

Pour configurer le niveau de journalisation, vous devez personnaliser la section **log** dans le fichier *sysdig-agent-daemonset-v2.yaml*. 

L'agent Sysdig génère des entrées de journal dans */opt/draios/logs/draios.log*. 
* Le fichier journal pivote lorsque sa taille atteint 10 Mo.
* Les 10 derniers fichiers journaux sont conservés. L'horodatage qui est ajouté au nom de fichier permet de déterminer les fichiers à conserver.
* Les niveaux de journalisation valides sont les suivants : *none*, *error*, *warning*, *info*, *debug*, *trace*.
* Le niveau de journalisation par défaut est *info*, où une entrée est créée pour chaque transmission de métriques agrégées aux serveurs de back end, sur la base d'une par seconde, outre les entrées pour les avertissements et les erreurs.
* Vous pouvez personnaliser le type de journal et les entrées collectées en configurant le fichier de configuration de l'agent Sysdig **/opt/draios/etc/dragent.yaml**. Une fois le fichier modifié, vous devez redémarrer l'agent sur le shell avec `service dragent restart` pour
activer les modifications.

Le tableau suivant répertorie certains scénarios courants, ainsi que la valeur que vous devez définir dans chacun d'eux :

| Cas d'utilisation                                     | Entrée de section de journal           |
|-----------------------------------------------|-----------------------------|
| Traitement des incidents liés au comportement de l'agent                   | `file_priority: debug`      |
| Réduction de la sortie de la console de conteneur               | `console_priority: warning` |
| Filtrage des événements par gravité                  | `event_priority: warning`   |
| Vérification de l'inclusion ou de l'exclusion de métriques  | `metrics_excess_log: true`  |
{: caption="Tableau 2. Entrée de la section de journal" caption-side="top"} 

Pour configurer le niveau de journalisation, procédez comme suit :

1. Configurez l'environnement de cluster. Exécutez les commandes suivantes :

    Lancez d'abord la commande permettant de définir la variable d'environnement et téléchargez les fichiers de configuration Kubernetes.

    ```
    ibmcloud ks cluster-config <ID_ou_nom_cluster>
    ```
    {: codeblock}

    Une fois les fichiers de configuration téléchargés, une commande s'affiche ; elle vous permet de définir le chemin vers le fichier de configuration Kubernetes local en tant que variable d'environnement.

    Ensuite, copiez et collez la commande qui s'affiche sur votre terminal pour définir la variable d'environnement KUBECONFIG.

    **Remarque :** Chaque fois que vous vous connectez à l'interface CLI {{site.data.keyword.containerlong}} pour utiliser des clusters, vous devez exécuter ces commandes pour définir le chemin d'accès au fichier de configuration du cluster en tant que variable de session. L'interface CLI de Kubernetes utilise cette variable pour localiser un fichier de configuration local et les certificats requis pour connexion au cluster dans {{site.data.keyword.cloud_notm}}.

2. Editez le fichier *sysdig-agent-daemonset-v2.yaml*. 

    Exécutez la commande suivante :

    ```
    kubectl edit daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Effectuez les modifications. Ajoutez la section *log* ou mettez-la à jour.

    Par exemple, pour filtrer les événements de faible gravité (*notice*, *information*, *debug*), vous devez définir l'entrée **metrics_excess_log** dans la section **log** sur *true* :

    ```
    log:
      file_priority: warning
      console_priority: info
      event_priority: warning
      metrics_excess_log: true
    ```
    {: codeblock}

6. Sauvegardez les modifications. 

Elles sont appliquées automatiquement. 


## Filtrage des événements Kubernetes par gravité
{: #change_kube_agent_filterby_severity}

Pour filtrer des événements par gravité, vous devez modifier le fichier *sysdig-agent-daemonset-v2.yaml*. Définissez l'entrée **event_priority** dans la section **log** sur *none*. 

Le niveau de journalisation par défaut est **information**. Cela signifie que seuls les événements de type avertissement et de gravité supérieure sont transmis.

Les niveaux valides sont les suivants : *emergency*, *alert*, *critical*, *error*, *warning*, *notice*, *information*, *debug* et *none*. **Remarque** : Les valeurs sont répertoriées par ordre de priorité décroissant.

Procédez comme suit :

1. Configurez l'environnement de cluster. Exécutez les commandes suivantes :

    Lancez d'abord la commande permettant de définir la variable d'environnement et téléchargez les fichiers de configuration Kubernetes.

    ```
    ibmcloud ks cluster-config <ID_ou_nom_cluster>
    ```
    {: codeblock}

    Une fois les fichiers de configuration téléchargés, une commande s'affiche ; elle vous permet de définir le chemin vers le fichier de configuration Kubernetes local en tant que variable d'environnement.

    Ensuite, copiez et collez la commande qui s'affiche sur votre terminal pour définir la variable d'environnement KUBECONFIG.

    **Remarque :** Chaque fois que vous vous connectez à l'interface CLI {{site.data.keyword.containerlong}} pour utiliser des clusters, vous devez exécuter ces commandes pour définir le chemin d'accès au fichier de configuration du cluster en tant que variable de session. L'interface CLI de Kubernetes utilise cette variable pour localiser un fichier de configuration local et les certificats requis pour connexion au cluster dans {{site.data.keyword.cloud_notm}}.

2. Editez le fichier *sysdig-agent-daemonset-v2.yaml*. 

    Exécutez la commande suivante :

    ```
    kubectl edit daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Effectuez les modifications. Ajoutez la section *log* ou mettez-la à jour.

    Par exemple, pour filtrer les événements de faible gravité (*notice*, *information*, *debug*), vous devez définir la section de journal **event_priority** sur *warning* :

    ```
    log:
  event_priority: warning
    ```
    {: codeblock}

6. Sauvegardez les modifications. 

Elles sont appliquées automatiquement. 

## Journalisation des métriques incluses ou exclues dans un fichier
{: #change_kube_agent_log_metrics}

Pour journaliser dans un fichier les informations indiquant quelles métriques personnalisées sont incluses ou exclues, vous devez personnaliser le fichier *sysdig-agent-daemonset-v2.yaml*. Définissez l'entrée **metrics_excess_log** sur **true** dans la section **log**.

* La journalisation est désactivée par défaut. 
* La journalisation se produit au niveau INFO toutes les 30 secondes et dure 10 secondes. 
* Le fichier journal se trouve dans */opt/draios/logs/draios.log*.
* Les données de journalisation sont formatées comme suit :

    ```
    +/-[type][metric included/excluded]: metric.name (filter: +/-[metric.filter])
    ```
    {: screen}

    * Le symbole *+/-* indique si la métrique est incluse ou exclue. Le signe plus (*+*) indique qu'une métrique est incluse, tandis que le signe moins (*-*) indique qu'elle est exclue. 

    * *[type]* spécifie le type de métrique, par exemple, *statsd*.
    
    * *[metric included/excluded]* indique de façon lisible si la métrique est incluse ou exclue.

    *  *metric.name* indique le nom de la métrique.

    * *(filter: +/-[metric.filter])* fournit des informations sur les filtres définis dans la section **metrics_filter** du fichier *sysdig-agent-daemonset-v2.yaml*.

Voici un exemple d'entrée :

```
-[statsd] metric excluded: mongo.statsd.vsize (filter: -[mongo.statsd.*])
+[statsd] metric included: mongo.statsd.netIn (filter: +[mongo.statsd.net*])
```
{: screen}

Procédez comme suit :

1. Configurez l'environnement de cluster. Exécutez les commandes suivantes :

    Lancez d'abord la commande permettant de définir la variable d'environnement et téléchargez les fichiers de configuration Kubernetes.

    ```
    ibmcloud ks cluster-config <ID_ou_nom_cluster>
    ```
    {: codeblock}

    Une fois les fichiers de configuration téléchargés, une commande s'affiche ; elle vous permet de définir le chemin vers le fichier de configuration Kubernetes local en tant que variable d'environnement.

    Ensuite, copiez et collez la commande qui s'affiche sur votre terminal pour définir la variable d'environnement KUBECONFIG.

    **Remarque :** Chaque fois que vous vous connectez à l'interface CLI {{site.data.keyword.containerlong}} pour utiliser des clusters, vous devez exécuter ces commandes pour définir le chemin d'accès au fichier de configuration du cluster en tant que variable de session. L'interface CLI de Kubernetes utilise cette variable pour localiser un fichier de configuration local et les certificats requis pour connexion au cluster dans {{site.data.keyword.cloud_notm}}.

2. Editez le fichier *sysdig-agent-daemonset-v2.yaml*. 

    Exécutez la commande suivante :

    ```
    kubectl edit daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Effectuez les modifications. Ajoutez la section *log* ou mettez-la à jour.

    Par exemple, pour filtrer les événements de faible gravité (*notice*, *information*, *debug*), vous devez définir l'entrée **metrics_excess_log** dans la section **log** sur *true* :

    ```
    log:
      metrics_excess_log: true
    ```
    {: codeblock}

6. Sauvegardez les modifications. 

Elles sont appliquées automatiquement. 


## Exemple de fichier yaml configmap
{: #change_kube_agent_sample_configmap}

```
apiVersion: v1
data:
  dragent.yaml: | 
    ### Agent tags
    # tags: linux:ubuntu,dept:dev,local:nyc
    #### Sysdig Software related config 
    ####
    # Sysdig collector address
    # collector: 192.168.1.1
    # Collector TCP port
    # collector_port: 6666
    # Whether collector accepts ssl
    # ssl: true
    # collector certificate validation
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

## Exemple de fichier yaml daemonset
{: #change_kube_agent_sample_daemonset}

```
 Editez l'objet ci-après. Les lignes qui commencent par un '#' sont ignorées
# et un fichier vide annule l'édition. Si une erreur se produit lors de la sauvegarde,
# ce fichier est rouvert avec les incidents correspondants.
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

