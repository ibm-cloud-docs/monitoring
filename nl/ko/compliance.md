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


# 규제 준수
{: #compliance}

[{{site.data.keyword.Bluemix}}는 IBM의 엄격한 보안 기준에 따라 빌드된 여러 서비스 및 Cloud 플랫폼을 제공합니다](/docs/security/compliance.html#compliance). {{site.data.keyword.monitoringlong}} 서비스는 {{site.data.keyword.Bluemix_notm}}용으로 빌드된 DevOps 서비스입니다. 
{:shortdesc}


## 일반 개인정보 보호법률(General Data Protection Regulation)

GDPR(General Data Protection Regulation)은 EU 전역에서 통합 데이터 보호 법률 체계를 만들기 위해 노력하며 세계 어느 곳에서나 개인 데이터를 '처리' 및 호스팅하는 데 엄격한 규칙을 적용하여 개인 데이터의 제어 권한을 모든 개인에게 돌려주는 것을 목표로 합니다. 또한 이 규정에서는 EU 안팎에서 개인 데이터의 자유로운 이동과 관련된 규칙을 소개합니다. 

**면책사항:** {{site.data.keyword.monitoringshort}} 서비스는 {{site.data.keyword.Bluemix_notm}}의 사용자 계정에서 실행하는 클라우드 리소스의 메트릭 및 {{site.data.keyword.Bluemix_notm}} 외부에서 전송할 수 있는 메트릭을 저장하고 표시합니다. PI(Personal information)를 {{site.data.keyword.monitoringshort}}에 저장되는 메트릭 항목에 포함해서는 안 됩니다. 이 데이터는 기업 내의 다른 사용자뿐만 아니라 Cloud Service를 지원하기 위해 {{site.data.keyword.IBM_notm}}에서 액세스할 수 있으므로 메트릭 항목에 포함되지 않아야 합니다.

### 지역
{: #regions}

{{site.data.keyword.monitoringshort}} 서비스는 서비스를 사용할 수 있는 {{site.data.keyword.Bluemix_notm}} 퍼블릭 지역 내에서 GDPR을 준수합니다.


### 데이터 보존
{: #data_retention}

{{site.data.keyword.monitoringshort}} 서비스는 표준 또는 Lite 서비스 플랜의 경우 15일 동안 메트릭을 저장하며 프리미엄 플랜의 경우에는 45일 동안 저장합니다.


### 데이터 삭제
{: #data_deletion}

다음 정보를 고려하십시오.

* {{site.data.keyword.monitoringshort}} 서비스 표준 또는 Lite 플랜의 경우 15일 후에 메트릭이 자동으로 삭제됩니다.
* {{site.data.keyword.monitoringshort}} 서비스 프리미엄 플랜의 경우 45일 후에 메트릭이 자동으로 삭제됩니다.
* 활성이 아닌 메트릭은 7일 후에 자동으로 삭제됩니다.


 언제든지 메트릭 API를 사용하여 메트릭을 삭제할 수 있습니다. 



### 자세한 정보
{: #info}

자세한 정보는 다음을 참조하십시오.

[{{site.data.keyword.Bluemix_notm}} 보안 규제 준수](/docs/security/compliance.html#compliance)

[GDPR - {{site.data.keyword.IBM_notm}} 공식 페이지](https://www.ibm.com/data-responsibility/gdpr/)



