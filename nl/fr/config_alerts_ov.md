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



# Configuration d'alertes
{: #config_alerts_ov}

Le service {{site.data.keyword.monitoringshort}} fournit un système d'alerte reposant sur des requêtes. Vous pouvez configurer des alertes à l'aide de l'API {{site.data.keyword.monitoringshort}} ou via Grafana. Pour configurer une alerte, vous devez définir des règles et des méthodes de notification pour chaque requête de métrique que vous souhaitez surveiller. Vous pouvez envoyer une notification par courrier électronique, en déclenchant un webhook ou en envoyant une alerte à PagerDuty.
{:shortdesc}

Vous pouvez définir une alerte dans le but de déclencher une notification pour une métrique. Une alerte est définie par une règle qui décrit la requête de métrique à surveiller, la valeur de seuil, l'action à effectuer en cas de dépassement du seuil, ainsi qu'une ou plusieurs méthodes de notification.  

Le tableau suivant répertorie les différentes méthodes, ainsi que les différentes actions prises en charge, que vous pouvez utiliser pour gérer les alertes :

<table>
  <caption>Méthodes de gestion des alertes</caption>
	<tr>
    <th>Méthode</th>
		<th>Définir une alerte</th>
		<th>Mettre à jour une alerte</th>
		<th>Supprimer une alerte</th>
	</tr>
	<tr>
    <td>API Alerts</td>
		<td>Oui</td>
		<td>Oui</td>
		<td>Oui</td>
	</tr>
	<tr>
    <td>Grafana</td>
		<td>Oui</td>
		<td>Oui</td>
		<td>Oui</td>
	</tr>
</table>

**Remarque :** les alertes que vous définissez à l'aide de l'API Alerts n'apparaissent pas dans le tableau de bord Grafana.


L'illustration suivante montre les différents types de notification que vous pouvez configurer dans le service {{site.data.keyword.monitoringshort}} pour vous alerter :

![Présentation générale des types de notification disponibles dans le service {{site.data.keyword.monitoringlong}} ](images/alerts_ov_f1.gif)

Vous pouvez définir des alertes pour une ou plusieurs instance(s). Lorsqu'une requête que vous surveillez via une règle d'alerte inclut un caractère générique, celui-ci identifie plusieurs cibles, c'est-à-dire, plusieurs instances de service ou instances d'application. Toutes les 5 minutes, le service {{site.data.keyword.monitoringshort}} exécute la requête qui est configurée dans une règle d'alerte, et vérifie les derniers points de données qui sont renvoyés pour chaque instance ou pour plusieurs instances. Le service {{site.data.keyword.monitoringshort}} effectue le suivi du dernier état pour chaque instance et génère une nouvelle alerte si l'état de l'alerte change. 



## Gestion des alertes à l'aide de l'API Alerts
{: #api}

Vous pouvez définir, mettre à jour ou supprimer des alertes en utilisant l'API Alerts.

Pour définir une alerte sur une requête de métrique à l'aide de l'API Alerts, vous devez :

1. Définir une ou plusieurs requêtes de métrique sur un tableau de bord Grafana. 

    **Remarque :** vous ne pouvez pas définir d'alertes sur des tableaux de bord Grafana qui utilisent des variables de modèle.

2. Configurer une alerte sur une requête de métrique qui est définie sur le tableau de bord Grafana.

    * [Configuration d'une alerte qu envoie un courrier électronique](/docs/services/cloud-monitoring/alerts/configure_email_alert.html#configure_email_alert).
    * [Configuration d'une alerte qui envoie une notification PagerDuty](/docs/services/cloud-monitoring/alerts/configure_pagerduty_alert.html#configure_pagerduty_alert)
    * [Configuration d'une alerte qui envoie une notification webhook](/docs/services/cloud-monitoring/alerts/configure_webhook_alert.html#configure_webhook_alert)

    **Remarque :** vous ne pouvez définir des notifications par courrier électronique que pour les requêtes de métrique définies dans le domaine de métrique de compte.



## Gestion des alertes à l'aide de Grafana
{: #grafana}

Vous pouvez définir et supprimer des alertes directement sur un tableau de bord Grafana. Vous pouvez également mettre à jour des définitions de règle. Toutefois, toutes les modifications de canal de notification doivent être réalisées à l'aide de l'API Alerts.

Tenez compte des informations suivantes lorsque vous gérez des alertes dans Grafana :

* Pour modifier les canaux de notification affectés à une règle, vous devez utiliser l'API Alerts.
* Lorsque vous supprimez un canal de notification dans un domaine d'espace, les règles pour lesquelles ce canal est configuré ne sont pas mises à jour. Vous devez utiliser l'API Alerts pour modifier la règle et retirer ce canal de notification de cette règle. 

Pour définir une alerte sur une requête de métrique directement sur un tableau de bord Grafana, vous devez :

1. Définir une ou plusieurs requêtes de métrique sur un tableau de bord Grafana. 

    **Remarque :** vous ne pouvez pas définir d'alertes sur des tableaux de bord Grafana qui utilisent des variables de modèle.

2. Configurer une alerte sur une requête de métrique qui est définie sur le tableau de bord Grafana.

    Pour plus d'informations, voir [Configuration d'alertes dans Grafana](/docs/services/cloud-monitoring/alerts/config_alerts_grafana.html#config_alerts_grafana).


## Etats des alertes
{: #status}

Une alerte peut être associée à l'un des états suivants lorsque la règle est activée :

* *OK* : l'état d'une règle a pour valeur *OK* dans les cas suivants :
    
	* Des données sont disponibles dans le service {{site.data.keyword.monitoringshort}} pour la requête de métrique qui est associée à cette règle. Vous avez défini un seuil d'avertissement et un seuil d'erreur. La valeur des données ne dépasse pas la valeur de seuil.
	 
	* Aucune donnée n'est disponible dans le service {{site.data.keyword.monitoringshort}} pour la requête de métrique qui est associée à cette règle et vous configurez la propriété de règle `allow_no_data` avec la valeur *true*.           
	 
* *WARNING* : l'état de la règle a pour valeur *WARNING* lorsque des données sont disponibles dans le service {{site.data.keyword.monitoringshort}} pour la requête de métrique associée à cette règle. Vous avez défini un seuil d'avertissement et un seuil d'erreur. La valeur des données est comprise entre la valeur de seuil d'avertissement et la valeur de seuil d'erreur.
	
* *ERROR* : l'état de la règle a pour valeur *ERROR* lorsque des données sont disponibles dans le service {{site.data.keyword.monitoringshort}} pour la requête de métrique associée à cette règle. Vous avez défini un seuil d'avertissement et un seuil d'erreur. La valeur de seuil d'erreur est atteinte.  

* *UNKNOWN* : l'état de la règle a pour valeur *UNKNOWN* lorsqu'aucune donnée n'est disponible dans le service {{site.data.keyword.monitoringshort}} pour la requête de métrique associée à cette règle. Vous pouvez indiquer si vous souhaitez recevoir ou non une notification basée sur la propriété `allow_no_data` que vous configurez pour la règle. Si vous affectez la valeur `false` à cette propriété, vous êtes averti qu'aucune donnée n'a été trouvée pour la règle.



	
## Historique de l'alerte
{: #history}

A chaque fois que l'état d'une alerte change, l'enregistrement d'historique de l'alerte est mis à jour. Vous pouvez utiliser l'API Alerts (*/v1/alert/history*) pour extraire des informations sur l'historique d'une métrique.

L'état d'une alerte est utilisé pour définir le statut dans les scénarios suivants :

* Statut de la requête avant que la règle ne déclenche une notification.
* Statut de la requête après le déclenchement de la règle. 

Par exemple, si un seuil d'avertissement est dépassé, un enregistrement d'historique qui enregistre la transition de *OK* à *WARNING* est généré. De même, lorsque la valeur repasse sous le seuil, un enregistrement d'historique qui enregistre la transition de *WARNING* à *OK* est généré.

Pour plus d'informations, voir [Extraction de l'historique d'une règle](/docs/services/cloud-monitoring/alerts/retrieve_history.html#retrieve_history).


## Règles
{: #rules1}

Une règle décrit la requête de métrique à surveiller, la valeur de seuil et l'action à effectuer en cas de dépassement du seuil. 

* Vous pouvez créer, supprimer et mettre à jour une règle, afficher les détails d'une règle, et répertorier toutes les règles à l'aide de l'API Alerts. Pour plus d'informations, voir [Utilisation de règles](/docs/services/cloud-monitoring/alerts/rules.html#rules).

    * Pour créer une règle, voir [Création d'une règle](/docs/services/cloud-monitoring/alerts/rules.html#create).
	* Pour supprimer une règle, voir [Suppression d'une règle](/docs/services/cloud-monitoring/alerts/rules.html#delete).
	* Pour mettre à jour une règle, voir [Mise à jour d'une règle](/docs/services/cloud-monitoring/alerts/rules.html#update).
	* Pour établir la liste de toutes les règles, voir [Liste de toutes les rèles](/docs/services/cloud-monitoring/alerts/rules.html#list).
	* Pour afficher les informations concernant une règle, voir [Affichage des détails d'une règle](/docs/services/cloud-monitoring/alerts/rules.html#showing-the-details-of-a-rule).

* Le système d'alerte vérifie toutes les 5 minutes les règles qui sont activées dans l'espace.

* Par défaut, une règle est activée lorsque vous la créez. Toutefois, vous pouvez définir la règle, et la désactiver, en affectant la valeur `false` à la zone *enable*.

* Lorsque le paramètre de règle *comparison* a pour valeur below, la valeur error_level doit être inférieure à la valeur du niveau d'avertissement. Lorsque le paramètre de règle *comparison* a pour valeur above, la valeur error_level doit être supérieure à la valeur du niveau d'avertissement.

* Par défaut, une règle est créée avec la valeur `true` affectée à la zone *allow_no_data*. Lorsqu'aucun point de données n'est disponible, aucune notification n'est envoyée sauf si la condition de règle est déclenchée. Si vous souhaitez recevoir une notification vous informant qu'aucune donnée n'a été trouvée pour la règle X, vous devez affecter la valeur `false` à la zone *allow_no_data*. 

**Astuce :** vérifiez la requête que vous surveillez au moyen d'une règle d'alerte dans Grafana. Assurez-vous qu'aucun dépassement de délai d'attente ne se produit. Par exemple, un dépassement de délai d'attente peut se produire pour une requête en raison de la configuration d'une période prolongée ou suite à la définition d'une requête qui inclut un caractère générique. Notez que lorsque la requête subit un dépassement de délai d'attente dans Grafana, une alerte configurée pour cette requête n'est pas déclenchée.

Les zones suivantes sont requises pour définir une règle :

<table>
  <caption>Tableau 1. Liste des zones utilisées pour définir une règle</caption>
  <tr>
    <th>Nom de zone</th>
	<th>Description</th>
  </tr>
  <tr>
    <td>name</td>
	<td>Nom de la règle. Il doit être unique.</td>
  </tr>
  <tr>
    <td>description</td>
	<td>Récapitulatif de la règle.</td>
  </tr>
  <tr>
    <td>expression</td>
	<td>Requête de métrique à surveiller et pour laquelle envoyer une alerte si un seuil est dépassé. <br>Les expressions valides sont les suivantes : un nom de métrique unique, plusieurs métriques identifiées par des caractères génériques ou des fonctions ajoutées à des données d'agrégation. <br>**Astuce :** vous pouvez copier une requête vérifiée depuis Grafana.</td>
  </tr>
  <tr>
    <td>enabled</td>
	<td>Décrit le statut de la règle : <br>Définissez `true` pour activer la règle. <br>Définissez `false` pour désactiver la règle. <br>Par défaut, cette zone a pour valeur `true`.</td>
  </tr>
  <tr>
    <td>from</td>
	<td>Point de départ pour l'analyse des données en fonction des valeurs de seuil que vous avez définies pour la requête dans la zone expression. Exemple : `"from": "-5min"`</td>
  </tr>
  <tr>
    <td>until</td>
	<td>Point de fin pour l'analyse des données en fonction des valeurs de seuil que vous avez définies pour la requête dans la zone expression. Exemple : `"until": "now"`</td>
  </tr>
  <tr>
    <td>comparison</td>
	<td>Opération de comparaison utilisée pour identifier le type de vérification à effectuer. Les valeurs valides sont *below* et *above*. </td>
  </tr>
  <tr>
    <td>comparison_scope</td>
	<td>Définit la portée des données qui sont analysées. <br>Définissez *last* pour examiner la dernière valeur dans la série (les données qui sont disponibles pour votre requête).</td>
  </tr>
  <tr>
    <td>error_level</td>
	<td>Définit le seuil que vous avez configuré pour le déclenchement d'une alerte d'erreur. <br>Définissez la valeur qui, si elle est atteinte, entraîne la génération d'une alerte d'erreur. Exemple : `"error_level" : 27.94`</td>
  </tr>
  <tr>
    <td>warning_level</td>
	<td>Définit le seuil que vous avez configuré pour le déclenchement d'une alerte d'avertissement. <br>Définissez la valeur qui, si elle est atteinte, entraîne la génération d'une alerte d'avertissement. Exemple : `"warning_level" : 24`</td>
  </tr>
  <tr>
    <td>frequency</td>
	<td>Définit la fréquence à laquelle la vérification est effectuée. <br>Elle est mesurée en minutes, heures ou jours, par exemple, 5min, 1h, 7d. <br>Par exemple, pour effectuer une vérification toutes les minutes, vous pouvez affecter la valeur `"frequency": "1min"`. <br>**Note :** actuellement, la fréquence est de 5 minutes.</td>
  </tr>
  <tr>
    <td>dashboard_url</td>
	<td>Définit l'adresse URL d'un tableau de bord Grafana dans lequel la requête qui est surveillée est définie.</td>
  </tr>
    <tr>
    <td>allow_no_data</td>
	<td>Définit la condition à laquelle une notification n'est envoyée lorsqu'aucun point de données n'est disponible. <br>Par défaut, cette zone a pour valeur `true`. <br>Si vous souhaitez recevoir une notification vous informant qu'aucune donnée n'a été trouvée pour la règle X, affectez la valeur `false` à cette zone.</td>
  </tr>
  <tr>
    <td>notifications</td>
	<td>Nom d'une notification qui définit l'action à déclencher pour la règle. <br>**Note :** vous pouvez définir 1 ou plusieurs notifications par règle en répertoriant des noms de notification séparés par une virgule.</td>
  </tr>
</table>

Exemple de règle :

```
{
  "name": "checkbytesin1",
  "description": "MH check Bytes In per second",
  "expression": "movingAverage(messagehub.65ad9211-1234-5678-a751-c82123411eee.1.kafka-java-console-sa
mple-topic.BytesInPerSec.15MinuteRate,\"5min\")",
  "enabled": true,
  "from": "-5min",
  "until": "now",
  "comparison": "below",
  "comparison_scope": "last",
   "error_level" : 22.94,
   "warning_level" : 25,
  "frequency": "1min",
  "dashboard_url": "https://metrics.ng.bluemix.net",
  "notifications": [
    "emailXXX"
  ]
}
```
{: screen}



## Notifications
{: #alert_notifications}

Une notification décrit la méthode et les détails qui sont utilisés pour envoyer une notification lorsqu'une alerte est déclenchée. Par exemple, afin d'obtenir une notification d'avertissement et une notification d'erreur pour une métrique, définissez une règle qui surveille le seuil d'avertissement et une règle qui surveille le seuil d'erreur. 

* Une notification est envoyée uniquement lorsque l'état de l'alerte change, par exemple, lorsque l'état d'une alerte définie pour une métrique passe de "OK" à "ERROR" ou de "ERROR" à "WARNING". 

    **Remarque :** si l'état (*OK*, *WARNING*, *ERROR* ou *UNKNOWN*) d'une règle d'alerte ne change pas, celle-ci n'est pas redéclenchée à l'itération suivante.

* Les notifications sont considérées comme des événements de 24 heures. Vous ne pouvez pas spécifier d'intervalle de temps lorsqu'une notification peut être déclenchée.

* Vous pouvez configurer 1 ou plusieurs méthodes de notification par règle en répertoriant des noms de notification séparés par une virgule. 

* Vous pouvez utiliser l'[API REST Alerts](https://console.bluemix.net/apidocs/940-ibm-cloud-monitoring-alerts-api?&language=node#introduction){: new_window} pour créer, supprimer et mettre à jour une notification, pour afficher les détails d'une notification, et pour répertorier les notifications qui sont définies dans un espace.

    * Pour créer une notification, voir [Création d'une notification](/docs/services/cloud-monitoring/alerts/notifications.html#notifications_create).
	* Pour supprimer une notification, voir [Suppression d'une notification](/docs/services/cloud-monitoring/alerts/notifications.html#notifications_delete).
	* Pour mettre à jour une notification, voir [Mise à jour d'une  notification](/docs/services/cloud-monitoring/alerts/notifications.html#notifications_update).
	* Pour établir la liste de toutes les notifications, voir [Liste de toutes les notifications](/docs/services/cloud-monitoring/alerts/notifications.html#notifications_list).
	* Pour afficher les informations concernant une notification, voir [Affichage des détails d'une notification](/docs/services/cloud-monitoring/alerts/notifications.html#show).

* Vous pouvez configurer une notification par courrier électronique, une notification PagerDuty et une notification webhook. 

**Remarque :** vous définissez les notifications d'alerte indépendamment des règles afin de pouvoir réutiliser les notifications avec plusieurs règles.

	
## Notification - Modèles JSON
{: #notification_template}
	
Une notification est un fichier JSON. 

Le tableau suivant inclut un modèle de notification pour chaque type de méthode de notification :

<table>
  <caption>Tableau 3. Modèles de notification</caption>
  <tr>
    <th>Type</th>
	<th>Modèle</th>
	<th>Exemple</th>
  </tr>
  <tr>
    <td>Email</td>
	<td>
	```
	{
	"name": "Template_Name",
	"type": "Email",
	"description" : "Description",
	"detail": "EmailAddress"
	}
	```
	{: screen}
	</td>
	<td>
	```
	{
	"name": "my-email",
	"type": "Email",
	"description" : "Send email notification when there is an infrastructure problem.",
	"detail": "xxx@yyy.com"}
	```
	{: screen}
	</td>
  </tr>
  <tr>
    <td>Webhook</td>
	<td>
	```
	{
	"name": "Template_Name",
	"type": "Webhook",
	"description" : "Description",
	"detail": "Endpoint"
	}
	```
	{: codeblock}
	</td>
	<td>
	```
	{
	"name": "my-webhook",
	"type": "Webhook",
	"description" : "Fire a webhook when there is an infrastructure problem..",
	"detail": "https://myendpoint.bluemix.net?key=abcd1234"
	}
	```
	{: screen}
	</td>
  </tr>
  <tr>
    <td>Pagerduty</td>
	<td>
	```
	"name": "Template_Name",
	"type": "PagerDuty",
	"description" : "Description",
	"detail": "Pagerduty_APIkey"
	}
	```
	{: codeblock}
	</td>
	<td>
	```
	{
	"name": "my-pagerduty",
	"type": "PagerDuty",
	"description" : "Fire a PagerDuty alert when there is an infrastructure problem..",
	"detail": "abcd1234"
	}
	```
	{: screen}
	</td>
  </tr>
</table>

Où

* *Template_Name* correspond au nom du modèle de notification.
* *Description* indique à quel moment ce type de notification est utilisé.
* *EmailAddress* définit l'adresse électronique du destinataire de la notification.
* *Endpoint* définit l'adresse URL à laquelle la demande POST doit être émise. 
* *Pagerduty_APIkey* définit une clé d'API unique. Celle-ci est générée par un administrateur ou un propriétaire de compte PagerDuty.



## Règles - Modèle JSON
{: #rules_template}

Une règle est décrite à l'aide d'un fichier JSON. 

Le code suivant est un modèle de règle :

```
{
"name": "Enter rule name",
"description": "Desccribe rule",
"expression": "Add metric query",
"enabled": true,
"from": "-5min",
"until": "now",
"comparison": "below",
"comparison_scope": "last",
"error_level" : xxxx,
"warning_level" : xxxx,
"frequency": "1min",
"dashboard_url": "https://metrics.ng.bluemix.net",
"notifications": [
 "List of Notifications by name. Include all the motification methods for this rule separated by commas."
 ]
}
```
{: screen}



