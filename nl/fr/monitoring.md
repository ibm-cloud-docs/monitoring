---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring

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

# Surveillance de votre environnement
{: #monitoring}

Vous pouvez surveiller votre infrastructure et les applications qui s'exécutent dessus avec le service {{site.data.keyword.mon_full_notm}}. Vous pouvez demander une capture pour analyser ce qui se passe dans un noeud au cours d'une période donnée.
{:shortdesc}

Après la mise à disposition d'une instance du service {{site.data.keyword.mon_full_notm}} dans {{site.data.keyword.Bluemix}} et la configuration d'agents Sysdig pour vos sources de métriques, vous pouvez afficher, surveiller et gérer des données via l'interface utilisateur Web du service.

Les données pour les métriques par défaut sont collectées automatiquement. Vous pouvez configurer des métriques personnalisées et leur ajouter des libellés pour décrire leurs caractéristiques. Les données pour ces métriques personnalisées sont également collectées automatiquement.

Vous pouvez analyser des données dans l'onglet *Explorer* et dans l'onglet *Tableau de bord* de l'interface utilisateur Web. Les vues de métrique et les tableaux de bord vous permettent de surveiller les données. 

* Utilisez une vue de métrique pour surveiller une métrique individuelle.
* Utilisez des tableaux de bord pour obtenir une vue spécialisée des données réseau, des données d'application, de la topologie, des services, des hôtes et des conteneurs en surveillant les données via des panneaux. Un panneau affiche une métrique ou un groupe de métriques dans un tableau de bord.

Pour chaque vue de métrique et tableau de bord, vous pouvez définir la portée des données, le mode d'agrégation des données, ainsi que les filtres temporels et de groupe à appliquer aux données. Pour plus d'informations, voir [Gestion des données](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-manage#manage).

L'onglet *Explorer* vous permet de surveiller des données à l'aide des métriques et tableaux de bord par défaut. Vous pouvez utiliser des libellés pour définir de nouveaux groupes d'infrastructure, que vous pouvez ensuite utiliser pour agréger différemment les données et pour surveiller votre environnement. Vous pouvez également utiliser des tableaux de bord personnalisés que vous définissez via l'onglet *Tableau de bord*.

L'onglet *Tableau de bord* vous permet de surveiller des données à l'aide de l'un des tableaux de bord par défaut ou en en créant de nouveaux.

Vous pouvez configurer un tableau de bord par défaut comme point d'entrée par défaut pour une équipe, en unifiant l'expérience d'une équipe et en permettant aux utilisateurs de concentrer immédiatement leur attention sur les informations les plus importantes pour eux. 
{: tip}

Vous pouvez utiliser des alertes pour avertir les utilisateurs de problèmes nécessitant leur attention via un ou plusieurs canaux de notification.
* La section *Alertes* dans l'interface utilisateur Web affiche la liste des alertes prédéfinies. A partir de cette vue, vous pouvez activer et désactiver les alertes prédéfinies, modifier des alertes existantes et créer de nouvelles alertes.
* La section *Paramètres* de l'interface utilisateur Web permet de configurer des canaux de notification.
 
Vous pouvez demander une capture sur un noeud pour analyser ce qui se passe dans ce noeud au cours d'une période donnée. Par exemple, vous pouvez l'utiliser pour analyser les goulots d'étranglement ou les interactions de composants.

## Métriques
{: #monitoring_metrics}

Une métrique est une mesure quantitative comportant un ou plusieurs libellés pour définir ses caractéristiques. Utilisez des métriques pour analyser statistiquement des données comportant des valeurs numériques. 

Une métrique est représentée par une série temporelle. Une série temporelle est un ensemble de points de données numériques sur une période de temps. 

Les métriques sont classées en deux groupes : 

* [Métriques par défaut](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-metrics#metrics_default) 
* [Métriques personnalisées](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-metrics#metrics_custom)

Les libellés sont classés en tant que libellés d'infrastructure et libellés de descripteur de métrique. Chaque métrique possède un ensemble de libellés prédéfinis. Pour les métriques personnalisées, vous pouvez configurer davantage de libellés. 

Vous pouvez utiliser des libellés pour identifier et différencier les caractéristique d'une métrique, par exemple,
* Vous pouvez regrouper des objets d'infrastructure en hiérarchies logiques. 
* Vous pouvez filtrer des données. 
* Vous pouvez fractionner des données agrégées en segments. 

Pour plus d'informations, voir [Libellés](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-metrics#metrics_labels).

## Panneaux
{: #monitoring_panels}

Un panneau affiche une métrique ou un groupe de métriques dans un tableau de bord. 

Vous pouvez utiliser l'un des types de panneaux suivants pour visualiser des métriques :

| Type | Description |
|------|-------------|
| Ligne | Utilisez ce panneau pour afficher les tendances au fil du temps pour une ou plusieurs métriques.  |
| Zone | Utilisez ce panneau pour afficher les tendances au fil du temps pour une ou plusieurs métriques.  |
| Liste supérieure | Utilisez ce panneau pour comparer une métrique sur un groupe d'entités. Le graphique à barres est trié par ordre décroissant.  |
| Histogramme | Utilisez ce panneau pour afficher la distribution des fréquences d'une métrique dans des compartiments.  |
| Topologie | Utilisez ce panneau pour visualiser l'infrastructure sous forme de mappe topologique, ainsi que les relations entre les entités de la mappe.  |
| Nombre | Utilisez ce panneau pour afficher un seul nombre qui représente la valeur d'une métrique agrégée au fil du temps pour une ou plusieurs entités.  |
| Tableau | Utilisez ce panneau pour afficher des données numériques pour votre infrastructure en fonction des métriques et segments.  |
| Texte | Utilisez ce panneau pour ajouter du texte. Utilisez Markdown pour ajouter votre texte.  |
{: caption="Tableau 3. Types de panneaux" caption-side="top"} 

Vous pouvez copier, modifier la portée, dupliquer, supprimer, exporter et explorer des panneaux.

Vous pouvez exporter des données à partir d'un panneau. Prenez en compte les informations suivantes lorsque vous exportez des données :

* Vous pouvez exporter des données vers un **fichier JSON** à partir d'un graphique à courbes.
* Vous pouvez exporter des données vers un **fichier CSV** à partir d'un tableau ou d'un graphique à courbes.


Le tableau suivant répertorie les tâches que vous pouvez exécuter avec des panneaux :

| Tâche | Description |
|------|-------------|
| [Copie d'un panneau](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_copy) | Copie un panneau dans un nouveau tableau de bord.  |
| [Modification de la portée](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_scope) | Modifie la portée d'un panneau. |
| [Duplication d'un panneau](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_duplicate) | Copie un panneau dans le même tableau de bord.  |
| [Suppression d'un panneau](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_delete) | Supprime un panneau du tableau de bord.  |
| [Exportation de données](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_export) | Exporte des données à partir d'un panneau dans un fichier CSV ou JSON.  |
| [Création d'une alerte](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_alert) | Définit une alerte sur une métrique. |
{: caption="Tableau 4. Tâches de panneau" caption-side="top"} 


## Tableaux de bord
{: #monitoring_dashboards}

Un **tableau de bord** affiche des groupes de métriques qui génèrent des rapports sur la santé, la performance et l'état de votre infrastructure, de vos applications et de vos services pour un hôte unique ou un groupe d'hôtes. Les tableaux de bord détaillent les données réseau, les données d'application, la topologie, les services, les hôtes et les conteneurs. Les tableaux de bord permettent de surveiller votre infrastructure, vos applications et vos services.


Dans la section **DASHBOARDS** de l'interface utilisateur Web, les tableaux de bord sont organisés en trois groupes principaux :

* *My Dashboards* : il s'agit des tableaux de bord qui sont créés par l'utilisateur actuellement connecté.
* *My Shared Dashboards* : il s'agit des tableaux de bord qui sont créés par l'utilisateur actuellement connecté et qui sont partagés avec d'autres utilisateurs.
* *Dashboards Shared With Me* : il s'agit des tableaux de bord qui sont créés par d'autres utilisateurs et qui sont partagés avec l'utilisateur en cours.

Dans la section **EXPLORE** de l'interface utilisateur Web, les tableaux de bord sont organisés en deux groupes :
* *Default dashboards* : il s'agit des tableaux de bord prédéfinis.
* *My Dashboards* : il s'agit des tableaux de bord qui sont créés par l'utilisateur actuellement connecté.

Vous pouvez utiliser des tableaux de bord prédéfinis. Vous pouvez également créer des tableaux de bord personnalisés via l'interface utilisateur Web ou à l'aide d'un programme. Vous pouvez sauvegarder et restaurer des tableaux de bord à l'aide de scripts Python ou de l'API REST Sysdig.

Vous pouvez également copier et partager des tableaux de bord via l'interface utilisateur Web. 

Le tableau suivant décrit les tâches que vous pouvez exécuter pour utiliser des tableaux de bord à partir de l'interface utilisateur :

| Tâche | Description |
|------|-------------|
| [Création d'un tableau de bord](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_create) | Crée un tableau de bord personnalisé dans l'interface utilisateur Web. |
| [Copie d'un tableau de bord](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_copy) | Effectue une copie d'un tableau de bord dans l'équipe où le tableau est actuellement disponible, ou copie un tableau de bord dans une autre équipe. |
| [Modification de la portée](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_scope) | Modifie la portée d'un tableau de bord.       |
| [Suppression d'un tableau de bord](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_delete) |  Supprime un tableau de bord. |
| [Partager un tableau de bord](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_share) | Partage des tableaux de bord entre des utilisateurs dans une équipe, et en externe, en configurant une URL publique pour le tableau de bord. |
{: caption="Tableau 1. Tâches de tableau de bord que vous pouvez exécuter dans l'interface utilisateur Web" caption-side="top"} 

Le tableau suivant décrit les tâches que vous pouvez exécuter à l'aide d'un programme pour utiliser des tableaux de bord :

| Tâche                    |	Utilisation de l'API REST                |
|-------------------------|-------------------------------|
| Création d'un tableau de bord      | [Création d'un tableau de bord à l'aide de l'API](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_create_dashboard) |
| Suppression d'un tableau de bord      | [Suppression d'un tableau de bord à l'aide de l'API](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_delete_dashboard) |
| Sauvegarde de tableaux de bord       | [Sauvegarde des tableaux de bord d'une équipe à l'aide de l'API](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_save_dashboard) |
{: caption="Tableau 2. Tâches permettant de gérer les tableaux de bord à l'aide d'un programme" caption-side="top"} 



## Evénements
{: #monitoring_events}

Un événement est une notification qui vous informe sur un fait qui s'est produit dans l'un des noeuds qui transmettent les données à votre instance {{site.data.keyword.mon_full_notm}}. Utilisez des événements pour passer en revue, suivre et résoudre les problèmes. 

Il existe différents types d'événements : 

* Les *événements d'alerte* sont des événements qui sont déclenchés par des alertes configurées par l'utilisateur. Pour plus d'informations, voir [Utilisation des alertes](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-monitoring#monitoring_alerts).
* Les *événements d'infrastructure* sont des événements qui sont collectés à partir de noeuds Kubernetes et Docker. Par défaut, l'agent Sysdig reconnaît et collecte automatiquement les données provenant d'un groupe d'événements spécifique. Vous pouvez éditer le fichier de configuration de l'agent pour activer davantage d'événements.
* Les *événements personnalisés* que vous configurez via les intégrations suivantes : Slackbot, scripts Python préconfigurés, scripts Python personnalisés créés par l'utilisateur, ou demandes cURL.

Par défaut, un événement a un état : 
* *Actif* : cet état indique que les circonstances qui ont déclenché l'événement demeurent, par exemple, un noeud continue à être en panne.
* *OK* : cet état indique que la situation est revenue à la normale, par exemple, un noeud est opérationnel.

Vous pouvez gérer des événements dans la section *Events* de l'interface utilisateur Web. 
* Vous pouvez afficher des événements d'alerte via l'onglet *Alert Events*.
* Vous pouvez afficher des événements basés sur l'infrastructure via l'onglet *Custom events*.
* Vous pouvez afficher des événements personnalisés via l'onglet *Custom events*.
* Vous pouvez envoyer des événements personnalisés à l'une de vos équipes à l'aide du [jeton d'API pour cette équipe](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token). Pour plus d'informations, voir [Evénements personnalisés ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/222822463/Custom+Events){:new_window}.

Vous pouvez résoudre la situation qui a déclenché un événement. Pendant que vous attendez que la condition qui a déclenché l'événement s'exécute à nouveau et que vous définissiez
son statut sur *OK*, vous pouvez définir l'événement en tant que **Résolu** pour afficher graphiquement le fait que le problème ait été résolu. 
{: #tip}



## Alertes
{: #monitoring_alerts}

Une alerte est un événement de notification que vous pouvez utiliser pour avertir de situations qui requièrent votre attention. Chaque alerte possède un statut de gravité. Ce statut vous informe de l'importance des informations qu'elle signale. 

Lorsque vous définissez une alerte, vous devez définir la condition qui déclenche la notification, un ou plusieurs canaux de notification par le biais desquels vous voulez être averti, la gravité de l'alerte et le type d'alerte. 

Vous pouvez définir des alertes pour les types suivants :

| Type              | Description |
|-------------------|-------------|
| Détection d'anomalie | Permet de surveiller les hôtes en fonction de leur comportement historique et d'envoyer une alerte lorsqu'ils s'en écartent. |
| Indisponibilité          | Permet de surveiller tout type d'entité, par exemple, un hôte, un conteneur, un processus ou un service, et d'envoyer une alerte lorsque l'entité tombe en panne. |
| Evénement             | Permet de surveiller les occurrences d'événements spécifiques et d'envoyer une alerte si le nombre total d'occurrences dépasse un seuil. Par exemple, vous pouvez l'utiliser pour avertir des redémarrages et déploiements de conteneurs, d'orchestrations et d'événements de service.|
| Valeur extrême de groupe     | Permet de surveiller un groupe d'hôtes et d'être averti lorsque l'un d'eux agit différemment des autres. |
| Métrique            | Permet de surveiller les métriques de série temporelle et d'envoyer une alerte si elles dépassent les seuils définis par l'utilisateur. |
{: caption="Tableau 5. Types d'alerte" caption-side="top"} 

Par défaut, le niveau de gravité est défini sur *warning* (avertissement). Vous pouvez définir la gravité d'une alerte sur l'une des valeurs suivantes :
*emergency* (urgence), *alert* (alerte), *critical* (critique), *error* (erreur), *warning* (avertissement), *notice* (avis), *informational* (information), debug* (débogage) 

Vous pouvez définir un ou plusieurs canaux de notification pour l'une des intégrations de notification suivantes :
* Notifications par courrier électronique
* Notifications PagerDuty
* Notifications Slack
* Notifications VictorOps
* Notifications OpsGenie
* Configuration d'un canal webhook

Pour plus d'informations, voir [Configuration d'un canal de notification](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-notifications#notifications_create).


Vous pouvez activer des alertes prédéfinies, modifier des alertes et créer des alertes personnalisées dans l'interface utilisateur Web et à l'aide de l'API Sysdig.

Vous pouvez gérer des alertes dans la vue *Alerts* de l'interface utilisateur Web. Vous pouvez configurer les colonnes du tableau qui sont affichées dans la vue *Alerts*. Les options de colonne valides sont les suivantes : *Name*, *Scope*, *Alert When*, *Segment By*, *Notifications*, *Enabled*, *Modified*, *Captures*, *Channels*, *Created*, *Description*, *Email recipients*, *For at least*, *OpsGenie*, *PagerDuty*, *Severity*, *Slack*, *WebHook*, *SNS topics*, *Type*, *VictorOps*.

La liste suivante présente les principales tâches exécutées lorsque vous utilisez des alertes :
* [Configuration d'une alerte ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-ConfigureanAlert){:new_window}
* [Activation ou désactivation d'une alerte ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-Enable/DisableAlerts){:new_window} 
* [Recherche d'une alerte
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-SearchforanAlert){:new_window}
* [Modification d'une alerte ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-EditanExistingAlert){:new_window}
* [Copie d'une alerte dans la même équipe ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-CopyanAlerttothesameteam){:new_window}
* [Copie d'une alerte dans une autre équipe ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-CopyanAlerttoaDifferentTeam){:new_window}
* [Exportation d'une alerte ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-ExportAlertJSON){:new_window}
* [Suppression d'une alerte ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-DeleteAlerts){:new_window}
* [Définition de seuils d'alerte en tant qu'expressions booléennes personnalisées
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-AdvancedAlertThresholds){:new_window}


## Captures
{: #monitoring_captures}

Une capture est un fichier de trace que vous pouvez générer pour analyser les événements qui se produisent dans un noeud pendant une période donnée. La taille maximale du fichier de capture est 100 Mo. Par exemple, vous pouvez l'utiliser pour analyser les goulots d'étranglement ou les interactions de composants. 

Les captures contiennent des appels système et d'autres événements du système d'exploitation, tels que les temps d'attente au niveau système, la durée des travaux par lots,
les durées d'interruption des déploiements, les temps d'attente de la mise à l'échelle automatique, les heures de démarrage des conteneurs ou l'heure de la transaction d'application. Les captures incluent des informations détaillées provenant de chaque conteneur situé sur un noeud. 

En fonction des instructions de votre organisation, envisagez la désactivation des captures. Par défaut,
les captures sont activées lorsque vous configurez un agent Sysdig dans un noeud.
{: tip}

Vous pouvez créer, explorer, télécharger et supprimer des *captures* pour des noeuds individuels. Un noeud peut être un hôte, un conteneur, une machine virtuelle, un serveur bare metal, ou une source de métriques sur laquelle vous installez un agent Sysdig. 

* L'interface utilisateur Web vous permet de créer des captures dans la section *Explore* et de gérer les fichiers de capture via la section *Captures*.
* Vous pouvez visualiser les données d'une capture à l'aide de *Csysdig* (l'interface utilisateur de ligne de commande basée sur Curses pour Sysdig) ou des utilitaires Sysdig open source pour analyser les données d'une capture.
* Vous pouvez rechercher des données dans une capture à l'aide de filtres.
* Vous pouvez manipuler des données dans une capture à l'aide de chisels (scripts). 

Lorsque vous activez la fonction de capture pour une équipe, les fichiers de capture sont visibles uniquement par les membres de cette équipe.

La liste suivante présente les principales tâches exécutées lorsque vous utilisez des captures :
* [Création d'une capture](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures_create)
* [Suppression d'une capture](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures_delete)
* [Exploration d'une capture](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures_explore)
* [Téléchargement d'une capture](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures_download)

Pour plus d'informations, voir [Utilisation des captures](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures).


