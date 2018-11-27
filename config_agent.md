---

copyright:
  years: 2018
lastupdated: "2018-12-03"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# Configuring a Sysdig agent
{: #sysdig_config_agent}

After you provision an instance of the IBM Cloud Monitoring with Sysdig service in the {{site.data.keyword.Bluemix}}, you must configure a Sysdig agent in each environment that you want to monitor. The Sysdig agent automatically collects and reports on pre-defined metrics. You can configure which metrics to monitor in each environment.
{:shortdesc}


## Configuring a Sysdig agent on Linux
{: #linux}

Complete the following steps to configure a Sysdig agent on Linux to collect and forward metrics to an instance of the IBM Cloud Monitoring with Sysdig service:

1. Obtain the Sysdig access key. For more information, see [Getting the access key through the {{site.data.keyword.Bluemix_notm}} UI](/docs/services/Monitoring-with-Sysdig/access_key.html#ibm_cloud_ui).

2. Obtain the ingestion URL. For more information, see [Sysdig collector endpoints](/docs/services/Monitoring-with-Sysdig/endpoints.html#sysdig).

3. Deploy the Sysdig agent. Run the following command from a terminal.

    ```
    curl -s https://s3.amazonaws.com/download.draios.com/stable/install-agent | sudo bash -s -- --access_key SYSDIG_ACCESS_KEY --collector COLLECTOR_ENDPOINT --collector_port 6443 --secure false --check_certificate false --tags TAG_DATA --additional_conf 'sysdig_capture_enabled: false'
    ```
    {: codeblock}

    where

    * SYSDIG_ACCESS_KEY is the ingestion key for the instance.

    * COLLECTOR_ENDPOINT is the ingestion URL for the region where the monitoring instance is available.

    * TAG_DATA are comma-separated tags that are formatted as *TAG_NAME:TAG_VALUE*. You can associate one or more tags to your Sysdig agent. For example: *role:serviceX,location:us-south*. Later on, you can use these tags to identify metrics from the environment where the agent is running.

    * Set **sysdig_capture_enabled** to *false* to disable the Sysdig capture feature. By default is set to *true*. For more information, see [Working with captures](/docs/services/Monitoring-with-Sysdig/captures.html#captures).

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
{: #docker}

Complete the following steps to configure a Sysdig agent on a Docker container to collect and forward metrics to an instance of the IBM Cloud Monitoring with Sysdig service:

1. Obtain the Sysdig access key. For more information, see [Getting the access key through the {{site.data.keyword.Bluemix_notm}} UI](/docs/services/Monitoring-with-Sysdig/access_key.html#ibm_cloud_ui).

2. Obtain the ingestion URL. For more information, see [Sysdig collector endpoints](/docs/services/Monitoring-with-Sysdig/endpoints.html#sysdig).

3. Deploy the Sysdig agent. Run the following command:

    ```
    docker run -d --name sysdig-agent --restart always --privileged --net host --pid host -e ACCESS_KEY=SYSDIG_ACCESS_KEY -e COLLECTOR=COLLECTOR_ENDPOINT -e COLLECTOR_PORT=6443 -e SECURE=true -e CHECK_CERTIFICATE=false -e TAGS=TAG_DATA -e ADDITIONAL_CONF="sysdig_capture_enabled: false" -v /var/run/docker.sock:/host/var/run/docker.sock -v /dev:/host/dev -v /proc:/host/proc:ro -v /boot:/host/boot:ro -v /lib/modules:/host/lib/modules:ro -v /usr:/host/usr:ro --shm-size=350m sysdig/agent
    ```
    {: codeblock}

    where

    * SYSDIG_ACCESS_KEY is the ingestion key for the instance.

    * COLLECTOR_ENDPOINT is the ingestion URL for the region where the monitoring instance is available.

    * TAG_DATA are comma-separated tags that are formatted as *TAG_NAME:TAG_VALUE*. You can associate one or more tags to your Sysdig agent. For example: *role:serviceX,location:us-south*. Later on, you can use these tags to identify metrics from the environment where the agent is running.

    * Set **sysdig_capture_enabled** to *false* to disable the Sysdig capture feature. By default is set to *true*. For more information, see [Working with captures](/docs/services/Monitoring-with-Sysdig/captures.html#captures).

    **Note:**  The container runs in detached mode. To see the container’s output, remove *-d*.




## Configuring a Sysdig agent on a Kubernetes cluster by using a script
{: #kube_script}

Complete the following steps to configure a Sysdig agent on a Kubernetes cluster that runs in the {{site.data.keyword.containerlong_notm}}:

1. Obtain the Sysdig access key. For more information, see [Getting the access key through the {{site.data.keyword.Bluemix_notm}} UI](/docs/services/Monitoring-with-Sysdig/access_key.html#ibm_cloud_ui).

2. Obtain the ingestion URL. For more information, see [Sysdig collector endpoints](/docs/services/Monitoring-with-Sysdig/endpoints.html#sysdig).

3. Set up the cluster environment. Run the following commands:

    First, get the command to set the environment variable and download the Kubernetes configuration files.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    When the download of the configuration files is finished, a command is displayed that you can use to set the path to the local Kubernetes configuration file as an environment variable.

    Then, copy and paste the command that is displayed in your terminal to set the KUBECONFIG environment variable.

    **Note:** Every time you log in to the {{site.data.keyword.containerlong}} CLI to work with clusters, you must run these commands to set the path to the cluster's configuration file as a session variable. The Kubernetes CLI uses this variable to find a local configuration file and certificates that are necessary to connect with the cluster in {{site.data.keyword.Bluemix_notm}}.

4. Deploy the Sysdig agent. Run the following command:

    ```
    curl -sL https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/IBMCloud-Kubernetes-Service/install-agent-k8s.sh | bash -s -- -a SYSDIG_ACCESS_KEY -c COLLECTOR_ENDPOINT -t TAG_DATA -ac 'sysdig_capture_enabled: false'
    ```
    {: codeblock}

    where

    * SYSDIG_ACCESS_KEY is the ingestion key for the instance.

    * COLLECTOR_ENDPOINT is the ingestion URL for the region where the monitoring instance is available.

    * TAG_DATA are comma-separated tags that are formatted as *TAG_NAME:TAG_VALUE*. You can associate one or more tags to your Sysdig agent. For example: *role:serviceX,location:us-south*. Later on, you can use these tags to identify metrics from the environment where the agent is running.

    * Set **sysdig_capture_enabled** to *false* to disable the Sysdig capture feature. By default is set to *true*. For more information, see [Working with captures](/docs/services/Monitoring-with-Sysdig/captures.html#captures).



## Configuring a Sysdig agent on a Kubernetes cluster manually
{: #kube_manually}

Complete the following steps to configure a Sysdig agent on a Kubernetes cluster that runs in the {{site.data.keyword.containerlong_notm}}:

1. Obtain the Sysdig access key. For more information, see [Getting the access key through the {{site.data.keyword.Bluemix_notm}} UI](/docs/services/Monitoring-with-Sysdig/access_key.html#ibm_cloud_ui).

2. Obtain the ingestion URL. For more information, see [Sysdig collector endpoints](/docs/services/Monitoring-with-Sysdig/endpoints.html#sysdig).

3. Set up the cluster environment. Run the following commands:

    First, get the command to set the environment variable and download the Kubernetes configuration files.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    When the download of the configuration files is finished, a command is displayed that you can use to set the path to the local Kubernetes configuration file as an environment variable.

    Then, copy and paste the command that is displayed in your terminal to set the KUBECONFIG environment variable.

    **Note:** Every time you log in to the {{site.data.keyword.containerlong}} CLI to work with clusters, you must run these commands to set the path to the cluster's configuration file as a session variable. The Kubernetes CLI uses this variable to find a local configuration file and certificates that are necessary to connect with the cluster in {{site.data.keyword.Bluemix_notm}}.

4. Create a service account called **sysdig-agent** to monitor the kubernetes cluster. Run the following command:

    ```
    kubectl create serviceaccount sysdig-agent
    ```
    {: codeblock}

5. Add a secret to your Kubernetes cluster. Run the following command:

    ```
    kubectl create secret generic sysdig-agent --from-literal=access-key=SYSDIG_ACCESS_KEY
    ```
    {: codeblock}

    The SYSDIG_ACCESS_KEY is the ingestion key for the instance.

    The Kubernetes secret contains the ingestion key which is used to authenticate the Sysdig agent with the IBM Cloud Monitoring with Sysdig service. It is used to open a secure web socket to the ingestion server on the monitoring back-end system.

6. Create a cluster role and cluster role binding. 

    Download the [**sysdig-agent-clusterrole.yaml**](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-agent-clusterrole.yaml).
    
    To add a cluster role, run the following command:
    
    ```
    kubectl apply -f /tmp/sysdig-agent-clusterrole.yaml
    ```
    {: codeblock}

    To add a cluster role binding, run the following command:

    ```
    kubectl create clusterrolebinding sysdig-agent --clusterrole=sysdig-agent --serviceaccount=default:sysdig-agent
    ```
    {: codeblock}

7. Edit the **sysdig-agent-configmap.yaml** and add required parameters for configuring the agent to work in the {{site.data.keyword.Bluemix_notm}}.

    Download the [**sysdig-agent-configmap.yaml**](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-agent-configmap.yaml).

    Use an editor to open the sysdig-agent-configmap.yaml file. Then, add the following params:

    * **collector**: This parameter is used to specify the ingestion URL for the region where the monitoring instance is available. 
    
    * **ssl**: This parameter must be set to *true*.
    
    * **ssl_verfiy_certificate**: This parameter must be set to *true*.
    
    * **new_k8s**: This parameter must be set to *true* to capture kube state metrics.

    * **sysdig_capture_enabled**: This parameter is used to enable or disable the Sysdig capture feature. By default is set to *true*. For more information, see [Working with captures](/docs/services/Monitoring-with-Sysdig/captures.html#captures).

    An example yaml file looks like this:

     ```
     apiVersion: v1
     kind: ConfigMap
     metadata:
       name: sysdig-agent
     data:
       dragent.yaml: 
       tags: linux:ubuntu,dept:dev,local:nyc
       collector: us-south.monitoring.cloud.ibm.com
       ssl: true
       ssl_verify_certificate: false
       new_k8s: true
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




