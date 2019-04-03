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


# 取得 UAA 記號
{: #auth_uaa}

使用 {{site.data.keyword.Bluemix}} UAA 模型來取得您可用來使用 {{site.data.keyword.monitoringshort}} 服務的鑑別記號。您可以使用 {{site.data.keyword.Bluemix_notm}} CLI 來取得鑑別記號。
{:shortdesc}

記號具有有效期限。 
		
## 使用 IBM Cloud CLI 取得 UAA 記號
{: #uaa_cli}


若要取得 UAA 記號，請完成下列步驟：

1. （必要條件）安裝 {{site.data.keyword.Bluemix_notm}} CLI。

   如需相關資訊，請參閱[安裝 {{site.data.keyword.Bluemix_notm}} CLI](/docs/services/cloud-monitoring/qa/cli_qa.html#cli_qa)。
   
   如果已安裝 CLI，請繼續進行下一步。
    
2. 登入 {{site.data.keyword.Bluemix_notm}} 中的地區、組織及空間。 

    如需相關資訊，請參閱[如何登入 {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login)。
	
3. 執行 `ibmcloud iam oauth-tokens` 指令，以取得 UAA 記號。

    ```
	ibmcloud iam oauth-tokens
	```
	{: codeblock}
	
	輸出會傳回 UAA 記號。

**附註：**在使用記號時，請從在 API 呼叫中傳遞的記號值中移除 *Bearer*。
	


	
