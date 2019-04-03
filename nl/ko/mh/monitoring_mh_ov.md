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



# {{site.data.keyword.messagehub}}
{: #monitoring_mh_ov}

{{site.data.keyword.Bluemix}}에서, {{site.data.keyword.messagehub}} 메트릭은 자동으로 수집됩니다. 토픽의 수신 및 발신 바이트 수가 수집됩니다. 체크포인트는 15분 간격입니다. Grafana를 사용하여 이러한 메트릭을 시각화할 수 있습니다. 
{:shortdesc}


**참고:** {{site.data.keyword.messagehub}} 메트릭은 미국 남부, 영국 및 시드니에서만 {{site.data.keyword.messagehub}} 표준 플랜으로 사용 가능합니다.  




## 메트릭 보기 및 분석
{: #view}

{{site.data.keyword.Bluemix_notm}}에서 {{site.data.keyword.messagehub}}의 성능을 모니터링하려면 Grafana를 사용하십시오. {{site.data.keyword.messagehub}}에서는 토픽의 성능을 보고 모니터링하는 데 사용할 수 있는 대시보드를 제공합니다.

{{site.data.keyword.monitoringlong}} 서비스는 오픈 소스 분석 및 시각화 플랫폼인 Grafana를 사용하여 메트릭을 모니터링하고, 검색하고, 분석하고, 다양한 그래프(예: 차트 및 표)로 시각화합니다. 

Grafana는 다음 방법 중 하나로 실행할 수 있습니다.

* {{site.data.keyword.Bluemix_notm}} 콘솔에 있는 {{site.data.keyword.messagehub}} 대시보드에서 **Grafana** 단추를 클릭할 수 있습니다.

    {{site.data.keyword.messagehub}}가 실행 중인 {{site.data.keyword.Bluemix_notm}}의 컨텍스트 영역 내에서 Grafana가 열립니다.
    
* 웹 브라우저에서 직접 Grafana를 실행할 수 있습니다.

    {{site.data.keyword.messagehub}} 인스턴스가 실행 중인 올바른 조직 및 영역에 있는지 확인하십시오.
    
    자세한 정보는 [웹 브라우저에서 Grafana 대시보드로 이동](/docs/services/cloud-monitoring/grafana/navigating_grafana.html#launch_grafana_from_browser)을 참조하십시오.
    

다음 정보를 고려하십시오.

* {{site.data.keyword.messagehub}} 인스턴스가 실행 중인 동일한 {{site.data.keyword.Bluemix_notm}} 지역에서 Grafana를 실행해야 합니다.
* 기본적으로 제공되는 Grafana 대시보드를 사용하여 {{site.data.keyword.messagehub}} 인스턴스의 모니터링을 시작하십시오.
* 임시 대시보드를 빌드하려면 사용자 정의 Grafana 대시보드를 작성하십시오. Grafana 대시보드에 하나 이상의 메트릭 조회를 정의하여 {{site.data.keyword.messagehub}} 인스턴스를 모니터링할 수 있습니다. 자세한 정보는 [Grafana에서 메트릭 조회 구성](/docs/services/cloud-monitoring/grafana/define_query.html#define_query)을 참조하십시오.
* 또한 조회에 대한 경보를 정의할 수 있습니다. 자세한 정보는 [경보 구성](/docs/services/cloud-monitoring/config_alerts_ov.html#config_alerts_ov)을 참조하십시오.


## Kafka 토픽에 대한 메트릭
{: #kafka_topic_metrics}

정의되는 각 Kafka 토픽의 경우 다음 메트릭이 수집됩니다.


<table>
  <caption>Kafka 토픽당 메트릭</caption>
  <tr>
    <th>메트릭</th>
    <th>설명</th>
  </tr>
  <tr>
    <td>BytesInPerSec</td>
    <td>Kafka 클라이언트 애플리케이션에 의해 토픽으로 전송된 바이트 비율입니다.</td>
  </tr>
  <tr>
    <td>BytesOutPerSec</td>
    <td>Kafka 클라이언트 애플리케이션에 의해 토픽으로부터 수신한 바이트 비율입니다.</td>
  </tr>
</table>



## Kafka 파티션에 대한 메트릭
{: #kafka_partition_metrics}

메시지를 이용하는 Cloud Storage 브릿지가 있는 각 Kafka 파티션의 경우 다음 메트릭이 수집됩니다.


<table>
  <caption>Kafka 파티션 메트릭</caption>
  <tr>
    <th>메트릭</th>
    <th>설명</th>
  </tr>
  <tr>
    <td>lastSeen</td>
    <td>Cloud Storage 브릿지에서 처리하는 마지막 Kafka 레코드에 대한 오프셋입니다.</td>
  </tr>
  <tr>
    <td>lastCommitted</td>
    <td>Cloud Storage 브릿지에서 처리하는 Kafka 레코드에 대한 커미트된 오프셋입니다.</td>
  </tr>
  <tr>
    <td>notParsedButProcessedMessages</td>
    <td>Kafka 토픽으로부터 Cloud Storage 브릿지 인스턴스가 수신하는 메시지의 수입니다. 브릿지에서 처리할 수 없는 올바른 JSON을 포함하는 메시지만 계산됩니다.</td>
  </tr>
  <tr>
    <td>notParsedIgnoredMessages</td>
    <td>Kafka 토픽으로부터 Cloud Storage 브릿지 인스턴스가 수신하는 메시지의 수입니다. 데이터가 올바른 JSON 문서가 아니므로 구문 분석할 수 없는 데이터를 포함하는 메시지만 계산됩니다.</td>
  </tr>
</table>




## 참조
{: #mhlinks}

* [메시지 허브 시작하기](/docs/services/EventStreams/index.html#getting_started)
* [모니터링 및 로깅](/docs/services/EventStreams/messagehub072.html#monitoring)

