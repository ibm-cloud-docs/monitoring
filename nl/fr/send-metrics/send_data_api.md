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

# Envoi de données à l'aide de l'API Metrics
{: #send_data_api}

Vous pouvez envoyer des métriques au service {{site.data.keyword.monitoringshort}} à l'aide de l'API Metrics. 
{:shortdesc}


Pour les conteneurs Docker {{site.data.keyword.Bluemix_notm}}, les métriques système de base sont collectées automatiquement. Pour les applications Cloud Foundry et les applications s'exécutant sur une machine virtuelle, les métriques doivent être envoyées directement depuis l'application à l'aide de l'[API Metrics](https://console.bluemix.net/apidocs/927-ibm-cloud-monitoring-rest-api?&language=node#introduction){: new_window}. 



## Envoi de métriques à un domaine d'espace
{: #space_uaa}

Pour envoyer des métriques à un espace à l'aide de cURL, procédez comme suit :

1. Connectez-vous à une région, une organisation et un espace dans {{site.data.keyword.Bluemix_notm}}. 

    Pour plus d'informations, voir [Comment se connecter à {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login).

2. Obtenez le jeton de sécurité. Vous pouvez utiliser un jeton UAA, un jeton IAM ou une clé d'API.

    Choisissez l'une des méthodes suivantes pour obtenir le jeton de sécurité nécessaire pour envoyer des métriques :
	
	* Pour obtenir un jeton UAA, voir [Obtention du jeton UAA à l'aide de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security/auth_uaa.html#uaa_cli);
	
	* Pour obtenir un jeton IAM, voir [Obtention du jeton IAM à l'aide de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security/auth_iam.html#auth_iam).
	
	* Pour obtenir une clé d'API, voir [Obtention d'une clé d'API](/docs/services/cloud-monitoring/security/auth_api_key.html#auth_api_key).
	
	Sur le terminal à partir duquel vous vous êtes connecté à {{site.data.keyword.Bluemix_notm}}, définissez la variable *Token* pour le jeton.

    Par exemple, définissez un jeton UAA et retirez la partie *Bearer* de la valeur de jeton :

    ```
    export Token="kjshdgf.....ldkdjdj"
    ```
    {: screen}
		
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
	
5. Exécutez la commande cURL suivante pour envoyer des métriques :

    ```
	curl -XPOST -d @Metric_File --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" Endpoint/v1/metrics
	```
	{: codeblock}
	
	où
	
	* Metrics_File représente le fichier JSON qui comporte la définition des métriques envoyées au service {{site.data.keyword.monitoringshort}}.
	
	* *X-Auth-User-Token* est un paramètre qui transmet le jeton de sécurité.
	
	* *Auth_Type* est le préfixe qui définit le type de jeton. Les valeurs valides sont : *uaa* pour un jeton UAA, *iam* pour un jeton IAM et *api* pour une clé d'API.
	
	* *X-Auth-Scope-Id* est un paramètre qui transmet l'identificateur global unique de l'espace. L'identificateur global unique doit avoir le préfixe *s-* pour identifier un espace.
	
	* Token représente le jeton de sécurité ou la clé d'API.
	
	* Space représente l'identificateur global unique de l'espace. 
	
	* Endpoint représente le point d'entrée vers le service. Chaque région a une adresse URL différente. Pour la liste des noeuds finaux par région, voir [Noeuds finaux](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).
	
	Par exemple, vous pouvez exécuter la commande suivante pour envoyer deux métriques, `myhost.cpu.idle` et `myapp.login.attempts`, au service {{site.data.keyword.monitoringshort}} :
	
	```
	curl -XPOST @metric.json --header "X-Auth-User-Token: uaa ${Token}" https://metrics.ng.bluemix.net/v1/metrics
	```
	{: screen}
	
	L'exemple de fichier *metric.json* est défini comme suit :

    ```
    [
      {
        "name" : "myhost.cpu.idle",
        "value" : 22.37
      },
      {
        "name": "myapp.login.retries",
        "value": 4
      }
    ]
	```
	{: screen}

 











 
