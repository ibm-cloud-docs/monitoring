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


# Configuration d'une requête de métrique dans Grafana
{: #define_query}

Dans {{site.data.keyword.Bluemix}}, les métriques provenant de certains services de cloud sont automatiquement collectées. Pour les surveiller via {{site.data.keyword.monitoringlong}}, vous devez définir une requête Grafana. 
{:shortdesc}

## Etape 1 : Collecte de données pour l'application ou le service CF à surveiller
{: #step18}

Procurez-vous les informations suivantes pour l'application CF ou le service que vous souhaitez surveiller :

* **Région** dans laquelle l'application CF s'exécute.
* **Organisation** dans laquelle l'application CF s'exécute. 	
* **Espace** dans lequel l'application CF s'exécute. 
* **Nom de l'application CF** ou **nom du service** que vous souhaitez surveiller. 


## Etape 2 : Lancement de Grafana
{: #step27}

Démarrez Grafana depuis un navigateur. Pour plus d'informations, voir [Accès au tableau de bord Grafana depuis un navigateur Web](/docs/services/cloud-monitoring/grafana/navigating_grafana.html#launch_grafana_from_browser).

Assurez-vous que, dans Grafana, vous êtes connecté au compte, à l'organisation et à la région dans lesquels l'application CF ou le service s'exécute. 


## Etape 3 : Définition d'une requête dans Grafana
{: #step36}

Pour créer un tableau de bord Grafana et définir une requête, procédez comme suit :

1. Créez un tableau de bord.

    * Sélectionnez le bouton de basculement de la barre de menus latérale ![Barre de menus latérale de Grafana](images/grafana_settings.gif "Barre de menus latérale de Grafana").
    * Sélectionnez **Dashboards**.
    * Cliquez sur **New**.

    Un tableau de bord s'ouvre. Il comporte une ligne vide prête pour la configuration.

2. Ajoutez un panneau *Graph*.

    1. Sélectionnez **Graph**.

    2. Cliquez sur le titre du graphique, puis sélectionnez **edit**.

        L'onglet *Metrics* s'ouvre. Il affiche la source de données par défaut.

3. Définissez la requête qui filtre les données affichées dans le graphique. 

    Dans l'onglet *Metrics*, sélectionnez **Add query**. <br>Une entrée de requête est ajoutée. Chaque requête est associée à une lettre.
    
    ![Nouvelle entrée de requête](images/grafana4_query_f1.gif "Nouvelle entrée de requête")
        
    1. Cliquez sur **Select metric**, puis choisissez la source : `ibmcloud`.
    
    2. Cliquez sur **Select metric**, puis choisissez le type de cloud : `public`.
    
    3. Cliquez sur **Select metric**, puis choisissez le nom de service, par exemple, `cloud-foundry` pour les métriques d'application CF ou `message hub` pour les métriques {{site.data.keyword.messagehub}}.
    
    4. Cliquez sur **Select metric**, puis choisissez la région à partir de laquelle vous travaillez, par exemple, `ng` pour la région Sud des Etats-Unis.
    
    5. Sélectionnez les zones de service qui s'appliquent spécifiquement au service ou à l'application CF que vous souhaitez surveiller.

        <table>
          <caption>Formats de requête de métrique par service ou par application CF</caption>
          <tr>
            <th>Nom de service</th>
            <th>Lien vers le format de requête de métrique</th> 
          </tr>
          <tr>
            <td>{{site.data.keyword.containershort_notm}}</td>
            <td>[Format de requête des métriques d'unité centrale collectées pour les conteneurs](/docs/services/cloud-monitoring/reference/metrics_format_containers.html#cpu_containers) </br>[Format de requête des métriques de charge collectées pour les agents](/docs/services/cloud-monitoring/reference/metrics_format_containers.html#load_workers) </br>[Format de requête des métriques de mémoire collectées pour les conteneurs](/docs/services/cloud-monitoring/reference/metrics_format_containers.html#mem_containers)</td> 
          </tr>
          <tr>
            <td>Applications CF</td>
            <td>[Format de requête pour les applications CF](/docs/services/cloud-monitoring/reference/cfapps_metrics_format.html#cfapps_metrics_format)</td> 
          </tr>
        </table>

        Par exemple, pour une application CF, choisissez :
    
        Cliquez sur **Select metric**, puis choisissez le nom d'application CF, par exemple, `logtester`.
    
        Cliquez sur **Select metric**, puis choisissez l'index d'instance d'application CF, par exemple, `0`.

        Cliquez sur **Select metric**, puis choisissez `container`.
    
    9. Cliquez sur **Select metric**, puis choisissez un type de métrique. Par exemple, **cpu** pour des métriques d'unité centrale, **memory** pour des métriques de mémoire et **disk** pour des métriques de disque. 

        **Remarque :** ignorez cette étape pour les applications CF. 

    10. Cliquez sur **Select metric**, puis choisissez une métrique. 

        <table>
          <caption>Liste des métriques par service ou par application CF</caption>
          <tr>
            <th>Nom de service</th>
            <th>Lien vers des métriques</th> 
          </tr>
          <tr>
            <td>{{site.data.keyword.containershort_notm}}</td>
            <td>[Métriques d'unité centrale](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#cpu_metrics) </br>[Métriques de disque](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#disk_metrics) </br>[Métriques de mémoire](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#mem_metrics)</td> 
          </tr>
          <tr>
            <td>Applications CF</td>
            <td>[Métriques d'unité centrale](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#cpu_metrics)  </br>[Métriques de disque](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#disk_metrics)   </br>[Métriques de mémoire](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#mem_metrics)</td> 
          </tr>
          <tr>
            <td>{{site.data.keyword.messagehub}}</td>
            <td>[Métriques pour une rubrique Kafka](/docs/services/cloud-monitoring/mh/monitoring_mh_ov.html#kafka_topic_metrics) </br>[Métriques pour une partition Kafka](/docs/services/cloud-monitoring/mh/monitoring_mh_ov.html#kafka_partition_metrics)</td> 
          </tr>
        </table>

    10. Cliquez sur le signe plus ![Icône Ajouter](images/grafana_plus_image.gif "Signe Plus"), puis choisissez une fonction. Vous pouvez ajouter une fonction pour transformer et combiner des données disponibles pour une métrique, et effectuer des calculs sur ces données.
        
        Par exemple, vous pouvez ajouter la fonction **alias(newName)** afin d'ajouter un alias pour une métrique. Cet alias sera utilisé pour afficher une chaîne à la place du nom de la métrique dans la légende du graphique.
        
        Afin d'ajouter un alias pour votre métrique, procédez comme suit :
        
        1. Cliquez sur le signe plus.
        2. Sélectionnez **Special**. 
        3 Sélectionnez **alias**.
        4. Entrez une chaîne, par exemple `Mon exemple de métrique`.


## Etape 4 : Sauvegarde du tableau de bord en vue de sa réutilisation
{: #step44}

Procédez comme suit :

1. Cliquez sur l'icône de sauvegarde du tableau de bord ![Icône Sauvegarder le tableau de bord](images/grafana_save_image.gif "Icône Sauvegarder le tableau de bord").
2. Entrez le nom du tableau de bord.
3. Cliquez sur **Save**.
