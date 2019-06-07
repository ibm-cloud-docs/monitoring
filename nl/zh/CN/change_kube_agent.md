---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-06"

keywords: Sysdig, IBM Cloud, monitoring, customize, kubernetes agent

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

# 定制 Kubernetes Sysdig 代理程序
{: #change_kube_agent}

在 {{site.data.keyword.mon_full_notm}} 中，可以定制 Sysdig 代理程序配置以设置日志级别，阻止端口，包含或排除度量值数据，添加或除去事件以及过滤掉容器。
{:shortdesc}

要定制 Kubernetes Sysdig 代理程序，可能需要在以下任一文件中配置相应部分：

|文件名|操作|
|----------------------------------|-------------------|
|`sysdig-agent-daemonset-v2.yaml`|修改日志级别。|
|`sysdig-agent-configmap.yaml`|阻止端口。</br>包含或排除度量值数据。</br>添加或除去事件。</br>过滤掉容器。|
{: caption="表 1. Kubernetes Sysdig 代理程序配置文件" caption-side="top"} 

要编辑 Kubernetes Sysdig 代理程序，您可能需要编辑 *sysdig-agent-configmap.yaml* 和/或 *sysdig-agent-daemonset-v2.yaml*。
{: tip}

可以使用两种方法来修改配置文件：
* 方法 1：直接在运行代理程序的集群上修改文件。
* 方法 2：本地修改文件，然后将更改应用于集群。

## 使用 kubectl edit 编辑 Kubernetes Sysdig 代理程序配置
{: #change_kube_agent_edit_kube_agent_method1}

要编辑 Kubernetes Sysdig 代理程序配置，请完成以下步骤：

1. 设置集群环境。运行以下命令：

    首先，获取用于设置环境变量的命令，并下载 Kubernetes 配置文件。

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    配置文件下载完成后，会显示一个命令，您可以使用该命令将本地 Kubernetes 配置文件的路径设置为环境变量。

    然后，复制并粘贴终端中显示的命令，以设置 KUBECONFIG 环境变量。

    **注：**每次登录到 {{site.data.keyword.containerlong}} CLI 来使用集群时，都必须运行这些命令，以将集群的配置文件的路径设置为会话变量。Kubernetes CLI 使用此变量来查找与 {{site.data.keyword.cloud_notm}} 中的集群连接所必需的本地配置文件和证书。

2. 编辑 *sysdig-agent-configmap.yaml* 文件。 

    运行以下命令：

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

    进行更改。**注：**请参阅 `vi` 编辑器指示信息以了解如何进行更改。

    保存更改。更改会自动应用。 

3. 编辑 *sysdig-agent-daemonset-v2.yaml* 文件。 

    运行以下命令： 

    ```
    kubectl edit daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

    进行更改。**注：**请参阅 `vi` 编辑器指示信息以了解如何进行更改。

    保存更改。更改会自动应用。

## 使用 kubectl apply 编辑 Kubernetes Sysdig 代理程序配置
{: #change_kube_agent_edit_kube_agent_method2}

如果是在源代码控制系统中存储和管理配置 YAML 文件，请使用此方法。

要编辑 Kubernetes Sysdig 代理程序配置，请完成以下步骤：

1. 从源代码控制器中获取每个文件的最新副本。 

    要使用集群中部署的配置来创建本地文件，还可以运行以下命令：
    
    ```
    kubectl get configmap sysdig-agent -n=ibm-observe -o=yaml > prod-sysdig-agent-configmap.yaml
    ```
    {: codeblock} 
    
    或者 
    
    ```
    kubectl get daemonset sysdig-agent -n=ibm-observe -o=yaml > prod-sysdig-agent-daemonset-v2.yaml
    ```
    {: codeblock}

2. 编辑配置。

3. 使用以下命令来应用更改：

    ```
    kubectl apply -f sysdig-agent-configmap.yaml
    ```
    {: codeblock}
    
    或者
    
    ```
    kubectl apply -f sysdig-agent-daemonset-v2.yaml
    ```
    {: codeblock}

Kubernetes 将更改推送到集群中的所有节点后，运行中的代理程序会自动选取新配置。


## 向通过 Kubernetes Sysdig 代理程序收集的数据添加更多标记
{: #change_kube_agent_add_tags}

要向已经部署的 Kubernetes Sysdig 代理程序配置添加更多标记，请完成以下步骤：

1. 设置集群环境。运行以下命令：

    首先，获取用于设置环境变量的命令，并下载 Kubernetes 配置文件。

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    配置文件下载完成后，会显示一个命令，您可以使用该命令将本地 Kubernetes 配置文件的路径设置为环境变量。

    然后，复制并粘贴终端中显示的命令，以设置 KUBECONFIG 环境变量。

    **注：**每次登录到 {{site.data.keyword.containerlong}} CLI 来使用集群时，都必须运行这些命令，以将集群的配置文件的路径设置为会话变量。Kubernetes CLI 使用此变量来查找与 {{site.data.keyword.cloud_notm}} 中的集群连接所必需的本地配置文件和证书。

2. 编辑 *sysdig-agent-configmap.yaml* 文件。 

    运行以下命令：

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. 进行更改。**注：**请参阅 `vi` 编辑器指示信息以了解如何进行更改。

    ```
    apiVersion: v1
      data:
        dragent.yaml: |
            k8s_cluster_name: marisa-production
            collector: ingest.us-south.monitoring.cloud.ibm.com
            collector_port: 6443
            ssl: true
            sysdig_capture_enabled: false
            new_k8s: true
            tags: department:finance,region:us-south
      ...
    ```
    {: codeblock}

4. 保存更改。 

更改会自动应用。 

对于提供的样本，您将获得 **agent.tag.cluster_version** 和 **agent.tag.region** 标记。您可以使用这两个标记来定义警报，定制作用域，等等。



## 收集一组 Kubernetes 事件
{: #change_kube_agent_collect_events}

{{site.data.keyword.mon_full_notm}} 支持与 Kubernetes 的事件集成。Sysdig 代理程序会自动发现这些服务并从中收集事件数据。您可以编辑代理程序配置文件以更改其缺省行为，还可以包含或排除事件数据。 

缺省情况下，只收集一组有限的事件。有关缺省情况下收集的事件的更多信息，请参阅 [Kubernetes Events ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://sysdigdocs.atlassian.net/wiki/spaces/Platform/pages/234356795/Enable+Disable+Event+Data#Enable/DisableEventData-KubernetesEvents){:new_window}。

要添加或除去事件，必须定制 *sysdig-agent-configmap.yaml* 文件，并指定要包含的事件和要过滤掉的事件。**注：**更改 *sysdig-agent-configmap.yaml* 某个部分中的条目会覆盖缺省配置中该部分的整个内容。
{: tip}

要过滤来自 Kubernetes pod 的事件，请完成以下步骤：

1. 设置集群环境。运行以下命令：

    首先，获取用于设置环境变量的命令，并下载 Kubernetes 配置文件。

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    配置文件下载完成后，会显示一个命令，您可以使用该命令将本地 Kubernetes 配置文件的路径设置为环境变量。

    然后，复制并粘贴终端中显示的命令，以设置 KUBECONFIG 环境变量。

    **注：**每次登录到 {{site.data.keyword.containerlong}} CLI 来使用集群时，都必须运行这些命令，以将集群的配置文件的路径设置为会话变量。Kubernetes CLI 使用此变量来查找与 {{site.data.keyword.cloud_notm}} 中的集群连接所必需的本地配置文件和证书。

2. 编辑 *sysdig-agent-configmap.yaml* 文件。 

    运行以下命令：

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. 进行更改。添加 *events* 部分或更新该部分。

    **注：**请参阅 `vi` 编辑器指示信息以了解如何进行更改。

    例如，您可能希望收集 Kubernetes pod 拉出事件，并过滤掉缺省情况下收集的其他 pod 事件。但您仍希望为节点和 replicationController 收集缺省 Kubernetes 事件。

    ```
    events:
      kubernetes:
        pod:
          - Pulling
    ```
    {: codeblock}

4. 保存更改。 

更改会自动应用。 


在另一个示例中，您可以看到如何收集 Kubernetes 事件的子集：您只想监视 pod 的正在拉出、已拉出和失败的事件。

* 选项 1：将条目中的序列定义为项目符号列表：

    ```
    events:
      kubernetes:
        pod: 
          - Pulling
          - Pulled
          - Failed
    ```
    {: codeblock}

* 选项 2：将条目中的序列定义为用方括号括起的一行：

    ```
    events:
      kubernetes:
        pod: [Pulling, Pulled, Failed]
    ```
    {: codeblock}

有关如何使用定制事件的更多信息，请参阅 [Custom Events ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/222822463/Custom+Events){:new_window}。


## 禁用事件收集
{: #change_kube_agent_disable_events}

要禁止 Sysdig 代理程序收集 Kubernetes 事件，必须修改 *sysdig-agent-configmap.yaml* 文件。请将 **events** 部分中的 **Kubernetes** 条目设置为 *none*。 

完成以下步骤：

1. 设置集群环境。运行以下命令：

    首先，获取用于设置环境变量的命令，并下载 Kubernetes 配置文件。

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    配置文件下载完成后，会显示一个命令，您可以使用该命令将本地 Kubernetes 配置文件的路径设置为环境变量。

    然后，复制并粘贴终端中显示的命令，以设置 KUBECONFIG 环境变量。

    **注：**每次登录到 {{site.data.keyword.containerlong}} CLI 来使用集群时，都必须运行这些命令，以将集群的配置文件的路径设置为会话变量。Kubernetes CLI 使用此变量来查找与 {{site.data.keyword.cloud_notm}} 中的集群连接所必需的本地配置文件和证书。

2. 编辑 *sysdig-agent-configmap.yaml* 文件。 

    运行以下命令：

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. 进行更改。添加 *events* 部分或更新该部分。

    ```
    events:
      kubernetes: none
    ```
    {: codeblock}

6. 保存更改。 

更改会自动应用。 






## 包含和排除度量值
{: #change_kube_agent_inc_exc_metrics}

要过滤定制度量值，必须定制 *sysdig-agent-configmap.yaml* 文件中的 **metrics_filter** 部分。通过配置 **include** 和 **exclude** 过滤参数，可以指定要包含的度量值以及要过滤掉的度量值。

<p class="important">过滤规则顺序的设置如下所示：将应用与度量值匹配的第一个规则。该度量值的后续规则将被忽略。</p>

完成以下步骤：

1. 设置集群环境。运行以下命令：

    首先，获取用于设置环境变量的命令，并下载 Kubernetes 配置文件。

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    配置文件下载完成后，会显示一个命令，您可以使用该命令将本地 Kubernetes 配置文件的路径设置为环境变量。

    然后，复制并粘贴终端中显示的命令，以设置 KUBECONFIG 环境变量。

    **注：**每次登录到 {{site.data.keyword.containerlong}} CLI 来使用集群时，都必须运行这些命令，以将集群的配置文件的路径设置为会话变量。Kubernetes CLI 使用此变量来查找与 {{site.data.keyword.cloud_notm}} 中的集群连接所必需的本地配置文件和证书。

2. 编辑 *sysdig-agent-configmap.yaml* 文件。 

    运行以下命令：

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. 进行更改。添加 *metrics_filter* 部分或更新该部分。

    例如，如果 Sysdig 代理程序的 *metrics_filter* 部分如下所示：

    ```
    metrics_filter:
      - include: metricA.*
      - exclude: metricA.*
      - include: metricB.*
      - include: haproxy.backend.*
      - exclude: haproxy.*
      - exclude: metricC.*
    ```
    {: screen}

    * 您将 Sysdig 代理程序配置为从以 *metricA*、*metricB* 和 *haproxy.backend* 开头的度量值收集所有数据。 

    * 您将过滤掉以 *metricC* 开头的度量值以及以 *haproxy* 开头的其他度量值。 

    * `exclude: metricA.*` 条目将被忽略。

4. 保存更改。 

更改会自动应用。 




## 过滤从中收集数据的 Kubernetes 对象和容器
{: #change_kube_agent_filter_data}

Kubernetes Sysdig 代理程序会自动从它在集群中检测到的*所有容器*收集度量值，包括 Prometheus、StatsD、JMX、应用程序检查和内置度量值。
 
可以定制 Sysdig 代理程序以从度量值收集中排除容器。 

排除容器时，请考虑以下信息：
* 降低代理程序和后端负载。
* 仅从要监视的容器收集数据。
* 可以通过只报告重要容器，而过滤掉不必要或不重要的容器，从而控制成本。

要启用 Sysdig 代理程序用于过滤容器的功能，必须定制 *sysdig-agent-configmap.yaml* 文件。请将 **containers** 部分中的 **use_container_filter** 条目设置为 *true*。**注：**缺省情况下，此功能已关闭。然后，定义包含一个或多个条件并且您要应用的规则。

下表概述了可以定义用于在集群中设置过滤规则的参数：

|参数|条件|
|------------------------------------|------------------------------------------------|
|`container.image`|容器映像名称|
|`container.name`|容器名称|
|`container.label.*`|容器标签|
|`kubernetes.object.*`|Kubernetes 对象。对象可以是 pod、名称空间等|
|`kubernetes.object.annotation.*`|Kubernetes 对象注释|
|`kubernetes.object.label.*`|Kubernetes 对象标签|
|`all`|用于指定所有对象的缺省规则|
{: caption="表 2. 用于在容器上定义条件的参数" caption-side="top"} 

请考虑以下信息，了解 Sysdig 代理程序如何应用您在 **container_filter** 部分中定义的规则：
* 通过为条件配置 **include** 和 **exclude** 过滤参数来定义条件。 
* 列表中的第一个匹配规则将确定是包含还是排除容器。
* 条件由键名和值组成。如果容器的给定键与值相匹配，那么将应用该规则。
* 规则包含多个条件时，`所有条件`都需要匹配，才能应用该规则。

要过滤掉 Sysdig 代理程序在集群中监视的容器，请完成以下步骤：

1. 设置集群环境。运行以下命令：

    首先，获取用于设置环境变量的命令，并下载 Kubernetes 配置文件。

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    配置文件下载完成后，会显示一个命令，您可以使用该命令将本地 Kubernetes 配置文件的路径设置为环境变量。

    然后，复制并粘贴终端中显示的命令，以设置 KUBECONFIG 环境变量。

    **注：**每次登录到 {{site.data.keyword.containerlong}} CLI 来使用集群时，都必须运行这些命令，以将集群的配置文件的路径设置为会话变量。Kubernetes CLI 使用此变量来查找与 {{site.data.keyword.cloud_notm}} 中的集群连接所必需的本地配置文件和证书。

2. 编辑 *sysdig-agent-configmap.yaml* 文件。 

    运行以下命令：

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. 进行更改。添加 *metrics_filter* 部分或更新该部分。

    例如，请参阅以下配置映射摘录：

    ```
    containers:
        # Enable the feature
        use_container_filter: true
        #
        # Include or exclude conditions
        container_filter:
           - include:
                container.image: 
           - include:
                container.name: 
           - exclude:
                kubernetes.namespace.name: kube-system
    ```  
    {: codeblock}

6. 保存更改。 

更改会自动应用。 


## 阻止端口
{: #change_kube_agent_block_ports}

要阻止来自网络端口的网络流量和度量值，必须定制 *sysdig-agent-configmap.yaml* 文件中的 **blacklisted_ports** 部分。必须列出要从中过滤掉任何数据的端口。

**注：**端口 53 (DNS) 始终列入黑名单。 

完成以下步骤：

1. 设置集群环境。运行以下命令：

    首先，获取用于设置环境变量的命令，并下载 Kubernetes 配置文件。

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    配置文件下载完成后，会显示一个命令，您可以使用该命令将本地 Kubernetes 配置文件的路径设置为环境变量。

    然后，复制并粘贴终端中显示的命令，以设置 KUBECONFIG 环境变量。

    **注：**每次登录到 {{site.data.keyword.containerlong}} CLI 来使用集群时，都必须运行这些命令，以将集群的配置文件的路径设置为会话变量。Kubernetes CLI 使用此变量来查找与 {{site.data.keyword.cloud_notm}} 中的集群连接所必需的本地配置文件和证书。

2. 编辑 *sysdig-agent-configmap.yaml* 文件。 

    运行以下命令：

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. 进行更改。添加 *metrics_filter* 部分或更新该部分。

    例如，以下样本显示了如何设置 Sysdig 代理程序的 *blacklisted_ports* 部分，以排除来自端口 6666 和 6379 的数据：

    ```
    blacklisted_ports:
      - 6666
      - 6379
    ```
    {: screen}

6. 保存更改。 

更改会自动应用。 



## 更改日志级别
{: #change_kube_agent_log_level}

要配置日志级别，必须定制 *sysdig-agent-daemonset-v2.yaml* 文件中的 **log** 部分。 

Sysdig 代理程序在 */opt/draios/logs/draios.log* 中生成日志条目。 
* 日志文件在大小达到 10 MB 时会循环。
* 将保留 10 个最近的日志文件。附加到文件名的日期戳记用于确定要保留的文件。
* 有效日志级别为：*none*、*error*、*warning*、*info*、*debug* 和 *trace*
* 缺省日志级别为 *info*，其中除了用于任何警告和错误的条目外，每次向后端服务器传输聚集的度量值时（每秒一次），都会创建一个条目。
* 可以通过配置 Sysdig 代理程序配置文件 **/opt/draios/etc/dragent.yaml** 来定制日志的类型和收集的条目。编辑该文件后，必须在 shell 中使用 `service dragent restart` 重新启动代理程序以使更改生效。

下表列出了一些常见场景以及必须在其中每个场景中设置的值：

|用例|Log 部分条目|
|-----------------------------------------------|-----------------------------|
|对代理程序行为进行故障诊断|`file_priority: debug`|
|减少容器控制台输出|`console_priority: warning`|
|按严重性过滤事件|`event_priority: warning`|
|验证包含或排除的度量值|`metrics_excess_log: true`|
{: caption="表 2. Log 部分条目" caption-side="top"} 

要配置日志级别，请完成以下步骤：

1. 设置集群环境。运行以下命令：

    首先，获取用于设置环境变量的命令，并下载 Kubernetes 配置文件。

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    配置文件下载完成后，会显示一个命令，您可以使用该命令将本地 Kubernetes 配置文件的路径设置为环境变量。

    然后，复制并粘贴终端中显示的命令，以设置 KUBECONFIG 环境变量。

    **注：**每次登录到 {{site.data.keyword.containerlong}} CLI 来使用集群时，都必须运行这些命令，以将集群的配置文件的路径设置为会话变量。Kubernetes CLI 使用此变量来查找与 {{site.data.keyword.cloud_notm}} 中的集群连接所必需的本地配置文件和证书。

2. 编辑 *sysdig-agent-daemonset-v2.yaml* 文件。 

    运行以下命令：

    ```
    kubectl edit daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. 进行更改。添加 *log* 部分或更新该部分。

    例如，要过滤掉低严重性的事件（*notice*、*information* 和 *debug*），必须将 **log** 部分的 **metrics_excess_log** 条目设置为 *true*：

    ```
    log:
      file_priority: warning
      console_priority: info
      event_priority: warning
      metrics_excess_log: true
    ```
    {: codeblock}

6. 保存更改。 

更改会自动应用。 


## 按严重性过滤 Kubernetes 事件
{: #change_kube_agent_filterby_severity}

要按严重性过滤事件，必须修改 *sysdig-agent-daemonset-v2.yaml* 文件。请将 **log** 部分中的 **event_priority** 条目设置为 *none*。 

缺省日志级别为 **information**。这表示仅传输警告和更高严重性的事件。

有效级别为：*emergency*、*alert*、*critical*、*error*、*warning*、*notice*、*information*、*debug* 和 *none*。**注**：值按优先级从高到低列出。

完成以下步骤：

1. 设置集群环境。运行以下命令：

    首先，获取用于设置环境变量的命令，并下载 Kubernetes 配置文件。

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    配置文件下载完成后，会显示一个命令，您可以使用该命令将本地 Kubernetes 配置文件的路径设置为环境变量。

    然后，复制并粘贴终端中显示的命令，以设置 KUBECONFIG 环境变量。

    **注：**每次登录到 {{site.data.keyword.containerlong}} CLI 来使用集群时，都必须运行这些命令，以将集群的配置文件的路径设置为会话变量。Kubernetes CLI 使用此变量来查找与 {{site.data.keyword.cloud_notm}} 中的集群连接所必需的本地配置文件和证书。

2. 编辑 *sysdig-agent-daemonset-v2.yaml* 文件。 

    运行以下命令：

    ```
    kubectl edit daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. 进行更改。添加 *log* 部分或更新该部分。

    例如，要过滤掉低严重性的事件（*notice*、*information* 和 *debug*），必须将 log 部分的 **event_priority** 设置为 *warning*：

    ```
    log:
      event_priority: warning
    ```
    {: codeblock}

6. 保存更改。 

更改会自动应用。 

## 将包含或排除的度量值记录到日志文件
{: #change_kube_agent_log_metrics}

要将有关包含及排除哪些定制度量值的信息记录到日志文件，必须定制 *sysdig-agent-daemonset-v2.yaml* 文件。请将 **log** 部分中的 **metrics_excess_log** 条目设置为 **true**。

* 缺省情况下，日志记录处于禁用状态。 
* 日志记录每 30 秒在 INFO 级别执行一次并持续 10 秒。 
* 日志文件位于 */opt/draios/logs/draios.log*。
* 日志记录数据的格式如下所示：

    ```
    +/-[type][metric included/excluded]: metric.name (filter: +/-[metric.filter])
    ```
    {: screen}

    * *+/-* 符号指示是包含还是排除该度量值。加号 (*+*) 指示包含度量值。减号 (*-*) 指示排除度量值。 

    * *[type]* 指定度量类型，例如 *statsd*。
    
    * *[metric excluded/excluded]* 以人类可读的方式指示是包含还是排除该度量值。

    *  *metric.name* 指示度量名称。

    * *(filter: +/-[metric.filter])* 提供有关 *sysdig-agent-daemonset-v2.yaml* 文件的 **metrics_filter** 部分中所定义任何过滤器的信息。

样本条目类似于以下内容：

```
-[statsd] metric excluded: mongo.statsd.vsize (filter: -[mongo.statsd.*])
+[statsd] metric included: mongo.statsd.netIn (filter: +[mongo.statsd.net*])
```
{: screen}

完成以下步骤：

1. 设置集群环境。运行以下命令：

    首先，获取用于设置环境变量的命令，并下载 Kubernetes 配置文件。

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    配置文件下载完成后，会显示一个命令，您可以使用该命令将本地 Kubernetes 配置文件的路径设置为环境变量。

    然后，复制并粘贴终端中显示的命令，以设置 KUBECONFIG 环境变量。

    **注：**每次登录到 {{site.data.keyword.containerlong}} CLI 来使用集群时，都必须运行这些命令，以将集群的配置文件的路径设置为会话变量。Kubernetes CLI 使用此变量来查找与 {{site.data.keyword.cloud_notm}} 中的集群连接所必需的本地配置文件和证书。

2. 编辑 *sysdig-agent-daemonset-v2.yaml* 文件。 

    运行以下命令：

    ```
    kubectl edit daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. 进行更改。添加 *log* 部分或更新该部分。

    例如，要过滤掉低严重性的事件（*notice*、*information* 和 *debug*），必须将 **log** 部分的 **metrics_excess_log** 条目设置为 *true*：

    ```
    log:
      metrics_excess_log: true
    ```
    {: codeblock}

6. 保存更改。 

更改会自动应用。 


## 样本配置映射 YAML 文件
{: #change_kube_agent_sample_configmap}

```
apiVersion: v1
data:
  dragent.yaml: | 
    ### Agent tags
    # tags: linux:ubuntu,dept:dev,local:nyc
    #### Sysdig Software related config 
    ####
    # Sysdig collector address
    # collector: 192.168.1.1
    # Collector TCP port
    # collector_port: 6666
    # Whether collector accepts ssl
    # ssl: true
    # collector certificate validation
    # ssl_verify_certificate: true
    #######################################
    #
    k8s_cluster_name: cluster12
    collector: ingest.us-south.monitoring.cloud.ibm.com
    collector_port: 6443
    ssl: true
    ssl_verify_certificate: true
    sysdig_capture_enabled: false
    new_k8s: true
    tags: type:mycluster,region:us-south
    blacklisted_ports:
      - 6666
      - 6379
    events:    
      kubernetes:
        node: 
          - Rebooted
      metrics_filter:
        - include: metricA.*
        - exclude: metricA.*
        - include: metricB.*
      use_container_filter: true
      container_filter: 
        - exclude:
          kubernetes.namespace.name: kube-system
kind: ConfigMap
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"v1","data":{"dragent.yaml":"### Agent tags\n# tags: linux:ubuntu,dept:dev,local:nyc\n#### Sysdig Software related config \n####\n# Sysdig collector address\n# collector: xxx.xxx.x.x\n# Collector TCP port\n# collector_port: 6666\n# Whether collector accepts ssl\n# ssl: true\n# collector certificate validation\n# ssl_verify_certificate: true\n#######################################\n#\nk8s_cluster_name: marisa-production\ncollector: ingest.us-south.monitoring.cloud.ibm.com\ncollector_port: 6443\nssl: true\nssl_verify_certificate: true\nsysdig_capture_enabled: true\nnew_k8s: true\ntags: cluster:mycluster,region:us-south\nevents:    \n  kubernetes:\n     node: \n       - Rebooted\nuse_container_filter: true\ncontainer_filter: \n      - exclude:\n         kubernetes.namespace.name: kube-system\n         container.image: \"registry.ng.bluemix.net/*\"\n"},"kind":"ConfigMap","metadata":{"annotations":{},"creationTimestamp":"2018-11-07T10:57:38Z","name":"sysdig-agent","namespace":"default","resourceVersion":"9999999","selfLink":"/api/v1/namespaces/default/configmaps/sysdig-agent","uid":"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"}}
  creationTimestamp: 2018-11-07T10:57:38Z
  name: sysdig-agent
  namespace: default
  resourceVersion: "9999999"
  selfLink: /api/v1/namespaces/default/configmaps/sysdig-agent
  uid: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```
{: codeblock}

## 样本守护程序 YAML 文件
{: #change_kube_agent_sample_daemonset}

```
 Please edit the object below. Lines beginning with a '#' will be ignored,
# and an empty file will abort the edit. If an error occurs while saving this file will be
# reopened with the relevant failures.
#
apiVersion: extensions/v1beta1
kind: DaemonSet
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"extensions/v1beta1","kind":"DaemonSet","metadata":{"annotations":{},"labels":{"app":"sysdig-agent"},"name":"sysdig-agent","namespace":"default"},"spec":{"template":{"metadata":{"labels":{"app":"sysdig-agent"}},"spec":{"containers":[{"image":"sysdig/agent","imagePullPolicy":"Always","name":"sysdig-agent","readinessProbe":{"exec":{"command":["test","-e","/opt/draios/logs/running"]},"initialDelaySeconds":10},"resources":{"limits":{"memory":"1024Mi"},"requests":{"cpu":"100m","memory":"512Mi"}},"securityContext":{"privileged":true},"volumeMounts":[{"mountPath":"/host/var/run/docker.sock","name":"docker-sock","readOnly":false},{"mountPath":"/host/dev","name":"dev-vol","readOnly":false},{"mountPath":"/host/proc","name":"proc-vol","readOnly":true},{"mountPath":"/host/boot","name":"boot-vol","readOnly":true},{"mountPath":"/host/lib/modules","name":"modules-vol","readOnly":true},{"mountPath":"/host/usr","name":"usr-vol","readOnly":true},{"mountPath":"/dev/shm","name":"dshm"},{"mountPath":"/opt/draios/etc/kubernetes/config","name":"sysdig-agent-config"},{"mountPath":"/opt/draios/etc/kubernetes/secrets","name":"sysdig-agent-secrets"}]}],"dnsPolicy":"ClusterFirstWithHostNet","hostNetwork":true,"hostPID":true,"serviceAccount":"sysdig-agent","terminationGracePeriodSeconds":5,"tolerations":[{"effect":"NoSchedule","key":"node-role.kubernetes.io/master"}],"volumes":[{"emptyDir":{"medium":"Memory"},"name":"dshm"},{"hostPath":{"path":"/var/run/docker.sock"},"name":"docker-sock"},{"hostPath":{"path":"/dev"},"name":"dev-vol"},{"hostPath":{"path":"/proc"},"name":"proc-vol"},{"hostPath":{"path":"/boot"},"name":"boot-vol"},{"hostPath":{"path":"/lib/modules"},"name":"modules-vol"},{"hostPath":{"path":"/usr"},"name":"usr-vol"},{"configMap":{"name":"sysdig-agent","optional":true},"name":"sysdig-agent-config"},{"name":"sysdig-agent-secrets","secret":{"secretName":"sysdig-agent"}}]}},"updateStrategy":{"type":"RollingUpdate"}}}
  creationTimestamp: 2018-11-07T13:39:58Z
  generation: 2
  labels:
    app: sysdig-agent
  name: sysdig-agent
  namespace: default
  resourceVersion: "5980648"
  selfLink: /apis/extensions/v1beta1/namespaces/default/daemonsets/sysdig-agent
  uid: 9ea3353f-e292-11e8-b4b3-260d32136de0
spec:
  revisionHistoryLimit: 10
  selector:
    matchLabels:
      app: sysdig-agent
log:
  event_priority: warning
  file_priority: warning
  console_priority: info
  metrics_excess_log: true
```
{: codeblock}

