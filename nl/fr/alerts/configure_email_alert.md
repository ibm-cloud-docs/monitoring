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

# Configuration d'une alerte e-mail à l'aide de l'API {{site.data.keyword.monitoringshort}}
{: #configure_email_alert}

Pour configurer une alerte e-mail sur une métrique, définissez une règle et une notification par courrier électronique. Ensuite, enregistrez la règle et la méthode de notification dans le service {{site.data.keyword.monitoringshort}}.
{:shortdesc}

Procédez comme suit :

## Etape 1 : Création d'une règle
{: #step11}

Créez une règle pour une requête de métrique que vous avez définie dans Grafana. Pour plus d'informations, voir [Création d'une règle](/docs/services/cloud-monitoring/alerts/rules.html#create).

Par exemple, créez le fichier de règle `s-rule-1.json` dans le répertoire `~/cloud-monitoring/rules/`. 

```
{
"name": "checkbytesin",
    "description": "MH check Bytes In per second",
    "expression": "movingAverage(messagehub.65qser11-8034-1234-5678-c82fb42wdfgh.1.kafka-java-console-sample-topic.BytesInPerSec.15MinuteRate,\"5min\")",
    "enabled": true,
    "from": "-5min",
    "until": "now",
    "comparison": "above",
    "comparison_scope": "last",
    "error_level" : 27,
    "warning_level" : 25,
    "frequency": "1min",
    "dashboard_url": "https://metrics.ng.bluemix.net",
    "notifications": [
"NOTIFICATION_NAME"
]
}
```
{: screen}

Puis exportez la variable *RULE_FILE*:
	
```
export RULE_FILE="s-rule-1.json"
```
{: screen}

## Etape 2 : Enregistrement de la règle dans le service Monitoring
{: #step2}
	
A partir d'un terminal, procédez comme suit :

1. Connectez-vous à une région, une organisation et un espace dans {{site.data.keyword.Bluemix_notm}}. 

    Pour plus d'informations, voir [Comment se connecter à {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login).

2. Obtenez le jeton de sécurité. Vous pouvez utiliser un jeton UAA, un jeton IAM ou une clé d'API. Choisissez l'une des méthodes suivantes pour obtenir le jeton de sécurité :
	
	* Pour obtenir un jeton, voir [Obtention du jeton UAA à l'aide de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security/auth_uaa.html#uaa_cli).
	
	* Pour obtenir un jeton IAM, voir [Obtention du jeton IAM à l'aide de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security/auth_iam.html#auth_iam).
	
	* Pour obtenir une clé d'API, voir [Obtention d'une clé d'API](/docs/services/cloud-monitoring/security/auth_api_key.html#auth_api_key).
	
	Par exemple, pour utiliser le jeton IAM, exécutez la commande suivante :

    ```
	ibmcloud iam oauth-tokens
	```
	{: codeblock}
	
	Le résultat de cette commande est le suivant :
	
	```
	IAM token:  Bearer djn.._l_HWtlNTibmcloudslibmclouds0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	Exportez ensuite la variable *Token* :
	
	```
	export Token="djn.._l_HWtlNTibmcloudslibmclouds0qjBI9GqCnuQ"
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
	
	Exportez ensuite la variable *Space* :
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. Exécutez la commande cURL suivante pour enregistrer une règle :
	
    ```
	curl -XPOST -d @$RULE_FILE --header "X-Auth-User-Token: Auth_Type ${Token}" METRICS_ENDPOINT/v1/alert/rule
	```
	{: screen}
	
	où
	
	* RULE_FILE est le fichier JSON qui définit votre règle d'alerte.
	
	* *X-Auth-User-Token* est un paramètre qui transmet le jeton UAA, le jeton IAM ou la clé d'API.
	
	* *Auth_Type* est le préfixe qui définit le type de jeton ou de clé d'API. Les valeurs valides sont : *apikey*, *iam* ou *uaa*, où

        * *apikey* identifie le jeton comme étant une clé d'API.
		* *iam* identifie le jeton spécifié comme étant un jeton généré par IAM.
		* *uaa* identifie le jeton spécifié comme étant un jeton généré par UAA.
	
	* *X-Auth-Scope-Id* est un paramètre qui transmet l'identificateur global unique de l'espace. L'identificateur global unique doit avoir le préfixe *s-* pour identifier un espace. Cet en-tête est requis si vous utilisez un jeton d'authentification UAA. Si vous utilisez un jeton d'authentification IAM, cet en-tête est facultatif et les informations de domaine qui sont associées au jeton sont utilisées.
	
	* TOKEN est le jeton d'identification UAA ou IAM ou la clé d'API.
	
	* SPACE est l'identificateur global unique de l'espace. 
	
	* METRICS_ENDPOINT représente le point d'entrée vers le service. Chaque région a une adresse URL différente. Pour la liste des noeuds finaux par région, voir [Noeuds finaux](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).
	
	Pour vérifier que la règle a été créée, exécutez la commande suivante :
	
	```
	curl -XGET --header "X-Auth-User-Token:iam ${Token}" METRICS_ENDPOINT/v1/alert/rule/checkbytesin
	```
	{: codeblock}
	
	Par exemple

    ```
	curl -XGET --header "X-Auth-User-Token:iam ${Token}" https://metrics.ng.bluemix.net/v1/alert/rule/checkbytesin
	```
	{: screen}

## Etape 3 : Création d'une notification par courrier électronique
{: #step3}


Prenez en compte les informations suivantes pour créer un fichier de notification qui envoie un courrier électronique :

* Utilisez le modèle de notification pour l'envoi de courriers électroniques. Pour plus d'informations, voir [Modèles de notification](/docs/services/cloud-monitoring/config_alerts_ov.html#notification_template).
* Créez le fichier dans un répertoire local, par exemple, `~/cloud-monitoring/notifications`.

Par exemple, créez le fichier **email.json** à l'aide de l'éditeur vi : 
	
```
{
"name": "NOTIFICATION_NAME",
"type": "Email",
"description" : "Send email to manager of department X when ....",
"detail": "Enter email address, for example, xxx@yyy"
}
```
{: codeblock}	
	
Pour plus d'informations, voir [Création d'une notification](/docs/services/cloud-monitoring/alerts/notifications.html#notifications_create).
	
## Etape 4 : Enregistrement de la méthode de notification dans le service Monitoring
{: #step4}
	
A partir d'un terminal, procédez comme suit :

1. Connectez-vous à une région, une organisation et un espace dans {{site.data.keyword.Bluemix_notm}}. 

    Pour plus d'informations, voir [Comment se connecter à {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login).

2. Obtenez le jeton de sécurité. Vous pouvez utiliser un jeton UAA, un jeton IAM ou une clé d'API. Choisissez l'une des méthodes suivantes pour obtenir le jeton de sécurité :
	
	* Pour obtenir un jeton, voir [Obtention du jeton UAA à l'aide de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security/auth_uaa.html#uaa_cli).
	
	* Pour obtenir un jeton IAM, voir [Obtention du jeton IAM à l'aide de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security/auth_iam.html#auth_iam).
	
	* Pour obtenir une clé d'API, voir [Obtention d'une clé d'API](/docs/services/cloud-monitoring/security/auth_api_key.html#auth_api_key).
	
	Par exemple, pour utiliser le jeton IAM, exécutez la commande suivante :

    ```
	ibmcloud iam oauth-tokens
	```
	{: codeblock}
	
	Le résultat de cette commande est le suivant :
	
	```
	IAM token:  Bearer djn.._l_HWtlNTibmcloudslibmclouds0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	Exportez ensuite la variable *Token* :
	
	```
	export Token="djn.._l_HWtlNTibmcloudslibmclouds0qjBI9GqCnuQ"
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
	
	Exportez ensuite la variable *Space* :
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. Exécutez la commande cURL suivante pour enregistrer une notification :

    ```
	curl -XPOST -d @$NOTIFICATION_FILE --header "X-Auth-User-Token: Auth_Type ${Token}" METRICS_ENDPOINT/v1/alert/notification
	```
	{: screen}
	
	où
	
	* NOTIFICATION_FILE est le fichier JSON qui définit votre notification.
	
	* *X-Auth-User-Token* est un paramètre qui transmet le jeton UAA, le jeton IAM ou la clé d'API {{site.data.keyword.Bluemix_notm}}.
	
	* *Auth_Type* est le préfixe qui définit le type de jeton ou de clé d'API. Les valeurs valides sont : *apikey*, *iam* ou *uaa*, où

        * *apikey* identifie le jeton comme étant une clé d'API.
		* *iam* identifie le jeton spécifié comme étant un jeton généré par IAM.
		* *uaa* identifie le jeton spécifié comme étant un jeton généré par UAA.
	
	* *X-Auth-Scope-Id* est un paramètre qui transmet l'identificateur global unique de l'espace. L'identificateur global unique doit avoir le préfixe *s-* pour identifier un espace. Cet en-tête est requis si vous utilisez un jeton d'authentification UAA. Si vous utilisez un jeton d'authentification IAM, cet en-tête est facultatif et les informations de domaine qui sont associées au jeton sont utilisées.
	
	* TOKEN est le jeton d'identification UAA ou IAM ou la clé d'API.
	
	* SPACE est l'identificateur global unique de l'espace. 
	
	* METRICS_ENDPOINT représente le point d'entrée vers le service. Chaque région a une adresse URL différente. Pour la liste des noeuds finaux par région, voir [Noeuds finaux](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).
	
    Pour vérifier que la notification a été créée, exécutez la commande suivante :

	```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" METRICS_ENDPOINT/v1/alert/notification/NOTIFICATION_NAME
	```
	{: codeblock}
	
	Par exemple :
	
    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" https://metrics.ng.bluemix.net/v1/alert/notification/NOTIFICATION_NAME
	```
	{: screen}
	


    
   
  


 
	  
