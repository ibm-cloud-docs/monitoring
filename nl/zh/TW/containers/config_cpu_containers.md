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


# 在 Grafana 中配置容器的 CPU 度量值
{: #config_cpu_containers}

在 {{site.data.keyword.Bluemix}} 中，會自動收集針對容器所選取的 CPU 度量值。若要透過 {{site.data.keyword.monitoringlong}} 進行監視，您必須定義 Grafana 查詢。
{:shortdesc}

如需自動收集的 CPU 度量值清單，請參閱[容器的 CPU 度量值](/docs/services/cloud-monitoring/containers?topic=cloud-monitoring-monitoring_bmx_containers_ov#cpu_metrics_containers)。


## 步驟 1：收集您要監視之容器的資料
{: #step15}

取得您要監視之容器的下列資訊：

* 叢集執行所在的**地區**。
* 容器執行所在的**叢集名稱**。 	
* 容器部署所在的**名稱空間**。 

    使用名稱空間來將叢集資源群組在一起。
	
* 與您要監視之容器相關聯的 **Pod 名稱**。 

    Pod 定義一個以上容器的群組（含共用儲存空間及網路），以及如何執行叢集中容器的詳細資料。
	
* 您要監視之容器的**容器名稱**。

了解將度量值轉遞至空間網域還是帳戶網域。

若要識別叢集轉遞度量值的位置，請執行下列指令：

```
$ ibmcloud cs cluster-get ClusterName --json
```
{: codeblock}

其中 *ClusterName* 是叢集的名稱。

在輸出中，下列欄位會提供度量值轉遞位置的相關資訊：

* **logOrg** 定義 CF 組織的 ID。
* **logOrgName** 定義 CF 組織的名稱。
* **logSpace** 定義 CF 空間的 ID。
* **logSpaceName** 定義 CF 空間的名稱。

如果欄位是空的，則會將度量值轉遞至帳戶網域。
如果欄位已設定 CF 組織及 CF 空間，則會將度量值轉遞至與此空間相關聯的空間網域。

## 步驟 2：啟動 Grafana
{: #step24}

從瀏覽器啟動 Grafana。如需相關資訊，請參閱[從 Web 瀏覽器導覽至 Grafana 儀表板](/docs/services/cloud-monitoring/grafana?topic=cloud-monitoring-navigating_grafana#launch_grafana_from_browser)。

請確定，在 Grafana 中，您已登入叢集執行所在的帳戶。 

1. 從瀏覽器啟動 Grafana。 

    輸入您已建立叢集之地區的 {{site.data.keyword.monitoringshort}} 服務 URL。 
    
    若要取得每個地區的 URL，請參閱[監視服務的 URL](/docs/services/cloud-monitoring?topic=cloud-monitoring-monitoring_ov#region)。

    例如，對於「美國南部」地區，啟動：[https://metrics.ng.bluemix.net/](https://metrics.ng.bluemix.net/)。

2. 設定您可檢視叢集度量值的 {{site.data.keyword.monitoringshort}} 網域。

    在 Grafana 中，選取 ID。然後，確認您使用正確的帳戶，並選擇網域。

    具有相關聯 CF 空間的叢集會將度量值轉遞至空間度量值網域。選取 `Domain = space`，以及與您叢集相關聯的組織及空間。

    已在帳戶層次建立的叢集會將度量值轉遞至帳戶度量值網域。選取 `Domain = account`




## 步驟 3：在 Grafana 中定義 CPU 度量值的查詢
{: #step33}

請完成下列步驟，以建立 Grafana 儀表板，以及定義查詢來監視容器的 CPU 用量：

1. 建立新的儀表板。

    * 選取側邊功能表列切換 ![Grafana 側邊功能表列](images/grafana_settings.gif "Grafana 側邊功能表列")。
    * 選取**儀表板**。
    * 按一下**新建**。

    即會開啟儀表板。儀表板包括已備妥可進行配置的空白列。

2. 新增*圖形*畫面，以監視 Pod 的 CPU 度量值。

    1. 選取**圖形**。

    2. 按一下圖形標題，然後選取**編輯**。

        即會開啟*度量值*標籤。您可以在這裡看到預設資料來源。

3. 定義過濾圖形中所顯示資料的查詢。 

    如需查詢格式的相關資訊，請參閱[針對容器所收集之 CPU 度量值的查詢格式](/docs/services/cloud-monitoring/reference?topic=cloud-monitoring-metrics_format_containers#cpu_containers)。

    在*度量值*標籤中，選取**新增查詢**。</br>即會新增查詢項目。每一個查詢都會以一個字母標示。
	
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
	
	    如需 CPU 度量值的清單，請參閱[容器的 CPU 度量值](/docs/services/cloud-monitoring/containers?topic=cloud-monitoring-monitoring_bmx_containers_ov#cpu_metrics_containers)。
	
	11. 按一下加號影像 ![新增圖示](images/grafana_plus_image.gif "加號影像")，然後選擇函數。您可以新增函數，以在可供度量值使用的資料上轉換、結合及執行運算。

        例如，您可以新增 **alias(newName)** 函數來新增度量值的別名。此別名用來列印字串，而不是圖形中所顯示圖註中的度量值名稱。

        若要新增度量值的別名，請完成下列步驟：

        1. 按一下加號。
        2. 選取**特殊**。
        3. 選取**別名**。
        4. 輸入字串，例如，`My sample metric`。


## 步驟 4：儲存儀表板，以供之後重複使用
{: #step43}

請完成下列步驟：

1. 按一下儲存儀表板影像 ![儲存儀表板影像](images/grafana_save_image.gif "儲存儀表板影像")。
2. 輸入儀表板的名稱。
3. 按一下**儲存**。

