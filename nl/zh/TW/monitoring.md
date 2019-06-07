---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring

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

# 監視您的環境
{: #monitoring}

您可以使用 {{site.data.keyword.mon_full_notm}} 服務來監視基礎架構以及在其上執行的應用程式。您可以要求擷取來分析節點在某個時間範圍發生什麼情況。
{:shortdesc}

首先，在 {{site.data.keyword.cloud_notm}} 中佈建 {{site.data.keyword.mon_full_notm}} 服務的實例。然後，為度量值來源配置 Sysdig 代理程式。配置來源之後，您可以透過服務的 Web 使用者介面檢視、監視和管理資料。

會自動收集預設度量值的資料。您可以配置自訂度量值，並將標籤新增至那些度量值，以說明其特徵。也會自動收集這些自訂度量值的資料。

您可以在*探索* 標籤，以及在 Web 使用者介面的*儀表板* 標籤中分析資料。您可以透過度量值視圖和儀表板來監視資料。 

* 使用度量值視圖來監視個別度量值。
* 使用儀表板，透過畫面監視資料，以取得對網路資料、應用程式資料、拓蹼、服務、主機及容器的專業見解。畫面會在儀表板中顯示度量值或度量值群組。

對於每一個度量值視圖及儀表板，您可以定義資料的範圍、如何聚集資料，以及要套用至資料的時間和群組過濾器。如需相關資訊，請參閱[管理資料](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-manage#manage)。

在*探索* 標籤中，您可以使用預設度量值和預設儀表板來監視資料。您可以使用標籤來定義新的基礎架構群組，然後使用這些群組，以不同方式聚集資料，並監視您的環境。您也可以使用透過*儀表板* 標籤定義的自訂儀表板。

在*儀表板* 標籤中，您可以使用任何預設儀表板或建立新的儀表板來監視資料。

可以將預設儀表板配置為團隊的預設登錄點，以統一團隊的體驗，並容許使用者立即關注與其最相關的資訊。
{: tip}

您可以使用警示，透過一個以上的通知頻道來通知使用者需要注意的問題。
* Web 使用者介面中的*警示* 區段會顯示預先定義的警示清單。從這個視圖中，您可以啟用和停用預先定義的警示，可以修改現有的警示，也可以建立新的警示。
* Web 使用者介面中的*設定* 區段是您可以配置通知頻道的位置。
 
您可以要求節點上的擷取來分析該節點在某個時間範圍發生什麼情況。例如，您可以將其用來分析瓶頸或元件互動。

## 度量值
{: #monitoring_metrics}

度量值是一種定量度量，具有一個以上標籤用於定義其性質。使用度量值，以統計方式分析具有數值的資料。 

度量值是以時間序列表示。時間系列是一段時間內的一組數值資料點。 

度量值會分類為兩個群組： 

* [預設度量值](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-metrics#metrics_default) 
* [自訂度量值](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-metrics#metrics_custom)

標籤可分類為基礎架構標籤和度量值描述子標籤。每一個度量值都有一組預先定義的標籤。對於自訂度量值，您可以配置其他標籤。 

您可以使用標籤來識別及區分度量值的特徵，例如，
* 您可以將基礎架構物件分組為邏輯階層。 
* 您可以過濾掉資料。 
* 您可以將聚集資料分割為區段。 

如需相關資訊，請參閱[標籤](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-metrics#metrics_labels)。

## 畫面
{: #monitoring_panels}

畫面會在儀表板中顯示度量值或度量值群組。 

您可以使用下列任何畫面類型將度量值視覺化：

| 類型 | 說明 |
|------|-------------|
| `折線圖` | 使用此畫面，可以檢視一個以上度量值的時間趨勢。|
| `區域圖` | 使用此畫面，可以檢視一個以上度量值的時間趨勢。|
| `前幾名清單` | 使用此畫面，可以跨實體群組比較度量值。長條圖依降冪排序。|
| `直方圖` | 使用此畫面，可以檢視儲存區中的度量值頻率分佈。|
| `拓蹼` | 使用此畫面，可將基礎架構視覺化為拓蹼對映，以及對映中實體之間的關係。|
| `數字` | 使用此畫面，可以檢視單一數字，其代表一個以上的實體在一段時間後的聚集度量值。|
| `表格` | 使用此畫面，可以根據度量值和區段，顯示基礎架構的數值資料。|
| `文字` | 使用此儀表板，可以新增文字。請使用 Markdown 來新增您的文字。|
{: caption="表 1. 畫面類型" caption-side="top"} 

您可以複製、變更範圍、複製、刪除、匯出及探索畫面。

您可以從畫面匯出資料。匯出資料時，請考量下列資訊：

* 您可以從折線圖中將資料匯出至 **json 檔案**。
* 您可以從表格圖表或折線圖中將資料匯出至 **csv 檔案**。


下表列出您可以使用畫面執行的作業：

| 作業 | 說明 |
|------|-------------|
| [複製畫面](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_copy) | 將畫面複製到新的儀表板。|
| [變更範圍](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_scope) | 變更畫面的範圍。|
| [複製畫面](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_duplicate) | 複製相同儀表板中的畫面。|
| [刪除畫面](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_delete) | 從儀表板刪除畫面。|
| [匯出資料](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_export) | 將畫面中的資料匯出至 csv 檔案或 json 檔案。|
| [建立警示](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_alert) | 定義度量值上的警示。|
{: caption="表 2. 畫面作業" caption-side="top"} 


## 儀表板
{: #monitoring_dashboards}

**儀表板**會顯示度量值的群組，而這些度量值可為單一主機或主機群組報告基礎架構、應用程式及服務的性能、效能及狀態。儀表板提供對網路資料、應用程式資料、拓蹼、服務、主機及容器的專業見解。使用儀表板來監視您的基礎架構、應用程式及服務。


在 Web 使用者介面的**儀表板**區段中，會將儀表板組織成三個主要群組：

* **我的儀表板**：這些儀表板由目前登入的使用者所建立。
* **我共用的儀表板**：這些是現行登入的使用者建立並與其他使用者共用的儀表板。
* **與我共用的儀表板**：這些是由其他使用者建立並與現行使用者共用的儀表板。

在 Web 使用者介面的**探索**區段中，會將儀表板組織成兩個群組：
* **預設儀表板**：這些是預定義儀表板。
* **我的儀表板**：這些儀表板由目前登入的使用者所建立。

您可以使用預先定義的儀表板。也可以透過 Web 使用者介面或以程式設計方式，建立自訂儀表板。可以使用 Python Script 或 Sysdig REST API 來備份和還原儀表板。


您也可以透過Web 使用者介面來複製及共用儀表板。 

下表概述您可以從使用者介面執行哪些作業來使用儀表板：

| 作業 | 說明 |
|------|-------------|
| [建立儀表板](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_create) | 在 Web 使用者介面中建立自訂儀表板。|
| [複製儀表板](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_copy) | 在儀表板可用的現行團隊中，建立儀表板的副本，或將儀表板複製到另一個團隊。|
| [變更範圍](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_scope) | 變更儀表板的範圍。|
| [刪除儀表板](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_delete) |  刪除儀表板。|
| [共用儀表板](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_share) | 透過配置儀表板的公用 URL，在團隊中的使用者與外部使用者之間共用儀表板。|
{: caption="表 1. 可在 Web 使用者介面中執行的儀表板作業" caption-side="top"} 

下表概述您可以程式設計方式執行哪些作業來使用儀表板：

| 作業                    |	使用 REST API                |
|-------------------------|-------------------------------|
| 建立儀表板      | [使用 API 來建立儀表板](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_create_dashboard) |
| 刪除儀表板      | [使用 API 來刪除儀表板](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_delete_dashboard) |
| 儲存儀表板       | [使用 API 來儲存團隊的儀表板](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_save_dashboard) |
{: caption="表 4. 以程式設計方式管理儀表板的作業" caption-side="top"} 



## 事件
{: #monitoring_events}

事件是一種通知，用於通知在將資料轉遞至 {{site.data.keyword.mon_full_notm}} 實例的任何節點中發生的活動。請使用事件來檢閱、追蹤及解決問題。 

下列清單概述了不同類型的事件： 

* *警示事件* 是由使用者配置之警示所觸發的事件。如需相關資訊，請參閱[使用警示](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-monitoring#monitoring_alerts)。
* *基礎架構型事件* 是從 Docker 和 Kubernetes 節點中收集的事件。依預設，Sysdig 會自動從選取事件群組探索及收集資料。您可以編輯代理程式配置檔來啟用其他事件。
* *自訂事件*，您可以透過下列任何整合進行配置：Slackbot、預先建置的 Python Script、自訂使用者建立的 Python Script，或 cURL 要求。

依預設，事件具有下列狀態： 
* **作用中**：此狀態指出觸發事件的情況持續存在，例如，節點繼續關閉。
* **正常**：此狀態指出狀況回到正常，例如，節點啟動並執行中。

您可以在 Web 使用者介面的*事件* 區段中管理事件。 
* 您可以透過*警示事件* 標籤來檢視警示事件。
* 您可以透過*自訂事件* 標籤來檢視基礎架構型事件。
* 您可以透過*自訂事件* 標籤來檢視自訂事件。
* 您可以使用[該團隊的 API 記號](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token)，將自訂事件傳送至任何團隊。如需相關資訊，請參閱[自訂事件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/222822463/Custom+Events){:new_window}。
* 您可以將事件設定為**已解決**，以通知其他使用者問題已解決，而不需要等待狀態設定為**正常**。
{: #tip}



## 警示
{: #monitoring_alerts}

警示是一個通知事件，您可以用來警告需要注意的狀況。每一個警示都具有一個嚴重性狀態。此狀態會通知您其所報告資訊的重要性。 

定義警示時，您必須定義觸發通知的狀況、要藉以獲得通知的一個以上通知頻道。您還必須定義警示的嚴重性以及警示的類型。 

您可以定義下列任何警示類型的警示：

| 類型              | 說明 |
|-------------------|-------------|
| 異常偵測 | 用來根據其歷程行為監視主機，並在其偏差時發出警示。|
| 關閉時間          | 用來監視任何類型的實體（例如，主機、容器、處理程序或服務），並在實體關閉時發出警示。|
| 事件             | 用來監視特定事件的出現次數，並在出現的總次數違反臨界值時發出警示。例如，在重新啟動及部署容器、編排及服務事件時，您可以使用它來發出警示。|
| 群組離群值     | 用來監視主機群組，並在某個主機有不同於其餘主機的行為時發出通知。|
| 度量值            | 用來監視時間序列度量值，並在它們違反使用者定義的臨界值時發出警示。|
{: caption="表 5. 警示類型" caption-side="top"} 

依預設，嚴重性會設為*警告*。您可以將警示的嚴重性設為下列任一值：*緊急*、*警示*、*重要*、*錯誤*、*警告*、*注意*、*參考資訊*、*除錯* 

您可以為下列任何一個通知整合定義一個以上的通知頻道：
* 電子郵件通知
* PagerDuty 通知
* Slack 通知
* VictorOps 通知
* OpsGenie 通知
* 配置 Webhook 頻道

如需相關資訊，請參閱[配置通知頻道](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-notifications#notifications_create)。


您可以在 Web 使用者介面中，以及藉由使用 Sysdig API，來啟用預先定義的警示、修改警示，以及建立自訂警示。

您可以在 Web 使用者介面的*警示* 視圖中管理警示。您可以配置在*警示* 視圖中顯示的表格直欄。有效直欄選項為：*名稱*、*範圍*、*警示條件*、*分段依據*、*通知*、*已啟用*、*已修改*、*擷取*、*頻道*、*已建立*、*說明*、*電子郵件收件者*、*至少針對*、*OpsGenie*、*PagerDuty*、*嚴重性*、*Slack*、*Webhook*、*SNS 主題*、*類型*和 *VictorOps*。

下列清單概述您處理警示時的主要作業：
* [配置警示 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-ConfigureanAlert){:new_window}
* [啟用或停用警示 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-Enable/DisableAlerts){:new_window} 
* [搜尋警示 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-SearchforanAlert){:new_window}
* [修改警示 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-EditanExistingAlert){:new_window}
* [將警示複製到相同團隊 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-CopyanAlerttothesameteam){:new_window}
* [將警示複製到不同團隊 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-CopyanAlerttoaDifferentTeam){:new_window}
* [匯出警示 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-ExportAlertJSON){:new_window}
* [刪除警示 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-DeleteAlerts){:new_window}
* [將警示臨界值定義為自訂布林表示式 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-AdvancedAlertThresholds){:new_window}


## 擷取
{: #monitoring_captures}

擷取是您可以產生的追蹤檔，用來分析節點在某個時間範圍內發生什麼情況。擷取檔案大小限制為 100 MB。例如，您可以將其用來分析瓶頸或元件互動。 

擷取包含系統呼叫及其他作業系統事件，例如系統層次延遲、批次工作持續時間、部署岔斷時間、自動調整延遲、容器啟動時間，或應用程式交易時間。擷取包括節點上每個容器的詳細資訊。 

根據您組織的準則，請考慮停用擷取。依預設，在節點中配置 Sysdig 代理程式時，會啟用擷取。
{: tip}

您可以建立、探索、下載及刪除個別節點的*擷取*。節點可以是主機、容器、虛擬機器、裸機，或任何您安裝 Sysdig 代理程式的度量值來源。 

* 在 Web 使用者介面中，您可以在*探索* 區段中建立擷取，並透過*擷取* 區段來管理擷取。
* 可以使用 *Csysdig*（Sysdig 的基於 curses 的命令行使用者介面）或開放程式碼 Sysdig 公用程式來分析擷取中的資料，從而對擷取中的資料進行視覺化。
* 您可以使用過濾器來搜尋擷取中的資料。
* 您可以使用 chisels (Script) 來操作擷取中的資料。 

為團隊啟用擷取特性時，擷取檔案僅可供該團隊的成員查看。

下列清單概述您使用擷取時的主要作業：
* [建立擷取](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures_create)
* [刪除擷取](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures_delete)
* [探索擷取](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures_explore)
* [下載擷取](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures_download)

如需相關資訊，請參閱[使用擷取](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures)。


