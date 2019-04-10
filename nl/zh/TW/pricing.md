---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, pricing

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


# 定價
{: #pricing_plans}

{{site.data.keyword.mon_full_notm}} 實例提供不同的定價方案。
{:shortdesc}
 

| 方案            | 層級         | 資料收集  |
|------------------|--------------|------------------|
| `試用`          |              | 每個節點最多可收集 20 個容器的資料，或每個節點最多可收集 200 個自訂度量的資料，限時 30 天。|
| `提升層級` | `基本`      | 每個節點最多可收集 20 個容器的資料，或每個節點最多可收集 200 個自訂度量的資料。|
| `提升層級` | `專業`        | 每個節點最多可收集 50 個容器的資料，或每個節點最多可收集 500 個自訂度量的資料。|
| `提升層級` | `進階`   | 每個節點最多可收集 110 個容器的資料，或每個節點最多可收集 1000 個自訂度量的資料。|
{: caption="表 1. 服務方案的清單" caption-side="top"} 


**附註：**節點可以是主機、容器、虛擬機器、裸機，或任何您安裝 Sysdig 代理程式的度量來源。

當每個節點的容器數目或度量數目在一段時間超出提升層級方案的臨界值限制時，會套用自動層級偵測。如果您啟用下列警示 **[{{site.data.keyword.IBM_notm}}]: Usage 層級變更**，則會在配置計費使用通知後觸發警示通知

您可以使用 [IBM Cloud 支援中心 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/unifiedsupport/supportcenter){:new_window} 來開立問題單，針對超過*進階提升層級付款方案* 上限的任何項目要求**自訂報價**。
{: tip}

根據所有方案中的標準準則，收集並保留資料。如需相關資訊，請參閱[資料收集](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-about#overview_collection)及[資料保留](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-about#overview_retention)。


## 檢查您的使用情形
{: #pricing_usage}

若要監視 {{site.data.keyword.mon_full_notm}} 服務的使用方式，以及與其使用方式相關聯的成本，請參閱[檢視您的使用情形](/docs/billing-usage?topic=billing-usage-viewingusage#viewingusage)。



## 啟用在層級變更上通知的警示
{: #pricing_alert}

若要在發生層級變更時發出通知，您必須啟用下列警示：**[{{site.data.keyword.IBM_notm}}]: Usage Tier Change**

請完成下列步驟來啟用警示：

1. 啟動 Web 使用者介面。如需如何啟動 Web 使用者介面的相關資訊，請參閱[導覽至 Web 使用者介面](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch)。 
2. 建立通知頻道。如需相關資訊，請參閱[配置通知頻道](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-notifications#notifications_create)。 
3. 按一下**警示**來導覽至*警示* 區段。
2. 搜尋 **[IBM]: Usage Tier Change**。
3. 編輯警示來新增通知頻道。
4. 按一下**儲存**。



## 如何產生服務方案警示？
{: #pricing_how}

若要在發生層級變更時發出通知，您必須啟用下列警示：**[{{site.data.keyword.IBM_notm}}]: Usage Tier Change**

**附註：**當啟用此警示時，您必須指定要在其中通知您的通知頻道。

使用情形會計算為前一個小時每 10 秒取樣的節點及度量數目的平均值。不包括小型、短暫的變動。前一個使用情形與現行使用情形之間的差異，一小時發生一次。

定義的臨界值以下列方式設定：

``` 
usageTiers {
  containerDensity {
    Basic = [0, 20]
    Pro = [21, 50]
    Advanced = [51, 100]
  }
  metricDensity {
    Basic = [0, 200]
    Pro = [201, 500]
    Advanced = [501, 1000]
}
```
{: screen}

警示通知的產生方式如下：
1. 每小時，如果層級中每個節點的容器數目增加，則會產生自訂事件。
2. 警示條件會檢查是否有任何自訂事件通知每個節點的容器數目變更。如果發現事件層級中的容器數目從前次計算使用情形時增加，則會傳送通知。

警示的頻率是每小時一次。對於變動節點，警示頻率最多是每兩個小時。

請注意，只有在節點從*基本* 層級移至*專業* 層級，或移至*進階* 層級時，才會產生警示。 



### 範例
{: #pricing_examples}

**範例 1** 

如果平均容器計數如下： 

| 小時     | 容器數 | 說明                                                                   | 是否產生警示？|
|----------|----------------------|-------------------------------------------------------------------------------|------------------------|
| 10:00    | 18                   | 層級設為**基本**。                                                     | 否                     |
| 11:00    | 21                   | 容器數高於*基本* 層級。層級移至**專業**。            | 是                    |
| 12:00    | 19                   | 容器數低於*基本* 層級。層級移回**基本**。     | 否                    |
| 13:00    | 20                   | 無層級變更。層級設為**基本**。                                     | 否                     |
{: caption="表 2. 範例 1" caption-side="top"} 


**範例 2**

如果平均容器計數如下： 

| 小時     | 容器數 | 說明                                                                   | 是否產生警示？|
|----------|----------------------|-------------------------------------------------------------------------------|------------------------|
| 10:00    | 15                   | 層級設為**基本**。                                                     | 否                     |
| 11:00    | 19                   | 層級設為**基本**。                                                     | 否                     |
| 12:00    | 20                   | 層級設為**基本**。                                                     | 否                    |
| 13:00    | 21                   | 容器數高於*基本* 層級。層級移至**專業**。            | 是                    |
{: caption="表 3. 範例 2" caption-side="top"}


**範例 3**

如果平均容器計數如下： 

| 小時     | 容器數 | 說明                                                                   | 是否產生警示？|
|----------|----------------------|-------------------------------------------------------------------------------|------------------------|
| 10:00    | 15                   | 層級設為**基本**。                                                     | 否                     |
| 11:00    | 20                   | 層級設為**基本**。                                                     | 否                    |
| 12:00    | 21                   | 層級設為**基本**。                                                     | 是                    |
| 13:00    | 20                   | 容器數回到*基本* 層級。層級移至**專業**。            | 否                     |
{: caption="表 3. 範例 3" caption-side="top"}



