---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, teams

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

# Utilisation des équipes
{: #teams}

Un administrateur ou un responsable d'une instance {{site.data.keyword.mon_full_notm}} peut créer, supprimer, ajouter des membres et modifier la portée des équipes dans cette instance. 
{:shortdesc} 

Un administrateur ou un responsable d'une instance {{site.data.keyword.mon_full_notm}} doit basculer vers l'équipe *Monitor Operations* pour pouvoir créer des équipes et gérer les équipes existantes.
{: tip}

## Création d'une équipe
{: #teams_create}

Pour créer une équipe, procédez comme suit :

1. Lancez l'interface utilisateur Web. Pour plus d'informations sur le lancement de l'interface utilisateur Web,
voir [Accès à l'interface utilisateur Web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. A partir du bouton *Sélecteur* dans la barre de navigation, sélectionnez **Monitor Operations**. Choisissez ensuite **Settings**.

3. Sélectionnez **Teams**. La liste des équipes existantes s'affiche.

4. Cliquez sur **Add Team**. La page de configuration d'équipe s'affiche.

5. Configurez les détails de l'équipe. 

    * Choisissez une couleur.

    * Saisissez le nom de l'équipe.

    * [Facultatif] Entrez une description pour cette équipe.

    * [Facultatif] Définissez le paramètre **Default team** si vous voulez que cette équipe devienne l'équipe par défaut pour les nouveaux utilisateurs.

    * Définissez le **Point d'entrée par défaut** pour spécifier la vue de l'interface utilisateur Web qui s'ouvre chaque fois qu'un utilisateur se connecte. Les points d'entrée valides sont les suivants : vue *Explorer*, vue *Tableaux de bord*, vue *Evénements*, vue *Alertes* et vue *Paramètres*. La vue *Explorer* est définie par défaut.

6. Configurez la portée de l'équipe. 

    * [Facultatif] Définissez le paramètre **Scope by** pour spécifier le niveau de données auquel les membres de l'équipe ont accès. Les valeurs admises sont *host* et *container*. Si le paramètre est défini sur *Host*, les membres peuvent voir toutes les informations de niveau hôte et conteneur. Si le paramètre est défini sur *Container*, les membres peuvent voir uniquement les informations de niveau conteneur.

    * Définissez la **portée** pour limiter les données que les utilisateurs peuvent voir. Vous pouvez définir une ou plusieurs conditions en spécifiant des expressions pour les métriques. Par défaut, la portée est définie sur *everywhere*.
	
    * [Facultatif] Activez ou désactivez l'option **Sysdig captures**. Cochez cette case pour autoriser cette équipe à prendre des captures Sysdig. Les fichiers de capture seront visibles uniquement par les membres de cette équipe. **Remarque :** Les captures incluent des informations détaillées provenant de chaque conteneur situé sur un hôte, quelle que soit la portée de l'équipe.

    * [Facultatif] Activez ou désactivez l'option **Infrastructure Events**. Cochez cette case pour autoriser les membres à afficher tous les événements d'infrastructure personnalisés provenant de chaque utilisateur et agent Sysdig dans l'instance. Lorsqu'elle n'est pas cochée, les utilisateurs peuvent voir les événements d'infrastructure qui sont envoyés spécifiquement à cette équipe. 

6. Ajoutez des membres à l'équipe. Cliquez sur **Assign user**. Recherchez un utilisateur et ajoutez-le.



## Modification de la portée d'une équipe
{: #teams_scope}

Pour modifier la portée des données qui sont visibles par les membres d'une équipe, procédez comme suit : 

1. Lancez l'interface utilisateur Web. Pour plus d'informations sur le lancement de l'interface utilisateur Web,
voir [Accès à l'interface utilisateur Web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. A partir du bouton *Sélecteur* dans la barre de navigation, sélectionnez **Monitor Operations**. Choisissez ensuite **Settings**.

3. Sélectionnez **Teams**. La liste des équipes existantes s'affiche.

4. Identifiez l'équipe et sélectionnez-la. Les détails de l'équipe s'affichent.

5. Modifiez les informations de configuration dans la section *Visibilité*.

6. Cliquez sur **Sauvegarder**. 


## Ajout d'utilisateurs à une équipe
{: #teams_users}

Pour ajouter des membres à une équipe, procédez comme suit : 

1. Lancez l'interface utilisateur Web. Pour plus d'informations sur le lancement de l'interface utilisateur Web,
voir [Accès à l'interface utilisateur Web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. A partir du bouton *Sélecteur* dans la barre de navigation, sélectionnez **Monitor Operations**. Choisissez ensuite **Settings**.

3. Sélectionnez **Teams**. La liste des équipes existantes s'affiche.

4. Identifiez l'équipe et sélectionnez-la. Les détails de l'équipe s'affichent.

5. Cliquez sur **Assign user** dans la section *Team users*.

6. Cliquez sur **Save**. 


## Suppression d'une équipe
{: #teams_delete}

L'équipe par défaut, **Monitor Operations**, ne peut pas être supprimée. 

Pour supprimer une équipe, procédez comme suit :

1. Lancez l'interface utilisateur Web. Pour plus d'informations sur le lancement de l'interface utilisateur Web,
voir [Accès à l'interface utilisateur Web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. A partir du bouton *Sélecteur* dans la barre de navigation, sélectionnez **Monitor Operations**. Choisissez ensuite **Settings**.

3. Sélectionnez **Teams**. La liste des équipes existantes s'affiche.

4. Identifiez l'équipe que vous voulez supprimer et sélectionnez-la. Les détails de l'équipe s'affichent.

5. Cliquez sur **Delete team**.

**Remarque :** Lorsque vous supprimez une équipe, les utilisateurs qui appartiennent uniquement à cette équipe sont déplacés vers l'équipe par défaut.



