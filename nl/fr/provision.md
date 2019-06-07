---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, provision instance

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

# Mise à disposition d'une instance
{: #provision}

Pour pouvoir surveiller et gérer des métriques avec Sysdig, vous devez mettre à disposition une instance du service dans {{site.data.keyword.cloud_notm}}.
{:shortdesc}


## Mise à disposition d'une instance Sysdig à partir du catalogue
{: #provision_ui}

Pour mettre à disposition une instance de Sysdig à partir du catalogue {{site.data.keyword.cloud_notm}}, procédez comme suit :

1. Connectez-vous à votre compte {{site.data.keyword.cloud_notm}}.

    Cliquez sur le tableau de bord [{{site.data.keyword.cloud_notm}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/login){:new_window} pour lancer le tableau de bord {{site.data.keyword.cloud_notm}}.

	Une fois que vous êtes connecté avec votre ID utilisateur et votre mot de passe, l'interface utilisateur {{site.data.keyword.cloud_notm}} s'ouvre.

2. Cliquez sur **Catalogue**. La liste des services disponibles dans {{site.data.keyword.cloud_notm}} s'affiche.

3. Pour filtrer la liste de services qui s'affiche, sélectionnez la catégorie **Developer Tools**.

4. Cliquez sur la vignette **{{site.data.keyword.mon_full_notm}}**. Le tableau de bord *Observabilité* s'ouvre.

5. Sélectionnez **Créer une instance**. 

6. Sélectionnez un plan de service. Par défaut, le plan **Essai** est défini.

    Pour plus d'informations sur les plans de service, voir [Plans de service](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-pricing_plans#pricing_plans).

7. Sélectionnez un groupe de ressources. Le groupe de ressources **par défaut** est défini automatiquement.

8. Cliquez sur **Créer**.

Après avoir mis à disposition une instance, 

* Le tableau de bord *Observabilité* s'ouvre. 
* Un ID de service est automatiquement créé. Vous pouvez utiliser cet ID de service pour obtenir la clé d'accès Sysdig pour votre instance.

Ensuite, configurez une source de métriques en ajoutant un agent Sysdig. Cet agent est responsable de la collecte et de la transmission des métriques à Sysdig. 



## Mise à disposition d'une instance Sysdig via l'interface de ligne de commande
{: #provision_cli}

Pour mettre à disposition une instance de Sysdig via la ligne de commande, procédez comme suit :

1. [Prérequis] Installation de l'interface de ligne de commande {{site.data.keyword.cloud_notm}}. Si l'interface de ligne de commande est installée, passez à l'étape suivante.

   Pour plus d'informations, voir [Installation de l'interface de ligne de commande {{site.data.keyword.cloud_notm}}.](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli)

2. Connectez-vous à la région d'{{site.data.keyword.cloud_notm}} où vous souhaitez mettre à disposition l'instance. Exécutez la commande suivante : [`ibmcloud login`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_login)

3. Définissez le groupe de ressources où vous souhaitez mettre à disposition l'instance. Exécutez la commande suivante : [`ibmcloud target`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_target)

    Le groupe de ressources `default` est défini par défaut.

4. Créez l'instance Sysdig. Exécutez la commande [`ibmcloud resource service-instance-create`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_instance_create) :

    ```
    ibmcloud resource service-instance-create NAME sysdig-monitor SERVICE_PLAN_NAME LOCATION
    ```
    {: codeblock}

    où

    * NAME est le nom de l'instance Sysdig.
    
    * `sysdig-monitor` est le nom du service {{site.data.keyword.mon_full_notm}} dans {{site.data.keyword.cloud_notm}}.
    
    * SERVICE_PLAN_NAME est le type de plan. Valeurs admises : *lite* et *graduated-tier*.
    
    * LOCATION est la région où l'instance est créée.

    Par exemple, pour mettre à disposition une instance avec le plan payant, exécutez la commande suivante :

    ```
    ibmcloud resource service-instance-create sysdig-instance-01 sysdig-monitor graduated-tier us-south
    ```
    {: screen}

