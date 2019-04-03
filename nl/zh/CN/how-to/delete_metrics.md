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



# 删除度量值
{: #delete_metrics}

可以使用[度量值 API](https://console.bluemix.net/apidocs/monitoring-metrics-api) 从 {{site.data.keyword.monitoringshort}} 服务中删除度量值。
{:shortdesc}

在您[登录到 {{site.data.keyword.Bluemix_notm}} 中的一个区域](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login)后，请完成以下步骤来删除通知：


## 步骤 1：获取安全性令牌
{: #step1_delete_metrics}

您可以使用 UAA 令牌、IAM 令牌或 API 密钥。 

选择下列其中一种方法来获取安全性令牌：
	
* 要获取 UAA 令牌，请参阅[使用 {{site.data.keyword.Bluemix_notm}} CLI 获取 UAA 令牌](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_uaa#uaa_cli)。
* 要获取 IAM 令牌，请参阅[使用 {{site.data.keyword.Bluemix_notm}} CLI 获取 IAM 令牌](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_iam#auth_iam)。
* 要获取 API 密钥，请参阅[获取 API 密钥](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_api_key#auth_api_key)。
	
例如，要使用 IAM 令牌，请运行以下命令：

```
ibmcloud iam oauth-tokens
```
{: codeblock}
	
此命令的结果如下所示：
	
```
    IAM token:  Bearer djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
```
{: screen}
	
然后，导出变量 *Token*：
	
```
    export Token="djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ"
```
{: screen}
	
**注：**令牌不包含 *Bearer*。
	
## 步骤 2：验证是否有使用度量值的许可权 
{: #step2_delete_metrics}

根据度量值在其中可用的域，请考虑以下信息：

* 要使用在空间域中可用的度量值，用户需要与该域关联的 Cloud Foundry 空间中的*开发者*角色。 
* 要使用在帐户域中可用的度量值，用户需要 IAM 策略并具有*管理员*角色、*操作者*角色或*编辑者*角色。

要验证用户许可权，请完成以下步骤：

1. 登录到 {{site.data.keyword.Bluemix_notm}} 控制台。

    打开 Web 浏览器并启动 {{site.data.keyword.Bluemix_notm}} 仪表板：[http://console.bluemix.net ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](http://bluemix.net){:new_window}
	
	使用用户标识和密码登录后，{{site.data.keyword.Bluemix_notm}} UI 即会打开。

2. 从菜单栏中，单击**管理 > 帐户 > 用户**。 

    *用户*窗口将显示一个用户列表，其中包含当前选定帐户的电子邮件地址。
	
3. 验证是否有使用 {{site.data.keyword.monitoringshort}} 服务的许可权。


## 步骤 3：获取空间标识 
{: #step3_delete_metrics}

仅当您想要删除空间域中可用的度量值时，才使用此步骤。

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

	

## 步骤 4：列出度量值
{: #step4_delete_metrics}


运行以下 cURL 命令来列出空间域中可用的度量值：

```
curl -H "X-Auth-Scope-Id: ${Space}" -H “X-Auth-User-Token: Auth_Type ${TOKEN}" -XGET METRICS_ENDPOINT/v1/metrics/list?query=*

```
{: screen}

运行以下 cURL 命令来列出帐户域中可用的度量值：

```
curl -H "X-Auth-User-Token: apikey ${TOKEN}" -XGET METRICS_ENDPOINT/v1/metrics/list?query=*
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
	
* METRICS_ENDPOINT 表示服务的入口点。 每个区域都有不同的 URL。 要获取每个区域的端点列表，请参阅[端点](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints)。

* *query* 定义应用的过滤器。 例如，`query=metric-service.*` 列出在层次结构 `metric-service.*` 下存在的所有度量值，`query=*` 列出域中的所有度量值。


## 步骤 5 - 选项 1：删除所有度量值
{: #step5_delete_metrics}
  

运行以下 cURL 命令来删除空间域中的所有度量值：

```
curl -XDELETE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/metrics/list?query=*
```
{: screen}

运行以下 cURL 命令来删除帐户域中的所有度量值：

```
curl -H "X-Auth-User-Token: Auth_Type ${Token}" -XDELETE  METRICS_ENDPOINT/v1/metrics/list?query=*
```
{: screen}

其中
	
* *X-Auth-User-Token* 是用于传递 {{site.data.keyword.Bluemix_notm}} UAA 令牌的参数。
	
* Auth_Type 是用于定义令牌类型的前缀。 有效值为：*uaa*（代表 UAA 令牌）、*iam*（代表 IAM 令牌）和 *api*（代表 API 密钥）。
	
* *X-Auth-Scope-Id* 是用于传递空间 GUID 的参数。 GUID 必须以 *s-* 为前缀以标识空间。
	
* *Token* 表示安全性令牌。
	
* *Space* 表示空间的 GUID。 
	
* *METRICS_ENDPOINT* 表示服务的入口点。 每个区域都有不同的 URL。 要获取每个区域的端点列表，请参阅[端点](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints)。

* *query* 定义应用的过滤器。 `query=*` 指示域中的所有度量值。


## 步骤 6 - 选项 2：删除服务的所有度量值
{: #step6_delete_metrics}
  

运行以下 cURL 命令来删除空间域中服务的所有度量值：

```
curl -XDELETE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/metrics/list?query=metric-service.*
```
{: screen}

运行以下 cURL 命令来删除帐户域中的所有度量值：

```
curl -H "X-Auth-User-Token: Auth_Type ${Token}" -XDELETE  METRICS_ENDPOINT/v1/metrics/list?query=metric-service.*
```
{: screen}

其中
	
* *X-Auth-User-Token* 是用于传递 {{site.data.keyword.Bluemix_notm}} UAA 令牌的参数。
	
* Auth_Type 是用于定义令牌类型的前缀。 有效值为：*uaa*（代表 UAA 令牌）、*iam*（代表 IAM 令牌）和 *api*（代表 API 密钥）。
	
* *X-Auth-Scope-Id* 是用于传递空间 GUID 的参数。 GUID 必须以 *s-* 为前缀以标识空间。
	
* *Token* 表示安全性令牌。
	
* *Space* 表示空间的 GUID。 
	
* *METRICS_ENDPOINT* 表示服务的入口点。 每个区域都有不同的 URL。 要获取每个区域的端点列表，请参阅[端点](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints)。

* *query* 定义应用的过滤器。 `query=*` 指示域中的所有度量值。

* *metric-service.** 是服务的名称。 例如，`containers-kubernetes`。
