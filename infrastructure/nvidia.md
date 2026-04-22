---

copyright:
  years:  2018, 2026
lastupdated: "2026-04-22"

keywords:

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}


# Monitoring NVIDIA GPUs with {{site.data.keyword.mon_full_notm}}
{: #nvidia-gpu-monitoring}

You can monitor NVIDIA GPU performance in your IKS clusters, ROKS clusters, and VSI instances with {{site.data.keyword.mon_full_notm}}. On IKS and ROKS clusters, GPU metrics are automatically collected by the {{site.data.keyword.mon_short}} agent once the NVIDIA GPU Operator is installed. On VSI instances, a simple scrape configuration must be added to the agent. Metrics are sent to your {{site.data.keyword.mon_short}} instance for analysis, troubleshooting, and alerting.
{: shortdesc}


## Metrics
{: #nvidia-gpu-monitoring-metrics}

With the NVIDIA DCGM Exporter, you can collect GPU performance metrics including:

- GPU utilization and temperature
- GPU memory usage and saturation
- Power consumption
- NVLink throughput
- ECC memory errors
- Per-GPU and per-workload breakdowns


## Prerequisites
{: #nvidia-gpu-monitoring-prereqs}

- You must have an {{site.data.keyword.mon_short}} instance provisioned in your account. For more information, see [Getting started with {{site.data.keyword.mon_full_notm}}](/docs/monitoring?topic=monitoring-getting-started).

- You must have an IKS or ROKS cluster with GPU-enabled worker nodes, or a VSI instance provisioned with NVIDIA GPUs.

- For IKS and ROKS clusters, you need `kubectl` and `helm` CLI tools installed and configured to access your cluster.

- For ROKS clusters, you need `oc` CLI access.

- [Learn more about the NVIDIA GPU Operator](https://github.com/NVIDIA/gpu-operator){: external}.


## Monitoring GPUs on IKS clusters
{: #nvidia-gpu-monitoring-iks}

### Step 1. Verify the {{site.data.keyword.mon_short}} agent
{: #nvidia-gpu-monitoring-iks-step1}

The {{site.data.keyword.mon_short}} agent is automatically deployed when creating IKS clusters. Verify the agent is running with the following command:

```sh
kubectl -n ibm-observe get pods
```
{: pre}

You should see the `sysdig-agent` pods in a `Running` state.

If the agent is not present, you can install it by following the [{{site.data.keyword.mon_short}} agent installation guide](/docs/monitoring?topic=monitoring-about-collect-metrics#about-collect-metrics-2).
{: note}

### Step 2. Install the NVIDIA GPU Operator
{: #nvidia-gpu-monitoring-iks-step2}

1. Add the NVIDIA Helm repository and update it.

    ```sh
    helm repo add nvidia https://helm.ngc.nvidia.com/nvidia
    helm repo update
    ```
    {: pre}

2. Create a `values.yaml` file with the following content:

    ```yaml
    nodeSelector:
      "ibm-cloud.kubernetes.io/gpu-enabled": "true"
    dcgmExporter:
      serviceMonitor:
        enabled: false
    ```
    {: codeblock}

    In this file, the operator is configured to only be installed on worker nodes provisioned with NVIDIA GPUs. The `serviceMonitor` feature is disabled to ensure compatibility with {{site.data.keyword.mon_full_notm}}.

3. Install the GPU Operator using Helm.

    ```sh
    helm upgrade --install gpu-operator nvidia/gpu-operator \
      --namespace gpu-operator \
      --create-namespace \
      -f values.yaml
    ```
    {: pre}

### Step 3. Verify GPU metrics collection
{: #nvidia-gpu-monitoring-iks-step3}

After the GPU Operator is installed, the {{site.data.keyword.mon_short}} agent automatically uses an out-of-the-box configuration sent from the backend to scrape all GPU metrics from the DCGM Exporter. No additional configuration is needed.

Restart the {{site.data.keyword.mon_short}} agent to ensure the new configuration is picked up:

```sh
kubectl rollout restart daemonset sysdig-agent --namespace ibm-observe
```
{: pre}

After a few minutes, you will be able to see the **Nvidia GPU Monitoring** dashboard in your {{site.data.keyword.mon_short}} instance.


## Monitoring GPUs on ROKS clusters
{: #nvidia-gpu-monitoring-roks}

### Step 1. Verify the {{site.data.keyword.mon_short}} agent
{: #nvidia-gpu-monitoring-roks-step1}

The {{site.data.keyword.mon_short}} agent is automatically deployed when creating ROKS clusters. Verify the agent is running with the following command:

```sh
kubectl -n ibm-observe get pods
```
{: pre}

You should see the `sysdig-agent` pods in a `Running` state.

If the agent is not present, you can install it by following the [{{site.data.keyword.mon_short}} agent installation guide](/docs/monitoring?topic=monitoring-about-collect-metrics#about-collect-metrics-2).
{: note}

### Step 2. Install the NVIDIA GPU Operator
{: #nvidia-gpu-monitoring-roks-step2}

For ROKS clusters, follow the official Red Hat guide:

1. Install the Node Feature Discovery Operator (NFD) and verify it.

2. Install the NVIDIA GPU Operator.

For detailed instructions, see the [NVIDIA GPU Operator on OpenShift documentation](https://docs.nvidia.com/datacenter/cloud-native/openshift/latest/index.html){: external}.

### Step 3. Verify GPU metrics collection
{: #nvidia-gpu-monitoring-roks-step3}

Once the GPU Operator is installed, the {{site.data.keyword.mon_short}} agent automatically uses an out-of-the-box configuration sent from the backend to scrape all GPU metrics from the DCGM Exporter. No additional configuration is needed.

After a few minutes, you will be able to see the **Nvidia GPU Monitoring** dashboard in your {{site.data.keyword.mon_short}} instance.


## Monitoring GPUs on VSI instances
{: #nvidia-gpu-monitoring-vsi}

### Step 1. Verify the {{site.data.keyword.mon_short}} agent
{: #nvidia-gpu-monitoring-vsi-step1}

Ensure the {{site.data.keyword.mon_short}} agent is installed and running on your VSI instance. For more information, see [Collecting default metrics by using the {{site.data.keyword.mon_short}} agent](/docs/monitoring?topic=monitoring-about-collect-metrics#about-collect-metrics-2).

### Step 2. Install the NVIDIA DCGM Exporter
{: #nvidia-gpu-monitoring-vsi-step2}

Run the NVIDIA DCGM Exporter as a Docker container:

```sh
docker run -d --gpus all --cap-add SYS_ADMIN --rm -p 9400:9400 nvcr.io/nvidia/k8s/dcgm-exporter:4.4.2-4.7.0-ubuntu22.04
```
{: pre}

It is recommended to create a `systemd` service or similar so the container runs automatically after a reboot.
{: tip}

### Step 3. Configure the {{site.data.keyword.mon_short}} agent
{: #nvidia-gpu-monitoring-vsi-step3}

Add the following `prometheus.yaml` section to the {{site.data.keyword.mon_short}} agent configuration file at `/opt/draios/etc/dragent.yaml`:

```yaml
prometheus.yaml: |
  scrape_configs:
    - job_name: "nvidia-metrics"
      static_configs:
        - targets: ["localhost:9400"]
```
{: codeblock}

Restart the agent to apply the configuration:

```sh
service dragent restart
```
{: pre}

After a few minutes, you will be able to see the **Nvidia GPU Monitoring** dashboard in your {{site.data.keyword.mon_short}} instance.


## Dashboard and alerts
{: #nvidia-gpu-monitoring-dashboard}

With this integration, the following are available in your {{site.data.keyword.mon_short}} instance:

- **Nvidia GPU Monitoring** dashboard with GPU performance data. The dashboard can be scoped by cluster, namespace, workload, and GPU device.

- **Alerts** ready to be enabled in the Alerts Library:

    - **[Nvidia] Gpu Memory Exhaustion** — GPU VRAM usage exceeded the configured threshold. The device is at risk of out-of-memory errors.
    - **[Nvidia] Gpu Temperature Too High** — GPU temperature exceeded the configured threshold. Risk of thermal throttling or hardware damage.
    - **[Nvidia] Gpu Underutilization** — GPU utilization has been below the configured threshold for too much time. The device may be idle or misconfigured.

You can customize the dashboard and enable the alerts from the {{site.data.keyword.mon_short}} UI. For more information, see [Working with dashboards](/docs/monitoring?topic=monitoring-dashboards) and [Working with alerts](/docs/monitoring?topic=monitoring-alerts).
