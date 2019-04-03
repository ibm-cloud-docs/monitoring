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

使用 Alerts API 來建立、刪除及更新通知、顯示通知的詳細資料，以及列出空間中所定義的通知。
{:shortdesc}

## 建立通知
{: #notifications_create}

若要建立通知，請完成下列步驟：

1. 建立通知檔案。

    1. 使用通知範本來建立通知檔案。如需相關資訊，請參閱[通知範本](/docs/services/cloud-monitoring/config_alerts_ov.html#notification_template)。
	
	2. 更新檔案：
	
	    * 在 *name* 欄位中輸入唯一名稱。此欄位的值稍後會用於更新、刪除及顯示通知的詳細資料。
		* 輸入說明。
		* 輸入有效的電子郵件位址、URL 端點或 PagerDuty 金鑰。
		
	3. 儲存檔案。例如，請對您為空間中所執行查詢定義的通知，使用 *s-* 之類的字首。
	
	    **提示：**請在下列目錄中建立通知檔案：*~/cloud-monitoring/notifications/*，以將 {{site.data.keyword.monitoringshort_notm}} 服務的資源分組。 
	
	4. 匯出變數 *NOTIFICATION_FILE*：
	
	```
	export NOTIFICATION_FILE="mynotificationfile.json"
	```
	{: screen}
	
2. 登入 {{site.data.keyword.Bluemix_notm}} 中的地區、組織及空間。 

    如需相關資訊，請參閱[如何登入 {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login)。

3. 取得安全記號。您可以使用 UAA 記號、IAM 記號或 API 金鑰。選擇下列其中一種方法來取得安全記號：
	
	* 若要取得 UAA 記號，請參閱[使用 {{site.data.keyword.Bluemix_notm}} CLI 取得 UAA 記號](/docs/services/cloud-monitoring/security/auth_uaa.html#uaa_cli)。
	
	* 若要取得 IAM 記號，請參閱[使用 {{site.data.keyword.Bluemix_notm}} CLI 取得 IAM 記號](/docs/services/cloud-monitoring/security/auth_iam.html#auth_iam)。
	
	* 若要取得 API 金鑰，請參閱[取得 API 金鑰](/docs/services/cloud-monitoring/security/auth_api_key.html#auth_api_key)。
	
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
	
4. 取得空間 GUID。GUID 必須加上字首 *s-*，以識別空間。

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
	
	然後，匯出變數 *Space*：
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
5. 向 {{site.data.keyword.monitoringshort}} 服務登錄通知。

    ```
	curl -XPOST -d @$NOTIFICATION_FILE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notification
	```
	{: codeblock}
	
	其中
	
	* NOTIFICATION_FILE 是用於定義通知的 JSON 檔案。
	
	* *X-Auth-User-Token* 參數會傳遞 {{site.data.keyword.Bluemix_notm}} UAA 記號、IAM 記號或 API 金鑰。
	
	* *Auth_Type* 是定義記號或 API 金鑰類型的字首。下列清單概述有效值：*apikey*、*iam* 或 *uaa*，其中

        * *apikey* 識別該記號是 API 金鑰。
		* *iam* 識別所指定的記號是 IAM 產生的記號。
		* *uaa* 識別所指定的記號是 UAA 產生的記號。
	
	* *X-Auth-Scope-Id* 參數會傳遞空間 GUID。GUID 必須加上字首 *s-*，以識別空間。如果您使用 UAA 記號鑑別，此標頭為必要項目。如果您使用 IAM 鑑別記號，則此標頭是選用項目，並且會使用連結至該記號的網域資訊。
	
	* Token 是 UAA 記號、IAM 記號或 API 金鑰。
	
	* Space 是空間的 GUID。 
	
	* METRICS_ENDPOINT 代表服務的進入點。每一個地區都有不同的 URL。若要取得每個地區的端點清單，請參閱[端點](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints)。
	
    例如， 	
	
	```
	curl -XPOST -d @$NOTIFICATION_FILE  --header "X-Auth-User-Token: iam ${Token}" https://metrics.ng.bluemix.net/v1/alert/notification
	```
	{: screen}

## 刪除通知
{: #notifications_delete}

若要刪除通知，請完成下列步驟：

1. 登入 {{site.data.keyword.Bluemix_notm}} 中的地區、組織及空間。 

    如需相關資訊，請參閱[如何登入 {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login)。

2. 取得安全記號。您可以使用 UAA 記號、IAM 記號或 API 金鑰。選擇下列其中一種方法來取得安全記號：
	
	* 若要取得 UAA 記號，請參閱[使用 {{site.data.keyword.Bluemix_notm}} CLI 取得 UAA 記號](/docs/services/cloud-monitoring/security/auth_uaa.html#uaa_cli)。
	
	* 若要取得 IAM 記號，請參閱[使用 {{site.data.keyword.Bluemix_notm}} CLI 取得 IAM 記號](/docs/services/cloud-monitoring/security/auth_iam.html#auth_iam)。
	
	* 若要取得 API 金鑰，請參閱[取得 API 金鑰](/docs/services/cloud-monitoring/security/auth_api_key.html#auth_api_key)。
	
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
	
	然後，匯出變數 *Space*：
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. 執行下列 cURL 指令，以刪除通知：

    ```
	curl -XDELETE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notification/Notification_Name
	```
	{: codeblock}
	
	其中
	
	* *X-Auth-User-Token* 參數會傳遞 UAA 記號、IAM 記號或 API 金鑰。
	
	* *Auth_Type* 是定義記號或 API 金鑰類型的字首。下列清單概述有效值：*apikey*、*iam* 或 *uaa*，其中

        * *apikey* 識別該記號是 API 金鑰。
		* *iam* 識別所指定的記號是 IAM 產生的記號。
		* *uaa* 識別所指定的記號是 UAA 產生的記號。
	
	* *X-Auth-User-Token* 參數會傳遞 {{site.data.keyword.Bluemix_notm}} UAA 記號、IAM 記號或 API 金鑰。記號或 API 金鑰必須加上下列其中一個值作為字首：*apikey*、*iam* 或 *uaa*，其中

        * *apikey* 識別該記號是 API 金鑰。
		* *iam* 識別所指定的記號是 IAM 產生的記號。
		* *uaa* 識別所指定的記號是 UAA 產生的記號。
		
	* Token 是 UAA 記號、IAM 記號或 API 金鑰。
	
	* Space 是空間的 GUID。 
	
	* Notification_Name 是通知的名稱，亦即當您列出通知內容時的 *name* 欄位值。
	
	* METRICS_ENDPOINT 代表服務的進入點。每一個地區都有不同的 URL。若要取得每個地區的端點清單，請參閱[端點](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints)。
	


## 列出所有通知
{: #notifications_list}

若要列出所有通知，請完成下列步驟：

1. 登入 {{site.data.keyword.Bluemix_notm}} 中的地區、組織及空間。 

    如需相關資訊，請參閱[如何登入 {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login)。

2. 取得安全記號。您可以使用 UAA 記號、IAM 記號或 API 金鑰。選擇下列其中一種方法來取得安全記號：
	
	* 若要取得 UAA 記號，請參閱[使用 {{site.data.keyword.Bluemix_notm}} CLI 取得 UAA 記號](/docs/services/cloud-monitoring/security/auth_uaa.html#uaa_cli)。
	
	* 若要取得 IAM 記號，請參閱[使用 {{site.data.keyword.Bluemix_notm}} CLI 取得 IAM 記號](/docs/services/cloud-monitoring/security/auth_iam.html#auth_iam)。
	
	* 若要取得 API 金鑰，請參閱[取得 API 金鑰](/docs/services/cloud-monitoring/security/auth_api_key.html#auth_api_key)。
	
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
	
	然後，匯出變數 *Space*：
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. 執行下列 cURL 指令，以列出所有通知：

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notifications
	```
	{: codeblock}
	
	其中
	
	* *X-Auth-User-Token* 參數會傳遞 {{site.data.keyword.Bluemix_notm}} UAA 記號、IAM 記號或 API 金鑰。
	
	* *Auth_Type* 是定義記號或 API 金鑰類型的字首。下列清單概述有效值：*apikey*、*iam* 或 *uaa*，其中

        * *apikey* 識別該記號是 API 金鑰。
		* *iam* 識別所指定的記號是 IAM 產生的記號。
		* *uaa* 識別所指定的記號是 UAA 產生的記號。
		
	* *X-Auth-User-Token* 參數會傳遞 {{site.data.keyword.Bluemix_notm}} UAA 記號、IAM 記號或 API 金鑰。記號或 API 金鑰必須加上下列其中一個值作為字首：*apikey*、*iam* 或 *uaa*，其中

        * *apikey* 識別該記號是 API 金鑰。
		* *iam* 識別所指定的記號是 IAM 產生的記號。
		* *uaa* 識別所指定的記號是 UAA 產生的記號。
		
	* Token 是 UAA 記號、IAM 記號或 API 金鑰。
	
	* Space 是空間的 GUID。 
	
	* METRICS_ENDPOINT 代表服務的進入點。每一個地區都有不同的 URL。若要取得每個地區的端點清單，請參閱[端點](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints)。

			

## 顯示通知的詳細資料
{: #show}


若要顯示通知的相關資訊，請完成下列步驟：

1. 登入 {{site.data.keyword.Bluemix_notm}} 中的地區、組織及空間。 

    如需相關資訊，請參閱[如何登入 {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login)。

2. 取得安全記號。您可以使用 UAA 記號、IAM 記號或 API 金鑰。選擇下列其中一種方法來取得安全記號：
	
	* 若要取得 UAA 記號，請參閱[使用 {{site.data.keyword.Bluemix_notm}} CLI 取得 UAA 記號](/docs/services/cloud-monitoring/security/auth_uaa.html#uaa_cli)。
	
	* 若要取得 IAM 記號，請參閱[使用 {{site.data.keyword.Bluemix_notm}} CLI 取得 IAM 記號](/docs/services/cloud-monitoring/security/auth_iam.html#auth_iam)。
	
	* 若要取得 API 金鑰，請參閱[取得 API 金鑰](/docs/services/cloud-monitoring/security/auth_api_key.html#auth_api_key)。
	
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
	
	然後，匯出變數 *Space*：
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. 執行下列 cURL 指令，以顯示通知的詳細資料：

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notification/NOTIFICATION_NAME
	```
	{: codeblock}
	
	其中
	
	* *X-Auth-User-Token* 參數會傳遞 {{site.data.keyword.Bluemix_notm}} UAA 記號、IAM 記號或 API 金鑰。
	
	* *Auth_Type* 是定義記號或 API 金鑰類型的字首。下列清單概述有效值：*apikey*、*iam* 或 *uaa*，其中

        * *apikey* 識別該記號是 API 金鑰。
		* *iam* 識別所指定的記號是 IAM 產生的記號。
		* *uaa* 識別所指定的記號是 UAA 產生的記號。
		
	* Token 是 UAA 記號、IAM 記號或 API 金鑰。
	
	* Space 是空間的 GUID。 
	
	* NOTIFICATION_NAME 是通知的名稱，亦即當您列出通知內容時的 *name* 欄位值。
	
	* METRICS_ENDPOINT 代表服務的進入點。每一個地區都有不同的 URL。若要取得每個地區的端點清單，請參閱[端點](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints)。
	
     
		

			
## 測試通知
{: #test}	
			
若要測試通知，請完成下列步驟：

1. 登入 {{site.data.keyword.Bluemix_notm}} 中的地區、組織及空間。 

    如需相關資訊，請參閱[如何登入 {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login)。

2. 取得安全記號。您可以使用 UAA 記號、IAM 記號或 API 金鑰。選擇下列其中一種方法來取得安全記號：
	
	* 若要取得 UAA 記號，請參閱[使用 {{site.data.keyword.Bluemix_notm}} CLI 取得 UAA 記號](/docs/services/cloud-monitoring/security/auth_uaa.html#uaa_cli)。
	
	* 若要取得 IAM 記號，請參閱[使用 {{site.data.keyword.Bluemix_notm}} CLI 取得 IAM 記號](/docs/services/cloud-monitoring/security/auth_iam.html#auth_iam)。
	
	* 若要取得 API 金鑰，請參閱[取得 API 金鑰](/docs/services/cloud-monitoring/security/auth_api_key.html#auth_api_key)。
	
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
	
	然後，匯出變數 *Space*：
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. 執行下列 cURL 指令，以測試通知：

    ```
	curl -XPOST --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notification/test/NOTIFICATION_NAME
	```
	{: codeblock}
	
	其中
	
	* *X-Auth-User-Token* 參數會傳遞 {{site.data.keyword.Bluemix_notm}} UAA 記號、IAM 記號或 API 金鑰。
	
	* *Auth_Type* 是定義記號或 API 金鑰類型的字首。下列清單概述有效值：*apikey*、*iam* 或 *uaa*，其中

        * *apikey* 識別該記號是 API 金鑰。
		* *iam* 識別所指定的記號是 IAM 產生的記號。
		* *uaa* 識別所指定的記號是 UAA 產生的記號。
	
	* *X-Auth-User-Token* 參數會傳遞 {{site.data.keyword.Bluemix_notm}} UAA 記號、IAM 記號或 API 金鑰。記號或 API 金鑰必須加上下列其中一個值作為字首：*apikey*、*iam* 或 *uaa*，其中

        * *apikey* 識別該記號是 API 金鑰。
		* *iam* 識別所指定的記號是 IAM 產生的記號。
		* *uaa* 識別所指定的記號是 UAA 產生的記號。
		
	* Token 是 UAA 記號、IAM 記號或 API 金鑰。
	
	* Space 是空間的 GUID。 
	
	* NOTIFICATION_NAME 是通知的名稱，亦即當您列出通知內容時的 *name* 欄位值。
	
	* METRICS_ENDPOINT 代表服務的進入點。每一個地區都有不同的 URL。若要取得每個地區的端點清單，請參閱[端點](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints)。
	


## 更新通知
{: #notifications_update}

若要更新通知，請完成下列步驟：

1. 登入 {{site.data.keyword.Bluemix_notm}} 中的地區、組織及空間。 

    如需相關資訊，請參閱[如何登入 {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login)。

2. 取得安全記號。您可以使用 UAA 記號、IAM 記號或 API 金鑰。選擇下列其中一種方法來取得安全記號：
	
	* 若要取得 UAA 記號，請參閱[使用 {{site.data.keyword.Bluemix_notm}} CLI 取得 UAA 記號](/docs/services/cloud-monitoring/security/auth_uaa.html#uaa_cli)。
	
	* 若要取得 IAM 記號，請參閱[使用 {{site.data.keyword.Bluemix_notm}} CLI 取得 IAM 記號](/docs/services/cloud-monitoring/security/auth_iam.html#auth_iam)。
	
	* 若要取得 API 金鑰，請參閱[取得 API 金鑰](/docs/services/cloud-monitoring/security/auth_api_key.html#auth_api_key)。
	
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
	
	然後，匯出變數 *Space*：
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. 執行下列 cURL 指令，以更新通知：

    ```
	curl -XPUT -d @$NOTIFICATION_FILE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notification
	```
	{: codeblock}
	
	其中
	
	* NOTIFICATION_FILE 是用於定義通知的 JSON 檔案。
	
	* *Auth_Type* 是定義記號或 API 金鑰類型的字首。下列清單概述有效值：*apikey*、*iam* 或 *uaa*，其中

        * *apikey* 識別該記號是 API 金鑰。
		* *iam* 識別所指定的記號是 IAM 產生的記號。
		* *uaa* 識別所指定的記號是 UAA 產生的記號。
	
	* *X-Auth-User-Token* 參數會傳遞 Bluemix UAA 記號、IAM 記號或 API 金鑰。記號或 API 金鑰必須加上下列其中一個值作為字首：*apikey*、*iam* 或 *uaa*，其中

        * *apikey* 識別該記號是 API 金鑰。
		* *iam* 識別所指定的記號是 IAM 產生的記號。
		* *uaa* 識別所指定的記號是 UAA 產生的記號。
		
	* Token 是 UAA 記號、IAM 記號或 API 金鑰。
	
	* Space 是空間的 GUID。 

	* METRICS_ENDPOINT 代表服務的進入點。每一個地區都有不同的 URL。若要取得每個地區的端點清單，請參閱[端點](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints)。
	
        

