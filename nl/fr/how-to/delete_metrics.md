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



# Suppression des métriques
{: #delete_metrics}

Vous pouvez supprimer des métriques du service {{site.data.keyword.monitoringshort}} à l'aide de l'[API Metrics](https://console.bluemix.net/apidocs/monitoring-metrics-api).
{:shortdesc}

Après vous être [connecté à une région dans {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login), suivez les instructions fournies ci-dessous pour supprimer une notification :


## Etape 1 : Obtention du jeton de sécurité
{: #step1_delete_metrics}

Vous pouvez utiliser un jeton UAA, un jeton IAM ou une clé d'API. 

Choisissez l'une des méthodes suivantes pour obtenir le jeton de sécurité :
	
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
	
## Etape 2 : Vérification des droits d'utilisation des métriques 
{: #step2_delete_metrics}

Suivant le domaine où se trouvent les métriques, vous devrez tenir compte des informations suivantes :

* Pour travailler avec des métriques qui sont disponibles dans un domaine d'espace, l'utilisateur nécessite un rôle *developer* dans l'espace Cloud Foundry associé au domaine. 
* Pour travailler avec des métriques qui sont disponibles dans le domaine de compte, l'utilisateur nécessite une règle IAM avec le rôle *administrator*, le rôle *operator* ou le rôle *editor*.

Pour vérifier vos droits d'utilisateur, procédez comme suit :

1. Connectez vous à la console {{site.data.keyword.Bluemix_notm}}.

    Ouvrez un navigateur Web et démarrez le tableau de bord {{site.data.keyword.Bluemix_notm}} : [http://console.bluemix.net ![Icône de lien externe](../../../icons/launch-glyph.svg "Icône de lien externe")](http://bluemix.net){:new_window}
	
	Après que vous vous êtes connecté avec votre ID utilisateur et votre mot de passe, l'interface utilisateur {{site.data.keyword.Bluemix_notm}} s'ouvre.

2. Dans la barre de menus, cliquez sur **Gérer > Compte > Utilisateurs**. 

    La fenêtre *Utilisateurs* affiche une liste d'utilisateurs avec leur adresse électronique pour le compte actuellement sélectionné.
	
3. Vérifiez les droits d'accès pour l'utilisation du service {{site.data.keyword.monitoringshort}}.


## Etape 3 : Obtention de l'ID d'espace 
{: #step3_delete_metrics}

Cette étape s'applique uniquement si vous souhaitez supprimer des métriques qui sont disponibles dans un domaine d'espace.

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

	

## Etape 4 : Etablissement d'une liste des métriques
{: #step4_delete_metrics}


Exécutez la commande cURL suivante pour répertorier les métriques disponibles dans un domaine d'espace :

```
curl -H "X-Auth-Scope-Id: ${Space}" -H “X-Auth-User-Token: Auth_Type ${TOKEN}" -XGET METRICS_ENDPOINT/v1/metrics/list?query=*

```
{: screen}

Exécutez la commande cURL suivante pour répertorier les métriques disponibles dans le domaine de compte :

```
curl -H "X-Auth-User-Token: apikey ${TOKEN}" -XGET METRICS_ENDPOINT/v1/metrics/list?query=*
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
	
* METRICS_ENDPOINT représente le point d'entrée vers le service. Chaque région a une adresse URL différente. Pour la liste des noeuds finaux par région, voir [Noeuds finaux](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).

* *query* définit le filtre qui est appliqué. Par exemple, `query=metric-service.*` affiche une liste de toutes les métriques qui existent sous la hiérarchie `metric-service.*` et `query=*` affiche une liste de toutes les métriques présentes dans le domaine.


## Etape 5 - Option 1 : Suppression de toutes les métriques
{: #step5_delete_metrics}
  

Exécutez la commande cURL suivante pour supprimer toutes les métriques dans un domaine d'espace :

```
curl -XDELETE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/metrics/list?query=*
```
{: screen}

Exécutez la commande cURL suivante pour supprimer toutes les métriques du domaine de compte :

```
curl -H "X-Auth-User-Token: Auth_Type ${Token}" -XDELETE  METRICS_ENDPOINT/v1/metrics/list?query=*
```
{: screen}

où
	
* *X-Auth-User-Token* est un paramètre qui transmet le jeton UAA {{site.data.keyword.Bluemix_notm}}.
	
* Auth_Type est le préfixe qui définit le type de jeton. Les valeurs valides sont : *uaa* pour un jeton UAA, *iam* pour un jeton IAM et *api* pour une clé d'API.
	
* *X-Auth-Scope-Id* est un paramètre qui transmet l'identificateur global unique de l'espace. L'identificateur global unique doit avoir le préfixe *s-* pour identifier un espace.
	
* *Token* représente le jeton de sécurité.
	
* *Space* représente l'identificateur global unique de l'espace. 
	
* *METRICS_ENDPOINT* représente le point d'entrée vers le service. Chaque région a une adresse URL différente. Pour la liste des noeuds finaux par région, voir [Noeuds finaux](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).

* *query* définit le filtre qui est appliqué. `query=*` indique toutes les métriques présentes dans le domaine.


## Etape 6 - Option 2 : Suppression de toutes les métriques d'un service
{: #step6_delete_metrics}
  

Exécutez la commande cURL suivante pour supprimer toutes les métriques d'un service dans un domaine d'espace :

```
curl -XDELETE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/metrics/list?query=metric-service.*
```
{: screen}

Exécutez la commande cURL suivante pour supprimer toutes les métriques du domaine de compte :

```
curl -H "X-Auth-User-Token: Auth_Type ${Token}" -XDELETE  METRICS_ENDPOINT/v1/metrics/list?query=metric-service.*
```
{: screen}

où
	
* *X-Auth-User-Token* est un paramètre qui transmet le jeton UAA {{site.data.keyword.Bluemix_notm}}.
	
* Auth_Type est le préfixe qui définit le type de jeton. Les valeurs valides sont : *uaa* pour un jeton UAA, *iam* pour un jeton IAM et *api* pour une clé d'API.
	
* *X-Auth-Scope-Id* est un paramètre qui transmet l'identificateur global unique de l'espace. L'identificateur global unique doit avoir le préfixe *s-* pour identifier un espace.
	
* *Token* représente le jeton de sécurité.
	
* *Space* représente l'identificateur global unique de l'espace. 
	
* *METRICS_ENDPOINT* représente le point d'entrée vers le service. Chaque région a une adresse URL différente. Pour la liste des noeuds finaux par région, voir [Noeuds finaux](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).

* *query* définit le filtre qui est appliqué. `query=*` indique toutes les métriques présentes dans le domaine.

* *metric-service.** est le nom d'un service. Par exemple, `containers-kubernetes`.
