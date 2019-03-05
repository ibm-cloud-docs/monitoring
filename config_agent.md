---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, config sysdig agent

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

# Configuring a Sysdig agent
{: #config_agent}

After you provision an instance of the {{site.data.keyword.mon_full_notm}} service in the {{site.data.keyword.cloud_notm}}, you must configure a Sysdig agent in each environment that you want to monitor. The Sysdig agent automatically collects and reports on pre-defined metrics. You can configure which metrics to monitor in each environment.
{:shortdesc}

You can associate one or more tags to each Sysdig agent. Tags are comma-separated values that are formatted as **TAG_NAME:TAG_VALUE**. When you monitor your environment, you can use these tags to identify metrics that are available from an agent. For example, you can include information about the service name and location with all of the metrics that are collected by this agent.
{: tip}

## Configuring a Sysdig agent on Linux
{: #config_agent_linux}

Complete the following steps to configure a Sysdig agent on Linux to collect and forward metrics to an instance of the {{site.data.keyword.mon_full_notm}} service:

1. Obtain the Sysdig access key. For more information, see [Getting the access key through the {{site.data.keyword.cloud_notm}} UI](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui).

2. Obtain the ingestion URL. For more information, see [Sysdig collector endpoints](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion).

3. Deploy the Sysdig agent. Run the following command from a terminal.

    ```
    curl -sL https://ibm.biz/install-sysdig-agent | sudo bash -s -- --access_key SYSDIG_ACCESS_KEY --collector COLLECTOR_ENDPOINT --collector_port 6443 --secure true --tags TAG_DATA --additional_conf 'sysdig_capture_enabled: false'
    ```
    {: codeblock}

    Where

    * SYSDIG_ACCESS_KEY is the ingestion key for the instance.

    * COLLECTOR_ENDPOINT is the ingestion URL for the region where the monitoring instance is available.

    * TAG_DATA are comma-separated tags that are formatted as *TAG_NAME:TAG_VALUE*. You can associate one or more tags to your Sysdig agent. For example: *role:serviceX,location:us-south*. 

    * Set **sysdig_capture_enabled** to *false* to disable the Sysdig capture feature. By default is set to *true*. For more information, see [Working with captures](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures).

    * Set **secure** to *true* to use SSL with the communication.

If the Sysdig agent fails to install correctly, install the kernel headers manually. Choose a distribution and run the command for that distribution. Then, retry the deployment of the Sysdig agent.

* **For Debian and Ubuntu Linux distributions**, run the following command:

    ```
    apt-get -y install linux-headers-$(uname -r)
    ```
    {: codeblock}

* **For RHEL, CentOS, and Fedora Linux distributions**, run the following command:

    ```
    yum -y install kernel-devel-$(uname -r)
    ```
    {: codeblock}


## Configuring a Sysdig agent on a Docker container
{: #config_agent_docker}

Complete the following steps to configure a Sysdig agent on a Docker container to collect and forward metrics to an instance of the {{site.data.keyword.mon_full_notm}} service:

1. Obtain the Sysdig access key. For more information, see [Getting the access key through the {{site.data.keyword.cloud_notm}} UI](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui).

2. Obtain the ingestion URL. For more information, see [Sysdig collector endpoints](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion).

3. Deploy the Sysdig agent. Run the following command:

    ```
    docker run -d --name sysdig-agent --restart always --privileged --net host --pid host -e ACCESS_KEY=SYSDIG_ACCESS_KEY -e COLLECTOR=COLLECTOR_ENDPOINT -e COLLECTOR_PORT=6443 -e SECURE=true -e ADDITIONAL_CONF="sysdig_capture_enabled: false" -e TAGS=TAG_DATA  -v /var/run/docker.sock:/host/var/run/docker.sock -v /dev:/host/dev -v /proc:/host/proc:ro -v /boot:/host/boot:ro -v /lib/modules:/host/lib/modules:ro -v /usr:/host/usr:ro --shm-size=350m sysdig/agent
    ```
    {: codeblock}

    where

    * SYSDIG_ACCESS_KEY is the ingestion key for the instance.

    * COLLECTOR_ENDPOINT is the ingestion URL for the region where the monitoring instance is available.

    * TAG_DATA are comma-separated tags that are formatted as *TAG_NAME:TAG_VALUE*. You can associate one or more tags to your Sysdig agent. For example: *role:serviceX,location:us-south*. 

    * Set **sysdig_capture_enabled** to *false* to disable the Sysdig capture feature. By default is set to *true*. For more information, see [Working with captures](/docs/services/Monitoring-with-Sysdig/captures.html#captures).

    * Set **SECURE** to *true* to use SSL with the communication.

    **Note:**  The container runs in detached mode. To see the container’s output, remove *-d*.




## Configuring a Sysdig agent on a Kubernetes cluster by using a script
{: #config_agent_kube_script}

Complete the following steps to configure a Sysdig agent on a Kubernetes cluster that runs in the {{site.data.keyword.containerlong_notm}}:

1. Obtain the Sysdig access key. For more information, see [Getting the access key through the {{site.data.keyword.cloud_notm}} UI](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui).

2. Obtain the ingestion URL. For more information, see [Sysdig collector endpoints](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion).

3. Set up the cluster environment. Run the following commands:

    First, get the command to set the environment variable and download the Kubernetes configuration files.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    When the download of the configuration files is finished, a command is displayed that you can use to set the path to the local Kubernetes configuration file as an environment variable.

    Then, copy and paste the command that is displayed in your terminal to set the KUBECONFIG environment variable.

    **Note:** Every time you log in to the {{site.data.keyword.containerlong}} CLI to work with clusters, you must run these commands to set the path to the cluster's configuration file as a session variable. The Kubernetes CLI uses this variable to find a local configuration file and certificates that are necessary to connect with the cluster in {{site.data.keyword.cloud_notm}}.

4. Deploy the Sysdig agent. Run the following command:

    ```
    curl -sL https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/IBMCloud-Kubernetes-Service/install-agent-k8s.sh | bash -s -- -a SYSDIG_ACCESS_KEY -c COLLECTOR_ENDPOINT -t TAG_DATA -ac 'sysdig_capture_enabled: false'
    ```
    {: codeblock}

    where

    * SYSDIG_ACCESS_KEY is the ingestion key for the instance.

    * COLLECTOR_ENDPOINT is the ingestion URL for the region where the monitoring instance is available.

    * TAG_DATA are comma-separated tags that are formatted as *TAG_NAME:TAG_VALUE*. You can associate one or more tags to your Sysdig agent. For example: *role:serviceX,location:us-south*. 

    * Set **sysdig_capture_enabled** to *false* to disable the Sysdig capture feature. By default is set to *true*. For more information, see [Working with captures](/docs/services/Monitoring-with-Sysdig/captures.html#captures).



## Configuring a Sysdig agent on a Kubernetes cluster manually
{: #config_agent_kube_manually}

Complete the following steps to configure a Sysdig agent on a Kubernetes cluster that runs in the {{site.data.keyword.containerlong_notm}}:

1. Obtain the Sysdig access key. For more information, see [Getting the access key through the {{site.data.keyword.cloud_notm}} UI](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui).

2. Obtain the ingestion URL. For more information, see [Sysdig collector endpoints](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion).

3. Set up the cluster environment. Run the following commands:

    First, get the command to set the environment variable and download the Kubernetes configuration files.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    When the download of the configuration files is finished, a command is displayed that you can use to set the path to the local Kubernetes configuration file as an environment variable.

    Then, copy and paste the command that is displayed in your terminal to set the KUBECONFIG environment variable.

    **Note:** Every time you log in to the {{site.data.keyword.containerlong}} CLI to work with clusters, you must run these commands to set the path to the cluster's configuration file as a session variable. The Kubernetes CLI uses this variable to find a local configuration file and certificates that are necessary to connect with the cluster in {{site.data.keyword.cloud_notm}}.

4. Create a service account called **sysdig-agent** to monitor the kubernetes cluster. Run the following command:

    ```
    kubectl create serviceaccount sysdig-agent -n ibm-observe
    ```
    {: codeblock}

5. Add a secret to your Kubernetes cluster. Run the following command:

    ```
    kubectl create secret generic sysdig-agent --from-literal=access-key=SYSDIG_ACCESS_KEY -n ibm-observe
    ```
    {: codeblock}

    The SYSDIG_ACCESS_KEY is the ingestion key for the instance.

    The Kubernetes secret contains the ingestion key which is used to authenticate the Sysdig agent with the {{site.data.keyword.mon_full_notm}} service. It is used to open a secure web socket to the ingestion server on the monitoring back-end system.

6. Create a cluster role and cluster role binding. 

    Download the [**sysdig-agent-clusterrole.yaml**](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-agent-clusterrole.yaml).
    
    To add a cluster role, run the following command:
    
    ```
    kubectl apply -f /tmp/sysdig-agent-clusterrole.yaml
    ```
    {: codeblock}

    To add a cluster role binding, run the following command:

    ```
    kubectl create clusterrolebinding sysdig-agent --clusterrole=sysdig-agent --serviceaccount=default:sysdig-agent -n ibm-observe
    ```
    {: codeblock}

7. Edit the **sysdig-agent-configmap.yaml** and add required parameters for configuring the agent to work in the {{site.data.keyword.cloud_notm}}.

    Download the [**sysdig-agent-configmap.yaml**](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-agent-configmap.yaml).

    Use an editor to open the sysdig-agent-configmap.yaml file. Then, add the following parameters:

    * **k8s_cluster_name**: This parameter specifies the cluster name as a metric label. You can use the label *kubernetes.cluster.name* to navigate the Kubernetes dashboards by cluster name and filter out metrics associated with the cluster.

    * **collector**: This parameter specifies the ingestion URL for the region where the monitoring instance is available. 

    * **collector_port**: This parameter indicates the port on which the collector is listening on. It's value must be *6443*.
    
    * **ssl**: This parameter must be set to *true*.
    
    * **ssl_verfiy_certificate**: This parameter must be set to *true*.
    
    * **new_k8s**: This parameter must be set to *true* to capture kube state metrics.

    * **sysdig_capture_enabled**: This parameter enables or disables the Sysdig capture feature. By default is set to *true*. For more information, see [Working with captures](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures).

    An example yaml file looks like this:

    ```
     apiVersion: v1
     kind: ConfigMap
     metadata:
       name: sysdig-agent
     data:
       dragent.yaml: |
       tags: linux:ubuntu,dept:dev,local:nyc
       collector: us-south.monitoring.cloud.ibm.com
       collector_port: 6443
       ssl: true
       new_k8s: true
       k8s_cluster_name: my_cluster_name
       sysdig_capture_enabled: false
    ```
    {: screen}

8. Apply the config map to the cluster. Run the following command:

    ```
    kubectl apply -f sysdig-agent-configmap.yaml
    ```
    {: codeblock}

9. Apply the daemonset to deploy the Sysdig agent to the cluster. Run the following command:

    Download the [**sysdig-agent-daemonset-v2.yaml**](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-agent-daemonset-v2.yaml).

    ```
    kubectl apply -f sysdig-agent-daemonset-v2.yaml
    ```
    {: codeblock}




