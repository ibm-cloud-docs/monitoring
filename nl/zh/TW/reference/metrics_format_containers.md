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

Grafana 中所定義以監視 {{site.data.keyword.containershort_notm}} 服務的查詢，遵循下列型樣：
{:shortdesc}



## 針對容器所收集之 CPU 度量值的查詢格式
{: #cpu_containers}

您在 Grafana 中定義以監視 {{site.data.keyword.containershort_notm}} 服務中所執行容器之 CPU 度量值的查詢格式說明如下： 

```
{Source}.{Cloud Type}.{Service Name}.{Region}.{Cluster Name}.{Namespace}.{Metric Source}.{Pod Name}.{Container Name}.{Metric Type}.{Metric Subtype}.[Functions]
```
{: codeblock}  

其中

<table>
  <caption>定義容器之 CPU 度量值所需的欄位</caption>
  <tr>
    <th>欄位</th>
	  <th>說明</th>
	  <th>值</th>
  </tr>
  <tr>
    <td>來源</td>
	  <td>這是保留名稱。此階層下的度量值來自 {{site.data.keyword.Bluemix_notm}} 應用程式及服務。</td>
	  <td>*ibmcloud*</td>
  </tr>
  <tr>
    <td>雲端類型</td>
	  <td>指出雲端類型。</td>
	  <td>對於 {{site.data.keyword.Bluemix_notm}} 公用雲端，值為：*public*</td>
  </tr>
  <tr>
    <td>服務名稱</td>
	  <td>定義 {{site.data.keyword.Bluemix_notm}} 中服務的名稱。</td>
	  <td>對於 CF 應用程式，值為：*cloud-foundry*</td>
  </tr>
  <tr>
    <td>地區</td>
	  <td>定義容器執行所在的地區。</td>
	  <td>對於「美國南部」地區，值為：*us-south* <br>對於「英國」地區，值為：*united-kingdom*  <br>對於「德國」，值為：*frankfurt* <br>對於「雪梨」，值為：*sydney* </td>
  </tr>
  <tr>
    <td>叢集名稱</td>
	  <td>要監視之叢集的名稱。</td>
	  <td></td>
  </tr>
  <tr>
    <td>度量值來源</td>
	  <td>資料的來源。</td>
	  <td>*container* </td>
  </tr>
  <tr>
    <td>名稱空間</td>
	<td>Kubernetes 叢集中容器部署所在的名稱空間。</td>
	<td></td>
  </tr>
   <tr>
    <td>Pod 名稱</td>
	<td>Pod 的名稱。</td>
	<td></td>
  </tr>
  <tr>
    <td>容器名稱</td>
	<td>容器的名稱。</td>
	<td></td>
  </tr>
  <tr>
    <td>度量值類型</td>
	  <td>度量值的類型。</td>
	  <td>*CPU*</td>
  </tr>
  <tr>
    <td>度量值子類型</td>
	  <td>要顯示的度量值。</td>
	  <td>*usage*、*num-cores*、*usage-pct*、*usage-pct-container-requested*</td>
  </tr>
  <tr>
    <td>函數</td>
    <td>您可以選取以視覺化畫面中之容器度量值的查詢函數。</td>
    <td>[Functions ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
   </tr>
</table>

例如，監視「美國南部」地區的 Kubernetes 叢集中所執行容器之 CPU 用量的查詢定義如下：

```
ibmcloud.public.containers-kubernetes.us-south.myCluster.container.default.myPod.myContainer-1775968925-kfwfk.cpu.usage
```
{: screen}



## 針對工作者節點所收集之負載度量值的查詢格式
{: #load_workers}

您在 Grafana 中定義以監視 {{site.data.keyword.containershort_notm}} 服務中所執行工作者節點之負載度量值的查詢格式說明如下： 

```
{Source}.{Cloud Type}.{Service Name}.{Region}.{Cluster Name}.{Metric Source}.{Worker Name}.{Metric Type}.{Metric Subtype}.[Functions]
```
{: codeblock}  

其中

<table>
  <caption>定義工作者節點之負載度量值所需的欄位</caption>
  <tr>
    <th>欄位</th>
	<th>說明</th>
	<th>值</th>
  </tr>
  <tr>
    <td>來源</td>
	  <td>這是保留名稱。此階層下的度量值來自 {{site.data.keyword.Bluemix_notm}} 應用程式及服務。</td>
	  <td>*ibmcloud*</td>
  </tr>
  <tr>
    <td>雲端類型</td>
	  <td>指出雲端類型。</td>
	  <td>對於 {{site.data.keyword.Bluemix_notm}} 公用雲端，值為：*public*</td>
  </tr>
  <tr>
    <td>服務名稱</td>
	  <td>定義 {{site.data.keyword.Bluemix_notm}} 中服務的名稱。</td>
	  <td>對於 CF 應用程式，值為：*cloud-foundry*</td>
  </tr>
  <tr>
    <td>地區</td>
	  <td>定義容器執行所在的地區。</td>
	  <td>對於「美國南部」地區，值為：*us-south* <br>對於「英國」地區，值為：*united-kingdom*  <br>對於「德國」，值為：*frankfurt* <br>對於「雪梨」，值為：*sydney* </td>
  </tr>
  <tr>
    <td>叢集名稱</td>
	<td>要監視之叢集的名稱。</td>
	<td></td>
  </tr>
  <tr>
    <td>度量值來源</td>
	<td>資料的來源。</td>
	<td>*worker* </td>
  </tr>
   <tr>
    <td>工作者節點名稱</td>
	<td>工作者節點的名稱。</td>
	<td></td>
  </tr>
  <tr>
    <td>度量值類型</td>
	<td>度量值的類型。</td>
	<td>*load*</td>
  </tr>
  <tr>
    <td>度量值子類型</td>
	  <td>要顯示的度量值。</td>
	  <td>*avg-1*、*avg-5*、*avg-15*</td>
  </tr>
  <tr>
    <td>函數</td>
    <td>您可以選取以視覺化畫面中之容器度量值的查詢函數。</td>
    <td>[Functions ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
   </tr>
</table>

例如，監視「美國南部」地區的 Kubernetes 叢集中所執行工作者節點之 CPU 用量的查詢定義如下：

```
ibmcloud.public.containers-kubernetes.us-south.myCluster.worker.MyWorker.load.avg-1
```
{: screen}


## 針對容器所收集之記憶體度量值的查詢格式
{: #mem_containers}

您在 Grafana 中定義以監視 {{site.data.keyword.containershort_notm}} 服務中所執行容器之記憶體度量值的查詢格式說明如下： 

```
{Source}.{Cloud Type}.{Service Name}.{Region}.{Cluster Name}.{Namespace}.{Metric Source}.{Pod Name}.{Container Name}.{Metric Type}.{Metric Subtype}.[Functions]
```
{: codeblock}  

其中

<table>
  <caption>定義容器之記憶體度量值所需的欄位</caption>
  <tr>
    <th>欄位</th>
	<th>說明</th>
	<th>值</th>
  </tr>
  <tr>
    <td>來源</td>
	  <td>這是保留名稱。此階層下的度量值來自 {{site.data.keyword.Bluemix_notm}} 應用程式及服務。</td>
	  <td>*ibmcloud*</td>
  </tr>
  <tr>
    <td>雲端類型</td>
	  <td>指出雲端類型。</td>
	  <td>對於 {{site.data.keyword.Bluemix_notm}} 公用雲端，值為：*public*</td>
  </tr>
  <tr>
    <td>服務名稱</td>
	  <td>定義 {{site.data.keyword.Bluemix_notm}} 中服務的名稱。</td>
	  <td>對於 CF 應用程式，值為：*cloud-foundry*</td>
  </tr>
  <tr>
    <td>地區</td>
	  <td>定義容器執行所在的地區。</td>
	  <td>對於「美國南部」地區，值為：*us-south* <br>對於「英國」地區，值為：*united-kingdom*  <br>對於「德國」，值為：*frankfurt* <br>對於「雪梨」，值為：*sydney* </td>
  </tr>
  <tr>
    <td>叢集名稱</td>
	<td>要監視之叢集的名稱。</td>
	<td></td>
  </tr>
  <tr>
    <td>度量值來源</td>
	<td>資料的來源。</td>
	<td>*container* </td>
  </tr>
  <tr>
    <td>名稱空間</td>
	<td>Kubernetes 叢集中容器部署所在的名稱空間。</td>
	<td></td>
  </tr>
   <tr>
    <td>Pod 名稱</td>
	<td>Pod 的名稱。</td>
	<td></td>
  </tr>
  <tr>
    <td>容器名稱</td>
	  <td>容器的名稱。</td>
	  <td></td>
  </tr>
  <tr>
    <td>度量值類型</td>
  	<td>度量值的類型。</td>
  	<td>*memory*</td>
  </tr>
  <tr>
    <td>度量值子類型</td>
	  <td>要顯示的度量值。</td>
	  <td>*limit*、*current*、*usage-pct*</td>
  </tr>
  <tr>
    <td>函數</td>
    <td>您可以選取以視覺化畫面中之容器度量值的查詢函數。</td>
    <td>[Functions ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
   </tr>
</table>

例如，監視「美國南部」地區的 Kubernetes 叢集中所執行容器之記憶體使用率的查詢定義如下：

```
ibmcloud.public.containers-kubernetes.us-south.myCluster.container.default.myPod.myContainer-1775968925-kfwfk.memory.usage
```
{: screen}
