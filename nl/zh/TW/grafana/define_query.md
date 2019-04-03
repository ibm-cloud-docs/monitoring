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


# 在 Grafana 中配置度量值查詢
{: #define_query}

在 {{site.data.keyword.Bluemix}} 中，會自動收集所選取 Cloud 服務的度量值。若要透過 {{site.data.keyword.monitoringlong}} 進行監視，您必須定義 Grafana 查詢。
{:shortdesc}

## 步驟 1：收集您要監視之 CF 應用程式或服務的資料
{: #step18}

取得您要監視之 CF 應用程式或服務的下列資訊：

* CF 應用程式執行所在的**地區**。
* CF 應用程式執行所在的**組織**。 	
* CF 應用程式執行所在的**空間**。 
* 您要監視之應用程式的 **CF 應用程式名稱**，或**服務名稱**。 


## 步驟 2：啟動 Grafana
{: #step27}

從瀏覽器啟動 Grafana。如需相關資訊，請參閱[從 Web 瀏覽器導覽至 Grafana 儀表板](/docs/services/cloud-monitoring/grafana?topic=cloud-monitoring-navigating_grafana#launch_grafana_from_browser)。

請確定，在 Grafana 中，您已登入 CF 應用程式或服務執行所在的帳戶、組織及地區。 


## 步驟 3：在 Grafana 中定義查詢
{: #step36}

請完成下列步驟，以建立 Grafana 儀表板以及定義查詢：

1. 建立新的儀表板。

    * 選取側邊功能表列切換 ![Grafana 側邊功能表列](images/grafana_settings.gif "Grafana 側邊功能表列")。
    * 選取**儀表板**。
    * 按一下**新建**。

    即會開啟儀表板。儀表板包括已備妥可進行配置的空白列。

2. 新增*圖形*畫面。

    1. 選取**圖形**。

    2. 按一下圖形標題，然後選取**編輯**。

        即會開啟*度量值*標籤。您可以在這裡看到預設資料來源。

3. 定義過濾圖形中所顯示資料的查詢。 

    在*度量值*標籤中，選取**新增查詢**。<br>即會新增查詢項目。每一個查詢都會以一個字母標示。
    
    ![新建查詢項目](images/grafana4_query_f1.gif "新建查詢項目")
        
    1. 按一下**選取度量值**，然後選擇來源：`ibmcloud`。
    
    2. 按一下**選取度量值**，然後選擇雲端類型：`public`。
    
    3. 按一下**選取度量值**，然後選擇服務名稱，例如，`cloud-foundry` 作為 CF 應用程式度量值，或 `message hub` 作為 {{site.data.keyword.messagehub}} 度量值。
    
    4. 按一下**選取度量值**，然後選擇您工作的地區，例如，`ng` 表示「美國南部」地區。
    
    5. 選取套用至您要監視之服務或 CF 應用程式的特定服務欄位。

        <table>
          <caption>每個服務或 CF 應用程式的度量值查詢格式</caption>
          <tr>
            <th>服務名稱</th>
            <th>度量值查詢格式的鏈結</th> 
          </tr>
          <tr>
            <td>{{site.data.keyword.containershort_notm}}</td>
            <td>[針對容器所收集之 CPU 度量值的查詢格式](/docs/services/cloud-monitoring/reference?topic=cloud-monitoring-metrics_format_containers#cpu_containers) </br>[針對工作者節點所收集之負載度量值的查詢格式](/docs/services/cloud-monitoring/reference?topic=cloud-monitoring-metrics_format_containers#load_workers) </br>[針對容器所收集之記憶體度量值的查詢格式](/docs/services/cloud-monitoring/reference?topic=cloud-monitoring-metrics_format_containers#mem_containers)</td> 
          </tr>
          <tr>
            <td>CF 應用程式</td>
            <td>[CF 應用程式的查詢格式](/docs/services/cloud-monitoring/reference?topic=cloud-monitoring-cfapps_metrics_format#cfapps_metrics_format)</td> 
          </tr>
        </table>

        例如，針對 CF 應用程式，選擇：
    
        按一下**選取度量值**，然後選擇 CF 應用程式名稱，例如，`logtester`。
    
        按一下**選取度量值**，然後選擇 CF 應用程式實例索引，例如，`0`。

        按一下**選取度量值**，然後選擇 `container`。
    
    9. 按一下**選取度量值**，然後選擇度量值類型。例如，**cpu** 作為 CPU 度量值、**memory** 作為記憶體度量值，而 **disk** 作為磁碟度量值。 

        **附註：**針對 CF 應用程式，跳過此步驟。 

    10. 按一下**選取度量值**，然後選擇度量值。 

        <table>
          <caption>每個服務或 CF 應用程式的度量值清單</caption>
          <tr>
            <th>服務名稱</th>
            <th>度量值鏈結</th> 
          </tr>
          <tr>
            <td>{{site.data.keyword.containershort_notm}}</td>
            <td>[CPU 度量值](/docs/services/cloud-monitoring/cf?topic=cloud-monitoring-cloud-foundry-apps#cpu_metrics) </br>[磁碟度量值](/docs/services/cloud-monitoring/cf?topic=cloud-monitoring-cloud-foundry-apps#disk_metrics)   </br>[記憶體度量值](/docs/services/cloud-monitoring/cf?topic=cloud-monitoring-cloud-foundry-apps#mem_metrics)</td> 
          </tr>
          <tr>
            <td>CF 應用程式</td>
            <td>[CPU 度量值](/docs/services/cloud-monitoring/cf?topic=cloud-monitoring-cloud-foundry-apps#cpu_metrics) </br>[磁碟度量值](/docs/services/cloud-monitoring/cf?topic=cloud-monitoring-cloud-foundry-apps#disk_metrics)   </br>[記憶體度量值](/docs/services/cloud-monitoring/cf?topic=cloud-monitoring-cloud-foundry-apps#mem_metrics)</td> 
          </tr>
          <tr>
            <td>{{site.data.keyword.messagehub}}</td>
            <td>[Kafka 主題的度量值](/docs/services/cloud-monitoring/mh?topic=cloud-monitoring-monitoring_mh_ov#kafka_topic_metrics) </br>[Kafka 分割區的度量值](/docs/services/cloud-monitoring/mh?topic=cloud-monitoring-monitoring_mh_ov#kafka_partition_metrics)</td> 
          </tr>
        </table>

    10. 按一下加號影像 ![新增圖示](images/grafana_plus_image.gif "加號影像")，然後選擇函數。您可以新增函數，以在可供度量值使用的資料上轉換、結合及執行運算。
        
        例如，您可以新增 **alias(newName)** 函數來新增度量值的別名。此別名用來列印字串，而不是圖形中所顯示圖註中的度量值名稱。
        
        若要新增度量值的別名，請完成下列步驟：
        
        1. 按一下加號。
        2. 選取**特殊**。
        3. 選取**別名**。
        4. 輸入字串，例如，`My sample metric`。


## 步驟 4：儲存儀表板，以供之後重複使用
{: #step44}

請完成下列步驟：

1. 按一下儲存儀表板影像 ![儲存儀表板影像](images/grafana_save_image.gif "儲存儀表板影像")。
2. 輸入儀表板的名稱。
3. 按一下**儲存**。
