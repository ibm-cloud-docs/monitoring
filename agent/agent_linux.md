---

copyright:
  years:  2018, 2022
lastupdated: "2022-08-08"

keywords: IBM Cloud, monitoring, config monitoring agent

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

Check the topic [Host Requirements for Agent Installation](https://docs.sysdig.com/en/host-requirements-for-agent-installation.html){: external}

## Deploying the Linux agent by using a script
{: #agent_linux_deploy}

Complete the following steps to configure a monitoring agent on Linux to collect and forward metrics to an instance of the {{site.data.keyword.mon_full_notm}} service:

1. [Obtain the access key](/docs/monitoring?topic=monitoring-access_key#access_key_ibm_cloud_ui).

2. Obtain the public or private ingestion URL. For more information, see [collector endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_ingestion).

3. Install the kernel headers. 

    When you install a monitoring agent, the agent uses kernel header files. [Learn more](https://docs.sysdig.com/en/agent-install--non-orchestrated.html){: external}

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
    curl -sL https://ibm.biz/install-sysdig-agent | sudo bash -s -- --access_key MONITORING_ACCESS_KEY --collector COLLECTOR_ENDPOINT --collector_port 6443 --secure true --tags TAG_DATA --additional_conf 'sysdig_capture_enabled: false'
    ```
    {: pre}

    Where

    * MONITORING_ACCESS_KEY is the ingestion key for the instance.

    * COLLECTOR_ENDPOINT is the public or private ingestion URL for the region where the monitoring instance is available. To get an endpoint, see [Collector endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_ingestion).

    * TAG_DATA are comma-separated tags that are formatted as *TAG_NAME:TAG_VALUE*. You can associate one or more tags to your monitoring agent. For example, *role:serviceX,location:us-south*. 

    * Set **sysdig_capture_enabled** to *false* to disable the capture feature. By default is set to *true*. For more information, see [Working with captures](/docs/monitoring?topic=monitoring-captures#captures).

    * Set **secure** to *true* to use SSL with the communication.

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
    


## Deploying the agent on a Linux host with no public access
{: #agent_linux_deploy_1}

Follow these steps if your bare metal or VM is running on the {{site.data.keyword.cloud_notm}} private network and does not have access to the public sites.

Complete the following steps to configure a monitoring agent on Linux to collect and forward metrics to an instance of the {{site.data.keyword.mon_full_notm}} service:

1. [Obtain the access key](/docs/monitoring?topic=monitoring-access_key#access_key_ibm_cloud_ui).

2. Obtain the private ingestion URL. For more information, see [collector endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_ingestion).

3. Check that you can reach the repo `http://mirrors.service.networklayer.com/sysdig/`.

    Whether you have a Bare metal or a Classic VSI, by default you get access to the repo. However, if you have attached a firewall such as vyatta to your server, you must allow traffic through to the subnets listed for your data center in [SSL VPN network (on backend/private network)](/hardware-firewall-dedicated?topic=hardware-firewall-dedicated-ibm-cloud-ip-ranges#back-end-private-network). 

    Make sure that you allow all ports, both directions for UDP/TCP/ICMP in your data center.

4. Install the kernel headers. 

    When you install a monitoring agent, the agent uses kernel header files. [Learn more](https://docs.sysdig.com/en/agent-install--non-orchestrated.html){: external}

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

5. Configure the repository.

    For Debian and Ubuntu Linux distributions, run the following commands:

    ```text
    curl -s http://mirrors.service.networklayer.com/sysdig/DRAIOS-GPG-KEY.public | apt-key add -
    ```
    {: pre}    

    ```text
    curl -s -o /etc/apt/sources.list.d/draios.list http://mirrors.service.networklayer.com/sysdig/stable/deb/draios.list
    ```
    {: pre}

    ```text
    apt-get update
    ```
    {: pre}

    For RHEL, CentOS, and Fedora Linux distributions, run the following command:

    ```text
    rpm --import http://mirrors.service.networklayer.com/sysdig/DRAIOS-GPG-KEY.public
    ```
    {: pre}

    ```text
    curl -s -o /etc/yum.repos.d/draios.repo  http://mirrors.service.networklayer.com/sysdig/stable/rpm/draios.repo
    ```
    {: pre}

6. Edit the `draios.repo` file and change the file contents to the following:

   ```text
   [draios]
   name=Draios
   baseurl=http://mirrors.service.networklayer.com/sysdig/stable/rpm/$basearch
   enabled=1
   gpgcheck=1
   gpgkey=http://mirrors.service.networklayer.com/sysdig/DRAIOS-GPG-KEY.public
   #repo_gpgcheck=1
   ```
   {: codeblock}

7. Configure the EPEL repository for RHEL, CentOS, and Fedora Linux distributions.

    Go to the next step if DKMS is available in the distribution.
    {: note}

    To verify if DKMS is available, run the following command:

    For RHEL, CentOS, and Fedora Linux distributions, run the following command:

    ```text
    yum list dkms
    ```
    {: pre}

    To configure the EPEL repository, create a file named `/etc/yum.repos.d/epel.repo` with the following content:

    ```text
    [epel]
    name=Extra Packages for Enterprise Linux 7 - $basearch
    #baseurl=http://download.fedoraproject.org/pub/epel/7/$basearch
    #baseurl=http://mirrors.service.softlayer.com/fedora-epel/7Server/$basearch
    baseurl=http://mirrors.service.softlayer.com/fedora-epel/7/$basearch
    #metalink=https://mirrors.fedoraproject.org/metalink?repo=epel-7&arch=$basearch
    failovermethod=priority
    enabled=1
    gpgcheck=0
    gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-7
    ```
    {: codeblock}

8. Deploy the monitoring agent. 

    This command must be run from a [private endpoint](/docs/monitoring?topic=monitoring-endpoints#endpoints_ingestion_private).
    
    For example:

    ```text
    echo collector: ingest.private.jp-tok.monitoring.cloud.ibm.com >> /opt/draios/etc/dragent.yaml
    ```
    {: pre}

    For Debian and Ubuntu Linux distributions, run the following commands:

    ```text
    apt-get -y install draios-agent
    ```
    {: pre}

    ```text
    echo customerid: MONITORING_ACCESS_KEY >> /opt/draios/etc/dragent.yaml
    ```
    {: pre}

    ```text
    echo tags: TAG_DATA >> /opt/draios/etc/dragent.yaml
    ```
    {: pre}

    ```text
    service dragent restart
    ```
    {: pre}

    For RHEL, CentOS, and Fedora Linux distributions, run the following commands from a terminal:

    ```text
    yum -y install draios-agent
    ```
    {: pre}

    ```text
    echo customerid: MONITORING_ACCESS_KEY >> /opt/draios/etc/dragent.yaml
    ```
    {: pre}

    ```text
    echo tags: TAG_DATA >> /opt/draios/etc/dragent.yaml
    ```
    {: pre}

    ```text
    sudo systemctl enable dragent
    ```
    {: pre}

    ```text
    sudo systemctl start dragent
    ```
    {: pre}

    Where

    * MONITORING_ACCESS_KEY is the ingestion key for the instance.

    * TAG_DATA are comma-separated tags that are formatted as *TAG_NAME:TAG_VALUE*. You can associate one or more tags to your monitoring agent. For example, *role:serviceX,location:us-south*. 

    * Set **sysdig_capture_enabled** to *false* to disable the capture feature. By default is set to *true*. For more information, see [Working with captures](/docs/monitoring?topic=monitoring-captures#captures).

    * Set **secure** to *true* to use SSL with the communication.

9. Check that the monitoring agent is running. Run the following command:

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



