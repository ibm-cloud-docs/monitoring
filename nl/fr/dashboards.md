---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, dashboards

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


# Utilisation des tableaux de bord
{: #dashboards}

Les tableaux de bord permettent de surveiller votre infrastructure, vos applications et vos services. Vous pouvez utiliser des tableaux de bord prédéfinis. Vous pouvez également créer des tableaux de bord personnalisés via l'interface utilisateur Web ou à l'aide d'un programme. Vous pouvez sauvegarder et restaurer des tableaux de bord à l'aide de scripts Python.
{:shortdesc}

Un **tableau de bord** affiche des groupes de métriques qui génèrent des rapports sur la santé, la performance et l'état de votre infrastructure, de vos applications et de vos services pour un hôte unique ou un groupe d'hôtes. Les tableaux de bord détaillent les données réseau, les données d'application, la topologie, les services, les hôtes et les conteneurs.

Dans la section **DASHBOARDS** de l'interface utilisateur Web, les tableaux de bord sont organisés en trois groupes principaux :

* *My Dashboards* : il s'agit des tableaux de bord qui sont créés par l'utilisateur actuellement connecté.
* *My Shared Dashboards* : il s'agit des tableaux de bord qui sont créés par l'utilisateur actuellement connecté et qui sont partagés avec d'autres utilisateurs.
* *Dashboards Shared With Me* : il s'agit des tableaux de bord qui sont créés par d'autres utilisateurs et qui sont partagés avec l'utilisateur en cours.

Dans la section **EXPLORE** de l'interface utilisateur Web, les tableaux de bord sont organisés en deux groupes :
* *Default dashboards* : il s'agit des tableaux de bord prédéfinis.
* *My Dashboards* : il s'agit des tableaux de bord qui sont créés par l'utilisateur actuellement connecté.

Vous pouvez copier et partager des tableaux de bord via l'interface utilisateur Web. 

Vous pouvez exécuter des scripts pour effectuer les actions suivantes à l'aide d'un programme :
* Sauvegarder les tableaux de bord existants dans un fichier local.
* Créer de nouveaux tableaux de bord identiques à ceux que vous sauvegardez.
* Restaurer des tableaux de bord.



## Tableaux de bord prédéfinis
{: #dashboards_predefined}

Les tableaux de bord prédéfinis sont conçus autour des diverses applications prises en charge, des topologies de réseau, des agencements d'infrastructure et des services. 

Les tableaux de bord prédéfinis incluent une série de panneaux qui sont déjà configurés.

Le tableau suivant répertorie les différents types de tableaux de bord prédéfinis :

| Type | Description | Informations complémentaires | 
|------|-------------|------------------|
| Applications | Tableaux de bord que vous pouvez utiliser pour surveiller vos applications et les composants de l'infrastructure.  | [Tableaux de bord d'application](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-default_dashboards#default_dashboards_applications) |
| Hôte et conteneurs | Tableaux de bord que vous pouvez utiliser pour surveiller l'utilisation des ressources et l'activité du système sur vos hôtes et dans vos conteneurs. | [Tableaux de bord d'hôte et de conteneur](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-default_dashboards#default_dashboards_host_container) |
| Réseau | Tableaux de bord que vous pouvez utiliser pour surveiller vos connexions réseau et votre activité. | [Tableaux de bord de réseau](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-default_dashboards#default_dashboards_network) |
| Service | Tableaux de bord que vous pouvez utiliser pour surveiller les performances de vos services, même si ces derniers sont déployés dans des conteneurs orchestrés. | [Tableaux de bord de service](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-default_dashboards#default_dashboards_service) |
| Topologie | Tableaux de bord que vous pouvez utiliser pour surveiller les dépendances logiques de vos groupes de serveurs d'applications et métriques de superposition. | [Tableaux de bord de topologie](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-default_dashboards#default_dashboards_topology) |
{: caption="Tableau 1. Liste des tableaux de bord prédéfinis" caption-side="top"} 



## Création de tableaux de bord personnalisés dans l'interface utilisateur Web
{: #dashboards_create}

Lorsque vous créez un tableau de bord personnalisé, vous pouvez utiliser un modèle tel qu'un tableau de bord prédéfini, ou choisir un tableau de bord vierge. Un tableau de bord contient des panneaux qui sont configurés pour afficher des données spécifiques dans différents formats. Vous pouvez également définir la façon dont les données sont agrégées. La **portée** définit les données qui sont utilisées pour l'agrégation et affichées. Vous pouvez définir la portée au niveau du tableau de bord, ou pour la remplacer pour chacun des panneaux. 

Pour créer un tableau de bord personnalisé, procédez comme suit :

1. Accédez à la section *DASHBOARD** dans l'interface utilisateur Web, puis sélectionnez **Add Dashboard**. La page *Create a New Dashboard* s'ouvre.

    1. Sélectionnez un tableau de bord prédéfini ou choisissez le *tableau de bord vierge*. 

    2. Entrez un nom pour le tableau de bord.

    3. Cliquez sur **Create Dashboard**.

2. Définissez la portée du tableau de bord. Cliquez sur **c** pour modifier la portée par défaut. **Everywhere** est sélectionné par défaut.
    
    1. Sélectionnez la portée. 

    2. Cliquez éventuellement sur **Override the custom panel scopes** pour remplacer la portée de tous les panneaux pour lesquels une portée personnalisée est actuellement définie. **Remarque : cette action ne peut pas être annulée.** 

    **Remarque :** Pour réinitialiser la portée du tableau de bord sur la totalité de l'infrastructure, ou pour mettre à jour la portée d'un tableau de bord existant sur l'ensemble de l'infrastructure, sélectionnez **Everywhere**.

    3. Cliquez sur **Save**.

3. Configurez les panneaux. Répétez cette étape pour tous les panneaux du tableau de bord que vous souhaitez modifier.

    1. Identifiez le panneau que vous souhaitez modifier.

    2. Sélectionnez **Edit Panel**. Il s'agit de l'icône en forme de crayon.
    
    3. Changez le type de graphique.

    4. Changez la métrique et le taux. Le taux définit le type d'agrégation qui est effectué sur les données.

    5. Changez la portée du panneau. Cliquez sur **Override Dashboard Scope**. Modifiez ensuite la portée. Si vous avez besoin de restaurer la portée du tableau de bord sur le panneau, sélectionnez **Default to Dashboard Scope**.

    6. Dans la zone *Compare to*, cliquez sur **Configure**. Définissez la plage de temps pour la comparaison.

    7. Définissez la couleur d'arrière-plan du panneau en fonction des seuils de métrique. Cliquez sur **Override Color Coding**, puis sur **Enable**. Définissez des valeurs pour les différents seuils.

    8. Cliquez sur **Save**.


## Modification de la portée
{: #dashboards_scope}

Au lieu de modifier la portée d'un tableau de bord prédéfini, copiez le tableau de bord et modifiez la portée dans le tableau de bord copié.
{: tip}

Procédez comme suit pour modifier la portée d'un tableau de bord :

1. Accédez à la section **DASHBOARD** dans l'interface utilisateur Web, puis sélectionnez un tableau de bord.

2. Cliquez sur **c** pour modifier la portée par défaut. 

    **Everywhere** est sélectionné par défaut.
    
3. Sélectionnez la portée. 

4. Cliquez éventuellement sur **Override the custom panel scopes** pour remplacer la portée de tous les panneaux pour lesquels une portée personnalisée est actuellement définie. 

    **Remarque : cette action ne peut pas être annulée.** 

    Pour réinitialiser la portée du tableau de bord sur la totalité de l'infrastructure, ou pour mettre à jour la portée d'un tableau de bord existant sur l'ensemble de l'infrastructure, sélectionnez **Everywhere**.
    {: tip}

5. Cliquez sur **Save**.



## Copie d'un tableau de bord
{: #dashboards_copy}

Lorsque vous copiez un tableau de bord, vous créez un doublon.

Le tableau suivant présente les différentes actions et les droits utilisateur requis pour copier un tableau de bord :

| Action     |	Autorisation de copie     |	Instance du tableau de bord	   | Autorisation d'affichage du tableau de bord     | Autorisation de modification du tableau de bord  |
|------------|-------------------|-------------------------|--------------------------------|-----------------------------|
| Copie dans l'équipe en cours    |	Utilisateurs de l'équipe dotés de droits d'édition | Nouvelle instance de tableau de bord  | Membres de l'équipe dotés de droits d'affichage	 | Utilisateurs de l'équipe dotés de droits d'édition |
| Copie dans une autre équipe    | Utilisateurs de l'équipe dotés de droits d'édition dans les deux équipes | Nouvelle instance de tableau de bord  | Si le tableau de bord d'origine n'est pas partagé, seul l'utilisateur qui le copie dispose d'un accès. </br>Si le tableau de bord d'origine est partagé, tous les membres de l'équipe disposent d'un accès. | Si le tableau de bord d'origine n'est pas partagé, seul l'utilisateur qui le copie. </br>Si le tableau de bord d'origine est partagé, tous les membres de l'équipe dotés de droits d'édition. |
{: caption="Tableau 2. Informations relatives aux utilisateurs et aux tableaux de bord pour la copie de tableaux de bord" caption-side="top"} 

Procédez comme suit pour copier un tableau de bord dans l'interface utilisateur Web :

1. Accédez à la section *DASHBOARDS* dans l'interface utilisateur Web.
2. Sélectionnez le tableau de bord situé dans le panneau de gauche.
3. Cliquez sur **Settings** (icône des trois points), puis sélectionnez **Copy dashboard**. 
4. Sélectionnez l'emplacement où copier le tableau de bord.

    1. Choisissez **Current Team** pour copier le tableau de bord de l'équipe en cours.
    
    2. Choisissez **Other Teams** pour copier le tableau de bord dans d'autres équipes. Sélectionnez les équipes où vous souhaitez copier le tableau de bord.

    3. Saisissez un nom pour le tableau de bord.

    4. Cliquez sur **Send copy**.
    
    5. Vérifiez que la portée du tableau de bord dans la nouvelle équipe est mise à jour en fonction des droits de l'équipe de destination.

## Suppression d'un tableau de bord
{: #dashboards_delete}

Procédez comme suit pour supprimer un tableau de bord dans l'interface utilisateur Web :

1. Accédez à la section *DASHBOARDS* dans l'interface utilisateur Web.
2. Sélectionnez le tableau de bord situé dans le panneau de gauche.
3. Cliquez sur **Settings** ![icône des trois points](images/actions.png), puis sélectionnez **Delete dashboard**. 
4. Confirmez la suppression en cliquant sur **Yes, delete dashboard**.


## Partage d'un tableau de bord
{: #dashboards_share}

Vous pouvez partager des tableaux de bord entre des utilisateurs dans une équipe, et en externe, en configurant une URL publique pour le tableau de bord.  

Le tableau suivant présente les différentes actions et les droits utilisateur requis pour partager un tableau de bord ou utiliser un tableau de bord partagé :

| Action      |	Autorisation de partage        |	Instance du tableau de bord	       | Autorisation d'affichage du tableau de bord        | Autorisation de modification du tableau de bord  |
|-------------|-------------------|-----------------------------|------------------------------------|-----------------------------|
| Partage avec l'équipe en cours |	Créateur du tableau de bord         |	Partage de la même instance du tableau de bord   | Membres de l'équipe dotés de droits d'affichage  | Membres de l'équipe dotés de droits d'édition   |
| Partage public en tant qu'URL	  | Tout éditeur de l'équipe |	Partage de la même instance du tableau de bord   | Tout le monde     | Personne                      |
{: caption="Tableau 3. Informations relatives aux utilisateurs et aux tableaux de bord pour le partage de tableaux de bord" caption-side="top"} 


Procédez comme suit pour partager un tableau de bord dans l'interface utilisateur Web :

1. Accédez à la section *DASHBOARDS* dans l'interface utilisateur Web.
2. Sélectionnez le tableau de bord situé dans le panneau de gauche.
3. Cliquez sur **Settings** ![icône des trois points](images/actions.png), puis sélectionnez **Share**.
4. Choisissez le mode de partage du tableau de bord :

    * Activez la règle **Share with Team** pour partager le tableau de bord avec l'équipe en cours. L'équipe dans laquelle le tableau de bord est partagé s'affiche.

    * Activez la règle **Share Public URL** pour afficher l'URL publique personnalisée.

5. Cliquez sur **Close**.

Partagez un tableau de bord en externe pour permettre à des utilisateurs externes d'afficher les métriques du tableau de bord, tout en limitant l'accès à la modification des panneaux et des configurations.
{: tip}


## Gestion des tableaux de bord à l'aide d'un programme
{: #dashboards_programmatically}

Utilisez l'API REST Sysdig pour automatiser des tâches de routine et surveiller des notifications. Vous pouvez également utiliser la bibliothèque Python Sysdig. 

**Remarque :** La bibliothèque Python expose une partie de la fonctionnalité d'API REST Sysdig. 


Lorsque vous utilisez l'API à partir de vos programmes ou scripts personnalisés, vous devez vous servir d'un jeton Sysdig pour vous authentifier sur l'instance {{site.data.keyword.mon_full_notm}}. Pour plus d'informations, voir [Utilisation des jetons d'API](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token).


| Tâche                    | Utilisation de l'API REST                |
|-------------------------|-------------------------------|
| Création d'un tableau de bord      | [Création d'un tableau de bord à l'aide de l'API](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_create_dashboard) |
| Suppression d'un tableau de bord      | [Suppression d'un tableau de bord à l'aide de l'API](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_delete_dashboard) |
| Sauvegarde de tableaux de bord       | [Sauvegarde des tableaux de bord d'une équipe à l'aide de l'API](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_save_dashboard) |
{: caption="Tableau 4. Tâches permettant de gérer les tableaux de bord à l'aide d'un programme" caption-side="top"} 


