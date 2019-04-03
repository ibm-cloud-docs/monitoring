---

copyright:
  years: 2017, 2019

lastupdated: "2019-03-06"

keywords: IBM Cloud, monitoring

subcollection: cloud-monitoring

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


# Création d'un tableau de bord Grafana pour surveiller un cluster Kubernetes
{: #container_grafana_dashboard}


Utilisez ce tutoriel pour apprendre à créer un tableau de bord Grafana dans le service {{site.data.keyword.monitoringlong}} afin de surveiller les performances de votre cluster. 
{:shortdesc}


## Objectifs
{: #cgd_objectives}

Apprenez à rechercher et à analyser des métriques de conteneur pour une application déployée dans un cluster Kubernetes :

1. Lancez Grafana et définissez le domaine {{site.data.keyword.monitoringshort}} dans lequel vous pourrez visualiser les métriques de cluster.
2. Créez un tableau de bord Grafana et définissez une métrique qui surveille l'utilisation de l'unité centrale par un conteneur.


## Hypothèses
{: #cgd_assumptions}

Les hypothèses du tutoriel sont les suivantes :

* Un cluster est disponible dans la région Sud des Etats-Unis. 
* Votre ID utilisateur contient une règle IAM pour le service {{site.data.keyword.monitoringshort}} avec des droits **viewer**.

Avant de suivre ce tutoriel, vous devez exécuter le tutoriel [Analyse des métriques dans Grafana pour une application qui est déployée dans un cluster Kubernetes](/docs/services/cloud-monitoring/tutorials/container_service_metrics.html#container_service_metrics) ou disposer d'un cluster mis à disposition avec au moins 1 application déployée.



## Etape 1 : Lancement de Grafana
{: #cgd_step1}

Lancez Grafana à partir d'un domaine et définissez le domaine {{site.data.keyword.monitoringshort}} dans lequel vous pourrez visualiser les métriques de cluster.

Pour analyser les métriques pour un cluster, vous devez accéder à Grafana dans la région publique du cloud où le cluster a été créé. Pour plus d'informations, voir [Accès au tableau de bord Grafana depuis un navigateur Web](/docs/services/cloud-monitoring/grafana/navigating_grafana.html#launch_grafana_from_browser).

1. A partir d'un navigateur, démarrez Grafana. 

    Entrez l'adresse URL du service {{site.data.keyword.monitoringshort}} pour la région où vous avez créé le cluster. 
    
    Pour obtenir les adresses URL par région, voir [URL pour le service de surveillance](/docs/services/cloud-monitoring/monitoring_ov.html#region).

    Par exemple, pour la région Sud des Etats-Unis, démarrez : [https://metrics.ng.bluemix.net/](https://metrics.ng.bluemix.net/).

2. Affectez au domaine {{site.data.keyword.monitoringshort}} la valeur **account**.

    Dans Grafana, sélectionnez votre ID. Ensuite, assurez-vous que vous êtes connecté au compte approprié, puis choisissez `Domain = account`.


## Etape 2 : Création d'un tableau de bord Grafana
{: #cgd_step2}

Pour créer un nouveau tableau de bord, procédez comme suit :

1. Sélectionnez le bouton de basculement de la barre de menus latérale ![Barre de menus latérale de Grafana](images/grafana_settings.gif "Barre de menus latérale de Grafana").
2. Sélectionnez **Dashboards**.
3. Cliquez sur **New**.

Un tableau de bord s'ouvre. Il comporte une ligne vide prête pour la configuration.

![Tableau de bord Grafana](images/grafana4_f1.gif "Tableau de bord Grafana")

Dans Grafana, ajoutez des lignes pour diviser le tableau de bord en sections. Une ligne regroupe un ou plusieurs panneaux. Dans une ligne, un panneau constitue l'unité de visualisation la plus petite que vous pouvez configurer pour l'affichage des données d'une métrique. Par exemple, vous pouvez choisir un panneau de graphique ou un panneau de tableau. Vous pouvez faire glisser des panneaux et les déposer à l'emplacement de votre choix afin de les réorganiser dans un tableau de bord. Les données affichées dans un panneau sont configurées via des requêtes. Vous pouvez définir une ou plusieurs requêtes dans un panneau. Chaque requête représente un ensemble différent de données. Vous pouvez aussi définir l'intervalle pour un panneau. Normalement, il est défini par le sélecteur de temps du *tableau de bord*.

## Etape 3 : Ajout d'un graphique au tableau de bord pour surveiller une métrique
{: #cgd_step3}

Procédez comme suit :

1. Sélectionnez **Graph**.

2. Cliquez sur le titre du graphique, puis sélectionnez **edit**.

    L'onglet *Metrics* s'ouvre. Il affiche la source de données par défaut.


![Panneau du graphique comportant des onglets de configuration](images/grafana4_f2.gif "Panneau du graphique comportant des onglets de configuration")


## Etape 4 : Définition d'une requête de métrique
{: #cgd_step4}

Définissez la requête qui filtre les données affichées dans le graphique. Cette requête surveille le nombre de nanosecondes du temps UC sur tous les coeurs d'un conteneur.

Pour plus d'informations sur le format de la requête, voir [Format de requête des métriques d'unité centrale collectées pour les conteneurs](/docs/services/cloud-monitoring/reference/metrics_format_containers.html#cpu_containers).
 
Dans l'onglet *Metrics*, sélectionnez **Add query**. <br>Une entrée de requête est ajoutée. Chaque requête est associée à une lettre. 

![Nouvelle entrée de requête](images/grafana4_query_f1.gif "Nouvelle entrée de requête") 
	
Procédez comme suit pour définir la requête :
        
1. Cliquez sur **Select metric** pour spécifier la source, puis choisissez `ibmcloud`.
    
2. Cliquez sur **Select metric** pour spécifier le type de cloud, puis choisissez `public`.
    
3. Cliquez sur **Select metric** pour indiquer le nom du service, puis sélectionnez `containers-kubernetes`.
	
4. Cliquez sur **Select metric** pour spécifier la région, puis choisissez la région dans laquelle votre cluster s'exécute. Par exemple, `us-south`.
    
5. Cliquez sur **Select metric** pour spécifier le nom de cluster, puis choisissez le nom du cluster dans lequel votre conteneur s'exécute.
		
6. Cliquez sur **Select metric** pour spécifier la source de métriques. Sélectionnez **container**.
		
7. Cliquez sur **Select metric** pour spécifier les espace-noms. Entrez ensuite le nom de l'espace-noms dans votre cluster qui est associé à votre conteneur.
		
8. Cliquez sur **Select metric** pour spécifier le nom de pod.
	
9. Cliquez sur **Select metric** pour spécifier le nom du conteneur à surveiller.
	
10. Cliquez sur **Select metric** pour spécifier le type de métrique, puis cliquez sur **Select metric** pour spécifier le sous-type de métrique.
	
    Par exemple, pour surveiller le nombre de nanosecondes du temps UC sur tous les coeurs pour un conteneur, sélectionnez **cpu** pour le type et **usage** pour le sous-type.
		
	Pour obtenir une liste de métriques d'unité centrale, voir [Métriques d'unité centrale pour les conteneurs](/docs/services/cloud-monitoring/containers/monitoring_containers_ov.html#cpu_metrics_containers).
    
11. Cliquez sur le signe plus ![Icône Ajouter](images/grafana_plus_image.gif "Signe Plus"), puis choisissez une fonction. Vous pouvez ajouter une fonction pour transformer et combiner des données disponibles pour une métrique, et effectuer des calculs sur ces données.

    Par exemple, vous pouvez ajouter la fonction **alias(newName)** afin d'ajouter un alias pour une métrique. Cet alias sera utilisé pour afficher une chaîne à la place du nom de la métrique dans la légende du graphique.

    Afin d'ajouter un alias pour votre métrique, procédez comme suit :

    1. Cliquez sur le signe plus.
    2. Sélectionnez **Special**.
    3 Sélectionnez **alias**.
    4. Entrez une chaîne, par exemple `Mon exemple de métrique`.

## Etape 5 : Sauvegarde du tableau de bord
{: #cgd_step5}

Sauvegardez le tableau de bord en vue de sa réutilisation ultérieure.

1. Cliquez sur l'icône de sauvegarde du tableau de bord ![Icône Sauvegarder le tableau de bord](images/grafana_save_image.gif "Icône Sauvegarder le tableau de bord").

    ![Sauvegarder le tableau de bord](images/grafana_save_dashboard.gif "Sauvegarder le tableau de bord")

2. Entrez le nom du tableau de bord.
3. Cliquez sur **Save**.



## Etapes suivantes
{: #cgd_next_steps}

Définissez une alerte pour une métrique. Pour plus d'informations, voir [Configuration d'alertes](/docs/services/cloud-monitoring/config_alerts_ov.html#config_alerts_ov).
