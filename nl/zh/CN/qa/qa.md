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



# 常见问题及解答
{: #qa}

下面是对有关 {{site.data.keyword.monitoringshort}} 服务的常见问题的解答。
{:shortdesc}

* [对于我最近未发送度量值的某个度量值，为什么我看不到旧数据？](#qa31)


## 对于我最近未发送其度量值的某个度量值，为什么我看不到旧数据？
{: #qa31}

{{site.data.keyword.monitoringshort}} 通过识别在过去 7 天内未写入的度量值，删除看起来性质是瞬态的度量值路径的所有数据。 

例如：

* 删除容器时，与该容器关联的度量值会保留 7 天，在此之后会将其删除。
* 如果您有一个名为 `<space_id>.test.statsd.gauge-hello` 的 statsd 量表，并且一周内未向其写入内容，那么该度量值将被识别为瞬态，因此将删除该度量值及其所有历史信息。 

