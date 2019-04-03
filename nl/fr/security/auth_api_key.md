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


# Utilisation des clés d'API
{: #auth_api_key}

Vous pouvez obtenir une clé d'API à l'aide de l'interface de ligne de commande {{site.data.keyword.Bluemix}} ou de l'interface utilisateur {{site.data.keyword.Bluemix_notm}}. La clé d'API n'arrive jamais à expiration. Si une API est compromise, vous pouvez la révoquer et en générer une nouvelle.
{:shortdesc}

## Génération d'une clé d'API IAM à l'aide de l'interface de ligne de commande IBM Cloud
{: #iam_apikey_cli}

Pour générer une clé d'API à l'aide de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}, procédez comme suit :

1. (Prérequis) Installez l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}.

   Pour plus d'informations, voir [Installation de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}.](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#cli_qa)
   
   Si l'interface de ligne de commande est installée, passez à l'étape suivante.
	
2. Connectez-vous à une région, une organisation et un espace dans {{site.data.keyword.Bluemix_notm}}. 

    Pour plus d'informations, voir [Comment se connecter à {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login).
 
3. Exécutez la commande `ibmcloud iam api-key-create` pour créer une clé d'API.

    ```
    ibmcloud iam api-key-create NAME [-d DESCRIPTION][-f, --file FILE]
	```
	{: codeblock} 
	
	où
	
	* NAME est le nom de la clé d'API à créer.
	* DESCRIPTION est un texte décrivant la clé d'API.
	* FILE est le nom du fichier dans lequel la clé est sauvegardée.
	
    Par exemple, pour créer la clé d'API *MyKey*, exécutez la commande suivante :
	
	```
	ibmcloud iam api-key-create MyKey -d "This is my API key for service X" 
	```
	{: screen}
	
	
	
	
## Génération d'une clé d'API IAM à l'aide de l'interface utilisateur IBM Cloud
{: #iam_apikey_ui}

Pour générer une clé d'API via l'interface utilisateur {{site.data.keyword.Bluemix_notm}}, procédez comme suit :

1. Connectez vous à la console {{site.data.keyword.Bluemix_notm}}.

    Ouvrez un navigateur Web et démarrez le tableau de bord {{site.data.keyword.Bluemix_notm}} : [http://console.bluemix.net ![Icône de lien externe](../../../icons/launch-glyph.svg "Icône de lien externe")](http://bluemix.net){:new_window}
	
	Après que vous vous êtes connecté avec votre ID utilisateur et votre mot de passe, l'interface utilisateur {{site.data.keyword.Bluemix_notm}} s'ouvre.

2. Dans la barre de menus de la console, cliquez sur **Gérer > Sécurité > Clés d'API IBM Cloud**.

3. Cliquez sur **Créer une clé d'API**.

4. Entrez un nom et une description pour votre clé d'API. Cliquez ensuite sur **Créer une clé d'API**.

5. Sauvegardez la clé d'API. Cliquez sur **Télécharger une clé d'API**.

    Cliquez sur **Afficher** pour afficher la clé d'API.  

**Remarque :** la clé d'API ne peut être affichée ou téléchargée qu'au moment de sa création. Si elle est perdue, vous devez en créer une autre.  


	
## Révocation d'une clé d'API à l'aide de l'interface utilisateur IBM Cloud
{: #revoke_ui}
	
Pour révoquer une clé d'API IAM à l'aide de l'interface utilisateur {{site.data.keyword.Bluemix_notm}}, procédez comme suit :

1. Connectez vous à la console {{site.data.keyword.Bluemix_notm}}.

    Ouvrez un navigateur Web et démarrez le tableau de bord {{site.data.keyword.Bluemix_notm}} : [http://console.bluemix.net ![Icône de lien externe](../../../icons/launch-glyph.svg "Icône de lien externe")](http://bluemix.net){:new_window}
	
	Après que vous vous êtes connecté avec votre ID utilisateur et votre mot de passe, l'interface utilisateur {{site.data.keyword.Bluemix_notm}} s'ouvre.

2. Dans la barre de menus de la console, cliquez sur **Gérer > Sécurité > Clés d'API IBM Cloud**.

3. Cliquez sur **Actions**, puis sur **Supprimer la clé**.





	

	
	
	
	
	
	
