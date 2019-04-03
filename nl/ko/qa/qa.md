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



# 자주 묻는 질문과 응답
{: #qa}

여기에는 {{site.data.keyword.monitoringshort}} 서비스에 대한 일반적인 질문의 답이 제공되어 있습니다. 
{:shortdesc}

* [최근에 메트릭 값을 전송하지 않은 메트릭에 대한 내 이전 데이터를 볼 수 없는 이유는 무엇입니까?](#qa31)


## 최근에 메트릭 값을 전송하지 않은 메트릭에 대한 내 이전 데이터를 볼 수 없는 이유는 무엇입니까?
{: #qa31}

{{site.data.keyword.monitoringshort}}에서는 지난 7일 동안 기록되지 않은 메트릭을 식별하여 임시적인 것으로 보이는 메트릭 경로의 모든 데이터를 삭제합니다. 

예를 들어 다음과 같습니다.

* 컨테이너가 삭제된 경우, 해당 컨테이너와 연관된 메트릭은 메트릭이 삭제된 시점부터 7일 동안 보존됩니다.
* `<space_id>.test.statsd.gauge-hello`라는 이름의 statsd 게이지가 있으며 이 항목이 1주일 동안 기록되지 않은 경우에는 해당 메트릭이 임시적인 것으로 식별되며 이 메트릭이 모든 해당 히스토리 정보와 함께 삭제됩니다. 

