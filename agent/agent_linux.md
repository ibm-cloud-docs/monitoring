---

copyright:
  years:  2018, 2025
lastupdated: "2025-02-27"

keywords:

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}

# Working with the Linux agent
{: #agent_linux}

After you provision an instance of the {{site.data.keyword.mon_full_notm}} service in the {{site.data.keyword.cloud_notm}}, you can deploy the {{site.data.keyword.mon_short}} agent on your Linux hosts to collect data and metrics automatically. You can configure which metrics to monitor in each environment.
{: shortdesc}

You can associate one or more tags to each monitoring agent. Tags are comma-separated values that are formatted as **TAG_NAME:TAG_VALUE**. When you monitor your environment, you can use these tags to identify metrics that are available from an agent. For example, you can include information about the service name and location with all of the metrics that are collected by this agent.
{: tip}

## Prereqs
{: #agent_linux_prereqs}

Check the topic [Tune Agent](https://docs.sysdig.com/en/docs/installation/configuration/sysdig-agent/tune-agent/){: external}

## Deploying the Linux agent by using a script
{: #agent_linux_deploy}

Complete the following steps to configure a monitoring agent on Linux to collect and forward metrics to an instance of the {{site.data.keyword.mon_full_notm}} service:

1. [Obtain the access key](/docs/monitoring?topic=monitoring-access_key#access_key_ibm_cloud_ui).

2. Obtain the public or private ingestion URL. For more information, see [collector endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_ingestion).

3. Install the kernel headers.

    When you install a monitoring agent, the agent uses kernel header files. [Learn more](https://docs.sysdig.com/en/sysdig-secure/install-agent-components/troubleshooting/kernel-header-troubleshooting/){: external}

    Choose a distribution and run the following command for that distribution.

    For Debian and Ubuntu Linux distributions, run the following command:

    ```text
    apt-get -y install linux-headers-$(uname -r)
    ```
    {: pre}

    For RHEL, CentOS, and Fedora Linux distributions, run the following command:

    ```text
    yum -y install kernel-devel-$(uname -r)
    ```
    {: pre}

4. Deploy the monitoring agent. Run the following command from a terminal.

    ```text
    curl -sL https://ibm.biz/install-sysdig-agent | sudo bash -s -- --access_key MONITORING_ACCESS_KEY --collector COLLECTOR_ENDPOINT --collector_port 6443  --tags TAG_DATA --additional_conf 'sysdig_capture_enabled: false\nfeature:\n    mode: monitor_light'
    ```
    {: pre}

    Where

    * MONITORING_ACCESS_KEY is the ingestion key for the instance.

    * COLLECTOR_ENDPOINT is the public or private ingestion URL for the region where the monitoring instance is available. To get an endpoint, see [Collector endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_ingestion).

    * TAG_DATA are comma-separated tags that are formatted as *TAG_NAME:TAG_VALUE*. You can associate one or more tags to your monitoring agent. For example, *role:serviceX,location:us-south*.

    * Set **sysdig_capture_enabled** to *false* to disable the capture feature. By default is set to *true*. For more information, see [Working with captures](/docs/monitoring?topic=monitoring-captures#captures).

    To install cURL, run `yum -q -y install curl` for RHEL, CentOS, and Fedora Linux distributions.
    {: tip}

5. Check that the monitoring agent is running. Run the following command:

    ```text
    ps -ef | grep sysdig
    ```
    {: pre}

    To see the latest monitoring agent logs, go to the directory `/opt/draios/logs` and check the log file `draios.log`.

    To look for errors, you can run the following command:

    ```text
    grep error /opt/draios/logs/draios.log
    ```
    {: pre}




## Checking the status of an agent by using the CLI
{: #agent_linux_status}

To check the status of an agent, run the following command:

```text
service dragent status
```
{: pre}


## Checking the version of an agent by using the CLI
{: #agent_linux_version}


To check the version of an agent, run the following command:

```text
/opt/draios/bin/dragent --version
```
{: pre}



## Updating a Linux agent
{: #agent_linux_update}

Complete the following steps to update a monitoring agent on Linux:

* To update the agent from **Debian and Ubuntu Linux distributions**, run the following commands as the **sudo** user from a terminal:

    ```text
    sudo apt-get update
    ```
    {: pre}

    ```text
    sudo apt-get -y install draios-agent
    ```
    {: pre}

* To update the agent from **RHEL, CentOS, and Fedora Linux distributions**, run the following commands as the **sudo** user from a terminal:

    ```text
    yum clean expire-cache
    ```
    {: pre}

    ```text
    sudo yum -y install draios-agent
    ```
    {: pre}


## Removing a monitoring agent that has been deployed as a service in a Linux system
{: #agent_linux_remove}

Complete the following steps to remove a monitoring agent on Linux:

* To uninstall the agent from **Debian and Ubuntu Linux distributions**, run the following command as the **sudo** user from a terminal:

    ```text
    sudo apt-get remove draios-agent
    ```
    {: codeblock}

* To uninstall the agent from **RHEL, CentOS, and Fedora Linux distributions**, run the following command as the **sudo** user from a terminal:

    ```text
    sudo yum erase draios-agent
    ```
    {: codeblock}



## Viewing the logs of an agent
{: #agent_linux_logs}

To see the latest monitoring agent logs, go to the directory `/opt/draios/logs` and check the log file `draios.log`.

To look for errors, you can run the following command:

```text
grep error /opt/draios/logs/draios.log
```
{: pre}


## Verifying the state of the agent
{: #agent_linux_verify}

Check that the monitoring agent is running. Run the following command:

```text
ps -ef | grep sysdig
```
{: pre}
