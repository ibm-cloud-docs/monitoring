---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, regions, endpoints

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


# 지역 및 엔드포인트
{: #endpoints}

{{site.data.keyword.mon_full_notm}} 서비스에 대해 지원되는 지역 및 엔드포인트의 목록:
{:shortdesc}

## 지역
{: #endpoints_regions}

{{site.data.keyword.mon_full_notm}} 서비스는 다음 지역에서 사용 가능합니다.

| 지역                | 위치  | 
|-----------------------|-----------|
| `미국 남부`            |댈러스    | 
| `EU-DE`               |프랑크푸르트 | 
| `EU-GB`               |런던    | 
| `JP-TOK`              |도쿄    |
{: caption="표 1. 서비스 가능 지역의 목록" caption-side="top"} 

현재, **프랑크푸르트** 및 **EU GB**는 EU에서 관리되지 **않는** 지역입니다. 자세한 정보는 [EU 지원 사용 설정](/docs/account?topic=account-eu-hipaa-supported#bill_eusupported)을 참조하십시오.
{: important}


## Sysdig 콜렉터 엔드포인트
{: #endpoints_ingestion}

**Sysdig 콜렉터** 엔드포인트는 데이터 전송에 사용할 수 있는 수집 엔드포인트입니다.

다음 표에는 지역마다 사용 가능한 **Sysdig 콜렉터 엔드포인트**가 나열되어 있습니다.

| 지역        | 엔드포인트                                                  | 포트 |
|---------------|-----------------------------------------------------------|------|
| `미국 남부`    | `ingest.us-south.monitoring.cloud.ibm.com`                | TCP 6443 |
| `EU DE`       | `ingest.eu-de.monitoring.cloud.ibm.com`                   | TCP 6443 | 
| `EU GB`       | `ingest.eu-gb.monitoring.cloud.ibm.com`                   | TCP 6443 | 
| `JP TOK`      | `ingest.jp-tok.monitoring.cloud.ibm.com`                  | TCP 6443 | 
{: caption="표 2. 수집 엔드포인트의 목록" caption-side="top"} 



## Sysdig 엔드포인트
{: #endpoints_sysdig}

다음 표에는 지역마다 사용 가능한 **Sysdig 엔드포인트**가 나열되어 있습니다.

| 지역       | 엔드포인트                                                  | 포트            |
|--------------|-----------------------------------------------------------|-----------------|
| `미국 남부`   | `https://us-south.monitoring.cloud.ibm.com `               | HTTPS(TLS) 443 |  
| `EU DE`      | `https://eu-de.monitoring.cloud.ibm.com `                 | HTTPS(TLS) 443 |
| `EU GB`     | `https://eu-gb.monitoring.cloud.ibm.com `                 | HTTPS(TLS) 443 |
| `JP TOK`     | `https://jp-tok.monitoring.cloud.ibm.com`                 | HTTPS(TLS) 443 |
{: caption="표 3. Sysdig 엔드포인트의 목록" caption-side="top"} 


