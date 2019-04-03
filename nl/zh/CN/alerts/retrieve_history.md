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


# 使用警报 API 检索警报的历史记录
{: #retrieve_history}

使用警报 API 可检索警报的历史记录。 
{:shortdesc}


要使用警报 API 来检索警报的历史记录，请完成以下步骤：

1. 登录到 {{site.data.keyword.Bluemix_notm}} 中的区域、组织和空间。 

    有关更多信息，请参阅[如何登录到 {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login)。

2. 获取安全性令牌。 您可以使用 UAA 令牌、IAM 令牌或 API 密钥。 选择下列其中一种方法来获取安全性令牌：
	
	* 要获取 UAA 令牌，请参阅[使用 {{site.data.keyword.Bluemix_notm}} CLI 获取 UAA 令牌](/docs/services/cloud-monitoring/security/auth_uaa.html#uaa_cli)。
	
	* 要获取 IAM 令牌，请参阅[使用 {{site.data.keyword.Bluemix_notm}} CLI 获取 IAM 令牌](/docs/services/cloud-monitoring/security/auth_iam.html#auth_iam)。
	
	* 要获取 API 密钥，请参阅[获取 API 密钥](/docs/services/cloud-monitoring/security/auth_api_key.html#auth_api_key)。
	
	通过您登录到 {{site.data.keyword.Bluemix_notm}} 的相同终端，为令牌设置 Token 变量。

    例如，要使用 IAM 令牌，请运行以下命令：

    ```
	ibmcloud iam oauth-tokens
	```
	{: codeblock}
	
	此命令的结果如下所示：
	
	```
	IAM token:  Bearer djn.._l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	然后，导出变量 *Token*：
	
	```
	export Token="djn.._l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ"
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
	
	然后，导出变量 *Space*。 **注：**GUID 必须以 *s-* 为前缀以标识空间。
	
	例如：
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. 检索规则的历史记录。

    * 要按规则的名称检索规则的历史记录，请参阅[使用规则名称检索规则的历史记录](/docs/services/cloud-monitoring/alerts/retrieve_history.html#by_name)。
	* 要检索一段时间的规则历史记录，请参阅[检索最近 48 小时的规则历史记录](/docs/services/cloud-monitoring/alerts/retrieve_history.html#by_time)。
	* 要从规则的历史记录中检索多个条目，请参阅[检索规则的历史记录中的最后 3 个条目](/docs/services/cloud-monitoring/alerts/retrieve_history.html#number)。
	
	
## 按规则名称检索规则的历史记录
{: #by_name}
	
运行以下 cURL 命令来获取警报的历史记录：

```
curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/history?rule_name=RULE_NAME
```
{: codeblock}
	
其中
	
* *X-Auth-User-Token* 是用于传递 UAA 令牌、IAM 令牌或 API 密钥的参数。
	
* *Auth_Type* 是用于定义令牌或 API 密钥的类型的前缀。 以下列表列出了有效值：*apikey*、*iam* 或 *uaa*，其中：

    * *apikey* 表明令牌是 API 密钥。
	* *iam* 表明指定的令牌是 IAM 生成的令牌。
	* *uaa* 表明指定的令牌是 UAA 生成的令牌。
	
* *X-Auth-Scope-Id* 是用于传递空间 GUID 的参数。 GUID 必须以 *s-* 为前缀以标识空间。 如果使用 UAA 认证令牌，此头是必需的。 如果使用 IAM 认证令牌，那么此头是可选的，并且将使用绑定到该令牌的域信息。
	
* *Token* 是 UAA 或 IAM 认证令牌或者 API 密钥。
	
* *Space* 是空间的 GUID。 
	
* *RULE_NAME* 是用于触发警报的规则的名称。 值为在 *name* 字段中指定的名称。
	
* *METRICS_ENDPOINT* 表示服务的入口点。 每个区域都有不同的 URL。 要获取每个区域的端点列表，请参阅[端点](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints)。
	
    
例如，规则 `highNginxCPU` 的历史记录如下所示：

```
curl -XGET --header "X-Auth-User-Token: iam ${Token}" --header "X-Auth-Scope-Id: ${Space}" https://metrics.ng.bluemix.net/v1/alert/history?rule_name=highNginxCPU
```
{: screen}

```
[
 {
 "rule": "highNginxCPU",
 "timestamp": "2017-04-17T22.23.21.000",
 "value": 99.5,
 "from_level": "OK",
 "to_level": "ERROR"
 },
 {
 "rule": "highNginxCPU",
 "timestamp": "2017-04-17T10.11.12.123",
 "value": 98.5,
 "from_level" : "OK",
 "to_level": "WARN"
 },
 {
 "rule": "highNginxCPU",
 "timestamp": "2017-04-17T10.12.14.000",
 "value": 97.0,
 "from_level" : "WARN",
 "to_level": "OK"
 }
]
```
{: screen}


## 检索最近 48 小时的规则历史记录
{: #by_time}

运行以下 cURL 命令以获取最近 48 小时的警报历史记录：

```
curl -H "X-Auth-User-Token: iam $Token" -H "X-Auth-Scope-Id:$Space" METRICS_ENDPOINT/v1/alert/history?start=-48h
```
{: codeblock}

其中
	
* *X-Auth-User-Token* 是用于传递 UAA 令牌、IAM 令牌或 API 密钥的参数。
	
* *Auth_Type* 是用于定义令牌或 API 密钥的类型的前缀。 以下列表列出了有效值：*apikey*、*iam* 或 *uaa*，其中：

    * *apikey* 表明令牌是 API 密钥。
	* *iam* 表明指定的令牌是 IAM 生成的令牌。
	* *uaa* 表明指定的令牌是 UAA 生成的令牌。
	
* *X-Auth-Scope-Id* 是用于传递空间 GUID 的参数。 GUID 必须以 *s-* 为前缀以标识空间。 如果使用 UAA 认证令牌，此头是必需的。 如果使用 IAM 认证令牌，那么此头是可选的，并且将使用绑定到该令牌的域信息。
	
* *Token* 是 UAA 或 IAM 认证令牌或者 API 密钥。
	
* *Space* 是空间的 GUID。 
	
* *RULE_NAME* 是用于触发警报的规则的名称。 值为在 *name* 字段中指定的名称。
	
* *METRICS_ENDPOINT* 表示服务的入口点。 每个区域都有不同的 URL。 要获取每个区域的端点列表，请参阅[端点](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints)。
	

## 检索规则的历史记录中的最后 3 个条目
{: #number}

运行以下 cURL 命令以获取警报历史记录中的最后 3 个条目：

```
curl -H "X-Auth-User-Token: iam $Token" -H "X-Auth-Scope-Id:$Space" METRICS_ENDPOINT/v1/alert/history?max_results=3
```
{: codeblock}

其中
	
* *X-Auth-User-Token* 是用于传递 UAA 令牌、IAM 令牌或 API 密钥的参数。
	
* *Auth_Type* 是用于定义令牌或 API 密钥的类型的前缀。 以下列表列出了有效值：*apikey*、*iam* 或 *uaa*，其中：

    * *apikey* 表明令牌是 API 密钥。
	* *iam* 表明指定的令牌是 IAM 生成的令牌。
	* *uaa* 表明指定的令牌是 UAA 生成的令牌。
	
* *X-Auth-Scope-Id* 是用于传递空间 GUID 的参数。 GUID 必须以 *s-* 为前缀以标识空间。 如果使用 UAA 认证令牌，此头是必需的。 如果使用 IAM 认证令牌，那么此头是可选的，并且将使用绑定到该令牌的域信息。
	
* *Token* 是 UAA 或 IAM 认证令牌或者 API 密钥。
	
* *Space* 是空间的 GUID。 
	
* *RULE_NAME* 是用于触发警报的规则的名称。 值为在 *name* 字段中指定的名称。
	
* *METRICS_ENDPOINT* 表示服务的入口点。 每个区域都有不同的 URL。 要获取每个区域的端点列表，请参阅[端点](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints)。
	
