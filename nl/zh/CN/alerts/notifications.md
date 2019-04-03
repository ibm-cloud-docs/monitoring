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


# CRUD 通知
{: #notifications}

使用警报 API 可创建、删除和更新通知，显示通知详细信息以及列出在空间中定义的通知。
{:shortdesc}

## 创建通知
{: #notifications_create}

要创建通知，请完成以下步骤：

1. 创建通知文件。

    1. 使用通知模板来创建通知文件。 有关更多信息，请参阅[通知模板](/docs/services/cloud-monitoring?topic=cloud-monitoring-config_alerts_ov#notification_template)。
	
	2. 更新文件：
	
	    * 在 *name* 字段中输入唯一名称。 此字段的值后续将用于更新、删除和显示通知的详细信息。
		* 输入描述。
		* 输入有效电子邮件地址、URL 端点或 PagerDuty 密钥。
		
	3. 保存文件。 例如，针对您为空间中运行的查询所定义的通知，使用 *s-* 之类的前缀。
	
	    **提示**：在 *~/cloud-monitoring/notifications/* 目录中创建通知文件，以用于对 {{site.data.keyword.monitoringshort_notm}} 服务的资源分组。 
	
	4. 导出变量 *NOTIFICATION_FILE*：
	
	```
	export NOTIFICATION_FILE="mynotificationfile.json"
	```
	{: screen}
	
2. 登录到 {{site.data.keyword.Bluemix_notm}} 中的区域、组织和空间。 

    有关更多信息，请参阅[如何登录到 {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login)。

3. 获取安全性令牌。 您可以使用 UAA 令牌、IAM 令牌或 API 密钥。 选择下列其中一种方法来获取安全性令牌：
	
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
	
4. 获取空间 GUID。 GUID 必须以 *s-* 为前缀以标识空间。

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
	
5. 向 {{site.data.keyword.monitoringshort}} 服务注册通知。

    ```
	curl -XPOST -d @$NOTIFICATION_FILE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notification
	```
	{: codeblock}
	
	其中
	
	* NOTIFICATION_FILE 是用于定义通知的 JSON 文件。
	
	* *X-Auth-User-Token* 是用于传递 {{site.data.keyword.Bluemix_notm}} UAA 令牌、IAM 令牌或 API 密钥的参数。
	
	* *Auth_Type* 是用于定义令牌或 API 密钥的类型的前缀。 以下列表列出了有效值：*apikey*、*iam* 或 *uaa*，其中：

        * *apikey* 表明令牌是 API 密钥。
		* *iam* 表明指定的令牌是 IAM 生成的令牌。
		* *uaa* 表明指定的令牌是 UAA 生成的令牌。
	
	* *X-Auth-Scope-Id* 是用于传递空间 GUID 的参数。 GUID 必须以 *s-* 为前缀以标识空间。 如果使用 UAA 认证令牌，此头是必需的。 如果使用 IAM 认证令牌，那么此头是可选的，并且将使用绑定到该令牌的域信息。
	
	* Token 是 UAA 令牌、IAM 令牌或 API 密钥。
	
	* Space 是空间的 GUID。 
	
	* METRICS_ENDPOINT 表示服务的入口点。 每个区域都有不同的 URL。 要获取每个区域的端点列表，请参阅[端点](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints)。
	
    例如： 	
	
	```
	curl -XPOST -d @$NOTIFICATION_FILE  --header "X-Auth-User-Token: iam ${Token}" https://metrics.ng.bluemix.net/v1/alert/notification
	```
	{: screen}

## 删除通知
{: #notifications_delete}

要删除通知，请完成以下步骤：

1. 登录到 {{site.data.keyword.Bluemix_notm}} 中的区域、组织和空间。 

    有关更多信息，请参阅[如何登录到 {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login)。

2. 获取安全性令牌。 您可以使用 UAA 令牌、IAM 令牌或 API 密钥。 选择下列其中一种方法来获取安全性令牌：
	
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
	
	然后，导出变量 *Space*：
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. 运行以下 cURL 命令来删除通知：

    ```
	curl -XDELETE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notification/Notification_Name
	```
	{: codeblock}
	
	其中
	
	* *X-Auth-User-Token* 是用于传递 UAA 令牌、IAM 令牌或 API 密钥的参数。
	
	* *Auth_Type* 是用于定义令牌或 API 密钥的类型的前缀。 以下列表列出了有效值：*apikey*、*iam* 或 *uaa*，其中：

        * *apikey* 表明令牌是 API 密钥。
		* *iam* 表明指定的令牌是 IAM 生成的令牌。
		* *uaa* 表明指定的令牌是 UAA 生成的令牌。
	
	* *X-Auth-User-Token* 是用于传递 {{site.data.keyword.Bluemix_notm}} UAA 令牌、IAM 令牌或 API 密钥的参数。 令牌或 API 密钥必须以下列其中一个值作为前缀：*apikey*、*iam* 或 *uaa*，其中

        * *apikey* 表明令牌是 API 密钥。
		* *iam* 表明指定的令牌是 IAM 生成的令牌。
		* *uaa* 表明指定的令牌是 UAA 生成的令牌。
		
	* Token 是 UAA 令牌、IAM 令牌或 API 密钥。
	
	* Space 是空间的 GUID。 
	
	* Notification_Name 是通知的名称，即列出通知属性时 *name* 字段的值。
	
	* METRICS_ENDPOINT 表示服务的入口点。 每个区域都有不同的 URL。 要获取每个区域的端点列表，请参阅[端点](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints)。
	


## 列出所有通知
{: #notifications_list}

要列出所有通知，请完成以下步骤：

1. 登录到 {{site.data.keyword.Bluemix_notm}} 中的区域、组织和空间。 

    有关更多信息，请参阅[如何登录到 {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login)。

2. 获取安全性令牌。 您可以使用 UAA 令牌、IAM 令牌或 API 密钥。 选择下列其中一种方法来获取安全性令牌：
	
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
	
	然后，导出变量 *Space*：
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. 运行以下 cURL 命令来列出所有通知：

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notifications
	```
	{: codeblock}
	
	其中
	
	* *X-Auth-User-Token* 是用于传递 {{site.data.keyword.Bluemix_notm}} UAA 令牌、IAM 令牌或 API 密钥的参数。
	
	* *Auth_Type* 是用于定义令牌或 API 密钥的类型的前缀。 以下列表列出了有效值：*apikey*、*iam* 或 *uaa*，其中：

        * *apikey* 表明令牌是 API 密钥。
		* *iam* 表明指定的令牌是 IAM 生成的令牌。
		* *uaa* 表明指定的令牌是 UAA 生成的令牌。
		
	* *X-Auth-User-Token* 是用于传递 {{site.data.keyword.Bluemix_notm}} UAA 令牌、IAM 令牌或 API 密钥的参数。 令牌或 API 密钥必须以下列其中一个值作为前缀：*apikey*、*iam* 或 *uaa*，其中

        * *apikey* 表明令牌是 API 密钥。
		* *iam* 表明指定的令牌是 IAM 生成的令牌。
		* *uaa* 表明指定的令牌是 UAA 生成的令牌。
		
	* Token 是 UAA 令牌、IAM 令牌或 API 密钥。
	
	* Space 是空间的 GUID。 
	
	* METRICS_ENDPOINT 表示服务的入口点。 每个区域都有不同的 URL。 要获取每个区域的端点列表，请参阅[端点](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints)。

			

## 显示通知的详细信息
{: #show}


要显示通知的相关信息，请完成以下步骤：

1. 登录到 {{site.data.keyword.Bluemix_notm}} 中的区域、组织和空间。 

    有关更多信息，请参阅[如何登录到 {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login)。

2. 获取安全性令牌。 您可以使用 UAA 令牌、IAM 令牌或 API 密钥。 选择下列其中一种方法来获取安全性令牌：
	
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
	
	然后，导出变量 *Space*：
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. 运行以下 cURL 命令来显示通知的详细信息：

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notification/NOTIFICATION_NAME
	```
	{: codeblock}
	
	其中
	
	* *X-Auth-User-Token* 是用于传递 {{site.data.keyword.Bluemix_notm}} UAA 令牌、IAM 令牌或 API 密钥的参数。
	
	* *Auth_Type* 是用于定义令牌或 API 密钥的类型的前缀。 以下列表列出了有效值：*apikey*、*iam* 或 *uaa*，其中：

        * *apikey* 表明令牌是 API 密钥。
		* *iam* 表明指定的令牌是 IAM 生成的令牌。
		* *uaa* 表明指定的令牌是 UAA 生成的令牌。
		
	* Token 是 UAA 令牌、IAM 令牌或 API 密钥。
	
	* Space 是空间的 GUID。 
	
	* NOTIFICATION_NAME 是通知的名称，即列出通知属性时 *name* 字段的值。
	
	* METRICS_ENDPOINT 表示服务的入口点。 每个区域都有不同的 URL。 要获取每个区域的端点列表，请参阅[端点](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints)。
	
     
		

			
## 测试通知
{: #test}	
			
要测试通知，请完成以下步骤：

1. 登录到 {{site.data.keyword.Bluemix_notm}} 中的区域、组织和空间。 

    有关更多信息，请参阅[如何登录到 {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login)。

2. 获取安全性令牌。 您可以使用 UAA 令牌、IAM 令牌或 API 密钥。 选择下列其中一种方法来获取安全性令牌：
	
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
	
	然后，导出变量 *Space*：
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. 运行以下 cURL 命令来测试通知：

    ```
	curl -XPOST --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notification/test/NOTIFICATION_NAME
	```
	{: codeblock}
	
	其中
	
	* *X-Auth-User-Token* 是用于传递 {{site.data.keyword.Bluemix_notm}} UAA 令牌、IAM 令牌或 API 密钥的参数。
	
	* *Auth_Type* 是用于定义令牌或 API 密钥的类型的前缀。 以下列表列出了有效值：*apikey*、*iam* 或 *uaa*，其中：

        * *apikey* 表明令牌是 API 密钥。
		* *iam* 表明指定的令牌是 IAM 生成的令牌。
		* *uaa* 表明指定的令牌是 UAA 生成的令牌。
	
	* *X-Auth-User-Token* 是用于传递 {{site.data.keyword.Bluemix_notm}} UAA 令牌、IAM 令牌或 API 密钥的参数。 令牌或 API 密钥必须以下列其中一个值作为前缀：*apikey*、*iam* 或 *uaa*，其中

        * *apikey* 表明令牌是 API 密钥。
		* *iam* 表明指定的令牌是 IAM 生成的令牌。
		* *uaa* 表明指定的令牌是 UAA 生成的令牌。
		
	* Token 是 UAA 令牌、IAM 令牌或 API 密钥。
	
	* Space 是空间的 GUID。 
	
	* NOTIFICATION_NAME 是通知的名称，即列出通知属性时 *name* 字段的值。
	
	* METRICS_ENDPOINT 表示服务的入口点。 每个区域都有不同的 URL。 要获取每个区域的端点列表，请参阅[端点](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints)。
	


## 更新通知
{: #notifications_update}

要更新通知，请完成以下步骤：

1. 登录到 {{site.data.keyword.Bluemix_notm}} 中的区域、组织和空间。 

    有关更多信息，请参阅[如何登录到 {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login)。

2. 获取安全性令牌。 您可以使用 UAA 令牌、IAM 令牌或 API 密钥。 选择下列其中一种方法来获取安全性令牌：
	
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
	
	然后，导出变量 *Space*：
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. 运行以下 cURL 命令来更新通知：

    ```
	curl -XPUT -d @$NOTIFICATION_FILE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notification
	```
	{: codeblock}
	
	其中
	
	* NOTIFICATION_FILE 是用于定义通知的 JSON 文件。
	
	* *Auth_Type* 是用于定义令牌或 API 密钥的类型的前缀。 以下列表列出了有效值：*apikey*、*iam* 或 *uaa*，其中：

        * *apikey* 表明令牌是 API 密钥。
		* *iam* 表明指定的令牌是 IAM 生成的令牌。
		* *uaa* 表明指定的令牌是 UAA 生成的令牌。
	
	* *X-Auth-User-Token* 是用于传递 bluemix UAA 令牌、IAM 令牌或 API 密钥的参数。 令牌或 API 密钥必须以下列其中一个值作为前缀：*apikey*、*iam* 或 *uaa*，其中

        * *apikey* 表明令牌是 API 密钥。
		* *iam* 表明指定的令牌是 IAM 生成的令牌。
		* *uaa* 表明指定的令牌是 UAA 生成的令牌。
		
	* Token 是 UAA 令牌、IAM 令牌或 API 密钥。
	
	* Space 是空间的 GUID。 

	* METRICS_ENDPOINT 表示服务的入口点。 每个区域都有不同的 URL。 要获取每个区域的端点列表，请参阅[端点](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints)。
	
        

