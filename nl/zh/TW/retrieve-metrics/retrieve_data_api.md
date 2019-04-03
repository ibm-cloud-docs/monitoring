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

# 擷取度量值
{: #retrieve_data_api}

您可以使用 [Metrics API](https://console.bluemix.net/apidocs/927-ibm-cloud-monitoring-rest-api?&language=node#introduction){: new_window}，從 {{site.data.keyword.monitoringshort}} 服務擷取度量值。
{:shortdesc}


## 從空間擷取度量值
{: #uaa}

若要從空間擷取度量值，請完成下列步驟：

1. 登入 {{site.data.keyword.Bluemix_notm}} 中的地區、組織及空間。 

    如需相關資訊，請參閱[如何登入 {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login)。

2. 設定安全記號或 API 金鑰
  
    您必須設定欄位 **X-Auth-User-Token** 的安全記號或 API 金鑰。您可以使用 UAA 記號、IAM 記號或 API 金鑰。

    先選擇下列其中一種方法來取得您需要傳送度量值的安全記號：
	
    * 若要取得 UAA 記號，請參閱[使用 {{site.data.keyword.Bluemix_notm}} CLI 取得 UAA 記號](/docs/services/cloud-monitoring/security/auth_uaa.html#uaa_cli)。
    
	* 若要取得 IAM 記號，請參閱[使用 {{site.data.keyword.Bluemix_notm}} CLI 取得 IAM 記號](/docs/services/cloud-monitoring/security/auth_iam.html#auth_iam)。
    
	* 若要取得 API 金鑰，請參閱[取得 API 金鑰](/docs/services/cloud-monitoring/security/auth_api_key.html#auth_api_key)。 

    記號或 API 金鑰必須加上下列其中一個值作為字首：`apikey`、`iam` 或 `uaa` 

    其中 

    * *apikey* 識別該記號是 API 金鑰。
    * *iam* 識別所指定的記號是 IAM 產生的記號。
    * *uaa* 識別所指定的記號是 UAA 產生的記號。

    例如，您可以為 API 金鑰設定下列標頭：`X-Auth-User-Token: apikey SomeIAMGeneratedKey`
	
	然後，從登入 {{site.data.keyword.Bluemix_notm}} 的相同終端機中，設定記號的 Token 變數。

    例如，設定 UAA 記號，然後移除記號值的 *Bearer* 部分：

    ```
    export Token="kjshdgf.....ldkdjdj"
    ```
    {: screen}
		
3. 取得空間ID。

    若要擷取度量值，標頭欄位 **X-Auth-Scope-Id** 是必要項目，而且必須設定為空間 GUID。 

    執行下列指令：
	
	```
	ibmcloud iam space SpaceName --guid
	```
	{: codeblock}
	
	其中 *SpaceName* 是空間名稱，您將在該空間裡定義通知。
	
	例如，若要取得名為 *dev* 的空間 GUID，請執行下列指令：
	
	```
	ibmcloud iam space dev --guid
	```
	{: screen}
	
	這個指令的結果如下：
	
	```
	667fadfc-jhtg-1234-9f0e-cf4123451095
	```
	{: screen}
	
	然後，匯出變數 *Space*。**附註：**GUID 必須加上字首 *s-*，以識別空間。
	
	例如：
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}

4. 執行下列 cURL 指令，以傳送度量值：

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/metrics?from=Start_Time&until=End_Time&target=string
	```
	{: codeblock}

	其中
	
	* *X-Auth-User-Token* 參數會傳遞 {{site.data.keyword.Bluemix_notm}} UAA 記號。
	
	* Auth_Type 是用於定義記號類型的字首。有效值包含：*uaa*（適用於 UAA 記號）、*iam*（適用於 IAM 記號）及 *api*（適用於 API 金鑰）。
	
	* *X-Auth-Scope-Id* 參數會傳遞空間 GUID。GUID 必須加上字首 *s-*，以識別空間。只有在使用 UAA 鑑別時，才需要此標頭。如果您使用 IAM 鑑別記號，則此標頭是選用項目，並且會使用連結至該記號的網域資訊。
	
	* *Token* 代表安全記號。
	
	* *Space* 代表空間的 GUID。 
	
	* *Start_Time* 定義要求的開始時間。此資訊是用來計算相對或絕對時段。*End_Time* 定義要求的結束時間。此資訊是用來計算相對或絕對時段。如需相關資訊，請參閱[設定時段](/docs/services/cloud-monitoring/retrieve-metrics/retrieve_data_api.html#time)。
	
	* *Path* 識別一個或數個度量值。您可以選擇將函數套用至每個度量值。路徑也支援萬用字元，這樣可讓您以單一路徑識別多個度量值。如需相關資訊，請參閱[定義度量值](/docs/services/cloud-monitoring/retrieve-metrics/retrieve_data_api.html#metrics)。
	
	* *METRICS_ENDPOINT* 代表服務的進入點。每一個地區都有不同的 URL。若要取得每個地區的端點清單，請參閱[端點](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints)。
	

	
## 定義度量值
{: #metrics}

若要擷取度量值的資料，您必須指定度量值的路徑（從度量值樹狀結構根目錄到度量值），而且必須以句號 (.) 區隔每個步驟。

路徑指定在 **Target** 參數中。每個要求最多可以指定 5 個目標。  

您可以選擇將函數套用至度量值。如需所支援函數的相關資訊，請參閱 [Graphite 0.9.15 函數 ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](http://graphite.readthedocs.io/en/latest/functions.html)。

您可以使用萬用字元來定義路徑。藉由使用萬用字元，您可以用單一路徑識別多個度量值。 

* **星號**：您可以使用星號 (*) 以符合零個以上的字元。 

    在單一路徑元素內可以有多個星號，例如：`servers.sp*aeg*r.cpu.total.*` 這個範例會傳回符合型樣之所有伺服器的 CPU 總計相關資料。

* **字元清單或範圍**：您可以在方括弧 ([...]) 中定義字元，以指定路徑字串中的單一字元位置。 

    您可以指定以連字號 (-) 區隔的兩個字元，來設定字元內含範圍。這兩個字元之間的任何字元都會符合。 
	
	您可以在方括弧內定義一個以上的字元範圍。 
	
	當一組方括弧內的字元無法當作範圍來讀取時，會將字元視為值的清單。 
	
	您可以包含連字號 (-) 作為值清單中的字元，方法是將它放在方括弧內的開始或結束處。

* **值清單**：您可以在大括弧內設定以逗點區隔的值，以定義值清單。 

    例如，若要下載下列路徑的度量值：`servers.myserver.cpu.total.user` 及 `servers.myserver.cpu.total.system`，您可以為這兩種類型設定單一路徑：`servers.myserver.cpu.total.{user,system}`



## 設定時段
{: #time}

您可以使用相對時間或絕對時間，選擇性地指定時段。您必須定義查詢參數 **From** 和 **Until**。  

* 如果省略時段的開始時間，預設值是 24 小時前。 

* 如果省略時段的結束時間，預設值是現行時間 *now*。

**相對時間**一律會在前面加上減號 (-)，後面接著一個時間單位。 

下表列出您可以使用的不同相對時間縮寫：


|縮寫         |說明|
|--------------|-------------|
|s            |秒|
|min          |分鐘|
|h            |小時|
|d            |天|
|w            |週|
|mon          |月|
|now          |現行時間|


您可以使用下列任何格式來定義**絕對時間**：`HH:MM_YYMMDD`、`YYYYMMDD`、`MM/DD/YY`

|縮寫         |說明|
|--------------|-------------|
|YYYY         |四位數年份|
|MM           |二位數月份（01=一月，依此類推）|
|DD           |二位數日期（01 到 31）|
|hh           |二位數的小時（00 到 23）|
|mm           |二位數的分鐘（00 到 59）|
|ss           |二位數的秒鐘（00 到 59）|

**範例**

下表顯示如何設定 *from* 及 *until* 參數以設定不同時段的不同範例：

<table>
  <caption>表 1. 顯示如何設定 *from* 及 *until* 參數以設定不同時段的不同範例</caption>
  <tr>
    <th>範例</th>
	<th>說明</th>
  </tr>
  <tr>
    <td>&from=monday</td>
	<td>包括從上星期一到目前為止之資料的時段。</td>
  </tr>
  <tr>
    <td>&from=20171101&until=20171130</td>
	<td>設為月份的時段，例如 11 月</td>
  </tr>
  <tr>
    <td>&from=02:00_20170701&until=14:00_20170701</td>
	<td>以 24 小時週期顯示資料，例如 2017 年 7 月 1 日從 02:00 至 14:00</td>
  </tr>
  <tr>
    <td>&from=-8d&until=-7d</td>
	<td>顯示當週的同一天，例如上週</td>
  </tr>
  
</table>


