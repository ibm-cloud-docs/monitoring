---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, metrics

subcollection: Sysdig

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

# 使用度量值
{: #metrics}

在 {{site.data.keyword.Bluemix}} 中佈建 {{site.data.keyword.mon_full_notm}} 服務的實例，並為度量值來源配置 Sysdig 代理程式之後，您可以透過 {{site.data.keyword.mon_full_notm}} Web 使用者介面來檢視、監視及管理度量值。使用度量值，以統計方式分析具有數值的資料。
{:shortdesc}


**度量值是一種定量測量，具有一個以上的標籤來定義其特徵。**

度量值是以時間序列表示。 

時間序列是一組經過一段時間的數值資料點。 

度量值會分類為兩個群組： 

* 預設度量值 
* 自訂度量值


## 標籤
{: #metrics_labels}

**標籤定義度量值的特徵。**

標籤可分類為基礎架構標籤和度量值描述子標籤。每一個度量值都有一組預先定義的標籤。對於自訂度量值，您可以配置其他標籤。 

您可以使用標籤來識別及區分度量值的特徵，例如，
* 您可以將基礎架構物件分組為邏輯階層。 
* 您可以過濾掉資料。 
* 您可以將聚集資料分割為區段。 


## 預設度量值 
{: #metrics_default}

**預設度量會報告系統、編排器及網路基礎架構上的度量值。**

監視服務會自動將標籤新增至每一個度量值。


## 自訂度量值
{: #metrics_custom}

**自訂度量值根據基礎架構的類型及您監視的應用程式而有所不同。部分範例為 JMX、Prometheus 及 StatsD。**

這些度量值具有一組預先定義的標籤。您可以新增其他自訂標籤。

監視服務會維護過去 14 天報告資料之所有自訂度量值和自訂標籤的索引。您可以使用這些度量值來配置儀表板、範圍及警示。

請考量關於監視服務如何管理索引項目的下列資訊：
*  當發生下列任何狀況時，會自動從監視服務索引中移除度量值，並標示為遺漏：
    
    * 監視服務不會接收任何超過 14 天的度量值或標籤資料。
    
    * 度量值或標籤從未報告資料。

* 您無法配置遺漏度量值或遺漏標籤的新構件。 
* 您無法更新現有構件，直到遺漏的度量值和標籤從現行配置中移除為止。
* 您可以在資料查詢和圖表上使用遺漏的度量值或遺漏的標籤。 
* 如果您的現有構件包括遺漏的度量值或遺漏的標籤，則它們不會受到影響。
* 當收到遺漏度量值或標籤的資料時，該度量值或標籤會新增回索引。



