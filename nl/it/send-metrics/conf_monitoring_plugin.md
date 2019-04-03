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

# Invio dei dati utilizzando il plugin di monitoraggio (collectd)
{: #conf_monitoring_plugin}

Puoi configurare collectd per raccogliere le metriche in un ambiente. Utilizza il plugin {{site.data.keyword.monitoringshort}} per inviare queste metriche a un dominio dello spazio dal tuo ambiente. 
{: shortdesc}

La seguente figura mostra una visualizzazione di alto livello di come utilizzare il plugin {{site.data.keyword.monitoringshort}} per inviare le metriche al servizio {{site.data.keyword.monitoringshort}}:

![Visualizzazione di alto livello di come utilizzare il plugin {{site.data.keyword.monitoringshort}} ](images/monitoring_plugin_ov.png "Visualizzazione di alto livello di come utilizzare il plugin {{site.data.keyword.monitoringshort}} ")



## Installa il plugin di monitoraggio
{: #install}

Da un terminale, completa la seguente procedura: 

1. (Pre-req) Installa la CLI {{site.data.keyword.Bluemix_notm}}.

   Per ulteriori informazioni, vedi [Installazione della CLI {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#cli_qa).
   
   Se la CLI è installata, vai al passo successivo.
	
2. Accedi a una regione, un'organizzazione e uno spazio in {{site.data.keyword.Bluemix_notm}}. 

    Per ulteriori informazioni, consulta [Come accedo a {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login).

    Ad esempio, per accedere alla regione Stati Uniti Sud, esegui il seguente comando:
	
	```
    ibmcloud login -a https://api.ng.bluemix.net
	ibmcloud target -o MyOrg -s MySpace
    ```
    {: codeblock}

    Segui le istruzioni. Immetti le tue credenziali {{site.data.keyword.Bluemix_notm}}, seleziona un'organizzazione e uno spazio.

### Passo 1: installa collectd
{: #collectd}

Come amministratore, completa la seguente procedura per installare collectd:

1.	Accedi come utente root. 

    ```
    sudo -s
    ```
    {: codeblock}

2.	Installa il pacchetto NTP (Network Time Protocol) per sincronizzare l'ora dei log. 

    Ad esempio, per un sistema Ubuntu, verifica se `timedatectl status` visualizza *Network time on: yes*. Se è così, il tuo sistema Ubuntu è già configurato ad utilizzare ntp e puoi saltare questo passo.
    
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
    
    Completa la seguente procedura per installare ntp in un sistema Ubuntu:

    1.	Immetti il seguente comando per aggiornare i pacchetti. 

        ```
        apt-get update
        ```
        {: codeblock}
        
    2.	Immetti il seguente comando per installare il pacchetto ntp. 

        ```
        apt-get install ntp
        ```
        {: codeblock}
        
    3.	Immetti il seguente comando per installare il pacchetto ntpdate. 
    
        ```
        apt-get install ntpdate
        ```
        {: codeblock}
        
    4.	Immetti il seguente comando per arrestare il servizio 
        
        ```
        service ntp stop
        ```
        {: codeblock}
        
    5.	Immetti il seguente comando per sincronizzare l'orologio del sistema. 
    
        ```
        ntpdate -u 0.ubuntu.pool.ntp.org
        ```
        {: codeblock}
        
        Il risultato conferma che l'ora è stata modificata, ad esempio:
        
        ```
        4 May 19:02:17 ntpdate[5732]: adjust time server 50.116.55.65 offset 0.000685 sec
        ```
        {: screen}
        
    6.	Immetti il seguente comando per avviare nuovamente ntpd. 
    
        ```
        service ntp start
        ```
        {: codeblock}
    
        Il risultato conferma che il servizio è in fase di avvio.

3. Installa collectd. Immetti il seguente comando:

    ```
	apt-get install collectd 
	```
	{: codeblock}


### Passo 2: installa il plugin di monitoraggio
{: #plugin}

Completa la seguente procedura per installare il plugin {{site.data.keyword.monitoringshort}}:

1. 	Accedi come utente root. 

    ```
    sudo -s
    ```
    {: codeblock}
	
2. Aggiungi il repository del sevizio {{site.data.keyword.monitoringshort}}. Immetti il seguente comando:

    ```
    wget -O - https://downloads.opvis.bluemix.net/client/IBM_Logmet_repo_install.sh | bash
    ```
   {: codeblock}
   
3. Installa il plugin. Immetti il seguente comando:

    ```
	apt-get install ibmcloud-monitoring
	```
	{: codeblock}


## Configura il plugin di monitoraggio
{: #configure}

Per configurare il plugin {{site.data.keyword.monitoringshort}}, completa la seguente procedura:
	
### Passo 1: assegna una politica IAM all'utente
{: #iam_policy}

Per inviare le metriche a tutti i domini, il tuo ID utente deve avere un ruolo IAM con le autorizzazioni per inviare le metriche al servizio di monitoraggio.
 
* Le autorizzazioni vengono inviate assegnando una politica IAM per tale utente in IBM Cloud. 
* I seguenti ruoli IAM consentono a un utente di inviare le metriche: *Amministratore*, *Editor*, *Operatore*. 

Per assegnare a un utente una politica IAM, scegli uno dei seguenti metodi:

* Tramite la IU {{site.data.keyword.Bluemix_notm}}: per ulteriori informazioni, consulta [Assegnazione a un utente di una politica IAM tramite la IU {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security/assign_policy.html#assign_policy_ui).
* Utilizzando la riga di comando: per ulteriori informazioni, consulta [Assegnazione a un utente di una politica IAM utilizzando la riga di comando](/docs/services/cloud-monitoring/security/assign_policy.html#assign_policy_commandline).
 
### Passo 2: Ottieni una chiave API
{: #api_key}
 
Per inviare le metriche in uno spazio, devi ottenere una chiave API per l'autenticazione con il servizio {{site.data.keyword.monitoringshort}}.

Per ulteriori informazioni su come ottenere una chiave API, consulta [Ottenimento di una chiave API](/docs/services/cloud-monitoring/security/auth_api_key.html#auth_api_key).
	
Dallo stesso terminale a cui hai eseguito l'accesso a {{site.data.keyword.Bluemix_notm}}, configura la variabile APIKEY per il token.

Ad esempio,

```
export APIKEY="kjshdgf.....ldkdjdj"
```
{: screen}
	
### Passo 3: Ottieni le informazioni sull'endpoint
{: #endpoint}

Per determinare l'endpoint {{site.data.keyword.monitoringshort}} a cui stai per inviare le metriche, consulta l'elenco degli endpoint per regione, consulta [Endpoint](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints) e identifica l'endpoint per la regione a cui desideri inviare le metriche.

Dallo stesso terminale a cui hai eseguito l'accesso a {{site.data.keyword.Bluemix_notm}}, configura la variabile **METRIC_ENDPOINT**. Ad esempio,

```
export METRIC_ENDPOINT="metrics.ng.bluemix.net"
```
{: screen}



### Passo 4: Ottieni le informazioni sull'ID del dominio dello spazio 
{: #domain}

Per ottenere l'ID del dominio di uno spazio, [ottieni il GUID dello spazio](/docs/services/cloud-monitoring/qa/cli_qa.html#space_guid). Quindi, configura l'ID del dominio nel seguente modo: `s-SpaceID` dove SpaceID è il GUID dello spazio.

Dallo stesso terminale a cui hai eseguito l'accesso a {{site.data.keyword.Bluemix_notm}}, configura la variabile SpaceID:

```
export SpaceID="kjshdgf.....ldkdjdj"
```
{: screen}



### Passo 5: Esegui lo script di configurazione
{: #script}

Esegui il seguente script per configurare il plugin {{site.data.keyword.monitoringshort}} ad inviare le metriche a uno spazio:

```
/opt/ibmcloud_monitoring/configure -e $METRIC_ENDPOINT -a $APIKEY -s s-$SpaceID
```
{: codeblock}


Lo script aggiunge automaticamente la stanza **Include** nel file collectd.conf principale:

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


### Passo 6: Riavvia il daemon collectd
{: #restart}

Completa la seguente procedura:

1. 	Accedi come utente root. 

    ```
    sudo -s
    ```
    {: codeblock}
	
2.  Riavvia collectd.

   Se il daemon collectd è stato aggiunto come un servizio, immetti il seguente comando:
	
	```
	service collectd restart
	```
	{: codeblock}

Le metriche abilitate in collectd sono quelle disponibili per le analisi in Grafana.


