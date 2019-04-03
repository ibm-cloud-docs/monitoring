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


# 在 Grafana 中分析 Kubernetes 集群的度量值
{: #container_service_metrics}

使用本教程可了解如何使用 {{site.data.keyword.monitoringlong}} 服务来监视容器的性能。 
{:shortdesc}


## 目标
{: #ks_objectives}

了解如何对部署在 Kubernetes 集群中的应用程序进行容器度量值的搜索和分析：

1. 确定将集群中收集的度量值转发到 {{site.data.keyword.monitoringshort}} 服务的位置。 
2. 启动 Grafana 并设置可以在其中查看集群度量值的 {{site.data.keyword.monitoringshort}} 域。
3. 在 {{site.data.keyword.Bluemix_notm}} 中对部署在 Kubernetes 集群中的应用程序进行容器度量值的搜索和分析。

本教程将逐步执行在 {{site.data.keyword.Bluemix_notm}} 中运行以下端到端场景所需的步骤：供应集群，确定集群将度量值发送到 {{site.data.keyword.Bluemix_notm}} 中 {{site.data.keyword.monitoringshort}} 服务的位置，在集群中部署应用程序，以及使用 Grafana 来查看和过滤该集群的容器度量值。


**注：**要完成本教程，您必须完成不同步骤中链接的先决条件和教程。


## 先决条件
{: #ks_prereqs}

1. 您必须是 {{site.data.keyword.Bluemix_notm}} 帐户的成员或所有者，并有权创建 Kubernetes 标准集群、将应用程序部署到集群以及查询 {{site.data.keyword.Bluemix_notm}} 中的度量值以在 Grafana 中进行监视。

    您的 {{site.data.keyword.Bluemix_notm}} 用户标识必须分配有以下策略：
    
    * 具有 {{site.data.keyword.containershort}} 的*操作员*或*管理员*许可权的 IAM 策略。
    
    有关更多信息，请参阅[通过 IBM Cloud UI 向用户分配 IAM 策略](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-grant_permissions#assign_policy_ui)。

2. 打开终端会话，您可以在其中通过命令行来管理 Kubernetes 集群和部署应用程序。 本教程中提供的示例适用于 Ubuntu Linux 系统。

3. 安装 CLI 以在 Ubuntu 系统中使用 {{site.data.keyword.containershort}}。

    * 安装 {{site.data.keyword.Bluemix_notm}} CLI。 
    * 安装 {{site.data.keyword.containershort}} CLI 以在 {{site.data.keyword.containershort}} 中创建和管理 Kubernetes 集群，以及将容器化应用程序部署到集群中。
    
    有关更多信息，请参阅[安装 {{site.data.keyword.Bluemix_notm}} CLI](/docs/cli?topic=cloud-cli-ibmcloud-cli#overview)。
    
    

    
 

## 步骤 1：供应 Kubernetes 集群
{: #ks_step1}

请完成以下步骤：

1. 创建标准 Kubernetes 集群。 有关更多信息，请参阅[创建 Kubernetes 标准集群](/docs/containers?topic=containers-cs_cluster_tutorial#cs_cluster_tutorial)。

2. 在终端中设置集群上下文。 设置上下文后，您可以管理 Kubernetes 集群并在 Kubernetes 集群中部署应用程序。

    登录到 {{site.data.keyword.Bluemix_notm}} 中与已创建集群关联的区域、组织和空间。 有关更多信息，请参阅[如何登录到 {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa?topic=cloudloganalysis-cli_qa#login)。

	初始化 {{site.data.keyword.containershort}} 服务插件。

	```
	ibmcloud cs init
	```
	{: codeblock}

    将终端上下文设置为您的集群。
    
	```
	ibmcloud cs cluster-config MyCluster
	```
	{: codeblock}

    运行此命令的输出提供了必须在终端中运行以设置配置文件路径的命令。 例如：

	```
	export KUBECONFIG=/Users/ibm/.bluemix/plugins/container-service/clusters/MyCluster/kube-config-hou02-MyCluster.yml
	```
	{: codeblock}

    复制并粘贴用于在终端中设置环境变量的命令，然后按 **Enter** 键。



## 步骤 2：授予用户查看帐户域中度量值的许可权
{: #ks_step2}

要授予用户查看帐户域中度量值的许可权，您必须为该用户分配具有 {{site.data.keyword.monitoringshort}} 服务的**查看者**角色的 IAM 策略。

完成以下步骤以授予用户使用 {{site.data.keyword.monitoringshort}} 服务的许可权：

1. 登录到 {{site.data.keyword.Bluemix_notm}} 控制台。

    打开 Web 浏览器并启动 {{site.data.keyword.Bluemix_notm}}“仪表板”：[http://bluemix.net ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](http://bluemix.net){:new_window}
	
	使用用户标识和密码登录后，{{site.data.keyword.Bluemix_notm}} UI 即会打开。

2. 从菜单栏中，单击**管理 > 帐户 > 用户**。 

    *用户*窗口将显示一个用户列表，其中包含当前选定帐户的电子邮件地址。
	
3. 如果用户是帐户的成员，请从列表中选择用户名，或从*操作*菜单中单击**管理用户**。

    如果用户不是帐户的成员，请参阅[邀请用户](/docs/iam?topic=iam-iamuserinv#iamuserinv)。

4. 选择**访问策略 > 分配访问权 > 分配对资源的访问权**。

5. 选择服务 **{{site.data.keyword.monitoringlong}}**，选择集群在其中可用的区域（对于本教程为**美国南部**），然后选择**查看者**角色。



## 步骤 3：授予 {{site.data.keyword.containershort_notm}} 密钥所有者许可权
{: #ks_step3}

要使集群能够将度量值转发到帐户域，{{site.data.keyword.containershort}} 密钥所有者必须拥有以下 IAM 策略：

* 具有 {{site.data.keyword.monitoringshort}} 服务的**编辑者**许可权的 IAM 策略。
* 具有 {{site.data.keyword.containershort}} 的**管理员**许可权的 IAM 策略。


要授予 {{site.data.keyword.containershort}} 密钥所有者许可权，请完成以下步骤：

1. 登录到 {{site.data.keyword.Bluemix_notm}} 控制台。

    打开 Web 浏览器并启动 {{site.data.keyword.Bluemix_notm}}“仪表板”：[http://bluemix.net ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](http://bluemix.net){:new_window}
	
	使用用户标识和密码登录后，{{site.data.keyword.Bluemix_notm}} UI 即会打开。

2. 从菜单栏中，单击**管理 > 帐户 > 用户**。 

    *用户*窗口将显示一个用户列表，其中包含当前选定帐户的电子邮件地址。
	
3. 找到 {{site.data.keyword.containershort}} 密钥所有者用户标识。

    运行 `ibmcloud cs api-key-info ClusterName` 命令以获取 {{site.data.keyword.containershort}} 密钥所有者用户标识。

4. 选择**访问策略 > 分配访问权 > 分配对资源的访问权**。

5. 选择服务 **{{site.data.keyword.monitoringlong}}**，选择集群在其中可用的区域（对于本教程为**美国南部**），然后选择**编辑者**角色。	

6. 重复步骤 2 到 4，并选择服务 {{site.data.keyword.containershort}}。 选择**所有区域**，并选择**管理员**角色。	




## 步骤 4：在 Kubernetes 集群中部署样本应用程序
{: #ks_step4}

在 Kubernetes 集群中部署并运行样本应用程序。 完成以下教程中的步骤以部署样本应用程序：[第 1 课：将单实例应用程序部署到 Kubernetes 集群](/docs/containers?topic=containers-cs_apps_tutorial#cs_apps_tutorial_lesson1)。

该应用程序是 Hello World Node.js 应用程序：

```
var express = require('express')
var app = express()

app.get('/', function(req, res) {
  res.send('Hello world! Your app is up and running in a cluster!\n')
})
app.listen(8080, function() {
  console.log('Sample app is listening on port 8080.')
})
```
{: screen}

在此样本应用程序中，当您在浏览器中测试应用程序时，应用程序会将以下消息写入 stdout：`Sample app is listening on port 8080.`


## 步骤 5：启动 Grafana 并设置度量值域
{: #ks_step5}

通过浏览器启动 Grafana，并设置可以在其中查看集群度量值的 {{site.data.keyword.monitoringshort}} 域。

要分析集群的度量值，您必须在创建集群的云公共区域中访问 Grafana。 有关更多信息，请参阅[通过 Web 浏览器导航至 Grafana 仪表板](/docs/services/cloud-monitoring/grafana?topic=cloud-monitoring-navigating_grafana#launch_grafana_from_browser)。

1. 通过浏览器启动 Grafana。 

    输入创建集群的区域的 {{site.data.keyword.monitoringshort}} 服务 URL。 
    
    要获取每个区域的 URL，请参阅 [Monitoring 服务的 URL](/docs/services/cloud-monitoring?topic=cloud-monitoring-monitoring_ov#region)。

    例如，对于美国南部区域，请启动：[https://metrics.ng.bluemix.net/](https://metrics.ng.bluemix.net/)。

2. 将 {{site.data.keyword.monitoringshort}} 域设置为**帐户**。

    在 Grafana 中，选择您的标识。 接着，检查您是否位于正确的帐户中，然后选择一个域。 选择 `Domain = account`。

    集群会将度量值转发到帐户度量值域。 

## 步骤 6：在 Grafana 中监视集群
{: #ks_step6}

{{site.data.keyword.containershort}} 提供了一个 Grafana 仪表板，可以用于监视集群度量值。 

要打开样本仪表板，请完成以下步骤：

1. 选择侧菜单栏切换 ![Grafana 侧菜单栏](images/grafana_settings.gif "Grafana 侧菜单栏")。
2. 选择**仪表板**。
3. 单击**打开**。
4. 选择 **ClusterMonitoringDashboard_v1**。

这将打开样本仪表板。 

![Grafana 样本仪表板](images/cluster_grafana_sample_dashboard.png "Grafana 样本仪表板")



## 后续步骤
{: #ks_next_steps}

为度量值定义警报。 有关更多信息，请参阅[配置警报](/docs/services/cloud-monitoring?topic=cloud-monitoring-config_alerts_ov#config_alerts_ov)。
