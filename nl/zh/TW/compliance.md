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


# 法規遵循
{: #compliance}

[{{site.data.keyword.Bluemix}} 提供雲端平台及服務，它們是遵照 IBM 嚴格的安全標準而建置。](/docs/security/compliance.html#compliance){{site.data.keyword.monitoringlong}} 服務是針對 {{site.data.keyword.Bluemix_notm}} 而建置的 DevOps 服務。
{:shortdesc}


## 一般資料保護規範

「一般資料保護規範 (GDPR)」嘗試建立跨歐盟的協調資料保護法律架構，而且目的是將居民的個人資料控制權返還給居民，同時對於在全球任何位置管理及「處理」此資料的人強制施行嚴格的規則。此「規範」也會建立與在歐盟內外部自由移動個人資料有關的規則。 

**聲明：**{{site.data.keyword.monitoringshort}} 服務會針對您 {{site.data.keyword.Bluemix_notm}} 帳戶中執行的雲端資源，儲存及顯示其度量值，以及您可能從 {{site.data.keyword.Bluemix_notm}} 之外傳送的度量值。「個人資訊 (PI)」不得包含在 {{site.data.keyword.monitoringshort}} 中儲存的任何度量值項目，因為您企業內的其他使用者能存取此資料，{{site.data.keyword.IBM_notm}} 為了能夠支援雲端服務也能存取此資料。

### 地區
{: #regions}

{{site.data.keyword.monitoringshort}} 服務在提供該服務的「{{site.data.keyword.Bluemix_notm}} 公用」地區中遵循 GDPR。


### 資料保留
{: #data_retention}

{{site.data.keyword.monitoringshort}} 服務會針對標準或精簡方案儲存度量值長達 15 天，針對超值方案則為 45 天。


### 資料刪除
{: #data_deletion}

請考量下列資訊：

* 針對 {{site.data.keyword.monitoringshort}} 服務標準或精簡方案，度量值會自動在 15 天之後刪除。
* 針對 {{site.data.keyword.monitoringshort}} 服務超值方案，度量值會自動在 45 天之後刪除。
* 在 7 天之後自動刪除非作用中度量值。


 您可以隨時使用 Metrics API 來刪除您的度量值。 



### 相關資訊
{: #info}

如需相關資訊，請參閱：

[{{site.data.keyword.Bluemix_notm}} 安全規範](/docs/security/compliance.html#compliance)

[GDPR - {{site.data.keyword.IBM_notm}} 官方頁面](https://www.ibm.com/data-responsibility/gdpr/)



