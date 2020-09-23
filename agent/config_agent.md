---

copyright:
  years:  2018, 2020
lastupdated: "2020-09-15"

keywords: Sysdig, IBM Cloud, monitoring, config sysdig agent

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
{:external: target="_blank" .external}

# Deploying a Sysdig agent
{: #config_agent}

After you provision an instance of the {{site.data.keyword.mon_full_notm}} service in the {{site.data.keyword.cloud_notm}}, you must configure a Sysdig agent in each environment that you want to monitor. The Sysdig agent automatically collects and reports on pre-defined metrics. You can configure which metrics to monitor in each environment.
{:shortdesc}

You can associate one or more tags to each Sysdig agent. Tags are comma-separated values that are formatted as **TAG_NAME:TAG_VALUE**. When you monitor your environment, you can use these tags to identify metrics that are available from an agent. For example, you can include information about the service name and location with all of the metrics that are collected by this agent.
{: tip}

## Prereqs
{: #config_agent_prereqs}

Check the Sysdig topic [Host Requirements for Agent Installation](https://docs.sysdig.com/en/host-requirements-for-agent-installation.html){: external}

## Deploying a Sysdig agent on Linux manually
{: #config_agent_linux}

Complete the following steps to configure a Sysdig agent on Linux to collect and forward metrics to an instance of the {{site.data.keyword.mon_full_notm}} service:

1. [Obtain the Sysdig access key](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-access_key#access_key_ibm_cloud_ui).

2. Obtain the public or private ingestion URL. For more information, see [Sysdig collector endpoints](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-endpoints#endpoints_ingestion).

3. Deploy the Sysdig agent. Run the following command from a terminal.

    ```
    curl -sL https://ibm.biz/install-sysdig-agent | sudo bash -s -- --access_key SYSDIG_ACCESS_KEY --collector COLLECTOR_ENDPOINT --collector_port 6443 --secure true --tags TAG_DATA --additional_conf 'sysdig_capture_enabled: false'
    ```
    {: codeblock}

    Where

    * SYSDIG_ACCESS_KEY is the ingestion key for the instance.

    * COLLECTOR_ENDPOINT is the public or private ingestion URL for the region where the monitoring instance is available. To get an endpoint, see [Collector endpoints](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-endpoints#endpoints_ingestion).

    * TAG_DATA are comma-separated tags that are formatted as *TAG_NAME:TAG_VALUE*. You can associate one or more tags to your Sysdig agent. For example, *role:serviceX,location:us-south*. 

    * Set **sysdig_capture_enabled** to *false* to disable the Sysdig capture feature. By default is set to *true*. For more information, see [Working with captures](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-captures#captures).

    * Set **secure** to *true* to use SSL with the communication.

4. Check that the Sysdig agent is running. Run the following command:

    ```
    ps -ef | grep sysdig
    ```
    {: codeblock}

    To see the latest Sysdig agent logs, go to the directory `/opt/draios/logs` and check the log file `draios.log`.

    To look for erros, you can run the following command:

    ```
    grep error /opt/draios/logs/draios.log
    ```
    {: codeblock}

If the Sysdig agent fails to install correctly, install the kernel headers manually. Choose a distribution and run the command for that distribution. Then, retry the deployment of the Sysdig agent.

For Debian and Ubuntu Linux distributions, run the following command:

```
apt-get -y install linux-headers-$(uname -r)
```
{: codeblock}

For RHEL, CentOS, and Fedora Linux distributions, run the following command:

```
yum -y install kernel-devel-$(uname -r)
```
{: codeblock}


## Deploying a Sysdig agent as a Docker container
{: #config_agent_docker}

When you configure a Sysdig agent directly on a Linux host as a standard Docker container, you may need to install external linux headers to launch the Sysdig agent correctly. 

For example, you might need to run the following command to install external linux headers:

```
apt-get -y install linux-headers-$(uname -r)
```
{: codeblock}

Notice that when you use a MacOS with a container that returns *...-linuxkit* with the command `uname -r`, it is most likely not compatible.

Complete the following steps to configure a Sysdig agent on a Docker container to collect and forward metrics to an instance of the {{site.data.keyword.mon_full_notm}} service:

1. Obtain the Sysdig access key. For more information, see [Getting the access key through the {{site.data.keyword.cloud_notm}} UI](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-access_key#access_key_ibm_cloud_ui).

2. Obtain the public or private ingestion URL. For more information, see [Sysdig collector endpoints](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-endpoints#endpoints_ingestion).

3. Deploy the Sysdig agent. Run the following command:

    ```
    docker run -d --name sysdig-agent --restart always --privileged --net host --pid host -e ACCESS_KEY=SYSDIG_ACCESS_KEY -e COLLECTOR=COLLECTOR_ENDPOINT -e COLLECTOR_PORT=6443 -e SECURE=true -e ADDITIONAL_CONF="sysdig_capture_enabled: false" -e TAGS=TAG_DATA  -v /var/run/docker.sock:/host/var/run/docker.sock -v /dev:/host/dev -v /proc:/host/proc:ro -v /boot:/host/boot:ro -v /lib/modules:/host/lib/modules:ro -v /usr:/host/usr:ro --shm-size=350m sysdig/agent
    ```
    {: codeblock}

    Where

    * SYSDIG_ACCESS_KEY is the ingestion key for the instance.

    * COLLECTOR_ENDPOINT is the public or private ingestion URL for the region where the monitoring instance is available. To get an endpoint, see [Collector endpoints](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-endpoints#endpoints_ingestion).

    * TAG_DATA are comma-separated tags that are formatted as *TAG_NAME:TAG_VALUE*. You can associate one or more tags to your Sysdig agent. For example, *role:serviceX,location:us-south*. 

    * Set **sysdig_capture_enabled** to *false* to disable the Sysdig capture feature. By default is set to *true*. For more information, see [Working with captures](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-captures#captures).

    * Set **SECURE** to *true* to use SSL with the communication.

    The container runs in detached mode. To see the container’s output, remove *-d*.
    {: note}

4. Check that the Sysdig agent is running. Run the following command:

    ```
    docker ps -a
    ```
    {: codeblock}

    The list of running containers is displayed. Check that a container with name `sysdig-agent` is listed.

    To see the Sysdig agent logs, you can run the following command:

    ```
    docker logs sysdig-agent
    ```
    {: codeblock}

    To look for erros, you can run the following command:

    ```
    docker logs sysdig-agent 2>&1 | grep "error"
    ```
    {: codeblock}



## Deploying a Sysdig agent in a standard Kubernetes environment
{: #config_agent_kube_std}

### Deploying a Sysdig agent in a standard Kubernetes cluster by using a script
{: #config_agent_kube_script}

In order to use this script, you must have a minimum of `Viewer` and `Manager` IAM permissions assigned for the Kubernetes cluster.
{: note}

Complete the following steps to configure a Sysdig agent on a Kubernetes cluster:

1. Obtain the Sysdig access key. For more information, see [Getting the access key through the {{site.data.keyword.cloud_notm}} UI](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-access_key#access_key_ibm_cloud_ui).

2. Obtain the public or private ingestion URL. For more information, see [Sysdig collector endpoints](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-endpoints#endpoints_ingestion).

3. Set up the cluster environment. 

    If the cluster runs in the {{site.data.keyword.containerlong_notm}}, run the following commands:

    First, get the command to set the environment variable and download the Kubernetes configuration files.

    ```
    ibmcloud ks cluster config --cluster <cluster_name_or_ID>
    ```
    {: codeblock}

4. Deploy the Sysdig agent. Run the following command:

    ```
    curl -sL https://ibm.biz/install-sysdig-k8s-agent | bash -s -- -a SYSDIG_ACCESS_KEY -c COLLECTOR_ENDPOINT -t TAG_DATA -ac 'sysdig_capture_enabled: false'
    ```
    {: codeblock}

    Where

    * SYSDIG_ACCESS_KEY is the ingestion key for the instance.

    * COLLECTOR_ENDPOINT is the public or private ingestion URL for the region where the monitoring instance is available. To get an endpoint, see [Collector endpoints](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-endpoints#endpoints_ingestion).

    * TAG_DATA are comma-separated tags that are formatted as *TAG_NAME:TAG_VALUE*. You can associate one or more tags to your Sysdig agent. For example: *role:serviceX,location:us-south*. 

    * Set **sysdig_capture_enabled** to *false* to disable the Sysdig capture feature. By default is set to *true*. For more information, see [Working with captures](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-captures#captures).

Use kubectl version 1.14 or higher.
{: tip}

### Deploying a Sysdig agent in a standard Kubernetes cluster manually
{: #config_agent_kube_manually}

In order to execute all of the commands that follow, you must have a minimum of `Viewer` and `Manager` IAM permissions assigned for the Kubernetes cluster.
{: tip}

Complete the following steps to configure a Sysdig agent on a Kubernetes cluster that runs in the {{site.data.keyword.containerlong_notm}}:

1. Obtain the Sysdig access key. For more information, see [Getting the access key through the {{site.data.keyword.cloud_notm}} UI](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-access_key#access_key_ibm_cloud_ui).

2. Obtain the public or private ingestion URL. For more information, see [Sysdig collector endpoints](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-endpoints#endpoints_ingestion).

3. Set up the cluster environment. Run the following commands:

    First, get the command to set the environment variable and download the Kubernetes configuration files.

    ```
    ibmcloud ks cluster config --cluster <cluster_name_or_ID>
    ```
    {: codeblock}

4. Create the **ibm-observe** namespace.

    ```
    kubectl create namespace ibm-observe
    ```
    {: codeblock}

5. Create a service account called **sysdig-agent** to monitor the kubernetes cluster. Run the following command:

    ```
    kubectl create serviceaccount sysdig-agent -n ibm-observe
    ```
    {: codeblock}

6. Add a secret to your Kubernetes cluster. Run the following command:

    ```
    kubectl create secret generic sysdig-agent --from-literal=access-key=SYSDIG_ACCESS_KEY -n ibm-observe
    ```
    {: codeblock}

    The SYSDIG_ACCESS_KEY is the ingestion key for the instance.

    The Kubernetes secret contains the ingestion key that is used to authenticate the Sysdig agent with the {{site.data.keyword.mon_full_notm}} service. It is used to open a secure web socket to the ingestion server on the monitoring back-end system.

7. Create a cluster role and cluster role binding. 

    Download the [**sysdig-agent-clusterrole.yaml**](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-agent-clusterrole.yaml).
    
    To add a cluster role, run the following command:
    
    ```
    kubectl apply -f /tmp/sysdig-agent-clusterrole.yaml
    ```
    {: codeblock}

    To add a cluster role binding, run the following command:

    ```
    kubectl create clusterrolebinding sysdig-agent --clusterrole=sysdig-agent --serviceaccount=ibm-observe:sysdig-agent -n ibm-observe
    ```
    {: codeblock}

8. Edit the **sysdig-agent-configmap.yaml** and add required parameters for configuring the agent to work in the {{site.data.keyword.cloud_notm}}.

    Download the [**sysdig-agent-configmap.yaml**](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-agent-configmap.yaml).

    Use an editor to open the sysdig-agent-configmap.yaml file. Then, add the following parameters:

    * **k8s_cluster_name**: This parameter specifies the cluster name as a metric label. You can use the label *kubernetes.cluster.name* to navigate the Kubernetes dashboards by cluster name and filter out metrics that are associated with the cluster.

    * **collector**: This parameter specifies the public or private ingestion URL for the region where the monitoring instance is available. 

    * **collector_port**: This parameter indicates the port on which the collector is listening on. The value must be set to *6443*.
    
    * **ssl**: This parameter must be set to *true*.
    
    * **ssl_verfiy_certificate**: This parameter must be set to *true*.
    
    * **new_k8s**: This parameter must be set to *true* to capture kube state metrics.

    * **sysdig_capture_enabled**: This parameter enables or disables the Sysdig capture feature. By default is set to *true*. For more information, see [Working with captures](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-captures#captures).

    An example Yaml file looks as follows:

    ```yaml
     apiVersion: v1
     kind: ConfigMap
     metadata:
       name: sysdig-agent
     data:
       dragent.yaml: |
       tags: env:prod
       collector: ingest.us-south.monitoring.cloud.ibm.com
       collector_port: 6443
       ssl: true
       new_k8s: true
       k8s_cluster_name: my_cluster_name
       sysdig_capture_enabled: false
    ```
    {: screen}

9. Apply the config map to the cluster. Run the following command:

    ```
    kubectl apply -f sysdig-agent-configmap.yaml -n ibm-observe
    ```
    {: codeblock}

10. Apply the daemonset to deploy the Sysdig agent to the cluster. Run the following command:

    **Normal Agent:**

    Download the [**sysdig-agent-daemonset-v2.yaml**](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-agent-daemonset-v2.yaml).

    ```
    kubectl apply -f sysdig-agent-daemonset-v2.yaml -n ibm-observe
    ```
    {: codeblock}
    
     **Slim Agent:**

    Download the [**sysdig-agent-slim-daemonset-v2.yaml**](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-agent-slim-daemonset-v2.yaml).

    ```
    kubectl apply -f sysdig-agent-slim-daemonset-v2.yaml -n ibm-observe
    ```
    {: codeblock}

11. At this point, the Sysdig pods should be starting.  You can run the following command to confirm the pods are running:

    ```
    kubectl get pods -n ibm-observe
    ```
    {: codeblock}

    In the event that the pods are not running, you can run the following command to understand why:

    ```
    kubectl get events
    ```
    {: codeblock}
    
   
## Deploying a Sysdig agent in an OpenShift cluster
{: #config_agent_kube_os}

### Pre-reqs
{: #config_agent_kube_os_prereqs}

1. Obtain the Sysdig access key. For more information, see [Getting the access key through the {{site.data.keyword.cloud_notm}} UI](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-access_key#access_key_ibm_cloud_ui).

2. Obtain the public or private ingestion URL. For more information, see [Sysdig collector endpoints](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-endpoints#endpoints_ingestion).

3. Log in to the OpenShift cluster. Choose a method to login to an OpenShift cluster. [Learn more about the methods to login](/docs/openshift?topic=openshift-access_cluster#access_automation).


### Deploying a Sysdig agent in an OpenShift cluster by using a script
{: #config_agent_kube_os_script}

In order to use this script, you must have a minimum of `Viewer` and `Manager` IAM permissions assigned for the Kubernetes cluster.
{: tip}

To deploy the Sysdig agent, complete the following steps:

1. Set the cluster context by using the `ibmcloud ks` commands. Run the following command:

    ```
    ibmcloud ks cluster config --cluster <cluster_name_or_ID>
    ```
    {: codeblock}

2. Install the agent. Run the following command:

    ```
    curl -sL https://ibm.biz/install-sysdig-k8s-agent | bash -s -- -a SYSDIG_ACCESS_KEY -c COLLECTOR_ENDPOINT -t TAG_DATA -ac 'sysdig_capture_enabled: false' --openshift
    ```
    {: codeblock}

    Where

    * SYSDIG_ACCESS_KEY is the ingestion key for the instance.

    * COLLECTOR_ENDPOINT is the public or private ingestion URL for the region where the monitoring instance is available. To get an endpoint, see [Collector endpoints](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-endpoints#endpoints_ingestion).

    * TAG_DATA are comma-separated tags that are formatted as *TAG_NAME:TAG_VALUE*. You can associate one or more tags to your Sysdig agent. For example: *role:serviceX,location:us-south*. 

    * Set **sysdig_capture_enabled** to *false* to disable the Sysdig capture feature. By default is set to *true*. For more information, see [Working with captures](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-captures#captures).

