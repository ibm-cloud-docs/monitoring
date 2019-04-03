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


# 使用 Alerts API 擷取警示歷程
{: #retrieve_history}

使用 Alerts API，以擷取警示的歷程。
{:shortdesc}


若要使用 Alerts API 擷取警示的歷程，請完成下列步驟：

1. 登入 {{site.data.keyword.Bluemix_notm}} 中的地區、組織及空間。 

    如需相關資訊，請參閱[如何登入 {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login)。

2. 取得安全記號。您可以使用 UAA 記號、IAM 記號或 API 金鑰。選擇下列其中一種方法來取得安全記號：
	
	* 若要取得 UAA 記號，請參閱[使用 {{site.data.keyword.Bluemix_notm}} CLI 取得 UAA 記號](/docs/services/cloud-monitoring/security/auth_uaa.html#uaa_cli)。
	
	* 若要取得 IAM 記號，請參閱[使用 {{site.data.keyword.Bluemix_notm}} CLI 取得 IAM 記號](/docs/services/cloud-monitoring/security/auth_iam.html#auth_iam)。
	
	* 若要取得 API 金鑰，請參閱[取得 API 金鑰](/docs/services/cloud-monitoring/security/auth_api_key.html#auth_api_key)。
	
	從登入 {{site.data.keyword.Bluemix_notm}} 的相同終端機中，設定記號的 Token 變數。

    例如，若要使用 IAM 記號，請執行下列指令：

    ```
	ibmcloud iam oauth-tokens
	```
	{: codeblock}
	
	這個指令的結果如下：
	
	```
	IAM token:  Bearer djn.._l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	然後，匯出變數 *Token*：
	
	```
	export Token="djn.._l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ"
	```
	{: screen}
	
	**附註：**記號會排除 *Bearer*。
	
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
	
4. 擷取規則的歷程

    * 若要依規則名稱擷取規則的歷程，請參閱[使用規則名稱擷取規則的歷程](/docs/services/cloud-monitoring/alerts/retrieve_history.html#by_name)。
	* 若要擷取一段期間的規則歷程，請參閱[擷取過去 48 小時的規則歷程](/docs/services/cloud-monitoring/alerts/retrieve_history.html#by_time)。
	* 若要從規則歷程中擷取一些項目，請參閱[擷取規則歷程中的最後 3 個項目](/docs/services/cloud-monitoring/alerts/retrieve_history.html#number)。
	
	
## 依規則名稱擷取規則的歷程
{: #by_name}
	
執行下列 cURL 指令，以取得警示的歷程：

```
curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/history?rule_name=RULE_NAME
```
{: codeblock}
	
其中
	
* *X-Auth-User-Token* 參數會傳遞 UAA 記號、IAM 記號或 API 金鑰。
	
* *Auth_Type* 是定義記號或 API 金鑰類型的字首。下列清單概述有效值：*apikey*、*iam* 或 *uaa*，其中

    * *apikey* 識別該記號是 API 金鑰。
	* *iam* 識別所指定的記號是 IAM 產生的記號。
	* *uaa* 識別所指定的記號是 UAA 產生的記號。
	
* *X-Auth-Scope-Id* 參數會傳遞空間 GUID。GUID 必須加上字首 *s-*，以識別空間。如果您使用 UAA 記號鑑別，此標頭為必要項目。如果您使用 IAM 鑑別記號，則此標頭是選用項目，並且會使用連結至該記號的網域資訊。
	
* *Token* 是 UAA 或 IAM 鑑別記號，或是 API 金鑰。
	
* *Space* 是空間的 GUID。 
	
* *RULE_NAME* 是用來觸發警示的規則的名稱。該值是指定在 *name* 欄位中的值。
	
* *METRICS_ENDPOINT* 代表服務的進入點。每一個地區都有不同的 URL。若要取得每個地區的端點清單，請參閱[端點](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints)。
	
    
例如，`highNginxCPU` 規則的歷程如下：

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


## 擷取過去 48 小時的規則歷程
{: #by_time}

執行下列 cURL 指令，以擷取過去 48 小時的警示歷程：

```
curl -H "X-Auth-User-Token: iam $Token" -H "X-Auth-Scope-Id:$Space" METRICS_ENDPOINT/v1/alert/history?start=-48h
```
{: codeblock}

其中
	
* *X-Auth-User-Token* 參數會傳遞 UAA 記號、IAM 記號或 API 金鑰。
	
* *Auth_Type* 是定義記號或 API 金鑰類型的字首。下列清單概述有效值：*apikey*、*iam* 或 *uaa*，其中

    * *apikey* 識別該記號是 API 金鑰。
	* *iam* 識別所指定的記號是 IAM 產生的記號。
	* *uaa* 識別所指定的記號是 UAA 產生的記號。
	
* *X-Auth-Scope-Id* 參數會傳遞空間 GUID。GUID 必須加上字首 *s-*，以識別空間。如果您使用 UAA 記號鑑別，此標頭為必要項目。如果您使用 IAM 鑑別記號，則此標頭是選用項目，並且會使用連結至該記號的網域資訊。
	
* *Token* 是 UAA 或 IAM 鑑別記號，或是 API 金鑰。
	
* *Space* 是空間的 GUID。 
	
* *RULE_NAME* 是用來觸發警示的規則的名稱。該值是指定在 *name* 欄位中的值。
	
* *METRICS_ENDPOINT* 代表服務的進入點。每一個地區都有不同的 URL。若要取得每個地區的端點清單，請參閱[端點](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints)。
	

## 擷取規則歷程中的最後 3 個項目
{: #number}

執行下列 cURL 指令，以取得警示歷程中的最後 3 個項目：

```
curl -H "X-Auth-User-Token: iam $Token" -H "X-Auth-Scope-Id:$Space" METRICS_ENDPOINT/v1/alert/history?max_results=3
```
{: codeblock}

其中
	
* *X-Auth-User-Token* 參數會傳遞 UAA 記號、IAM 記號或 API 金鑰。
	
* *Auth_Type* 是定義記號或 API 金鑰類型的字首。下列清單概述有效值：*apikey*、*iam* 或 *uaa*，其中

    * *apikey* 識別該記號是 API 金鑰。
	* *iam* 識別所指定的記號是 IAM 產生的記號。
	* *uaa* 識別所指定的記號是 UAA 產生的記號。
	
* *X-Auth-Scope-Id* 參數會傳遞空間 GUID。GUID 必須加上字首 *s-*，以識別空間。如果您使用 UAA 記號鑑別，此標頭為必要項目。如果您使用 IAM 鑑別記號，則此標頭是選用項目，並且會使用連結至該記號的網域資訊。
	
* *Token* 是 UAA 或 IAM 鑑別記號，或是 API 金鑰。
	
* *Space* 是空間的 GUID。 
	
* *RULE_NAME* 是用來觸發警示的規則的名稱。該值是指定在 *name* 欄位中的值。
	
* *METRICS_ENDPOINT* 代表服務的進入點。每一個地區都有不同的 URL。若要取得每個地區的端點清單，請參閱[端點](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints)。
	
