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

# Configuration d'alertes dans Grafana
{: #config_alerts_grafana}

Le service {{site.data.keyword.monitoringshort}} fournit un système d'alerte reposant sur des requêtes. Vous pouvez configurer des alertes dans Grafana sur des tableaux de bord qui ne comportent pas de variables de modèle. 
{:shortdesc}

Pour configurer une alerte sur une requête de métrique via l'interface utilisateur Grafana, procédez comme suit :

1. Démarrez Grafana.
2. Définissez un ou plusieurs canaux de notification.
3. Créez un tableau de bord Grafana qui inclut un graphique et au moins une métrique de requête. 
4. Configurez l'alerte via l'onglet **Alerts** sur un graphique Grafana.

## Etape 1 : Lancement de Grafana
{: #step1_cag}

Démarrez Grafana depuis un navigateur. Par exemple, entrez l'URL suivante pour ouvrir Grafana dans la région Sud des Etats-Unis : [https://metrics.ng.bluemix.net/](https://metrics.ng.bluemix.net/).

Pour obtenir la liste des adresses URL Grafana par région, voir [URL pour le service {{site.data.keyword.monitoringshort}}](/docs/services/cloud-monitoring?topic=cloud-monitoring-monitoring_ov#region).

## Etape 2 : Définition d'un ou de plusieurs canaux de notification
{: #step2_cag}

Procédez comme suit :

1. Dans Grafana, sélectionnez votre barre de menus latérale.

2. Sélectionnez **Alerting > Notification channels > New channel**.

3. Entrez les données relatives au nouveau canal. Ajoutez un canal de notification par courrier électronique, par exemple :

<table>
  <caption>Méthode de notification par courrier électronique et données que vous devez entrer pour créer un nouveau canal</caption>
  <tr>
     <th>Zone</th>
     <th>Description</th>
  </tr>
  <tr>
    <td>Name</td>
    <td>Nom du canal de notification. Cette valeur doit être unique.</td>
  </tr>
  <tr>
    <td>Description</td>
    <td>Informations supplémentaires que vous souhaiterez peut-être inclure à des fins de documentation.</td>
  </tr>
  <tr>
    <td>Type</td>
    <td>Sélectionnez **Email**</td>
  </tr>
  <tr>
    <td>Email ID</td>
    <td>Entrez l'adresse de courrier électronique du destinataire. </br>Vous pouvez entrer plusieurs adresses électroniques
en les séparant par des virgules.</td>
  </tr>
</table>

<table>
  <caption>Méthode de notification par webhook et données que vous devez entrer pour créer un nouveau canal</caption>
  <tr>
     <th>Zone</th>
     <th>Description</th>
  </tr>
  <tr>
    <td>Name</td>
    <td>Nom du canal de notification. Cette valeur doit être unique.</td>
  </tr>
  <tr>
    <td>Description</td>
    <td>Informations supplémentaires que vous souhaiterez peut-être inclure à des fins de documentation.</td>
  </tr>
  <tr>
    <td>Type</td>
    <td>Sélectionnez **Webhook**</td>
  </tr>
  <tr>
    <td>Webhook POST URL</td>
    <td>Entrez l'adresse URL à laquelle la demande POST doit être émise.</td>
  </tr>
  <tr>
    <td>Webhook headers</td>
    <td>Entrez des en-têtes.</td>
  </tr>
  <tr>
    <td>Webhook query parameters</td>
    <td>Entrez des paramètres de requête.</td>
  </tr>
</table>

<table>
  <caption>Méthode de notification par PagerDuty et données que vous devez entrer pour créer un nouveau canal</caption>
  <tr>
     <th>Zone</th>
     <th>Description</th>
  </tr>
  <tr>
    <td>Name</td>
    <td>Nom du canal de notification. Cette valeur doit être unique.</td>
  </tr>
  <tr>
    <td>Description</td>
    <td>Informations supplémentaires que vous souhaiterez peut-être inclure à des fins de documentation.</td>
  </tr>
  <tr>
    <td>Type</td>
    <td>Sélectionnez **PagerDuty**</td>
  </tr>
  <tr>
    <td>PagerDuty API key</td>
    <td>Entrez la clé PagerDuty.</td>
  </tr>
</table>

## Etape 3 : Définition d'une métrique
{: #step3_cag}

Pour créer un nouveau tableau de bord, procédez comme suit :

1. Sélectionnez le bouton de basculement de la barre de menus latérale ![Barre de menus latérale de Grafana](images/grafana_settings.gif "Barre de menus latérale de Grafana").
2. Sélectionnez **Dashboards**.
3. Cliquez sur **New**.

Un tableau de bord s'ouvre. Il comporte une ligne vide prête pour la configuration. 

Ajoutez une métrique :

1. Ajoutez un panneau *Graph*.
2. Sélectionnez **Graph**.
3. Cliquez sur le titre du graphique, puis sélectionnez **edit**.
    
    L'onglet *Metrics* s'ouvre. Il affiche la source de données par défaut.
    
4. Définissez la requête de métrique qui filtre les données affichées dans le graphique. 


## Etape 4 : Définition d'une alerte
{: #step4_cag}

Pour définir une alerte dans l'interface utilisateur Grafana, procédez comme suit :

1. Sélectionnez l'onglet **Alert**.
2. Dans la section **Alert Config**, définissez la règle qui conditionne la génération d'une notification d'alerte.

    Configurez la zone **Evaluate every** et la section **Conditions**.

3. Dans la section **Notifications**, sélectionnez un ou plusieurs canaux de notification.

**Remarque :** 

* Lorsqu'une condition est définie, une ligne rouge définissant le seuil défini apparaît sur le graphique. Vous pouvez la faire glisser sur le graphique pour la modifier.
* Une fois l'alerte créée, si vous souhaitez la modifier, vous devez utiliser l'API Alerts pour le faire.
* Si vous sélectionnez **Delete**, l'alerte est supprimée.

## Etape suivante : Vérification de la génération d'une alerte
{: #next_cag}

Par exemple, si vous avez créé un canal de notification par courrier électronique, vérifiez vos courriers électroniques.

Recherchez les courriers électroniques ayant **IBM Cloud Monitoring** pour expéditeur.

Un courrier électronique comprend des informations sur l'alerte déclenchée, ainsi qu'un lien vers le tableau de bord Grafana dans lequel vous pouvez visualiser la situation.

Par exemple :

```
Rule : grafana4_alerting-dashboard_1
Description : Alert created via Grafana 4 dashboard: alerting-dashboard on expression: ibmcloud.public.containers-kubernetes.eu-de.MyDemoCluster.worker.*.load.avg-15
Expression : ibmcloud.public.containers-kubernetes.eu-de.MyDemoCluster.worker.*.load.avg-15
Error Level : 0.8
Warn Level : 
Notification : email-channel
Dashboard URL : https://urldefense.proofpoint.com/v2/url?u=https-3A__metrics.eu-2Dde.bluemix.n......&s=Csta29jgJ8BsUZuJOeyX9G_6NoEnGi2RBbtIDFhjtfw&e=

Alerts:
Target: ibmcloud.public.containers-kubernetes.eu-de.MyDemoCluster.worker.kube-fra02-cr39f48d743e90451fa5a57d636796a489-w2.load.avg-15    From: WARN    To: OK    CurrentValue: 0.66    Comparison: above    Timestamp: 2018-02-06T17:34:14Z
```
{: screen}


