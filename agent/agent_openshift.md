---

copyright:
  years:  2018, 2023
lastupdated: "2022-08-08"

keywords: IBM Cloud, Monitoring, agent, sysdig

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

# Working with the {{site.data.keyword.redhat_openshift_notm}} agent
{: #agent_openshift}

After you provision an instance of the {{site.data.keyword.mon_full_notm}} service in the {{site.data.keyword.cloud_notm}}, you can deploy the {{site.data.keyword.mon_short}} agent on your {{site.data.keyword.redhat_openshift_notm}} cluster to collect data and metrics automatically. You can configure which metrics to monitor in each environment.
{: shortdesc}


## Pre-reqs
{: #agent_openshift_prereqs}

- Check the topic [Tuning Sysdig Agent](https://docs.sysdig.com/en/docs/installation/sysdig-agent/troubleshooting-agent-installation/tuning-sysdig-agent/){: external}

- Obtain the access key. For more information, see [Getting the access key](/docs/monitoring?topic=monitoring-access_key).

- Obtain the public or private ingestion URL. For more information, see [collector endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_ingestion).

- Log in to the OpenShift cluster. Choose a method to login to an OpenShift cluster. [Learn more about the methods to login](/docs/openshift?topic=openshift-access_cluster#access_automation).


## Deploying an agent by using a script
{: #agent_openshift_script}

In order to use this script, you must have a minimum of `Viewer` and `Manager` IAM permissions assigned for the OpenShift cluster.
{: tip}


```sh
curl -sL https://ibm.biz/install-sysdig-k8s-agent | bash -s -- -a ACCESS_KEY -c COLLECTOR_ENDPOINT -t TAG_DATA -ac 'sysdig_capture_enabled: false' --nodeanalyzer  --analysismanager https://<COLLECTOR ENDPOINT>/internal/scanning/scanning-analysis-collector --collector_port 6443 --API_ENDPOINT <API-ENDPOINT> --openshift [-as] [-af]
```
{: codeblock}

Where

* ACCESS_KEY is the ingestion key for the instance.

* COLLECTOR_ENDPOINT is the public or private ingestion URL for the region where the instance is available. To get an endpoint, see [Collector endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_ingestion).

* TAG_DATA are comma-separated tags that are formatted as *TAG_NAME:TAG_VALUE*. You can associate one or more tags to your agent. For example: *role:serviceX,location:us-south*.

* Set **sysdig_capture_enabled** to *false* to disable the capture feature. By default is set to *true*. For more information, see [Working with captures](/docs/monitoring?topic=monitoring-captures#captures).

* Add `--imageanalyzer --analysismanager https://<COLLECTOR ENDPOINT>/internal/scanning/scanning-analysis-collector`, if you have images that are hosted in the {{site.data.keyword.registryshort_notm}}, to install the image analyzer component.

* Add `--nodeanalyzer --analysismanager https://<COLLECTOR ENDPOINT>/internal/scanning/scanning-analysis-collector --API_ENDPOINT <API-ENDPOINT>`to install image-analyzer, host-analyzer, and benchmark runner. The `API_ENDPOINT` is needed by the benchmark runner. The `COLLECTOR_ENDPOINT` is needed by the image analyzer.

* Add the option that defines the type of agent that you want to deploy:

    - `-as` to deploy a slim agent. This is the default option. Use this option to reduce the surface area of attack for potential vulnerabilities. When you deploy the agent, you install the agent package as two containers, one running the agent-kmodule and the other ruuning the agent-slim.

    - `-af` to deploy the full agent. When you deploy the agent, the agent runs as a single container or a service.


To deploy the agent by using a public endpoint, run the following command:

```sh
curl -sL https://ibm.biz/install-sysdig-k8s-agent | bash -s -- -a ACCESS_KEY -c ingest.<REGION>.monitoring.cloud.ibm.com -t TAG_DATA -ac 'sysdig_capture_enabled: false' --nodeanalyzer --analysismanager https://ingest.<REGION>.monitoring.cloud.ibm.com/internal/scanning/scanning-analysis-collector --collector_port 6443 --API_ENDPOINT <REGION>.monitoring.cloud.ibm.com --openshift [-as] [-af]
```
{: codeblock}

To deploy the agent by using a private endpoint, run the following command:

```sh
curl -sL https://ibm.biz/install-sysdig-k8s-agent | bash -s -- -a ACCESS_KEY -c ingest.private.<REGION>.monitoring.cloud.ibm.com -t TAG_DATA -ac 'sysdig_capture_enabled: false' --nodeanalyzer --analysismanager https://ingest.private.<REGION>.monitoring.cloud.ibm.com/internal/scanning/scanning-analysis-collector --collector_port 6443 --API_ENDPOINT private.<REGION>.monitoring.cloud.ibm.com --openshift [-as] [-af]
```
{: codeblock}



For example, you can run in the US-South region the following command to deploy the agent:

```sh
curl -sL https://ibm.biz/install-sysdig-k8s-agent | bash -s -- -a APIKEY -c ingest.us-south.monitoring.cloud.ibm.com -ac 'sysdig_capture_enabled: false' --nodeanalyzer  --analysismanager https://ingest.us-south.monitoring.cloud.ibm.com/internal/scanning/scanning-analysis-collector  --collector_port 6443 --api_endpoint us-south.monitoring.cloud.ibm.com --openshift
```
{: screen}




## Removing an agent
{: #agent_openshift_script_remove}

Run the following command to remove an agent:

```sh
curl -sL https://ibm.biz/install-sysdig-k8s-agent | bash -s -- -a ACCESS_KEY -c COLLECTOR_ENDPOINT --openshift --remove
```
{: codeblock}

Where ACCESS_KEY is the ingestion key for the instance.




## Verifying the state of the agent
{: #agent_openshift_verify}

Run the following command to check the status of the agent:

```text
oc get pods -n ibm-observe
```
{: codeblock}

If pods are listed with status running, the agent is running.

If no pods are listed, the agent is not running.

In the event that the pods are not running but you expect the agent to be running, you can run the following command to understand why:

```text
oc get events
```
{: codeblock}
