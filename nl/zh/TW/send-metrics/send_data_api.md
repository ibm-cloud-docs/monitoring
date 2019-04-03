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

# 使用 Metrics API 傳送資料
{: #send_data_api}

您可以使用 Metrics API，將度量值傳送至 {{site.data.keyword.monitoringshort}} 服務。
{:shortdesc}


若為 {{site.data.keyword.Bluemix_notm}} Docker 容器，會自動收集基本系統度量值。若為 Cloud Foundry 應用程式及「虛擬機器 (VM)」中執行的應用程式，則必須使用 [Metrics API](https://console.bluemix.net/apidocs/927-ibm-cloud-monitoring-rest-api?&language=node#introduction){: new_window}，直接從應用程式傳送度量值。 



## 將度量值傳送至空間網域
{: #space_uaa}

若要使用 cURL 將度量值傳送至空間，請完成下列步驟：

1. 登入 {{site.data.keyword.Bluemix_notm}} 中的地區、組織及空間。 

    如需相關資訊，請參閱[如何登入 {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login)。

2. 取得安全記號。您可以使用 UAA 記號、IAM 記號或 API 金鑰。

    選擇下列其中一種方法來取得您需要傳送度量值的安全記號：
	
	* 若要取得 UAA 記號，請參閱[使用 {{site.data.keyword.Bluemix_notm}} CLI 取得 UAA 記號](/docs/services/cloud-monitoring/security/auth_uaa.html#uaa_cli)；
	
	* 若要取得 IAM 記號，請參閱[使用 {{site.data.keyword.Bluemix_notm}} CLI 取得 IAM 記號](/docs/services/cloud-monitoring/security/auth_iam.html#auth_iam)。
	
	* 若要取得 API 金鑰，請參閱[取得 API 金鑰](/docs/services/cloud-monitoring/security/auth_api_key.html#auth_api_key)。
	
	從登入 {{site.data.keyword.Bluemix_notm}} 的相同終端機中，設定記號的 *Token* 變數。

    例如，設定 UAA 記號，然後移除記號值的 *Bearer* 部分：

    ```
    export Token="kjshdgf.....ldkdjdj"
    ```
    {: screen}
		
3. 取得空間 GUID。GUID 必須加上字首 *s-*，以識別空間。

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
	
5. 執行下列 cURL 指令，以傳送度量值：

    ```
	curl -XPOST -d @Metric_File --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" Endpoint/v1/metrics
	```
	{: codeblock}
	
	其中
	
	* Metrics_File 代表 JSON 檔案，其中包括傳送至 {{site.data.keyword.monitoringshort}} 服務的度量值定義。
	
	* *X-Auth-User-Token* 參數會傳遞安全記號。
	
	* *Auth_Type* 是定義記號類型的字首。有效值包含：*uaa*（適用於 UAA 記號）、*iam*（適用於 IAM 記號）及 *api*（適用於 API 金鑰）。
	
	* *X-Auth-Scope-Id* 參數會傳遞空間 GUID。GUID 必須加上字首 *s-*，以識別空間。
	
	* Token 代表安全記號或 API 金鑰。
	
	* Space 代表空間的 GUID。 
	
	* Endpoint 代表服務的進入點。每一個地區都有不同的 URL。若要取得每個地區的端點清單，請參閱[端點](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints)。
	
	例如，您可以執行下列指令，將 2 個度量值（`myhost.cpu.idle` 及 `myapp.login.attempts`）傳送至 {{site.data.keyword.monitoringshort}} 服務：
	
	```
	curl -XPOST @metric.json --header "X-Auth-User-Token: uaa ${Token}" https://metrics.ng.bluemix.net/v1/metrics
	```
	{: screen}
	
	範例檔 *metric.json* 定義如下：

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

 











 
