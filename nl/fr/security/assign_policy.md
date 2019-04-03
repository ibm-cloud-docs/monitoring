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


# Accord de droits à un utilisateur
{: #grant_permissions}

Dans {{site.data.keyword.Bluemix}}, vous pouvez affecter un ou plusieurs rôles à des utilisateurs. Ces rôles définissent quelles tâches sont activées pour que cet utilisateur utilise le service {{site.data.keyword.monitoringshort}}. 
{:shortdesc}

Pour autoriser un utilisateur à gérer des métriques, vous devez ajouter une règle pour cet utilisateur qui décrit les actions qu'il peut effectuer avec le service {{site.data.keyword.monitoringshort}} dans le compte. Seuls les propriétaires de compte peuvent affecter des règles individuelles à des utilisateurs.


## Affectation d'une règle IAM à un utilisateur via l'interface utilisateur IBM Cloud 
{: #assign_policy_ui}

Pour autoriser un utilisateur à gérer le service {{site.data.keyword.monitoringshort}}, procédez comme suit :

1. Connectez vous à la console {{site.data.keyword.Bluemix_notm}}.

    Ouvrez un navigateur Web et démarrez le tableau de bord {{site.data.keyword.Bluemix_notm}} : [http://console.bluemix.net ![Icône de lien externe](../../../icons/launch-glyph.svg "Icône de lien externe")](http://bluemix.net){:new_window}
	
	Après que vous vous êtes connecté avec votre ID utilisateur et votre mot de passe, l'interface utilisateur {{site.data.keyword.Bluemix_notm}} s'ouvre.

2. Dans la barre de menus, cliquez sur **Gérer > Compte > Utilisateurs**. 

    La fenêtre *Utilisateurs* affiche une liste d'utilisateurs avec leur adresse électronique pour le compte actuellement sélectionné.
	
3. Si l'utilisateur est membre du compte, sélectionnez le nom de l'utilisateur dans la liste ou cliquez sur **Gérer un utilisateur** dans le menu *Actions*.

    Si l'utilisateur n'est pas membre du compte, voir [Invitation d'utilisateurs](/docs/iam?topic=iam-iamuserinv#iamuserinv).

4. Cliquez sur **Affecter une règle de service**.

5. Entrez les informations concernant la règle. Le tableau suivant répertorie les zones requises et facultatives permettant de définir une règle : 

    <table>
	  <caption>Liste des zones de configuration d'une règle IAM.</caption>
	  <tr>
	    <th>Zone</th>
		<th>Valeur</th>
		<th>Statut</th>
	  </tr>
	  <tr>
	    <td>Service</td>
		<td>{{site.data.keyword.monitoringlong}}</td>
		<td>Obligatoire</td>
	  </tr>
	  <tr>
	    <td>Rôles</td>
		<td>Sélectionnez un ou plusieurs rôles IAM. <br>Les rôles valides sont : *administrateur*, *opérateur*, *éditeur* et *afficheur*. <br>Pour plus d'informations sur les actions autorisées pour chaque rôle, voir [Rôle IAM](/docs/services/cloud-monitoring?topic=cloud-monitoring-security_ov#iam_roles).</td>
		<td>Obligatoire</td>
	  </tr>
	  <tr>
	    <td>Régions</td>
		<td>Vous pouvez spécifier les régions auxquelles l'utilisateur aura accès pour utiliser des métriques. Sélectionnez **Spécifier un contexte de service facultatif**. Ensuite, ajoutez une ou plusieurs régions individuellement ou sélectionnez **Toutes les régions en cours** pour accorder l'accès à toutes les régions.</td>
		<td>Facultatif</td>
	  </tr>
	</table>
	
6. Cliquez sur **Affecter une règle**.
	
La règle que vous configurez est applicable aux régions sélectionnées. 

## Affectation d'une règle IAM à un utilisateur via la ligne de commande
{: #assign_policy_commandline}

Pour autoriser un utilisateur à afficher des métriques via la ligne de commande, procédez comme suit :

1. (Prérequis) Installez l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}.

   Pour plus d'informations, voir [Installation de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}.](/docs/cli?topic=cloud-cli-ibmcloud-cli#overview)
   
   Si l'interface de ligne de commande est installée, passez à l'étape suivante.
	
2. Connectez-vous à une région, une organisation et un espace dans {{site.data.keyword.Bluemix_notm}}. 

    Pour plus d'informations, voir [Comment se connecter à {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login).
	
3. Obtenez l'ID de compte. 

    Pour obtenir l'ID de compte, exécutez la commande suivante :

    ```
	ibmcloud iam accounts
	```
    {: codeblock}	

	La liste des comptes et de leur identificateur global unique s'affiche.
	
	Exportez l'ID du compte dans lequel vous prévoyez d'accorder des droits à un utilisateur. Configurez une variable d'environnement telle que `$acct_id`, par exemple :
	
	```
	export acct_id="1234567891234567812341234123412"
	```
	{: screen}

4. Obtenez l'ID {{site.data.keyword.IBM_notm}} de l'utilisateur auquel vous voulez accorder des droits.

    1. Affichez les utilisateurs associés au compte. Exécutez la commande suivante :
	
	    ```
		ibmcloud iam account-users
		```
		{: codeblock}
		
	2. Obtenez l'identificateur global unique de l'utilisateur. **Remarque : cette étape doit être effectuée par l'utilisateur auquel vous prévoyez d'accorder des droits.**
	
	    Demandez, par exemple, à l'utilisateur d'exécuter les commandes suivantes pour obtenir son ID utilisateur :
		
		Obtenez le jeton IAM. Pour plus d'informations, voir [Obtention du jeton IAM à l'aide de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_iam#iam_token_cli).

        Prenez les données situées entre les deux premiers points dans le jeton IAM. Exportez les données vers une variable d'environnement telle que `$user_data`. 
		
		```
	    export user_data="xxxxxxxxxxxxxxxxxxxxxxxxxxx"
	    ```
	    {: screen}
		
		Exécutez, par exemple, la commande suivante pour obtenir l'ID utilisateur. Cette commande utilise jq dans cet exemple pour décoder les informations que contient le texte JSON formaté :
		
		```
		echo $user_data | base64 -d | jq
		```
		{: codeblock}
		
		La sortie de cette commande est la suivante :
		
		```
		$ echo $user_data | base64 -d | jq
        {
        "iam_id": "IBMid-xxxxxxxxxx",
        "id": "IBMid-xxxxxxxxxx",
        "realmid": "IBMid",
        ......
		}
        ```
	    {: screen}
		
		Envoyez l'ID utilisateur, autrement dit la valeur de la zone *id* au propriétaire de compte. 
		
	3. Exportez l'ID utilisateur vers une variable d'environnement telle que `$user_ibm_id`.
	
		```
		export user_ibm_id="IBMid-xxxxxxxxxx"
		```
		{: codeblock}

3. Invitez l'utilisateur au compte s'il n'en est pas déjà membre. Pour plus d'informations, voir [Invitation d'utilisateurs](/docs/iam?topic=iam-iamuserinv#iamuserinv).

    Par exemple, exécutez la commande suivante pour inviter l'utilisateur xxx@yyy.com au compte zzz@ggg.com:
	
	```
	ibmcloud iam account-user-invite xxx@yyy.com zzz@ggg.com OrgAuditor dev SpaceDeveloper
	```
	{: codeblock}
		
4. Créez un nom de fichier de règle. 

    Par exemple, utilisez le modèle suivant pour accorder des droits d'affichage dans la région Sud des Etats-Unis :
	
	```
	{
		"roles" : [
			{
				"id": "crn:v1:bluemix:public:iam::::role:Editor" 
			}
		],
		"resources": [
			{
				"serviceName": "ibmcloud-monitoring",
				"region": "us-south"
			}
		]
	}
	```
	{: codeblock}
	
	Nommez le fichier de règle : `policy.json`
	
5. Obtenez le jeton IAM pour votre ID utilisateur.

    Pour plus d'informations, voir [Obtention du jeton IAM à l'aide de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_iam#iam_token_cli).

    Exportez le jeton IAM vers une variable d'environnement telle que `$iam_token`, par exemple :
	
	```
	export iam_token="xxxxxxxxxxxxxxxxxxxxx"
	```
	{: screen}
	
6. Accordez à l'utilisateur des droits lui permettant d'utiliser le service {{site.data.keyword.monitoringshort}}. 

   Exécutez la commande cURL suivante pour accorder des droits dans la région Sud des Etats-Unis :
	
    ```
	curl -X POST --header "Authorization: $iam_token" --header "Content-Type: application/json" https://iampap.ng.bluemix.net/acms/v1/scopes/a%2F$acct_id/users/$user_ibm_id/policies -d @policy.json
	```
	{: codeblock}
	
	Exécutez la commande cURL suivante pour accorder des droits dans la région Royaume-Uni :
	
    ```
	curl -X POST --header "Authorization: $iam_token" --header "Content-Type: application/json" https://iampap.eu-gb.bluemix.net/acms/v1/scopes/a%2F$acct_id/users/$user_ibm_id/policies -d @policy.json
	```
	{: codeblock}

	





## Octroi d'un rôle CF à un utilisateur à l'aide de l'interface utilisateur IBM Cloud 
{: #grant_permissions_ui_space}


Pour qu'un utilisateur puisse utiliser des métriques dans le domaine de l'espace ou le domaine de l'organisation, un rôle Cloud Foundry (CF) doit lui être affecté dans {{site.data.keyword.Bluemix_notm}}. Un rôle CF décrit les actions qu'un utilisateur peut effectuer avec le service {{site.data.keyword.monitoringshort}} dans un espace ou une organisation. 

Pour autoriser un utilisateur à gérer le service {{site.data.keyword.monitoringshort}}, procédez comme suit :

1. Connectez vous à la console {{site.data.keyword.Bluemix_notm}}.

    Ouvrez un navigateur Web et lancez le tableau de bord {{site.data.keyword.Bluemix_notm}} : [http://bluemix.net ![Icône de lien externe](../../../icons/launch-glyph.svg "Icône de lien externe")](http://bluemix.net){:new_window}
	
	Après que vous vous êtes connecté avec votre ID utilisateur et votre mot de passe, l'interface utilisateur {{site.data.keyword.Bluemix_notm}} s'ouvre.

2. Dans la barre de menus, cliquez sur **Gérer > Compte > Utilisateurs**. 

    La fenêtre *Utilisateurs* affiche une liste d'utilisateurs avec leur adresse électronique pour le compte actuellement sélectionné.
	
3. Si l'utilisateur est membre du compte, sélectionnez le nom de l'utilisateur dans la liste ou cliquez sur **Gérer un utilisateur** dans le menu *Actions*.

    Si l'utilisateur n'est pas membre du compte, voir [Invitation d'utilisateurs](/docs/iam?topic=iam-iamuserinv#iamuserinv).

4. Cliquez sur **Affecter une organisation**.

5. Entrez les informations concernant la règle. Le tableau suivant répertorie les zones requises et facultatives permettant de définir une règle : 

    <table>
	  <caption>Liste des zones de configuration d'une règle CF.</caption>
	  <tr>
	    <th>Zone</th>
		<th>Valeur</th>
	  </tr>
	  <tr>
	    <td>Organisation</td>
		<td>Sélectionnez une organisation dans la liste.</td>
	  </tr>
	  <tr>
	    <td>Rôles d'organisation</td>
		<td>Sélectionnez **Aucun rôle d'organisation**. Toutefois, si l'utilisateur détient un rôle organisationnel, sélectionnez un rôle d'organisation dans la liste. <br>Les valeurs valides sont : **Responsable de la facturation**, **Auditeur**, **Responsable**</td>
	  </tr>
	  <tr>
	    <td>Région</td>
		<td>Sélectionnez une région dans la liste. <br>Les valeurs valides sont : **Toutes les régions en cours**, **Sud des Etats-Unis**, **Royaume-Uni**</td>
	  </tr>
	  <tr>
	    <td>Espace</td>
		<td>Par défaut, **Tous les espaces en cours** est prédéfini lorsque la zone *Région* a pour valeur **Toutes les régions en cours**. Pour accorder un droit à un espace individuel, sélectionnez une région spécifique, puis sélectionnez un espace dans la liste.</td>
	  </tr>
	  <tr>
	    <td>Rôles d'espace</td>
		<td>Sélectionnez un rôle d'espace dans la liste. <br>Les valeurs valides sont : **Responsable**, **Auditeur**, **Développeur** et **Aucun rôle d'espace**. Pour plus d'informations, voir [Rôles Cloud Foundry](/docs/services/cloud-monitoring?topic=cloud-monitoring-security_ov#bmx_roles).</td>
	  </tr>
	</table>
	
6. Cliquez sur **Affecter une règle**.
	
La règle que vous configurez est applicable aux régions sélectionnées. 


