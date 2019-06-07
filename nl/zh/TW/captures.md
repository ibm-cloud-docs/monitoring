---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, captures

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

# 管理擷取
{: #captures}

擷取是您可以產生的追蹤檔，用來分析主機在某個時間範圍內發生什麼情況。例如，您可以將其用來分析瓶頸或元件互動。在 {{site.data.keyword.mon_full_notm}} 服務中，您可以建立、探索、下載及刪除個別節點的*擷取*。
{:shortdesc}

如需相關資訊，請參閱[擷取](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures)。


## 建立擷取
{: #captures_create}

您可以在*探索* 視圖中建立擷取。

請完成下列步驟來建立擷取檔：

1. 導覽至 Web 使用者介面中的*探索* 區段。[進一步瞭解](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch)。

2. 按一下切換主機圖示 ![切換主機圖示](images/switch_hosts.png)。

3. 選取主機或容器。

4. 按一下動作圖示 ![三點圖示](images/actions.png)，然後選取 **Sysdig 擷取**。

    即會開啟 *Sysdig 擷取* 視窗。

5. 在 *Sysdig 擷取* 視窗中，定義下列參數：

    1. 在*擷取路徑及名稱* 欄位中，輸入擷取檔的名稱。您可以保留預設值或加以修改。預設名稱包括建立擷取時的日期及時間戳記。 

    2. 設定*時間範圍* 來指定收集資料的秒數。預設擷取時間為 15 秒。擷取時間上限為 86400 秒（24 小時）。 

    3. （選用）新增過濾器來限制所收集的追蹤資訊數量。 

6. 按一下**啟動擷取**。即會發出信號，通知 Sysdig 代理程式啟動擷取，並傳回產生的追蹤檔。 

7. 按一下**移至擷取頁面**，以在 Web 使用者介面的*擷取* 區段中顯示擷取清單。 

*擷取* 頁面會顯示一個表格，其中列出擷取檔名稱、擷取來源的主機、時間範圍，以及擷取的大小。 

擷取檔的狀態可以是下列任何值：
* `已要求`：正在產生檔案。
* `已上傳`：檔案可供下載及分析。
* `錯誤`：由於逾時、從未收到資料或代理程式錯誤，檔案無法使用。



## 刪除擷取
{: #captures_delete}

請完成下列步驟來刪除擷取檔：

1. 導覽至 Web 使用者介面中的*擷取* 區段。[進一步瞭解](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch)。
2. 識別並選取您要刪除的擷取檔。
3. 按一下 **刪除**。



## 探索擷取
{: #captures_explore}

請完成下列步驟來探索擷取檔：

1. 導覽至 Web 使用者介面中的*擷取* 區段。[進一步瞭解](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch)。
2. 識別並選取包含您要分析之主機資料的擷取檔。
3. 按一下**探索**。



## 下載擷取
{: #captures_download}

請完成下列步驟來下載擷取檔：

1. 導覽至 Web 使用者介面中的*擷取* 區段。[進一步瞭解](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch)。
2. 識別並選取包含您要下載之資料的擷取檔。
3. 按一下**下載**。


## Chisel
{: #captures_chisels}

Sysdig Chisel 是以 LIA（Scripting 語言）撰寫的 Script。您可以將其用來分析擷取檔中的資料。 

如需相關資訊，請參閱 [Chisels User Guide ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/draios/sysdig/wiki/Chisels-User-Guide){:new_window}。



## Csysdig
{: #captures_csysdig}

CSysdig 是為了監視和除錯而設計的 Linux 開放程式碼工具。您可以將其用來分析擷取檔。 

如需相關資訊，請參閱下列資源：
* [Csysdig 部落格 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://sysdig.com/blog/csysdig-explained-visually/){:new_window}
* [Csysdig 視訊 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.youtube.com/watch?v=UJ4wVrbP-Q8){:new_window}


