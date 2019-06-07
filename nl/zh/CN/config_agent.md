---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, config sysdig agent

subcollection: Sysdig

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}
{:important: .important}
{:note: .note}

# 配置 Sysdig 代理程序
{: #config_agent}

在 {{site.data.keyword.cloud_notm}} 中供应 {{site.data.keyword.mon_full_notm}} 服务的实例后，必须在要监视的每个环境中配置 Sysdig 代理程序。Sysdig 代理程序会自动收集和报告预定义的度量值。可以配置每个环境中要监视的度量值。
{:shortdesc}

可以将一个或多个标记与每个 Sysdig 代理程序相关联。标记是格式为 **TAG_NAME:TAG_VALUE** 的逗号分隔值。监视环境时，可以使用这些标记来标识代理程序提供的度量值。例如，可以使用此代理程序收集的所有度量值来包含有关服务名称和位置的信息。
{: tip}

## 在 Linux 上配置 Sysdig 代理程序
{: #config_agent_linux}

要在 Linux 上配置 Sysdig 代理程序，以收集度量值并将其转发到 {{site.data.keyword.mon_full_notm}} 服务的实例，请完成以下步骤：

1. 获取 Sysdig 访问密钥。有关更多信息，请参阅[通过 {{site.data.keyword.cloud_notm}} UI 获取访问密钥](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui)。

2. 获取采集 URL。有关更多信息，请参阅 [Sysdig 收集器端点](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion)。

3. 部署 Sysdig 代理程序。在终端中运行以下命令。

    ```
    curl -sL https://ibm.biz/install-sysdig-agent | sudo bash -s -- --access_key SYSDIG_ACCESS_KEY --collector COLLECTOR_ENDPOINT --collector_port 6443 --secure true --tags TAG_DATA --additional_conf 'sysdig_capture_enabled: false'
    ```
    {: codeblock}

    其中

    * SYSDIG_ACCESS_KEY 是实例的采集密钥。

    * COLLECTOR_ENDPOINT 是监视实例在其中可用的区域的采集 URL。

    * TAG_DATA 是格式为 *TAG_NAME:TAG_VALUE* 的逗号分隔标记。可以将一个或多个标记与 Sysdig 代理程序相关联。例如，*role:serviceX,location:us-south*。 

    * 将 **sysdig_capture_enabled** 设置为 *false* 以禁用 Sysdig 捕获功能。缺省情况下，此值设置为 *true*。有关更多信息，请参阅[使用捕获](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures)。

    * 将 **secure** 设置为 *true* 以将 SSL 用于通信。

如果 Sysdig 代理程序未能正确安装，请手动安装内核头文件。选择分发版，并对该分发版运行该命令。然后，重试部署 Sysdig 代理程序。

* **对于 Debian 和 Ubuntu Linux 分发版**，请运行以下命令：

    ```
    apt-get -y install linux-headers-$(uname -r)
    ```
    {: codeblock}

* **对于 RHEL、CentOS 和 Fedora Linux 分发版**，请运行以下命令：

    ```
    yum -y install kernel-devel-$(uname -r)
    ```
    {: codeblock}


## 在 Docker 容器上配置 Sysdig 代理程序
{: #config_agent_docker}

要在 Docker 容器上配置 Sysdig 代理程序，以收集度量值并将其转发到 {{site.data.keyword.mon_full_notm}} 服务的实例，请完成以下步骤：

1. 获取 Sysdig 访问密钥。有关更多信息，请参阅[通过 {{site.data.keyword.cloud_notm}} UI 获取访问密钥](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui)。

2. 获取采集 URL。有关更多信息，请参阅 [Sysdig 收集器端点](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion)。

3. 部署 Sysdig 代理程序。运行以下命令：

    ```
    docker run -d --name sysdig-agent --restart always --privileged --net host --pid host -e ACCESS_KEY=SYSDIG_ACCESS_KEY -e COLLECTOR=COLLECTOR_ENDPOINT -e COLLECTOR_PORT=6443 -e SECURE=true -e ADDITIONAL_CONF="sysdig_capture_enabled: false" -e TAGS=TAG_DATA  -v /var/run/docker.sock:/host/var/run/docker.sock -v /dev:/host/dev -v /proc:/host/proc:ro -v /boot:/host/boot:ro -v /lib/modules:/host/lib/modules:ro -v /usr:/host/usr:ro --shm-size=350m sysdig/agent
    ```
    {: codeblock}

    其中

    * SYSDIG_ACCESS_KEY 是实例的采集密钥。

    * COLLECTOR_ENDPOINT 是监视实例在其中可用的区域的采集 URL。

    * TAG_DATA 是格式为 *TAG_NAME:TAG_VALUE* 的逗号分隔标记。可以将一个或多个标记与 Sysdig 代理程序相关联。例如，*role:serviceX,location:us-south*。 

    * 将 **sysdig_capture_enabled** 设置为 *false* 以禁用 Sysdig 捕获功能。缺省情况下，此值设置为 *true*。有关更多信息，请参阅[使用捕获](/docs/services/Monitoring-with-Sysdig/captures.html#captures)。

    * 将 **SECURE** 设置为 *true* 以将 SSL 用于通信。

    容器以拆离方式运行。要查看容器的输出，请除去 *-d*。
    {: note}




## 使用脚本在 Kubernetes 集群上配置 Sysdig 代理程序
{: #config_agent_kube_script}

要在 {{site.data.keyword.containerlong_notm}} 中运行的 Kubernetes 集群上配置 Sysdig 代理程序，请完成以下步骤：

1. 获取 Sysdig 访问密钥。有关更多信息，请参阅[通过 {{site.data.keyword.cloud_notm}} UI 获取访问密钥](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui)。

2. 获取采集 URL。有关更多信息，请参阅 [Sysdig 收集器端点](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion)。

3. 设置集群环境。运行以下命令：

    首先，获取用于设置环境变量的命令，并下载 Kubernetes 配置文件。

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    配置文件下载完成后，会显示一个命令，您可以使用该命令将本地 Kubernetes 配置文件的路径设置为环境变量。

    然后，复制并粘贴终端中显示的命令，以设置 KUBECONFIG 环境变量。

4. 部署 Sysdig 代理程序。运行以下命令：

    ```
    curl -sL https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/IBMCloud-Kubernetes-Service/install-agent-k8s.sh | bash -s -- -a SYSDIG_ACCESS_KEY -c COLLECTOR_ENDPOINT -t TAG_DATA -ac 'sysdig_capture_enabled: false'
    ```
    {: codeblock}

    其中

    * SYSDIG_ACCESS_KEY 是实例的采集密钥。

    * COLLECTOR_ENDPOINT 是监视实例在其中可用的区域的采集 URL。

    * TAG_DATA 是格式为 *TAG_NAME:TAG_VALUE* 的逗号分隔标记。可以将一个或多个标记与 Sysdig 代理程序相关联。例如：*role:serviceX,location:us-south*。 

    * 将 **sysdig_capture_enabled** 设置为 *false* 以禁用 Sysdig 捕获功能。缺省情况下，此值设置为 *true*。有关更多信息，请参阅[使用捕获](/docs/services/Monitoring-with-Sysdig/captures.html#captures)。



## 在 Kubernetes 集群上手动配置 Sysdig 代理程序
{: #config_agent_kube_manually}

要在 {{site.data.keyword.containerlong_notm}} 中运行的 Kubernetes 集群上配置 Sysdig 代理程序，请完成以下步骤：

1. 获取 Sysdig 访问密钥。有关更多信息，请参阅[通过 {{site.data.keyword.cloud_notm}} UI 获取访问密钥](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui)。

2. 获取采集 URL。有关更多信息，请参阅 [Sysdig 收集器端点](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion)。

3. 设置集群环境。运行以下命令：

    首先，获取用于设置环境变量的命令，并下载 Kubernetes 配置文件。

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    配置文件下载完成后，会显示一个命令，您可以使用该命令将本地 Kubernetes 配置文件的路径设置为环境变量。

    然后，复制并粘贴终端中显示的命令，以设置 KUBECONFIG 环境变量。

4. 创建名为 **sysdig-agent** 的服务帐户来监视 Kubernetes 集群。运行以下命令：

    ```
    kubectl create serviceaccount sysdig-agent -n ibm-observe
    ```
    {: codeblock}

5. 向 Kubernetes 集群添加私钥。运行以下命令：

    ```
    kubectl create secret generic sysdig-agent --from-literal=access-key=SYSDIG_ACCESS_KEY -n ibm-observe
    ```
    {: codeblock}

    SYSDIG_ACCESS_KEY 是实例的采集密钥。

    Kubernetes 私钥包含用于向 {{site.data.keyword.mon_full_notm}} 服务认证 Sysdig 代理程序的采集密钥。此密钥用于打开安全 Web 套接字来连接监视后端系统上的采集服务器。

6. 创建集群角色和集群角色绑定。 

    下载 [**sysdig-agent-clusterrole.yaml**](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-agent-clusterrole.yaml)。
    
    要添加集群角色，请运行以下命令：
    
    ```
    kubectl apply -f /tmp/sysdig-agent-clusterrole.yaml
    ```
    {: codeblock}

    要添加集群角色绑定，请运行以下命令：

    ```
    kubectl create clusterrolebinding sysdig-agent --clusterrole=sysdig-agent --serviceaccount=ibm-observe:sysdig-agent -n ibm-observe
    ```
    {: codeblock}

7. 编辑 **sysdig-agent-configmap.yaml**，并添加用于配置代理程序以在 {{site.data.keyword.cloud_notm}} 中工作的必需参数。

    下载 [**sysdig-agent-configmap.yaml**](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-agent-configmap.yaml)。

    使用编辑器打开 sysdig-agent-configmap.yaml 文件。然后，添加以下参数：

    * **k8s_cluster_name**：此参数将集群名称指定为度量值标签。可以使用 *kubernetes.cluster.name* 标签按集群名称导航 Kubernetes 仪表板，并过滤掉与该集群关联的度量值。

    * **collector**：此参数指定监视实例在其中可用的区域的采集 URL。 

    * **collector_port**：此参数指示收集器侦听的端口。该值必须设置为 *6443*。
    
    * **ssl**：此参数必须设置为 *true*。
    
    * **ssl_verfiy_certificate**：此参数必须设置为 *true*。
    
    * **new_k8s**：此参数必须设置为 *true*，以捕获 Kube 状态度量值。

    * **sysdig_capture_enabled**：此参数启用或禁用 Sysdig 捕获功能。缺省情况下，此值设置为 *true*。有关更多信息，请参阅[使用捕获](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures)。

    YAML 文件示例如下所示：

    ```
     apiVersion: v1
     kind: ConfigMap
     metadata:
       name: sysdig-agent
     data:
       dragent.yaml: |
       tags: linux:ubuntu,dept:dev,local:nyc
       collector: ingest.us-south.monitoring.cloud.ibm.com
       collector_port: 6443
       ssl: true
       new_k8s: true
       k8s_cluster_name: my_cluster_name
       sysdig_capture_enabled: false
    ```
    {: screen}

8. 将配置映射应用于集群。运行以下命令：

    ```
    kubectl apply -f sysdig-agent-configmap.yaml
    ```
    {: codeblock}

9. 应用守护程序集以将 Sysdig 代理程序部署到集群。运行以下命令：

    下载 [**sysdig-agent-daemonset-v2.yaml**](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-agent-daemonset-v2.yaml)。

    ```
    kubectl apply -f sysdig-agent-daemonset-v2.yaml
    ```
    {: codeblock}




