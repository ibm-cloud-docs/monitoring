---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, api token

subcollection: Sysdig

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


# Utilisation des jetons d'API
{: #api_token}

Utilisez le jeton d'API pour vous authentifier sur le service {{site.data.keyword.mon_full_notm}} lorsque vous utilisez des scripts Python ou l'API REST Sysdig pour automatiser des tâches de routine et surveiller des notifications. 
{:shortdesc}

Prenez en compte les informations suivantes pour chaque instance du service {{site.data.keyword.mon_full_notm}} :

* Il existe un jeton d'API par équipe.
* Si le jeton est compromis ou que les règles de sécurité de votre organisation nécessitent la réinitialisation du jeton après la survenue de certaines conditions, un utilisateur doté de droits d'administration peut réinitialiser le jeton d'API.


## Obtention du jeton d'API Sysdig
{: #api_token_get}


Pour obtenir le jeton, procédez comme suit :

1. A partir du bouton *Sélecteur* dans la barre de navigation, choisissez **Paramètres**.
2. A partir de la section *Sysdig Monitor API*, copiez le **jeton d'API de surveillance Sysdig**.

## Réinitialisation du jeton d'API Sysdig
{: #api_token_reset}

Pour obtenir le jeton, procédez comme suit :

1. A partir du bouton *Sélecteur* dans la barre de navigation, choisissez **Paramètres**.
2. Dans la section *Sysdig Monitor API*, cliquez sur **Reset Token** pour réinitialiser le jeton d'API.
