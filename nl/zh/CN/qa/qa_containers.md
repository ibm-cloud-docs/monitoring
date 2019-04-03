---

copyright:
  years: 2017, 2019

lastupdated: "2019-03-06"

keywords: IBM Cloud, monitoring

subcollection: cloud-monitoring

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



# 监视 Kubernetes 集群的常见问题
{: #qa_containers}

下面是对 {{site.data.keyword.monitoringshort}} 服务和 {{site.data.keyword.containershort_notm}} 服务的常见问题的解答。
{:shortdesc}

* [对容器执行 Grafana 查询不显示数据或者发生错误](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-qa_containers#metric_format_change)
* [如何在终端会话中设置集群环境？](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-qa_containers#qa1)
* [在哪里可以获取集群名称和集群标识？](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-qa_containers#qa3)
* [如何获取名称空间的列表？](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-qa_containers#qa7)
* [如何获取 Kubernetes 集群中名称空间的 pod 列表？](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-qa_containers#qa8)
* [如何按名称空间获取集群中的所有 pod？](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-qa_containers#qa9)

## 对容器执行 Grafana 查询不显示数据或者发生错误
{: #metric_format_change}

您可以为容器定义的查询格式已更改。

不推荐使用以下格式： 

```
{Prefix}.{Version}.{Provider}.{Type}.{ServiceName}.{Region}.{Account}.{Cluster}.{Metric}.{Container in a pod}.{Functions}
```
{: screen}

有效的新格式如下：

* [容器的 CPU 度量值查询格式](/docs/services/cloud-monitoring/reference?topic=cloud-monitoring-metrics_format_containers#cpu_containers)
* [工作程序的负载度量值查询格式](/docs/services/cloud-monitoring/reference?topic=cloud-monitoring-metrics_format_containers#load_workers)
* [容器的内存度量值查询格式](/docs/services/cloud-monitoring/reference?topic=cloud-monitoring-metrics_format_containers#mem_containers)

将旧查询迁移到新格式，以在 Grafana 中对数据进行可视化。

例如，如果查询以 `crn.v1.bluemix.public.containers-kubernetes.us-south.` 开头，那么必须将查询迁移到新格式，即 `ibmcloud.public.containers-kubernetes.us-south`。

下表列出了其格式不推荐使用的字段：

 <table>
      <caption>表 1. 容器的 Grafana 查询字段</caption>
      <tr>
        <th align="center">字段</th>
        <th align="center">描述</th>
        <th align="center">有效值</th>
      </tr>
      <tr>
        <td>前缀</td>
        <td>用于指示是 {{site.data.keyword.IBM_notm}} Cloud 资源的前缀。</td>
        <td>`crn`</td>
      </tr>
      <tr>
        <td>版本</td>
        <td>指示所收集度量值数据的格式和字段的版本。</td>
        <td>`v1`</td>
      </tr>
      <tr>
        <td>提供者</td>
        <td>在其中收集数据的云提供者。此字段是字母数字标识。</td>
        <td>对于公共 {{site.data.keyword.IBM_notm}} Cloud，值为：`bluemix`</td>
      </tr>
      <tr>
        <td>类型</td>
        <td>在其中收集数据的云环境。</td>
        <td>对于公共 {{site.data.keyword.IBM_notm}} Cloud，值为：`public`</td>
      </tr>
      <tr>
        <td>服务名称</td>
        <td>在其中收集度量值的云基础架构。</td>
        <td>对于 {{site.data.keyword.monitoringshort}} 服务，值为：`containers-kubernetes`</td>
      </tr>
      <tr>
        <td>区域</td>
        <td>在其中收集度量值的云区域。</td>
        <td>对于美国南部区域，值为：`ng`<br>对于英国区域，值为：`eu-gb`<br>对于德国，值为：`eu-de`<br>对于悉尼，值为：`au-syd`</td>
      </tr>
      <tr>
        <td>帐户</td>
        <td>收集度量值的帐户的 GUID。<br>此字段的格式如下：`a_ID`，其中 ID 是帐户的 GUID。<br>要获取帐户的 GUID，请参阅[如何获取帐户的 GUID](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#account_guid)。</td>
        <td>a_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</td>
      </tr>
      <tr>
        <td>集群</td>
        <td>收集度量值的集群的 GUID。</td>
        <td>xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</td>
      </tr>
      <tr>
        <td>度量值</td>
        <td>为容器自动收集的度量值。</td>
        <td>有关 CPU 度量值的列表，请参阅[容器的 CPU 度量值](/docs/services/cloud-monitoring/containers?topic=cloud-monitoring-monitoring_bmx_containers_ov#cpu_metrics_containers)<br>有关内存度量值的列表，请参阅[内存度量值](/docs/services/cloud-monitoring/containers?topic=cloud-monitoring-monitoring_bmx_containers_ov#memory_metrics)</td>
      </tr>
      <tr>
        <td>pod 中的容器</td>
        <td>Kubernetes 资源名称和 GUID 的组合，此组合对于唯一标识在 pod 中运行的容器是必需的。<br>**注**：查看查询中此条目的可用选项列表时，请注意还有一个以下格式的条目：{namespace}{pod_name}{deploymentname_name}_POD{container_ID}。此条目对应于 Kubernetes 创建的内部容器标识。</td>
		<td>{namespace}_{pod_name}_{deployment_name}_{container_id}</td>
      </tr>
      <tr>
        <td>函数</td>
        <td>可以选择用于在面板中可视化容器度量值的查询函数。<br>有关更多信息，请参阅[函数 ![（外部链接图标）](../../icons/launch-glyph.svg "外部链接图标")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
        <td></td>
      </tr>
    </table>


## 如何在终端会话中设置集群环境？
{: #qa1}

您必须使用命令来设置 Kubernetes 集群的上下文以对其进行管理。

**注**：要管理集群，您需要将 {{site.data.keyword.containershort_notm}} 服务的 IAM 策略分配给有权完成该任务的用户。

要设置集群的上下文，请完成以下步骤：

1. 登录到 {{site.data.keyword.Bluemix_notm}} 中与已创建集群关联的区域、组织和空间。有关更多信息，请参阅[如何登录到 {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login)。

2. 初始化 {{site.data.keyword.containershort_notm}} 服务插件。运行以下命令：

	```
	ibmcloud cs init
	```
	{: codeblock}

3. 在终端会话中设置集群的上下文。运行以下命令：
    
	```
	ibmcloud cs cluster-config MyCluster
	```
	{: codeblock}

    运行此命令的输出提供了必须在终端中运行以设置配置文件路径的命令。例如：

	```
	export KUBECONFIG=/Users/ibm/.bluemix/plugins/container-service/clusters/MyCluster/kube-config-hou02-MyCluster.yml
	```
	{: codeblock}

    复制并粘贴用于在终端中设置环境变量的命令，然后按 **Enter** 键。

 
 

## 在哪里可以获取集群名称和集群标识？
{: #qa3}

要通过 UI 获取集群名称和标识，请完成以下步骤：

1. 登录到 {{site.data.keyword.Bluemix_notm}} 帐户。

    可以在以下网址处找到 {{site.data.keyword.Bluemix_notm}} 仪表板：[http://bluemix.net ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](http://bluemix.net){:new_window}。
    
	使用用户标识和密码登录后，{{site.data.keyword.Bluemix_notm}} UI 即会打开。

2. 在 {{site.data.keyword.Bluemix_notm}} *仪表板*中，选择**菜单 > 容器**。

    这将显示帐户中可用的集群列表。



3. 要获取集群标识，请选择一个集群条目。 

    这将打开“概述”页面。在此页面中，可以获取集群标识。







要通过命令行获取集群名称和标识，请完成以下步骤：



1. 登录到 {{site.data.keyword.Bluemix_notm}} 中与已创建集群关联的区域、组织和空间。有关更多信息，请参阅[如何登录到 {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login)。

2. 列出帐户中可用的集群。运行以下命令： 

    ```
	ibmcloud cs clusters
	``` 
	{: codeblock}
	
	此命令的输出列出帐户中所有集群及其相应标识。
	

	
3. 要获取集群标识，请运行以下命令：

    ```
	ibmcloud cs cluster-get my_cluster
	```
    {: screen}	
 


## 如何获取名称空间的列表？
{: #qa7}

要获取集群中所有名称空间的列表，请完成以下步骤：

请完成以下步骤：

1. 设置集群上下文。有关更多信息，请参阅[如何在终端会话中设置集群环境？](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-qa_containers#qa1)。

2. 列出所有名称空间。运行以下 kubectl 命令：

    

    ```
    kubectl get namespaces
	```
	{: codeblock}

## 如何获取 Kubernetes 集群中每个名称空间的 pod 列表？
{: #qa8}
		
要获取名称空间中的 pod 列表，请完成以下步骤：



1. 设置集群上下文。有关更多信息，请参阅[如何在终端会话中设置集群环境？](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-qa_containers#qa1)。

2. 要获取 Kubernetes 集群中每个名称空间的 pod 列表，请运行以下命令：

    ```
	kubectl --namespace=NamespaceName get pods 
	```
	{: codeblock}
	
	其中，Namespacename 是名称空间的名称，例如 *default*。

## 如何按名称空间获取集群中的所有 pod？
{: #qa9}
		
请完成以下步骤：

1. 设置集群上下文。有关更多信息，请参阅[如何在终端会话中设置集群环境？](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-qa_containers#qa1)。
	
2. 要按名称空间获取集群中的所有 pod，请运行以下命令：

	```
	kubectl get pods --all-namespaces
	```
	{: codeblock}
		


