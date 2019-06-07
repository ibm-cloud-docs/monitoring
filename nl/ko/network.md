---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, network traffic, firewall

subcollection: Sysdig

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

 
# 사용자 정의 방화벽 구성에 대한 네트워크 트래픽 관리
{: #network}

추가 방화벽이 설정되어 있거나 {{site.data.keyword.cloud_notm}} 인프라에서 방화벽 설정을 사용자 정의하는 경우 {{site.data.keyword.mon_full_notm}} 서비스로의 발신 네트워크 트래픽을 허용해야 합니다.
{:shortdesc}


## 수집 엔드포인트
{: #network_send}

메트릭 데이터를 {{site.data.keyword.mon_full_notm}} 서비스로 전송하려면 호스트에서 다음 방화벽 규칙을 정의해야 합니다.

| 지역      | 수집 엔드포인트                                | 공인 IP 주소                                     | 포트    |
|-------------|---------------------------------------------------|---------------------------------------------------------|----------|
| `미국 남부`  | ingest.us-south.monitoring.cloud.ibm.com          | 169.60.151.174 </br>169.46.0.70 </br>169.48.214.70      | TCP 6443 | 
| `EU DE`     | ingest.eu-de.monitoring.cloud.ibm.com             | 149.81.77.78 </br>161.156.102.206 </br>159.122.102.38   | TCP 6443 | 
| `EU GB`     | ingest.eu-gb.monitoring.cloud.ibm.com             | 158.175.98.206 </br>141.125.73.118 </br>159.122.210.174 | TCP 6443 | 
| `JP TOK`    | ingest.jp-tok.monitoring.cloud.ibm.com            | 165.192.84.14 </br>128.168.75.14 </br>169.56.51.238     | TCP 6443 | 
{: caption="표 1. {{site.data.keyword.mon_full_notm}}에 데이터를 전송하기 위한 IP 주소" caption-side="top"}


## 웹 UI 엔드포인트
{: #network_ui}

{{site.data.keyword.mon_full_notm}} 웹 UI에 액세스하려면 호스트에서 다음 방화벽 규칙을 정의해야 합니다.

| 지역      | 웹 UI 엔드포인트                                   | 공인 IP 주소                                       | 포트   |
|-------------|---------------------------------------------------|-----------------------------------------------------------|---------|
| `미국 남부`  | us-south.monitoring.cloud.ibm.com                 | 169.60.151.174 </br>169.46.0.70 </br>169.48.214.70        | https (TLS) 443 | 
| `EU DE`     | eu-de.monitoring.cloud.ibm.com                    | 149.81.77.78 </br>161.156.102.206 </br>159.122.102.38     | https (TLS) 443 | 
| `EU GB`     | eu-gb.monitoring.cloud.ibm.com                    | 158.175.98.206 </br>141.125.73.118 </br>159.122.210.174   | https (TLS) 443 | 
| `JP TOK`    | ingest.jp-tok.monitoring.cloud.ibm.com            | 165.192.84.14 </br>128.168.75.14 </br>169.56.51.238       | https (TLS) 443 |
{: caption="표 2. {{site.data.keyword.mon_full_notm}} 웹 UI에 액세스하기 위한 IP 주소" caption-side="top"}


