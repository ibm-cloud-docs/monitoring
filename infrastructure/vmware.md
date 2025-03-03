---

copyright:
  years:  2018, 2025
lastupdated: "2025-02-27"

keywords:

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}


# Monitoring for VMware vCenter Server deployments
{: #vmware-vcenter}

You can add monitoring capabilities to VMware vCenter Server deployments by configuring the VMware vCenter Exporter for Prometheus and a monitoring agent on a Linux server. Performance data of vCenter Server, clusters, ESXi hosts, and Virtual Machines that are collected from your vSphere environment are sent to {{site.data.keyword.mon_full_notm}} for analysis, troubleshooting, and alerting.
{: shortdesc}


VMware vCenter Server® is a hosted private cloud that delivers the VMware vSphere® stack as a service. The VMware® environment is built in addition to a minimum of three {{site.data.keyword.cloud}} bare metal servers and it offers shared network-attached storage and dedicated software-defined storage options. It also includes the automatic deployment and configuration of an easy-to-manage logical edge firewall, which VMware NSX® powers. For more information, see [vCenter Server overview](/docs/vmwaresolutions?topic=vmwaresolutions-vc_vcenterserveroverview).

The following graphic depicts the high-level architecture and components of a three node vCenter Server with NSX-T deployment.

![Architecture of a vCenter Server NSX-T deployment](../images/Log-Analysis-05-VMware-vCenter-Architecture.svg "Architecture of a vCenter Server NSX-T deployment"){: caption="Architecture of a vCenter Server NSX-T deployment" caption-side="bottom"}


## Metrics
{: #vmware-vcenter-metrics}

With the VMware vCenter Exporter for Prometheus, you can collect the following performance metrics:

- VMware Host time series
- VMware Datastore time series
- VMware VM guest time series per VM partition
- VMware VM time series per VM


## Prereqs
{: #vmware-vcenter-prereqs}

- You must have access to a {{site.data.keyword.mon_short}} instance in your account where you plan to monitor and manage the metrics that are collected from your VMware vCenter deployment. You also need the access key to configure the agent to send metrics to this instance, and the region where the instance is provisioned. For more information, see [Getting started with {{site.data.keyword.mon_full_notm}}](/docs/monitoring?topic=monitoring-getting-started).

- You need the vSphere user ID and password, and the vSphere vCenter IP address to configure the VMware vCenter Exporter for Prometheus.

- Check the topic [Tune Agent](https://docs.sysdig.com/en/docs/installation/configuration/sysdig-agent/tune-agent/){: external}

- [Learn more about the VMware vCenter Exporter for Prometheus](https://github.com/pryorda/vmware_exporter){: external}.


## Step 1. Configure the Linux server
{: #vmware-vcenter-step1}

You need to provision a Linux server where you will configure the {{site.data.keyword.mon_short}} agent and the VMware vCenter Exporter for Prometheus. For example, you can use a Linux server such as a Red Hat VSI.

You can deploy the {{site.data.keyword.mon_short}} agent for non-orchestrated environments and pay for the metrics that you configure thorugh the exporter, or deploy the agent for orchestrated environments that gives you an entitlement of 1000 time series per hour included in the price. For more information on agents, see [Collecting default metrics by using the {{site.data.keyword.mon_short}} agent](/docs/monitoring?topic=monitoring-about-collect-metrics#about-collect-metrics-2).
{: note}


The instructions in this topic are based on a Red Hat VSI.

### Provision a Linux VPC server instance
{: #vmware-vcenter-step1-0}

Configure a Linux server to collect metrics from your VMware vCenter to forward the metrics to a {{site.data.keyword.mon_short}} instance.

1. [Provision a bare metal server](/docs/bare-metal?topic=bare-metal-getting-started).

    To complete the steps in this topic, ensure you have internet access from the bare metal server.

2. Configure a VPN connection between your terminal and the bare metal server.

    Virtual Private Networking (VPN) access enables users to manage all servers remotely and securely over the {{site.data.keyword.cloud_notm}} private network. A VPN connection from your location to the private network allows out-of-band management and server rescue through an encrypted VPN tunnel. VPN tunnels can be initiated to any {{site.data.keyword.cloud_notm}} data center or PoP allowing you geographic redundancy.

    Complete the following steps to configure a VPN connection between your terminal and the bare metal server:

    1. [Enable VPN access on each account that needs VPN access](/docs/iaas-vpn?topic=iaas-vpn-getting-started#enable-user-vpn-access).

    2. Depending on your operating system, download the latest `MotionPro` 32-bit or 64-bit files from the Array Networks [Clients and Tools](https://support.arraynetworks.net/prx/001/http/supportportal.arraynetworks.net/downloads/downloads.html){: external} download site. [Learn more](/docs/iaas-vpn?topic=iaas-vpn-standalone-vpn-clients){: external}.

    3. Configure a standalone SSL VPN client and open a connection:

    For example, if you use the MotionPro Plus client for MacOS, click **Add** to add a profile.

    In the `Basic` section, enter a `Title`. Enter a `Gateway`, for example, for a bare metal in Dallas 10, enter `vpn.dal10.softlayer.com`. Enter your VPN user name. Check that the `Port` is set to `443`. Then, click **OK**.

    To open a secure connection, click **Login**.

3. Connect to a bare metal server by using SSH

    You might require a VPN to access your system depending on your security setup and `ssh` configuration on the bare metal host.

    You must use `ssh` to connect to the host by using your credentials, or the root credentials that are available from the {{site.data.keyword.cloud_notm}} Console.

    You will require root permissions to install the monitoring agent.

    For example, you can complete the following steps to get the bare metal server information that you need to use the `ssh` command to access the server:

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

       `<USER_ID>` is the user ID that you use to log in to the bare metal server. For example,  `root`.

       `<IP_ADDRESS>` is the public IP address of the bare metal server.

       For example: `ssh root@45.123.122.12`


### Deploy the {{site.data.keyword.mon_short}} agent
{: #vmware-vcenter-step1-1}

Complete the following steps to configure a {{site.data.keyword.mon_short}} agent on the Linux server. The agent collects metrics from your VMware vCenter deployment and forwards them to a {{site.data.keyword.mon_short}} instance in your account.

1. [Obtain the access key](/docs/monitoring?topic=monitoring-access_key#access_key_ibm_cloud_ui).

2. Obtain the public or private ingestion URL. For more information, see [collector endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_ingestion).

3. Install the kernel headers.

    When you install a monitoring agent, the agent uses kernel header files. [Learn more](https://docs.sysdig.com/en/sysdig-secure/install-agent-components/troubleshooting/kernel-header-troubleshooting/){: external}

    Choose a distribution and run the following command for that distribution.

    For Debian and Ubuntu Linux distributions, run the following command:

    ```sh
    apt-get -y install linux-headers-$(uname -r)
    ```
    {: pre}

    For RHEL, CentOS, and Fedora Linux distributions, run the following command:

    ```sh
    yum -y install kernel-devel-$(uname -r)
    ```
    {: pre}

4. Deploy the monitoring agent for non-orchestrated environments. Run the following command from a terminal.

    ```sh
    curl -sL https://ibm.biz/install-sysdig-agent | sudo bash -s -- --access_key MONITORING_ACCESS_KEY --collector COLLECTOR_ENDPOINT --collector_port 6443  --tags TAG_DATA --additional_conf 'sysdig_capture_enabled: false\nfeature:\n    mode: monitor_light'
    ```
    {: pre}

    Where

    * MONITORING_ACCESS_KEY is the ingestion key for the instance.

    * COLLECTOR_ENDPOINT is the public or private ingestion URL for the region where the monitoring instance is available. To get an endpoint, see [Collector endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_ingestion). For example, for US-South, the endpoint is `ingest.private.us-south.monitoring.cloud.ibm.com`.

    * TAG_DATA is a list of comma-separated tags that are formatted as *TAG_NAME:TAG_VALUE*. You can associate one or more tags to your monitoring agent. For example, *type:VMware,location:us-south*.

    To install cURL, run `yum -q -y install curl` for RHEL, CentOS, and Fedora Linux distributions.
    {: tip}

5. Check that the monitoring agent is running. Run the following command:

    ```sh
    ps -ef | grep sysdig
    ```
    {: pre}

    To see the latest monitoring agent logs, go to the directory `/opt/draios/logs` and check the log file `draios.log`.

    To look for errors, you can run the following command:

    ```sh
    grep error /opt/draios/logs/draios.log
    ```
    {: pre}

### Configure the {{site.data.keyword.mon_short}} agent
{: #vmware-vcenter-step1-2}

You must configure the {{site.data.keyword.mon_short}} agent to forward the Prometheus metrics that the VMware vCenter Exporter for Prometheus collects.

Complete the following steps:

1. In the `/opt/draios/etc` directory, create a `prometheus.yaml` file with the following information:

    ```yaml
    global:
      scrape_interval: 60s
    scrape_configs:
      - job_name: vmware-exporter
        static_configs:
          - targets: ['localhost:9272']
            labels:
              type: vmdemo
    ```
    {: codeblock}

2. Restart the agent to activate the changes. Run the following command:

    ```sh
    service dragent restart
    ```
    {: codeblock}



### Deploy the VMware vCenter Exporter for Prometheus
{: #vmware-vcenter-step1-3}

To deploy and run the VMware vCenter Exporter for Prometheus, you must have Python version 3.6 or higher.
{: note}

Complete the following steps to deploy and configure the VMware vCenter Exporter for Prometheus on a Linux server:

1. Install python 3. Run the following command:

    ```sh
    dnf install python3-pip
    ```
    {: codeblock}

    If you get the error message `vmware exporter ModuleNotFoundError: No module named 'attrs'`, run the following command:

    ```sh
    pip install --upgrade attrs
    ```
    {: codeblock}

2. Install the VMware vCenter Exporter. Run the following command:

    ```sh
    pip install vmware_exporter
    ```
    {: codeblock}

3. Create the directory `/usr/monitoring`. Run the following commands:

    ```sh
    mkdir /usr/monitoring
    ```
    {: codeblock}

4. Create a `config.yml` file. Run the following commands:

    ```yaml
    default:
        vsphere_host: "VMware vCenter IP address"
        vsphere_user: "vCenter user ID"
        vsphere_password: "vCenter password"
        ignore_ssl: False
        specs_size: 5000
        fetch_custom_attributes: True
        fetch_tags: True
        fetch_alarms: True
        collect_only:
            vms: True
            vmguests: True  # For Linux based VMs: Set to false to collect metrics by deploying a Monitoring agent on the VM.
            datastores: True
            hosts: True
            snapshots: True
    ```
    {: codeblock}

The VMware vCenter Exporter for Prometheus is deployed in `/usr/local/bin/vmware_exporter/`.

Then, change the permissions of the file:

```sh
chmod 777 vmware_exporter.service
```
{: codeblock}

### Run the VMware vCenter Exporter for Prometheus as a service
{: #vmware-vcenter-step1-4}

Complete the following steps to run the VMware vCenter Exporter for Prometheus as a service in your Linux server:

1. Create a `vmware_exporter.service` file under `/etc/systemd/system`.

    ```sh
    vi /etc/systemd/system/vmware_exporter.service
    ```
    {: codeblock}

    ```text
    [Unit]
    Description=VMware Exporter
    After=network.target

    [Service]
    User=root
    Group=root
    Restart=always
    Type=simple
    ExecStart=/usr/local/bin/vmware_exporter --config /usr/monitoring/config.yml

    [Install]
    WantedBy=multi-user.target
    ```
    {: codeblock}

    Change the permissions on the file.

    ```sh
    chmod 777 /usr/monitoring/config.yml
    ```
    {: codeblock}

2. Reload the system daemon. Run the following command:

    ```sh
    systemctl daemon-reload
    ```
    {: codeblock}

3. Enable the `vmware_exporter.service`. Run the following command:

    ```sh
    systemctl enable vmware_exporter.service
    ```
    {: codeblock}

4. Start the service. Run the following command:

    ```sh
    systemctl start vmware_exporter.service
    ```
    {: codeblock}

To stop the service, you can run `systemctl stop vmware_exporter.service`.

To see the status of the service, you can run `systemctl status vmware_exporter.service`.

To get the list of metrics that are collected, you can run the following cURL command: `curl localhost:9272/metrics`.
{: tip}


## Step 2. Define your dashboards
{: #vmware-vcenter-step2}

Create a dashboard to monitor your VMware deployment. You can use the **Applications** > **VMWare Overview** template in the **Dashboard Library** to [configure your dashboard.](/docs/monitoring?topic=monitoring-dashboards#dashboards_create)
