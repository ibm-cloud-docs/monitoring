---

copyright:
  years:  2018, 2022
lastupdated: "2022-08-08"

keywords: 

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

# Working with the Kubernetes agent
{: #agent_Kube}

After you provision an instance of the {{site.data.keyword.mon_full}} service in the {{site.data.keyword.cloud_notm}}, you can deploy the {{site.data.keyword.mon_short}} agent on your cluster to collect data and metrics automatically. You can configure which metrics to monitor in each environment.
{: shortdesc}

You can associate one or more tags to each monitoring agent. Tags are comma-separated values that are formatted as **TAG_NAME:TAG_VALUE**. When you monitor your environment, you can use these tags to identify metrics that are available from an agent. For example, you can include information about the service name and location with all of the metrics that are collected by this agent.
{: tip}


## Prereqs
{: #agent_Kube_prereqs}

- Check the topic [Tuning Sysdig Agent](https://docs.sysdig.com/en/docs/installation/sysdig-agent/troubleshooting-agent-installation/tuning-sysdig-agent/){: external}

- [Get information about Kubernetes monitoring agent images](/docs/monitoring?topic=monitoring-monitoring_agent_image).

- [Install the {{site.data.keyword.cloud_notm}} CLI and plug-ins](/docs/containers?topic=containers-cs_cli_install#cs_cli_install_steps):

    * {{site.data.keyword.cloud_notm}} CLI (`ibmcloud`)
    
    * {{site.data.keyword.containerlong_notm}} plug-in (`ibmcloud ks`)
    
    * {{site.data.keyword.registrylong_notm}} plug-in (`ibmcloud cr`)
    
    * {{site.data.keyword.containerlong_notm}} observability plug-in (`ibmcloud ob`)

- [Install the Kubernetes CLI (kubectl)](/docs/containers?topic=containers-cs_cli_install#kubectl)

    Make sure that the `kubectl` version is compatible with your cluster version. If the `kubectl` version is not compatible, you can get an error such as `kubectl create clusterrolebinding failed!`. You can use `kubectl version --short` to check versions of your cluster and your `kubectl` client.

- If you plan to run the {{site.data.keyword.mon_short}} service, Secure with the node analyzer, or both, check your cluster flavor. You need a minimum `b3c.4x16` flavor for node analyzer to run.

    If you have a cluster with a `free` plan, you do not have sufficient CPU to run the {{site.data.keyword.mon_short}} agent.
    {: note}

- Obtain the access key. For more information, see [Getting the access key](/docs/monitoring?topic=monitoring-access_key#access_key_ibm_cloud_ui).

- Obtain the public or private ingestion URL. For more information, see [collector endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_ingestion).

- Log in to the Kubernetes cluster. Choose a method to login to an Kubernetes cluster. [Learn more about the methods to login](/docs/containers?topic=containers-access_cluster).

- Check public endpoints are enabled if you plan to install image-analyzer, host-analyzer, and benchmark runner. For example, to deploy these components in a cluster in your Virtual Private Cloud (VPC), check that a public gateway is attached to the subnet configured for the cluster.

### Deploying an agent by using a script
{: #agent_Kube_script}

In order to use this script, you must have a minimum of `Viewer` and `Manager` IAM permissions assigned for the Kubernetes cluster.
{: tip}

To deploy the agent, run the following command:

```
curl -sL https://ibm.biz/install-sysdig-k8s-agent | bash -s -- -a ACCESS_KEY -c COLLECTOR_ENDPOINT -t TAG_DATA -ac 'sysdig_capture_enabled: false' --nodeanalyzer  --analysismanager https://<COLLECTOR ENDPOINT>/internal/scanning/scanning-analysis-collector --collector_port 6443 --api_endpoint <API-ENDPOINT> [-as] [-af]
```
{: codeblock}

Where

* ACCESS_KEY is the ingestion key for the instance.

* COLLECTOR_ENDPOINT is the public or private ingestion URL for the region where the instance is available. To get an endpoint, see [Collector endpoints](/docs/sysdig-secure?topic=sysdig-secure-endpoints#endpoints_ingestion).

* TAG_DATA are comma-separated tags that are formatted as *TAG_NAME:TAG_VALUE*. You can associate one or more tags to your agent. For example: *role:serviceX,location:us-south*. 

* Set **sysdig_capture_enabled** to *false* to disable the capture feature. By default is set to *true*. For more information, see [Working with captures](/docs/monitoring?topic=monitoring-captures#captures).

* Add `--imageanalyzer --analysismanager https://<COLLECTOR ENDPOINT>/internal/scanning/scanning-analysis-collector` to install the image analyzer component. Configure this component when you have images that are hosted in the {{site.data.keyword.registryshort_notm}}.

* Add `--nodeanalyzer --analysismanager https://<COLLECTOR ENDPOINT>/internal/scanning/scanning-analysis-collector --api_endpoint <API-ENDPOINT>`to install image-analyzer, host-analyzer, and benchmark runner. The `API_ENDPOINT` is needed by the benchmark runner. The `COLLECTOR_ENDPOINT` is needed by the image analyzer.

* Add the option that defines the type of agent that you want to deploy:

    - `-as` to deploy a slim agent. This is the default option. Use this option to reduce the surface area of attack for potential vulnerabilities. When you deploy the agent, you install the agent package as two containers, one running the agent-kmodule and the other running the agent-slim. 

    - `-af` to deploy the full agent. When you deploy the agent, the agent runs as a single container or a service.


To deploy the agent by using a public endpoint, run the following command:

```
curl -sL https://ibm.biz/install-sysdig-k8s-agent | bash -s -- -a ACCESS_KEY -c ingest.<REGION>.monitoring.cloud.ibm.com -t TAG_DATA -ac 'sysdig_capture_enabled: false' --nodeanalyzer --analysismanager https://ingest.<REGION>.monitoring.cloud.ibm.com/internal/scanning/scanning-analysis-collector --collector_port 6443 --api_endpoint <REGION>.monitoring.cloud.ibm.com [-as] [-af]
```
{: codeblock}api

To deploy the agent by using a private endpoint, run the following command:

```
curl -sL https://ibm.biz/install-sysdig-k8s-agent | bash -s -- -a ACCESS_KEY -c ingest.private.<REGION>.monitoring.cloud.ibm.com -t TAG_DATA -ac 'sysdig_capture_enabled: false' --nodeanalyzer --analysismanager https://ingest.private.<REGION>.monitoring.cloud.ibm.com/internal/scanning/scanning-analysis-collector --collector_port 6443 --api_endpoint private.<REGION>.monitoring.cloud.ibm.com [-as] [-af]
```
{: codeblock}




For example, you can run in the US-South region the following command to deploy the agent:

```
curl -sL https://ibm.biz/install-sysdig-k8s-agent | bash -s -- -a APIKEY -c ingest.us-south.monitoring.cloud.ibm.com -ac 'sysdig_capture_enabled: false' --nodeanalyzer  --analysismanager https://ingest.us-south.monitoring.cloud.ibm.com/internal/scanning/scanning-analysis-collector  --collector_port 6443 --api_endpoint us-south.monitoring.cloud.ibm.com
```
{: screen}



## Removing an agent
{: #agent_kube_script_remove}

Run the following command to remove an agent:

```
curl -sL https://ibm.biz/install-sysdig-k8s-agent | bash -s -- -a ACCESS_KEY -c COLLECTOR_ENDPOINT --remove
```
{: codeblock}

Where ACCESS_KEY is the ingestion key for the instance.



## Verifying the state of the agent
{: #agent_kube_verify}

Run the following command to check the status of the agent:

```text
kubectl get pods -n ibm-observe
```
{: codeblock}

If pods are listed with status running, the agent is running.

If no pods are listed, the agent is not running.

In the event that the pods are not running but you expect the agent to be running, you can run the following command to understand why:

```text
kubectl get events -n ibm-observe
```
{: codeblock}

   

 




