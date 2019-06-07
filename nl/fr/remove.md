---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, delete instance

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

# Retrait d'une instance
{: #remove}

Vous pouvez retirer une instance du service {{site.data.keyword.mon_full_notm}} à partir de l'interface utilisateur {{site.data.keyword.Bluemix}} ou via la ligne de commande.
{:shortdesc}

Lorsque vous retirez une instance d'{{site.data.keyword.cloud_notm}}, prenez en compte les informations suivantes pour le nettoyage :

1. Notez la liste des sources qui transmettent des métriques à l'instance {{site.data.keyword.mon_full_notm}} que vous souhaitez retirer. Vous devez retirer l'agent Sysdig de chaque source.
2. Supprimez les droits accordés aux utilisateurs qui leur permettant d'utiliser l'instance. 

    Si vous utilisez un groupe d'accès pour gérer les droits d'accès à l'instance, vous devez supprimer le groupe d'accès.

    Si vous utilisez un groupe d'accès pour gérer les droits d'accès aux différentes instances de service, vous devez supprimer les règles accordant les droits d'accès à l'instance que vous souhaitez retirer.
    
    Si vous accordez des règles individuelles à des utilisateurs, vous devez collecter les informations de chaque utilisateur disposant d'un accès à l'instance. Vous devez ensuite retirer une par une les règles liées à l'instance que vous souhaitez supprimer.


Supprimez ensuite l'instance du Tableau de bord {{site.data.keyword.cloud_notm}}.


## Retrait d'une instance via l'interface utilisateur {{site.data.keyword.cloud_notm}}
{: #remove_ui}

Pour retirer une instance {{site.data.keyword.mon_full_notm}} à l'aide de l'interface utilisateur {{site.data.keyword.cloud_notm}}, procédez comme suit :

1. [Connectez-vous à votre compte {{site.data.keyword.cloud_notm}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/login){:new_window}.

	Une fois que vous êtes connecté avec votre ID utilisateur et votre mot de passe, l'interface utilisateur {{site.data.keyword.cloud_notm}} s'ouvre.

2. Sélectionnez **Observabilité**. 

3. Sélectionnez **Surveillance**. La liste des instances s'affiche.

4. Sélectionnez l'instance que vous souhaitez supprimer.

5. Dans le menu *Action*, sélectionnez **Retirer**.


## Retrait d'une instance via l'interface de ligne de commande
{: #remove_cli}

Pour retirer une instance {{site.data.keyword.mon_full_notm}} via la ligne de commande, procédez comme suit :

1. [Prérequis] Installation de l'interface de ligne de commande {{site.data.keyword.cloud_notm}}. Si l'interface de ligne de commande est installée, passez à l'étape suivante.

   Pour plus d'informations, voir [Installation de l'interface de ligne de commande {{site.data.keyword.cloud_notm}}.](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli)

2. Connectez-vous à la région d'{{site.data.keyword.cloud_notm}} où vous souhaitez mettre à disposition l'instance. Exécutez la commande suivante : [`ibmcloud login`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_login)

3. Définissez le groupe de ressources où l'instance est mise à disposition. Exécutez la commande suivante : [`ibmcloud target`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_target)

    Le groupe de ressources `default` est défini par défaut.

4. Retirez l'instance. Exécutez la commande [`ibmcloud resource service-instance-delete`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_instance_delete) :

    ```
    ibmcloud resource service-instance-delete NAME 
    ```
    {: codeblock}

    Où NAME est le nom de l'instance

    Par exemple, pour retirer une instance, exécutez la commande suivante :

    ```
    ibmcloud resource service-instance-delete sysdig-instance-01
    ```
    {: codeblock}
