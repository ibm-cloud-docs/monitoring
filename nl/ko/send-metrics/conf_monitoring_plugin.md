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

# Monitoring 플러그인(collectd)을 사용하여 데이터 전송
{: #conf_monitoring_plugin}

환경에서 메트릭을 수집하도록 collectd를 구성할 수 있습니다. {{site.data.keyword.monitoringshort}} 플러그인을 사용하여 이러한 메트릭을 사용자 환경의 영역 도메인으로 전송하십시오. 
{: shortdesc}

다음 그림은 {{site.data.keyword.monitoringshort}} 플러그인을 사용하여 {{site.data.keyword.monitoringshort}} 서비스에 메트릭을 전송하는 방법에 대한 상위 레벨 보기를 보여줍니다.

![{{site.data.keyword.monitoringshort}} 플러그인 사용 방법에 대한 상위 레벨 보기](images/monitoring_plugin_ov.png "{{site.data.keyword.monitoringshort}} 플러그인 사용 방법에 대한 상위 레벨 보기")



## Monitoring 플러그인 설치
{: #install}

터미널에서 다음 단계를 완료하십시오. 

1. (전제조건) {{site.data.keyword.Bluemix_notm}} CLI를 설치하십시오.

   자세한 정보는 [{{site.data.keyword.Bluemix_notm}} CLI 설치](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#cli_qa)를 참조하십시오.
   
   CLI가 설치되어 있는 경우에는 다음 단계를 진행하십시오.
	
2. {{site.data.keyword.Bluemix_notm}} 지역, 조직 및 영역에 로그인하십시오. 

    자세한 정보는 [{{site.data.keyword.Bluemix_notm}}에 로그인하는 방법](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login)을 참조하십시오.

    예를 들어, 미국 남부 지역에 로그인하려면 다음 명령을 실행하십시오.
	
	```
    ibmcloud login -a https://api.ng.bluemix.net
	ibmcloud target -o MyOrg -s MySpace
    ```
    {: codeblock}

    지시사항을 따르십시오. {{site.data.keyword.Bluemix_notm}} 인증 정보를 입력하고 조직 및 영역을 선택하십시오.

### 1단계: collectd 설치
{: #collectd}

관리자로 다음 단계를 완료하여 collectd를 설치하십시오.

1.	루트 사용자로 로그인하십시오. 

    ```
    sudo -s
    ```
    {: codeblock}

2.	로그의 시간을 동기화하려면 NTP(Network Time Protocol) 패키지를 설치하십시오. 

    예를 들어, Ubunutu 시스템의 경우 `timedatectl status`가 *Network time on: yes*를 표시하는지 확인하십시오. 이와 같이 표시되는 경우 Ubuntu 시스템이 이미 ntp를 사용하도록 구성되었으므로 이 단계를 건너뛸 수 있습니다.
    
    ```
    # timedatectl status
    Local time: Mon 2017-06-12 03:01:22 PDT
    Universal time: Mon 2017-06-12 10:01:22 UTC
    RTC time: Mon 2017-06-12 10:01:22
    Time zone: America/Los_Angeles (PDT, -0700)
    Network time on: yes
    NTP synchronized: yes
    RTC in local TZ: no
    ```
    {: screen}
    
    Ubuntu 시스템에서 ntp를 설치하려면 다음 단계를 완료하십시오.

    1.	다음 명령을 실행하여 패키지를 업데이트하십시오. 

        ```
        apt-get update
        ```
        {: codeblock}
        
    2.	다음 명령을 실행하여 ntp 패키지를 설치하십시오. 

        ```
        apt-get install ntp
        ```
        {: codeblock}
        
    3.	다음 명령을 실행하여 ntpdate 패키지를 설치하십시오. 
    
        ```
        apt-get install ntpdate
        ```
        {: codeblock}
        
    4.	다음 명령을 실행하여 서비스를 중지하십시오. 
        
        ```
        service ntp stop
        ```
        {: codeblock}
        
    5.	다음 명령을 실행하여 시스템 시계를 동기화하십시오. 
    
        ```
        ntpdate -u 0.ubuntu.pool.ntp.org
        ```
        {: codeblock}
        
        결과를 통해 시간이 동기화되었는지 확인할 수 있습니다. 예를 들어, 다음과 같습니다.
        
        ```
        4 May 19:02:17 ntpdate[5732]: adjust time server 50.116.55.65 offset 0.000685 sec
        ```
        {: screen}
        
    6.	다음 명령을 실행하여 ntpd를 다시 시작하십시오. 
    
        ```
        service ntp start
        ```
        {: codeblock}
    
        결과를 통해 서비스가 시작 중임을 확인할 수 있습니다.

3. collectd를 설치하십시오. 다음 명령을 실행하십시오.

    ```
	apt-get install collectd 
	```
	{: codeblock}


### 2단계: Monitoring 플러그인 설치
{: #plugin}

다음 단계를 완료하여 {{site.data.keyword.monitoringshort}} 플러그인을 설치하십시오.

1. 	루트 사용자로 로그인하십시오. 

    ```
    sudo -s
    ```
    {: codeblock}
	
2. {{site.data.keyword.monitoringshort}} 서비스 저장소를 추가하십시오. 다음 명령을 실행하십시오.

    ```
    wget -O - https://downloads.opvis.bluemix.net/client/IBM_Logmet_repo_install.sh | bash
    ```
   {: codeblock}
   
3. 플러그인을 설치하십시오. 다음 명령을 실행하십시오.

    ```
	apt-get install ibmcloud-monitoring
	```
	{: codeblock}


## Monitoring 플러그인 구성
{: #configure}

{{site.data.keyword.monitoringshort}} 플러그인을 구성하려면 다음 단계를 완료하십시오.
	
### 1단계: 사용자에게 IAM 정책 지정
{: #iam_policy}

메트릭을 도메인에 전송하려면 메트릭을 Monitoring 서비스에 전송할 수 있는 권한이 있는 IAM 역할을 사용자 ID에 부여해야 합니다.
 
* IBM Cloud에서 해당 사용자에 대한 IAM 정책을 지정하여 권한을 설정합니다. 
* *관리자*, *편집자*, *운영자* IAM 역할이 사용자가 메트릭을 전송하도록 허용합니다. 

사용자에게 IAM 정책을 지정하려면 다음 방법 중 하나를 선택하십시오.

* {{site.data.keyword.Bluemix_notm}} UI를 통해: 자세한 정보는 [{{site.data.keyword.Bluemix_notm}} UI를 통해 사용자에게 IAM 정책 지정 ](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-grant_permissions#assign_policy_ui).
* 명령행 사용: 자세한 정보는 [명령행을 사용하여 사용자에게 IAM 정책 지정](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-grant_permissions#assign_policy_commandline)을 참조하십시오.
 
### 2단계: API 키 가져오기
{: #api_key}
 
메트릭을 영역에 전송하려면 {{site.data.keyword.monitoringshort}} 서비스에 인증하기 위한 API 키를 가져와야 합니다.

API 키를 가져오는 방법에 대한 자세한 정보는 [API 키 가져오기](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_api_key#auth_api_key)를 참조하십시오.
	
{{site.data.keyword.Bluemix_notm}}에 로그인한 것과 동일한 터미널에서 토큰에 대한 APIKEY 변수를 설정하십시오.

예를 들어 다음과 같습니다.

```
export APIKEY="kjshdgf.....ldkdjdj"
```
{: screen}
	
### 3단계: 엔드포인트에 대한 정보
{: #endpoint}

메트릭을 전송할 {{site.data.keyword.monitoringshort}} 엔드포인트를 판별하려면 지역별 엔드포인트 목록과 [엔드포인트](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints)를 참조하고 메트릭을 전송하려는 지역에 대한 엔드포인트를 식별하십시오.

{{site.data.keyword.Bluemix_notm}}에 로그인한 터미널에서 **METRIC_ENDPOINT** 변수를 설정하십시오. 예를 들어 다음과 같습니다.

```
export METRIC_ENDPOINT="metrics.ng.bluemix.net"
```
{: screen}



### 4단계: 영역 도메인 ID에 대한 정보 가져오기 
{: #domain}

영역의 도메인 ID를 가져오려면 [영역 GUID 가져오기](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#space_guid)를 수행하십시오. 그런 다음, `s-SpaceID`와 같이 도메인 ID를 설정하십시오. 여기서 SpaceID는 영역의 GUID입니다.

{{site.data.keyword.Bluemix_notm}}에 로그인한 것과 동일한 터미널에서 SpaceID 변수를 설정하십시오.

```
export SpaceID="kjshdgf.....ldkdjdj"
```
{: screen}



### 5단계: 구성 스크립트 실행
{: #script}

다음 스크립트를 실행하여 메트릭을 영역에 전송하도록 {{site.data.keyword.monitoringshort}} 플러그인을 구성하십시오.

```
/opt/ibmcloud_monitoring/configure -e $METRIC_ENDPOINT -a $APIKEY -s s-$SpaceID
```
{: codeblock}


스크립트가 자동으로 기본 collectd.conf 파일에 **Include** 스탠자를 추가합니다.

```
<LoadPlugin IBMCloudMonitoring>
   FlushInterval 60
</LoadPlugin>
<Plugin IBMCloudMonitoring>
  <Endpoint "ng">
     Host "metrics.ng.bluemix.net"
     Port 9095
     ApiKey "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
     SkipInternalPrefixForStatsd false
     RateCounter false
     ScopeId "s-cedc73c5-6d55-4193-a9de-378620d6fab5"
  </Endpoint>
</Plugin>
```
{: screen}


### 6단계: collectd 디먼 다시 시작
{: #restart}

다음 단계를 완료하십시오.

1. 	루트 사용자로 로그인하십시오. 

    ```
    sudo -s
    ```
    {: codeblock}
	
2.  collectd를 다시 시작하십시오.

   collectd 디먼이 서비스로 추가된 경우 다음 명령을 실행하십시오.
	
	```
	service collectd restart
	```
	{: codeblock}

collectd에서 사용으로 설정되는 메트릭은 Grafana에서 분석에 사용 가능한 메트릭입니다.


