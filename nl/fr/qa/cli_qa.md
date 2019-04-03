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



# Foire aux questions liées à l'utilisation de l'interface de ligne de commande IBM Cloud
{: #cli_qa}

Vous trouverez ci-après les réponses aux questions fréquentes concernant l'utilisation de l'interface de ligne de commande {{site.data.keyword.Bluemix}} avec le service {{site.data.keyword.monitoringshort}}. 
{:shortdesc}

* [Comment se connecter à {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login)
* [Comment installer l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#install_bmx_cli)
* [Comment obtenir l'identificateur global unique d'un compte](/docs/services/cloud-monitoring/qa/cli_qa.html#account_guid)
* [Comment obtenir l'identificateur global unique d'une organisation](/docs/services/cloud-monitoring/qa/cli_qa.html#org_guid)
* [Comment obtenir l'identificateur global unique d'un espace](/docs/services/cloud-monitoring/qa/cli_qa.html#space_guid)

## Comment se connecter à IBM Cloud ?
{: #login}

Exécutez la commande suivante pour vous connecter à une région, une organisation et un espace dans {{site.data.keyword.Bluemix_notm}} :

```
ibmcloud login -a Endpoint
```
{: codeblock}
	
Où *Endpoint* est l'URL permettant de se connecter à {{site.data.keyword.Bluemix_notm}}. Cette adresse URL varie selon les régions.
	
<table>
    <caption>Liste des noeuds finaux permettant d'accéder à {{site.data.keyword.Bluemix_notm}}</caption>
	<tr>
	  <th>Région</th>
	  <th>URL</th>
	</tr>
	<tr>
	  <td>Allemagne</td>
	  <td>api.eu-de.bluemix.net</td>
	</tr>
	<tr>
	  <td>Sydney</td>
	  <td>api.au-syd.bluemix.net</td>
	</tr>
	<tr>
	  <td>Royaume-Uni</td>
	  <td>api.eu-gb.bluemix.net</td>
	</tr>
	<tr>
	  <td>Sud des Etats-Unis</td>
	  <td>api.ng.bluemix.net</td>
	</tr>
</table>

Par exemple, pour vous connecter à la région Sud des Etats-Unis, exécutez la commande suivante :
	
```
ibmcloud login -a https://api.ng.bluemix.net
```
{: codeblock}

Suivez les instructions. 

Définissez ensuite l'organisation et l'espace. Exécutez la commande suivante :

```
ibmcloud target -o OrgName -s SpaceName
```
{: codeblock}

où

* OrgName est le nom de l'organisation.
* SpaceName est le nom de l'espace.

	
## Comment installer l'interface de ligne de commande IBM Cloud ?
{: #install_bmx_cli}

Voir [Téléchargement et installation de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}](/docs/cli/index.html#overview).

## Comment obtenir l'identificateur global unique d'un compte ?
{: #account_guid}
	
Procédez comme suit pour obtenir l'identificateur global unique d'un compte :
	
1. Connectez-vous à une région, une organisation et un espace dans {{site.data.keyword.Bluemix_notm}}. Exécutez la commande :

    ```
	ibmcloud login -a Endpoint
	```
	{: codeblock}
	
	Où *Endpoint* est l'URL permettant de se connecter à {{site.data.keyword.Bluemix_notm}}. Cette adresse URL varie selon les régions.
	
	<table>
	    <caption>Liste des noeuds finaux permettant d'accéder à {{site.data.keyword.Bluemix_notm}}</caption>
		<tr>
		  <th>Région</th>
		  <th>URL</th>
		</tr>
		<tr>
		  <td>Sud des Etats-Unis</td>
		  <td>api.ng.bluemix.net</td>
		</tr>
		<tr>
		  <td>Royaume-Uni</td>
		  <td>api.eu-gb.bluemix.net</td>
		</tr>
	</table>

    Par exemple, pour vous connecter à la région Sud des Etats-Unis, exécutez la commande suivante :
	
	```
    ibmcloud login -a https://api.ng.bluemix.net
    ```
    {: codeblock}

    Suivez les instructions. Entrez vos données d'identification {{site.data.keyword.Bluemix_notm}} et sélectionnez une organisation et un espace.
	
	Pour les **ID utilisateur fédéré**, exécutez la commande suivante et appliquez les instructions :
	
	```
    ibmcloud login -a https://api.ng.bluemix.net --sso
    ```
    {: codeblock}
	
2. Exécutez la commande `ibmcloud iam accounts` pour obtenir l'identificateur global unique d'un compte.

    ```
	ibmcloud iam accounts
	```
	{: codeblock} 
	
	Par exemple, afin d'extraire tous les comptes et les identificateurs globaux uniques correspondants pour l'utilisateur xxx@yyy.com, exécutez la commande :
	
	```
	ibmcloud iam accounts
	Retrieving all accounts of xxx@yyy.com...
    OK
    Account GUID                       Name                               Type    State    Owner User ID   
    12345123451234512345123451234512   A Account                          TRIAL   ACTIVE   xxx@yyy.com   
    23456234562345622456234561234561   B Account                          TRIAL   ACTIVE   zzz@yyy.com   
	```
	{: screen}

	
## Comment obtenir l'identificateur global unique d'une organisation ?
{: #org_guid}

Procédez comme suit pour obtenir l'identificateur global unique d'une organisation :
	
1. Connectez-vous à une région, une organisation et un espace dans {{site.data.keyword.Bluemix_notm}}. Exécutez la commande :

    ```
	ibmcloud login -a Endpoint
	```
	{: codeblock}
	
	Où *Endpoint* est l'URL permettant de se connecter à {{site.data.keyword.Bluemix_notm}}. Cette adresse URL varie selon les régions.
	
	<table>
	    <caption>Liste des noeuds finaux permettant d'accéder à {{site.data.keyword.Bluemix_notm}}</caption>
		<tr>
		  <th>Région</th>
		  <th>URL</th>
		</tr>
		<tr>
		  <td>Sud des Etats-Unis</td>
		  <td>api.ng.bluemix.net</td>
		</tr>
		<tr>
		  <td>Royaume-Uni</td>
		  <td>api.eu-gb.bluemix.net</td>
		</tr>
	</table>

    Par exemple, pour vous connecter à la région Sud des Etats-Unis, exécutez la commande suivante :
	
	```
    ibmcloud login -a https://api.ng.bluemix.net
    ```
    {: codeblock}

    Suivez les instructions. Entrez vos données d'identification {{site.data.keyword.Bluemix_notm}} et sélectionnez une organisation et un espace.
	
	Pour les ID utilisateur fédéré, exécutez la commande suivante et suivez les instructions :
	
	```
    ibmcloud login -a https://api.ng.bluemix.net --sso
    ```
    {: codeblock}

2. Exécutez la commande `ibmcloud iam org` pour obtenir l'identificateur global unique de l'organisation. 

    ```
    ibmcloud iam org NAME --guid
    ```
    {: codeblock}
	
    où NAME est le nom de l'organisation {{site.data.keyword.Bluemix_notm}}.        
		
## Comment obtenir l'identificateur global unique d'un espace
{: #space_guid}
	
Procédez comme suit pour obtenir l'identificateur global unique d'un espace :
	
1. Connectez-vous à une région, une organisation et un espace dans {{site.data.keyword.Bluemix_notm}}. Exécutez la commande :

    ```
	ibmcloud login -a Endpoint
	```
	{: codeblock}
	
	Où *Endpoint* est l'URL permettant de se connecter à {{site.data.keyword.Bluemix_notm}}. Cette adresse URL varie selon les régions.
	
	<table>
	    <caption>Liste des noeuds finaux permettant d'accéder à {{site.data.keyword.Bluemix_notm}}</caption>
		<tr>
		  <th>Région</th>
		  <th>URL</th>
		</tr>
		<tr>
		  <td>Sud des Etats-Unis</td>
		  <td>api.ng.bluemix.net</td>
		</tr>
		<tr>
		  <td>Royaume-Uni</td>
		  <td>api.eu-gb.bluemix.net</td>
		</tr>
	</table>

    Par exemple, pour vous connecter à la région Sud des Etats-Unis, exécutez la commande suivante :
	
	```
    ibmcloud login -a https://api.ng.bluemix.net
    ```
    {: codeblock}

    Suivez les instructions. Entrez vos données d'identification {{site.data.keyword.Bluemix_notm}} et sélectionnez une organisation et un espace.
	
	Pour les ID utilisateur fédéré, exécutez la commande suivante et suivez les instructions :
	
	```
    ibmcloud login -a https://api.ng.bluemix.net --sso
    ```
    {: codeblock}
	
2. Exécutez la commande `ibmcloud iam space` pour obtenir l'identificateur global unique de l'espace. 

    ```
    ibmcloud iam space NAME --guid
    ```
    {: codeblock}
	
    où NAME est le nom d'un espace {{site.data.keyword.Bluemix_notm}}. 
	
    Par exemple, pour obtenir l'identificateur global unique de l'espace *dev*, exécutez la commande suivante :
	
    ```
    ibmcloud iam space dev --guid
    e03afff1-3456-4af6-1234-59treg1b0abc
    ```
    {: screen}




		
		
