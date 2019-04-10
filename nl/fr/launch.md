---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, launch web UI

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

# Accès à l'interface utilisateur Web
{: #launch}

Après la mise à disposition d'une instance du service {{site.data.keyword.mon_full_notm}} dans {{site.data.keyword.Bluemix}} et la configuration d'un agent Sysdig pour une source de métriques, vous pouvez afficher, surveiller et gérer des métriques via l'interface utilisateur Web {{site.data.keyword.mon_full_notm}}.
{:shortdesc}


## Octroi de règles IAM à un utilisateur pour afficher des données 
{: #launch_step1}

**Remarque :** Vous devez être un administrateur du service {{site.data.keyword.mon_full_notm}}, un administrateur de l'instance {{site.data.keyword.mon_full_notm}}, ou disposer de droits IAM sur le compte pour accorder des règles à d'autres utilisateurs.

Le tableau suivant répertorie les règles minimales dont doit disposer un utilisateur pour être en mesure de lancer l'interface utilisateur Web {{site.data.keyword.mon_full_notm}} et d'afficher des données :

| Service                        | Rôle                      | Droits accordés     |
|--------------------------------|---------------------------|------------------------|
| `{{site.data.keyword.mon_full_notm}}` | Rôle de plateforme : Afficheur     | Permet à l'utilisateur d'afficher la liste des instances de service dans le tableau de bord de surveillance de l'observabilité. |
| `{{site.data.keyword.mon_full_notm}}` | Rôle de service : Auteur      | Permet à l'utilisateur de lancer l'interface utilisateur Web et d'afficher des métriques dans l'interface utilisateur Web.  |
{: caption="Tableau 1. Règles IAM" caption-side="top"} 

Pour plus d'informations sur la configuration de ces règles pour un utilisateur, voir [Octroi de droits à un utilisateur pour afficher des métriques dans Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-iam_work#user_sysdig).


## Lancement de l'interface utilisateur Web via l'interface utilisateur {{site.data.keyword.cloud_notm}}
{: #launch_step2}

Vous pouvez lancer l'interface utilisateur Web dans le cadre d'une instance {{site.data.keyword.mon_full_notm}}, à partir de l'interface utilisateur {{site.data.keyword.cloud_notm}}. 

Pour lancer l'interface utilisateur Web, procédez comme suit :

1. Connectez-vous à votre compte {{site.data.keyword.cloud_notm}}.

    Cliquez sur le tableau de bord [{{site.data.keyword.cloud_notm}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/login){:new_window} pour lancer le tableau de bord {{site.data.keyword.cloud_notm}}.

	Une fois que vous êtes connecté avec votre ID utilisateur et votre mot de passe, le tableau de bord {{site.data.keyword.cloud_notm}} s'ouvre.

2. Dans le menu de navigation, sélectionnez **Observabilité**. 

3. Sélectionnez **Surveillance**. 

    La liste des instances disponibles sur {{site.data.keyword.cloud_notm}} s'affiche.

4. Sélectionnez une instance. Cliquez ensuite sur **Afficher Sysdig**.

L'interface utilisateur Web s'ouvre.


