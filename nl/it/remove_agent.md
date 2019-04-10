---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, delete agent

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

# Rimozione di un agent Sysdig
{: #remove_agent}

Quando elimini un'istanza {{site.data.keyword.mon_full_notm}} o se vuoi arrestare la raccolta delle metriche da un'origine, devi disinstallare l'agent Sysdig.
{:shortdesc}


## Rimozione di un agent Sysdig da un cluster Kubernetes
{: #remove_agent_kube}

Completa la seguente procedura per rimuovere un agent Sysdig da un cluster Kubernetes:

1. Configura l'ambiente cluster. Immetti i seguenti comandi:

    Per prima cosa, richiama il comando per impostare la variabile di ambiente e scarica i file di configurazione Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Quando il download dei file di configurazione è terminato, viene visualizzato un comando che puoi utilizzare per impostare il percorso al file di configurazione di Kubernetes locale come una variabile di ambiente.

    Poi, copia e incolla il comando visualizzato nel tuo terminale per impostare la variabile di ambiente KUBECONFIG.

    **Nota:** ogni volta che accedi alla CLI {{site.data.keyword.containerlong}} per utilizzare i cluster, devi eseguire questi comandi per impostare il percorso al file di configurazione del cluster come una variabile di sessione. La CLI Kubernetes utilizza questa variabile per trovare i certificati e un file di configurazione locale necessari per il collegamento con il cluster in {{site.data.keyword.cloud_notm}}.

2. Rimuovi l'associazione del ruolo cluster. Immetti il seguente comando:

    ```
    kubectl delete clusterrolebinding sysdig-agent
    ```
    {: codeblock}

3. Rimuovi l'account di servizio. Immetti il seguente comando:

    ```
    kubectl delete serviceaccount -n ibm-observe sysdig-agent
    ```
    {: codeblock}

4. Rimuovi il la serie di daemon. Immetti il seguente comando:

    ```
    kubectl delete daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

5. Rimuovi il segreto. Immetti il seguente comando:

    ```
    kubectl delete secret sysdig-agent -n ibm-observe
    ```
    {: codeblock}




## Rimozione di un agent Sysdig su Linux
{: #remove_agent_linux}

Completa la seguente procedura per rimuovere un agent Sysdig su Linux:

* Per disinstallare l'agent dalle **distribuzioni Debian e Ubuntu Linux**, immetti il seguente comando come utente **sudo** da un terminale:

    ```
    sudo apt-get remove draios-agent
    ```
    {: codeblock}

* Per disinstallare l'agent dalle **distribuzioni RHEL, CentOS e Fedora Linux**, immetti il seguente comando come utente **sudo** da un terminale:

    ```
    sudo yum erase draios-agent
    ```
    {: codeblock}


