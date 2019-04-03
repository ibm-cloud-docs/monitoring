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


# 汎用フォーマット
{: #metrics_format}

{{site.data.keyword.Bluemix}} サービスをモニターするために Grafana で定義する照会は、以下のフォーマットに準拠している必要があります。 
{:shortdesc}

```
{Source}.{Cloud Type}.{Service Name}.{Region}.[service fields].{Metric type}.{Metric Subtype}.[Functions]
```
{: codeblock}

ここで、[service fields] は、サービスまたは CF アプリのメトリック照会の特定のフィールドを表します。 

<table>
  <caption>照会の共通フィールド</caption>
  <tr>
    <th>フィールド</th>
	<th>説明</th>
	<th>値</th>
  </tr>
  <tr>
    <td>Source</td>
	<td>これは予約名です。 この階層の下のメトリックは {{site.data.keyword.Bluemix_notm}} サービスからのものです。</td>
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
	  <td>{{site.data.keyword.containershort}} の場合、値は *containers-kubernetes* です。</td>
  </tr>
  <tr>
    <td>Region</td>
	  <td>コンテナーが実行されている地域を定義します。</td>
	  <td>米国南部地域の場合、この値は *us-south* <br>英国地域の場合、この値は *united-kingdom*  <br>ドイツの場合、この値は *frankfurt* <br>シドニーの場合、この値は *sydney* </td>
  </tr>
  <tr>
    <td>Metric Type</td>
	<td>メトリックのタイプ。</td>
	<td>*cpu* <br>*load* <br>*memory*</td>
  </tr>
  <tr>
    <td>Metric Subtype</td>
	<td>メトリックのサブタイプ。</td>
	<td>例: *usage*、*num-cores*、*usage-pct*、*usage-pct-container-requested*</td>
  </tr>
  <tr>
    <td>Functions</td>
    <td>パネル内でコンテナー・メトリックを視覚化するために選択できる照会関数。 </td>
    <td>[Functions ![(外部リンク・アイコン)](../../../icons/launch-glyph.svg "外部リンク・アイコン")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
   </tr>
</table>




