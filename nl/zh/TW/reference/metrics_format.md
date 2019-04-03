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


# 一般格式
{: #metrics_format}

Grafana 中所定義以監視 {{site.data.keyword.Bluemix}} 服務的查詢，必須符合下列格式：
{:shortdesc}

```
{Source}.{Cloud Type}.{Service Name}.{Region}.[service fields].{Metric type}.{Metric Subtype}.[Functions]
```
{: codeblock}

其中 [service fields] 代表服務或 CF 應用程式之度量值查詢的特定欄位。 

<table>
  <caption>查詢中的一般欄位</caption>
  <tr>
    <th>欄位</th>
	<th>說明</th>
	<th>值</th>
  </tr>
  <tr>
    <td>來源</td>
	<td>這是保留名稱。此階層下的度量值來自 {{site.data.keyword.Bluemix_notm}} 服務。</td>
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
	  <td>對於 {{site.data.keyword.containershort}}，值為：*containers-kubernetes*</td>
  </tr>
  <tr>
    <td>地區</td>
	  <td>定義容器執行所在的地區。</td>
	  <td>對於「美國南部」地區，值為：*us-south* <br>對於「英國」地區，值為：*united-kingdom*  <br>對於「德國」，值為：*frankfurt* <br>對於「雪梨」，值為：*sydney* </td>
  </tr>
  <tr>
    <td>度量值類型</td>
	<td>度量值的類型。</td>
	<td>*cpu* <br>*load* <br>*memory*</td>
  </tr>
  <tr>
    <td>度量值子類型</td>
	<td>度量值的子類型。</td>
	<td>例如：*usage*、*num-cores*、*usage-pct*、*usage-pct-container-requested*</td>
  </tr>
  <tr>
    <td>函數</td>
    <td>您可以選取以視覺化畫面中之容器度量值的查詢函數。</td>
    <td>[Functions ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
   </tr>
</table>




