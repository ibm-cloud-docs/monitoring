---

copyright:
  years:  2018, 2024
lastupdated: "2024-10-09"

keywords:

subcollection: monitoring

content-type: tutorial
services: monitoring
account-plan: lite
completion-time: 1h

---

{{site.data.keyword.attribute-definition-list}}


# Monitoring a Windows environment
{: #windows}
{: toc-content-type="tutorial"}
{: toc-services="monitoring"}
{: toc-completion-time="1h"}

The standard monitoring agent cannot be installed on a Windows platform. To monitor a Windows system with {{site.data.keyword.mon_full_notm}} use the Windows Prometheus Bundle to collect the metrics from a Windows system.
{: shortdesc}

The Windows Prometheus Bundle is a comprehensive package that installs and configures a [Prometheus Agent](https://prometheus.io/blog/2021/11/16/agent/){: external} and the [Windows Exporter](https://github.com/prometheus-community/windows_exporter){: external} allowing you to send metrics to your {{site.data.keyword.mon_full_notm}} instance.​

Complete the following steps to configure a Windows system to send metrics to a {{site.data.keyword.mon_short}} instance by downloading and using the installer.

You can also install the Windows Prometheus Bundle using the command line. See [Installing using a command line](/docs/monitoring?topic=monitoring-agent_windows#win_config_cli) for more information.
{: tip}

## Configure the Windows Prometheus Bundle
{: #windows_step1}
{: step}

The Windows Prometheus Bundle provides an installation wizard that installs the required agent and Prometheus Windows exporter Windows service and allows you to select your choice of [collectors.](https://github.com/prometheus-community/windows_exporter/tree/v0.20.0#collectors){: external}

If you accept the defaults when installing using the wizard, the following collectors will be enabled:

| Collector | Description |
| -------------- | ---------------- |
| `cpu` | CPU metrics |
| `cs` | Computer system metrics |
| `logical_disk` | Disk metrics |
| `os` | Operating System metrics |
| `system` | System metrics |
| `net` |  Network interface metrics |
{: caption="Default collectors" caption-side="bottom"}

All collectors that can be configured can be found in the [Prometheus exporter documentation](https://github.com/prometheus-community/windows_exporter/tree/v0.20.0#collectors){: external}.


Complete the following steps to configure the Windows Prometheus Bundle in your Windows system:

1. Download the Windows Prometheus Bundle binary installer from the [latest project release.](https://github.com/sysdiglabs/Sysdig-Windows-Prometheus-Bundle/releases)

2. Run the installer on your Windows system.

3. Configure the [ingestion endpoints for remote write](/docs/monitoring?topic=monitoring-prometheus_remote_write#prometheus_remote_write_endpoints) and your [Monitor API token](/docs/monitoring?topic=monitoring-api_monitoring_token) in the wizard.

4. Click **Next**.

5. For the *Host Configuration* do not change the port or IP values. Specify any additional [CLI flags](https://github.com/prometheus-community/windows_exporter/tree/v0.20.0#flags){: externl} or remote IP addresses required for your Windows Firewall.

6. Click **Next**.

7. Select the collectors that you want to enable to generate metrics.

   ![Windows Exporter selections](../images/windows_exporters.png "Windows Exporter selections"){: caption="Windows Exporter selections" caption-side="bottom"}

   The most commonly used metrics can be selected. Additional [Windows Exporter](https://github.com/prometheus-community/windows_exporter){: external} metrics can be added as a comma separated list.

8. Metrics in Promethus format can be written by other processes to a file on the system. These metrics can be exported and sent to {{site.data.keyword.mon_full_notm}} by selecting `Prometheus metrics from files` then indicating the directory where the metrics are located.

9. Click **Install** then **Finish** to complete the installation.

## Monitor Windows system metrics
{: #windows_step2}
{: step}

You can use the default dashboard `Windows Host Overview` to view the Windows metrics. This default dashboard is located in the **Dashboards** > **Applications** section. The `Windows Process Overview` dashboard is available when you have `process` metrics enabled. The `Windows Services Overview` dashboard is available when you have `service` metrics enabled. You can also search the **Alerts** > **Library** for `Windows` for available default alerts.

![Example of a Windows metrics dashboard](images/windows_dashboard.png "Example of a Windows metrics dashboard"){: caption="Example of a Windows metrics dashboard" caption-side="bottom"}
