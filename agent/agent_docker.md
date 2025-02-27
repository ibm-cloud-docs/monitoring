---

copyright:
  years:  2018, 2025
lastupdated: "2025-02-27"

keywords:

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

# Working with the Docker agent
{: #agent_docker}

After you provision an instance of the {{site.data.keyword.mon_full_notm}} service in the {{site.data.keyword.cloud_notm}}, you can deploy the {{site.data.keyword.mon_short}} agent as two Docker containers in supported hosts to collect data and metrics automatically. You can configure which metrics to monitor in each environment.
{: shortdesc}

You can associate one or more tags to each monitoring agent. Tags are comma-separated values that are formatted as **TAG_NAME:TAG_VALUE**. When you monitor your environment, you can use these tags to identify metrics that are available from an agent. For example, you can include information about the service name and location with all of the metrics that are collected by this agent.
{: tip}

## Prereqs
{: #agent_docker_prereqs}

Review [Tune Agent](https://docs.sysdig.com/en/docs/installation/sysdig-agent/agent-configuration/tune-agent/){: external}


## Deploying a monitoring agent as two Docker containers
{: #agent_docker_deploy}

When you configure a monitoring agent directly on a Linux host as standard Docker containers, you may need to install external linux headers to launch the monitoring agent correctly.

For example, you might need to run the following command to install external linux headers:

```text
apt-get -y install linux-headers-$(uname -r)
```
{: pre}

Notice that when you use a MacOS with a container that returns *...-linuxkit* with the command `uname -r`, it is most likely not compatible.

Complete the following steps to configure a monitoring agent on two Docker containers to collect and forward metrics to an instance of the {{site.data.keyword.mon_full_notm}} service:

1. Obtain the access key. For more information, see [Getting the access key through the {{site.data.keyword.cloud_notm}} UI](/docs/monitoring?topic=monitoring-access_key#access_key_ibm_cloud_ui).

2. Obtain the public or private ingestion URL. For more information, see [collector endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_ingestion).

3. Deploy the monitoring agent. Run the following command:

    ```sh
    docker run -it --privileged --rm --name sysdig-agent-kmodule \
    -v /usr:/host/usr:ro \
    -v /boot:/host/boot:ro \
    -v /lib/modules:/host/lib/modules \
    quay.io/sysdig/agent-kmodule
    ```
    {: pre}

4. Run the monitoring agent:

   ```sh
   docker run -d --name sysdig-agent \
   --restart always \
   --privileged \
   --net host \
   --pid host \
   -e ACCESS_KEY=[MONITORING_ACCESS_KEY] \
   -e COLLECTOR=[COLLECTOR_ENDPOINT] \
   [-e TAGS=[TAG_DATA]]
   -v /var/run/docker.sock:/host/var/run/docker.sock \
   -v /dev:/host/dev \
   -v /proc:/host/proc:ro \
   -v /boot:/host/boot:ro \
   --shm-size=512m \
   quay.io/sysdig/agent-slim
   ```
   {: pre}

    Where

    * MONITORING_ACCESS_KEY is the ingestion key for the instance.

    * COLLECTOR_ENDPOINT is the public or private ingestion URL for the region where the monitoring instance is available. To get an endpoint, see [Collector endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_ingestion).

    * TAG_DATA are comma-separated tags that are formatted as *TAG_NAME:TAG_VALUE*. You can associate one or more tags to your monitoring agent. For example, *role:serviceX,location:us-south*.

The container runs in detached mode. To see the container’s output, remove *-d*.
{: tip}

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

## Finding agent logs
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



## Updating a Docker agent
{: #agent_docker_update}

Complete the following steps to remove the monitoring agent that is deployed as a container in a Linux system:

1. Stop the monitoring agent container. Run the following command:

    ```text
    docker stop sysdig-agent
    ```
    {: pre}

2. Remove the monitoring agent container. Run the following command:

    ```text
    docker rm sysdig-agent
    ```
    {: pre}

3. Get the latest version of the monitoring agent. Run the following command:

    ```text
    docker pull sysdig/agent
    ```
    {: pre}

4. Install the agent. [Learn more](/docs/monitoring?topic=monitoring-agent_docker#agent_docker_deploy).



## Removing the monitoring agent containers
{: #agent_docker_remove}

Complete the following steps to remove a deployed monitoring agent:

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
