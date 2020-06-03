---

copyright:
  years:  2018, 2020
lastupdated: "2020-06-03"

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

# Configuring a Sysdig agent
{: #config_agent}

After you provision an instance of the {{site.data.keyword.mon_full_notm}} service in the {{site.data.keyword.cloud_notm}}, you must configure a Sysdig agent in each environment that you want to monitor. The Sysdig agent automatically collects and reports on pre-defined metrics. You can configure which metrics to monitor in each environment.
{:shortdesc}

You can associate one or more tags to each Sysdig agent. Tags are comma-separated values that are formatted as **TAG_NAME:TAG_VALUE**. When you monitor your environment, you can use these tags to identify metrics that are available from an agent. For example, you can include information about the service name and location with all of the metrics that are collected by this agent.
{: tip}

## Configuring a Sysdig agent on Linux
{: #config_agent_linux}

Complete the following steps to configure a Sysdig agent on Linux to collect and forward metrics to an instance of the {{site.data.keyword.mon_full_notm}} service:

1. Obtain the Sysdig access key. For more information, see [Getting the access key through the {{site.data.keyword.cloud_notm}} UI](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-access_key#access_key_ibm_cloud_ui).

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

When you configure a Sysdig agent on a Docker container, you may need to install external linux headers to launch the Sysdig agent correctly. 

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


### Configuring a Sysdig agent on a standard Kubernetes cluster
{: #config_agent_kube_std}

### Configuring a Sysdig agent on a standard Kubernetes cluster by using a script
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

    When the download of the configuration files is finished, a command is displayed that you can use to set the path to the local Kubernetes configuration file as an environment variable.

    Then, copy and paste the command that is displayed in your terminal to set the KUBECONFIG environment variable.

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



### Configuring a Sysdig agent on a standard Kubernetes cluster manually
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

    When the download of the configuration files is finished, a command is displayed that you can use to set the path to the local Kubernetes configuration file as an environment variable.

    Then, copy and paste the command that is displayed in your terminal to set the KUBECONFIG environment variable.

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

    ```
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
    
   
### Configuring a Sysdig agent on an OpenShift cluster
{: #config_agent_kube_os}

### Pre-reqs
{: #config_agent_kube_os_prereqs}

1. Obtain the Sysdig access key. For more information, see [Getting the access key through the {{site.data.keyword.cloud_notm}} UI](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-access_key#access_key_ibm_cloud_ui).

2. Obtain the public or private ingestion URL. For more information, see [Sysdig collector endpoints](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-endpoints#endpoints_ingestion).

3. Log in to the OpenShift cluster. Choose a method to login to an OpenShift cluster. [Learn more about the methods to login](/docs/openshift?topic=openshift-access_cluster#access_automation).


### Configuring a Sysdig agent on an OpenShift cluster by using a script
{: #config_agent_kube_os_script}

In order to use this script, you must have a minimum of `Viewer` and `Manager` IAM permissions assigned for the Kubernetes cluster.
{: tip}

To deploy the Sysdig agent, run the following command:

```
curl -sL https://ibm.biz/install-sysdig-k8s-agent | bash -s -- -a SYSDIG_ACCESS_KEY -c COLLECTOR_ENDPOINT -t TAG_DATA -ac 'sysdig_capture_enabled: false' --openshift
```
{: codeblock}

Where

* SYSDIG_ACCESS_KEY is the ingestion key for the instance.

* COLLECTOR_ENDPOINT is the public or private ingestion URL for the region where the monitoring instance is available. To get an endpoint, see [Collector endpoints](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-endpoints#endpoints_ingestion).

* TAG_DATA are comma-separated tags that are formatted as *TAG_NAME:TAG_VALUE*. You can associate one or more tags to your Sysdig agent. For example: *role:serviceX,location:us-south*. 

* Set **sysdig_capture_enabled** to *false* to disable the Sysdig capture feature. By default is set to *true*. For more information, see [Working with captures](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-captures#captures).



### Configuring a Sysdig agent on an OpenShift cluster manually
{: #config_agent_kube_os_manual}

Complete the following steps:

1. Store your Sysdig access key as a Kubernetes secret.

    You must create a Kubernetes secret to store your Sysdig access key for your service instance. The Sysdig access key is used to open a secure web socket to the Sysdig access server and to authenticate the agent with the {{site.data.keyword.mon_full_notm}} service.

2. Create a project. A project is a namespace in a cluster.

    ```
    oc adm new-project --node-selector='' ibm-observe
    ```
    {: pre}

    Set `--node-selector=''` to disable the default project-wide node selector in your namespace and avoid pod recreates on the nodes that got unselected by the merged node selector.

2. Create the service account **sysdig-agent** in the cluster namespace **ibm-observe**. A service account is in Openshift what a service ID is in {{site.data.keyword.cloud_notm}}. Run the following command:

    ```
    oc create serviceaccount SERVICEACCOUNT_NAME -n PROJECT
    ```
    {: pre}

    Where

    `PROJECT` is the namespace where the Sysdig pods run. Set this value to **ibm-observe**.

    `SERVICEACCOUNT_NAME` is the name of the service account that you use to deploy the Sysdig agent. Set this value to **sysdig-agent**. Notice that if you leave the service account name blank, the default service account is used instead of the service account that you created. 

    ```
    oc create serviceaccount sysdig-agent -n ibm-observe
    ```
    {: pre}

4. Grant the serviceaccount access to the **Privileged SCC** so the service account has permissions to create priviledged Sysdig pods. Run the following command:

    ```
    oc adm policy add-scc-to-user privileged system:serviceaccount:PROJECT:SERVICEACCOUNT_NAME
    ```
    {: pre}

    Where

    `PROJECT` is the namespace where the Sysdig pods run. Set this value to **ibm-observe**.

    `SERVICEACCOUNT_NAME` is the name of the service account that you use to deploy the Sysdig agent. Set this value to **sysdig-agent**.

    ```
    oc adm policy add-scc-to-user privileged system:serviceaccount:ibm-observe:sysdig-agent
    ```
    {: pre}

5. Add a secret. The secret sets the access key that the Sysdig agent uses to send metrics.

    ```
    oc create secret generic sysdig-agent --from-literal=access_key=ACCESS_KEY -n PROJECT 
    ```
    {: pre}

    Where 
    
    `PROJECT` is the namespace where the Sysdig pods run. Set this value to **ibm-observe**.
    
    `ACCESS_KEY` is the ingestion key for the Sysdig instance where you plan to forward and collect the cluster metrics.


## Step 3. Enable virtual routing and forwarding (VRF)
{: #config_agent_os_cluster_step3}

This step is required if you plan to use private endpoints.  

You must enable virtual routing and forwarding (VRF) and connectivity to service endpoints for your account. [Learn more](/docs/account?topic=account-vrf-service-endpoint)

## Step 4. Deploy the Sysdig agent in the cluster
{: #config_agent_os_cluster_step4}

Create a Kubernetes daemon set to deploy the Sysdig agent on every worker node of your Kubernetes cluster. 

The Sysdig agent collects metrics with the extension `*.log` and extensionsless files that are stored in the `/var/log` directory of your pod. By default, metrics are collected from all namespaces, including `kube-system`, and automatically forwarded to the {{site.data.keyword.mon_full_notm}} service.

### Sysdig agent V1
{: #config_agent_kube_cluster_step4_V1}

Choose one of the following commands to install and configure the Sysdig agent version 1:

| Location                  | Command (By using public endpoints)               | 
|--------------------------|----------------------------------------------------|
| `Chennai (in-che)`       | `kubectl create -f https://assets.in-che.logging.cloud.ibm.com/clients/sysdig-agent-ds-os.yaml -n ibm-observe`       |
| `Dallas (us-south)`      | `kubectl create -f https://assets.us-south.logging.cloud.ibm.com/clients/sysdig-agent-ds-os.yaml -n ibm-observe`       |
| `Frankfurt (eu-de)`      | `kubectl create -f https://assets.eu-de.logging.cloud.ibm.com/clients/sysdig-agent-ds-os.yaml -n ibm-observe`         |
| `London (eu-gb)`         | `kubectl create -f https://assets.eu-gb.logging.cloud.ibm.com/clients/sysdig-agent-ds-os.yaml -n ibm-observe`          |
| `Tokyo (jp-tok)`         | `kubectl create -f https://assets.jp-tok.logging.cloud.ibm.com/clients/sysdig-agent-ds-os.yaml -n ibm-observe`       |
| `Seoul (kr-seo)`         | `kubectl create -f https://assets.kr-seo.logging.cloud.ibm.com/clients/sysdig-agent-ds-os.yaml -n ibm-observe` |
| `Sydney (au-syd)`        | `kubectl create -f https://assets.au-syd.logging.cloud.ibm.com/clients/sysdig-agent-ds-os.yaml -n ibm-observe`        |
| `Washington (us-east)`   | `kubectl create -f https://assets.us-east.logging.cloud.ibm.com/clients/sysdig-agent-ds-os.yaml -n ibm-observe`       |
{: caption="Table 1. Commands by location when you use public endpoints" caption-side="top"}
{: #end-api-table-1}
{: tab-title="Command (By using public endpoints)"}
{: tab-group="agent"}
{: class="simple-tab-table"}
{: row-headers}

| Location                  | Command (By using private endpoints)               | 
|--------------------------|----------------------------------------------------|
| `Chennai (in-che)`       | `kubectl create -f https://assets.in-che.logging.cloud.ibm.com/clients/sysdig-agent-ds-os-private.yaml -n ibm-observe`       |
| `Dallas (us-south)`      | `kubectl create -f https://assets.us-south.logging.cloud.ibm.com/clients/sysdig-agent-ds-os-private.yaml -n ibm-observe`      |
| `Frankfurt (eu-de)`      | `kubectl create -f https://assets.eu-de.logging.cloud.ibm.com/clients/sysdig-agent-ds-os-private.yaml -n ibm-observe`          |
| `London (eu-gb)`         | `kubectl create -f https://assets.eu-gb.logging.cloud.ibm.com/clients/sysdig-agent-ds-os-private.yaml -n ibm-observe`       |
| `Tokyo (jp-tok)`         | `kubectl create -f https://assets.jp-tok.logging.cloud.ibm.com/clients/sysdig-agent-ds-os-private.yaml -n ibm-observe`        |
| `Seoul (kr-seo)`         | `kubectl create -f https://assets.kr-seo.logging.cloud.ibm.com/clients/sysdig-agent-ds-os-private.yaml -n ibm-observe` |
| `Sydney (au-syd)`        | `kubectl create -f https://assets.au-syd.logging.cloud.ibm.com/clients/sysdig-agent-ds-os-private.yaml -n ibm-observe`       |
| `Washington (us-east)`   | `kubectl create -f https://assets.us-east.logging.cloud.ibm.com/clients/sysdig-agent-ds-os-private.yaml -n ibm-observe`      |
{: caption="Table 2. Commands by location when you use private endpoints" caption-side="top"}
{: #end-api-table-2}
{: tab-title="Command (By using private endpoints)"}
{: tab-group="agent"}
{: class="simple-tab-table"}
{: row-headers}


## Step 5. Verify that the Sysdig agent is deployed successfully
{: #config_agent_os_cluster_step5}

### Verify the Sysdig agent is deployed successfully
{: #config_agent_os_cluster_step51}

To verify that the Sysdig agent is deployed successfully, run the following command:

1. Target the project where the Sysdig agent is deployed.

    ```
    oc project ibm-observe
    ```
    {: pre}

2. Verify that the `sysdig-agent` pods on each node are in a **Running** status.

    ```
    oc get pods -n PROJECT_NAME
    ```
    {: pre}

    For example, the following command lists all the pods in the namespace *ibm-observe*.

    ```
    oc get pods -n ibm-observe
    ```
    {: pre}


The deployment is successful when you see one or more Sysdig pods.
* **The number of Sysdig pods equals the number of worker nodes in your cluster.**
* All pods must be in a `Running` state.
* *Stdout* and *stderr* are automatically collected and forwarded from all containers. Log data includes application metrics and worker metrics.
* By default, the Sysdig agent pod that runs on a worker collects metrics from all namespaces on that node.

After the agent is configured, you should start seeing metrics from this cluster in the Sysdig web UI. If after a period of time you cannot see metrics, check the agent metrics.

To check the metrics that are generated by a Sysdig agent, run the following command:

```
oc metrics sysdig-agent-<ID>
```
{: pre}

Where *ID* is the ID for a Sysdig agent pod. 

For example, 

```
oc metrics sysdig-agent-xxxkz
```
{: pre}



