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


# 使用 {{site.data.keyword.monitoringshort}} API 配置 Webhook 警报
{: #configure_webhook_alert}

要针对度量值配置 Webhook 警报，请定义规则和 Webhook 通知。 然后，向 {{site.data.keyword.monitoringshort}} 服务注册规则和通知方法。
{:shortdesc}

请完成以下步骤：

## 步骤 1：创建规则
{: #step14}

为您在 Grafana 中定义的度量值查询创建规则。 有关更多信息，请参阅[创建规则](/docs/services/cloud-monitoring/alerts/rules.html#create)。

例如，在 `~/cloud-monitoring/rules/` 目录中创建 `s-rule-1.json` 规则文件。 

```
{
    "name": "RULE_NAME",
    "description": "MH check Bytes In per second",
    "expression": "movingAverage(messagehub.65qser11-8034-1234-5678-c82fb42wdfgh.1.kafka-java-console-sample-topic.BytesInPerSec.15MinuteRate,\"5min\")",
    "enabled": true,
    "from": "-5min",
    "until": "now",
    "comparison": "above",
    "comparison_scope": "last",
    "error_level" : 27,
    "warning_level" : 25,
    "frequency": "1min",
    "dashboard_url": "https://metrics.ng.bluemix.net",
    "notifications": [
      "NOTIFICATION_NAME"
    ]
}
```
{: screen}

然后，导出变量 *RULE_FILE*：
	
```
export RULE_FILE="s-rule-1.json"
```
{: screen}

## 步骤 2：在 Monitoring 服务中注册规则
{: #step23}
	
通过终端，完成以下步骤：

1. 登录到 {{site.data.keyword.Bluemix_notm}} 中的区域、组织和空间。 

    有关更多信息，请参阅[如何登录到 {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login)。

2. 获取安全性令牌。 您可以使用 UAA 令牌、IAM 令牌或 API 密钥。 选择下列其中一种方法来获取安全性令牌：
	
	* 要获取 UAA 令牌，请参阅[使用 {{site.data.keyword.Bluemix_notm}} CLI 获取 UAA 令牌](/docs/services/cloud-monitoring/security/auth_uaa.html#uaa_cli)。
	
	* 要获取 IAM 令牌，请参阅[使用 {{site.data.keyword.Bluemix_notm}} CLI 获取 IAM 令牌](/docs/services/cloud-monitoring/security/auth_iam.html#auth_iam)。
	
	* 要获取 API 密钥，请参阅[获取 API 密钥](/docs/services/cloud-monitoring/security/auth_api_key.html#auth_api_key)。
	
	例如，要使用 IAM 令牌，请运行以下命令：

    ```
	ibmcloud iam oauth-tokens
	```
	{: codeblock}
	
	此命令的结果如下所示：
	
	```
	IAM token:  Bearer djn.._l_HWtlNTibmcloudslibmclouds0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	然后，导出变量 *Token*：
	
	```
	export Token="djn.._l_HWtlNTibmcloudslibmclouds0qjBI9GqCnuQ"
	```
	{: screen}
	
	**注：**令牌不包含 *Bearer*。
	
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
	
	然后，导出变量 *Space*：
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. 运行以下 cURL 命令来注册规则：
	
    ```
	curl -XPOST -d @$RULE_FILE --header "X-Auth-User-Token: Auth_Type ${Token}" METRICS_ENDPOINT/v1/alert/rule
	```
	{: screen}
	
	其中
	
	* RULE_FILE 是定义警报规则的 JSON 文件。
	
	* *X-Auth-User-Token* 是用于传递 {{site.data.keyword.Bluemix_notm}} UAA 令牌、IAM 令牌或 API 密钥的参数。
	
	* *Auth_Type* 是用于定义令牌或 API 密钥的类型的前缀。 以下列表列出了有效值：*apikey*、*iam* 或 *uaa*，其中：

        * *apikey* 表明令牌是 API 密钥。
		* *iam* 表明指定的令牌是 IAM 生成的令牌。
		* *uaa* 表明指定的令牌是 UAA 生成的令牌。
	
	* *X-Auth-Scope-Id* 是用于传递空间 GUID 的参数。 GUID 必须以 *s-* 为前缀以标识空间。 如果使用 UAA 认证令牌，此头是必需的。 如果使用 IAM 认证令牌，那么此头是可选的，并且将使用绑定到该令牌的域信息。
	
	* Token 是 UAA 或 IAM 认证令牌或者 API 密钥。
	
	* Space 是空间的 GUID。 
	
	* METRICS_ENDPOINT 表示服务的入口点。 每个区域都有不同的 URL。 要获取每个区域的端点列表，请参阅[端点](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints)。
	
	要验证规则是否已成功创建，请运行以下命令：
	
	```
	curl -XGET --header "X-Auth-User-Token:iam ${Token}" METRICS_ENDPOINT/v1/alert/rule/checkbytesin
	```
	{: codeblock}
	
	例如：

    ```
	curl -XGET --header "X-Auth-User-Token:iam ${Token}" https://metrics.ng.bluemix.net/v1/alert/rule/checkbytesin
	```
	{: screen}

## 步骤 3：创建 Webhook 通知
{: #step32}


要创建通知文件，请考虑以下信息：

* 对 Webhook 警报使用通知模板。 有关更多信息，请参阅[通知模板](/docs/services/cloud-monitoring/config_alerts_ov.html#notification_template)。
* 在本地目录中创建该文件，例如，`~/cloud-monitoring/notifications`。

例如，使用 vi 编辑器创建 **webhook.json** 文件： 
	
```
{
"name": "NOTIFICATION_NAME",
"type": "Webhook",
"description" : "Fire this webhook when ....",
"detail": "https://myendpoint.bluemix.net?key=abcd1234"
}
```
{: codeblock}	

为了调用 Webhook，必须将 *detail* 字段设置为应该执行 POST 操作的 URL。 为 HTTPS 端点配置 Webhook 并添加参数。
	
有关更多信息，请参阅[创建通知](/docs/services/cloud-monitoring/alerts/notifications.html#notifications_create)。
	
## 步骤 4：在 Monitoring 服务中注册通知方法
{: #step42}
	
通过终端，完成以下步骤：

1. 登录到 {{site.data.keyword.Bluemix_notm}} 中的区域、组织和空间。 

    有关更多信息，请参阅[如何登录到 {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login)。

2. 获取安全性令牌。 您可以使用 UAA 令牌、IAM 令牌或 API 密钥。 选择下列其中一种方法来获取安全性令牌：
	
	* 要获取 UAA 令牌，请参阅[使用 {{site.data.keyword.Bluemix_notm}} CLI 获取 UAA 令牌](/docs/services/cloud-monitoring/security/auth_uaa.html#uaa_cli)。
	
	* 要获取 IAM 令牌，请参阅[使用 {{site.data.keyword.Bluemix_notm}} CLI 获取 IAM 令牌](/docs/services/cloud-monitoring/security/auth_iam.html#auth_iam)。
	
	* 要获取 API 密钥，请参阅[获取 API 密钥](/docs/services/cloud-monitoring/security/auth_api_key.html#auth_api_key)。
	
	例如，要使用 IAM 令牌，请运行以下命令：

    ```
	ibmcloud iam oauth-tokens
	```
	{: codeblock}
	
	此命令的结果如下所示：
	
	```
	IAM token:  Bearer djn.._l_HWtlNTibmcloudslibmclouds0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	然后，导出变量 *Token*：
	
	```
	export Token="djn.._l_HWtlNTibmcloudslibmclouds0qjBI9GqCnuQ"
	```
	{: screen}
	
	**注：**令牌不包含 *Bearer*。
	
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
	
	然后，导出变量 *Space*：
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. 运行以下 cURL 命令来注册通知：

    ```
	curl -XPOST -d @$NOTIFICATION_FILE --header "X-Auth-User-Token: Auth_Type ${Token}" METRICS_ENDPOINT/v1/alert/notification
	```
	{: screen}
	
	其中
	
	* NOTIFICATION_FILE 是用于定义通知的 JSON 文件。
	
	* *X-Auth-User-Token* 是用于传递 {{site.data.keyword.Bluemix_notm}} UAA 令牌、IAM 令牌或 API 密钥的参数。
	
	* *Auth_Type* 是用于定义令牌或 API 密钥的类型的前缀。 以下列表列出了有效值：*apikey*、*iam* 或 *uaa*，其中：

        * *apikey* 表明令牌是 API 密钥。
		* *iam* 表明指定的令牌是 IAM 生成的令牌。
		* *uaa* 表明指定的令牌是 UAA 生成的令牌。
	
	* *X-Auth-Scope-Id* 是用于传递空间 GUID 的参数。 GUID 必须以 *s-* 为前缀以标识空间。 如果使用 UAA 认证令牌，此头是必需的。 如果使用 IAM 认证令牌，那么此头是可选的，并且将使用绑定到该令牌的域信息。
	
	* Token 是 UAA 或 IAM 认证令牌或者 API 密钥。
	
	* Space 是空间的 GUID。 
	
	* METRICS_ENDPOINT 表示服务的入口点。 每个区域都有不同的 URL。 要获取每个区域的端点列表，请参阅[端点](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints)。
	
    要验证通知是否已成功创建，请运行以下命令：

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" METRICS_ENDPOINT/v1/alert/notification/NOTIFICATION_NAME
	```
	{: screen}
	


    
   
  


 
	  
