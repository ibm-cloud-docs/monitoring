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



# Grafana 사용에 대한 FAQ
{: #grafana_qa}

여기에는 Grafana를 {{site.data.keyword.monitoringshort}} 서비스와 함께 사용하는 데 대한 일반적인 질문의 답이 제공되어 있습니다. 
{:shortdesc}

* [Grafana 대시보드에서 경보 API를 사용하여 정의한 경보가 표시되지 않음](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-grafana_qa#alerts1)
* [Grafana 대시보드에 수행한 변경사항을 저장하려고 시도할 때 BXNMSAL41E가 발생함](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-grafana_qa#BXNMSAL41E)
* [Grafana 대시보드에 경보를 추가한 후에 변경사항을 저장하려고 시도할 때 BXNMSAL36E가 발생함](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-grafana_qa#BXNMSAL36E)
* [Monitoring 서비스 웹 UI에 로그인할 때 404 오류가 발생함](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-grafana_qa#404)
* [방금 Grafana 대시보드를 위한 json 데이터를 업로드했는데 화면이동 막대가 사라진 이유가 무엇입니까?](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-grafana_qa#2)


## Grafana 대시보드에서 경보 API를 사용하여 정의한 경보가 표시되지 않음
{: #alerts1}

경보 API를 사용하여 정의하는 경보는 Grafana의 경보 탭에 표시되지 않습니다. Grafana에서 경보를 보려면 Grafana 대시보드에서 직접 정의해야 합니다.

자세한 정보는 [Grafana에서 경보 구성](/docs/services/cloud-monitoring/alerts?topic=cloud-monitoring-config_alerts_grafana#config_alerts_grafana)을 참조하십시오.

## Grafana 대시보드에 수행한 변경사항을 저장하려고 시도할 때 BXNMSAL41E가 발생함
{: #BXNMSAL41E}

Grafana에서 알림 채널 및 경보를 정의할 수 있습니다. Grafana에서 알림 채널을 삭제하고 알림 채널을 제거하도록 규칙을 업데이트하지 않으면 Grafana 대시보드를 저장하려고 시도할 때 **BXNMSAL41E** 오류가 발생합니다.

이 문제점을 수정하려면 경보 API를 사용하여 규칙을 업데이트하고 대시보드 저장을 다시 시도하십시오. 규칙을 저장할 때 삭제된 알림 채널을 제거하십시오.

자세한 정보는 [경보 API](https://console.bluemix.net/apidocs/940-ibm-cloud-monitoring-alerts-api?&language=node#introduction)를 참조하십시오.

## Grafana 대시보드에 경보를 추가한 후에 변경사항을 저장하려고 시도할 때 BXNMSAL36E가 발생함
{: #BXNMSAL36E}

{{site.data.keyword.monitoringshort}} 서비스에서 메트릭을 모니터링하는 도메인에 대한 할당량에 도달하는 경우, **BXNMSAL36E** 오류가 발생합니다.

플랜을 업그레이드하고 다시 시도하십시오.

플랜을 업그레이드하는 방법에 대한 자세한 정보는 [플랜 변경](/docs/services/cloud-monitoring/plan?topic=cloud-monitoring-change_plan#change_plan)을 참조하십시오.


## UUA 인증 모델을 사용해 Monitoring 서비스 웹 UI에 로그인할 때 404 오류가 발생함
{: #404}

{{site.data.keyword.monitoringshort}} 서비스 웹 UI(Grafana)에 로그인하는 중에 404 오류가 발생하는 경우에는 해당 영역이 존재하며 여기에 대한 액세스 권한이 있는지 확인하십시오.

[UAA 인증 모델](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_uaa#auth_uaa)을 사용하여 {{site.data.keyword.monitoringshort}} 서비스에 액세스하는 경우에는 {{site.data.keyword.Bluemix_notm}} 콘솔에 로그인할 때 사용하는 것과 같은 사용자 ID 및 비밀번호를 사용해야 합니다. 

로그인하려는 계정, 조직 및 영역에 대한 액세스 권한이 있는지 확인하려면 {{site.data.keyword.Bluemix_notm}} 콘솔에 로그인한 후 영역으로 전환하십시오. 

명령행을 사용하여 영역에 대한 액세스 권한이 있는지 확인할 수도 있습니다. 다음 명령을 실행하여 {{site.data.keyword.Bluemix_notm}} 지역, 조직 및 영역에 로그인하십시오.

```
ibmcloud login -a https://api.ng.bluemix.net
```
{: codeblock}

지시사항을 따르십시오. {{site.data.keyword.Bluemix_notm}} 인증 정보를 입력하고 조직 및 영역을 선택하십시오.


## 방금 Grafana 대시보드를 위한 JSON 데이터를 업로드했는데 화면이동 막대가 사라진 이유가 무엇입니까?
{: #2}

Grafana에는 대시보드를 가져온 후 화면이동 막대가 숨겨지는 버그가 있습니다. 

화면이동 막대를 표시하려면 대시보드를 가져온 후 저장하십시오. 








