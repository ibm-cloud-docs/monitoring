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


# CF 앱
{: #cfapps_metrics_format}

{{site.data.keyword.Bluemix}} 퍼블릭에서 실행되는 Cloud Foundry 애플리케이션을 모니터링하기 위해 Grafana에서 정의하는 조회는 다음 형식을 준수해야 합니다. 
{:shortdesc}

```
{Source}.{Cloud Type}.{Service Name}.{Region}.{CFapp Name}.{CFapp Index}.{CFapp container}.{Metric Type}.{Metric Subtype}.[Functions]
```
{: codeblock}

여기서,

<table>
  <caption>조회의 공통 필드</caption>
  <tr>
    <th>필드</th>
	<th>설명</th>
	<th>값</th>
  </tr>
  <tr>
    <td>Source</td>
	<td>예약된 이름입니다. 이 계층 구조 아래의 메트릭은 {{site.data.keyword.Bluemix_notm}} 애플리케이션 및 서비스에서 발생합니다.</td>
	<td>*ibmcloud*</td>
  </tr>
  <tr>
    <td>Cloud Type</td>
	<td>클라우드 유형을 표시합니다. </td>
	<td>{{site.data.keyword.Bluemix_notm}} 퍼블릭 클라우드의 경우, 값이 *public*입니다.</td>
  </tr>
  <tr>
    <td>Service Name</td>
	<td>{{site.data.keyword.Bluemix_notm}}의 서비스 이름을 정의합니다.</td>
	<td>CF 앱의 경우, 값이 *cloud-foundry*입니다.</td>
  </tr>
  <tr>
    <td>Region</td>
	<td>CF 앱 인스턴스가 실행 중인 지역을 정의합니다.</td>
	<td>미국 남부 지역의 경우 값은 *us-south*입니다. <br>영국 지역의 경우 값은 *eu-gb*입니다.  <br>독일의 경우 값은 *eu-de*입니다. <br>시드니의 경우 값은 *au-syd*입니다. </td>
  </tr>
  <tr>
    <td>CFapp Name</td>
	<td>CF 애플리케이션의 이름입니다.</td>
	<td></td>
  </tr>
  <tr>
    <td>CFapp Index</td>
	  <td>CF 애플리케이션 인스턴스의 인덱스입니다.</td>
	  <td>예: *0* </br>하나의 인스턴스가 있는 CF 앱이 있는 경우, 인덱스 0만 있습니다. 예를 들어, CF 앱을 10개의 인스턴스로 스케일링하는 경우, 인덱스 값으로 0에서 9까지 사용할 수 있습니다.</td>
  </tr>
  <tr>
    <td>CFapp container</td>
	  <td>고정 값입니다.</td>
	  <td>*container*</td>
  </tr>
  <tr>
    <td>Metric Type</td>
	  <td>메트릭의 유형입니다. 디스크, 메모리 및 CPU는 자동으로 수집되는 메트릭 시리즈입니다.</td>
	  <td>*CPU*</td>
  </tr>
  <tr>
    <td>Metric Subtype</td>
	  <td>표시할 메트릭입니다. </br>[CPU 메트릭](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#cpu_metrics) </br>[디스크 메트릭](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#disk_metrics) </br>[메모리 메트릭](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#mem_metrics)</td>
	  <td></td>
  </tr>
  <tr>
    <td>Functions</td>
    <td>패널에서 컨테이너 메트릭을 시각화하기 위해 선택할 수 있는 조회 함수입니다. </td>
    <td>[함수 ![(외부 링크 아이콘)](../../../icons/launch-glyph.svg "외부 링크 아이콘")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
   </tr>
</table>




