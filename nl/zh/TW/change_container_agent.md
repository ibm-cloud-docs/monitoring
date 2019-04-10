---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-18"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# 自訂容器 Sysdig 代理程式
{: #change_container_agent}

在 {{site.data.keyword.mon_full_notm}} 中，您可以自訂 Sysdig 代理程式配置來設定記載層次、封鎖埠、包括或排除度量值資料、新增或移除事件，以及濾出容器。
{:shortdesc}


## 編輯 dragent yaml 檔案
{: #change_container_agent_edit_config}

yaml 檔案位於 */opt/draios/etc/*。

請完成下列步驟來編輯檔案並套用變更：

1. 直接存取位於 `/opt/draios/etc/dragent.yaml` 的 *dragent.yaml*。
2. 編輯檔案。請使用有效的 YAML 語法。
3. 重新啟動代理程式。請執行下列指令：

    ```
    docker restart sysdig-agent
    ```
    {: codeblock}



## 封鎖埠
{: #change_container_agent_block_ports}

若要封鎖來自網路埠的網路資料流量及度量，您必須自訂 *dragent.yaml* 檔案中的 **blacklited_ports** 區段。您必須列出要從中濾出任何資料的埠。

**附註：**埠 53 (DNS) 一律列入黑名單。 

例如，下列範例顯示如何設定 Sysdig 代理程式的 *blackted_ports* 區段，以排除來自埠 6666 及 6379 的資料：

```
blacklisted_ports:
    - 6666
    - 6379
```
{: screen}



## 收集一組 Docker 事件
{: #change_container_agent_collect_docker_events}

{{site.data.keyword.mon_full_notm}} 支援與 Docker 進行事件整合。Sysdig 代理程式會自動探索 Docker 來源，並從中收集事件資料。您可以編輯代理程式配置檔來變更其預設行為，以及包括或排除事件資料。 

依預設，只會收集有限的一組事件。預設值配置檔 */opt/draios/etc/dragent.default.yaml* 包括所收集的事件。如需依預設收集之事件的相關資訊，請參閱 [Docker 事件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://sysdigdocs.atlassian.net/wiki/spaces/Platform/pages/234356795/Enable+Disable+Event+Data#Enable/DisableEventData-DockerEvents){:new_window}。

若要新增或移除事件，您必須自訂 *dragent.yaml* 檔，並指定要包括哪些事件，以及要濾出哪些事件。**附註：***dragent.yaml* 中的區段項目會置換預設配置中的整個區段。
{: tip}

例如，若要濾出 Docker 映像檔事件，並只收集連接、確定及複製動作的事件，您必須設定如下的 *docker* 區段：

* 選項 1：將項目上的順序定義為項目符號清單：

    ```
    events:
      docker:
        image: none
        container:
          - attach
          - commit
          - copy
    ```
    {: codeblock}

* 選項 2：在以方括弧括住的單一行上定義項目上的順序：

    ```
    events:
      docker:
        image: none
        container: [attach, commit, copy]
    ```
    {: codeblock}


## 停用事件的收集
{: #change_container_agent_disable_events}

若要停用 Sysdig 代理程式收集事件，請修改 *dragent.default.yaml* 檔。在 *dragent.yaml* 檔中，將 **events** 區段設為 *none*。

例如，若要濾出 Docker 事件，您必須在 *dragent.yaml* 檔中設定如下的 *events* 區段：

```
events:
  docker: none
```
{: codeblock}



## 依嚴重性過濾事件
{: #change_container_agent_filterby_severity}

若要依嚴重性過濾事件，您也可以在 *dragent.yaml* 檔中變更事件的日誌項目類型。 

預設記載層次為 **information**。這表示只會傳輸警告及更高的嚴重性事件。

有效層次為：*emergency*、*alert*、*critical*、*error*、*warning*、*notice*、*information*、*debug* 及 *none*。**附註**：從高優先順序至低優先順序列出這些值。

例如，若要濾出低嚴重性事件（*notice*、*information*、*debug*），您必須將日誌區段 **event_priority** 設為 *warning*：

```
log:
  event_priority: warning
```
{: codeblock}


若要封鎖事件的收集，您必須將日誌區段 **event_priority** 設為 *none*：

```
log:
  event_priority: none
```
{: codeblock}




## 包括及排除度量
{: #change_container_agent_inc_exc_metrics}

若要過濾自訂度量，您必須自訂 **dragent.yaml** 檔中的 *metrics_filter* 區段。您可以配置 **include** 及 **exclude** 過濾參數，來指定要包括哪些度量，以及要濾出哪些度量。

**附註：**過濾規則順序設定如下：套用符合度量的第一個規則。

比方說，如果 Sysdig 代理程式的 *metrics_filter* 區段如下所示：

```
metrics_filter:
  - include: metricA.*
  - exclude: metricA.*
  - include: metricB.*
  - include: haproxy.backend.*
  - exclude: haproxy.*
  - exclude: metricC.*
```
{: screen}

* 您正在配置 Sysdig 代理程式，從開頭為 *metricA*、*metricB* 及 *haproxy.backend* 的度量中收集所有資料。 
* 您正在濾出開頭為 *metricC* 的度量，以及其他開頭為 *haproxy* 的度量。 
* 忽略 `exclude: metricA.*` 項目。


## 變更記載層次
{: #change_container_agent_log_level}

若要配置記載層次，您必須自訂 **dragent.yaml** 檔中的 *log* 區段。 

Sysdig 代理程式會在 */opt/draios/logs/draios.log* 中產生日誌項目。 
* 日誌檔在大小達到 10MB 時即會替換。
* 保留 10 個最近的日誌檔。附加至檔名的日期戳記是用來決定要保留哪些檔案。
* 有效的記載層次為：*none*、*error*、*warning*、*info*、*debug*、*trace*
* 預設記載層次為 *info*，其中除了任何警告及錯誤的項目外，每次將聚集的度量傳輸至後端伺服器時都會建立一個項目，每秒一次。
* 您可以自訂日誌類型，以及藉由配置 Sysdig 代理程式配置檔 **/opt/draios/etc/dragent.yaml** 所收集的項目。在編輯檔案之後，必須使用 `docker restart Sysdig-agent` 在 Shell 上重新啟動代理程式，才能啟動變更。

| 使用案例                                     | 日誌區段項目           |
|-----------------------------------------------|-----------------------------|
| 疑難排解代理程式行為                   | `file_priority: debug`      |
| 減少容器主控台輸出               | `console_priority: warning` |
| 依嚴重性過濾事件                  | `event_priority: warning`   |
| 驗證包括或排除哪些度量  | `metrics_excess_log: true`  |
{: caption="表 2. 日誌區段項目" caption-side="top"} 


