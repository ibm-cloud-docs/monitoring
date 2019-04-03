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


# CF アプリ
{: #cfapps_metrics_format}

{{site.data.keyword.Bluemix}} Public で実行されている Cloud Foundry アプリケーションをモニターするために Grafana で定義する照会は、以下のフォーマットに準拠している必要があります。 
{:shortdesc}

```
{Source}.{Cloud Type}.{Service Name}.{Region}.{CFapp Name}.{CFapp Index}.{CFapp container}.{Metric Type}.{Metric Subtype}.[Functions]
```
{: codeblock}

ここで、

<table>
  <caption>照会の共通フィールド</caption>
  <tr>
    <th>フィールド</th>
	<th>説明</th>
	<th>値</th>
  </tr>
  <tr>
    <td>Source</td>
	<td>これは予約名です。 この階層の下のメトリックは {{site.data.keyword.Bluemix_notm}} アプリケーションおよびサービスからのものです。</td>
	<td>*ibmcloud*</td>
  </tr>
  <tr>
    <td>Cloud Type</td>
	<td>クラウドのタイプを示します。 </td>
	<td>{{site.data.keyword.Bluemix_notm}} パブリック・クラウドの場合、値は *public* です。</td>
  </tr>
  <tr>
    <td>Service Name</td>
	<td>{{site.data.keyword.Bluemix_notm}} 内のサービスの名前を定義します。</td>
	<td>CF アプリの場合、値は *cloud-foundry* です。</td>
  </tr>
  <tr>
    <td>Region</td>
	<td>CF アプリ・インスタンスが実行されている地域を定義します。</td>
	<td>米国南部地域の場合、この値は *us-south* <br>英国地域の場合、この値は *eu-gb*  <br>ドイツの場合、この値は *eu-de* <br>シドニーの場合、この値は*au-syd* </td>
  </tr>
  <tr>
    <td>CFapp Name</td>
	<td>CF アプリケーションの名前。</td>
	<td></td>
  </tr>
  <tr>
    <td>CFapp Index</td>
	  <td>CF アプリケーション・インスタンスの索引。</td>
	  <td>例: *0* </br>1 つのインスタンスを持つ CF アプリがある場合、索引は 0 のみです。CF アプリを、例えば 10 個のインスタンスに拡大する場合は、索引値は 0 から 9 までになります。</td>
  </tr>
  <tr>
    <td>CFapp container</td>
	  <td>固定値。</td>
	  <td>*container*</td>
  </tr>
  <tr>
    <td>Metric Type</td>
	  <td>メトリックのタイプ。 ディスク、メモリー、および CPU は、自動的に収集されるメトリック・シリーズです。</td>
	  <td>*CPU*</td>
  </tr>
  <tr>
    <td>Metric Subtype</td>
	  <td>表示されるメトリック。 </br>[CPU メトリック](/docs/services/cloud-monitoring/cf?topic=cloud-monitoring-cloud-foundry-apps#cpu_metrics) </br>[ディスクのメトリック](/docs/services/cloud-monitoring/cf?topic=cloud-monitoring-cloud-foundry-apps#disk_metrics) </br>[メモリーのメトリック](/docs/services/cloud-monitoring/cf?topic=cloud-monitoring-cloud-foundry-apps#mem_metrics)</td>
	  <td></td>
  </tr>
  <tr>
    <td>Functions</td>
    <td>パネル内でコンテナー・メトリックを視覚化するために選択できる照会関数。 </td>
    <td>[Functions ![(外部リンク・アイコン)](../../../icons/launch-glyph.svg "外部リンク・アイコン")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
   </tr>
</table>




