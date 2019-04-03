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


# Analyse des métriques dans Grafana pour une application CF
{: #cfapps_metrics}

Utilisez ce tutoriel pour apprendre à utiliser le service {{site.data.keyword.monitoringlong}} afin de surveiller les performances d'une application Cloud Foundry (CF) qui s'exécute dans l'environnement de cloud {{site.data.keyword.Bluemix_notm}} public. 
{:shortdesc}


## Objectifs
{: #objectives}

Apprenez à rechercher et à analyser des métriques pour une application CF :

1. Déployez une application CF.
2. Lancez Grafana et définissez le domaine {{site.data.keyword.monitoringshort}} dans lequel vous pourrez visualiser les métriques d'application CF.
3. Recherchez et analysez des métriques pour une application CF qui s'exécute dans un espace {{site.data.keyword.Bluemix_notm}}.

Ce tutoriel part du principe que vous travaillez dans la région Sud des Etats-Unis.


## Prérequis
{: #cfapps_prereqs}

1. Etre membre ou propriétaire d'un compte {{site.data.keyword.Bluemix_notm}} doté des droits permettant de mettre à disposition des services dans un espace, de déployer des applications CF et d'interroger des métriques dans {{site.data.keyword.Bluemix_notm}} via le service {{site.data.keyword.monitoringshort}}.

    Votre ID utilisateur pour {{site.data.keyword.Bluemix_notm}} doit posséder un rôle CF pour l'espace où le service {{site.data.keyword.monitoringshort}} et l'application CF sont mis à disposition. Le rôle requis est *developer*.
    
    Pour plus d'informations, voir [Octroi d'un rôle CF à un utilisateur à l'aide de l'interface utilisateur IBM Cloud](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-grant_permissions#grant_permissions_ui_space).

2. Mettez à disposition le service {{site.data.keyword.monitoringshort}} dans un espace sur lequel vous disposez des droits vous permettant de mettre des services à disposition dans la région Sud des Etats-Unis.

    Pour plus d'informations, voir [Mise à disposition du service {{site.data.keyword.monitoringshort}}](/docs/services/cloud-monitoring/how-to?topic=cloud-monitoring-provision#provision).

## Etape 1 : Octroi des droits permettant à votre utilisateur de gérer des applications CF et le service {{site.data.keyword.monitoringshort}}
{: #cfapps_step1}

Pour autoriser un utilisateur à déployer des applications CF dans un espace ou à afficher des métriques dans un domaine d'espace, vous devez affecter à cet utilisateur un rôle CF qui décrit les actions qu'il peut exécuter avec le service {{site.data.keyword.monitoringshort}} dans l'espace et dans {{site.data.keyword.Bluemix_notm}}. 

**Remarque :** ce tutoriel part du principe que vous êtes le propriétaire de compte ou que vous possédez les droits requis pour ajouter des rôles à votre ID utilisateur. Si vous ne possédez pas ces droits, demandez au propriétaire d'effectuer cette étape.

Pour autoriser un utilisateur à suivre le tutoriel, procédez comme suit :

1. Connectez vous à la console {{site.data.keyword.Bluemix_notm}}.

    Ouvrez un navigateur Web et lancez le tableau de bord {{site.data.keyword.Bluemix_notm}} : [http://bluemix.net ![Icône de lien externe](../../../icons/launch-glyph.svg "Icône de lien externe")](http://bluemix.net){:new_window}
	
	Après que vous vous êtes connecté avec votre ID utilisateur et votre mot de passe, l'interface utilisateur {{site.data.keyword.Bluemix_notm}} s'ouvre.

2. Dans la barre de menus, cliquez sur **Gérer > Compte > Utilisateurs**. 

    La fenêtre *Utilisateurs* affiche une liste d'utilisateurs avec leur adresse électronique pour le compte actuellement sélectionné.
	
3. Recherchez votre nom d'utilisateur dans la liste, puis cliquez sur **Gérer un utilisateur** dans le menu *Actions*.

4. Sélectionnez **Accès Cloud Foundry**, puis sélectionnez **Affecter une organisation**.

5. Entrez les valeurs suivantes : 

    <table>
      <caption>Liste des valeurs à sélectionner</caption>
      <tr>
        <th>Zone</th>
        <th>Valeur</th>
      </tr>
      <tr>
        <td>Organisation</td>
        <td>MyOrg</td>
      </tr>
      <tr>
        <td>Rôle d'organisation</td>
        <td>Aucun rôle d'organisation</td>
      </tr>
      <tr>
        <td>Région</td>
        <td>Sud des Etats-Unis</td>
      </tr>
      <tr>
        <td>Espace</td>
        <td>dev</td>
      </tr>
      <tr>
        <td>Rôle d'espace</td>
        <td>développeur</td>
      </tr>
    </table>
	
6. Cliquez sur **Sauvegarder un rôle**.
 

## Etape 2 : Déploiement d'une application CF
{: #cfapps_step2}

Effectuez les opérations suivantes à partir de la console {{site.data.keyword.Bluemix_notm}} :

1. Cliquez sur **Catalogue** dans la barre d'outils {{site.data.keyword.Bluemix_notm}}.

2. Cliquez sur **Applications Cloud Foundry > Liberty for Java**. 

3. Entrez les informations suivantes :

    * **Nom d'application** : Nom de l'application. Doit être unique.
    * **Région** : Choisissez Sud des Etats-Unis.
    * **Organisation** : Choisissez l'organisation dans laquelle vous avez mis à disposition le service {{site.data.keyword.monitoringshort}}.
    * **Espace** : Choisissez l'espace dans lequel vous avez mis à disposition le service {{site.data.keyword.monitoringshort}}.

3. Cliquez sur **Créer**.

Dès que l'application CF s'exécute, les métriques sont collectées et transmises au service {{site.data.keyword.monitoringshort}}.

## Etape 3 : Lancement de Grafana et définition du domaine des métriques
{: #cfapps_step3}

Lancez Grafana à partir d'un navigateur et définissez le domaine {{site.data.keyword.monitoringshort}} dans lequel vous pourrez visualiser les métriques d'application CF.

1. A partir d'un navigateur, démarrez Grafana. 

    Entrez l'adresse URL du service {{site.data.keyword.monitoringshort}} pour la région où ce dernier a été mis à disposition.
    
    Pour obtenir les adresses URL par région, voir [URL pour le service de surveillance](/docs/services/cloud-monitoring?topic=cloud-monitoring-monitoring_ov#region).

    Par exemple, pour la région Sud des Etats-Unis, démarrez : [https://metrics.ng.bluemix.net/](https://metrics.ng.bluemix.net/).

2. Définissez le domaine {{site.data.keyword.monitoringshort}} dans lequel vous pourrez visualiser les métriques de cluster.

    Dans Grafana, sélectionnez votre ID. Ensuite, assurez-vous que vous êtes connecté au compte approprié, puis choisissez `Domain = space`.

    Assurez-vous que le nom de l'organisation et le nom de l'espace correspondent à l'organisation et à l'espace où vous avez déployé l'application CF et mis à disposition le service {{site.data.keyword.monitoringshort}}.


## Etape 4 : Création d'un tableau de bord Grafana pour surveiller une métrique
{: #cfapps_step4}


Pour créer un nouveau tableau de bord dans Grafana, procédez comme suit :

1. Sélectionnez le bouton de basculement de la barre de menus latérale ![Barre de menus latérale de Grafana](images/grafana_settings.gif "Barre de menus latérale de Grafana").
2. Sélectionnez **Dashboards**.
3. Cliquez sur **New**.

Un tableau de bord s'ouvre. Il comporte une ligne vide prête pour la configuration.

![Tableau de bord Grafana](images/grafana4_f1.gif "Tableau de bord Grafana")

Dans Grafana, ajoutez des lignes pour diviser le tableau de bord en sections. Une ligne regroupe un ou plusieurs panneaux. Dans une ligne, un panneau constitue l'unité de visualisation la plus petite que vous pouvez configurer pour l'affichage des données d'une métrique. Par exemple, vous pouvez choisir un panneau de graphique ou un panneau de tableau. Vous pouvez faire glisser des panneaux et les déposer à l'emplacement de votre choix afin de les réorganiser dans un tableau de bord. Les données affichées dans un panneau sont configurées via des requêtes. Vous pouvez définir une ou plusieurs requêtes dans un panneau. Chaque requête représente un ensemble différent de données. Vous pouvez aussi définir l'intervalle pour un panneau. Normalement, il est défini par le sélecteur de temps du *tableau de bord*.

Définissez la requête qui filtre les données affichées dans le graphique. Cette requête surveille le pourcentage d'utilisation de l'unité centrale par rapport à la limite du conteneur.

Pour plus d'informations sur le format de la requête, voir [Format de requête Grafana pour les applications CF](/docs/services/cloud-monitoring/reference?topic=cloud-monitoring-cfapps_metrics_format#cfapps_metrics_format).
    
1. Ajoutez un panneau *Graph* afin de surveiller les nanosecondes de temps UC sur tous les coeurs d'un conteneur.
    
    1. Sélectionnez **Graph**.
    
    2. Cliquez sur le titre du graphique, puis sélectionnez **edit**.
    
        L'onglet *Metrics* s'ouvre. Il affiche la source de données par défaut.
    
        ![Panneau du graphique comportant des onglets de configuration](images/grafana4_f2.gif "Panneau du graphique comportant des onglets de configuration")
    
2. Définissez la requête qui filtre les données affichées dans le graphique. 
    
    Dans l'onglet *Metrics*, sélectionnez **Add query**. <br>Une entrée de requête est ajoutée. Chaque requête est associée à une lettre.
    
    ![Nouvelle entrée de requête](images/grafana4_query_f1.gif "Nouvelle entrée de requête")
        
    1. Cliquez sur **Select metric**, puis choisissez la source : `ibmcloud`.
    
    2. Cliquez sur **Select metric**, puis choisissez le type de cloud : `public`.
    
    3. Cliquez sur **Select metric**, puis choisissez `cloud-foundry`.
    
    4. Cliquez sur **Select metric**, puis choisissez la région à partir de laquelle vous travaillez, par exemple, `us-south`.
    
    5. Cliquez sur **Select metric**, puis choisissez le nom d'application CF, par exemple, `logtester`.
    
    6. Cliquez sur **Select metric**, puis choisissez l'index d'instance d'application CF, par exemple, `0`.

    7. Cliquez sur **Select metric**, puis choisissez `container`.
    
    9. Cliquez sur **Select metric**, puis choisissez une métrique. Pour surveiller le *pourcentage d'utilisation de l'unité centrale* d'un conteneur, choisissez `cpu-utilization`.

    10. Cliquez sur le signe plus ![Icône Ajouter](images/grafana_plus_image.gif "Signe Plus"), puis choisissez une fonction. Vous pouvez ajouter une fonction pour transformer et combiner des données disponibles pour une métrique, et effectuer des calculs sur ces données.
        
        Par exemple, vous pouvez ajouter la fonction **alias(newName)** afin d'ajouter un alias pour une métrique. Cet alias sera utilisé pour afficher une chaîne à la place du nom de la métrique dans la légende du graphique.
        
        Afin d'ajouter un alias pour votre métrique, procédez comme suit :
        
        1. Cliquez sur le signe plus.
        2. Sélectionnez **Special**. 
        3 Sélectionnez **alias**.
        4. Entrez une chaîne, par exemple `Mon exemple de métrique`.
        

## Etape 5 : Sauvegarde du tableau de bord
{: #cfapps_step5}

Sauvegardez le tableau de bord en vue de sa réutilisation ultérieure.

1. Cliquez sur l'icône de sauvegarde du tableau de bord ![Icône Sauvegarder le tableau de bord](images/grafana_save_image.gif "Icône Sauvegarder le tableau de bord").

    ![Sauvegarder le tableau de bord](images/grafana_save_dashboard.gif "Sauvegarder le tableau de bord")

2. Entrez le nom du tableau de bord.
3. Cliquez sur **Save**.


## Etapes suivantes
{: #cfapps_next_steps}

Définissez une alerte pour une métrique. Pour plus d'informations, voir [Configuration d'alertes](/docs/services/cloud-monitoring?topic=cloud-monitoring-config_alerts_ov#config_alerts_ov).
