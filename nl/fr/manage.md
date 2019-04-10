---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, manage

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

# Gestion des données
{: #manage}

Utilisez des libellés pour regrouper des ressources d'infrastructure en hiérarchies logiques, filtrer des données et fractionner les données agrégées en segments. Personnalisez l'agrégation des données lorsque vous configurez un graphique ou créez une alerte pour une métrique. Définissez la portée d'un tableau de bord, d'un panneau ou d'une alerte pour filtrer des points de données. Limitez l'accès aux données en gérant l'accès aux données des utilisateurs via des équipes. 
{:shortdesc}



## Libellés
{: #manage_labels}

Les **libellés** définissent les caractéristiques d'une métrique. Vous pouvez utiliser des libellés pour identifier et différencier les caractéristique d'une métrique. 

Les libellés sont classés en tant que libellés d'infrastructure et libellés de descripteur de métrique. Chaque métrique possède un ensemble de libellés prédéfinis. Pour les métriques personnalisées, vous pouvez configurer davantage de libellés. 

* Vous pouvez utiliser des **libellés d'infrastructure** pour identifier des objets au sein de l'infrastructure. Ces libellés sont obtenus à partir de l'infrastructure. Par exemple, un libellé peut être *kubernetes.pod.name*.
* Vous pouvez utiliser des **libellés de descripteur de métrique** pour définir des libellés personnalisés. Ces libellés sont des paires clé-valeur qui sont appliquées directement à des métriques, et sont obtenus à partir d'intégrations comme StatsD, Prometheus et JMX. 

## Groupes
{: #manage_groups}

Les **groupes** organisent des objets d'infrastructure en hiérarchies logiques. Utilisez des groupes pour structurer votre infrastructure et faciliter la surveillance de votre environnement.

Dans la vue *Explorer* de l'interface utilisateur Web, vous pouvez exécuter l'une des actions suivantes :

| Tâche                                                                                        | Description     |
|---------------------------------------------------------------------------------------------|-----------------|
| [Copie d'un groupe](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-groups#copy_group)                | Copie un groupe dans d'autres équipes. |
| [Création d'un groupe](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-groups#create_group)            | Crée un nouveau groupe. |
| [Suppression d'un groupe](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-groups#delete_group)            | Supprime un groupe. |
| [Changement de nom d'un groupe](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-groups#rename_group)            | Renomme un groupe. |
| [Partage d'un groupe](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-groups#share_group)              | Partage un groupe avec d'autres membres de l'équipe. |
{: caption="Tableau 1. Libellés de regroupement de tâches" caption-side="top"} 



## Agrégation
{: #manage_aggregation}

Une **agrégation** de données se produit automatiquement lorsque vous configurez un graphique ou créez une alerte pour une métrique. Il existe deux types d'agrégation : l'agrégation de temps et l'agrégation de groupe. 
* L'agrégation de temps s'effectue toujours avant l'agrégation de groupe.
* Pour créer des comparaisons multisérie et plusieurs alertes, vous pouvez également fractionner les données agrégées en sections plus petites
appelées **segments** en utilisant des libellés. 

Sysdig agrège des données au fil du temps. Il prend ensuite ces points de données et les regroupe pour afficher les données dans des métriques et des tableaux de bord, ou calcule des seuils d'alerte. 
{: tip}

Vous pouvez personnaliser l'agrégation des données lorsque vous configurez un graphique ou créez une alerte pour une métrique.

Il existe deux formes d'agrégation utilisées pour les métriques : 
* Agrégation de temps
* Agrégation de groupe

**L'agrégation de temps s'effectue toujours avant l'agrégation de groupe. **


### Agrégation de temps
{: #manage_time_aggregation}

**Par défaut, un agent Sysdig collecte et indique des métriques à une résolution de 10 secondes.**

Dans des graphiques de série temporelle incluant des données pour 5 minutes au maximum, 
* les points des données sont tracés à une résolution de 10 secondes,
* l'agrégation de temps n'a pas lieu.

L'agrégation de temps se produit automatiquement dans l'une des situations suivantes :

* Dans les graphiques de série temporelle incluant des données pour une durée supérieure à cinq minutes, les points de données sont tracés sous forme d'agrégat pour un intervalle de temps approprié. Par exemple, pour un graphique qui présente les données d'une heure, chaque point de données représente un intervalle d'une minute.
* Lorsque vous affichez des données d'historique. Les données sont cumulées au fil du temps. Vous pouvez choisir les points de données à utiliser lorsque vous affichez des données plus anciennes.

Le tableau suivant répertorie les différents types d'agrégation pour les graphiques de série temporelle :

| Type d'agrégation | Description                                                              |
|------------------|--------------------------------------------------------------------------|
| average          | Moyenne des valeurs de métrique extraites sur la période d'évaluation. |
| rate (timeAvg)   | Valeur moyenne de la métrique sur la période d'évaluation.            |
| maximum	         | Valeur la plus élevée au cours de la période d'évaluation.                          |
| minimum	         | Valeur la plus faible au cours de la période d'évaluation.                           |
| sum              | Somme combinée de la métrique sur la période d'évaluation.             |
{: caption="Tableau 2. Types d'agrégation pour les graphiques de série temporelle" caption-side="top"} 

**Remarque :** Par défaut, le type average est utilisé pour afficher des points de données pour un intervalle de temps.

Les types d'agrégation rate et average sont très similaires. Ils génèrent souvent le même résultat. Cependant, leur calcul est différent. Si l'agrégation de temps est définie sur
une minute, l'agent Sysdig est configuré pour extraire six échantillons, soit un toutes les 10 secondes. Notez que dans certains cas, les échantillons risquent de ne pas être générés en
raison de déconnexions ou d'autres circonstances.


### Agrégation de groupe
{: #manage_group_aggregation}

**Par défaut, la moyenne des métriques qui sont appliquées à un groupe de ressources, comme plusieurs conteneurs, hôtes, ou noeuds, est calculée entre les membres du groupe.**

Par exemple, si trois hôtes indiquent une utilisation d'UC différente pour un intervalle d'échantillonnage, la moyenne des trois valeurs est calculée et reportée sur le graphique sous la forme d'un point de données unique pour cette métrique.

Le tableau suivant répertorie les différents types d'agrégation de groupe :

| Type d'agrégation | Description                                        |
|------------------|----------------------------------------------------|
| average          | Valeur moyenne des échantillons de l'intervalle.           |
| maximum	         | Valeur la plus élevée des échantillons de l'intervalle.           |
| minimum	         | Valeur la plus faible des échantillons de l'intervalle.            |
| sum              | Valeur combinée des échantillons de l'intervalle.          |
{: caption="Tableau 3. Types d'agrégation pour une agrégation de groupe" caption-side="top"} 


**L'agrégation de groupe dépend de la segmentation.** Pour une vue qui affiche les métriques d'un groupe d'éléments, si la sélection *Segment By* est modifiée pour décomposer les éléments individuels, l'agrégation de groupe n'a pas lieu.



## Portée
{: #manage_scope}

La **portée** est une collection de libellés qui définissent les conditions de filtrage des points de données lorsque vous créez des tableaux de bord et des panneaux, que vous configurez des alertes et que vous personnalisez des équipes. 

Le tableau suivant répertorie les tâches que vous pouvez exécuter pour modifier la portée dans le service de surveillance :

| Tâche                                                                                        | Description     |
|---------------------------------------------------------------------------------------------|-----------------|
| [Modification de la portée d'un tableau de bord](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_scope) | Modifie la portée d'un tableau de bord pour filtrer des points de données pour toutes les métriques affichées via des panneaux du tableau de bord. |
| [Modification de la portée d'un panneau](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_scope) | Modifie la portée d'un panneau pour filtrer les données d'une métrique spécifique qui sont affichées via un panneau. |
| [Modification de la portée d'une équipe](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-teams#teams_scope) | Modifie la portée des données qui sont visibles par les utilisateurs membres d'une équipe. |
{: caption="Tableau 4. Tâches de modification de la portée" caption-side="top"} 


## Equipes
{: #manage_teams}

Les **équipes** regroupent des utilisateurs et contrôlent les données et les droits qui permettent d'utiliser des captures Sysdig et des événements d'infrastructure pour ces utilisateurs. 

Un administrateur Sysdig peut définir autant d'équipes qu'il le souhaite. Pour chaque équipe, il peut configurer les informations suivantes :
* L'*équipe par défaut* : vous pouvez définir cette équipe de sorte que tout utilisateur qui se connecte à l'interface utilisateur Web pour la première fois lui soit affecté par défaut.
* Le *point d'entrée par défaut* : vous pouvez définir la vue qui s'ouvre dans l'interface utilisateur Web chaque fois qu'un utilisateur se connecte. Les points d'entrée valides sont les suivants : vue *Explorer*, vue *Tableaux de bord*, vue *Evénements*, vue *Alertes* et vue *Paramètres*.
* La portée : vous pouvez limiter les données que les utilisateurs peuvent voir. Vous pouvez choisir *Hôte* ou *Conteneur* pour définir le niveau de données visible. Vous pouvez ensuite ajouter une ou plusieurs conditions. Si la portée est définie sur *Hôte*, les utilisateurs peuvent voir toutes les informations de niveau hôte et conteneur. Si la portée est définie sur *Conteneur*, les utilisateurs peuvent voir uniquement les informations de niveau conteneur.
* Droits : vous pouvez activer ou désactiver les fonctions suivantes : *captures Sysdig* et *événements d'infrastructure*. Les fichiers de capture seront visibles uniquement par les membres de l'équipe. **Remarque :** Les captures incluent des informations détaillées provenant de chaque conteneur situé sur un hôte, quelle que soit la portée de l'équipe. Lorsque des événements d'infrastructure sont activés, les utilisateurs peuvent afficher tous les événements d'infrastructure personnalisés provenant de chaque utilisateur et agent Sysdig dans l'instance.

Une équipe **Monitor Operations** est prédéfinie par défaut pour chaque instance {{site.data.keyword.mon_full_notm}}.
* Cette équipe ne peut pas être supprimée.
* Les utilisateurs sont automatiquement ajoutés en tant que membres de cette équipe et sont dotés d'une visibilité complète sur toutes les ressources disponibles dans l'instance. 

**Remarque :** 
* Un administrateur doit basculer vers l'équipe *Monitor Operations* pour pouvoir créer des équipes ou modifier les paramètres d'autres équipes.
* Une fois qu'un utilisateur se connecte à {{site.data.keyword.cloud_notm}} et lance l'interface utilisateur Web Sysdig, un administrateur peut gérer cet utilisateur
dans l'interface utilisateur Web Sysdig. L'utilisateur est créé dans la base de données Sysdig lorsqu'il se connecte à l'interface utilisateur Web Sysdig pour la première fois. 

Pour restreindre les droits d'affichage des utilisateurs, un administrateur peut effectuer l'une des actions suivantes :
* Modifier le rôle de l'utilisateur dans l'équipe *Monitor Operations* par défaut et lui affecter un rôle *Lire*. 
* Créer une équipe par défaut avec une portée et une visibilité limitées. Ensuite, il peut affecter manuellement des utilisateurs à d'autres équipes. 

Le tableau suivant répertorie les tâches que vous pouvez exécuter lorsque vous travaillez avec des équipes :

| Tâche                                                                            | Description                 |
|---------------------------------------------------------------------------------|-----------------------------|
| [Création d'une équipe](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-teams#teams_create)      | Crée une équipe pour contrôler la visibilité des données.  |
| [Suppression d'une équipe](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-teams#teams_delete)      | Supprime une équipe. </br>**Remarque :** Lorsque vous supprimez une équipe, les utilisateurs qui appartiennent uniquement à cette équipe sont déplacés vers l'équipe par défaut. |
| [Ajout de membres d'équipe](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-teams#teams_users)   | Ajoute davantage d'utilisateurs à une équipe. |
| [Edition d'une équipe ](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-teams#teams_scope)          | Modifie la portée des données qui sont visibles par les utilisateurs membres d'une équipe.  |
{: caption="Tableau 5. Tâches permettant de travailler avec des équipes" caption-side="top"} 





    


