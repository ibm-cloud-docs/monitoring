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


# CRUD 规则
{: #rules}

使用警报 API 可创建、删除或更新规则，显示规则的详细信息，以及列出在空间中定义的规则。
{:shortdesc}


## 创建规则
{: #create}

要在 {{site.data.keyword.monitoringshort}} 服务中配置规则，请创建包含规则详细信息的规则文件，然后向 {{site.data.keyword.monitoringshort}} 服务注册规则。

请完成以下步骤：

1. 创建包含有效 JSON 的规则文件。 保存文件。 

    例如，要保存文件，请针对您为空间中运行的查询所定义的规则，使用 *s-* 之类的前缀。
	
	**提示：** 
	
	* 为查询定义不同的规则，以使用不同的通知方法发出有关错误或警告的警报。 
	* 在 *~/cloud-monitoring/rules/* 目录中创建规则文件，以用于对 {{site.data.keyword.monitoringshort_notm}} 服务的资源分组。 

    在规则的文件中输入以下信息：
	
	* *name*：输入唯一名称。 此字段的值后续将用于更新、删除和显示规则的详细信息。
	* *description*：输入描述。
	* *expression*：输入要监视的查询。
	* *enabled*：设置为 *true* 可启用规则。
	* *from*：用于根据阈值来分析数据的初始时间点。
	* *until*：用于根据阈值来分析数据的结束时间点。
	* *comparison*：用于识别要执行哪种类型检查的比较操作，例如 *below*。
	* *error_level*：定义用于触发错误警报的阈值。
	* *warning_level*：定义用于触发警告警报的阈值。
	* *frequency*：定义检查数据的频率。
	* *dashboard_url*：定义 URL 以用于在 Grafana 中显示包含查询的仪表板。
	* *notifications*：触发此规则描述的警报时使用的通知方法。
	
	例如，规则文件 myrulefile.json 如下所示：
	
	```
	{
    "name": "checkbytesin",
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
      "emailXXX"
    ]
    }
    ```
	{: screen}
	
	然后，导出变量 *RULE_FILE*：
	
	```
	export RULE_FILE="myrulefile.json"
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
	
5. 运行以下 cURL 命令以在 {{site.data.keyword.monitoringshort}} 服务中注册规则：

    ```
	curl -XPOST -d @$RULE_FILE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/rule
	```
	{: codeblock}
	
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
	
	* METRICS_ENDPOINT 表示服务的入口点。 每个区域都有不同的 URL。 要获取每个区域的端点列表，请参阅[端点](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints)。
	
    例如： 	
	
	```
	curl -XPOST -d @$RULE_FILE --header "X-Auth-User-Token:iam ${Token}" https://metrics.ng.bluemix.net/v1/alert/rule
	```
	{: screen}

## 删除规则
{: #delete}

要删除规则，请完成以下步骤：

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
		
4. 运行以下 cURL 命令来删除规则：

    ```
	curl -XDELETE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/rule/Rule_Name
	```
	{: codeblock}
	
	其中
	
    * *X-Auth-User-Token* 是用于传递 UAA 令牌、IAM 令牌或 API 密钥的参数。
	
	* *Auth_Type* 是用于定义令牌或 API 密钥的类型的前缀。 以下列表列出了有效值：*apikey*、*iam* 或 *uaa*，其中：

        * *apikey* 表明令牌是 API 密钥。
		* *iam* 表明指定的令牌是 IAM 生成的令牌。
		* *uaa* 表明指定的令牌是 UAA 生成的令牌。
	
	* *X-Auth-Scope-Id* 是用于传递空间 GUID 的参数。 GUID 必须以 *s-* 为前缀以标识空间。 如果使用 UAA 认证令牌，此头是必需的。 如果使用 IAM 认证令牌，那么此头是可选的，并且将使用绑定到该令牌的域信息。
	
	* Token 是 UAA 或 IAM 认证令牌或者 API 密钥。
	
	* Space 是空间的 GUID。 
	
	* Rule_Name 是在 *name* 字段中指定的规则名称。
	
	* METRICS_ENDPOINT 表示服务的入口点。 每个区域都有不同的 URL。 要获取每个区域的端点列表，请参阅[端点](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints)。
	
    
	
## 列出所有规则
{: #list}

要列出所有规则，请完成以下步骤：

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
	
4. 运行以下 cURL 命令来列出空间中的所有规则：

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/rules
	```
	{: codeblock}
	
	其中
	
	* *X-Auth-User-Token* 是用于传递 UAA 令牌、IAM 令牌或 API 密钥的参数。
	
	* *Auth_Type* 是用于定义令牌或 API 密钥的类型的前缀。 以下列表列出了有效值：*apikey*、*iam* 或 *uaa*，其中：

        * *apikey* 表明令牌是 API 密钥。
		* *iam* 表明指定的令牌是 IAM 生成的令牌。
		* *uaa* 表明指定的令牌是 UAA 生成的令牌。
	
	* *X-Auth-Scope-Id* 是用于传递空间 GUID 的参数。 GUID 必须以 *s-* 为前缀以标识空间。 如果使用 UAA 认证令牌，此头是必需的。 如果使用 IAM 认证令牌，那么此头是可选的，并且将使用绑定到该令牌的域信息。
	
	* Token 是 UAA 或 IAM 认证令牌或者 API 密钥。
	
	* Space 是空间的 GUID。 
	
	* METRICS_ENDPOINT 表示服务的入口点。 每个区域都有不同的 URL。 要获取每个区域的端点列表，请参阅[端点](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints)。
	

	
	

## 显示规则的详细信息
{: show}

要显示规则的详细信息，请完成以下步骤：

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
	
4. 运行以下 cURL 命令来显示规则的详细信息：

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/rule/Rule_Name
	```
	{: codeblock}
	
	其中
	
	* *X-Auth-User-Token* 是用于传递 UAA 令牌、IAM 令牌或 API 密钥的参数。
	
	* *Auth_Type* 是用于定义令牌或 API 密钥的类型的前缀。 以下列表列出了有效值：*apikey*、*iam* 或 *uaa*，其中：

        * *apikey* 表明令牌是 API 密钥。
		* *iam* 表明指定的令牌是 IAM 生成的令牌。
		* *uaa* 表明指定的令牌是 UAA 生成的令牌。
	
	* *X-Auth-Scope-Id* 是用于传递空间 GUID 的参数。 GUID 必须以 *s-* 为前缀以标识空间。 如果使用 UAA 认证令牌，此头是必需的。 如果使用 IAM 认证令牌，那么此头是可选的，并且将使用绑定到该令牌的域信息。
	
	* Token 是 UAA 或 IAM 认证令牌或者 API 密钥。
	
	* Space 是空间的 GUID。 
	
	* Rule_Name 是在 *name* 字段中指定的规则名称。
	
	* METRICS_ENDPOINT 表示服务的入口点。 每个区域都有不同的 URL。 要获取每个区域的端点列表，请参阅[端点](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints)。
	

## 更新规则
{: #update}

要更新规则，请通过更新规则文件来修改规则，然后完成以下步骤：

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
	
4. 运行以下 cURL 命令来更新规则：

    ```
	curl -XPUT `-d @$RULE_FILE` --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/rule
	```
	{: codeblock}
	
	其中
	
	* RULE_FILE 是定义警报规则的 JSON 文件。
	
	* *X-Auth-User-Token* 是用于传递 UAA 令牌、IAM 令牌或 API 密钥的参数。
	
	* *Auth_Type* 是用于定义令牌或 API 密钥的类型的前缀。 以下列表列出了有效值：*apikey*、*iam* 或 *uaa*，其中：

        * *apikey* 表明令牌是 API 密钥。
		* *iam* 表明指定的令牌是 IAM 生成的令牌。
		* *uaa* 表明指定的令牌是 UAA 生成的令牌。
	
	* *X-Auth-Scope-Id* 是用于传递空间 GUID 的参数。 GUID 必须以 *s-* 为前缀以标识空间。 如果使用 UAA 认证令牌，此头是必需的。 如果使用 IAM 认证令牌，那么此头是可选的，并且将使用绑定到该令牌的域信息。
	
	* Token 是 UAA 或 IAM 认证令牌或者 API 密钥。
	
	* Space 是空间的 GUID。 
	
	* METRICS_ENDPOINT 表示服务的入口点。 每个区域都有不同的 URL。 要获取每个区域的端点列表，请参阅[端点](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints)。

	
	
