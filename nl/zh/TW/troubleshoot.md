---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, troubleshooting

subcollection: Sysdig

---

{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# {{site.data.keyword.mon_full_notm}} 的疑難排解
{: #troubleshoot}

進一步瞭解您在使用 {{site.data.keyword.mon_full_notm}} 服務時可能遇到的一些一般問題。在許多情況下，您可以遵照一些簡單的步驟，從這些問題回復。
{:shortdesc}

## 建立擷取時是否收到錯誤？
{: #troubleshoot-entry-1}

您無法為基礎架構中的主機建立[擷取檔](/docs/services/Monitoring-with-Sysdig/captures.html#captures)。 

在 Web 使用者介面的*擷取* 區段中，當您嘗試建立主機的擷取檔時，會發生錯誤。
{: tsSymptoms}

主機上執行的 Sysdig 代理程式已將 **sysdig_capture_enabled** 特性設為 *false*。
{: tsCauses}

在執行於主機的 Sysdig 代理程式中，啟用 **sysdig_capture_enabled** 特性。
{: tsResolve}


## 擷取檔的狀態會設為*已要求*，且狀態不會變更為*已上傳* 嗎？
{: #troubleshoot-entry-2}

[擷取檔](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures)的狀態會設為*已要求*，且狀態不會變更為*已上傳*。您正在等待可用於分析的擷取檔。

在 Web 使用者介面的*擷取* 區段中，主機的擷取檔狀態不會變更為*已上傳*。
{: tsSymptoms}

主機已停用 TCP 埠 6443。
{: tsCauses}


檢查埠 643 是否已開啟。如需相關資訊，請參閱[管理網路資料流量](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-network#network_send)
{: tsResolve}


