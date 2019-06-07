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

# 有关 {{site.data.keyword.mon_full_notm}} 的故障诊断
{: #troubleshoot}

了解您在使用 {{site.data.keyword.mon_full_notm}} 服务时可能遇到的一些一般问题的更多信息。在许多情况下，只需执行几个简单的步骤即可解决这些问题。
{:shortdesc}

## 创建捕获时是否收到错误？
{: #troubleshoot-entry-1}

您为基础架构中的主机创建[捕获文件](/docs/services/Monitoring-with-Sysdig/captures.html#captures)失败。 

在 Web UI 的*捕获*部分中，尝试为主机创建捕获文件时，收到了错误。
{: tsSymptoms}

在主机上运行的 Sysdig 代理程序的 **sysdig_capture_enabled** 功能设置为 *false*。
{: tsCauses}

在主机上运行的 Sysdig 代理程序中启用 **sysdig_capture_enabled** 功能。
{: tsResolve}


## 捕获文件的状态是否设置为*已请求*，并且不会更改为*已上传*状态？
{: #troubleshoot-entry-2}

[捕获文件](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures)的状态设置为*已请求*，并且不会更改为*已上传*状态。您一直等待捕获文件可用于分析。

在 Web UI 的*捕获*部分中，主机的捕获文件的状态不会更改为*已上传*。
{: tsSymptoms}

主机禁用了 TCP 端口 6443。
{: tsCauses}


检查是否打开了端口 6443。有关更多信息，请参阅[管理网络流量](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-network#network_send)。
{: tsResolve}


