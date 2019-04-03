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



# 刪除通知
{: #delete_notifications}

您可以使用 [Alerts API](https://console.bluemix.net/apidocs/940-ibm-cloud-monitoring-alerts-api?&language=node#introduction){: new_window}，刪除 {{site.data.keyword.monitoringshort}} 服務中的通知。
{:shortdesc}

在您[登入 {{site.data.keyword.Bluemix_notm}} 中的地區](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login)之後，請完成下列步驟來刪除通知：


## 步驟 1：取得安全記號
{: #step1_delete_notifications}

您可以使用 UAA 記號、IAM 記號或 API 金鑰。 

選擇下列其中一種方法來取得安全記號：
	
* 若要取得 UAA 記號，請參閱[使用 {{site.data.keyword.Bluemix_notm}} CLI 取得 UAA 記號](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_uaa#uaa_cli)。
* 若要取得 IAM 記號，請參閱[使用 {{site.data.keyword.Bluemix_notm}} CLI 取得 IAM 記號](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_iam#auth_iam)。
* 若要取得 API 金鑰，請參閱[取得 API 金鑰](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_api_key#auth_api_key)。
	
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
	

## 步驟 2：取得空間 ID 
{: #step2_delete_notifications}

此步驟僅適用於要刪除空間網域中可用的通知。

若要取得空間 GUID，請執行下列指令：
	
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
	
然後，匯出變數 *Space*。GUID 必須加上字首 *s-*，以識別空間。
	
```
export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
{: screen}

	

## 步驟 3：列出通知
{: #step3_delete_notifications}


執行下列 cURL 指令，以列出空間網域中的通知：

```
curl -H "X-Auth-Scope-Id: ${Space}" -H “X-Auth-User-Token: Auth_Type ${TOKEN}" -XGET METRICS_ENDPOINT/v1/alert/notifications

```
{: screen}

執行下列 cURL 指令，以列出帳戶網域中的通知：

```
curl -H "X-Auth-User-Token: apikey ${TOKEN}" -XGET METRICS_ENDPOINT/v1/alert/notifications
```
{: screen}

其中
	
* *X-Auth-User-Token* 參數會傳遞 {{site.data.keyword.Bluemix_notm}} UAA 記號、IAM 記號或 API 金鑰。
	
* *Auth_Type* 是定義記號或 API 金鑰類型的字首。下列清單概述有效值：*apikey*、*iam* 或 *uaa*，其中

    * *apikey* 識別該記號是 API 金鑰。
	* *iam* 識別所指定的記號是 IAM 產生的記號。
	* *uaa* 識別所指定的記號是 UAA 產生的記號。
	
* *X-Auth-Scope-Id* 參數會傳遞空間 GUID。GUID 必須加上字首 *s-*，以識別空間。 
	
* Token 是 UAA 或 IAM 鑑別記號，或是 API 金鑰。
	
* Space 是空間的 GUID。 
	
* METRICS_ENDPOINT 代表服務的進入點。每一個地區都有不同的 URL。若要取得每個地區的端點清單，請參閱[端點](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints)。


## 步驟 4：刪除通知
{: #step4_delete_notifications}
  

執行下列 cURL 指令，以刪除空間網域中的通知：

```
curl -H "X-Auth-Scope-Id: ${Space}" -H “X-Auth-User-Token: Auth_Type ${TOKEN}" -XDELETE METRICS_ENDPOINT/v1/alert/notification/{name} 
```
{: screen}

執行下列 cURL 指令，以刪除帳戶網域中的通知：

```
curl -H "X-Auth-User-Token: apikey ${TOKEN}" -XDELETE METRICS_ENDPOINT/v1/alert/notification/{name} 
```
{: screen}

	
其中
	
* *X-Auth-User-Token* 參數會傳遞 {{site.data.keyword.Bluemix_notm}} UAA 記號、IAM 記號或 API 金鑰。
	
* *Auth_Type* 是定義記號或 API 金鑰類型的字首。下列清單概述有效值：*apikey*、*iam* 或 *uaa*，其中

    * *apikey* 識別該記號是 API 金鑰。
	* *iam* 識別所指定的記號是 IAM 產生的記號。
	* *uaa* 識別所指定的記號是 UAA 產生的記號。
	
* *X-Auth-Scope-Id* 參數會傳遞空間 GUID。GUID 必須加上字首 *s-*，以識別空間。 
	
* Token 是 UAA 或 IAM 鑑別記號，或是 API 金鑰。
	
* Space 是空間的 GUID。 
	
* METRICS_ENDPOINT 代表服務的進入點。每一個地區都有不同的 URL。若要取得每個地區的端點清單，請參閱[端點](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints)。

* *name* 是您要刪除的通知的名稱。
	
