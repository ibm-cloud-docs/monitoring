---

copyright:
  years:  2018, 2024
lastupdated: "2024-08-27"

keywords:

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}


# Managing the {{site.data.keyword.mon_full_notm}} Linux agent on a PowerVS workspace
{: #linux_powervs}

After you provision an instance of the {{site.data.keyword.mon_full}} service in the {{site.data.keyword.cloud_notm}}, you can deploy the {{site.data.keyword.mon_short}} agent on your Linux hosts on a PowerVS workspace to automatically collect data and metrics. You can configure which metrics to monitor in each environment.
{: shortdesc}

For information on the available metrics, see [Metrics available in Monitor Light](https://docs.sysdig.com/en/docs/installation/configuration/sysdig-agent/configure-agent-modes/metrics-available-in-monitor-light/){: external}
{: tip}

{{site.data.keyword.mon_full_notm}} provides the following features to protect your standalone Linux hosts on a PowerVS workspace:

* Optimize resource utilization by understanding the capacity of the host and sizing workloads accordingly.

* Reduce risk by leveraging flexible permission management with {{site.data.keyword.cloud_notm}} IAM and custom roles.

* Start with the available default dashboards and alerts.

## Deploying the agent
{: #agent-deploy-linux-powervs-agent}

1. Obtain the access key. For more information, see [Getting the access key.](/docs/monitoring?topic=monitoring-access_key#access_key_ibm_cloud_ui)

2. Obtain the public or private ingestion URL. For more information, see [Collector endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_ingestion).

3. Make sure `dkms` is installed:

   For RHEL or CentOS, run the following commands:

   ```sh
   sudo yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm
   ```
   {: pre}
   
   ```sh
   sudo yum install dkms
   ```
   {: pre}

4. Install the kernel headers. When you install an {{site.data.keyword.mon_full_notm}} agent, the agent uses kernel header files.

   For RHEL or CentOS, run the following command:

   ```sh
   sudo yum -y install kernel-devel-$(uname -r)
   ```
   {: pre}

5. Trust the GPG key and configure the `yum` repository.

   For RHEL or CentOS, run the following commands:

   ```sh
   sudo rpm --import https://download.sysdig.com/DRAIOS-GPG-KEY.public &&
   ```
   {: pre} 
   
   ```sh
   sudo curl -s -o /etc/yum.repos.d/draios.repo https://download.sysdig.com/stable/rpm/draios.repo
   ```
   {: pre}

6. Install, configure, and restart the {{site.data.keyword.mon_full_notm}} agent by running the following commands.

   For RHEL or CentOS, run the following commands.

   * To install the agent package, run:

      ```sh
      sudo yum -y install draios-agent 
      ```
      {: pre}

   * To add the collector endpoint and the access key, run:

      ```sh
      echo customerid: ACCESS_KEY >> /opt/draios/etc/dragent.yaml
      ```
      {: pre}

      ```sh
      echo collector: COLLECTOR_URL >> /opt/draios/etc/dragent.yaml
      ```
      {: pre}

      ```sh
      echo feature: >> /opt/draios/etc/dragent.yaml
      ```
      {: pre}

      ```sh
      echo "  mode: monitor_light" >> /opt/draios/etc/dragent.yaml
      ```
      {: pre}

      ```sh
      sudo systemctl enable dragent powervs-linux-monitoring.md2024-04-26
      ```
      {: pre}

      ```sh
      sudo systemctl start dragent
      ```
      {: pre}

Wait a few seconds to make sure the agent is started and has access to the {{site.data.keyword.mon_full_notm}} data sources. From the {{site.data.keyword.mon_full_notm}} UI you can use **Integrations** > **Data Sources** >> **Sysdig Agents** to verify that the agent is conencted correctly.

You can find more details about the configuration for the {{site.data.keyword.mon_short}} agent [here.](https://docs.sysdig.com/en/docs/installation/configuration/sysdig-agent/understand-the-agent-configuration/){: external}. 
{: tip}

## Updating the agent
{: #linux_powervs_update}

Run the following commands to update an {{site.data.keyword.mon_full_notm}} agent on Linux on a PowerVS workspace.

```sh
sudo yum clean expire-cache
```
{: pre}

```sh
sudo yum -y install draios-agent
```
{: pre}

## Troubleshooting the agent
{: #linux_powervs_ts}

To see the latest {{site.data.keyword.mon_full_notm}} agent logs, go to the `/opt/draios/logs` directory and review the `draios.log` file.

To look for errors, you can run the following command:

```sh
grep -i error /opt/draios/logs/draios.log
```
{: pre}
