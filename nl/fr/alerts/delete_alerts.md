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



# Suppression des alertes
{: #delete_alerts}

Vous pouvez supprimer des alertes du service {{site.data.keyword.monitoringshort}} à l'aide de l'[API Alerts](https://console.bluemix.net/apidocs/940-ibm-cloud-monitoring-alerts-api?&language=node#introduction){: new_window}.
{:shortdesc}


Après vous être [connecté à une région dans {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login), suivez les instructions fournies ci-dessous pour supprimer une notification :


## Etape 1 : Obtention du jeton de sécurité
{: #step1_delete_alerts}

Vous pouvez utiliser un jeton UAA, un jeton IAM ou une clé d'API. 

Choisissez l'une des méthodes suivantes pour obtenir le jeton de sécurité :
	
* Pour obtenir un jeton, voir [Obtention du jeton UAA à l'aide de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_uaa#uaa_cli).
* Pour obtenir un jeton IAM, voir [Obtention du jeton IAM à l'aide de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_iam#auth_iam).
* Pour obtenir une clé d'API, voir [Obtention d'une clé d'API](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_api_key#auth_api_key).
	
Par exemple, pour utiliser le jeton IAM, exécutez la commande suivante :

```
ibmcloud iam oauth-tokens
```
{: codeblock}
	
Le résultat de cette commande est le suivant :
	
```
IAM token:  Bearer djn.._l_HWtlNTibmcloudsl0qjBI9GqCnuQ
UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
```
{: screen}
	
Exportez ensuite la variable *Token* :
	
```
export Token="djn.._l_HWtlNTibmcloudslibmclouds0qjBI9GqCnuQ"
```
{: screen}
	
**Remarque :** le jeton exclut *Bearer*.
	

## Etape 2 : Obtention d'un ID d'espace 
{: #step2_delete_alerts}

Cette étape est uniquement applicable si vous souhaitez supprimer des alertes qui sont disponibles dans un domaine d'espace.

Pour obtenir l'identificateur global unique de l'espace, exécutez la commande suivante :
	
```
ibmcloud iam space SpaceName --guid
```
{: codeblock}
	
Où *SpaceName* est le nom de l'espace dans lequel vous allez définir une notification. 
	
Par exemple, pour obtenir l'identificateur global unique d'un espace dont le nom est *dev*, exécutez la commande suivante :
	
```
ibmcloud iam space dev --guid
```
{: screen}
	
Le résultat de cette commande est le suivant :
	
```
667fadfc-jhtg-1234-9f0e-cf4123451095
```
{: screen}
	
Exportez ensuite la variable *Space*. L'identificateur global unique doit avoir le préfixe *s-* pour identifier un espace.
	
```
export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
```
{: screen}

	

## Etape 3 : Etablissement d'une liste des règles
{: #step3_delete_alerts}


Exécutez la commande cURL suivante pour répertorier les règles qui sont définies dans un domaine d'espace :

```
curl -H "X-Auth-Scope-Id: ${Space}" -H “X-Auth-User-Token: Auth_Type ${TOKEN}" -XGET METRICS_ENDPOINT/v1/alert/rules

```
{: screen}

Exécutez la commande cURL suivante pour afficher une liste des notifications dans le domaine de compte :

```
curl -H "X-Auth-User-Token: apikey ${TOKEN}" -XGET METRICS_ENDPOINT/v1/alert/rules
```
{: screen}

où
	
* *X-Auth-User-Token* est un paramètre qui transmet le jeton UAA, le jeton IAM ou la clé d'API {{site.data.keyword.Bluemix_notm}}.
	
* *Auth_Type* est le préfixe qui définit le type de jeton ou de clé d'API. Les valeurs valides sont : *apikey*, *iam* ou *uaa*, où

    * *apikey* identifie le jeton comme étant une clé d'API.
	* *iam* identifie le jeton spécifié comme étant un jeton généré par IAM.
	* *uaa* identifie le jeton spécifié comme étant un jeton généré par UAA.
	
* *X-Auth-Scope-Id* est un paramètre qui transmet l'identificateur global unique de l'espace. L'identificateur global unique doit avoir le préfixe *s-* pour identifier un espace. 
	
* TOKEN est le jeton d'identification UAA ou IAM ou la clé d'API.
	
* SPACE est l'identificateur global unique de l'espace. 
	
* METRICS_ENDPOINT représente le point d'entrée vers le service. Chaque région a une adresse URL différente. Pour la liste des noeuds finaux par région, voir [Noeuds finaux](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints).


## Etape 4 : Suppression d'une règle d'alerte
{: #step4_delete_alerts}
  

Exécutez la commande cURL suivante pour supprimer une règle dans un domaine d'espace :

```
curl -H "X-Auth-Scope-Id: ${Space}" -H “X-Auth-User-Token: Auth_Type ${TOKEN}" -XDELETE METRICS_ENDPOINT/v1/alert/rule/{name} 
```
{: screen}

Exécutez la commande cURL suivante pour supprimer une règle du domaine de compte :

```
curl -H "X-Auth-User-Token: apikey ${TOKEN}" -XDELETE METRICS_ENDPOINT/v1/alert/rule/{name} 
```
{: screen}

	
où
	
* *X-Auth-User-Token* est un paramètre qui transmet le jeton UAA, le jeton IAM ou la clé d'API {{site.data.keyword.Bluemix_notm}}.
	
* *Auth_Type* est le préfixe qui définit le type de jeton ou de clé d'API. Les valeurs valides sont : *apikey*, *iam* ou *uaa*, où

    * *apikey* identifie le jeton comme étant une clé d'API.
	* *iam* identifie le jeton spécifié comme étant un jeton généré par IAM.
	* *uaa* identifie le jeton spécifié comme étant un jeton généré par UAA.
	
* *X-Auth-Scope-Id* est un paramètre qui transmet l'identificateur global unique de l'espace. L'identificateur global unique doit avoir le préfixe *s-* pour identifier un espace. 
	
* TOKEN est le jeton d'identification UAA ou IAM ou la clé d'API.
	
* SPACE est l'identificateur global unique de l'espace. 
	
* METRICS_ENDPOINT représente le point d'entrée vers le service. Chaque région a une adresse URL différente. Pour la liste des noeuds finaux par région, voir [Noeuds finaux](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints).

* *name* est le nom de la règle que vous souhaitez supprimer.
	
