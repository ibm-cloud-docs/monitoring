---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, kubernetes, analyze metrics

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


# Analyser les métriques d'une application déployée dans un cluster Kubernetes
{: #kubernetes_cluster}

Utilisez ce tutoriel pour apprendre à configurer un cluster en vue de transmettre des métriques au service {{site.data.keyword.mon_full_notm}} dans {{site.data.keyword.cloud_notm}}.
{:shortdesc}

Vous pouvez utiliser le service {{site.data.keyword.mon_full_notm}} pour surveiller des clusters Kubernetes.

Pour configurer un cluster pour la transmission de métriques, vous devez installer un agent sur chaque noeud worker dans votre cluster Kubernetes à l'aide d'un DaemonSet. L'agent Sysdig utilise une clé d'accès (jeton) pour s'authentifier sur l'instance {{site.data.keyword.mon_full_notm}}. L'agent Sysdig fait office de collecteur de données. Il collecte automatiquement des métriques telles que l'*UC worker* et la mémoire worker*, *le trafic HTTP entrant et sortant de vos conteneurs*, et plusieurs composants du logiciel d'infrastructure commun. En outre, l'agent peut collecter des métriques d'application personnalisées à l'aide d'un scraper compatible avec Prometheus ou d'une façade statsd. 

Vous pouvez afficher des métriques via l'interface utilisateur Web de Sysdig.

![Présentation des composants sur {{site.data.keyword.cloud_notm}}](../images/kube.png "Présentation des composants sur {{site.data.keyword.cloud_notm}}")



## Avant de commencer
{: #kubernetes_cluster_prereqs}

Pour exécuter la procédure de ce tutoriel d'initiation, des instructions sont fournies pour la mise à disposition d'une instance {{site.data.keyword.mon_full_notm}} dans la région Sud des Etats-Unis. Vous pouvez utiliser un cluster existant ou un nouveau **cluster version 1.10**. Le cluster peut être disponible dans une autre région.  

Documentez-vous sur {{site.data.keyword.mon_full_notm}}. Pour plus d'informations, voir [A propos de](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-about#about).

Utilisez un ID utilisateur qui soit membre ou propriétaire d'un compte {{site.data.keyword.cloud_notm}}. Pour obtenir un ID utilisateur {{site.data.keyword.cloud_notm}}, accédez à [Inscription ![Icône de lien externe](../../../icons/launch-glyph.svg "Icône delien externe")](https://cloud.ibm.com/login){:new_window}.


Des règles IAM doivent être affectées à votre {{site.data.keyword.IBM_notm}}ID pour chacune des ressources suivantes : 

| Ressource                             | Portée de la règle d'accès | Rôle    | Région    | Informations                  |
|--------------------------------------|----------------------------|---------|-----------|------------------------------|
| Groupe de ressources **par défaut**           |  Groupe de ressources            | Afficheur  | us-south  | Cette règle est requise pour permettre à l'utilisateur de voir les instances de service dans le groupe de ressources par défaut.    |
| Service {{site.data.keyword.mon_full_notm}} |  Groupe de ressources            | Editeur  | us-south  | Cette règle est requise pour permettre à l'utilisateur de mettre à disposition et d'administrer le service {{site.data.keyword.mon_full_notm}} dans le groupe de ressources par défaut.   |
| Instance de cluster Kubernetes          |  Ressource                 | Editeur  | us-south  | Cette règle est requise pour configurer la valeur confidentielle et l'agent Sysdig dans le cluster Kubernetes. |
{: caption="Tableau 1. Liste des règles IAM requises pour l'exécution du tutoriel" caption-side="top"} 

Pour plus d'informations sur les rôles IAM {{site.data.keyword.containerlong}}, voir [Droits d'accès utilisateur](/docs/containers?topic=containers-access_reference#access_reference).

Installez l'interface CLI {{site.data.keyword.cloud_notm}} et le plug-in d'interface de ligne de commande Kubernetes. Pour plus d'informations, voir [Installation de l'interface de ligne de commande {{site.data.keyword.cloud_notm}}.](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli)


## Etape 1 : Mise à disposition d'une instance {{site.data.keyword.mon_full_notm}}
{: #kubernetes_cluster_step1}

Pour mettre à disposition une instance {{site.data.keyword.mon_full_notm}} via l'interface utilisateur {{site.data.keyword.cloud_notm}}, procédez comme suit :

1. Connectez-vous à votre compte {{site.data.keyword.cloud_notm}}.

    Cliquez sur le tableau de bord [{{site.data.keyword.cloud_notm}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/login){:new_window} pour lancer le tableau de bord {{site.data.keyword.cloud_notm}}.

	Une fois que vous êtes connecté avec votre ID utilisateur et votre mot de passe, l'interface utilisateur {{site.data.keyword.cloud_notm}} s'ouvre.

2. Cliquez sur **Catalogue**. La liste des services disponibles dans {{site.data.keyword.cloud_notm}} s'affiche.

3. Pour filtrer la liste de services qui s'affiche, sélectionnez la catégorie **Developer Tools**.

4. Cliquez sur la vignette **{{site.data.keyword.mon_full_notm}}**. Le tableau de bord *Observabilité* s'ouvre.

5. Sélectionnez **Créer une instance**. 

6. Saisissez un nom pour l'instance de service.

7. Sélectionnez le groupe de ressources **par défaut**. 

    Le groupe de ressources **par défaut** est défini automatiquement.

8. Sélectionnez le plan de service **Essai**. 

    Par défaut, le plan **Essai** est défini.

    Pour plus d'informations sur les autres plans de service, voir [Plans de tarification](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-pricing_plans#pricing_plans).

9. Pour mettre à disposition le service {{site.data.keyword.mon_full_notm}} dans le groupe de ressources {{site.data.keyword.cloud_notm}} auquel vous êtes connecté, cliquez sur **Créer**.

Après avoir mis à disposition une instance, le tableau de bord *Observabilité* s'ouvre. 


**Remarque :** Pour mettre à disposition une instance via l'interface de ligne de commande, voir [Mise à disposition d'une instance via l'interface
de ligne de commande {{site.data.keyword.cloud_notm}}](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-provision#provision_cli).


## Etape 2 : Configuration de votre cluster Kubernetes pour envoyer des métriques à votre instance
{: #kubernetes_cluster_step2}

Pour configurer votre cluster Kubernetes pour qu'il envoie des métriques à votre instance {{site.data.keyword.mon_full_notm}}, vous devez installer un pod d'agent Sysdig sur chaque noeud de votre cluster. L'agent Sysdig est installé via un DaemonSet qui vérifie qu'une instance de l'agent s'exécute sur chaque noeud worker. L'agent Sysdig collecte des métriques à partir du pod où il est installé, puis les transmet à votre instance.

**Remarque :** Pour fournir la suite complète des métriques système, l'agent Sysdig doit disposer d'un statut privilégié.

Pour configurer votre cluster Kubernetes pour qu'il transmette des métriques à votre instance {{site.data.keyword.mon_full_notm}}, procédez comme suit à partir de la ligne de commande :

1. Ouvrez un terminal. Ensuite, connectez-vous à {{site.data.keyword.cloud_notm}}. Exécutez la commande suivante et suivez les invites :

    ```
    ibmcloud login -a api.ng.bluemix.net
    ```
    {: codeblock}

    Sélectionnez le compte où vous avez mis à disposition l'instance {{site.data.keyword.mon_full_notm}}.

2. Configurez l'environnement de cluster. Exécutez les commandes suivantes :

    Lancez d'abord la commande permettant de définir la variable d'environnement et téléchargez les fichiers de configuration Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Une fois les fichiers de configuration téléchargés, une commande s'affiche ; elle vous permet de définir le chemin vers le fichier de configuration Kubernetes local en tant que variable d'environnement.

    Ensuite, copiez et collez la commande qui s'affiche sur votre terminal pour définir la variable d'environnement KUBECONFIG.

    **Remarque :** Chaque fois que vous vous connectez à l'interface CLI {{site.data.keyword.containerlong}} pour utiliser des clusters, vous devez exécuter ces commandes pour définir le chemin d'accès au fichier de configuration du cluster en tant que variable de session. L'interface CLI de Kubernetes utilise cette variable pour localiser un fichier de configuration local et les certificats requis pour connexion au cluster dans {{site.data.keyword.cloud_notm}}.

3. Obtenez la clé d'accès Sysdig. Pour plus d'informations, voir [Obtention de la clé d'accès via l'interface utilisateur {{site.data.keyword.cloud_notm}}](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui).

4. Obtenez l'URL d'ingestion. Pour plus d'informations, voir [Noeuds finaux de collecteur Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion).

5. Déployez l'agent Sysdig. Exécutez la commande suivante :

    ```
    curl -sL https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/IBMCloud-Kubernetes-Service/install-agent-k8s.sh | bash -s -- -a SYSDIG_ACCESS_KEY -c COLLECTOR_ENDPOINT -t TAG_DATA -ac 'sysdig_capture_enabled: false'
    ```
    {: codeblock}

    où

    * SYSDIG_ACCESS_KEY est la clé d'ingestion pour l'instance.

    * COLLECTOR_ENDPOINT est l'URL d'ingestion pour la région où se trouve l'instance de surveillance.

    * TAG_DATA sont des étiquettes séparées par une virgule qui se présentent sous la forme *TAG_NAME:TAG_VALUE*. Vous pouvez associer une ou plusieurs étiquettes à votre agent Sysdig. Exemple : *role:serviceX,location:us-south*. Vous pouvez utiliser ces étiquettes ultérieurement pour identifier les métriques provenant de l'environnement où l'agent s'exécute.

    * Définissez **sysdig_capture_enabled** sur *false* pour désactiver la fonction de capture Sysdig. La valeur par défaut est *true*. Pour plus d'informations, voir [Utilisation des captures](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures).

6. Vérifiez que l'agent Sysdig a été créé, ainsi que son statut. Exécutez la commande suivante :

    ```
    kubectl get pods
    ```
    {: codeblock}



## Etape 3 : Lancement de l'interface utilisateur Web Sysdig
{: #kubernetes_cluster_step3}

Pour lancer l'interface utilisateur Web, procédez comme suit :

1. Connectez-vous à votre compte {{site.data.keyword.cloud_notm}}.

    Cliquez sur le tableau de bord [{{site.data.keyword.cloud_notm}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/login){:new_window} pour lancer le tableau de bord {{site.data.keyword.cloud_notm}}.

	Une fois que vous êtes connecté avec votre ID utilisateur et votre mot de passe, le tableau de bord {{site.data.keyword.cloud_notm}} s'ouvre.

2. Dans le menu de navigation, sélectionnez **Observabilité**. 

3. Sélectionnez **Surveillance**. 

    La liste des instances disponibles sur {{site.data.keyword.cloud_notm}} s'affiche.

4. Sélectionnez votre instance. Cliquez ensuite sur **Afficher Sysdig**.

Si l'agent Sysdig est configuré correctement, la vue *EXPLORE* s'ouvre.

Cependant, si l'agent Sysdig n'est pas installé correctement, pointe vers le mauvais noeud final d'ingestion ou que la clé d'accès est incorrecte, la page qui s'ouvre vous informe de la procédure à suivre.

Une seule session d'interface utilisateur Web peut s'ouvrir par navigateur.
{: tip}


## Etape 4 : Surveillance de votre cluster
{: #kubernetes_cluster_step4}

Vous pouvez surveiller votre cluster dans la vue **EXPLORE**, qui est disponible via l'interface utilisateur Web. Cette vue est le point de départ pour identifier et surveiller votre infrastructure. Il s'agit de la page d'accueil par défaut de l'interface utilisateur Web pour les utilisateurs.

La section *Host and containers* contient la liste des noeuds worker de votre cluster qui transmettent des métriques à l'instance de surveillance. Chaque entrée de noeud worker représente un groupe d'objets d'infrastructure connexes pour ce noeud worker.

Cliquez sur **Host and containers** ![Host and containers](../images/switch_hosts.png) pour basculer entre les sources de données. Ensuite, sélectionnez un noeud worker. Les données affichées correspondent au noeud worker que vous avez sélectionné.

Si vous cliquez sur **Back to Explore Table**, le *tableau Explore* s'affiche. Chaque colonne contient une métrique différente. Vous pouvez configurer chaque métrique individuellement. Vous pouvez modifier l'ordre des colonnes. Notez que lorsque vous apportez des modifications à l'ordre des colonnes existantes, la modification demeure sur les différents regroupements tant que vous êtes connecté. Si vous ajoutez ou supprimez une colonne, la modification est permanente. Vous pouvez également configurer des couleurs pour mettre en évidence des valeurs et améliorer la lisibilité.

Par exemple, pour configurer le codage couleur pour une colonne, procédez comme suit :

1. Sélectionnez une colonne. Déplacez la souris sur le titre de la colonne. Ensuite, sélectionnez l'icône en forme de crayon.
2. Activez la barre pour activer le codage couleur.
3. Définissez des valeurs pour les différents seuils.

Si vous sélectionnez un noeud worker, un tableau de bord s'affiche par défaut. Cliquez sur ![changement de tableau de bord](images/switch_dashboards_1.png) et explorez les différents tableaux de bord et métriques par défaut. Notez que vous pouvez uniquement sélectionner des métriques et tableaux de bord qui sont pertinents pour le noeud worker sélectionné.


## Etapes suivantes
{: #kubernetes_cluster_next_steps}

Créez un tableau de bord personnalisé. Pour plus d'informations, voir [Utilisation des tableaux de bord](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards).

Vous pouvez également obtenir des informations sur les alertes. Pour plus d'informations, voir [Utilisation des alertes](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-monitoring#monitoring_alerts). 






