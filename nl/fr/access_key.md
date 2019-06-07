---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, access key

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

# Gestion des clés d'accès
{: #access_key}

La **clé d'accès** est un jeton que vous devez utiliser pour configurer des agents Sysdig afin qu'ils acheminent correctement les données vers votre instance {{site.data.keyword.mon_full_notm}} dans {{site.data.keyword.cloud_notm}}.   
{:shortdesc}


## Obtention de la clé d'accès via l'interface utilisateur {{site.data.keyword.cloud_notm}}
{: #access_key_ibm_cloud_ui}

Pour obtenir la clé d'accès d'une instance {{site.data.keyword.mon_full_notm}} via l'interface utilisateur {{site.data.keyword.cloud_notm}}, procédez comme suit :

1. Connectez-vous à votre compte {{site.data.keyword.cloud_notm}}.

    Cliquez sur le tableau de bord [{{site.data.keyword.cloud_notm}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/login){:new_window} pour lancer le tableau de bord {{site.data.keyword.cloud_notm}}.

	Une fois que vous êtes connecté avec votre ID utilisateur et votre mot de passe, l'interface utilisateur {{site.data.keyword.cloud_notm}} s'ouvre.

2. Dans le menu de navigation, sélectionnez **Observabilité**. 

3. Sélectionnez **Surveillance**. Le tableau de bord {{site.data.keyword.mon_full_notm}} s'ouvre. Vous pouvez afficher la liste des instances de surveillance disponibles sur {{site.data.keyword.cloud_notm}}.

3. Identifiez l'instance pour laquelle vous voulez obtenir une clé d'accès, puis cliquez sur **Afficher la clé d'accès**.

4. Une fenêtre en incrustation s'ouvre, dans laquelle vous pouvez cliquer sur **Afficher** pour visualiser la clé d'accès.



## Obtention de la clé d'accès via l'interface de ligne de commande
{: #access_key_cli}

Pour obtenir la clé d'accès pour une instance Sysdig via la ligne de commande, procédez comme suit :

1. [Prérequis] Installez l'interface de ligne de commande {{site.data.keyword.cloud_notm}}.

   Pour plus d'informations, voir [Installation de l'interface de ligne de commande {{site.data.keyword.cloud_notm}}.](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli)

   Si l'interface de ligne de commande est installée, passez à l'étape suivante.

2. Connectez-vous à la région d'{{site.data.keyword.cloud_notm}} où l'instance Sysdig s'exécute. Exécutez la commande suivante : [`ibmcloud login`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_login)

3. Définissez le groupe de ressources où l'instance Sysdig s'exécute. Exécutez la commande suivante : [`ibmcloud target`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_target)

    Le groupe de ressources `default` est défini par défaut.

4. Obtenez le nom d'instance. Exécutez la commande suivante : [`ibmcloud resource service-instances`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_instances)

    ```
    ibmcloud resource service-instances
    ```
    {: pre}

5. Obtenez le nom de la clé d'API qui est associée à l'instance Sysdig. Exécutez la commande [`ibmcloud resource service-keys`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_instances) :

    ```
    ibmcloud resource service-keys --instance-name INSTANCE_NAME
    ```
    {: pre}

    où INSTANCE_NAME est le nom de l'instance que vous avez obtenu à l'étape précédente.

6. Obtenez la clé d'accès. Exécutez la commande [`ibmcloud resource service-key`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_key) :

    ```
    ibmcloud resource service-key APIKEY_NAME
    ```
    {: pre}

    où APIKEY_NAME est le nom de la clé d'API.
 
    La sortie générée par cette commande inclut la zone **Sysdig Access Key**, qui contient la clé d'accès pour l'instance.


Par exemple, la commande suivante montre un exemple de sortie d'ID de service :

```
$ ic resource service-key "{{site.data.keyword.mon_full_notm}}-shg-key-admin"
Retrieving service key {{site.data.keyword.mon_full_notm}}-shg-key-admin in resource group Default under account Sample's Account as sample@ibm.com...
OK
                  
Name:          {{site.data.keyword.mon_full_notm}}-shg-key-admin   
ID:            crn:v1:staging:public:sysdig-monitor:us-south:a/1234567891234567891212346461b066:6e2637ff-4548-47a6-bf30-063fbe49760e:resource-key:bb18c701-0dba-4c4e-bda5-74380e41c4bf   
Created At:    Fri Nov  2 13:40:39 UTC 2018   
State:         active   
Credentials:                                      
               iam_role_crn:                crn:v1:bluemix:public:iam::::role:Administrator      
               iam_serviceid_crn:           crn:v1:staging:public:iam-identity::a/1234567891234567891212346461b066::serviceid:ServiceId-88888888-4444-4444-4444-77777777777      
               Sysdig Access Key:           xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx      
               Sysdig Customer Id:          111      
               iam_apikey_description:      Auto generated apikey during resource-key operation for Instance - crn:v1:staging:public:sysdig-monitor:us-south:a/1234567891234567891212346461b066:6e2637ff-4548-47a6-bf30-063fbe49760e::      
               iam_apikey_name:             auto-generated-apikey-bb18c701-0dba-4c4e-bda5-74380e41c4bf      
               Sysdig Collector Endpoint:   ingest.us-south.monitoring.test.cloud.ibm.com      
               Sysdig Endpoint:             https://us-south.monitoring.test.cloud.ibm.com      
               apikey:                      xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx     
                  
Parameters:                      
               role_crn:   crn:v1:bluemix:public:iam::::role:Administrator      
```
{: screen}




## Réinitialisation de la clé d'accès 
{: #access_key_reset}

Si la clé d'accès est compromise ou que vous disposez d'une règle permettant de la renouveler au bout d'un certain nombre de jours, vous pouvez générer une nouvelle clé et supprimer l'ancienne.

Pour renouveler la clé d'accès pour une instance {{site.data.keyword.mon_full_notm}}, procédez comme suit :

1. Lancez l'interface utilisateur Web {{site.data.keyword.mon_full_notm}}. Pour plus d'informations,
voir [Accès à l'interface utilisateur Web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch).

2. A partir du bouton *Sélecteur* dans la barre de navigation, choisissez **Paramètres**.

2. Dans la section relative à la *gestion des mots de passe*, cliquez sur **Réinitialiser votre mot de passe**.

**Remarque :** Une fois que vous avez réinitialisé la clé d'accès Sysdig, vous devez la mettre à jour afin qu'elle indique les sources de journal qui transmettent des métriques à cette instance {{site.data.keyword.mon_full_notm}}.
