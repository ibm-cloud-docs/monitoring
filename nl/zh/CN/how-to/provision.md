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


# 供应 Monitoring 服务
{: #provision}

您可以从 {{site.data.keyword.Bluemix}} UI 或从命令行供应 {{site.data.keyword.monitoringshort}} 服务。
{:shortdesc}


## 从 UI 供应
{: #ui}

要在 {{site.data.keyword.Bluemix_notm}} 中供应 {{site.data.keyword.monitoringshort}} 服务的实例，请完成以下步骤：

1. 登录到 {{site.data.keyword.Bluemix_notm}} 帐户。

    可以在以下网址处找到 {{site.data.keyword.Bluemix_notm}} 仪表板：[http://bluemix.net ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](http://bluemix.net){:new_window}。
    
	使用用户标识和密码登录后，{{site.data.keyword.Bluemix_notm}} UI 即会打开。

2. 单击**目录**。{{site.data.keyword.Bluemix_notm}} 上可用的服务列表即会打开。

3. 选择 **DevOps** 类别以过滤显示的服务列表。

4. 单击**监视**磁贴。

5. 选择服务套餐。 

    * 要收集和访问最多 45 天的度量值，以及定义警报规则（包括带有通配符的规则），请选择**高级**套餐。 
	
	* 缺省情况下，会设置 **Lite** 套餐，通过该套餐，您可以收集供应服务所在空间中的平台度量值，并保留这些度量值 15 天。 

    有关服务套餐的更多信息，请参阅[服务套餐](/docs/services/cloud-monitoring/monitoring_ov.html#plan)。
	
6. 单击**创建**以在您登录的 {{site.data.keyword.Bluemix_notm}} 空间中供应 {{site.data.keyword.monitoringshort}} 服务。
  
 

## 从 CLI 供应
{: #cli}

要通过命令行在 {{site.data.keyword.Bluemix_notm}} 中供应 {{site.data.keyword.monitoringshort}} 服务的实例，请完成以下步骤：

1. [先决条件] 安装 {{site.data.keyword.Bluemix_notm}} CLI。

   有关更多信息，请参阅[安装 {{site.data.keyword.Bluemix_notm}} CLI](/docs/cli/index.html#overview)。
   
   如果 CLI 已安装，请继续执行下一步。
    
2. 登录到 {{site.data.keyword.Bluemix_notm}} 中的区域、组织和空间。 

    有关更多信息，请参阅[如何登录到 {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login)。
	
3. 运行 `ibmcloud service create` 命令以供应实例。

    ```
	ibmcloud service create service_name service_plan service_instance_name
	```
	{: codeblock}
    
    其中
    	
    * *service_name* 是 **Monitoring**。
    * *service_plan* 是服务套餐名称。要收集和访问最多 45 天的度量值，以及定义警报规则（包括带有通配符的规则），请选择**高级**套餐。缺省情况下，会设置 **Lite** 套餐，通过该套餐，您可以收集供应服务所在空间中的平台度量值，并保留这些度量值 15 天。有关套餐的列表，请参阅 [{{site.data.keyword.monitoringshort}} 服务套餐](/docs/services/cloud-monitoring/monitoring_ov.html#plan)。
    * *service_instance_name* 是要用于所创建的新服务实例的名称。
    
    例如，要使用高端套餐创建 {{site.data.keyword.monitoringshort}} 服务的实例，请运行以下命令：
	
	
    
	```
	ibmcloud service create Monitoring premium my_monitoring_svc
	```
	{: codeblock}
    
4. 验证是否已成功创建服务。运行以下命令：

    ```	
	ibmcloud service list
	```
	{: codeblock}
	
	运行命令的输出如下所示：
	
	```
    Getting services in org MyOrg / space MySpace as xxx@yyy.com...
    OK
    
    name                           service                  plan                   bound apps              last operation
    my_monitoring_svc              Monitoring               premium                                        create succeeded
	```
	{: screen}

	



