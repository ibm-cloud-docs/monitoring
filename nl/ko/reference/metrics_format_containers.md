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

{{site.data.keyword.containershort_notm}} 서비스를 모니터링하기 위해 Grafana에서 정의하는 조회는 다음 패턴을 따라야 합니다. 
{:shortdesc}



## 컨테이너에 대해 수집된 CPU 메트릭의 조회 형식
{: #cpu_containers}

{{site.data.keyword.containershort_notm}} 서비스에서 실행되는 컨테이너에 대한 CPU 메트릭을 모니터링하기 위해 Grafana에서 정의하는 조회의 형식은 다음과 같이 설명됩니다. 

```
{Source}.{Cloud Type}.{Service Name}.{Region}.{Cluster Name}.{Namespace}.{Metric Source}.{Pod Name}.{Container Name}.{Metric Type}.{Metric Subtype}.[Functions]
```
{: codeblock}  

여기서,

<table>
  <caption>컨테이너에 대한 CPU 메트릭을 정의하기 위한 필수 필드 </caption>
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
	  <td>컨테이너가 실행 중인 지역을 정의합니다.</td>
	  <td>미국 남부 지역의 경우 값은 *us-south*입니다. <br>영국 지역의 경우 값은 *united-kingdom*입니다.  <br>독일의 경우 값은 *frankfurt*입니다. <br>시드니의 경우 값은 *sydney*입니다. </td>
  </tr>
  <tr>
    <td>Cluster Name</td>
	  <td>모니터링할 클러스터의 이름입니다.</td>
	  <td></td>
  </tr>
  <tr>
    <td>Metric Source</td>
	  <td>데이터의 소스입니다.</td>
	  <td>*container* </td>
  </tr>
  <tr>
    <td>Namespace</td>
	<td>컨테이너가 Kubernetes 클러스터에서 배치되는 네임스페이스입니다.</td>
	<td></td>
  </tr>
   <tr>
    <td>Pod Name</td>
	<td>팟(Pod)의 이름입니다.</td>
	<td></td>
  </tr>
  <tr>
    <td>Container Name</td>
	<td>컨테이너의 이름입니다.</td>
	<td></td>
  </tr>
  <tr>
    <td>Metric Type</td>
	  <td>메트릭의 유형입니다.</td>
	  <td>*CPU*</td>
  </tr>
  <tr>
    <td>Metric Subtype</td>
	  <td>표시할 메트릭입니다.</td>
	  <td>*usage*, *num-cores*, *usage-pct*, *usage-pct-container-requested*</td>
  </tr>
  <tr>
    <td>Functions</td>
    <td>패널에서 컨테이너 메트릭을 시각화하기 위해 선택할 수 있는 조회 함수입니다. </td>
    <td>[함수 ![(외부 링크 아이콘)](../../../icons/launch-glyph.svg "외부 링크 아이콘")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
   </tr>
</table>

예를 들어, 미국 남부 지역의 Kubernetes 클러스터에서 실행 중인 컨테이너에 대한 CPU 사용률을 모니터링하기 위한 조회는 다음과 같이 정의됩니다.

```
ibmcloud.public.containers-kubernetes.us-south.myCluster.container.default.myPod.myContainer-1775968925-kfwfk.cpu.usage
```
{: screen}



## 작업자에 대해 수집된 로드 메트릭의 조회 형식
{: #load_workers}

{{site.data.keyword.containershort_notm}} 서비스에서 실행되는 작업자에 대한 로드 메트릭을 모니터링하기 위해 Grafana에서 정의하는 조회의 형식은 다음과 같이 설명됩니다. 

```
{Source}.{Cloud Type}.{Service Name}.{Region}.{Cluster Name}.{Metric Source}.{Worker Name}.{Metric Type}.{Metric Subtype}.[Functions]
```
{: codeblock}  

여기서,

<table>
  <caption>작업자에 대한 로드 메트릭을 정의하기 위한 필수 필드 </caption>
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
	  <td>컨테이너가 실행 중인 지역을 정의합니다.</td>
	  <td>미국 남부 지역의 경우 값은 *us-south*입니다. <br>영국 지역의 경우 값은 *united-kingdom*입니다.  <br>독일의 경우 값은 *frankfurt*입니다. <br>시드니의 경우 값은 *sydney*입니다. </td>
  </tr>
  <tr>
    <td>Cluster Name</td>
	<td>모니터링할 클러스터의 이름입니다.</td>
	<td></td>
  </tr>
  <tr>
    <td>Metric Source</td>
	<td>데이터의 소스입니다.</td>
	<td>*worker* </td>
  </tr>
   <tr>
    <td>Worker Name</td>
	<td>작업자의 이름입니다.</td>
	<td></td>
  </tr>
  <tr>
    <td>Metric Type</td>
	<td>메트릭의 유형입니다.</td>
	<td>*load*</td>
  </tr>
  <tr>
    <td>Metric Subtype</td>
	  <td>표시할 메트릭입니다.</td>
	  <td>*avg-1*, *avg-5*, *avg-15*</td>
  </tr>
  <tr>
    <td>Functions</td>
    <td>패널에서 컨테이너 메트릭을 시각화하기 위해 선택할 수 있는 조회 함수입니다. </td>
    <td>[함수 ![(외부 링크 아이콘)](../../../icons/launch-glyph.svg "외부 링크 아이콘")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
   </tr>
</table>

예를 들어, 미국 남부 지역의 Kubernetes 클러스터에서 실행 중인 작업자에 대한 CPU 사용률을 모니터링하기 위한 조회는 다음과 같이 정의됩니다.

```
ibmcloud.public.containers-kubernetes.us-south.myCluster.worker.MyWorker.load.avg-1
```
{: screen}


## 컨테이너에 대해 수집된 메모리 메트릭의 조회 형식
{: #mem_containers}

{{site.data.keyword.containershort_notm}} 서비스에서 실행되는 컨테이너에 대한 메모리 메트릭을 모니터링하기 위해 Grafana에서 정의하는 조회의 형식은 다음과 같이 설명됩니다. 

```
{Source}.{Cloud Type}.{Service Name}.{Region}.{Cluster Name}.{Namespace}.{Metric Source}.{Pod Name}.{Container Name}.{Metric Type}.{Metric Subtype}.[Functions]
```
{: codeblock}  

여기서,

<table>
  <caption>컨테이너에 대한 메모리 메트릭을 정의하기 위한 필수 필드</caption>
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
	  <td>컨테이너가 실행 중인 지역을 정의합니다.</td>
	  <td>미국 남부 지역의 경우 값은 *us-south*입니다. <br>영국 지역의 경우 값은 *united-kingdom*입니다.  <br>독일의 경우 값은 *frankfurt*입니다. <br>시드니의 경우 값은 *sydney*입니다. </td>
  </tr>
  <tr>
    <td>Cluster Name</td>
	<td>모니터링할 클러스터의 이름입니다.</td>
	<td></td>
  </tr>
  <tr>
    <td>Metric Source</td>
	<td>데이터의 소스입니다.</td>
	<td>*container* </td>
  </tr>
  <tr>
    <td>Namespace</td>
	<td>컨테이너가 Kubernetes 클러스터에서 배치되는 네임스페이스입니다.</td>
	<td></td>
  </tr>
   <tr>
    <td>Pod Name</td>
	<td>팟(Pod)의 이름입니다.</td>
	<td></td>
  </tr>
  <tr>
    <td>Container Name</td>
	  <td>컨테이너의 이름입니다.</td>
	  <td></td>
  </tr>
  <tr>
    <td>Metric Type</td>
  	<td>메트릭의 유형입니다.</td>
  	<td>*memory*</td>
  </tr>
  <tr>
    <td>Metric Subtype</td>
	  <td>표시할 메트릭입니다.</td>
	  <td>*limit*, *current*, *usage-pct*입니다.</td>
  </tr>
  <tr>
    <td>Functions</td>
    <td>패널에서 컨테이너 메트릭을 시각화하기 위해 선택할 수 있는 조회 함수입니다. </td>
    <td>[함수 ![(외부 링크 아이콘)](../../../icons/launch-glyph.svg "외부 링크 아이콘")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
   </tr>
</table>

예를 들어, 미국 남부 지역의 Kubernetes 클러스터에서 실행 중인 컨테이너에 대한 메모리 사용률을 모니터링하기 위한 조회는 다음과 같이 정의됩니다.

```
ibmcloud.public.containers-kubernetes.us-south.myCluster.container.default.myPod.myContainer-1775968925-kfwfk.memory.usage
```
{: screen}
