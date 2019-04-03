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


# 建立 Grafana 儀表板以監視 Kubernetes 叢集
{: #container_grafana_dashboard}


使用此指導教學，以學習如何在 {{site.data.keyword.monitoringlong}} 服務中建立 Grafana 儀表板，以監視叢集的效能。
{:shortdesc}


## 目標
{: #cgd_objectives}

學習如何搜尋及分析 Kubernetes 叢集中所部署應用程式的容器度量值：

1. 啟動 Grafana，並設定您可檢視叢集度量值的 {{site.data.keyword.monitoringshort}} 網域。
2. 建立 Grafana 儀表板，以及定義度量值來監視容器的 CPU 用量。


## 假設情況
{: #cgd_assumptions}

此指導教學假設：

* 叢集可以在「美國南部」地區中使用。 
* 您的使用者 ID 具有 {{site.data.keyword.monitoringshort}} 服務的 IAM 原則及 **viewer** 許可權。

若要完成此指導教學，您必須完成[在 Grafana 中分析 Kubernetes 叢集中所部署應用程式的度量值](/docs/services/cloud-monitoring/tutorials?topic=cloud-monitoring-container_service_metrics#container_service_metrics)指導教學，或已佈建至少部署 1 個應用程式的叢集。



## 步驟 1：啟動 Grafana
{: #cgd_step1}

從瀏覽器啟動 Grafana，並設定您可檢視叢集度量值的 {{site.data.keyword.monitoringshort}} 網域。

若要分析叢集的度量值，您必須在叢集建立所在的「雲端公用」地區中存取 Grafana。如需相關資訊，請參閱[從 Web 瀏覽器導覽至 Grafana 儀表板](/docs/services/cloud-monitoring/grafana?topic=cloud-monitoring-navigating_grafana#launch_grafana_from_browser)。

1. 從瀏覽器啟動 Grafana。 

    輸入您已建立叢集之地區的 {{site.data.keyword.monitoringshort}} 服務 URL。 
    
    若要取得每個地區的 URL，請參閱[監視服務的 URL](/docs/services/cloud-monitoring?topic=cloud-monitoring-monitoring_ov#region)。

    例如，對於「美國南部」地區，啟動：[https://metrics.ng.bluemix.net/](https://metrics.ng.bluemix.net/)。

2. 將 {{site.data.keyword.monitoringshort}} 網域設為 **account**。

    在 Grafana 中，選取 ID。然後，確認您使用正確的帳戶，並選擇 `Domain = account`。


## 步驟 2：建立 Grafana 儀表板
{: #cgd_step2}

請完成下列步驟，以建立新的儀表板：

1. 選取側邊功能表列切換 ![Grafana 側邊功能表列](images/grafana_settings.gif "Grafana 側邊功能表列")。
2. 選取**儀表板**。
3. 按一下**新建**。

即會開啟儀表板。儀表板包括已備妥可進行配置的空白列。

![Grafana 儀表板](images/grafana4_f1.gif "Grafana 儀表板")

在 Grafana 中，您可以新增幾列，將儀表板區分為數個區段。一列集合了 1 個以上的畫面。在一列中，畫面是您可配置以顯示度量值資料的最小視覺效果單位，例如，您可以選擇圖形畫面或表格畫面。您可以拖放畫面，以重新排列儀表板中的畫面。畫面顯示的資料是透過查詢而配置。您可以在一個畫面中定義一個以上的查詢。每一個查詢都代表不同的資料集。您也可以設定畫面的時間範圍。通常，時間範圍是由*儀表板* 時間選取器所設定。

## 步驟 3：將圖形新增至儀表板來監視度量值
{: #cgd_step3}

請完成下列步驟：

1. 選取**圖形**。

2. 按一下圖形標題，然後選取**編輯**。

    即會開啟*度量值*標籤。您可以在這裡看到預設資料來源。


![包括配置標籤的圖形畫面](images/grafana4_f2.gif "包括配置標籤的圖形畫面")


## 步驟 4：定義度量值查詢
{: #cgd_step4}

定義過濾圖形中所顯示資料的查詢。此查詢會監視容器的所有核心的 CPU 時間（十億分之一秒）。

如需查詢格式的相關資訊，請參閱[針對容器所收集之 CPU 度量值的查詢格式](/docs/services/cloud-monitoring/reference?topic=cloud-monitoring-metrics_format_containers#cpu_containers)。
 
在*度量值*標籤中，選取**新增查詢**。<br>即會新增查詢項目。每一個查詢都會以一個字母標示。 

![新建查詢項目](images/grafana4_query_f1.gif "新建查詢項目") 
	
請完成下列步驟，以定義查詢：
        
1. 按一下**選取度量值**來指定來源，然後選擇 `ibmcloud`。
    
2. 按一下**選取度量值**來指定雲端類型，然後選擇 `public`。
    
3. 按一下**選取度量值**來指定服務名稱，然後選擇 `containers-kubernetes`。
	
4. 按一下**選取度量值**來指定地區，然後選擇叢集執行所在的地區。例如，`us-south`。
    
5. 按一下**選取度量值**來指定叢集名稱，然後選擇容器執行所在的叢集名稱。
		
6. 按一下**選取度量值**來指定度量值來源。選取**容器**。
		
7. 按一下**選取度量值**來指定名稱空間。然後輸入叢集中與容器相關聯的名稱空間名稱。
		
8. 按一下**選取度量值**來指定 Pod 名稱。
	
9. 按一下**選取度量值**來指定您要監視之容器的容器名稱。
	
10. 按一下**選取度量值**來指定度量值類型，然後按一下**選取度量值**來指定度量值子類型。
	
    例如，若要監視容器的所有核心的 CPU 時間（十億分之一秒），請選取 **cpu** 作為類型，並選取 **usage** 作為子類型。
		
	如需 CPU 度量值的清單，請參閱[容器的 CPU 度量值](/docs/services/cloud-monitoring/containers?topic=cloud-monitoring-monitoring_bmx_containers_ov#cpu_metrics_containers)。
    
11. 按一下加號影像 ![新增圖示](images/grafana_plus_image.gif "加號影像")，然後選擇函數。您可以新增函數，以在可供度量值使用的資料上轉換、結合及執行運算。

    例如，您可以新增 **alias(newName)** 函數來新增度量值的別名。此別名用來列印字串，而不是圖形中所顯示圖註中的度量值名稱。

    若要新增度量值的別名，請完成下列步驟：

    1. 按一下加號。
    2. 選取**特殊**。
    3. 選取**別名**。
    4. 輸入字串，例如，`My sample metric`。

## 步驟 5：儲存儀表板
{: #cgd_step5}

儲存儀表板，以供之後重複使用。

1. 按一下儲存儀表板影像 ![儲存儀表板影像](images/grafana_save_image.gif "儲存儀表板影像")。

    ![儲存儀表板](images/grafana_save_dashboard.gif "儲存儀表板")

2. 輸入儀表板的名稱。
3. 按一下**儲存**。



## 後續步驟
{: #cgd_next_steps}

定義度量值的警示。如需相關資訊，請參閱[配置警示](/docs/services/cloud-monitoring?topic=cloud-monitoring-config_alerts_ov#config_alerts_ov)。
