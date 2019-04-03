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



# 删除警报
{: #delete_alerts}

您可以使用 [警报 API](https://console.bluemix.net/apidocs/940-ibm-cloud-monitoring-alerts-api?&language=node#introduction){: new_window} 从 {{site.data.keyword.monitoringshort}} 服务删除警报。
{:shortdesc}


在您[登录到 {{site.data.keyword.Bluemix_notm}} 中的一个区域](/docs/services/cloud-monitoring/qa/cli_qa.html#login)后，完成以下步骤来删除通知：


## 步骤 1：获取安全性令牌
{: #step1_delete_alerts}

您可以使用 UAA 令牌、IAM 令牌或 API 密钥。 

选择下列其中一种方法来获取安全性令牌：
	
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
IAM token:  Bearer djn.._l_HWtlNTibmcloudsl0qjBI9GqCnuQ
UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
```
{: screen}
	
然后，导出变量 *Token*：
	
```
export Token="djn.._l_HWtlNTibmcloudslibmclouds0qjBI9GqCnuQ"
```
{: screen}
	
**注：**令牌不包含 *Bearer*。
	

## 步骤 2：获取空间标识 
{: #step2_delete_alerts}

仅当您想要删除空间域中可用的警报时，才使用此步骤。

要获取空间 GUID，请运行以下命令：
	
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
	
然后，导出变量 *Space*。 GUID 必须以 *s-* 为前缀以标识空间。
	
```
export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
```
{: screen}

	

## 步骤 3：列出规则
{: #step3_delete_alerts}


运行以下 cURL 命令来列出空间域中定义的规则：

```
curl -H "X-Auth-Scope-Id: ${Space}" -H “X-Auth-User-Token: Auth_Type ${TOKEN}" -XGET METRICS_ENDPOINT/v1/alert/rules

```
{: screen}

运行以下 cURL 命令来列出帐户域中的通知：

```
curl -H "X-Auth-User-Token: apikey ${TOKEN}" -XGET METRICS_ENDPOINT/v1/alert/rules
```
{: screen}

其中
	
* *X-Auth-User-Token* 是用于传递 {{site.data.keyword.Bluemix_notm}} UAA 令牌、IAM 令牌或 API 密钥的参数。
	
* *Auth_Type* 是用于定义令牌或 API 密钥的类型的前缀。 以下列表列出了有效值：*apikey*、*iam* 或 *uaa*，其中：

    * *apikey* 表明令牌是 API 密钥。
	* *iam* 表明指定的令牌是 IAM 生成的令牌。
	* *uaa* 表明指定的令牌是 UAA 生成的令牌。
	
* *X-Auth-Scope-Id* 是用于传递空间 GUID 的参数。 GUID 必须以 *s-* 为前缀以标识空间。 
	
* Token 是 UAA 或 IAM 认证令牌或者 API 密钥。
	
* Space 是空间的 GUID。 
	
* METRICS_ENDPOINT 表示服务的入口点。 每个区域都有不同的 URL。 要获取每个区域的端点列表，请参阅[端点](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints)。


## 步骤 4：删除警报规则
{: #step4_delete_alerts}
  

运行以下 cURL 命令来删除空间域中的规则：

```
curl -H "X-Auth-Scope-Id: ${Space}" -H “X-Auth-User-Token: Auth_Type ${TOKEN}" -XDELETE METRICS_ENDPOINT/v1/alert/rule/{name} 
```
{: screen}

运行以下 cURL 命令来删除帐户域中的规则：

```
curl -H "X-Auth-User-Token: apikey ${TOKEN}" -XDELETE METRICS_ENDPOINT/v1/alert/rule/{name} 
```
{: screen}

	
其中
	
* *X-Auth-User-Token* 是用于传递 {{site.data.keyword.Bluemix_notm}} UAA 令牌、IAM 令牌或 API 密钥的参数。
	
* *Auth_Type* 是用于定义令牌或 API 密钥的类型的前缀。 以下列表列出了有效值：*apikey*、*iam* 或 *uaa*，其中：

    * *apikey* 表明令牌是 API 密钥。
	* *iam* 表明指定的令牌是 IAM 生成的令牌。
	* *uaa* 表明指定的令牌是 UAA 生成的令牌。
	
* *X-Auth-Scope-Id* 是用于传递空间 GUID 的参数。 GUID 必须以 *s-* 为前缀以标识空间。 
	
* Token 是 UAA 或 IAM 认证令牌或者 API 密钥。
	
* Space 是空间的 GUID。 
	
* METRICS_ENDPOINT 表示服务的入口点。 每个区域都有不同的 URL。 要获取每个区域的端点列表，请参阅[端点](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints)。

* *name* 是要删除的规则的名称。
	
