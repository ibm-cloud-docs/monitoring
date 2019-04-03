---

copyright:
  years: 2017, 2019

lastupdated: "2019-03-22"

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


# Tutoriel d'initiation
{: #getting-started}

Utilisez ce tutoriel pour apprendre à commencer à utiliser le service {{site.data.keyword.monitoringlong}} dans {{site.data.keyword.cloud_notm}}.
{:shortdesc}

Par défaut, {{site.data.keyword.cloud_notm}} offre des fonctions de surveillance intégrées pour certains services. Vous pouvez utiliser le service {{site.data.keyword.monitoringlong_notm}} afin de développer vos fonctions de collecte et de conservation lorsque vous gérez des métriques et pour pouvoir définir des règles et des alertes qui vous informeront des conditions nécessitant votre attention. Le service {{site.data.keyword.monitoringshort}} offre des fonctions qui analysent les performances et la consommation en ressources de vos applications et qui vous aident à identifier les tendances et à détecter et diagnostiquer les problèmes rapidement, tout en vous procurant une rentabilisation immédiate et un faible coût total de possession. Vous pouvez surveiller votre environnement via Grafana. 

## Avant de commencer
{: #gs_prereqs}

Vous devez avoir un ID utilisateur qui est membre ou propriétaire d'un compte {{site.data.keyword.cloud_notm}}. Pour obtenir un ID utilisateur {{site.data.keyword.cloud_notm}}, accédez au site d'[inscription ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/login){:new_window}

## Etape 1 : Sélection d'une ressource de cloud à surveiller
{: #gs_step1}

Dans {{site.data.keyword.cloud_notm}}, les applications CF, les conteneurs qui s'exécutent sur {{site.data.keyword.containershort}} et certains services collectent automatiquement des données de série de métriques et les transfèrent vers le service {{site.data.keyword.monitoringshort}}.

Le tableau ci-après répertorie différentes ressources de cloud. Suivez le tutoriel relatif à une ressource afin de commencer à utiliser le service {{site.data.keyword.monitoringshort}} :

<table>
  <caption>Tutoriels permettant de commencer à utiliser le service {{site.data.keyword.monitoringshort}} </caption>
  <tr>
    <th>Ressource</th>
    <th>Tutoriel</th>
    <th>Environnement de cloud</th>
    <th>Scénario</th>
  </tr>
  <tr>
    <td>Conteneurs qui s'exécutent sur {{site.data.keyword.containershort}}</td>
    <td>[Analyse de métriques dans Grafana pour une application qui est déployée dans un cluster Kubernetes](/docs/services/cloud-monitoring/tutorials?topic=cloud-monitoring-container_service_metrics#container_service_metrics)</td>
    <td>Public </br>Dédié</td>
    <td>![Présentation générale des composants pour les conteneurs déployés dans un cluster Kubernetes](containers/images/containers_kube_metrics_dedicated.png "Présentation générale des composants pour les conteneurs déployés dans un cluster Kubernetes")</td>
  </tr>
  <tr>
    <td>Applications CF</td>
    <td>[Analyse de métriques dans Grafana pour une application CF](/docs/services/cloud-monitoring/tutorials?topic=cloud-monitoring-cfapps_metrics#cfapps_metrics)</td>
    <td>Public</td>
    <td>![High level view of monitoring of CF apps in the {{site.data.keyword.cloud_notm}}](cf/images/cfapp_metrics_ov.png "Présentation générale de la surveillance des applications CF dans {{site.data.keyword.cloud_notm}}")</td>
  </tr>
</table>



## Etape 2 : Définition de droits pour un utilisateur afin de lui permettre d'afficher des métriques
{: #gs_step2}

Pour contrôler les actions {{site.data.keyword.monitoringshort}} qu'un utilisateur est autorisé à effectuer, vous pouvez affecter des rôles et des règles à cet utilisateur. 

Deux types de droit de sécurité dans {{site.data.keyword.cloud_notm}} contrôlent les actions que les utilisateurs peuvent effectuer lorsqu'ils utilisent le service {{site.data.keyword.monitoringshort}} :

* Rôles Cloud Foundry (CF) : vous accordez à un utilisateur un rôle CF pour définir les droits lui permettant d'afficher des métriques dans un espace.
* Rôles IAM : vous accordez à un utilisateur une règle IAM pour définir les droits lui permettant d'afficher des métriques dans le domaine de compte.


Pour autoriser un utilisateur à afficher des métriques dans un espace, procédez comme suit :

1. [Connectez-vous à la console {{site.data.keyword.cloud_notm}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://cloud.ibm.com/login){:new_window}
	
	Après que vous vous êtes connecté avec votre ID utilisateur et votre mot de passe, l'interface utilisateur {{site.data.keyword.cloud_notm}} s'ouvre.

2. Dans la barre de menus, cliquez sur **Gérer > Compte > Utilisateurs**. 

    La fenêtre *Utilisateurs* affiche une liste d'utilisateurs avec leur adresse électronique pour le compte actuellement sélectionné.
	
3. Si l'utilisateur est membre du compte, sélectionnez le nom de l'utilisateur dans la liste ou cliquez sur **Gérer un utilisateur** dans le menu *Actions*.

    Si l'utilisateur n'est pas membre du compte, voir [Invitation d'utilisateurs](/docs/iam?topic=iam-iamuserinv#iamuserinv).

4. Sélectionnez **Accès Cloud Foundry**, puis sélectionnez l'organisation.

    La liste des espaces disponibles dans cette organisation est affichée.

5. Choisissez l'espace dans lequel vous avez mis à disposition le service {{site.data.keyword.monitoringshort}}. Puis, dans l'action de menu, sélectionnez **Editer un rôle d'espace**.

6. Sélectionnez *Auditor*. 

    Vous pouvez sélectionner 1 ou plusieurs rôles d'espace. Tous les rôles suivants permettent à un utilisateur d'afficher des journaux : *Manager*, *Developer* et *Auditor*
	
7. Cliquez sur **Sauvegarder un rôle**.


Pour plus d'informations, voir [Octroi de droits](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-grant_permissions#grant_permissions).

Pour vérifier que l'utilisateur peut afficher des données de métrique, lancez Grafana dans la région du cloud où vous avez suivi l'un des tutoriels. Par exemple, pour la région Sud des Etats-Unis, ouvrez un navigateur Web et entrez l'URL suivante : [https://metrics.ng.bluemix.net/](https://metrics.ng.bluemix.net/)


Pour en savoir plus sur le démarrage de Grafana dans d'autres régions, voir [Accès à Grafana à partir d'un navigateur Web](/docs/services/cloud-monitoring/grafana?topic=cloud-monitoring-navigating_grafana#navigating_grafana).

**Remarque :** lorsque vous démarrez Grafana, si vous recevez le message *Jeton bearer non valide
*, vérifiez vos droits dans l'espace. Ce message est une indication que votre ID utilisateur ne dispose pas des droits requis pour afficher des métriques.
    

## Etapes suivantes 
{: #gs_next_steps}

Définissez une alerte pour une métrique. Pour plus d'informations, voir [Configuration d'alertes](/docs/services/cloud-monitoring?topic=cloud-monitoring-config_alerts_ov#config_alerts_ov).
