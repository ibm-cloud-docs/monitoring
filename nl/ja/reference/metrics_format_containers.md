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

{{site.data.keyword.containershort_notm}} サービスをモニターするために Grafana で定義する照会は、以下のパターンに従います。 
{:shortdesc}



## コンテナーに関して収集される CPU メトリックの照会フォーマット
{: #cpu_containers}

{{site.data.keyword.containershort_notm}} サービス内で実行されているコンテナーに関する CPU メトリックをモニターするために Grafana で定義する照会のフォーマットは、以下のとおりです。 

```
{Source}.{Cloud Type}.{Service Name}.{Region}.{Cluster Name}.{Namespace}.{Metric Source}.{Pod Name}.{Container Name}.{Metric Type}.{Metric Subtype}.[Functions]
```
{: codeblock}  

ここで、

<table>
  <caption>コンテナーの CPU メトリックを定義するために必要なフィールド </caption>
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
	  <td>コンテナーが実行されている地域を定義します。</td>
	  <td>米国南部地域の場合、この値は *us-south* <br>英国地域の場合、この値は *united-kingdom*  <br>ドイツの場合、この値は *frankfurt* <br>シドニーの場合、この値は *sydney* </td>
  </tr>
  <tr>
    <td>Cluster Name</td>
	  <td>モニターするクラスターの名前。</td>
	  <td></td>
  </tr>
  <tr>
    <td>Metric Source</td>
	  <td>データのソース。</td>
	  <td>*container* </td>
  </tr>
  <tr>
    <td>Namespace</td>
	<td>コンテナーがデプロイされた Kubernetes クラスター内の名前空間。</td>
	<td></td>
  </tr>
   <tr>
    <td>Pod Name</td>
	<td>Pod の名前。</td>
	<td></td>
  </tr>
  <tr>
    <td>Container Name</td>
	<td>コンテナーの名前。</td>
	<td></td>
  </tr>
  <tr>
    <td>Metric Type</td>
	  <td>メトリックのタイプ。</td>
	  <td>*CPU*</td>
  </tr>
  <tr>
    <td>Metric Subtype</td>
	  <td>表示されるメトリック。</td>
	  <td>*usage*、*num-cores*、*usage-pct*、*usage-pct-container-requested*</td>
  </tr>
  <tr>
    <td>Functions</td>
    <td>パネル内でコンテナー・メトリックを視覚化するために選択できる照会関数。 </td>
    <td>[Functions ![(外部リンク・アイコン)](../../../icons/launch-glyph.svg "外部リンク・アイコン")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
   </tr>
</table>

例えば、米国南部地域の Kubernetes クラスターで実行されているコンテナーの CPU 使用量をモニターするための照会は、次のように定義されます。

```
ibmcloud.public.containers-kubernetes.us-south.myCluster.container.default.myPod.myContainer-1775968925-kfwfk.cpu.usage
```
{: screen}



## ワーカーに関して収集されるロード・メトリックの照会フォーマット
{: #load_workers}

{{site.data.keyword.containershort_notm}} サービス内で実行されているワーカーに関するロード・メトリックをモニターするために Grafana で定義する照会のフォーマットは、以下のとおりです。 

```
{Source}.{Cloud Type}.{Service Name}.{Region}.{Cluster Name}.{Metric Source}.{Worker Name}.{Metric Type}.{Metric Subtype}.[Functions]
```
{: codeblock}  

ここで、

<table>
  <caption>ワーカーのロード・メトリックを定義するために必要なフィールド </caption>
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
	  <td>コンテナーが実行されている地域を定義します。</td>
	  <td>米国南部地域の場合、この値は *us-south* <br>英国地域の場合、この値は *united-kingdom*  <br>ドイツの場合、この値は *frankfurt* <br>シドニーの場合、この値は *sydney* </td>
  </tr>
  <tr>
    <td>Cluster Name</td>
	<td>モニターするクラスターの名前。</td>
	<td></td>
  </tr>
  <tr>
    <td>Metric Source</td>
	<td>データのソース。</td>
	<td>*worker* </td>
  </tr>
   <tr>
    <td>Worker Name</td>
	<td>ワーカーの名前。</td>
	<td></td>
  </tr>
  <tr>
    <td>Metric Type</td>
	<td>メトリックのタイプ。</td>
	<td>*load*</td>
  </tr>
  <tr>
    <td>Metric Subtype</td>
	  <td>表示されるメトリック。</td>
	  <td>*avg-1*、*avg-5*、*avg-15*</td>
  </tr>
  <tr>
    <td>Functions</td>
    <td>パネル内でコンテナー・メトリックを視覚化するために選択できる照会関数。 </td>
    <td>[Functions ![(外部リンク・アイコン)](../../../icons/launch-glyph.svg "外部リンク・アイコン")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
   </tr>
</table>

例えば、米国南部地域の Kubernetes クラスターで実行されているワーカーの CPU 使用量をモニターするための照会は、次のように定義されます。

```
ibmcloud.public.containers-kubernetes.us-south.myCluster.worker.MyWorker.load.avg-1
```
{: screen}


## コンテナーに関して収集されるメモリー・メトリックの照会フォーマット
{: #mem_containers}

{{site.data.keyword.containershort_notm}} サービス内で実行されているコンテナーに関するメモリー・メトリックをモニターするために Grafana で定義する照会のフォーマットは、以下のとおりです。 

```
{Source}.{Cloud Type}.{Service Name}.{Region}.{Cluster Name}.{Namespace}.{Metric Source}.{Pod Name}.{Container Name}.{Metric Type}.{Metric Subtype}.[Functions]
```
{: codeblock}  

ここで、

<table>
  <caption>コンテナーのメモリー・メトリックを定義するために必要なフィールド</caption>
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
	  <td>コンテナーが実行されている地域を定義します。</td>
	  <td>米国南部地域の場合、この値は *us-south* <br>英国地域の場合、この値は *united-kingdom*  <br>ドイツの場合、この値は *frankfurt* <br>シドニーの場合、この値は *sydney* </td>
  </tr>
  <tr>
    <td>Cluster Name</td>
	<td>モニターするクラスターの名前。</td>
	<td></td>
  </tr>
  <tr>
    <td>Metric Source</td>
	<td>データのソース。</td>
	<td>*container* </td>
  </tr>
  <tr>
    <td>Namespace</td>
	<td>コンテナーがデプロイされた Kubernetes クラスター内の名前空間。</td>
	<td></td>
  </tr>
   <tr>
    <td>Pod Name</td>
	<td>Pod の名前。</td>
	<td></td>
  </tr>
  <tr>
    <td>Container Name</td>
	  <td>コンテナーの名前。</td>
	  <td></td>
  </tr>
  <tr>
    <td>Metric Type</td>
  	<td>メトリックのタイプ。</td>
  	<td>*memory*</td>
  </tr>
  <tr>
    <td>Metric Subtype</td>
	  <td>表示されるメトリック。</td>
	  <td>*limit*、*current*、*usage-pct*</td>
  </tr>
  <tr>
    <td>Functions</td>
    <td>パネル内でコンテナー・メトリックを視覚化するために選択できる照会関数。 </td>
    <td>[Functions ![(外部リンク・アイコン)](../../../icons/launch-glyph.svg "外部リンク・アイコン")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
   </tr>
</table>

例えば、米国南部地域の Kubernetes クラスターで実行されているコンテナーのメモリー使用量をモニターするための照会は、次のように定義されます。

```
ibmcloud.public.containers-kubernetes.us-south.myCluster.container.default.myPod.myContainer-1775968925-kfwfk.memory.usage
```
{: screen}
