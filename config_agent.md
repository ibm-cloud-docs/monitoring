---

copyright:
  years: 2018
lastupdated: "2018-09-21"

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

After you provision an instance of the Sysdig service in the {{site.data.keyword.Bluemix}}, you must configure a Sysdig agent in each environment that you want to monitor. The Sysdig agent automatically collects and reports on pre-defined metrics. You can configure which metrics to monitor in each environment.
{:shortdesc}


## Configuring a Sysdig agent on Linux
{: #linux}

Complete the following steps to configure a Sysdig agent on Linux to collect and forward metrics to an instance of the IBM Cloud Monitoring with Sysdig service:

1. Obtain the ingestion key (also known as the Sysdig access key). For more information, see [Getting the ingestion key through the {{site.data.keyword.Bluemix_notm}} UI](/docs/services/Monitoring-with-Sysdig/ingestion_key.html#ibm_cloud_ui).

2. Obtain the ingestion URL. For more information, see [Sysdig collector endpoints](/docs/services/Monitoring-with-Sysdig/endpoints.html#sysdig).

3. Deploy the Sysdig agent. Run the following command from a terminal.

    ```
    curl -s https://s3.amazonaws.com/download.draios.com/stable/install-agent | sudo bash -s -- --access_key SYSDIG_ACCESS_KEY --collector COLLECTOR_ENDPOINT --collector_port 6443 --secure false --check_certificate false --tags TAG_DATA
    ```
    {: codeblock}

    where

    * SYSDIG_ACCESS_KEY is the ingestion key for the instance.

    * COLLECTOR_ENDPOINT is the ingestion URL for the region where the monitoring instance is available.

    * TAG_DATA are comma-separated tags that are formatted as *TAG_NAME:TAG_VALUE*. You can associate one or more tags to your Sysdig agent. For example: *role:serviceX,location:us-south*. Later on, you can use these tags to identify metrics from the environment where the agent is running.


## Configuring a Sysdig agent on a Docker container
{: #docker}

Complete the following steps to configure a Sysdig agent on a Docker container to collect and forward metrics to an instance of the IBM Cloud Monitoring with Sysdig service:

1. Obtain the ingestion key (also known as the Sysdig access key). For more information, see [Getting the ingestion key through the {{site.data.keyword.Bluemix_notm}} UI](/docs/services/Monitoring-with-Sysdig/ingestion_key.html#ibm_cloud_ui).

2. Obtain the ingestion URL. For more information, see [Sysdig collector endpoints](/docs/services/Monitoring-with-Sysdig/endpoints.html#sysdig).

3. Deploy the Sysdig agent. Run the following command:

    ```
    docker run -d --name sysdig-agent --restart always --privileged --net host --pid host -e ACCESS_KEY=SYSDIG_ACCESS_KEY -e COLLECTOR=COLLECTOR_ENDPOINT -e COLLECTOR_PORT=6443 -e SECURE=true -e CHECK_CERTIFICATE=false -e TAGS=TAG_DATA -v /var/run/docker.sock:/host/var/run/docker.sock -v /dev:/host/dev -v /proc:/host/proc:ro -v /boot:/host/boot:ro -v /lib/modules:/host/lib/modules:ro -v /usr:/host/usr:ro --shm-size=350m sysdig/agent
    ```
    {: codeblock}

    where

    * SYSDIG_ACCESS_KEY is the ingestion key for the instance.

    * COLLECTOR_ENDPOINT is the ingestion URL for the region where the monitoring instance is available.

    * TAG_DATA are comma-separated tags that are formatted as *TAG_NAME:TAG_VALUE*. You can associate one or more tags to your Sysdig agent. For example: *role:serviceX,location:us-south*. Later on, you can use these tags to identify metrics from the environment where the agent is running.

    **Note:**  The container runs in detached mode. To see the container’s output, remove *-d*.


If the Sysdig agent fails to install correctly, install the kernel headers manually. Choose a distribution and run the command for that distribution. Then, retry the deployment of the Sysdig agent.

* **For Debian-syle distributions**, run the following command:

    ```
    apt-get -y install linux-headers-$(uname -r)
    ```
    {: codeblock}

* **For RHEL-style distributions**, run the following command:

    ```
    yum -y install kernel-devel-$(uname -r)
    ```
    {: codeblock}



## Configuring a Sysdig agent on a Kubernetes cluster by using a script
{: #kube_script}

Complete the following steps to configure a Sysdig agent on a Kubernetes cluster that runs in the {{site.data.keyword.containerlong_notm}}:

1. Obtain the ingestion key (also known as the Sysdig access key). For more information, see [Getting the ingestion key through the {{site.data.keyword.Bluemix_notm}} UI](/docs/services/Monitoring-with-Sysdig/ingestion_key.html#ibm_cloud_ui).

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
    curl -sL https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/IBMCloud-Kubernetes-Service/install-agent-k8s.sh | bash -s -- -a SYSDIG_ACCESS_KEY -c COLLECTOR_ENDPOINT -t TAG_DATA

    ```
    {: codeblock}

    where

    * SYSDIG_ACCESS_KEY is the ingestion key for the instance.

    * COLLECTOR_ENDPOINT is the ingestion URL for the region where the monitoring instance is available.

    * TAG_DATA are comma-separated tags that are formatted as *TAG_NAME:TAG_VALUE*. You can associate one or more tags to your Sysdig agent. For example: *role:serviceX,location:us-south*. Later on, you can use these tags to identify metrics from the environment where the agent is running.




