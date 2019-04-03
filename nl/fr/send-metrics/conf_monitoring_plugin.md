---

copyright:
  years: 2017, 2019

lastupdated: "2019-03-06"

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

# Envoi de données à l'aide du plug-in Monitoring (collectd)
{: #conf_monitoring_plugin}

Vous pouvez configurer collectd pour collecter des métriques dans un environnement. Utilisez le plug-in {{site.data.keyword.monitoringshort}} pour envoyer ces métriques vers un domaine d'espace depuis votre environnement. 
{: shortdesc}

La figure suivante offre une vue d'ensemble de l'utilisation du plug-in {{site.data.keyword.monitoringshort}} pour envoyer des métriques au service {{site.data.keyword.monitoringshort}} :

![Vue d'ensemble d'utilisation du plug-in {{site.data.keyword.monitoringshort}} ](images/monitoring_plugin_ov.png "Vue d'ensemble d'utilisation du plug-in {{site.data.keyword.monitoringshort}} ")



## Installation du plug-in Monitoring
{: #install}

A partir d'un terminal, procédez comme suit : 

1. (Prérequis) Installez l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}.

   Pour plus d'informations, voir [Installation de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}.](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#cli_qa)
   
   Si l'interface de ligne de commande est installée, passez à l'étape suivante.
	
2. Connectez-vous à une région, une organisation et un espace dans {{site.data.keyword.Bluemix_notm}}. 

    Pour plus d'informations, voir [Comment se connecter à {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login).

    Par exemple, pour vous connecter à la région Sud des Etats-Unis, exécutez la commande suivante :
	
	```
    ibmcloud login -a https://api.ng.bluemix.net
	ibmcloud target -o MyOrg -s MySpace
    ```
    {: codeblock}

    Suivez les instructions. Entrez vos données d'identification {{site.data.keyword.Bluemix_notm}} et sélectionnez une organisation et un espace.

### Etape 1 : Installation de collectd
{: #collectd}

En tant qu'administrateur, procédez comme suit pour installer collectd :

1.	Connectez-vous en tant que superutilisateur. 

    ```
    sudo -s
    ```
    {: codeblock}

2.	Installez le package NTP (Network Time Protocol) pour synchroniser l'heure des journaux. 

    Par exemple, pour un système Ubuntu, vérifiez si `timedatectl status` affiche *Network time on: yes*. Dans le cas affirmatif, votre système Ubuntu est déjà configuré pour utiliser ntp et vous pouvez sauter cette étape.
    
    ```
    # timedatectl status
    Local time: Mon 2017-06-12 03:01:22 PDT
    Universal time: Mon 2017-06-12 10:01:22 UTC
    RTC time: Mon 2017-06-12 10:01:22
    Time zone: America/Los_Angeles (PDT, -0700)
    Network time on: yes
    NTP synchronized: yes
    RTC in local TZ: no
    ```
    {: screen}
    
    Effectuez les étapes suivantes pour installer ntp dans un système Ubuntu :

    1.	Exécutez la commande suivante pour mettre à jour les packages : 

        ```
        apt-get update
        ```
        {: codeblock}
        
    2.	Exécutez la commande suivante pour installer le package ntp : 

        ```
        apt-get install ntp
        ```
        {: codeblock}
        
    3.	Exécutez la commande suivante pour installer le package ntpdate : 
    
        ```
        apt-get install ntpdate
        ```
        {: codeblock}
        
    4.	Exécutez la commande suivante pour arrêter le service : 
        
        ```
        service ntp stop
        ```
        {: codeblock}
        
    5.	Exécutez la commande suivante pour synchroniser l'horloge système : 
    
        ```
        ntpdate -u 0.ubuntu.pool.ntp.org
        ```
        {: codeblock}
        
        Le résultat confirme que l'heure est réglée, par exemple :
        
        ```
        4 May 19:02:17 ntpdate[5732]: adjust time server 50.116.55.65 offset 0.000685 sec
        ```
        {: screen}
        
    6.	Exécutez la commande suivante pour redémarrer ntpd : 
    
        ```
        service ntp start
        ```
        {: codeblock}
    
        Le résultat confirme que le service est en cours de démarrage.

3. Installez collectd. Exécutez la commande suivante :

    ```
	apt-get install collectd 
	```
	{: codeblock}


### Etape 2 : Installation du plug-in Monitoring
{: #plugin}

Procédez comme suit pour installer le plug-in {{site.data.keyword.monitoringshort}} :

1. 	Connectez-vous en tant que superutilisateur. 

    ```
    sudo -s
    ```
    {: codeblock}
	
2. Ajoutez le référentiel de service {{site.data.keyword.monitoringshort}}. Exécutez la commande suivante :

    ```
    wget -O - https://downloads.opvis.bluemix.net/client/IBM_Logmet_repo_install.sh | bash
    ```
   {: codeblock}
   
3. Installez le plug-in. Exécutez la commande suivante :

    ```
	apt-get install ibmcloud-monitoring
	```
	{: codeblock}


## Configuration du plug-in Monitoring
{: #configure}

Pour configurer le plug-in {{site.data.keyword.monitoringshort}}, procédez comme suit :
	
### Etape 1 : Affectation d'une règle IAM à l'utilisateur
{: #iam_policy}

Pour envoyer des métriques à n'importe quel domaine, votre ID utilisateur doit détenir un rôle IAM doté des droits permettant d'envoyer des métriques au service Monitoring.
 
* Les droits sont définis en affectant une règle IAM à cet utilisateur dans IBM Cloud. 
* Les rôles IAM suivants autorisent un utilisateur à envoyer des métriques : *Administrateur*, *Editeur*, *Opérateur*. 

Pour affecter une règle IAM à un utilisateur, choisissez l'une des méthodes suivantes :

* Via l'interface utilisateur {{site.data.keyword.Bluemix_notm}} : Pour plus d'informations, voir [Affectation d'une règle IAM à un utilisateur via l'interface utilisateur {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-grant_permissions#assign_policy_ui).
* Via la ligne de commande : Pour plus d'informations, voir [Affectation d'une règle IAM à un utilisateur via la ligne de commande](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-grant_permissions#assign_policy_commandline).
 
### Etape 2 : Obtention d'une clé d'API
{: #api_key}
 
Pour envoyer des métriques à un espace, vous devez obtenir une clé d'API permettant de vous authentifier auprès du service {{site.data.keyword.monitoringshort}}.

Pour plus d'informations sur la manière d'obtenir une clé d'API, voir [Obtention d'une clé d'API](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_api_key#auth_api_key).
	
Sur le terminal à partir duquel vous vous êtes connecté à {{site.data.keyword.Bluemix_notm}}, définissez la variable APIKEY pour le jeton.

Par exemple

```
export APIKEY="kjshdgf.....ldkdjdj"
```
{: screen}
	
### Etape 3 : Obtention des informations relatives au noeud final
{: #endpoint}

Pour déterminer le noeud final {{site.data.keyword.monitoringshort}} auquel vous allez envoyer les métriques, reportez-vous à la liste des métriques par région, consultez [Noeuds finaux](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints), et identifiez celui de la région où vous voulez envoyer les métriques.

Sur le terminal à partir duquel vous vous êtes connecté à {{site.data.keyword.Bluemix_notm}}, définissez la variable **METRIC_ENDPOINT**. Par exemple

```
export METRIC_ENDPOINT="metrics.ng.bluemix.net"
```
{: screen}



### Etape 4 : Obtention des informations relatives à l'ID de domaine d'espace 
{: #domain}

Pour obtenir l'ID de domaine d'un espace, [procurez-vous l'identificateur global unique de l'espace](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#space_guid). Définissez ensuite l'ID de domaine comme suit : `s-SpaceID` où SpaceID est l'identificateur global unique de l'espace.

Sur le terminal à partir duquel vous vous êtes connecté à {{site.data.keyword.Bluemix_notm}}, définissez la variable SpaceID :

```
export SpaceID="kjshdgf.....ldkdjdj"
```
{: screen}



### Etape 5 : Exécution du script de configuration
{: #script}

Exécutez le script suivant pour configurer le plug-in {{site.data.keyword.monitoringshort}} pour l'envoi de métriques à un espace :

```
/opt/ibmcloud_monitoring/configure -e $METRIC_ENDPOINT -a $APIKEY -s s-$SpaceID
```
{: codeblock}


Le script ajoute automatiquement la section **Include** dans le fichier collectd.conf principal :

```
<LoadPlugin IBMCloudMonitoring>
   FlushInterval 60
</LoadPlugin>
<Plugin IBMCloudMonitoring>
  <Endpoint "ng">
     Host "metrics.ng.bluemix.net"
     Port 9095
     ApiKey "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
     SkipInternalPrefixForStatsd false
     RateCounter false
     ScopeId "s-cedc73c5-6d55-4193-a9de-378620d6fab5"
  </Endpoint>
</Plugin>
```
{: screen}


### Etape 6 : Redémarrage du démon collectd
{: #restart}

Procédez comme suit :

1. 	Connectez-vous en tant que superutilisateur. 

    ```
    sudo -s
    ```
    {: codeblock}
	
2.  Redémarrez collectd.

   Si le démon collectd a été ajouté en tant que service, exécutez la commande suivante :
	
	```
	service collectd restart
	```
	{: codeblock}

Les métriques activées dans collectd sont celles disponibles pour analyse dans Grafana.


