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

# Retrait d'un agent Sysdig
{: #remove_agent}

Lorsque vous supprimez une instance {{site.data.keyword.mon_full_notm}}, ou si vous voulez arrêter la collecte de métriques à partir d'une source, vous devez désinstaller l'agent Sysdig.
{:shortdesc}


## Retrait d'un agent Sysdig d'un cluster Kubernetes
{: #remove_agent_kube}

Procédez comme suit pour retirer un agent Sysdig d'un cluster Kubernetes :

1. Configurez l'environnement de cluster. Exécutez les commandes suivantes :

    Lancez d'abord la commande permettant de définir la variable d'environnement et téléchargez les fichiers de configuration Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Une fois les fichiers de configuration téléchargés, une commande s'affiche ; elle vous permet de définir le chemin vers le fichier de configuration Kubernetes local en tant que variable d'environnement.

    Ensuite, copiez et collez la commande qui s'affiche sur votre terminal pour définir la variable d'environnement KUBECONFIG.

    **Remarque :** Chaque fois que vous vous connectez à l'interface CLI {{site.data.keyword.containerlong}} pour utiliser des clusters, vous devez exécuter ces commandes pour définir le chemin d'accès au fichier de configuration du cluster en tant que variable de session. L'interface CLI de Kubernetes utilise cette variable pour localiser un fichier de configuration local et les certificats requis pour connexion au cluster dans {{site.data.keyword.cloud_notm}}.

2. Retirez la liaison de rôle du cluster. Exécutez la commande suivante :

    ```
    kubectl delete clusterrolebinding sysdig-agent
    ```
    {: codeblock}

3. Retirez le compte de service. Exécutez la commande suivante :

    ```
    kubectl delete serviceaccount -n ibm-observe sysdig-agent
    ```
    {: codeblock}

4. Retirez le daemonset. Exécutez la commande suivante :

    ```
    kubectl delete daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

5. Supprimez la valeur confidentielle. Exécutez la commande suivante :

    ```
    kubectl delete secret sysdig-agent -n ibm-observe
    ```
    {: codeblock}




## Retrait d'un agent Sysdig sous Linux
{: #remove_agent_linux}

Procédez comme suit pour retirer un agent Sysdig sous Linux :

* Pour désinstaller l'agent de **distributions Debian et Ubuntu Linux**, exécutez la commande suivante en tant qu'utilisateur **sudo** depuis un terminal :

    ```
    sudo apt-get remove draios-agent
    ```
    {: codeblock}

* Pour désinstaller l'agent de **distributions RHEL, CentOS et Fedora Linux**, exécutez la commande suivante en tant qu'utilisateur **sudo** depuis un terminal :

    ```
    sudo yum erase draios-agent
    ```
    {: codeblock}


