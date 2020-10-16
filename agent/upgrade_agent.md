---

copyright:
  years:  2018, 2020
lastupdated: "2020-09-15"

keywords: Sysdig, IBM Cloud, monitoring, delete agent

subcollection: Monitoring-with-Sysdig

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

# Upgrading a Sysdig agent
{: #upgrade_agent}

{{site.data.keyword.mon_full_notm}} instance
{:shortdesc}


## Upgrading a Sysdig agent for a standard Kubernetes cluster
{: #update_agent_kube}

Complete the following steps to update a Sysdig agent for a Kubernetes cluster:

1. Set up the cluster environment. Run the following commands:

    First, get the command to set the environment variable and download the Kubernetes configuration files.

    ```
    ibmcloud ks cluster config --cluster <cluster_name_or_ID>
    ```
    {: codeblock}

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

4. Remove the `daemonset`. Run the following command:

    ```
    kubectl delete daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

5. Remove the secret. Run the following command:

    ```
    kubectl delete secret sysdig-agent -n ibm-observe
    ```
    {: codeblock}


## Updating a Sysdig agent that is deployed as a container in a Linux system
{: #update_agent_docker}

Complete the following steps to remove the Sysdig agent that is deployed as a conatiner in a Linux system:

1. Stop the Sysdig agent container. Run the following command:

    ```
    docker stop sysdig-agent
    ```
    {: pre}

2. Remove the Sysdig agent container. Run the following command:

    ```
    docker rm sysdig-agent
    ```
    {: pre}

3. Get the latest version of the Sysdig agent. Run the following command:

    ```
    docker pull sysdig/agent
    ```
    {: pre}

4. Install the agent. [Learn more](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-config_agent#config_agent_docker).



## Updating a Sysdig agent that has been deployed as a service in a Linux system 
{: #update_agent_linux}

Complete the following steps to update a Sysdig agent on Linux:

* To update the agent from **Debian and Ubuntu Linux distributions**, run the following commands as the **sudo** user from a terminal:

    ```
    sudo apt-get update
    ```
    {: pre}

    ```
    sudo apt-get -y install draios-agent
    ```
    {: pre}

* To update the agent from **RHEL, CentOS, and Fedora Linux distributions**, run the following commands as the **sudo** user from a terminal:

    ```
    yum clean expire-cache
    ```
    {: pre}

    ```
    sudo yum -y install draios-agent
    ```
    {: pre}

