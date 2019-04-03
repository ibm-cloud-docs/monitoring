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


# {{site.data.keyword.containershort_notm}}
{: #metrics_format_containers}

在 Grafana 中定义的用于监视 {{site.data.keyword.containershort_notm}} 服务的查询符合以下模式：
{:shortdesc}



## 为容器收集的 CPU 度量值的查询格式
{: #cpu_containers}

在 Grafana 中定义的用于监视在 {{site.data.keyword.containershort_notm}} 服务中运行的容器的 CPU 度量值的查询格式如下所述： 

```
{Source}.{Cloud Type}.{Service Name}.{Region}.{Cluster Name}.{Namespace}.{Metric Source}.{Pod Name}.{Container Name}.{Metric Type}.{Metric Subtype}.[Functions]
```
{: codeblock}  

其中

<table>
  <caption>定义容器的 CPU 度量值所需的字段</caption>
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
	  <td>定义运行容器的区域。</td>
	  <td>对于美国南部区域，值为：*us-south*<br>对于英国区域，值为：*united-kingdom*<br>对于德国，值为：*frankfurt*<br>对于悉尼，值为：*sydney*</td>
  </tr>
  <tr>
    <td>集群名称</td>
	  <td>要监视的集群的名称。</td>
	  <td></td>
  </tr>
  <tr>
    <td>度量源</td>
	  <td>数据的源。</td>
	  <td>*container* </td>
  </tr>
  <tr>
    <td>名称空间</td>
	<td>Kubernetes 集群中部署了容器的名称空间。</td>
	<td></td>
  </tr>
   <tr>
    <td>Pod 名称</td>
	<td>pod 的名称。</td>
	<td></td>
  </tr>
  <tr>
    <td>容器名称</td>
	<td>容器的名称。</td>
	<td></td>
  </tr>
  <tr>
    <td>度量值类型</td>
	  <td>度量值的类型。</td>
	  <td>*CPU*</td>
  </tr>
  <tr>
    <td>度量值子类型</td>
	  <td>要显示的度量值。</td>
	  <td>*usage*、*num-cores*、*usage-pct* 和 *usage-pct-container-requested*</td>
  </tr>
  <tr>
    <td>函数</td>
    <td>可以选择用于在面板中可视化容器度量值的查询函数。</td>
    <td>[函数 ![（外部链接图标）](../../../icons/launch-glyph.svg "外部链接图标")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
   </tr>
</table>

例如，用于监视在美国南部区域的 Kubernetes 集群中运行的容器的 CPU 使用率的查询定义如下：

```
ibmcloud.public.containers-kubernetes.us-south.myCluster.container.default.myPod.myContainer-1775968925-kfwfk.cpu.usage
```
{: screen}



## 为工作程序收集的负载度量值的查询格式
{: #load_workers}

在 Grafana 中定义的用于监视在 {{site.data.keyword.containershort_notm}} 服务中运行的工作程序的负载度量值的查询格式如下所述： 

```
{Source}.{Cloud Type}.{Service Name}.{Region}.{Cluster Name}.{Metric Source}.{Worker Name}.{Metric Type}.{Metric Subtype}.[Functions]
```
{: codeblock}  

其中

<table>
  <caption>定义工作程序的负载度量值所需的字段</caption>
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
	  <td>定义运行容器的区域。</td>
	  <td>对于美国南部区域，值为：*us-south*<br>对于英国区域，值为：*united-kingdom*<br>对于德国，值为：*frankfurt*<br>对于悉尼，值为：*sydney*</td>
  </tr>
  <tr>
    <td>集群名称</td>
	<td>要监视的集群的名称。</td>
	<td></td>
  </tr>
  <tr>
    <td>度量源</td>
	<td>数据的源。</td>
	<td>*worker* </td>
  </tr>
   <tr>
    <td>工作程序名称</td>
	<td>工作程序的名称。</td>
	<td></td>
  </tr>
  <tr>
    <td>度量值类型</td>
	<td>度量值的类型。</td>
	<td>*load*</td>
  </tr>
  <tr>
    <td>度量值子类型</td>
	  <td>要显示的度量值。</td>
	  <td>*avg-1*、*avg-5* 和 *avg-15*</td>
  </tr>
  <tr>
    <td>函数</td>
    <td>可以选择用于在面板中可视化容器度量值的查询函数。</td>
    <td>[函数 ![（外部链接图标）](../../../icons/launch-glyph.svg "外部链接图标")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
   </tr>
</table>

例如，用于监视在美国南部区域的 Kubernetes 集群中运行的工作程序的 CPU 使用率的查询定义如下：

```
ibmcloud.public.containers-kubernetes.us-south.myCluster.worker.MyWorker.load.avg-1
```
{: screen}


## 为容器收集的内存度量值的查询格式
{: #mem_containers}

在 Grafana 中定义的用于监视在 {{site.data.keyword.containershort_notm}} 服务中运行的容器的内存度量值的查询格式如下所述： 

```
{Source}.{Cloud Type}.{Service Name}.{Region}.{Cluster Name}.{Namespace}.{Metric Source}.{Pod Name}.{Container Name}.{Metric Type}.{Metric Subtype}.[Functions]
```
{: codeblock}  

其中

<table>
  <caption>定义容器的内存度量值所需的字段</caption>
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
	  <td>定义运行容器的区域。</td>
	  <td>对于美国南部区域，值为：*us-south*<br>对于英国区域，值为：*united-kingdom*<br>对于德国，值为：*frankfurt*<br>对于悉尼，值为：*sydney*</td>
  </tr>
  <tr>
    <td>集群名称</td>
	<td>要监视的集群的名称。</td>
	<td></td>
  </tr>
  <tr>
    <td>度量源</td>
	<td>数据的源。</td>
	<td>*container* </td>
  </tr>
  <tr>
    <td>名称空间</td>
	<td>Kubernetes 集群中部署了容器的名称空间。</td>
	<td></td>
  </tr>
   <tr>
    <td>Pod 名称</td>
	<td>pod 的名称。</td>
	<td></td>
  </tr>
  <tr>
    <td>容器名称</td>
	  <td>容器的名称。</td>
	  <td></td>
  </tr>
  <tr>
    <td>度量值类型</td>
  	<td>度量值的类型。</td>
  	<td>*memory*</td>
  </tr>
  <tr>
    <td>度量值子类型</td>
	  <td>要显示的度量值。</td>
	  <td>*limit*、*current* 和 *usage-pct*</td>
  </tr>
  <tr>
    <td>函数</td>
    <td>可以选择用于在面板中可视化容器度量值的查询函数。</td>
    <td>[函数 ![（外部链接图标）](../../../icons/launch-glyph.svg "外部链接图标")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
   </tr>
</table>

例如，用于监视在美国南部区域的 Kubernetes 集群中运行的容器的内存使用情况的查询定义如下：

```
ibmcloud.public.containers-kubernetes.us-south.myCluster.container.default.myPod.myContainer-1775968925-kfwfk.memory.usage
```
{: screen}
