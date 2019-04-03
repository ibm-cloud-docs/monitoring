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


# CRUD 規則
{: #rules}

使用 Alerts API 來建立、刪除或更新規則、顯示規則的詳細資料，以及列出空間中所定義的規則。
{:shortdesc}


## 建立規則
{: #create}

若要在 {{site.data.keyword.monitoringshort}} 服務中配置規則，請建立包括規則詳細資料的規則檔案，並向 {{site.data.keyword.monitoringshort}} 服務登錄此規則。

請完成下列步驟：

1. 建立規則檔案，其中包含有效的 JSON。儲存檔案。 

    例如，若要儲存檔案，請對您為空間中所執行查詢定義的規則，使用 *s-* 之類的字首。
	
	**提示：** 
	
	* 請使用不同的通知方法，為警示錯誤或警告的查詢定義不同的規則。 
	* 請在下列目錄中建立規則檔案：*~/cloud-monitoring/rules/*，以將 {{site.data.keyword.monitoringshort_notm}} 服務的資源分組。 

    在規則的檔案中輸入下列資訊：
	
	* *name*：輸入唯一名稱。此欄位的值稍後會用於更新、刪除及顯示規則的詳細資料。
	* *description*：輸入說明。
	* *expression*：輸入您要監視的查詢。
	* *enabled*：設為 *true* 以啟用規則。
	* *from*：用來根據臨界值分析資料的起始復原點。
	* *until*：用來根據臨界值分析資料的最終復原點。
	* *comparison*：用來識別進行哪種類型檢查的比較作業，例如 *below*。
	* *error_level*：定義您設定要觸發錯誤警示的臨界值。
	* *warning_level*：定義您設定要觸發警告警示的臨界值。
	* *frequency*：定義檢查資料的頻率。
	* *dashboard_url*：定義 URL，它會在 Grafana 顯示具有查詢的儀表板。
	* *notifications*：此規則所述警示觸發時的通知方法。
	
	例如，規則檔案 myrulefile.json 會如下所示：
	
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
	
	然後，匯出變數 *RULE_FILE*：
	
	```
	export RULE_FILE="myrulefile.json"
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
IAM token:  Bearer djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
    {: screen}
	
    然後，匯出變數 *Token*：
	
    ```
export Token="djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ"
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
	
5. 執行下列 cURL 指令，以在 {{site.data.keyword.monitoringshort}} 服務中登錄規則：

    ```
	curl -XPOST -d @$RULE_FILE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/rule
	```
	{: codeblock}
	
	其中
	
	* RULE_FILE 是用於定義警示規則的 JSON 檔案。
	
	* *X-Auth-User-Token* 參數會傳遞 {{site.data.keyword.Bluemix_notm}} UAA 記號、IAM 記號或 API 金鑰。
	
	* *Auth_Type* 是定義記號或 API 金鑰類型的字首。下列清單概述有效值：*apikey*、*iam* 或 *uaa*，其中

        * *apikey* 識別該記號是 API 金鑰。
		* *iam* 識別所指定的記號是 IAM 產生的記號。
		* *uaa* 識別所指定的記號是 UAA 產生的記號。
	
	* *X-Auth-Scope-Id* 參數會傳遞空間 GUID。GUID 必須加上字首 *s-*，以識別空間。如果您使用 UAA 記號鑑別，此標頭為必要項目。如果您使用 IAM 鑑別記號，則此標頭是選用項目，並且會使用連結至該記號的網域資訊。
	
	* Token 是 UAA 或 IAM 鑑別記號，或是 API 金鑰。
	
	* Space 是空間的 GUID。 
	
	* METRICS_ENDPOINT 代表服務的進入點。每一個地區都有不同的 URL。若要取得每個地區的端點清單，請參閱[端點](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints)。
	
    例如， 	
	
	```
	curl -XPOST -d @$RULE_FILE --header "X-Auth-User-Token:iam ${Token}" https://metrics.ng.bluemix.net/v1/alert/rule
	```
	{: screen}

## 刪除規則
{: #delete}

若要刪除規則，請完成下列步驟：

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
	IAM token:  Bearer djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	然後，匯出變數 *Token*：
	
	```
	export Token="djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ"
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
		
4. 執行下列 cURL 指令，以刪除規則：

    ```
	curl -XDELETE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/rule/Rule_Name
	```
	{: codeblock}
	
	其中
	
    * *X-Auth-User-Token* 參數會傳遞 UAA 記號、IAM 記號或 API 金鑰。
	
	* *Auth_Type* 是定義記號或 API 金鑰類型的字首。下列清單概述有效值：*apikey*、*iam* 或 *uaa*，其中

        * *apikey* 識別該記號是 API 金鑰。
		* *iam* 識別所指定的記號是 IAM 產生的記號。
		* *uaa* 識別所指定的記號是 UAA 產生的記號。
	
	* *X-Auth-Scope-Id* 參數會傳遞空間 GUID。GUID 必須加上字首 *s-*，以識別空間。如果您使用 UAA 記號鑑別，此標頭為必要項目。如果您使用 IAM 鑑別記號，則此標頭是選用項目，並且會使用連結至該記號的網域資訊。
	
	* Token 是 UAA 或 IAM 鑑別記號，或是 API 金鑰。
	
	* Space 是空間的 GUID。 
	
	* Rule_Name 是 *name* 欄位中指定的規則名稱。
	
	* METRICS_ENDPOINT 代表服務的進入點。每一個地區都有不同的 URL。若要取得每個地區的端點清單，請參閱[端點](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints)。
	
    
	
## 列出所有規則
{: #list}

若要列出所有規則，請完成下列步驟：

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
	IAM token:  Bearer djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	然後，匯出變數 *Token*：
	
	```
	export Token="djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ"
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
	
4. 執行下列 cURL 指令，以列出空間中的所有規則：

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/rules
	```
	{: codeblock}
	
	其中
	
	* *X-Auth-User-Token* 參數會傳遞 UAA 記號、IAM 記號或 API 金鑰。
	
	* *Auth_Type* 是定義記號或 API 金鑰類型的字首。下列清單概述有效值：*apikey*、*iam* 或 *uaa*，其中

        * *apikey* 識別該記號是 API 金鑰。
		* *iam* 識別所指定的記號是 IAM 產生的記號。
		* *uaa* 識別所指定的記號是 UAA 產生的記號。
	
	* *X-Auth-Scope-Id* 參數會傳遞空間 GUID。GUID 必須加上字首 *s-*，以識別空間。如果您使用 UAA 記號鑑別，此標頭為必要項目。如果您使用 IAM 鑑別記號，則此標頭是選用項目，並且會使用連結至該記號的網域資訊。
	
	* Token 是 UAA 或 IAM 鑑別記號，或是 API 金鑰。
	
	* Space 是空間的 GUID。 
	
	* METRICS_ENDPOINT 代表服務的進入點。每一個地區都有不同的 URL。若要取得每個地區的端點清單，請參閱[端點](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints)。
	

	
	

## 顯示規則的詳細資料
{: show}

若要顯示規則的詳細資料，請完成下列步驟：

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
	IAM token:  Bearer djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	然後，匯出變數 *Token*：
	
	```
	export Token="djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ"
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
	
4. 執行下列 cURL 指令，以顯示規則的詳細資料：

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/rule/Rule_Name
	```
	{: codeblock}
	
	其中
	
	* *X-Auth-User-Token* 參數會傳遞 UAA 記號、IAM 記號或 API 金鑰。
	
	* *Auth_Type* 是定義記號或 API 金鑰類型的字首。下列清單概述有效值：*apikey*、*iam* 或 *uaa*，其中

        * *apikey* 識別該記號是 API 金鑰。
		* *iam* 識別所指定的記號是 IAM 產生的記號。
		* *uaa* 識別所指定的記號是 UAA 產生的記號。
	
	* *X-Auth-Scope-Id* 參數會傳遞空間 GUID。GUID 必須加上字首 *s-*，以識別空間。如果您使用 UAA 記號鑑別，此標頭為必要項目。如果您使用 IAM 鑑別記號，則此標頭是選用項目，並且會使用連結至該記號的網域資訊。
	
	* Token 是 UAA 或 IAM 鑑別記號，或是 API 金鑰。
	
	* Space 是空間的 GUID。 
	
	* Rule_Name 是 *name* 欄位中指定的規則名稱。
	
	* METRICS_ENDPOINT 代表服務的進入點。每一個地區都有不同的 URL。若要取得每個地區的端點清單，請參閱[端點](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints)。
	

## 更新規則
{: #update}

若要更新規則，請藉由更新規則檔案來修改規則，然後完成下列步驟：

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
	IAM token:  Bearer djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	然後，匯出變數 *Token*：
	
	```
	export Token="djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ"
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
	
4. 執行下列 cURL 指令，以更新規則：

    ```
	curl -XPUT `-d @$RULE_FILE` --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/rule
	```
	{: codeblock}
	
	其中
	
	* RULE_FILE 是用於定義警示規則的 JSON 檔案。
	
	* *X-Auth-User-Token* 參數會傳遞 UAA 記號、IAM 記號或 API 金鑰。
	
	* *Auth_Type* 是定義記號或 API 金鑰類型的字首。下列清單概述有效值：*apikey*、*iam* 或 *uaa*，其中

        * *apikey* 識別該記號是 API 金鑰。
		* *iam* 識別所指定的記號是 IAM 產生的記號。
		* *uaa* 識別所指定的記號是 UAA 產生的記號。
	
	* *X-Auth-Scope-Id* 參數會傳遞空間 GUID。GUID 必須加上字首 *s-*，以識別空間。如果您使用 UAA 記號鑑別，此標頭為必要項目。如果您使用 IAM 鑑別記號，則此標頭是選用項目，並且會使用連結至該記號的網域資訊。
	
	* Token 是 UAA 或 IAM 鑑別記號，或是 API 金鑰。
	
	* Space 是空間的 GUID。 
	
	* METRICS_ENDPOINT 代表服務的進入點。每一個地區都有不同的 URL。若要取得每個地區的端點清單，請參閱[端點](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints)。

	
	
