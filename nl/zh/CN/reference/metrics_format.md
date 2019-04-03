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


# 通用格式
{: #metrics_format}

在 Grafana 中定义的用于监视 {{site.data.keyword.Bluemix}} 服务的查询必须符合以下格式：
{:shortdesc}

```
{Source}.{Cloud Type}.{Service Name}.{Region}.[service fields].{Metric type}.{Metric Subtype}.[Functions]
```
{: codeblock}

其中，[service fields] 表示服务或 CF 应用程序的度量值查询的具体字段。 

<table>
  <caption>查询中的常用字段</caption>
  <tr>
    <th>字段</th>
	<th>描述</th>
	<th>值</th>
  </tr>
  <tr>
    <td>源</td>
	<td>这是保留名称。此层次结构下的度量值来自 {{site.data.keyword.Bluemix_notm}} 服务。</td>
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
	  <td>对于 {{site.data.keyword.containershort}}，值为：*containers-kubernetes*</td>
  </tr>
  <tr>
    <td>区域</td>
	  <td>定义运行容器的区域。</td>
	  <td>对于美国南部区域，值为：*us-south*<br>对于英国区域，值为：*united-kingdom*<br>对于德国，值为：*frankfurt*<br>对于悉尼，值为：*sydney*</td>
  </tr>
  <tr>
    <td>度量值类型</td>
	<td>度量值的类型。</td>
	<td>*cpu*<br>*load*<br>*memory*</td>
  </tr>
  <tr>
    <td>度量值子类型</td>
	<td>度量值的子类型。</td>
	<td>例如：*usage*、*num-cores*、*usage-pct* 和 *usage-pct-container-requested*</td>
  </tr>
  <tr>
    <td>函数</td>
    <td>可以选择用于在面板中可视化容器度量值的查询函数。</td>
    <td>[函数 ![（外部链接图标）](../../../icons/launch-glyph.svg "外部链接图标")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
   </tr>
</table>




