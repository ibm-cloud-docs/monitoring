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


# Extraction de l'historique d'une alerte à l'aide de l'API Alerts
{: #retrieve_history}

Utilisez l'API Alerts pour extraire l'historique d'une alerte. 
{:shortdesc}


Pour extraire l'historique d'une alerte à l'aide de l'API Alerts, procédez comme suit :

1. Connectez-vous à une région, une organisation et un espace dans {{site.data.keyword.Bluemix_notm}}. 

    Pour plus d'informations, voir [Comment se connecter à {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login).

2. Obtenez le jeton de sécurité. Vous pouvez utiliser un jeton UAA, un jeton IAM ou une clé d'API. Choisissez l'une des méthodes suivantes pour obtenir le jeton de sécurité :
	
	* Pour obtenir un jeton, voir [Obtention du jeton UAA à l'aide de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_uaa#uaa_cli).
	
	* Pour obtenir un jeton IAM, voir [Obtention du jeton IAM à l'aide de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_iam#auth_iam).
	
	* Pour obtenir une clé d'API, voir [Obtention d'une clé d'API](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_api_key#auth_api_key).
	
	Sur le terminal à partir duquel vous vous êtes connecté à {{site.data.keyword.Bluemix_notm}}, définissez la variable Token pour le jeton.

    Par exemple, pour utiliser le jeton IAM, exécutez la commande suivante :

    ```
	ibmcloud iam oauth-tokens
	```
	{: codeblock}
	
	Le résultat de cette commande est le suivant :
	
	```
	IAM token:  Bearer djn.._l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	Exportez ensuite la variable *Token* :
	
	```
	export Token="djn.._l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ"
	```
	{: screen}
	
	**Remarque :** le jeton exclut *Bearer*.
	
3. Obtenez l'identificateur global unique de l'espace. L'identificateur global unique doit avoir le préfixe *s-* pour identifier un espace.

    Exécutez la commande suivante :
	
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
	
	Exportez ensuite la variable *Space*. **Remarque :** l'identificateur global unique doit avoir le préfixe *s-* pour identifier un espace.
	
	Par exemple :
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. Extrayez l'historique d'une règle

    * Pour extraire l'historique d'une règle d'après son nom, voir [Extraction de l'historique d'une règle en utilisant son nom](/docs/services/cloud-monitoring/alerts?topic=cloud-monitoring-retrieve_history#by_name).
	* Pour extraire l'historique d'une règle d'après une période, voir [Extraction de l'historique d'une règle pour les dernières 48 heures](/docs/services/cloud-monitoring/alerts?topic=cloud-monitoring-retrieve_history#by_time).
	* Pour extraire un nombre d'entrées à partir de l'historique d'une règle, voir [Extraction des 3 dernières entrées de l'historique d'une règle](/docs/services/cloud-monitoring/alerts?topic=cloud-monitoring-retrieve_history#number).
	
	
## Extraction de l'historique d'une règle d'après le nom de règle
{: #by_name}
	
Exécutez la commande cURL suivante pour obtenir l'historique d'une alerte :

```
curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/history?rule_name=RULE_NAME
```
{: codeblock}
	
où
	
* *X-Auth-User-Token* est un paramètre qui transmet le jeton UAA, le jeton IAM ou la clé d'API.
	
* *Auth_Type* est le préfixe qui définit le type de jeton ou de clé d'API. Les valeurs valides sont : *apikey*, *iam* ou *uaa*, où

    * *apikey* identifie le jeton comme étant une clé d'API.
	* *iam* identifie le jeton spécifié comme étant un jeton généré par IAM.
	* *uaa* identifie le jeton spécifié comme étant un jeton généré par UAA.
	
* *X-Auth-Scope-Id* est un paramètre qui transmet l'identificateur global unique de l'espace. L'identificateur global unique doit avoir le préfixe *s-* pour identifier un espace. Cet en-tête est requis si vous utilisez un jeton d'authentification UAA. Si vous utilisez un jeton d'authentification IAM, cet en-tête est facultatif et les informations de domaine qui sont associées au jeton sont utilisées.
	
* *Token* est le jeton d'identification UAA ou IAM ou la clé d'API.
	
* *Space* est l'identificateur global unique de l'espace. 
	
* *RULE_NAME* est le nom de la règle utilisée pour déclencher l'alerte. La valeur est celle spécifiée dans la zone *name*.
	
* *METRICS_ENDPOINT* représente le point d'entrée vers le service. Chaque région a une adresse URL différente. Pour la liste des noeuds finaux par région, voir [Noeuds finaux](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints).
	
    
Par exemple, l'historique de la règle `highNginxCPU` est le suivant :

```
curl -XGET --header "X-Auth-User-Token: iam ${Token}" --header "X-Auth-Scope-Id: ${Space}" https://metrics.ng.bluemix.net/v1/alert/history?rule_name=highNginxCPU
```
{: screen}

```
[
 {
 "rule": "highNginxCPU",
 "timestamp": "2017-04-17T22.23.21.000",
 "value": 99.5,
 "from_level": "OK",
 "to_level": "ERROR"
 },
 {
 "rule": "highNginxCPU",
 "timestamp": "2017-04-17T10.11.12.123",
 "value": 98.5,
 "from_level" : "OK",
 "to_level": "WARN"
 },
 {
 "rule": "highNginxCPU",
 "timestamp": "2017-04-17T10.12.14.000",
 "value": 97.0,
 "from_level" : "WARN",
 "to_level": "OK"
 }
]
```
{: screen}


## Extraction de l'historique d'une règle pour les dernières 48 heures
{: #by_time}

Exécutez la commande cURL suivante pour obtenir l'historique d'une alerte pour les dernières 48 heures :

```
curl -H "X-Auth-User-Token: iam $Token" -H "X-Auth-Scope-Id:$Space" METRICS_ENDPOINT/v1/alert/history?start=-48h
```
{: codeblock}

où
	
* *X-Auth-User-Token* est un paramètre qui transmet le jeton UAA, le jeton IAM ou la clé d'API.
	
* *Auth_Type* est le préfixe qui définit le type de jeton ou de clé d'API. Les valeurs valides sont : *apikey*, *iam* ou *uaa*, où

    * *apikey* identifie le jeton comme étant une clé d'API.
	* *iam* identifie le jeton spécifié comme étant un jeton généré par IAM.
	* *uaa* identifie le jeton spécifié comme étant un jeton généré par UAA.
	
* *X-Auth-Scope-Id* est un paramètre qui transmet l'identificateur global unique de l'espace. L'identificateur global unique doit avoir le préfixe *s-* pour identifier un espace. Cet en-tête est requis si vous utilisez un jeton d'authentification UAA. Si vous utilisez un jeton d'authentification IAM, cet en-tête est facultatif et les informations de domaine qui sont associées au jeton sont utilisées.
	
* *Token* est le jeton d'identification UAA ou IAM ou la clé d'API.
	
* *Space* est l'identificateur global unique de l'espace. 
	
* *RULE_NAME* est le nom de la règle utilisée pour déclencher l'alerte. La valeur est celle spécifiée dans la zone *name*.
	
* *METRICS_ENDPOINT* représente le point d'entrée vers le service. Chaque région a une adresse URL différente. Pour la liste des noeuds finaux par région, voir [Noeuds finaux](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints).
	

## Extraction des 3 dernières entrées de l'historique d'une règle
{: #number}

Exécutez la commande cURL suivante pour obtenir les 3 dernières entrées de l'historique d'une alerte :

```
curl -H "X-Auth-User-Token: iam $Token" -H "X-Auth-Scope-Id:$Space" METRICS_ENDPOINT/v1/alert/history?max_results=3
```
{: codeblock}

où
	
* *X-Auth-User-Token* est un paramètre qui transmet le jeton UAA, le jeton IAM ou la clé d'API.
	
* *Auth_Type* est le préfixe qui définit le type de jeton ou de clé d'API. Les valeurs valides sont : *apikey*, *iam* ou *uaa*, où

    * *apikey* identifie le jeton comme étant une clé d'API.
	* *iam* identifie le jeton spécifié comme étant un jeton généré par IAM.
	* *uaa* identifie le jeton spécifié comme étant un jeton généré par UAA.
	
* *X-Auth-Scope-Id* est un paramètre qui transmet l'identificateur global unique de l'espace. L'identificateur global unique doit avoir le préfixe *s-* pour identifier un espace. Cet en-tête est requis si vous utilisez un jeton d'authentification UAA. Si vous utilisez un jeton d'authentification IAM, cet en-tête est facultatif et les informations de domaine qui sont associées au jeton sont utilisées.
	
* *Token* est le jeton d'identification UAA ou IAM ou la clé d'API.
	
* *Space* est l'identificateur global unique de l'espace. 
	
* *RULE_NAME* est le nom de la règle utilisée pour déclencher l'alerte. La valeur est celle spécifiée dans la zone *name*.
	
* *METRICS_ENDPOINT* représente le point d'entrée vers le service. Chaque région a une adresse URL différente. Pour la liste des noeuds finaux par région, voir [Noeuds finaux](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints).
	
