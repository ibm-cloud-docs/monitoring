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


# Sécurité
{: #security_ov}

Pour contrôler les actions du service {{site.data.keyword.monitoringshort}} qu'un utilisateur est autorisé à effectuer, vous pouvez affecter un ou plusieurs rôles à l'utilisateur. Pour authentifier un utilisateur pour qu'il utilise des métriques et des alertes, vous pouvez utiliser un jeton UAA, un jeton IAM ou une clé d'API. 
{:shortdesc}





## Modèles d'authentification
{: #auth}

Une jeton d'authentification ou une clé d'API est nécessaire pour utiliser des métriques stockées dans le service {{site.data.keyword.monitoringshort}} pour un espace. 

Pour obtenir un jeton de sécurité, voir :

* [Obtention d'un jeton UAA](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_uaa#auth_uaa)
* [Obtention d'un jeton IAM](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_iam#auth_iam)

Pour obtenir une clé d'API, voir [Génération d'une clé d'API](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_api_key#auth_api_key). Si la clé d'API est compromise, vous pouvez la révoquer en la supprimant. Ensuite, vous pouvez en créer une nouvelle. Pour plus d'informations, voir [Révocation d'une clé d'API à l'aide de l'interface utilisateur {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_api_key#revoke_ui). 

Un jeton UAA et un jeton IAM arrivent à expiration au bout d'un certain temps. La clé d'API n'arrive jamais à expiration. 

Le tableau suivant répertorie les modèles de sécurité pris en charge pour chaque type de domaine :

<table>
  <caption>Tableau 1. Modèles de sécurité pris en charge pour chaque domaine</caption>
  <tr>
    <th></th>
	<th align="right">Compte</th>
    <th align="right">Organisation</th>
    <th align="right">Espace</th>	
  </tr>
  <tr>
    <th align="left">UAA</th>
	<td align="center">Non</td>
	<td align="center">Oui</td>
	<td align="center">Oui</td>
  </tr>
  <tr>
    <th align="left">IAM</th>
	<td align="center">Oui</td>
	<td align="center">Oui</td>
	<td align="center">Oui</td>
  </tr>
</table>

Le service {{site.data.keyword.monitoringshort}} utilise la fonction de contrôle d'accès IAM pour définir les actions et les opérations qu'un utilisateur ou un service peut effectuer pour le domaine. Par exemple, vous pouvez définir une règle IAM qui autorise un utilisateur à envoyer et à créer des tableaux de bord dans un domaine, mais qui ne lui permet pas d'extraire les métriques depuis le domaine.



## Rôles Cloud Foundry
{: #bmx_roles}

Le tableau suivant répertorie les privilèges de chaque rôle Cloud Foundry pouvant être utilisé avec le service {{site.data.keyword.monitoringshort}} :

<table>
  <caption>Tableau 2. Rôle et privilèges Cloud Foundry permettant d'utiliser le service {{site.data.keyword.monitoringshort}}</caption>
  <tr>
    <th>Rôle</th>
	<th>Domaine</th>
	<th>Privilèges d'accès</th>
  </tr>
  <tr>
    <td>Responsable</td>
	<td>Organisation <br>Espace</td>
	<td>Toutes les API RESTful</td>
  </tr>
  <tr>
    <td>Développeur</td>
	<td>Espace</td>
	<td>Toutes les API RESTful</td>
  </tr>
  <tr>
    <td>Auditeur</td>
	<td>Organisation <br>Espace</td>
	<td>Uniquement les API RESTful qui effectuent des opérations en lecture seule, comme interroger des métriques.</td>
  </tr>
</table>

Pour plus d'informations sur l'affectation de rôles utilisateur dans l'interface utilisateur, voir [Gestion de l'accès Cloud Foundry](/docs/iam?topic=iam-mngcf#mngcf).



## Rôles IAM
{: #iam_roles}

Le tableau suivant répertorie les actions du service {{site.data.keyword.monitoringshort}} lorsque vous utilisez des métriques et les rôles IAM qui accordent à un utilisateur des droits pour exécuter ces tâches :

<table>
  <caption>Tableau 3. Utilisation des métriques. </caption>
  <tr>
	<th>Action</th>
	<th>Rôle IAM</th>
  </tr>
  <tr>
    <td>Envoyer des métriques au domaine</td>
	<td>Administrateur, Editeur, Opérateur</td>
  </tr>
  <tr>
    <td>Extraire/interroger des métriques</td>
	<td>Administrateur, Editeur, Afficheur</td>
  </tr>
  <tr>
    <td>Rechercher des métriques dans le domaine</td>
	<td>Administrateur, Editeur</td>
  </tr>
</table>

Le tableau suivant répertorie les actions du service {{site.data.keyword.monitoringshort}} lorsque vous utilisez des alertes et les rôles IAM qui accordent à un utilisateur des droits pour exécuter ces tâches :

<table>
  <caption>Tableau 4. Utilisation des alertes. </caption>
  <tr>
	<th>Action</th>
	<th>Rôle IAM</th>
  </tr>
  <tr>
    <td>Créer, éditer et supprimer des règles d'alerte</td>
	<td>Administrateur, Editeur</td>
  </tr>
  <tr>
    <td>Afficher des alertes</td>
	<td>Administrateur, Editeur, Afficheur</td>
  </tr>
  <tr>
    <td>Créer, éditer et supprimer des notifications d'alerte</td>
	<td>Administrateur, Editeur</td>
  </tr>
  <tr>
    <td>Afficher des notifications</td>
	<td>Administrateur, Editeur, Afficheur</td>
  </tr>
  <tr>
    <td>Afficher des enregistrements d'historique d'alerte déclenchée</td>
	<td>Administrateur, Editeur, Afficheur</td>
  </tr>
</table>

Pour plus d'informations sur l'affectation de rôles utilisateur dans l'interface utilisateur, voir [Gestion de l'accès IAM](/docs/iam?topic=iam-iammanidaccser#iammanidaccser).

