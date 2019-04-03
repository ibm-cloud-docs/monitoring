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


# 在 Grafana 中配置度量值查询
{: #define_query}

在 {{site.data.keyword.Bluemix}} 中，将通过所选云服务自动收集度量值。要通过 {{site.data.keyword.monitoringlong}} 监视这些度量值，必须定义 Grafana 查询。
{:shortdesc}

## 步骤 1：收集要监视的 CF 应用程序或服务的数据
{: #step18}

获取要监视的 CF 应用程序或服务的以下信息：

* **区域** - 运行 CF 应用程序的区域。
* **组织** - 运行 CF 应用程序的组织。 	
* **空间** - 运行 CF 应用程序的空间。 
* **CF 应用程序名称**（要监视的 CF 应用程序的名称）或**服务名称**。 


## 步骤 2：启动 Grafana
{: #step27}

通过浏览器启动 Grafana。有关更多信息，请参阅[通过 Web 浏览器导航至 Grafana 仪表板](/docs/services/cloud-monitoring/grafana?topic=cloud-monitoring-navigating_grafana#launch_grafana_from_browser)。

确保在 Grafana 中登录到运行 CF 应用程序或服务的帐户、组织和区域。 


## 步骤 3：在 Grafana 中定义查询
{: #step36}

要创建 Grafana 仪表板并定义查询，请完成以下步骤：

1. 创建新的仪表板。

    * 选择侧菜单栏切换控件 ![Grafana 侧菜单栏](images/grafana_settings.gif "Grafana 侧菜单栏")。
    * 选择**仪表板**。
    * 单击**新建**。

    这将打开仪表板。仪表板包含一个空行，可随时用于配置。

2. 添加*图形*面板。

    1. 选择**图形**。

    2. 单击图形标题，然后选择**编辑**。

        这将打开*度量值*选项卡。在此可以看到缺省数据源。

3. 定义用于过滤图形中所显示数据的查询。 

    在*度量值*选项卡中，选择**添加查询**。<br>这将添加一个查询条目。每个查询都会使用一个字母进行标记。
    
    ![新建查询条目](images/grafana4_query_f1.gif "新建查询条目")
        
    1. 单击**选择度量值**，然后选择源：`ibmcloud`。
    
    2. 单击**选择度量值**，然后选择云类型：`public`。
    
    3. 单击**选择度量值**，然后选择服务名称，例如 `cloud-foundry` 用于收集 CF 应用程序度量值，`message hub` 用于收集 {{site.data.keyword.messagehub}} 度量值。
    
    4. 单击**选择度量值**，然后选择您在其中工作的区域，例如 `ng` 表示美国南部区域。
    
    5. 选择应用于要监视的服务或 CF 应用程序的特定服务字段。

        <table>
          <caption>每个服务或 CF 应用程序的度量值查询格式</caption>
          <tr>
            <th>服务名称</th>
            <th>度量值查询格式的链接</th> 
          </tr>
          <tr>
            <td>{{site.data.keyword.containershort_notm}}</td>
            <td>[为容器收集的 CPU 度量值的查询格式](/docs/services/cloud-monitoring/reference?topic=cloud-monitoring-metrics_format_containers#cpu_containers) </br>[为工作程序收集的负载度量值的查询格式](/docs/services/cloud-monitoring/reference?topic=cloud-monitoring-metrics_format_containers#load_workers) </br>[为容器收集的内存度量值的查询格式](/docs/services/cloud-monitoring/reference?topic=cloud-monitoring-metrics_format_containers#mem_containers)</td> 
          </tr>
          <tr>
            <td>CF 应用程序</td>
            <td>[CF 应用程序的查询格式](/docs/services/cloud-monitoring/reference?topic=cloud-monitoring-cfapps_metrics_format#cfapps_metrics_format)</td> 
          </tr>
        </table>

        例如，对于 CF 应用程序，请选择：
    
        单击**选择度量值**，然后选择 CF 应用程序名称，例如 `logtester`。
    
        单击**选择度量值**，然后选择 CF 应用程序实例索引，例如 `0`。

        单击**选择度量值**，然后选择 `container`。
    
    9. 单击**选择度量值**，然后选择度量值类型。例如，**cpu** 表示 CPU 度量值，**memory** 表示内存度量值，**disk** 表示磁盘度量值。 

        **注：**对于 CF 应用程序，请跳过此步骤。 

    10. 单击**选择度量值**，然后选择度量值。 

        <table>
          <caption>每个服务或 CF 应用程序的度量值列表</caption>
          <tr>
            <th>服务名称</th>
            <th>度量值的链接</th> 
          </tr>
          <tr>
            <td>{{site.data.keyword.containershort_notm}}</td>
            <td>[CPU 度量值](/docs/services/cloud-monitoring/cf?topic=cloud-monitoring-cloud-foundry-apps#cpu_metrics) </br>[磁盘度量值](/docs/services/cloud-monitoring/cf?topic=cloud-monitoring-cloud-foundry-apps#disk_metrics)</br>[内存度量值](/docs/services/cloud-monitoring/cf?topic=cloud-monitoring-cloud-foundry-apps#mem_metrics)</td> 
          </tr>
          <tr>
            <td>CF 应用程序</td>
            <td>[CPU 度量值](/docs/services/cloud-monitoring/cf?topic=cloud-monitoring-cloud-foundry-apps#cpu_metrics) </br>[磁盘度量值](/docs/services/cloud-monitoring/cf?topic=cloud-monitoring-cloud-foundry-apps#disk_metrics)</br>[内存度量值](/docs/services/cloud-monitoring/cf?topic=cloud-monitoring-cloud-foundry-apps#mem_metrics)</td> 
          </tr>
          <tr>
            <td>{{site.data.keyword.messagehub}}</td>
            <td>[Kafka 主题的度量值](/docs/services/cloud-monitoring/mh?topic=cloud-monitoring-monitoring_mh_ov#kafka_topic_metrics)</br>[Kafka 分区的度量值](/docs/services/cloud-monitoring/mh?topic=cloud-monitoring-monitoring_mh_ov#kafka_partition_metrics)</td> 
          </tr>
        </table>

    10. 单击加号图像 ![“添加”图标](images/grafana_plus_image.gif "加号图像")，然后选择函数。可以添加函数来对可用于度量值的数据执行变换、组合和计算。
        
        例如，可以添加 **alias(newName)** 函数来为度量值添加别名。此别名用于在图形中所显示的图注中显示字符串，而不显示度量值名称。
        
        要为度量值添加别名，请完成以下步骤：
        
        1. 单击加号。
        2. 选择**特殊**。
        3 选择**别名**。
        4. 输入字符串，例如 `My sample metric`。


## 步骤 4：保存仪表板以供将来复用
{: #step44}

请完成以下步骤：

1. 单击保存仪表板图像 ![保存仪表板图像](images/grafana_save_image.gif "保存仪表板图像")。
2. 输入仪表板的名称。
3. 单击**保存**。
