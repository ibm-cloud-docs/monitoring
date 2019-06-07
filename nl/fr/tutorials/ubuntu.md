---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, ubuntu, analyze metrics

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


# Analyser les métriques d'un hôte Ubuntu
{: #ubuntu}

Utilisez ce tutoriel pour apprendre à configurer un hôte Ubuntu en vue de transmettre des métriques au service {{site.data.keyword.mon_full_notm}} dans {{site.data.keyword.cloud_notm}}.
{:shortdesc}

Pour configurer un serveur Ubuntu pour la transmission de métriques, vous devez installer un agent Sysdig. L'agent utilise une clé d'accès (jeton) pour s'authentifier sur l'instance {{site.data.keyword.mon_full_notm}}. L'agent Sysdig fait office de collecteur de données. Il collecte automatiquement les métriques.

Vous pouvez afficher des métriques via l'interface utilisateur Web de Sysdig.

![Présentation des composants sur {{site.data.keyword.cloud_notm}}](../images/ubuntu.png "Présentation des composants sur {{site.data.keyword.cloud_notm}}")



## Avant de commencer
{: #ubuntu_prereqs}

Travaillez dans la région Sud des Etats-Unis. 

Documentez-vous sur {{site.data.keyword.mon_full_notm}}. Pour plus d'informations, voir [A propos de](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-about#about).

Utilisez un ID utilisateur qui soit membre ou propriétaire d'un compte {{site.data.keyword.cloud_notm}}. Pour obtenir un ID utilisateur {{site.data.keyword.cloud_notm}}, accédez à [Inscription ![Icône de lien externe](../../../icons/launch-glyph.svg "Icône delien externe")](https://cloud.ibm.com/login){:new_window}.


Des règles IAM doivent être affectées à votre {{site.data.keyword.IBM_notm}}ID pour chacune des ressources suivantes : 

| Ressource                             | Portée de la règle d'accès | Rôle    | Région    | Informations                  |
|--------------------------------------|----------------------------|---------|-----------|------------------------------|
| Groupe de ressources **par défaut**           |  Groupe de ressources            | Afficheur  | `Sud des Etats-Unis`  | Cette règle est requise pour permettre à l'utilisateur de voir les instances de service dans le groupe de ressources par défaut.    |
| Service {{site.data.keyword.mon_full_notm}} |  Groupe de ressources            | Editeur  | `Sud des Etats-Unis`  | Cette règle est requise pour permettre à l'utilisateur de mettre à disposition et d'administrer le service {{site.data.keyword.mon_full_notm}} dans le groupe de ressources par défaut.   |
{: caption="Tableau 1. Liste des règles IAM requises pour l'exécution du tutoriel" caption-side="top"} 

Installez l'interface de ligne de commande {{site.data.keyword.cloud_notm}}. Pour plus d'informations, voir [Installation de l'interface de ligne de commande {{site.data.keyword.cloud_notm}}.](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli)


## Etape 1. Mise à disposition d'une instance {{site.data.keyword.mon_full_notm}}
{: #ubuntu_step1}

Pour mettre à disposition une instance {{site.data.keyword.mon_full_notm}} via l'interface utilisateur {{site.data.keyword.cloud_notm}}, procédez comme suit :

1. [Connectez-vous à votre compte {{site.data.keyword.cloud_notm}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/login){:new_window}.

	Une fois que vous êtes connecté avec votre ID utilisateur et votre mot de passe, l'interface utilisateur {{site.data.keyword.cloud_notm}} s'ouvre.

2. Cliquez sur **Catalogue**. La liste des services disponibles dans {{site.data.keyword.cloud_notm}} s'affiche.

3. Pour filtrer la liste de services qui s'affiche, sélectionnez la catégorie **Developer Tools**.

4. Cliquez sur la vignette **{{site.data.keyword.mon_full_notm}}**. Le tableau de bord *Observabilité* s'ouvre.

5. Sélectionnez **Créer une instance**. 

6. Saisissez un nom pour l'instance de service.

7. Sélectionnez le groupe de ressources **par défaut**. 

    Le groupe de ressources **par défaut** est défini automatiquement.

8. Sélectionnez le plan de service **Lite**. 

    Le plan **Lite** est défini par défaut.

    Pour plus d'informations sur les autres plans de service, voir [Plans de tarification](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-pricing_plans#pricing_plans).

9. Pour mettre à disposition le service {{site.data.keyword.mon_full_notm}} dans le groupe de ressources {{site.data.keyword.cloud_notm}} auquel vous êtes connecté, cliquez sur **Créer**.

Après avoir mis à disposition une instance, le tableau de bord *Observabilité* s'ouvre. 


**Remarque :** Pour mettre à disposition une instance via l'interface de ligne de commande, voir [Mise à disposition d'une instance via l'interface
de ligne de commande {{site.data.keyword.cloud_notm}}](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-provision#provision_cli).


## Etape 2. Configuration de votre serveur Ubuntu pour envoyer des métriques à votre instance
{: #ubuntu_step2}

Pour configurer votre serveur Ubuntu pour qu'il envoie des métriques à votre instance {{site.data.keyword.mon_full_notm}}, vous devez installer un agent Sysdig. 

Procédez comme suit à partir de la ligne de commande :

1. Ouvrez un terminal. Ensuite, connectez-vous à {{site.data.keyword.cloud_notm}}. Exécutez la commande suivante et suivez les invites :

    ```
    ibmcloud login -a cloud.ibm.com
    ```
    {: codeblock}

    Sélectionnez le compte où l'instance {{site.data.keyword.mon_full_notm}} est disponible.

2. Obtenez la clé d'accès Sysdig. Pour plus d'informations, voir [Obtention de la clé d'accès via l'interface utilisateur {{site.data.keyword.cloud_notm}}](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui).

3. Obtenez l'URL d'ingestion. Pour plus d'informations, voir [Noeuds finaux de collecteur Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion).

4. Déployez l'agent Sysdig. Exécutez la commande suivante :

    ```
    curl -s https://s3.amazonaws.com/download.draios.com/stable/install-agent | sudo bash -s -- --access_key SYSDIG_ACCESS_KEY --collector COLLECTOR_ENDPOINT --collector_port 6443 --secure false --check_certificate false --tags TAG_DATA --additional_conf 'sysdig_capture_enabled: false'
    ```
    {: codeblock}

    où

    * SYSDIG_ACCESS_KEY est la clé d'ingestion pour l'instance.

    * COLLECTOR_ENDPOINT est l'URL d'ingestion pour la région où se trouve l'instance de surveillance.

    * TAG_DATA sont des étiquettes séparées par une virgule qui se présentent sous la forme *TAG_NAME:TAG_VALUE*. Vous pouvez associer une ou plusieurs étiquettes à votre agent Sysdig. Par exemple, *role:serviceX,location:us-south*. Vous pouvez utiliser ces étiquettes ultérieurement pour identifier les métriques provenant de l'environnement où l'agent s'exécute.

    * Définissez **sysdig_capture_enabled** sur *false* pour désactiver la fonction de capture Sysdig. La valeur par défaut est *true*. Pour plus d'informations, voir [Utilisation des captures](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures).

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



## Etape 3. Lancement de l'interface utilisateur Web Sysdig
{: #ubuntu_step3}

Pour lancer l'interface utilisateur Web, procédez comme suit :

1. [Connectez-vous à votre compte {{site.data.keyword.cloud_notm}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/login){:new_window}.

	Une fois que vous êtes connecté avec votre ID utilisateur et votre mot de passe, le tableau de bord {{site.data.keyword.cloud_notm}} s'ouvre.

2. Dans le menu de navigation, sélectionnez **Observabilité**. 

3. Sélectionnez **Surveillance**. 

    La liste des instances disponibles sur {{site.data.keyword.cloud_notm}} s'affiche.

4. Sélectionnez votre instance. Cliquez ensuite sur **Afficher Sysdig**.

Si l'agent Sysdig est configuré correctement, la vue *EXPLORE* s'ouvre.

Cependant, si l'agent Sysdig n'est pas installé correctement, pointe vers le mauvais noeud final d'ingestion ou que la clé d'accès est incorrecte, la page qui s'ouvre vous informe de la procédure à suivre.

Vous ne pouvez avoir qu'une seule session d'interface utilisateur Web ouverte par navigateur.
{: tip}


## Etape 4. Surveillance de votre serveur Ubuntu
{: #ubuntu_step4}

Vous pouvez surveiller votre serveur Ubuntu dans la vue **EXPLORE**, qui est disponible via l'interface utilisateur Web. Cette vue est le point de départ pour identifier et surveiller votre infrastructure. Il s'agit de la page d'accueil par défaut de l'interface utilisateur Web pour les utilisateurs.

La section *Host and containers* contient l'entrée pour votre serveur Ubuntu. Cliquez sur **Host and containers** ![Host and containers](../images/switch_hosts.png) pour basculer entre les sources de données. Ensuite, sélectionnez votre serveur Ubuntu. Les données affichées correspondent au serveur Ubuntu que vous sélectionnez.

Par exemple, pour configurer le codage couleur pour une colonne, procédez comme suit :

1. Sélectionnez une colonne. Déplacez la souris sur le titre de la colonne. Ensuite, sélectionnez l'icône en forme de crayon.
2. Activez la barre pour activer le codage couleur.
3. Définissez des valeurs pour les différents seuils.



## Etapes suivantes
{: #ubuntu_next_steps}

Créez un tableau de bord personnalisé. Pour plus d'informations, voir [Utilisation des tableaux de bord](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards).

Vous pouvez également obtenir des informations sur les alertes. Pour plus d'informations, voir [Utilisation des alertes](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-monitoring#monitoring_alerts). 






