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


# 使用 API 金鑰
{: #auth_api_key}

您可以使用 {{site.data.keyword.Bluemix}} CLI 或 {{site.data.keyword.Bluemix_notm}} 使用者介面來取得 API。API 金鑰不會到期。
如果 API 已外洩，您可以撤銷它，並產生新的 API。
{:shortdesc}

## 使用 IBM Cloud CLI 產生 IAM API 金鑰
{: #iam_apikey_cli}

完成下列步驟，以使用 {{site.data.keyword.Bluemix_notm}} CLI 產生 API 金鑰：

1. （必要條件）安裝 {{site.data.keyword.Bluemix_notm}} CLI。

   如需相關資訊，請參閱[安裝 {{site.data.keyword.Bluemix_notm}} CLI](/docs/services/cloud-monitoring/qa/cli_qa.html#cli_qa)。
   
   如果已安裝 CLI，請繼續進行下一步。
	
2. 登入 {{site.data.keyword.Bluemix_notm}} 中的地區、組織及空間。 

    如需相關資訊，請參閱[如何登入 {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login)。
 
3. 執行 `ibmcloud iam api-key-create` 指令，以建立 API 金鑰。

    ```
    ibmcloud iam api-key-create NAME [-d DESCRIPTION][-f, --file FILE]
	```
	{: codeblock} 
	
	其中
	
	* NAME 是要建立之 API 金鑰的名稱。
	* DESCRIPTION 是用來說明 API 金鑰的文字。
	* FILE 是儲存金鑰的檔案名稱。
	
    例如，若要建立 API 金鑰 *MyKey*，請執行下列指令：
	
	```
	ibmcloud iam api-key-create MyKey -d "This is my API key for service X" 
	```
	{: screen}
	
	
	
	
## 使用 IBM Cloud 使用者介面產生 IAM API 金鑰
{: #iam_apikey_ui}

請完成下列步驟，透過 {{site.data.keyword.Bluemix_notm}} 使用者介面產生 API 金鑰：

1. 登入 {{site.data.keyword.Bluemix_notm}} 主控台。

    開啟 Web 瀏覽器，並啟動 {{site.data.keyword.Bluemix_notm}} 儀表板：[http://console.bluemix.net ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](http://bluemix.net){:new_window}
	
	使用您的使用者 ID 和密碼登入之後，{{site.data.keyword.Bluemix_notm}} 使用者介面隨即開啟。

2. 從主控台功能表列中，按一下**管理 > 安全 > IBM Cloud API 金鑰**。

3. 按一下**建立 API 金鑰**。

4. 輸入 API 金鑰的名稱及說明。然後，按一下**建立 API 金鑰**。

5. 儲存 API 金鑰。按一下**下載 API 金鑰**。

    按一下**顯示**，以顯示 API 金鑰。  

**附註：**只能在建立時顯示或下載 API 金鑰。如果 API 金鑰遺失，您必須建立新的 API 金鑰。  


	
## 使用 IBM Cloud 使用者介面撤銷 API 金鑰
{: #revoke_ui}
	
請完成下列步驟，透過 {{site.data.keyword.Bluemix_notm}} 使用者介面撤銷 IAM API 金鑰：

1. 登入 {{site.data.keyword.Bluemix_notm}} 主控台。

    開啟 Web 瀏覽器，並啟動 {{site.data.keyword.Bluemix_notm}} 儀表板：[http://console.bluemix.net ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](http://bluemix.net){:new_window}
	
	使用您的使用者 ID 和密碼登入之後，{{site.data.keyword.Bluemix_notm}} 使用者介面隨即開啟。

2. 從主控台功能表列中，按一下**管理 > 安全 > IBM Cloud API 金鑰**。

3. 按一下**動作**，然後按一下**刪除金鑰**。





	

	
	
	
	
	
	
