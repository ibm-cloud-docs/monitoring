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

# Extraction de métriques
{: #retrieve_data_api}

Vous pouvez extraire des métriques à partir du service {{site.data.keyword.monitoringshort}} à l'aide de l'[API Metrics](https://console.bluemix.net/apidocs/927-ibm-cloud-monitoring-rest-api?&language=node#introduction){: new_window}.
{:shortdesc}


## Extraction de métriques depuis un espace
{: #uaa}

Pour extraire des métriques à partir d'un espace, procédez comme suit :

1. Connectez-vous à une région, une organisation et un espace dans {{site.data.keyword.Bluemix_notm}}. 

    Pour plus d'informations, voir [Comment se connecter à {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login).

2. Définissez le jeton de sécurité ou la clé d'API
  
    Vous devez définir la zone **X-Auth-User-Token** avec un jeton de sécurité ou une clé d'API. Vous pouvez utiliser un jeton UAA, un jeton IAM ou une clé d'API.

    Tout d'abord, choisissez l'une des méthodes suivantes pour obtenir le jeton de sécurité nécessaire pour envoyer des métriques :
	
    * Pour obtenir un jeton, voir [Obtention du jeton UAA à l'aide de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_uaa#uaa_cli).
    
	* Pour obtenir un jeton IAM, voir [Obtention du jeton IAM à l'aide de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_iam#auth_iam).
    
	* Pour obtenir une clé d'API, voir [Obtention d'une clé d'API](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_api_key#auth_api_key). 

    Un jeton ou une clé d'API doit avoir pour préfixe l'une des valeurs suivantes : `apikey`, `iam` ou `uaa` 

    où 

    * *apikey* identifie le jeton comme étant une clé d'API.
    * *iam* identifie le jeton spécifié comme étant un jeton généré par IAM.
    * *uaa* identifie le jeton spécifié comme étant un jeton généré par UAA.

    Par exemple, vous pouvez définir l'en-tête suivant pour une clé d'API : `X-Auth-User-Token: apikey SomeIAMGeneratedKey`
	
	Ensuite, sur le terminal à partir duquel vous vous êtes connecté à {{site.data.keyword.Bluemix_notm}}, définissez la variable Token pour le jeton.

    Par exemple, définissez un jeton UAA et retirez la partie *Bearer* de la valeur de jeton :

    ```
    export Token="kjshdgf.....ldkdjdj"
    ```
    {: screen}
		
3. Obtenez l'ID d'espace.

    Pour l'extraction des métriques, la zone d'en-tête **X-Auth-Scope-Id** est requise et doit avoir pour valeur l'identificateur global unique d'espace. 

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

4. Exécutez la commande cURL suivante pour envoyer des métriques :

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/metrics?from=Start_Time&until=End_Time&target=string
	```
	{: codeblock}

	où
	
	* *X-Auth-User-Token* est un paramètre qui transmet le jeton UAA {{site.data.keyword.Bluemix_notm}}.
	
	* Auth_Type est le préfixe qui définit le type de jeton. Les valeurs valides sont : *uaa* pour un jeton UAA, *iam* pour un jeton IAM et *api* pour une clé d'API.
	
	* *X-Auth-Scope-Id* est un paramètre qui transmet l'identificateur global unique de l'espace. L'identificateur global unique doit avoir le préfixe *s-* pour identifier un espace. Cet en-tête est requis uniquement si vous utilisez l'authentification UAA. Si vous utilisez un jeton d'authentification IAM, cet en-tête est facultatif et les informations de domaine qui sont associées au jeton sont utilisées.
	
	* *Token* représente le jeton de sécurité.
	
	* *Space* représente l'identificateur global unique de l'espace. 
	
	* *Start_Time* définit le début de la demande. Cette information est utilisée pour calculer la période relative ou absolue. *End_Time* définit la fin de la demande. Cette information est utilisée pour calculer la période relative ou absolue. Pour plus d'informations, voir [Définition d'une période](/docs/services/cloud-monitoring/retrieve-metrics?topic=cloud-monitoring-retrieve_data_api#time).
	
	* *Path* identifie une ou plusieurs métriques. Vous pouvez éventuellement appliquer des fonctions à chaque métrique. Les chemins prennent également en charge l'utilisation des caractères génériques, ce qui vous permet d'identifier une ou plusieurs métriques dans un seul chemin. Pour plus d'informations, voir [Définition des métriques](/docs/services/cloud-monitoring/retrieve-metrics?topic=cloud-monitoring-retrieve_data_api#metrics).
	
	* *METRICS_ENDPOINT* représente le point d'entrée vers le service. Chaque région a une adresse URL différente. Pour la liste des noeuds finaux par région, voir [Noeuds finaux](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints).
	

	
## Définition des métriques
{: #metrics}

Pour extraire des données pour une métrique, vous devez spécifier le chemin d'accès à cette dernière à partir de la racine de l'arborescence des métriques et séparer chaque étape par un point (.).

Le chemin est spécifié dans le paramètre **Target**. Un maximum de 5 cibles peut être spécifié pour chaque demande.  

Vous pouvez éventuellement appliquer des fonctions à la métrique. Pour plus d'informations sur les fonctions prises en charge, voir [Fonctions Graphite 0.9.15 ![Icône de lien externe](../../../icons/launch-glyph.svg "Icône de lien externe")](http://graphite.readthedocs.io/en/latest/functions.html).

Vous pouvez utiliser des caractères génériques pour définir un chemin. L'utilisation de caractères génériques vous permet d'identifier plusieurs métriques dans un seul chemin. 

* **Astérisque** : Vous pouvez utiliser l'astérisque (*) pour zéro ou plusieurs caractères. 

    Un élément de chemin peut contenir plusieurs astérisques, par exemple, `servers.sp*aeg*r.cpu.total.*` Cet exemple renvoie des données sur le nombre total d'UC pour tous les serveurs qui correspondent à ce modèle.

* **Liste ou plage de caractères** : Vous pouvez définir des caractères entre crochets ([...]) pour spécifier un seul emplacement de caractère dans la chaîne qui compose le chemin. 

    Vous pouvez définir une plage inclusive de caractères en spécifiant deux caractères séparés par un trait d'union (-). Une correspondance sera trouvée pour tout caractère placé entre ces deux caractères. 
	
	Vous pouvez définir une ou plusieurs plages de caractères entre crochets. 
	
	Lorsque les caractères inclus entre crochets ne peuvent pas être lus en tant que plage, ils sont traités comme une liste de valeurs. 
	
	Vous pouvez inclure un trait d'union (-) comme caractère dans une liste de valeurs en le plaçant au début ou à la fin des crochets.

* **Liste de valeurs** : Vous pouvez définir des valeurs séparées par une virgule entre accolades pour définir des listes de valeurs. 

    Par exemple, pour télécharger des métriques pour les chemins `servers.myserver.cpu.total.user` et `servers.myserver.cpu.total.system`, vous pouvez définir un seul et même chemin pour les deux types : `servers.myserver.cpu.total.{user,system}`



## Définition d'une période
{: #time}

Vous pouvez éventuellement spécifier une période en utilisant un temps relatif ou un temps absolu. Vous devez définir les paramètres de requête **From** et **Until**.  

* Lorsque l'heure de début de la période est omise, la valeur par défaut correspond à 24 heures en arrière. 

* Lorsque l'heure de fin de la période est omise, la valeur par défaut correspond à l'heure en cours *now*.

Le paramètre de **temps relatif** est toujours précédé du signe moins (-) et suivi d'une unité de temps. 

Le tableau suivant répertorie les différentes abréviations de temps relatives que vous pouvez utiliser :


| Abréviation | Description |
|--------------|-------------|
| s            | Secondes     |
| min          | Minutes     |
| h            | Heures       |
| d            | Jours        |
| w            | Semaines       |
| mon          | Mois      |
| now          | Heure en cours |


Vous pouvez utiliser n'importe quel des formats suivants pour définir un **temps absolu** : `HH:MM_YYMMDD`, `YYYYMMDD`, `MM/DD/YY`

| Abréviation | Description |
|--------------|-------------|
| YYYY         | Année à quatre chiffres |
| MM           | Mois à deux chiffres (01=Jan etc) |
| DD           | Jour du mois à deux chiffres (01 à 31) |
| hh           | Heure à deux chiffres (00 à 23) |
| mm           | Minute à deux chiffres (00 à 59) |
| ss           | Seconde à deux chiffres (00 à 59) |

**Exemple**

Le tableau suivant répertorie différents exemples permettant de définir différentes périodes à l'aide des paramètres *from* et *until* :

<table>
  <caption>Tableau 1. Différents exemples permettant de définir différentes périodes à l'aide des paramètres *from* et *until*</caption>
  <tr>
    <th>Exemple</th>
	<th>Description</th>
  </tr>
  <tr>
    <td>&from=monday</td>
	<td>Période de temps qui inclut des données comprises entre le dernier lundi jusqu'à maintenant.</td>
  </tr>
  <tr>
    <td>&from=20171101&until=20171130</td>
	<td>Période de temps définie sur un mois, en l'occurrence, sur novembre. </td>
  </tr>
  <tr>
    <td>&from=02:00_20170701&until=14:00_20170701</td>
	<td>Permet d'afficher des données sur un cycle de 24 heures, par exemple, entre 02h00 et 14h00, le 1er juillet 2017.</td>
  </tr>
  <tr>
    <td>&from=-8d&until=-7d</td>
	<td>Permet d'afficher les données correspondant au même jour de la semaine, en l'occurrence, la semaine dernière.</td>
  </tr>
  
</table>


