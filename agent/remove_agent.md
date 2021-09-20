---

copyright:
  years:  2018, 2020
lastupdated: "2020-09-15"

keywords: IBM Cloud, monitoring, delete agent

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

# Removing a monitoring agent
{: #remove_agent}

When you delete an {{site.data.keyword.mon_full_notm}} instance, or if you want to stop collecting metrics from a source, you must uninstall the monitoring agent from sources where it was installed as a service. If you deployed a monitoring agent as a container, you must run docker commands to remove the agent.
{: shortdesc}


## Removing a monitoring agent from a standard Kubernetes cluster
{: #remove_agent_kube}

Complete the following steps to remove a monitoring agent from a Kubernetes cluster:

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

## Removing a monitoring agent from an OpenShift cluster
{: #remove_agent_os}

Complete the following steps to remove a monitoring agent from an OpenShift cluster:

1. Delete the `daemonset` by running the following command:

   ```
   oc delete daemonset sysdig-agent -n ibm-observe
   ```
   {: pre}

2. Delete the `secret` by running the following command:

   ```
   oc delete secret sysdig-agent -n ibm-observe
   ```
   {: pre}

3. Delete the `serviceaccount` by running the following command:

   ```
   oc delete serviceaccount -n ibm-observe sysdig-agent
   ```
   {: pre}



## Removing a monitoring agent that is deployed as a container in a Linux system
{: #remove_agent_docker}

Complete the following steps to remove the monitoring agent that is deployed as a conatiner in a Linux system:

1. Stop the monitoring agent container. 

    Run the following command:

    ```
    docker stop sysdig-agent
    ```
    {: codeblock}

2. Remove references to the monitoring agent container.

    ```
    docker rm sysdig-agent
    ```
    {: codeblock}




## Removing a monitoring agent that has been deployed as a service in a Linux system 
{: #remove_agent_linux}

Complete the following steps to remove a monitoring agent on Linux:

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


