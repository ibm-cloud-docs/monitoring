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

# 检索度量值
{: #retrieve_data_api}

可以使用[度量值 API](https://console.bluemix.net/apidocs/927-ibm-cloud-monitoring-rest-api?&language=node#introduction){: new_window} 从 {{site.data.keyword.monitoringshort}} 服务检索度量值。
{:shortdesc}


## 从空间检索度量值
{: #uaa}

要从空间检索度量值，请完成以下步骤：

1. 登录到 {{site.data.keyword.Bluemix_notm}} 中的区域、组织和空间。 

    有关更多信息，请参阅[如何登录到 {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login)。

2. 设置安全性令牌或 API 密钥
  
    必须将字段 **X-Auth-User-Token** 设置为安全性令牌或 API 密钥。 您可以使用 UAA 令牌、IAM 令牌或 API 密钥。

    首先，选择下列其中一种方法来获取发送度量值所需的安全性令牌：
	
    * 要获取 UAA 令牌，请参阅[使用 {{site.data.keyword.Bluemix_notm}} CLI 获取 UAA 令牌](/docs/services/cloud-monitoring/security/auth_uaa.html#uaa_cli)。
    
	* 要获取 IAM 令牌，请参阅[使用 {{site.data.keyword.Bluemix_notm}} CLI 获取 IAM 令牌](/docs/services/cloud-monitoring/security/auth_iam.html#auth_iam)。
    
	* 要获取 API 密钥，请参阅[获取 API 密钥](/docs/services/cloud-monitoring/security/auth_api_key.html#auth_api_key)。 

    令牌或 API 密钥必须以下列其中一个值作为前缀：`apikey`、`iam` 或 `uaa` 

    其中 

    * *apikey* 表明令牌是 API 密钥。
    * *iam* 表明指定的令牌是 IAM 生成的令牌。
    * *uaa* 表明指定的令牌是 UAA 生成的令牌。

    例如，您可以设置 API 密钥的以下头：`X-Auth-User-Token: apikey SomeIAMGeneratedKey`
	
	然后，通过您登录到 {{site.data.keyword.Bluemix_notm}} 的相同终端，为令牌设置 Token 变量。

    例如，设置 UAA 令牌，并从令牌值中除去 *Bearer* 部分：

    ```
    export Token="kjshdgf.....ldkdjdj"
    ```
    {: screen}
		
3. 获取空间标识。

    要检索度量值，头字段 **X-Auth-Scope-Id** 是必需的，并且必须设置为空间 GUID。 

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

4. 运行以下 cURL 命令以发送度量值：

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/metrics?from=Start_Time&until=End_Time&target=string
	```
	{: codeblock}

	其中
	
	* *X-Auth-User-Token* 是用于传递 {{site.data.keyword.Bluemix_notm}} UAA 令牌的参数。
	
	* Auth_Type 是用于定义令牌类型的前缀。 有效值为：*uaa*（代表 UAA 令牌）、*iam*（代表 IAM 令牌）和 *api*（代表 API 密钥）。
	
	* *X-Auth-Scope-Id* 是用于传递空间 GUID 的参数。 GUID 必须以 *s-* 为前缀以标识空间。 仅当使用 UAA 认证时，此头才是必需的。 如果使用 IAM 认证令牌，那么此头是可选的，并且将使用绑定到该令牌的域信息。
	
	* *Token* 表示安全性令牌。
	
	* *Space* 表示空间的 GUID。 
	
	* *Start_Time* 定义请求的开始时间。 此信息用于计算相对或绝对时间段。 *End_Time* 定义请求的结束时间。 此信息用于计算相对或绝对时间段。 有关更多信息，请参阅[设置时间段](/docs/services/cloud-monitoring/retrieve-metrics/retrieve_data_api.html#time)。
	
	* *Path* 表明一个或多个度量值。 您可以选择对每个度量值应用函数。 路径还支持通配符，通过通配符，可以识别单个路径中的多个度量值。 有关更多信息，请参阅[定义度量值](/docs/services/cloud-monitoring/retrieve-metrics/retrieve_data_api.html#metrics)。
	
	* *METRICS_ENDPOINT* 表示服务的入口点。 每个区域都有不同的 URL。 要获取每个区域的端点列表，请参阅[端点](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints)。
	

	
## 定义度量值
{: #metrics}

要检索度量值的数据，必须将度量值的路径从度量值树的根目录更改为该度量值的目录，并且必须使用句点 (.) 来分隔每个步骤。

在 **Target** 参数中指定该路径。 每个请求最多可指定 5 个目标。  

可选择将函数应用于度量值。 有关受支持函数的更多信息，请参阅 [Graphite 0.9.15 函数 ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](http://graphite.readthedocs.io/en/latest/functions.html)。

您可以使用通配符定义路径。 通过使用通配符，可以识别单个路径中的多个度量值。 

* **星号**：可以使用星号 (*) 来匹配零个或多个字符。 

    单个路径元素中可以有多个星号，例如：`servers.sp*aeg*r.cpu.total.*`。此示例将返回与该模式匹配的所有服务器 CPU 总数的相关数据。

* **字符列表或范围**：可以在方括号 ([...]) 中定义字符，以在路径字符串中指定单个字符位置。 

    可以通过指定以连字符 (-) 分隔的两个字符来设置字符包含范围。 这两个字符之间的任何字符都将匹配。 
	
	您可以在方括号中定义一个或多个字符范围。 
	
	如果不能将一组方括号中的字符作为范围来读取，那么这些字符将被视为值列表。 
	
	您可以在值列表中包含连字符 (-) 作为字符，方法是将其放在方括号的开头或结尾。

* **值列表**：可以在花括号中设置以逗号分隔的值以定义值列表。 

    例如，要下载路径 `servers.myserver.cpu.total.user` 和 `servers.myserver.cpu.total.system` 的度量值，可以为这两种类型设置单个路径：`servers.myserver.cpu.total.{user,system}`



## 设置时间段
{: #time}

您可以选择使用相对时间或绝对时间来指定时间段。 必须定义查询参数 **From** 和 **Until**。  

* 当省略时间段的开始时间时，缺省值为 24 小时前。 

* 当省略时间段的结束时间时，缺省值为当前时间 *now*。

**相对时间**始终以减号 (-) 开头，后跟一个时间单位。 

下表列出了可以使用的不同相对时间缩写：


| 缩写 | 描述 |
|--------------|-------------|
| s            | 秒     |
| min          | 分钟     |
| h            | 小时       |
| d            | 日        |
| w            | 周       |
| mon          | 月      |
| now          | 当前时间 |


您可以使用以下任意格式来定义**绝对时间**：`HH:MM_YYMMDD`、`YYYYMMDD` 和 `MM/DD/YY`

| 缩写 | 描述 |
|--------------|-------------|
| YYYY         | 四位数年份 |
| MM           | 两位数月份（01=Jan 等） |
| DD           | 两位数日期（01 到 31） |
| hh           | 两位数小时（00 到 23） |
| mm           | 两位数分钟（00 到 59） |
| ss           | 两位数秒（00 到 59） |

**示例**

下表显示了有关如何通过设置 *from* 和 *until* 参数来设置不同时间段的不同示例：

<table>
  <caption>表 1. 显示有关如何通过设置 *from* 和 *until* 参数来设置不同时间段的不同示例</caption>
  <tr>
    <th>示例</th>
	<th>描述</th>
  </tr>
  <tr>
    <td>&from=monday</td>
	<td>包含上星期一到现在的数据的时间段。</td>
  </tr>
  <tr>
    <td>&from=20171101&until=20171130</td>
	<td>设置为月份的时间段，例如，11 月 </td>
  </tr>
  <tr>
    <td>&from=02:00_20170701&until=14:00_20170701</td>
	<td>以 24 小时为周期显示数据，例如，2017 年 7 月 1 日 02:00 到 14:00</td>
  </tr>
  <tr>
    <td>&from=-8d&until=-7d</td>
	<td>显示一周的同一天，例如，上周</td>
  </tr>
  
</table>


