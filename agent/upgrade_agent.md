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

# Upgrading a monitoring agent
{: #upgrade_agent}

Choose any of the following options to update a monitoring agent:
{:shortdesc}


## Upgrading a monitoring agent for a standard Kubernetes cluster
{: #update_agent_kube}

By default, the monitoring agent has a `RollingUpdate` update strategy. 

```
updateStrategy:
    rollingUpdate:
      maxUnavailable: 1
    type: RollingUpdate
```
{: screen}

When you update the agent's DaemonSet template, old DaemonSet pods are killed, and new DaemonSet pods are created automatically.

The image that is used to create the new pods is the one that is specified in the DaemonSet template. By default, the monitoring agent's image pull policy is configured to always so that it pulls the latest image. The `imagePullPolicy` of the container is set to `Always`. 

```
containers:
    - image: icr.io/ext/sysdig/agent
      imagePullPolicy: Always
      name: sysdig-agent
```
{: screen}

Complete the following steps to update a monitoring agent with a `RollingUpdate` update strategy:

1. Set up the cluster environment. Run the following command:

    First, get the command to set the environment variable and download the Kubernetes configuration files.

    ```
    ibmcloud ks cluster config --cluster <cluster_name_or_ID>
    ```
    {: codeblock}

2. List the DaemonSets that are running in the `ibm-observe` namespace, and verify that the monitoring agent is running in this namespace:

    ```
    kubectl get daemonsets -n ibm-observe
    ```
    {: pre}

    Verify the monitoring agent is running.

3. Check the DaemonSet update strategy:

    ```
    kubectl get ds/sysdig-agent -o go-template='{{.spec.updateStrategy.type}}{{"\n"}}' -n ibm-observe
    ```
    {: pre}

    Verify that is set to `RollingUpdate`.

4. Check the image version that is deployed:

    ```
    kubectl describe ds sysdig-agent -n ibm-observe | grep Image
    ```
    {: pre}

5. Update the image that is configured in the DaemonSet template to the monitoring agent image that you want to use:

    ```
    kubectl set image ds/sysdig-agent sysdig-agent=icr.io/ext/sysdig/agent:IMAGE_VERSION -n ibm-observe
    ```
    {: pre}

    Where `IMAGE_VERSION` is the version of the agent that you want to deploy. To see the the agent versions that are available, see [monitoring agent Release Notes](https://docs.sysdig.com/en/sysdig-agent-release-notes.html){: external}.
    
    For example, to update the agent to version `10.5.1`, you can run the following command:

    ```
    kubectl set image ds/sysdig-agent sysdig-agent=icr.io/ext/sysdig/agent:10.5.1 -n ibm-observe
    ```
    {: pre}

    This step will initiate the update request.

6. Check the update completes.

    ```
    kubectl rollout status ds/sysdig-agent -n ibm-observe
    ```
    {: pre}





## Updating a monitoring agent that is deployed as a container in a Linux system
{: #update_agent_docker}

Complete the following steps to remove the monitoring agent that is deployed as a conatiner in a Linux system:

1. Stop the monitoring agent container. Run the following command:

    ```
    docker stop sysdig-agent
    ```
    {: pre}

2. Remove the monitoring agent container. Run the following command:

    ```
    docker rm sysdig-agent
    ```
    {: pre}

3. Get the latest version of the monitoring agent. Run the following command:

    ```
    docker pull sysdig/agent
    ```
    {: pre}

4. Install the agent. [Learn more](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-config_agent#config_agent_docker).



## Updating a monitoring agent that has been deployed as a service in a Linux system 
{: #update_agent_linux}

Complete the following steps to update a monitoring agent on Linux:

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

