---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, customize, linux agent

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

# 自訂 Linux Sysdig 代理程式
{: #change_linux_agent}

依預設，Sysdig 代理程式會從廣泛的平台和應用程式收集資料。您可以編輯代理程式配置檔來變更其預設行為，以及包括或排除資料。您可以自訂 Sysdig 代理程式配置檔，以包括自訂度量值，例如 JMX、StatsD 及 Prometheus。您也可以過濾掉度量值及容器。
{:shortdesc}

Sysdig 代理程式使用兩個配置檔，其中指定要自動收集哪些資料：

| 檔案                   | 說明                                                     | 位置                                |
|------------------------|-----------------------------------------------------------------|-----------------------------------------|
| `dragent.default.yaml` | 主配置檔 </br>**附註：****請勿編輯此檔案。| `/opt/draios/etc/dragent.default.yaml`  |
| `dragent.yaml`         | 您編輯來自訂 Sysdig 代理程式的配置檔。| `/opt/draios/etc/dragent.yaml`          |
{: caption="表 1. Sysdig 代理程式配置檔" caption-side="top"} 

您可以編輯 *dragent.yaml* 檔來自訂收集的資料。變更會在您儲存檔案之後立即生效。代理程式會偵測變更，並自動重新啟動。您可以在 *dragent.default.yaml* 檔中找到 Sysdig 代理程式檢查的頻率及檔案。

例如，*dragent.default.yaml* 包括下列資訊：

```
check_frequency_s: 5
files:
- /opt/draios/etc/dragent.yaml
- /opt/draios/etc/kubernetes/config/dragent.yaml
- /opt/draios/etc/kubernetes/secrets/access-key
```
{: screen}



## 編輯 dragent yaml 檔案
{: #change_linux_agent_edit_agent}

yaml 檔案位於 */opt/draios/etc/*。

請完成下列步驟來編輯檔案並套用變更：

1. 直接存取 *dragent.yaml*。此檔案位於 `/opt/draios/etc/dragent.yaml`。
2. 編輯檔案。請使用有效的 YAML 語法。
3. 重新啟動代理程式。請執行下列指令：

    ```
    service dragent restart
    ```
    {: codeblock}


## 封鎖埠
{: #change_linux_agent_block_ports}

若要封鎖來自網路埠的網路資料流量及度量值，您必須自訂 *dragent.yaml* 檔案中的 **blacklited_ports** 區段。您必須列出要從中過濾掉任何資料的埠。

**附註：**埠 53 (DNS) 一律列入黑名單。 

例如，下列範例顯示如何設定 Sysdig 代理程式的 *blackted_ports* 區段，以排除來自埠 6666 及 6379 的資料：

```
blacklisted_ports:
    - 6666
    - 6379
```
{: screen}

## 包括及排除度量值
{: #change_linux_agent_inc_exc_metrics}

若要過濾自訂度量值，您必須自訂 **dragent.yaml** 檔中的 *metrics_filter* 區段。您可以配置 **include** 及 **exclude** 過濾參數，來指定要包括哪些度量值，以及要過濾掉哪些度量值。

**附註：**過濾規則順序設定如下：套用符合度量值的第一個規則。

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

* 您正在配置 Sysdig 代理程式，從開頭為 *metricA*、*metricB* 及 *haproxy.backend* 的度量值中收集所有資料。 
* 您正在過濾掉開頭為 *metricC* 的度量值，以及其他開頭為 *haproxy* 的度量值。 
* 忽略 `exclude: metricA.*` 項目。


## 變更記載層次
{: #change_linux_agent_log_level}

若要配置記載層次，您必須自訂 **dragent.yaml** 檔中的 *log* 區段。 

Sysdig 代理程式會在 */opt/draios/logs/draios.log* 中產生日誌項目。 
* 日誌檔在大小達到 10MB 時即會替換。
* 保留 10 個最近的日誌檔。附加至檔名的日期戳記是用來決定要保留哪些檔案。
* 有效的記載層次為：*none*、*error*、*warning*、*info*、*debug*、*trace*
* 預設記載層次為 *info*，其中除了任何警告及錯誤的項目外，每次將聚集的度量值傳輸至後端伺服器時都會建立一個項目，每秒一次。
* 您可以自訂日誌類型，以及藉由配置 Sysdig 代理程式配置檔 **/opt/draios/etc/dragent.yaml** 所收集的項目。在編輯檔案之後，必須使用 `service dragent restart` 在 Shell 上重新啟動代理程式，才能啟動變更。

| 使用案例                                     | 日誌區段項目           |
|-----------------------------------------------|-----------------------------|
| 疑難排解代理程式行為                   | `file_priority: debug`      |
| 減少容器主控台輸出               | `console_priority: warning` |
| 依嚴重性過濾事件                  | `event_priority: warning`   |
| 驗證包括或排除哪些度量值  | `metrics_excess_log: true`  |
{: caption="表 2. 日誌區段項目" caption-side="top"} 
