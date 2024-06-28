---

copyright:
  years:  2018, 2023
lastupdated: "2023-07-05"

keywords:

subcollection: monitoring

content-type: tutorial
services: monitoring
account-plan: lite
completion-time: 1h

---

{{site.data.keyword.attribute-definition-list}}

# Monitoring a Linux bare metal server
{: #baremetal_linux}
{: toc-content-type="tutorial"}
{: toc-services="monitoring"}
{: toc-completion-time="1h"}

You can monitor a Bare Metal server with {{site.data.keyword.mon_full_notm}} by configuring a monitoring agent in your server. The monitoring agent uses an access key (token) to authenticate with the {{site.data.keyword.mon_full_notm}} instance. The monitoring agent acts as a data collector. It automatically collects metrics. You view metrics via the web-based user interface. You can monitor Bare metals in {{site.data.keyword.cloud_notm}}, on-prem, and in other clouds.
{: shortdesc}

By default, this agent collects core infrastructure and network time series that you can use to monitor the host. For a list of collected metrics, see [Metrics Available for non-orchestrated environments](https://docs.sysdig.com/en/docs/installation/sysdig-agent/agent-configuration/configure-agent-modes/metrics-available-in-monitor-light/).

The {{site.data.keyword.mon_short}} agent automatically collects the following types of system metrics per host:

- `System hosts metrics` provide information about CPU, memory, and storage usage metrics, that you can use to analyze the performance and resource utilization of all your processes.

- `File and File System metrics` provide information about files and file system that you can use to analyze file interactions that occur in your system. For example, you can find information about your open files, bytes going in and out, or the percentage of usage of a given file system.

- `Process metrics` provide information about the processes that run in your servers. For example, you can use these metrics to  explore the number of processes, or get client or server information.

- `Network metrics` provide information about the network. They offer insight to the connections that are established between your applications, containers, and servers. For example, you can find information about the bytes that are being sent or received, or the number of HTTP requests, connections, and latency. In addition, for SQL or MongoDB, the agent collects additional information when it is configured in troubleshooting mode.

Through the {{site.data.keyword.mon_short}} UI, you can analyze data in the *Advisor* tab, the *Explore* tab, and in the *Dashboard* tab. You monitor the data through metric views and dashboards.
{: shortdesc}

Consider the following information when monitoring your data:
* In the *Explorer* tab, you can monitor individual metrics.
* In the *Advisor* tab, you can monitor {{site.data.keyword.redhat_openshift_notm}} or host level metrics.

    This tab is only available for users that belong to a team that has access to monitor {{site.data.keyword.redhat_openshift_notm}} or host level metrics.
    {: note}

* In the *Dashboard* tab, you can monitor through panels predefined dashboards or custom ones and get a specialized insight into network data, application data, topology, services, hosts, and containers. A panel displays a metric or group of metrics in a dashboard.


For each metric view and dashboard, you can define the scope of the data, how to aggregate data, and what time and group filters to apply to the data. For more information, see [Managing panels](/docs/monitoring?topic=monitoring-panels).


You can configure a dashboard as the default entry point for a team, unifying a team's experience, and allowing users to focus their immediate attention on the most relevant information for them.
{: tip}

For more information, see [Viewing metrics](/docs/monitoring?topic=monitoring-monitoring).



## Before you begin
{: #baremetal_linux_prereqs}

1. [Read about {{site.data.keyword.mon_full_notm}}](/docs/monitoring?topic=monitoring-getting-started).

2. Install the {{site.data.keyword.cloud_notm}} CLI. For more information, see [Installing the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli).

3. [Provision an {{site.data.keyword.mon_full_notm}} instance from the catalog](/docs/monitoring?topic=monitoring-provision#provision_ui).

4. [Provision a bare metal server](/docs/bare-metal?topic=bare-metal-getting-started).

    To complete the steps in this topic, ensure you have internet access from the bare metal. This is needed for configuring the monitoring agent.

5. Configure a VPN connection between your terminal and the bare metal server

    Virtual Private Networking (VPN) access enables users to manage all servers remotely and securely over the {{site.data.keyword.cloud}} private network. A VPN connection from your location to the private network allows out-of-band management and server rescue through an encrypted VPN tunnel. VPN tunnels can be initiated to any IBM Cloud data center or PoP allowing you geographic redundancy.

    Complete the following steps to configure a VPN connection between your terminal and the bare metal server:

    1. [Enable VPN access on each account that needs VPN access](/docs/iaas-vpn?topic=iaas-vpn-getting-started#enable-user-vpn-access).

    2. Depending on your operating system, download the latest `MotionPro` 32-bit or 64-bit files from the Array Networks [Clients and Tools](https://support.arraynetworks.net/prx/001/http/supportportal.arraynetworks.net/downloads/downloads.html){: external} download site. [Learn more](/docs/iaas-vpn?topic=iaas-vpn-standalone-vpn-clients){: external}.

    3. Configure a standalone SSL VPN client and open a connection:

    For example, if you use the MotionPro Plus client for MacOS, to add a profile, click **Add**.

    In the `Basic` section, enter a `Title`. Enter a `Gateway`, for example, for a bare metal in Dallas 10, enter `vpn.dal10.softlayer.com`. Enter your VPN user name. Check that the `Port` is set to `443`. Then, click **OK**.

    To open a secure connection, click **Login**.

6. Connect to a bare metal server by using SSH

    You might require a VPN to access your system depending on your security setup and `ssh` configuration on the bare metal host.

    You must `ssh` to the host by using your credentials, or the root credentials that are available from the {{site.data.keyword.cloud_notm}} Console.

    You will require root permissions in order to install the monitoring agent.

    For example, you can complete the following steps to get the bare metal information that you need to `ssh` into the server:

    1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

    2. Click the **Menu** icon ![Menu icon](../images/icon_hamburger.svg) &gt; **Classic Infrastructure** &gt; **Device List**.

    3. Identify the bare metal server that you want to monitor. Copy the **Public IP**.

    4. Click the bare metal server device name.

    5. Select **Passwords**. Copy the password for the **root** user.

       Then, from a terminal, run the following command:

       ```text
       ssh <USER_ID>@<IP_ADDRESS>
       ```
       {: pre}

       Where:

       `<USER_ID>` is the user ID that you use to log in to the bare metal server. For example, use `root`.

       `<IP_ADDRESS>` is the public IP address of the bare metal server.

       For example: `ssh root@45.123.122.12`


## Configure a monitoring agent to collect metrics from the bare metal server
{: #baremetal_linux_step1}
{: step}

You must install a monitoring agent to collect and forward metrics from a bare metal server to an {{site.data.keyword.mon_full_notm}} instance.

Complete the following steps from the command line to install a monitoring agent:

1. Obtain the access key. For more information, see [Getting the access key through the {{site.data.keyword.cloud_notm}} UI](/docs/monitoring?topic=monitoring-access_key#access_key_ibm_cloud_ui).

2. Obtain the ingestion URL. For more information, see [collector endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_ingestion).

3. Deploy the monitoring agent. Run the following command:

    ```text
    curl -sL https://ibm.biz/install-sysdig-agent | sudo bash -s -- --access_key ACCESS_KEY --collector COLLECTOR_ENDPOINT --collector_port 6443 --secure true --tags TAG_DATA --additional_conf 'sysdig_capture_enabled: false'
    ```
    {: pre}

    Where

    * ACCESS_KEY is the ingestion key for the instance.

    * COLLECTOR_ENDPOINT is the ingestion URL for the region where the monitoring instance is available.

    * TAG_DATA are comma-separated tags that are formatted as *TAG_NAME:TAG_VALUE*. You can associate one or more tags to your monitoring agent. For example, *role:serviceX,location:us-south*. Later on, you can use these tags to identify metrics from the environment where the agent is running.

    * The SECURE flag must be set to *true* to use a secure SSL/TLS connection to send metrics to the collector.

    * Set **sysdig_capture_enabled** to *false* to disable the capture feature. By default is set to *true*. For more information, see [Working with captures](/docs/monitoring?topic=monitoring-captures#captures).

    If `cURL` is not available, you must install it. For example, for an Ubuntu bare metal, run the following command: `sudo apt-get update`. Then, run the install command: `sudo apt-get install curl`.

    For example, see the following sample command to install a monitoring agent that forwards metrics to a monitoring instance in US South (Dallas):

    ```text
    curl -sL https://ibm.biz/install-sysdig-agent | sudo bash -s -- -a xxxxxxxxxxxxx -c ingest.us-south.monitoring.cloud.ibm.com --collector_port 6443 --secure true -ac "sysdig_capture_enabled: false" --tags sourceType:baremetal,location:dallas
    ```
    {: screen}

4. Configure the agent for non-orchestrated environments.

    Open the `dragent.yaml` file that is located in `/opt/draios/etc/`.

    Add the following configuration parameter:

    ```text
    feature:
      mode: monitor_light
    ```
    {: codeblock}

    Restart the agent. Run the following command:

    ```sh
    service dragent restart
    ```
    {: pre}

## Launch the monitoring UI to verify that you are getting data to monitor the bare metal server
{: #baremetal_linux_step2}
{: step}

Complete the following steps to launch the web UI:

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

	After you log in with your user ID and password, the {{site.data.keyword.cloud_notm}} console opens.

2. Click the **Menu** icon ![Menu icon](../images/icon_hamburger.svg) &gt; **Observability**.

3. Select **Monitoring**.

    The list of instances that are available on {{site.data.keyword.cloud_notm}} is displayed.

4. Select your instance. Then, click **Open dashboard**.

It may take some time before you see the bare metal entry while the information is initally collected and processed by the monitoring agent.
{: note}

You only can monitor one instance per browser. You could have multiple tabs for the same instance.
{: tip}

## Monitor your bare metal
{: #baremetal_linux_step3}
{: step}

In the *Advisor* tab, you can monitor and troubleshoot the health, risk, and capacity of hosts and Kubernetes clusters.

![Advisor tab](../images/advisor-tab.png "Advisor tab"){: caption="Advisor tab" caption-side="bottom"}

- Data is refreshed every 10 minutes.
- Metrics are prioritized by event count and severity.
- For more information, see [Advisor](https://docs.sysdig.com/en/docs/sysdig-monitor/advisor/){: external}.

In the *Advisor* section, choose to monitor by host. Check out the predefined dashboards that you can use to monitor the health of your resources.

When you choose to monitor by host, you can choose any of the following dashboards:
- Host Resource Usage
- File System Usage & Performance
- Memory Usage
- Network
- Sysdig Agent Health & Status



## [Optional] Configure the Prometheus IPMI Exporter to monitor sensor metrics
{: #baremetal_linux_step4}
{: step}

In addition to the set of metrics that are automatically collected by the monitoring agent, you might want to collect other metrics such as sensor metrics. You can use the `Prometheus IPMI Exporter` to perform the collection of Intelligent Platform Management Interface (IPMI) device sensor metrics from the bare metal server.

* The Prometheus IPMI Exporter exporter supports local IPMI devices and remote devices that can be accessed by using Remote Management Control Protocol (RMCP).
* When you use RMCP to access remote devices, you can use an IPMI exporter to monitor multiple IPMI devices. You identify each device by passing the target hostname as a parameter.
* The IPMI exporter relies on tools from the FreeIPMI suite.

You can collect the following metrics when you configure the IPMI exporter in a bare metal server:

* IPMI admin metrics

    The metric `ipmi_up {collector="<NAME>"}` reports `1` when data from a remote host is collected successfully. It reports `0` for collection of data in a local host.

    The metric `ipmi_scrape_duration_seconds` reports the amount of time that it takes the collector to retrieve the data.

* IPMI System event log (SEL) metrics

    The metric `ipmi_sel_entries_count` reports the number of entries in the system event log.

    The metric `ipmi_sel_free_space_bytes` reports the number of free bytes for new ystem event log entries.

* IPMI sensor data

    The IPMI exporter collects 2 metrics per sensor type: state and value. A value of `0` reports a normal state. A value of `1` reports a warning state. A value of `2` reports a critical state. A value of `NaN` reports information not available. For example, see the metrics for different sensors:

    Temperature sensor metrics: `ipmi_temperature_celsius`, `ipmi_temperature_state`

    Fan speed sensor metrics: `ipmi_fan_speed_rpm`, `ipmi_fan_speed_state`

    Voltage sensor metrics: `ipmi_voltage_state`, `ipmi_voltage_volts`

* IPMI chassis power state of the machine

    The metric `ipmi_chassis_power_state` informs about the current state of the chassis of the machine. It has a value of `1` when the power is on. It has a value of `0` when the power is off.

* DCMI data

    The metric `ipmi_dcmi_power_consumption_current_watts` informs about the live power consumption of the machine in Watts.

* BMC details

    The metric ipmi_bmc_info includes information about the firmware revision and manufacturer in labels and has a value of `1`.

For more information, see [Prometheus IPMI Exporter](https://github.com/soundcloud/ipmi_exporter){: external}.


Complete the following steps to configure the Prometheus IPMI Exporter:

### Install the Prometheus IPMI exporter
{: #baremetal_linux_step4_1}

Complete the following steps:

1. From a local terminal, [download the Prometheus IPMI exporter](https://github.com/soundcloud/ipmi_exporter){: external}.

2. In the bare metal server, from the `shh` session, create the directory `/usr/monitor`. Run the following commands:

    ```text
    cd /usr
    ```
    {: pre}

    ```text
    mkdir monitor
    ```
    {: pre}

3. Copy the file to the bare metal. From the directory where the file is available, run the following command:

    ```text
    scp ipmi_exporter-v1.2.0.linux-amd64.tar.gz  root@<IP_ADDRESS>:/usr/monitor/
    ```
    {: pre}

    Where `<IP_ADDRESS>` is the public IP address of the bare metal server.

    If the command fails, check that your VPN connection is still open.

4. In the bare metal server, from the `shh` session, uncompress the file. Run the following commands:

    ```text
    cd /usr/monitor/
    ```
    {: pre}

    ```text
    tar -xvf ipmi_exporter-v1.2.0.linux-amd64.tar.gz
    ```
    {: pre}

5. In the bare metal server, from the `shh` session, install the FreeIPMI suite. Run the following commands:

    ```text
    sudo apt-get update
    ```
    {: pre}

    ```text
    sudo apt-get install freeipmi
    ```
    {: pre}

6. In the bare metal server, from the `shh` session, check the `ipmi_local.yml` file. Optionally, you can update the file to exclude sensors that you do not want to monitor.

    Change to the directory where you have extracted the IPMI exporter:

    ```text
    cd ipmi_exporter-v1.2.0.linux-amd64/
    ```
    {: pre}

    Check the configuration file. Run the command: `more ipmi_local.yml` You should see a file with similar content.

    ```yaml
    # Configuration file for ipmi_exporter

    # This is an example config for scraping the local host.
    # In most cases, this should work without using a config file at all.
    modules:
            default:
                    # Available collectors are bmc, ipmi, chassis, dcmi, and sel
                    collectors:
                    - bmc
                    - ipmi
                    - dcmi
                    - chassis
                    - sel
                    # Got any sensors you don't care about? Add them here.
                    exclude_sensor_ids:
                    # - 2
    ```
    {: codeblock}

7. In the bare metal server, from the `shh` session, run the IPMI exporter.

    ```text
    ./ipmi_exporter --config.file=ipmi_local.yml &
    ```
    {: pre}

8. Check the IPMI exporter is running. Run the command:

    ```text
    ps -aux | grep ipmi
    ```
    {: pre}

    You should see the IPMI exporter running.



### Install the Prometheus exporter
{: #baremetal_linux_step4_2}

The monitoring agent automatically collects metrics from Prometheus exporters. Therefore, to collect metrics from your IPMI exporter, you must also configure the Prometheus exporter.

Complete the following steps to run the Prometheus exporter:

1. From a local terminal,[download the Prometheus exporter](https://github.com/prometheus-community/ipmi_exporter){: external}.

2. In the bare metal server, from the `shh` session, change to the directory `/usr/monitor/`. Run the following command:

    ```text
    cd /usr/monitor/
    ```
    {: pre}

3. Copy the file to the bare metal. From the directory where the file is available, run the following command:

    ```text
    scp prometheus-2.18.1.linux-amd64.tar.gz root@<IP_ADDRESS>:/usr/monitor/
    ```
    {: pre}

    Where `<IP_ADDRESS>` is the public IP address of the bare metal server.

    If the command fails, check that your VPN connection is still open.

4. In the bare metal server, from the `shh` session, uncompress the file. Run the following commands:

    ```text
    cd /usr/monitor/
    ```
    {: pre}

    ```text
    tar -xvf prometheus-2.18.1.linux-amd64.tar.gz
    ```
    {: pre}

5. Modify the `prometheus.yml` file to include information about the scrape_configuration for the IPMI exporter.

    Change to the Prometheus directory:

    ```text
    cd prometheus-2.18.1.linux-amd64/
    ```
    {: pre}

    Edit the `prometheus.yml` file and add the section **scrape_configs**:

    ```yaml
    # my global config
    global:
      scrape_interval:     15s # Set the scrape interval to every 15 seconds. Default is every 1 minute.
      evaluation_interval: 15s # Evaluate rules every 15 seconds. The default is every 1 minute.
      # scrape_timeout is set to the global default (10s).

    # Alertmanager configuration
    alerting:
      alertmanagers:
      - static_configs:
        - targets:
          # - alertmanager:9093

    # Load rules once and periodically evaluate them according to the global 'evaluation_interval'.
    rule_files:
      # - "first_rules.yml"
      # - "second_rules.yml"

    # A scrape configuration containing exactly one endpoint to scrape:
    # Here it's Prometheus itself.
    scrape_configs:
      # The job name is added as a label `job=<job_name>` to any timeseries scraped from this config.
      - job_name: ipmi

        metrics_path: '/metrics'
        scheme: http

        static_configs:
        - targets: ['localhost:9290']
          labels:
            instance: baremetal01
            region: us-south
    ```
    {: codeblock}

6. Run the Prometheus exporter:

    ```text
    ./prometheus &
    ```
    {: pre}



### Configure network settings
{: #baremetal_linux_step4_3}

If you want to collect metrics from remote servers, complete the following steps:

1. Enable the firewall to allow access to the `ipmi_exporter`.

2. [Optional] Update the VPC rules

    If you use private endpoints, add an inbound rule to the security group for port `9290` with `source type = Security Group` and choose the security group for the bare metal server.



### Update the monitoring agent that is running in the bare metal server
{: #baremetal_linux_step4_4}

Complete the following steps:

1. In the bare metal server, from the `shh` session, change to the directory `/opt/draios/etc/`. Run the following command:

    ```text
    cd /opt/draios/etc/
    ```
    {: pre}

2. Update the `/opt/draios/etc/dragent.yaml`.

    Append the following section to the `dragent.yaml` file:

    ```yaml
    prometheus:
     enabled: true
     interval: 30
     log_errors: true
     max_metrics: 3000
     max_metrics_per_process: 3000
     max_tags_per_metric: 20
     process_filter:
       - include:
           port: 9090
           conf:
             port: 9090
             path: "/metrics"
       - include:
           port: 9290
           conf:
             port: 9290
             path: "/metrics"
    ```
    {: codeblock}

3. Restart the monitoring agent. Run the following command:

    ```text
    service dragent restart
    ```
    {: pre}






## Verify that you can see the prometheus ipmi metrics
{: #baremetal_linux_step5}
{: step}

Complete the following steps:

1. Click the **Menu** icon ![Menu icon](../images/icon_hamburger.svg) &gt; **Observability**.

2. Select **Monitoring**.

3. Identify the monitoring instance that you created. Then, click **Open dashboard**.

4. In the `Explore` view, select **Hosts and Containers**. Then, select the bare metal server that you want to monitor.

    ![Hosts and Containers view](images/monitor-baremetal-img2.png "Hosts and Containers view"){: caption="Hosts and Containers view" caption-side="bottom"}

5. Open the option to **select more Dashboards and Metrics** . Then, enter in the search bar **ipmi**. The list of IPMI metrics is displayed.

    ![IPMI metrics](images/monitor-baremetal-img3.png "IPMI metrics"){: caption="IPMI metrics" caption-side="bottom"}


## Configure a dashboard to analyze the IPMI status of your Bare metal
{: #baremetal_linux_step6}
{: step}

To create a dashboard to monitor the IPMI metrics, complete the following steps:

1. Select the `ipmi_up` metric.

    ![ipmi_up metrics](images/monitor-baremetal-img4.png "ipmi_up metrics"){: caption="ipmi_up metrics" caption-side="bottom"}

2. Select the 3 dots icon. Then, select **Copy to dashboard**.

    ![Copy dashboard](images/monitor-baremetal-img5.png "Copy dashboard"){: caption="Copy dashboard" caption-side="bottom"}

3. Enter the name **[Bare Metal] IPMI monitoring**. Then, click **Copy and Open**.

    ![Copy and open a dashboard](images/monitor-baremetal-img6.png "Copy and open a dashboard"){: caption="Copy and open a dashboard" caption-side="bottom"}

    The dashboard opens.

    ![IPMI custom dashboard](images/monitor-baremetal-img7.png "IPMI custom dashboard"){: caption="IPMI custom dashboard" caption-side="bottom"}

4. Add more IPMI metrics to the **[Bare Metal] IPMI monitoring** custom dashboard. Repeat the steps for each of the IPMI metrics that you want to monitor.

5. Drag and drop, and resize panels to get the dashboard layout that you want. Save the layout.



## Next steps
{: #baremetal_linux_next_steps}

- Create a custom dashboard. For more information, see [Working with dashboards](/docs/monitoring?topic=monitoring-dashboards#dashboards).

- Learn about alerts. For more information, see [Working with alerts](/docs/monitoring?topic=monitoring-monitoring#monitoring_alerts).

- Learn how to manage logs. See [Logging with bare metal servers](/docs/log-analysis?topic=log-analysis-ubuntu_baremetal).

- Learn about the {{site.data.keyword.mon_full_notm}} {{site.data.keyword.sysdigsecure_short}} functionality to find and prioritize software vulnerabilities, detect and respond to threats, and manage configurations, permissions and compliance from source to run. See [Getting started with {{site.data.keyword.sysdigsecure_full}}](/docs/workload-protection?topic=workload-protection-getting-started).
