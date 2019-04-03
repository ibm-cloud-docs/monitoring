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


# CF 应用程序
{: #cfapps_metrics_format}

在 Grafana 中定义的用于监视在 {{site.data.keyword.Bluemix}} Public 中运行的 Cloud Foundry 应用程序的查询必须符合以下格式：
{:shortdesc}

```
{Source}.{Cloud Type}.{Service Name}.{Region}.{CFapp Name}.{CFapp Index}.{CFapp container}.{Metric Type}.{Metric Subtype}.[Functions]
```
{: codeblock}

其中

<table>
  <caption>查询中的常用字段</caption>
  <tr>
    <th>字段</th>
	<th>描述</th>
	<th>值</th>
  </tr>
  <tr>
    <td>源</td>
	<td>这是保留名称。此层次结构下的度量值来自 {{site.data.keyword.Bluemix_notm}} 应用程序和服务。</td>
	<td>*ibmcloud*</td>
  </tr>
  <tr>
    <td>云类型</td>
	<td>指示云的类型。</td>
	<td>对于 {{site.data.keyword.Bluemix_notm}} 公共云，值为 *public*</td>
  </tr>
  <tr>
    <td>服务名称</td>
	<td>定义服务在 {{site.data.keyword.Bluemix_notm}} 中的名称。</td>
	<td>对于 CF 应用程序，值为：*cloud-foundry*</td>
  </tr>
  <tr>
    <td>区域</td>
	<td>定义运行 CF 应用程序实例的区域。</td>
	<td>对于美国南部区域，值为：*us-south*<br>对于英国区域，值为：*eu-gb*<br>对于德国，值为：*eu-de*<br>对于悉尼，值为：*au-syd*</td>
  </tr>
  <tr>
    <td>CF 应用程序名称</td>
	<td>CF 应用程序的名称。</td>
	<td></td>
  </tr>
  <tr>
    <td>CF 应用程序索引</td>
	  <td>CF 应用程序实例的索引。</td>
	  <td>例如：*0*</br>如果您的 CF 应用程序有一个实例，那么只有索引 0。如果对 CF 应用程序进行缩放，例如缩放到 10 个实例，那么会有索引值 0 到 9。</td>
  </tr>
  <tr>
    <td>CF 应用程序容器</td>
	  <td>固定值。</td>
	  <td>*container*</td>
  </tr>
  <tr>
    <td>度量值类型</td>
	  <td>度量值的类型。磁盘、内存和 CPU 是自动收集的度量值序列。</td>
	  <td>*CPU*</td>
  </tr>
  <tr>
    <td>度量值子类型</td>
	  <td>要显示的度量值。</br>[CPU 度量值](/docs/services/cloud-monitoring/cf?topic=cloud-monitoring-cloud-foundry-apps#cpu_metrics) </br>[磁盘度量值](/docs/services/cloud-monitoring/cf?topic=cloud-monitoring-cloud-foundry-apps#disk_metrics)</br>[内存度量值](/docs/services/cloud-monitoring/cf?topic=cloud-monitoring-cloud-foundry-apps#mem_metrics)</td>
	  <td></td>
  </tr>
  <tr>
    <td>函数</td>
    <td>可以选择用于在面板中可视化容器度量值的查询函数。</td>
    <td>[函数 ![（外部链接图标）](../../../icons/launch-glyph.svg "外部链接图标")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
   </tr>
</table>




