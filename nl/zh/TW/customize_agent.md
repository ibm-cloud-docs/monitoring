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

# 自訂 Sysdig 代理程式以控制資料
{: #customize_agent}

依預設，Sysdig 代理程式會從廣泛的平台和應用程式收集資料。您可以編輯代理程式配置檔來變更其預設行為，以及包括或排除資料。您可以自訂 Sysdig 代理程式配置檔，以包括自訂度量，例如 JMX、StatsD 及 Prometheus。您也可以濾出度量、事件資料及容器。
{:shortdesc}

## 自訂 Kubernetes Sysdig 代理程式
{: #kube}

Kubernetes Sysdig 代理程式使用兩個配置檔，其中指定要自動收集哪些資料：

| 檔名                        | 動作       |
|----------------------------------|-------------------|
| `sysdig-agent-daemonset-v2.yaml` | 修改記載層次。 |
| `sysdig-agent-configmap.yaml`    | 封鎖埠。 </br>包括或排除度量值資料。</br>新增或移除事件。</br>濾出容器。|
{: caption="表 1. Kubernetes Sysdig 代理程式配置檔" caption-side="top"} 

若要編輯 Kubernetes Sysdig 代理程式，您可能需要編輯 *sysdig-agent-configmap.yaml*、*sysdig-agent-daemonset-v2.yaml* 或兩者。

有兩種您可以用來修改配置檔的方法：
* 方法 1：直接在執行代理程式的叢集上修改檔案。如需相關資訊，請參閱[使用 kibectl edit 來編輯 Kubernetes Sysdig 代理程式配置](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_edit_kube_agent_method1)。
* 方法 2：在本端修改檔案，並將變更套用至叢集。如需相關資訊，請參閱[使用 kibectl apply 來編輯 Kubernetes Sysdig 代理程式配置](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_edit_kube_agent_method2)。

您可以將標籤新增至代理程式所收集的資料。 
* 使用這些標籤可協助您管理所監視的資料。 

    * 使用這些標籤可將基礎架構資源分組為邏輯階層、濾出資料，以及將聚集資料分割為區段。 
    
    * 自訂在您配置圖形或建立度量的警示時聚集資料的方式。 
    
    * 設定儀表板的範圍、畫面或警示來濾出資料點。 
    
    * 透過團隊來管理使用者的資料存取，以限制資料存取。 
    
    * 如需如何管理資料的相關資訊，請參閱[管理資料](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-manage#manage)。

* 如需如何新增標籤的相關資訊，請參閱[將更多標籤新增至從 Kubernetes Sysdig 代理程式收集的資料](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_add_tags)。 


**您可以自訂 Sysdig 代理程式收集哪些資料。** 

排除事件、度量及容器時，請考量下列資訊：
* 您可以減少代理程式和後端負載。
* 您只會從要監視的容器中收集資料。
* 您可以透過報告重要容器，以及濾出不必要或不重要的容器來控制成本。
* 您可以配置要監視的 Kubernetes 事件。如需相關資訊，請參閱[收集一組 Kubernetes 事件](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_collect_events)。

下列清單概述您可以執行的動作，以控制由 Sysdig 代理程式收集的資料：
* [停用事件的收集](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_disable_events)
* [包括及排除度量](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_inc_exc_metrics)
* [過濾從中收集資料的 kubernetes 物件及容器](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_filter_data)
* [封鎖埠](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_block_ports)
* [依嚴重性過濾 Kubernetes 事件](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_filterby_severity)

您也可以自訂日誌的類型及所收集的項目。如需相關資訊，請參閱[變更記載層次](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_log_level)。

您也可以記載代理程式要報告其資料的度量清單。如需相關資訊，請參閱[將包括或排除哪些度量記載至檔案](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_log_metrics)。

Sysdig 代理程式會在 */opt/draios/logs/draios.log* 中產生日誌項目。 
* 日誌檔在大小達到 10MB 時即會替換。
* 保留 10 個最近的日誌檔。附加至檔名的日期戳記是用來決定要保留哪些檔案。
* 有效的記載層次為：*none*、*error*、*warning*、*info*、*debug*、*trace*
* 預設記載層次為 *info*，其中除了任何警告及錯誤的項目外，每次將聚集的度量傳輸至後端伺服器時都會建立一個項目，每秒一次。

下表列出一些常用的情境，以及您必須在其中每一個情境中設定的值：

| 使用案例                                     | 日誌區段項目           |
|-----------------------------------------------|-----------------------------|
| 疑難排解代理程式行為                   | `file_priority: debug`      |
| 減少容器主控台輸出               | `console_priority: warning` |
| 依嚴重性過濾事件                  | `event_priority: warning`   |
| 驗證包括或排除哪些度量  | `metrics_excess_log: true`  |

## 容器 Sysdig 代理程式
{: #container}


下列清單概述您可以執行的動作，以控制由 Sysdig 代理程式收集的資料：
* [停用事件的收集](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_disable_events)
* [包括及排除度量](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_inc_exc_metrics)
* [過濾從中收集資料的容器](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_collect_docker_events)
* [封鎖埠](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_block_ports)
* [依嚴重性過濾事件](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_filterby_severity)

您也可以自訂日誌的類型及所收集的項目。如需相關資訊，請參閱[變更記載層次](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_log_level)。



## Linux Sysdig 代理程式
{: #linux}

Linux Sysdig 代理程式使用兩個配置檔，其中指定要自動收集哪些資料：

| 檔案                   | 說明                                                     | 位置                                |
|------------------------|-----------------------------------------------------------------|-----------------------------------------|
| `dragent.default.yaml` | 主要配置檔 </br>**附註：****請不要編輯此檔案。| `/opt/draios/etc/dragent.default.yaml`  |
| `dragent.yaml`         | 您編輯來自訂 Sysdig 代理程式的配置檔。| `/opt/draios/etc/dragent.yaml`          |
{: caption="表 1. Sysdig 代理程式配置檔" caption-side="top"} 

您可以編輯 *dragent.yaml* 檔來自訂收集的資料。變更會在您儲存檔案之後立即生效。代理程式會偵測變更，並自動重新啟動。您可以在 *dragent.default.yaml* 檔中找到 Sysdig 代理程式檢查的頻率及檔案。如需相關資訊，請參閱[編輯 dragent yaml 檔案](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_linux_agent#change_linux_agent_edit_agent)。

例如，*dragent.default.yaml* 包括下列資訊：

```
check_frequency_s: 5
files:
- /opt/draios/etc/dragent.yaml
- /opt/draios/etc/kubernetes/config/dragent.yaml
- /opt/draios/etc/kubernetes/secrets/access-key
```
{: screen}

下列清單概述您可以執行的動作，以控制由 Sysdig 代理程式收集的資料：
* [包括及排除度量](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_linux_agent#change_linux_agent_inc_exc_metrics)
* [封鎖埠](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_linux_agent#change_linux_agent_block_ports)

您也可以自訂日誌的類型及所收集的項目。如需相關資訊，請參閱[變更記載層次](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_linux_agent#change_linux_agent_log_level)。


