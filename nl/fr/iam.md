---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, iam

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

 
# Gestion de l'accès utilisateur dans {{site.data.keyword.cloud_notm}}
{: #iam}

{{site.data.keyword.iamlong}} (IAM) vous permet d'authentifier les utilisateurs en toute sécurité et de contrôler l'accès à toutes les ressources de cloud de façon cohérente dans {{site.data.keyword.cloud_notm}}. 
{:shortdesc}

**Une règle d'accès avec un rôle utilisateur IAM doit être affectée à chaque utilisateur disposant d'un accès au service {{site.data.keyword.mon_full_notm}} sur votre compte.** La règle détermine les actions que l'utilisateur peut effectuer dans le cadre du service ou de l'instance que vous sélectionnez. Les actions autorisées sont personnalisées et définies en tant qu'opérations exécutables sur le service. Les actions sont ensuite mappées à des rôles utilisateur IAM.

Les *règles* permettent d'accorder l'accès à différents niveaux. Certaines des options sont les suivantes : 

* Accès à tous les services activés par IAM dans votre compte
* Accès à toutes les instances du service dans une région unique dans votre compte
* Accès à une instance de service individuelle de votre compte
* Accès à toutes les instances du service dans le cadre d'un groupe de ressources
* Accès à toutes les instances du service dans une région unique dans le cadre d'un groupe de ressources
* Accès à tous les services activés par IAM dans le cadre d'un groupe de ressources

Les *rôles* définissent les actions qu'un utilisateur ou un ID de service peut exécuter. Il existe différents types de rôles dans {{site.data.keyword.cloud_notm}} :
* Les *rôles de gestion de plateforme* permettent aux utilisateurs d'effectuer des tâches sur des ressources de service au niveau de la plateforme, par exemple d'affecter un accès utilisateur pour le service, de créer ou supprimer des ID de service, de créer des instances, d'affecter des règles pour votre service à d'autres utilisateurs et de lier des instances à des applications.
* Les *rôles d'accès à un service* permettent d'affecter divers niveaux de droits aux utilisateurs pour appeler l'API du service.

**Pour organiser un ensemble d'utilisateurs et d'ID de service en une entité unique qui facilite la gestion des droits IAM, utilisez des **groupes d'accès*.** Vous pouvez affecter une règle unique au groupe au lieu d'affecter plusieurs fois le même accès par utilisateur ou ID de service individuel.
{: tip}


## Gestion de l'accès à l'aide de groupes d'accès
{: #iam_groups}

Pour gérer l'accès ou affecter un nouvel accès à des utilisateurs à l'aide de groupes d'accès, vous devez être le propriétaire du compte, l'administrateur ou l'éditeur sur tous les services avec l'offre Identity and Access activée dans le compte, ou être l'administrateur ou l'éditeur affecté pour le service Groupes d'accès IAM. 

Choisissez l'une des actions suivantes pour gérer les groupes d'accès dans {{site.data.keyword.cloud_notm}} :

* [Création d'un groupe d'accès](/docs/iam?topic=iam-groups#create_ag).
* [Affectation d'accès à un groupe](/docs/iam?topic=iam-groups#access_ag).


## Gestion de l'accès en affectant des règles directement à des utilisateurs
{: #iam_users}

Pour gérer l'accès ou affecter un nouvel accès à des utilisateurs à l'aide de règles IAM, vous devez être le propriétaire du compte, l'administrateur de tous les services du compte, ou un administrateur du service ou de l'instance de service spécifique. 

Choisissez l'une des actions suivantes pour gérer les règles IAM dans {{site.data.keyword.cloud_notm}} :

* Pour modifier les droits d'un utilisateur, voir [Edition d'un accès existant](/docs/iam?topic=iam-iammanidaccser#edit_existing).
* Pour accorder des droits à un utilisateur, voir [Affectation d'un nouvel accès](/docs/iam?topic=iam-iammanidaccser#assign_new_access).
* Pour révoquer des droits d'accès, voir [Retrait de l'accès](/docs/iam?topic=iam-iammanidaccser#removing_access).
* Pour consulter les droits d'un utilisateur, voir [Révision des accès affectés](/docs/iam?topic=iam-iammanidaccser#review_your_access).


## Rôles de plateforme {{site.data.keyword.cloud_notm}}
{: #iam_platform}

Utilisez le tableau suivant pour identifier le rôle de plateforme que vous pouvez accorder à un utilisateur dans {{site.data.keyword.cloud_notm}} afin d'exécuter l'une des actions de plateforme suivantes :

| Actions de plateforme                                                        | Rôles de plateforme {{site.data.keyword.cloud_notm}}    | 
|-------------------------------------------------------------------------|------------------------------------------------------|
| `Octroi de l'accès à d'autres membres du compte pour utiliser le service`           | Administrateur                                        | 
| `Mise à disposition d'une instance de service`                                          | Administrateur </br>Editeur                            | 
| `Suppression d'une instance de service`                                             | Administrateur </br>Editeur                            | 
| `Création d'un ID de service`                                                   | Administrateur </br>Editeur                            |
| `Affichage des détails d'une instance de service`                                    | Administrateur </br>Editeur </br>Opérateur </br>Afficheur  | 
| `Affichage des instances de service dans le tableau de bord de surveillance de l'observabilité`      | Administrateur </br>Editeur </br>Opérateur </br>Afficheur  | 
{: caption="Tableau 1. Rôles et actions des utilisateurs IAM" caption-side="top"}



## Rôles Sysdig
{: #iam_sysdig_roles}

Le tableau suivant décrit les rôles Sysdig et les actions pour chacun d'eux :

| Actions                                                                    | Rôle Sysdig                                          | 
|----------------------------------------------------------------------------|------------------------------------------------------|
| `Réinitialisation de la clé d'accès Sysdig`                                              | Admin                                                |
| `Gestion des utilisateurs`                                                             | Admin                                                |
| `Création, configuration et suppression d'équipes`                                      | Admin                                                |
| `Configuration et suppression de canaux de notification`                              | Admin                                                | 
| `Configuration et suppression d'agents Sysdig`                                       | Admin                                                |
| `Création, suppression et édition de contenu dans l'interface utilisateur Web Sysdig`                    | Admin </br>Utilisateur                               |  
| `Affichage de métriques via l'interface utilisateur Web Sysdig`                                   | Admin </br>Utilisateur                               |  
| `Création et suppression d'alertes`                                                 | Admin </br>Utilisateur                               | 
| `Création et suppression de captures`                                               | Admin </br>Utilisateur                               |   
{: caption="Tableau 2. Rôles et actions Sysdig" caption-side="top"}


## Mappage de rôles Sysdig vers des rôles {{site.data.keyword.cloud_notm}}
{: #iam_sysdig}

Utilisez le tableau suivant pour voir la façon dont un rôle {{site.data.keyword.cloud_notm}} est mappé vers un rôle Sysdig :

| Type de rôle        | Rôle               | Rôle Sysdig                | Description                                 |
|---------------------|--------------------|----------------------------|---------------------------------------------|
| Rôle de plateforme       | Administrateur      | Admin                      | Accorde des privilèges admin Sysdig à l'utilisateur.   | 
| Rôle de service        | Responsable            | Admin                      | Accorde des privilèges admin Sysdig à l'utilisateur.   | 
| Rôle de service        | Auteur             | Utilisateur                       | Accorde des droits utilisateur Sysdig à l'utilisateur.    |
| Rôle de service        | Lecteur             |                            | Aucun droit n'est accordé.                 |
{: caption="Tableau 3. Rôles Sysdig" caption-side="top"}


