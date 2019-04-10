---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, iam, access groups

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

 
# Utilisation des règles IAM et des groupes d'accès
{: #iam_work}

{{site.data.keyword.iamlong}} (IAM) vous permet d'authentifier les utilisateurs en toute sécurité et de contrôler l'accès à toutes les ressources de cloud de façon cohérente dans {{site.data.keyword.cloud_notm}}. 
{:shortdesc}

Pour accorder des privilèges admin Sysdig à un utilisateur, vous pouvez lui attribuer l'un des rôles suivants :

* Rôle de plateforme `Administrateur` : accordez ce rôle si l'utilisateur est également un administrateur du service Sysdig dans {{site.data.keyword.cloud_notm}}.
* Rôle de plateforme `Editeur` : accordez ce rôle si l'utilisateur doit pouvoir mettre à disposition des instances Sysdig ou en supprimer dans {{site.data.keyword.cloud_notm}}.
* Rôle de service `Responsable` : accordez ce rôle si l'utilisateur ne doit pas pouvoir gérer le service Sysdig dans {{site.data.keyword.cloud_notm}}.

Pour accorder des droits utilisateur Sysdig à un utilisateur, vous pouvez lui affecter le rôle de service `Auteur`.

**Remarque :** Pour gérer l'accès ou affecter un nouvel accès à des utilisateurs à l'aide de règles IAM, vous devez être le propriétaire du compte, l'administrateur de tous les services du compte, ou un administrateur du service ou de l'instance de service spécifique. 

En tant que **propriétaire de compte** ou **administrateur de service {{site.data.keyword.mon_full_notm}}**, vous devez disposer de droits vous permettant d'exécuter les actions de plateforme suivantes : 

* Octroi de l'accès à d'autres membres du compte pour utiliser le service
* Mise à disposition d'une instance de service
* Supprimer une instance de service
* Affichage des détails d'une instance de service
* Création d'un ID de service

En tant qu'**utilisateur Devops**, vous devez disposer de droits vous permettant d'exécuter les actions de plateforme suivantes : 

* Mise à disposition d'une instance de service
* Supprimer une instance de service
* Affichage des détails d'une instance de service
* Création d'un ID de service


## Octroi de droits à un utilisateur pour devenir un administrateur du service dans le compte {{site.data.keyword.cloud_notm}}
{: #admin_account}

Pour accorder à un utilisateur le rôle d'administrateur afin qu'il gère le service dans le compte, l'utilisateur doit disposer d'une règle IAM pour le
service {{site.data.keyword.mon_full_notm}} avec le rôle de plateforme **Administrateur**. Vous devez attribuer cet accès utilisateur
à une ressource individuelle dans le compte. 

Procédez comme suit pour affecter un rôle d'administrateur au service {{site.data.keyword.mon_full_notm}} dans le compte : 

1. Dans la barre de menus, cliquez sur **Gérer** &gt; **Accès (IAM)** puis sélectionnez **Utilisateurs**.
2. Sur la ligne de l'utilisateur auquel vous voulez affecter un accès, sélectionnez le menu **Actions**, puis cliquez sur **Affecter un accès**.
3. Sélectionnez **Affecter l'accès aux ressources**.
4. Sélectionnez **{{site.data.keyword.mon_full_notm}}**.
5. Sélectionnez **Toutes les régions en cours**.
6. Sélectionnez **Toutes les instances de service en cours**.
7. Sélectionnez le rôle de plateforme **Administrateur**.
8. Cliquez sur Affecter.


## Octroi de droits à un utilisateur pour devenir un administrateur du service dans un groupe de ressources
{: #admin_rg}

Pour accorder à un utilisateur le rôle d'administrateur afin de gérer des instances au sein d'un groupe de ressources dans le compte, l'utilisateur doit disposer d'une règle IAM pour le service {{site.data.keyword.mon_full_notm}} avec le rôle de plateforme **Administrateur** dans le cadre du groupe de ressources. 

Procédez comme suit pour affecter un rôle d'administrateur au service {{site.data.keyword.mon_full_notm}} dans le cadre d'un groupe de ressources : 

1. Dans la barre de menus, cliquez sur **Gérer** &gt; **Accès (IAM)** puis sélectionnez **Utilisateurs**.
2. Sur la ligne de l'utilisateur auquel vous voulez affecter un accès, sélectionnez le menu **Actions**, puis cliquez sur **Affecter un accès**.
3. Sélectionnez **Affecter l'accès au sein d'un groupe de ressources**.
4. Sélectionnez un groupe de ressources.
5. Si aucun rôle n'a encore été accordé à l'utilisateur pour le groupe de ressources sélectionné, choisissez-en un pour la zone **Affecter l'accès à un groupe de ressources**. 

    Selon le rôle que vous sélectionnez, l'utilisateur peut afficher le groupe de ressources sur son tableau de bord, modifier le nom du groupe de ressources, ou gérer l'accès des utilisateurs au groupe. 
    
    Vous pouvez sélectionner **Aucun accès**, si vous souhaitez que l'utilisateur ait uniquement accès au service {{site.data.keyword.mon_full_notm}} dans le groupe de ressources.

6. Sélectionnez **{{site.data.keyword.mon_full_notm}}**.
7. Sélectionnez le rôle de plateforme **Administrateur**.
8. Cliquez sur **Affecter**.


## Octroi de droits à un utilisateur Devops pour gérer le service dans le compte {{site.data.keyword.cloud_notm}}
{: #devops_account}

Vous devez disposer d'une règle IAM pour le service {{site.data.keyword.mon_full_notm}} avec le rôle de plateforme **Editeur**.

Procédez comme suit pour affecter un rôle d'éditeur au service {{site.data.keyword.mon_full_notm}} dans le compte : 

1. Dans la barre de menus, cliquez sur **Gérer** &gt; **Accès (IAM)** puis sélectionnez **Utilisateurs**.
2. Sur la ligne de l'utilisateur auquel vous voulez affecter un accès, sélectionnez le menu **Actions**, puis cliquez sur **Affecter un accès**.
3. Sélectionnez **Affecter l'accès aux ressources**.
4. Sélectionnez **{{site.data.keyword.mon_full_notm}}**.
5. Sélectionnez **Toutes les instances de service**.
6. Sélectionnez le rôle de plateforme **Editeur**.
7. Cliquez sur Affecter.

## Octroi de droits à un utilisateur Devops pour gérer une instance dans le compte {{site.data.keyword.cloud_notm}}
{: #devops_account_instance}

Procédez comme suit pour affecter un rôle d'éditeur sur une instance du service {{site.data.keyword.mon_full_notm}} dans le compte : 

1. Dans la barre de menus, cliquez sur **Gérer** &gt; **Accès (IAM)** puis sélectionnez **Utilisateurs**.
2. Sur la ligne de l'utilisateur auquel vous voulez affecter un accès, sélectionnez le menu **Actions**, puis cliquez sur **Affecter un accès**.
3. Sélectionnez **Affecter l'accès aux ressources**.
4. Sélectionnez **{{site.data.keyword.mon_full_notm}}**.
5. Sélectionnez l'instance.
6. Sélectionnez le rôle de plateforme **Editeur**.
7. Cliquez sur Affecter.



## Octroi de droits à un utilisateur Devops pour gérer le service dans un groupe de ressources
{: #devops_rg}

Vous avez besoin d'une règle IAM pour le service {{site.data.keyword.mon_full_notm}} avec le rôle de plateforme **Editeur**.

Procédez comme suit pour affecter un rôle d'éditeur au service {{site.data.keyword.mon_full_notm}} dans le cadre d'un groupe de ressources : 

1. Dans la barre de menus, cliquez sur **Gérer** &gt; **Accès (IAM)** puis sélectionnez **Utilisateurs**.
2. Sur la ligne de l'utilisateur auquel vous voulez affecter un accès, sélectionnez le menu **Actions**, puis cliquez sur **Affecter un accès**.
3. Sélectionnez **Affecter l'accès au sein d'un groupe de ressources**.
4. Sélectionnez un groupe de ressources.
5. Si aucun rôle n'a encore été accordé à l'utilisateur pour le groupe de ressources sélectionné, choisissez-en un pour la zone **Affecter l'accès à un groupe de ressources**. 

    Selon le rôle que vous sélectionnez, l'utilisateur peut afficher le groupe de ressources sur son tableau de bord, modifier le nom du groupe de ressources, ou gérer l'accès des utilisateurs au groupe. 
    
    Vous pouvez sélectionner **Aucun accès**, si vous souhaitez que l'utilisateur ait uniquement accès au service {{site.data.keyword.mon_full_notm}} dans le groupe de ressources.

6. Sélectionnez **{{site.data.keyword.mon_full_notm}}**.
7. Sélectionnez le rôle de plateforme **Editeur**.
8. Cliquez sur **Affecter**.

## Octroi de droits pour gérer des métriques et configurer des alertes dans Sysdig
{: #admin_user_sysdig}

En tant qu'**utilisateur admin** dans Sysdig, vous devez disposer de droits vous permettant d'exécuter les actions suivantes : 

* Ajout de sources de métriques
* Affichage de métriques
* Recherche de métriques
* Filtrage de métriques
* Configuration d'alertes

Par conséquent, vous avez besoin des règles suivantes :

* Une règle IAM pour le service {{site.data.keyword.mon_full_notm}} avec le rôle de plateforme **Editeur**. Cette règle vous permet d'afficher les détails de l'instance de service via la ligne de commande et dans le tableau de bord {{site.data.keyword.cloud_notm}}.
* Une règle IAM pour le service {{site.data.keyword.mon_full_notm}} avec le rôle de service **Responsable**. Cette règle vous permet de surveiller, filtrer et rechercher des métriques, ainsi que de définir des alertes via l'interface utilisateur Web Sysdig.

**Remarque :** En tant qu'administrateur du service, lorsque vous accordez ces règles à un utilisateur, envisagez de le faire dans le cadre d'un groupe de ressources. Une instance {{site.data.keyword.mon_full_notm}} est mise à disposition dans le cadre d'un groupe de ressources. Par conséquent, vous devez accorder des droits d'accès dans le cadre du groupe de ressources.


Procédez comme suit pour affecter à un utilisateur les deux règles pour le service {{site.data.keyword.mon_full_notm}} dans le cadre d'un groupe de ressources : 

1. Dans la barre de menus, cliquez sur **Gérer** &gt; **Accès (IAM)** puis sélectionnez **Utilisateurs**.
2. Sur la ligne de l'utilisateur auquel vous voulez affecter un accès, sélectionnez le menu **Actions**, puis cliquez sur **Affecter un accès**.
3. Sélectionnez **Affecter l'accès au sein d'un groupe de ressources**.
4. Sélectionnez un groupe de ressources.
5. Si aucun rôle n'a encore été accordé à l'utilisateur pour le groupe de ressources sélectionné, choisissez-en un pour la zone **Affecter l'accès à un groupe de ressources**. 

    Selon le rôle que vous sélectionnez, l'utilisateur peut afficher le groupe de ressources sur son tableau de bord, modifier le nom du groupe de ressources, ou gérer l'accès des utilisateurs au groupe. 
    
    Vous pouvez sélectionner **Aucun accès**, si vous souhaitez que l'utilisateur ait uniquement accès au service {{site.data.keyword.mon_full_notm}} dans le groupe de ressources.

6. Sélectionnez **{{site.data.keyword.mon_full_notm}}**.
7. Sélectionnez le rôle de plateforme **Editeur**.
8. Sélectionnez le rôle de service **Responsable**.
8. Cliquez sur **Affecter**.

## Octroi de droits à un utilisateur pour afficher des métriques dans Sysdig
{: #user_sysdig}

En tant qu'**utilisateur**, **auditeur** ou **développeur**, vous aurez peut-être besoin de droits pour exécuter les actions suivantes : 

* Affichage de métriques
* Recherche de métriques
* Filtrage de métriques

Par conséquent, vous avez besoin des règles suivantes :

* Une règle IAM pour le service {{site.data.keyword.mon_full_notm}} avec le rôle de plateforme **Afficheur**. Cette règle vous permet d'afficher les détails de l'instance de service via la ligne de commande et dans le tableau de bord {{site.data.keyword.cloud_notm}}.
* Une règle IAM pour le service {{site.data.keyword.mon_full_notm}} avec le rôle de service **Auteur**. Cette règle vous permet d'afficher, de filtrer et de rechercher des métriques via l'interface utilisateur Web Sysdig.

**Remarque :** En tant qu'administrateur du service, lorsque vous accordez ces règles à un utilisateur, envisagez de le faire dans le cadre d'un groupe de ressources. Une instance {{site.data.keyword.mon_full_notm}} est mise à disposition dans le cadre d'un groupe de ressources. Par conséquent, vous devez accorder des droits d'accès dans le cadre du groupe de ressources.

Procédez comme suit pour affecter à un utilisateur les deux règles pour le service {{site.data.keyword.mon_full_notm}} dans le cadre d'un groupe de ressources : 

1. Dans la barre de menus, cliquez sur **Gérer** &gt; **Accès (IAM)** puis sélectionnez **Utilisateurs**.
2. Sur la ligne de l'utilisateur auquel vous voulez affecter un accès, sélectionnez le menu **Actions**, puis cliquez sur **Affecter un accès**.
3. Sélectionnez **Affecter l'accès au sein d'un groupe de ressources**.
4. Sélectionnez un groupe de ressources.
5. Si aucun rôle n'a encore été accordé à l'utilisateur pour le groupe de ressources sélectionné, choisissez-en un pour la zone **Affecter l'accès à un groupe de ressources**. 

    Selon le rôle que vous sélectionnez, l'utilisateur peut afficher le groupe de ressources sur son tableau de bord, modifier le nom du groupe de ressources, ou gérer l'accès des utilisateurs au groupe. 
    
    Vous pouvez sélectionner **Aucun accès**, si vous souhaitez que l'utilisateur ait uniquement accès au service {{site.data.keyword.mon_full_notm}} dans le groupe de ressources.

6. Sélectionnez **{{site.data.keyword.mon_full_notm}}**.
7. Sélectionnez le rôle de plateforme **Afficheur**.
8. Sélectionnez le rôle de service **Auteur**.
8. Cliquez sur **Affecter**.

