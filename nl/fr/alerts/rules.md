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


# Règles CRUD
{: #rules}

Utilisez l'API Alerts pour créer, supprimer ou mettre à jour une règle, afficher les détails d'une règle et répertorier les règles définies dans un espace.
{:shortdesc}


## Création d'une règle
{: #create}

Pour configurer une règle dans le service {{site.data.keyword.monitoringshort}}, créez un fichier de règle qui contient les détails de la règle et enregistrez la règle dans le service {{site.data.keyword.monitoringshort}}.

Procédez comme suit :

1. Créez un fichier de règle contenant un code JSON valide. Sauvegardez le fichier. 

    Par exemple, afin de sauvegarder le fichier, utilisez un préfixe, tel que *s-*, pour les règles que vous définissez pour les requêtes qui s'exécutent dans un espace.
	
	**Astuces :** 
	
	* Définissez des règles différentes pour une requête afin de signaler des erreurs ou des avertissements à l'aide d'une méthode de notification différente. 
	* Créez votre fichier de règle dans le répertoire *~/cloud-monitoring/rules/* afin de regrouper les ressources du service {{site.data.keyword.monitoringshort_notm}}. 

    Entrez les informations suivantes dans le fichier de règle :
	
	* *name* : entrez un nom unique. La valeur de cette zone sera utilisée ultérieurement pour mettre à jour ou supprimer la règle, ou afficher ses détails.
	* *description* : entrez une description.
	* *expression* : entrez la requête à surveiller.
	* *enabled* : définissez *true* pour activer la règle.
	* *from* : point de départ pour l'analyse des données en fonction des valeurs de seuil.
	* *until*: point de fin pour l'analyse des données en fonction des valeurs de seuil.
	* *comparison* : opération de comparaison utilisée pour identifier le type de vérification à effectuer, par exemple *below*.
	* *error_level* : définit le seul que vous avez configuré pour le déclenchement d'une alerte d'erreur.
	* *warning_level* : définit le seul que vous avez configuré pour le déclenchement d'une alerte d'avertissement.
	* *frequency* : définit la fréquence à laquelle vous vérifiez les données.
	* *dashboard_url* : définit une adresse URL qui affiche un tableau comportant la requête dans Grafana.
	* *notifications* : méthode de notification si l'alerte décrite par cette règle est déclenchée.
	
	Par exemple, le fichier de règle myrulefile.json se présente comme suit :
	
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
      "emailXXX"
    ]
    }
    ```
	{: screen}
	
	Puis exportez la variable *RULE_FILE* :
	
	```
	export RULE_FILE="myrulefile.json"
	```
	{: screen}
	
2. Connectez-vous à une région, une organisation et un espace dans {{site.data.keyword.Bluemix_notm}}.

    Pour plus d'informations, voir [Comment se connecter à {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login).

3. Obtenez le jeton de sécurité. Vous pouvez utiliser un jeton UAA, un jeton IAM ou une clé d'API. Choisissez l'une des méthodes suivantes pour obtenir le jeton de sécurité :
	
	* Pour obtenir un jeton UAA, voir [Obtention du jeton UAA à l'aide de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}} CLI](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_uaa#uaa_cli.
	
	* Pour obtenir un jeton IAM, voir [Obtention du jeton IAM à l'aide de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_iam#auth_iam).
	
	* Pour obtenir une clé d'API, voir [Obtention d'une clé d'API](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_api_key#auth_api_key).
	
	Par exemple, pour utiliser le jeton IAM, exécutez la commande suivante :
    
    ```
    ibmcloud iam oauth-tokens
    ```
    {: codeblock}
	
    Le résultat de cette commande est le suivant :
	
    ```
    IAM token:  Bearer djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
    ```
    {: screen}
	
    Exportez ensuite la variable *Token* :
	
    ```
    export Token="djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ"
    ```
    {: screen}
	
    **Remarque :** le jeton exclut *Bearer*.
	
4. Obtenez l'identificateur global unique de l'espace. L'identificateur global unique doit avoir le préfixe *s-* pour identifier un espace.

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
	
5. Exécutez la commande cURL suivante pour enregistrer la règle dans le service {{site.data.keyword.monitoringshort}} :

    ```
	curl -XPOST -d @$RULE_FILE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/rule
	```
	{: codeblock}
	
	où
	
	* RULE_FILE est le fichier JSON qui définit votre règle d'alerte.
	
	* *X-Auth-User-Token* est un paramètre qui transmet le jeton UAA, le jeton IAM ou la clé d'API {{site.data.keyword.Bluemix_notm}}.
	
	* *Auth_Type* est le préfixe qui définit le type de jeton ou de clé d'API. Les valeurs valides sont : *apikey*, *iam* ou *uaa*, où

        * *apikey* identifie le jeton comme étant une clé d'API.
		* *iam* identifie le jeton spécifié comme étant un jeton généré par IAM.
		* *uaa* identifie le jeton spécifié comme étant un jeton généré par UAA.
	
	* *X-Auth-Scope-Id* est un paramètre qui transmet l'identificateur global unique de l'espace. L'identificateur global unique doit avoir le préfixe *s-* pour identifier un espace. Cet en-tête est requis si vous utilisez un jeton d'authentification UAA. Si vous utilisez un jeton d'authentification IAM, cet en-tête est facultatif et les informations de domaine qui sont associées au jeton sont utilisées.
	
	* TOKEN est le jeton d'identification UAA ou IAM ou la clé d'API.
	
	* SPACE est l'identificateur global unique de l'espace. 
	
	* METRICS_ENDPOINT représente le point d'entrée vers le service. Chaque région a une adresse URL différente. Pour la liste des noeuds finaux par région, voir [Noeuds finaux](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints).
	
    Par exemple 	
	
	```
	curl -XPOST -d @$RULE_FILE --header "X-Auth-User-Token:iam ${Token}" https://metrics.ng.bluemix.net/v1/alert/rule
	```
	{: screen}

## Suppression d'une règle
{: #delete}

Pour supprimer une règle, procédez comme suit :

1. Connectez-vous à une région, une organisation et un espace dans {{site.data.keyword.Bluemix_notm}}. 

    Pour plus d'informations, voir [Comment se connecter à {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login).

2. Obtenez le jeton de sécurité. Vous pouvez utiliser un jeton UAA, un jeton IAM ou une clé d'API. Choisissez l'une des méthodes suivantes pour obtenir le jeton de sécurité :
	
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
	IAM token:  Bearer djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	Exportez ensuite la variable *Token* :
	
	```
	export Token="djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ"
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
		
4. Exécutez la commande cURL suivante pour supprimer une règle :

    ```
	curl -XDELETE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/rule/Rule_Name
	```
	{: codeblock}
	
	où
	
    * *X-Auth-User-Token* est un paramètre qui transmet le jeton UAA, le jeton IAM ou la clé d'API.
	
	* *Auth_Type* est le préfixe qui définit le type de jeton ou de clé d'API. Les valeurs valides sont : *apikey*, *iam* ou *uaa*, où

        * *apikey* identifie le jeton comme étant une clé d'API.
		* *iam* identifie le jeton spécifié comme étant un jeton généré par IAM.
		* *uaa* identifie le jeton spécifié comme étant un jeton généré par UAA.
	
	* *X-Auth-Scope-Id* est un paramètre qui transmet l'identificateur global unique de l'espace. L'identificateur global unique doit avoir le préfixe *s-* pour identifier un espace. Cet en-tête est requis si vous utilisez un jeton d'authentification UAA. Si vous utilisez un jeton d'authentification IAM, cet en-tête est facultatif et les informations de domaine qui sont associées au jeton sont utilisées.
	
	* TOKEN est le jeton d'identification UAA ou IAM ou la clé d'API.
	
	* SPACE est l'identificateur global unique de l'espace. 
	
	* Rule_Name est le nom de la règle tel que spécifié dans la zone *name*.
	
	* METRICS_ENDPOINT représente le point d'entrée vers le service. Chaque région a une adresse URL différente. Pour la liste des noeuds finaux par région, voir [Noeuds finaux](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints).
	
    
	
## Affichage de toutes les règles
{: #list}

Pour répertorier toutes les règles, procédez comme suit :

1. Connectez-vous à une région, une organisation et un espace dans {{site.data.keyword.Bluemix_notm}}. 

    Pour plus d'informations, voir [Comment se connecter à {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login).

2. Obtenez le jeton de sécurité. Vous pouvez utiliser un jeton UAA, un jeton IAM ou une clé d'API. Choisissez l'une des méthodes suivantes pour obtenir le jeton de sécurité :
	
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
	IAM token:  Bearer djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	Exportez ensuite la variable *Token* :
	
	```
	export Token="djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ"
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
	
4. Exécutez la commande cURL suivante pour répertorier toutes les règles dans un espace :

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/rules
	```
	{: codeblock}
	
	où
	
	* *X-Auth-User-Token* est un paramètre qui transmet le jeton UAA, le jeton IAM ou la clé d'API.
	
	* *Auth_Type* est le préfixe qui définit le type de jeton ou de clé d'API. Les valeurs valides sont : *apikey*, *iam* ou *uaa*, où

        * *apikey* identifie le jeton comme étant une clé d'API.
		* *iam* identifie le jeton spécifié comme étant un jeton généré par IAM.
		* *uaa* identifie le jeton spécifié comme étant un jeton généré par UAA.
	
	* *X-Auth-Scope-Id* est un paramètre qui transmet l'identificateur global unique de l'espace. L'identificateur global unique doit avoir le préfixe *s-* pour identifier un espace. Cet en-tête est requis si vous utilisez un jeton d'authentification UAA. Si vous utilisez un jeton d'authentification IAM, cet en-tête est facultatif et les informations de domaine qui sont associées au jeton sont utilisées.
	
	* TOKEN est le jeton d'identification UAA ou IAM ou la clé d'API.
	
	* SPACE est l'identificateur global unique de l'espace. 
	
	* METRICS_ENDPOINT représente le point d'entrée vers le service. Chaque région a une adresse URL différente. Pour la liste des noeuds finaux par région, voir [Noeuds finaux](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints).
	

	
	

## Affichage des détails d'une règle
{: show}

Pour afficher les détails d'une règle, procédez comme suit :

1. Connectez-vous à une région, une organisation et un espace dans {{site.data.keyword.Bluemix_notm}}. 

    Pour plus d'informations, voir [Comment se connecter à {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login).

2. Obtenez le jeton de sécurité. Vous pouvez utiliser un jeton UAA, un jeton IAM ou une clé d'API. Choisissez l'une des méthodes suivantes pour obtenir le jeton de sécurité :
	
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
	IAM token:  Bearer djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	Exportez ensuite la variable *Token* :
	
	```
	export Token="djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ"
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
	
4. Exécutez la commande cURL suivante pour afficher les détails d'une règle :

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/rule/Rule_Name
	```
	{: codeblock}
	
	où
	
	* *X-Auth-User-Token* est un paramètre qui transmet le jeton UAA, le jeton IAM ou la clé d'API.
	
	* *Auth_Type* est le préfixe qui définit le type de jeton ou de clé d'API. Les valeurs valides sont : *apikey*, *iam* ou *uaa*, où

        * *apikey* identifie le jeton comme étant une clé d'API.
		* *iam* identifie le jeton spécifié comme étant un jeton généré par IAM.
		* *uaa* identifie le jeton spécifié comme étant un jeton généré par UAA.
	
	* *X-Auth-Scope-Id* est un paramètre qui transmet l'identificateur global unique de l'espace. L'identificateur global unique doit avoir le préfixe *s-* pour identifier un espace. Cet en-tête est requis si vous utilisez un jeton d'authentification UAA. Si vous utilisez un jeton d'authentification IAM, cet en-tête est facultatif et les informations de domaine qui sont associées au jeton sont utilisées.
	
	* TOKEN est le jeton d'identification UAA ou IAM ou la clé d'API.
	
	* SPACE est l'identificateur global unique de l'espace. 
	
	* Rule_Name est le nom de la règle tel que spécifié dans la zone *name*.
	
	* METRICS_ENDPOINT représente le point d'entrée vers le service. Chaque région a une adresse URL différente. Pour la liste des noeuds finaux par région, voir [Noeuds finaux](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints).
	

## Mise à jour d'une règle
{: #update}

Pour mettre à jour une règle, modifiez-la en mettant à jour le fichier de règle, puis procédez comme suit :

1. Connectez-vous à une région, une organisation et un espace dans {{site.data.keyword.Bluemix_notm}}. 

    Pour plus d'informations, voir [Comment se connecter à {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login).

2. Obtenez le jeton de sécurité. Vous pouvez utiliser un jeton UAA, un jeton IAM ou une clé d'API. Choisissez l'une des méthodes suivantes pour obtenir le jeton de sécurité :
	
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
	IAM token:  Bearer djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	Exportez ensuite la variable *Token* :
	
	```
	export Token="djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ"
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
	
4. Exécutez la commande cURL suivante pour mettre à jour une règle :

    ```
	curl -XPUT `-d @$RULE_FILE` --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/rule
	```
	{: codeblock}
	
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
	
	* METRICS_ENDPOINT représente le point d'entrée vers le service. Chaque région a une adresse URL différente. Pour la liste des noeuds finaux par région, voir [Noeuds finaux](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints).

	
	
