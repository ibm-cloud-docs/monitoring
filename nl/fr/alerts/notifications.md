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


# Notifications CRUD
{: #notifications}

Utilisez l'API Alerts pour créer, supprimer et mettre à jour une notification, afficher les détails d'une notification, et répertorier les notifications qui sont définies dans un espace.
{:shortdesc}

## Création d'une notification
{: #notifications_create}

Pour créer une notification, procédez comme suit :

1. Créez un fichier de notification.

    1. Utilisez un modèle de notification pour créer un fichier de notification. Pour plus d'informations, voir [Modèles de notification](/docs/services/cloud-monitoring?topic=cloud-monitoring-config_alerts_ov#notification_template).
	
	2. Mettez à jour le fichier :
	
	    * Entrez un nom unique dans la zone *name*. La valeur de cette zone sera utilisée ultérieurement pour mettre à jour ou supprimer la notification, ou afficher ses détails.
		* Entrez une description.
		* Entrez une adresse électronique, un noeud final d'URL ou une clé PagerDuty valide.
		
	3. Sauvegardez le fichier. Par exemple, utilisez un préfixe, tel que *s-* pour les notifications que vous définissez pour les requêtes qui s'exécutent dans un espace.
	
	    **Astuce :** créez votre fichier de notification dans le répertoire *~/cloud-monitoring/notifications/* afin de regrouper les ressources du service {{site.data.keyword.monitoringshort_notm}}. 
	
	4. Exportez la variable *NOTIFICATION_FILE*:
	
	```
	export NOTIFICATION_FILE="mynotificationfile.json"
	```
	{: screen}
	
2. Connectez-vous à une région, une organisation et un espace dans {{site.data.keyword.Bluemix_notm}}. 

    Pour plus d'informations, voir [Comment se connecter à {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login).

3. Obtenez le jeton de sécurité. Vous pouvez utiliser un jeton UAA, un jeton IAM ou une clé d'API. Choisissez l'une des méthodes suivantes pour obtenir le jeton de sécurité :
	
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
	
5. Enregistrez une notification dans le service {{site.data.keyword.monitoringshort}}.

    ```
	curl -XPOST -d @$NOTIFICATION_FILE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notification
	```
	{: codeblock}
	
	où
	
	* NOTIFICATION_FILE est le fichier JSON qui définit votre notification.
	
	* *X-Auth-User-Token* est un paramètre qui transmet le jeton UAA, le jeton IAM ou la clé d'API {{site.data.keyword.Bluemix_notm}}.
	
	* *Auth_Type* est le préfixe qui définit le type de jeton ou de clé d'API. Les valeurs valides sont : *apikey*, *iam* ou *uaa*, où

        * *apikey* identifie le jeton comme étant une clé d'API.
		* *iam* identifie le jeton spécifié comme étant un jeton généré par IAM.
		* *uaa* identifie le jeton spécifié comme étant un jeton généré par UAA.
	
	* *X-Auth-Scope-Id* est un paramètre qui transmet l'identificateur global unique de l'espace. L'identificateur global unique doit avoir le préfixe *s-* pour identifier un espace. Cet en-tête est requis si vous utilisez un jeton d'authentification UAA. Si vous utilisez un jeton d'authentification IAM, cet en-tête est facultatif et les informations de domaine qui sont associées au jeton sont utilisées.
	
	* Token est le jeton UAA, le jeton IAM ou la clé d'API.
	
	* SPACE est l'identificateur global unique de l'espace. 
	
	* METRICS_ENDPOINT représente le point d'entrée vers le service. Chaque région a une adresse URL différente. Pour la liste des noeuds finaux par région, voir [Noeuds finaux](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints).
	
    Par exemple 	
	
	```
	curl -XPOST -d @$NOTIFICATION_FILE  --header "X-Auth-User-Token: iam ${Token}" https://metrics.ng.bluemix.net/v1/alert/notification
	```
	{: screen}

## Suppression d'une notification
{: #notifications_delete}

Pour supprimer une notification, procédez comme suit :

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
	
	Exportez ensuite la variable *Space* :
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. Exécutez la commande cURL suivante pour supprimer une notification :

    ```
	curl -XDELETE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notification/Notification_Name
	```
	{: codeblock}
	
	où
	
	* *X-Auth-User-Token* est un paramètre qui transmet le jeton UAA, le jeton IAM ou la clé d'API.
	
	* *Auth_Type* est le préfixe qui définit le type de jeton ou de clé d'API. Les valeurs valides sont : *apikey*, *iam* ou *uaa*, où

        * *apikey* identifie le jeton comme étant une clé d'API.
		* *iam* identifie le jeton spécifié comme étant un jeton généré par IAM.
		* *uaa* identifie le jeton spécifié comme étant un jeton généré par UAA.
	
	* *X-Auth-User-Token* est un paramètre qui transmet le jeton UAA, le jeton IAM ou la clé d'API {{site.data.keyword.Bluemix_notm}}. Le jeton ou la clé d'API doit avoir pour préfixe l'une des valeurs suivantes : *apikey*, *iam* ou *uaa*, où

        * *apikey* identifie le jeton comme étant une clé d'API.
		* *iam* identifie le jeton spécifié comme étant un jeton généré par IAM.
		* *uaa* identifie le jeton spécifié comme étant un jeton généré par UAA.
		
	* Token est le jeton UAA, le jeton IAM ou la clé d'API.
	
	* SPACE est l'identificateur global unique de l'espace. 
	
	* Notification_Name est le nom de la notification, c'est-à-dire la valeur de la zone *name* lorsque vous répertoriez les propriétés d'une notification.
	
	* METRICS_ENDPOINT représente le point d'entrée vers le service. Chaque région a une adresse URL différente. Pour la liste des noeuds finaux par région, voir [Noeuds finaux](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints).
	


## Affichage de toutes les notifications
{: #notifications_list}

Pour répertorier toutes les notifications, procédez comme suit :

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
	
	Exportez ensuite la variable *Space* :
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. Exécutez la commande cURL suivante pour répertorier toutes les notifications :

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notifications
	```
	{: codeblock}
	
	où
	
	* *X-Auth-User-Token* est un paramètre qui transmet le jeton UAA, le jeton IAM ou la clé d'API {{site.data.keyword.Bluemix_notm}}.
	
	* *Auth_Type* est le préfixe qui définit le type de jeton ou de clé d'API. Les valeurs valides sont : *apikey*, *iam* ou *uaa*, où

        * *apikey* identifie le jeton comme étant une clé d'API.
		* *iam* identifie le jeton spécifié comme étant un jeton généré par IAM.
		* *uaa* identifie le jeton spécifié comme étant un jeton généré par UAA.
		
	* *X-Auth-User-Token* est un paramètre qui transmet le jeton UAA, le jeton IAM ou la clé d'API {{site.data.keyword.Bluemix_notm}}. Le jeton ou la clé d'API doit avoir pour préfixe l'une des valeurs suivantes : *apikey*, *iam* ou *uaa*, où

        * *apikey* identifie le jeton comme étant une clé d'API.
		* *iam* identifie le jeton spécifié comme étant un jeton généré par IAM.
		* *uaa* identifie le jeton spécifié comme étant un jeton généré par UAA.
		
	* Token est le jeton UAA, le jeton IAM ou la clé d'API.
	
	* SPACE est l'identificateur global unique de l'espace. 
	
	* METRICS_ENDPOINT représente le point d'entrée vers le service. Chaque région a une adresse URL différente. Pour la liste des noeuds finaux par région, voir [Noeuds finaux](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints).

			

## Affichage des détails d'une notification
{: #show}


Pour afficher les informations relatives à une notification, procédez comme suit :

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
	
	Exportez ensuite la variable *Space* :
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. Exécutez la commande cURL suivante pour afficher les détails d'une notification :

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notification/NOTIFICATION_NAME
	```
	{: codeblock}
	
	où
	
	* *X-Auth-User-Token* est un paramètre qui transmet le jeton UAA, le jeton IAM ou la clé d'API {{site.data.keyword.Bluemix_notm}}.
	
	* *Auth_Type* est le préfixe qui définit le type de jeton ou de clé d'API. Les valeurs valides sont : *apikey*, *iam* ou *uaa*, où

        * *apikey* identifie le jeton comme étant une clé d'API.
		* *iam* identifie le jeton spécifié comme étant un jeton généré par IAM.
		* *uaa* identifie le jeton spécifié comme étant un jeton généré par UAA.
		
	* Token est le jeton UAA, le jeton IAM ou la clé d'API.
	
	* SPACE est l'identificateur global unique de l'espace. 
	
	* NOTIFICATION_NAME est le nom de la notification, c'est-à-dire la valeur de la zone *name* lorsque vous répertoriez les propriétés d'une notification.
	
	* METRICS_ENDPOINT représente le point d'entrée vers le service. Chaque région a une adresse URL différente. Pour la liste des noeuds finaux par région, voir [Noeuds finaux](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints).
	
     
		

			
## Test d'une notification
{: #test}	
			
Pour tester une notification, procédez comme suit :

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
	
	Exportez ensuite la variable *Space* :
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. Exécutez la commande cURL suivante pour tester une notification :

    ```
	curl -XPOST --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notification/test/NOTIFICATION_NAME
	```
	{: codeblock}
	
	où
	
	* *X-Auth-User-Token* est un paramètre qui transmet le jeton UAA, le jeton IAM ou la clé d'API {{site.data.keyword.Bluemix_notm}}.
	
	* *Auth_Type* est le préfixe qui définit le type de jeton ou de clé d'API. Les valeurs valides sont : *apikey*, *iam* ou *uaa*, où

        * *apikey* identifie le jeton comme étant une clé d'API.
		* *iam* identifie le jeton spécifié comme étant un jeton généré par IAM.
		* *uaa* identifie le jeton spécifié comme étant un jeton généré par UAA.
	
	* *X-Auth-User-Token* est un paramètre qui transmet le jeton UAA, le jeton IAM ou la clé d'API {{site.data.keyword.Bluemix_notm}}. Le jeton ou la clé d'API doit avoir pour préfixe l'une des valeurs suivantes : *apikey*, *iam* ou *uaa*, où

        * *apikey* identifie le jeton comme étant une clé d'API.
		* *iam* identifie le jeton spécifié comme étant un jeton généré par IAM.
		* *uaa* identifie le jeton spécifié comme étant un jeton généré par UAA.
		
	* Token est le jeton UAA, le jeton IAM ou la clé d'API.
	
	* SPACE est l'identificateur global unique de l'espace. 
	
	* NOTIFICATION_NAME est le nom de la notification, c'est-à-dire la valeur de la zone *name* lorsque vous répertoriez les propriétés d'une notification.
	
	* METRICS_ENDPOINT représente le point d'entrée vers le service. Chaque région a une adresse URL différente. Pour la liste des noeuds finaux par région, voir [Noeuds finaux](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints).
	


## Mise à jour d'une notification
{: #notifications_update}

Pour mettre à jour une notification, procédez comme suit :

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
	
	Exportez ensuite la variable *Space* :
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. Exécutez la commande cURL suivante pour mettre à jour une notification :

    ```
	curl -XPUT -d @$NOTIFICATION_FILE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notification
	```
	{: codeblock}
	
	où
	
	* NOTIFICATION_FILE est le fichier JSON qui définit votre notification.
	
	* *Auth_Type* est le préfixe qui définit le type de jeton ou de clé d'API. Les valeurs valides sont : *apikey*, *iam* ou *uaa*, où

        * *apikey* identifie le jeton comme étant une clé d'API.
		* *iam* identifie le jeton spécifié comme étant un jeton généré par IAM.
		* *uaa* identifie le jeton spécifié comme étant un jeton généré par UAA.
	
	* *X-Auth-User-Token* est un paramètre qui transmet le jeton UAA, le jeton IAM ou la clé d'API Bluemix. Le jeton ou la clé d'API doit avoir pour préfixe l'une des valeurs suivantes : *apikey*, *iam* ou *uaa*, où

        * *apikey* identifie le jeton comme étant une clé d'API.
		* *iam* identifie le jeton spécifié comme étant un jeton généré par IAM.
		* *uaa* identifie le jeton spécifié comme étant un jeton généré par UAA.
		
	* Token est le jeton UAA, le jeton IAM ou la clé d'API.
	
	* SPACE est l'identificateur global unique de l'espace. 

	* METRICS_ENDPOINT représente le point d'entrée vers le service. Chaque région a une adresse URL différente. Pour la liste des noeuds finaux par région, voir [Noeuds finaux](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints).
	
        

