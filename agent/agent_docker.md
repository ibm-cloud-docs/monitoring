---

copyright:
  years:  2018, 2022
lastupdated: "2022-08-08"

keywords: IBM Cloud, monitoring, config monitoring agent

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

# Working with the Docker agent
{: #agent_docker}

After you provision an instance of the {{site.data.keyword.mon_full_notm}} service in the {{site.data.keyword.cloud_notm}}, you can deploy the {{site.data.keyword.mon_short}} agent as a Docker container in supported hosts to collect data and metrics automatically. You can configure which metrics to monitor in each environment.
{: shortdesc}

You can associate one or more tags to each monitoring agent. Tags are comma-separated values that are formatted as **TAG_NAME:TAG_VALUE**. When you monitor your environment, you can use these tags to identify metrics that are available from an agent. For example, you can include information about the service name and location with all of the metrics that are collected by this agent.
{: tip}

## Prereqs
{: #agent_docker_prereqs}

Check the topic [Host Requirements for Agent Installation](https://docs.sysdig.com/en/host-requirements-for-agent-installation.html){: external}


## Deploying a monitoring agent as a Docker container
{: #agent_docker_deploy}

When you configure a monitoring agent directly on a Linux host as a standard Docker container, you may need to install external linux headers to launch the monitoring agent correctly. 

For example, you might need to run the following command to install external linux headers:

```text
apt-get -y install linux-headers-$(uname -r)
```
{: pre}

Notice that when you use a MacOS with a container that returns *...-linuxkit* with the command `uname -r`, it is most likely not compatible.

Complete the following steps to configure a monitoring agent on a Docker container to collect and forward metrics to an instance of the {{site.data.keyword.mon_full_notm}} service:

1. Obtain the access key. For more information, see [Getting the access key through the {{site.data.keyword.cloud_notm}} UI](/docs/monitoring?topic=monitoring-access_key#access_key_ibm_cloud_ui).

2. Obtain the public or private ingestion URL. For more information, see [collector endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_ingestion).

3. Deploy the monitoring agent. Run the following command:

    ```text
    docker run -d --name sysdig-agent --restart always --privileged --net host --pid host -e ACCESS_KEY=MONITORING_ACCESS_KEY -e COLLECTOR=COLLECTOR_ENDPOINT -e COLLECTOR_PORT=6443 -e SECURE=true -e ADDITIONAL_CONF="sysdig_capture_enabled: false" -e TAGS=TAG_DATA -e ADDITIONAL_CONF=“log:  { file_priority: error, console_priority: none }” -v /var/run/docker.sock:/host/var/run/docker.sock -v /dev:/host/dev -v /proc:/host/proc:ro -v /boot:/host/boot:ro -v /lib/modules:/host/lib/modules:ro -v /usr:/host/usr:ro --shm-size=350m sysdig/agent
    ```
    {: codeblock}

    Where

    * MONITORING_ACCESS_KEY is the ingestion key for the instance.

    * COLLECTOR_ENDPOINT is the public or private ingestion URL for the region where the monitoring instance is available. To get an endpoint, see [Collector endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_ingestion).

    * TAG_DATA are comma-separated tags that are formatted as *TAG_NAME:TAG_VALUE*. You can associate one or more tags to your monitoring agent. For example, *role:serviceX,location:us-south*. 

    * Set **sysdig_capture_enabled** to *false* to disable the capture feature. By default is set to *true*. For more information, see [Working with captures](/docs/monitoring?topic=monitoring-captures#captures).

    * Set **SECURE** to *true* to use SSL with the communication.

    * Set **log** to define the log level for the agent. By default, the log level that is configired through `file_priority` is set to `info`. Set the `console_priority` to `none` to reduce the container console output. [Learn more](/docs/monitoring?topic=monitoring-agent_log_level).

    The container runs in detached mode. To see the container’s output, remove *-d*.
    {: note}


## Checking the version of an agent by using the CLI
{: #agent_docker_version}

To check the version of an agent, run the following command:

```text
docker exec sysdig-agent /opt/draios/bin/dragent --version
```
{: pre}



## Checking the status of an agent by using the CLI
{: #agent_docker_status}

To check the status of an agent, run the following command:

```text
docker ps | grep sysdig-agent
```
{: pre}


You can run `docker ps -a` to see all the containers that are running.

The list of running containers is displayed. Check that a container with name `sysdig-agent` is listed.


## Viewing the logs of an agent
{: #agent_docker_logs}

To see the agent logs, you can run the following command:

```text
docker logs sysdig-agent
```
{: codeblock}


## Viewing the logs of an agent
{: #agent_docker_ts}

To look for errors, you can run the following command to view the logs:

```text
docker logs sysdig-agent 2>&1 | grep "error"
```
{: codeblock}



## Removing a monitoring agent that is deployed as a container
{: #agent_docker_remove}

Complete the following steps to remove the monitoring agent that is deployed as a container in a Linux system:

1. Stop the monitoring agent container. 

    Run the following command:

    ```text
    docker stop sysdig-agent
    ```
    {: codeblock}

2. Remove references to the monitoring agent container.

    ```text
    docker rm sysdig-agent
    ```
    {: codeblock}

