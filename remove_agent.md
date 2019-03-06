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

# Removing a Sysdig agent
{: #remove_agent}

When you delete an {{site.data.keyword.mon_full_notm}} instance, or if you want to stop collecting metrics from a source, you must uninstall the Sysdig agent.
{:shortdesc}


## Removing a Sysdig agent from a Kubernetes cluster
{: #remove_agent_kube}

Complete the following steps to remove a Sysdig agent from a Kubernetes cluster:

1. Set up the cluster environment. Run the following commands:

    First, get the command to set the environment variable and download the Kubernetes configuration files.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    When the download of the configuration files is finished, a command is displayed that you can use to set the path to the local Kubernetes configuration file as an environment variable.

    Then, copy and paste the command that is displayed in your terminal to set the KUBECONFIG environment variable.

    **Note:** Every time you log in to the {{site.data.keyword.containerlong}} CLI to work with clusters, you must run these commands to set the path to the cluster's configuration file as a session variable. The Kubernetes CLI uses this variable to find a local configuration file and certificates that are necessary to connect with the cluster in {{site.data.keyword.cloud_notm}}.

2. Remove the cluster role binding. Run the following command:

    ```
    kubectl delete clusterrolebinding sysdig-agent
    ```
    {: codeblock}

3. Remove the service account. Run the following command:

    ```
    kubectl delete serviceaccount -n ibm-observe sysdig-agent
    ```
    {: codeblock}

4. Remove the daemonset. Run the following command:

    ```
    kubectl delete daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

5. Remove the secret. Run the following command:

    ```
    kubectl delete secret sysdig-agent -n ibm-observe
    ```
    {: codeblock}




## Removing a Sysdig agent on Linux
{: #remove_agent_linux}

Complete the following steps to remove a Sysdig agent on Linux:

* To uninstall the agent from **Debian and Ubuntu Linux distributions**, run the following command as the **sudo** user from a terminal:

    ```
    sudo apt-get remove draios-agent
    ```
    {: codeblock}

* To uninstall the agent from **RHEL, CentOS, and Fedora Linux distributions**, run the following command as the **sudo** user from a terminal:

    ```
    sudo yum erase draios-agent
    ```
    {: codeblock}


