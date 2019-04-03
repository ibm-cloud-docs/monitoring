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

# 使用度量值 API 发送数据
{: #send_data_api}

您可以使用“度量值 API”将度量值发送到 {{site.data.keyword.monitoringshort}} 服务。 
{:shortdesc}


对于 {{site.data.keyword.Bluemix_notm}} Docker 容器，会自动收集基本系统度量值。 对于 Cloud Foundry 应用程序以及在虚拟机 (VM) 中运行的应用程序，必须使用[度量值 API](https://console.bluemix.net/apidocs/927-ibm-cloud-monitoring-rest-api?&language=node#introduction){: new_window} 从应用程序直接发送度量值。 



## 将度量值发送到空间域
{: #space_uaa}

要使用 cURL 将度量值发送到空间，请完成以下步骤：

1. 登录到 {{site.data.keyword.Bluemix_notm}} 中的区域、组织和空间。 

    有关更多信息，请参阅[如何登录到 {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login)。

2. 获取安全性令牌。 您可以使用 UAA 令牌、IAM 令牌或 API 密钥。

    选择下列其中一种方法来获取发送度量值所需的安全性令牌：
	
	* 要获取 UAA 令牌，请参阅[使用 {{site.data.keyword.Bluemix_notm}} CLI 获取 UAA 令牌](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_uaa#uaa_cli)。
	
	* 要获取 IAM 令牌，请参阅[使用 {{site.data.keyword.Bluemix_notm}} CLI 获取 IAM 令牌](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_iam#auth_iam)。
	
	* 要获取 API 密钥，请参阅[获取 API 密钥](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_api_key#auth_api_key)。
	
	通过您登录到 {{site.data.keyword.Bluemix_notm}} 的相同终端，为令牌设置 *Token* 变量。

    例如，设置 UAA 令牌，并从令牌值中除去 *Bearer* 部分：

    ```
    export Token="kjshdgf.....ldkdjdj"
    ```
    {: screen}
		
3. 获取空间 GUID。 GUID 必须以 *s-* 为前缀以标识空间。

    运行以下命令：
	
	```
	ibmcloud iam space SpaceName --guid
	```
	{: codeblock}
	
	其中，*SpaceName* 是要定义通知的空间的名称。
	
	例如，要获取名称为 *dev* 的空间的 GUID，请运行以下命令：
	
	```
	ibmcloud iam space dev --guid
	```
	{: screen}
	
	此命令的结果如下所示：
	
	```
	667fadfc-jhtg-1234-9f0e-cf4123451095
	```
	{: screen}
	
	然后，导出变量 *Space*。 **注：**GUID 必须以 *s-* 为前缀以标识空间。
	
	例如：
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
5. 运行以下 cURL 命令以发送度量值：

    ```
	curl -XPOST -d @Metric_File --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" Endpoint/v1/metrics
	```
	{: codeblock}
	
	其中
	
	* Metrics_File 表示 JSON 文件，其中包含发送到 {{site.data.keyword.monitoringshort}} 服务的度量值的定义。
	
	* *X-Auth-User-Token* 是用于传递安全性令牌的参数。
	
	* *Auth_Type* 是用于定义令牌类型的前缀。 有效值为：*uaa*（代表 UAA 令牌）、*iam*（代表 IAM 令牌）和 *api*（代表 API 密钥）。
	
	* *X-Auth-Scope-Id* 是用于传递空间 GUID 的参数。 GUID 必须以 *s-* 为前缀以标识空间。
	
	* Token 表示安全性令牌或 API 密钥。
	
	* Space 表示空间的 GUID。 
	
	* Endpoint 表示服务的入口点。 每个区域都有不同的 URL。 要获取每个区域的端点列表，请参阅[端点](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints)。
	
	例如，可以运行以下命令将 `myhost.cpu.idle` 和 `myapp.login.attempts` 这两个度量值发送到 {{site.data.keyword.monitoringshort}} 服务：
	
	```
	curl -XPOST @metric.json --header "X-Auth-User-Token: uaa ${Token}" https://metrics.ng.bluemix.net/v1/metrics
	```
	{: screen}
	
	样本文件 *metric.json* 按如下所示进行定义：

    ```
    [
      {
        "name" : "myhost.cpu.idle",
        "value" : 22.37
      },
      {
        "name": "myapp.login.retries",
        "value": 4
      }
    ]
	```
	{: screen}

 











 
