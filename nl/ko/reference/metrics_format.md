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


# 일반 형식
{: #metrics_format}

{{site.data.keyword.Bluemix}} 서비스를 모니터링하기 위해 Grafana에서 정의하는 조회는 다음 형식을 준수해야 합니다. 
{:shortdesc}

```
{Source}.{Cloud Type}.{Service Name}.{Region}.[service fields].{Metric type}.{Metric Subtype}.[Functions]
```
{: codeblock}

여기서, [service fields]는 서비스 또는 CF 앱의 메트릭 조회의 특정 필드를 나타냅니다. 

<table>
  <caption>조회의 공통 필드</caption>
  <tr>
    <th>필드</th>
	<th>설명</th>
	<th>값</th>
  </tr>
  <tr>
    <td>Source</td>
	<td>예약된 이름입니다. 이 계층 구조 아래의 메트릭은 {{site.data.keyword.Bluemix_notm}} 서비스에서 발생합니다.</td>
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
	  <td>{{site.data.keyword.containershort}}의 경우 값은 *containers-kubernetes*입니다.</td>
  </tr>
  <tr>
    <td>Region</td>
	  <td>컨테이너가 실행 중인 지역을 정의합니다.</td>
	  <td>미국 남부 지역의 경우 값은 *us-south*입니다. <br>영국 지역의 경우 값은 *united-kingdom*입니다.  <br>독일의 경우 값은 *frankfurt*입니다. <br>시드니의 경우 값은 *sydney*입니다. </td>
  </tr>
  <tr>
    <td>Metric Type</td>
	<td>메트릭의 유형입니다.</td>
	<td>*cpu* <br>*load* <br>*memory*</td>
  </tr>
  <tr>
    <td>Metric Subtype</td>
	<td>메트릭의 하위 유형입니다.</td>
	<td>예: *usage*, *num-cores*, *usage-pct*, *usage-pct-container-requested*</td>
  </tr>
  <tr>
    <td>Functions</td>
    <td>패널에서 컨테이너 메트릭을 시각화하기 위해 선택할 수 있는 조회 함수입니다. </td>
    <td>[함수 ![(외부 링크 아이콘)](../../../icons/launch-glyph.svg "외부 링크 아이콘")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
   </tr>
</table>




