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


# CF 應用程式
{: #cfapps_metrics_format}

Grafana 中所定義以監視「{{site.data.keyword.Bluemix}} 公用」中執行之 Cloud Foundry 應用程式的查詢，必須符合下列格式：
{:shortdesc}

```
{Source}.{Cloud Type}.{Service Name}.{Region}.{CFapp Name}.{CFapp Index}.{CFapp container}.{Metric Type}.{Metric Subtype}.[Functions]
```
{: codeblock}

其中

<table>
  <caption>查詢中的一般欄位</caption>
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
	<td>定義 CF 應用程式實例執行所在的地區。</td>
	<td>對於「美國南部」地區，值為：*us-south* <br>對於「英國」地區，值為：*eu-gb* <br>對於「德國」，值為：*eu-de* <br>對於「雪梨」，值為：*au-syd* </td>
  </tr>
  <tr>
    <td>CF 應用程式名稱</td>
	<td>CF 應用程式的名稱。</td>
	<td></td>
  </tr>
  <tr>
    <td>CF 應用程式索引</td>
	  <td>CF 應用程式實例的索引。</td>
	  <td>例如：*0* </br>如果您的 CF 應用程式有一個實例，則只會有索引 0。如果您擴充 CF 應用程式（例如，擴充為 10 個實例），則您有 0 到 9 作為索引值。</td>
  </tr>
  <tr>
    <td>CFapp 容器</td>
	  <td>固定值。</td>
	  <td>*container*</td>
  </tr>
  <tr>
    <td>度量值類型</td>
	  <td>度量值的類型。磁碟、記憶體及 CPU 是自動收集的度量值系列。</td>
	  <td>*CPU*</td>
  </tr>
  <tr>
    <td>度量值子類型</td>
	  <td>要顯示的度量值。</br>[CPU 度量值](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#cpu_metrics) </br>[磁碟度量值](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#disk_metrics)   </br>[記憶體度量值](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#mem_metrics)</td>
	  <td></td>
  </tr>
  <tr>
    <td>函數</td>
    <td>您可以選取以視覺化畫面中之容器度量值的查詢函數。</td>
    <td>[Functions ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
   </tr>
</table>




