---

copyright:
  years:  2018, 2024
lastupdated: "2024-02-29"

keywords:

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}


# Endpoints
{: #endpoints}

A list of supported public and private endpoints for the {{site.data.keyword.mon_full_notm}} service.
{: shortdesc}



## Web UI endpoints
{: #endpoints_monitoring}

To access the {{site.data.keyword.mon_short}} web UI, you might need to define a firewall rule in your host.
{: note}


The following table lists the endpoints that are available per region:

| Region      | Web UI endpoint                                  | Public IP addresses                                       |  Ports           |
|-------------|--------------------------------------------------|-----------------------------------------------------------|-----------------|
| Dallas (`US-South`)  | `https://us-south.monitoring.cloud.ibm.com`      | 169.60.151.174  \n 169.46.0.70  \n 169.48.214.70        | https (TLS) 443 |
| Frankfurt (`EU-DE`)     | `https://eu-de.monitoring.cloud.ibm.com`         | 149.81.77.78  \n 161.156.102.206  \n 159.122.102.38     | https (TLS) 443 |
| London (`EU-GB`)     | `https://eu-gb.monitoring.cloud.ibm.com`         | 158.175.98.206  \n 141.125.73.118  \n 159.122.210.174   | https (TLS) 443 |
| Madrid (`EU-ES`)     | `https://eu-es.monitoring.cloud.ibm.com`         |  13.120.68.187  \n  13.121.68.91  \n 13.122.68.140 | https (TLS) 443 |
| Osaka (`JP-OSA`)    | `https://jp-osa.monitoring.cloud.ibm.com`        | 163.68.67.98  \n 163.69.66.170  \n 163.73.67.180 | https (TLS) 443 |
| Sao Paulo (`BR-SAO`)    | `https://br-sao.monitoring.cloud.ibm.com`        | 163.107.66.98  \n 163.109.67.242  \n 169.57.141.43       | https (TLS) 443 |
| Sydney (`AU-SYD`)    | `https://au-syd.monitoring.cloud.ibm.com`        | 135.90.73.100  \n 130.198.80.155  \n 168.1.213.78
| Tokyo (`JP-TOK`)    | `https://jp-tok.monitoring.cloud.ibm.com`        | 165.192.84.14  \n 128.168.75.14  \n 169.56.51.238       | https (TLS) 443 |
| Toronto (`CA-TOR`)    | `https://ca-tor.monitoring.cloud.ibm.com`        | 163.74.69.186  \n 158.85.94.130  \n 163.75.65.237       | https (TLS) 443 |
| Washington (`US-East`)   | `https://us-east.monitoring.cloud.ibm.com`       | 169.60.112.74  \n 169.55.109.114  \n 169.62.3.82        | https (TLS) 443 |
   | https (TLS) 443 |
{: caption="Table 1. List of endpoints" caption-side="top"}




## REST API endpoints
{: #endpoints_rest_api}

To make API calls, you might need to define a firewall rule in your host.
{: note}

### Private REST API endpoints
{: #endpoints_rest_api_private}

The following table lists the *Private API endpoints* that are available per region:

| Region      | Private REST API endpoint       | Private IP addresses       |
|-------------|----------------------------------|----------------------------|
| Dallas (`US-South`)  | `private.us-south.monitoring.cloud.ibm.com/api`   | 166.9.228.45    \n 166.9.229.45    \n 166.9.230.44     |
| Frankfurt (`EU-DE`)     | `private.eu-de.monitoring.cloud.ibm.com/api`      | 166.9.248.88    \n 166.9.248.120    \n 166.9.248.152       |
| London (`EU-GB`)     | `private.eu-gb.monitoring.cloud.ibm.com/api`      | 166.9.244.29    \n 166.9.244.59                         |
| Madrid (`EU-ES`)     | `private.eu-es.monitoring.cloud.ibm.com/api`      | 166.9.226.17    \n 166.9.227.16     \n 166.9.225.16           |
| Osaka (`JP-OSA`)    | `private.jp-osa.monitoring.cloud.ibm.com/api`     | 166.9.247.44    \n 166.9.247.77    \n 166.9.247.109    |
| Sao Paulo (`BR-SAO`)  | `private.br-sao.monitoring.cloud.ibm.com/api`   | 166.9.246.77    \n 166.9.246.108    \n 166.9.246.133     |
| Sydney (`AU-SYD`)    | `private.au-syd.monitoring.cloud.ibm.com/api`     | 166.9.244.114    \n 166.9.244.144    \n 166.9.244.177        |
| Tokyo (`JP-TOK`)    | `private.jp-tok.monitoring.cloud.ibm.com/api`     | 166.9.249.112    \n 166.9.249.141    \n 166.9.249.177           |
| Toronto (`CA-TOR`)  | `private.ca-tor.monitoring.cloud.ibm.com/api`   | 166.9.247.153    \n 166.9.247.185    \n 166.9.247.205      |
| Washington (`US-East`)   | `private.us-east.monitoring.cloud.ibm.com/api`    | 166.9.231.240    \n 166.9.232.28    \n 166.9.233.17         |
{: caption="Table 2. Private REST API endpoints for the {{site.data.keyword.mon_full_notm}} service" caption-side="top"}





### Public REST API endpoints
{: #endpoints_rest_api_public}


| Region      | Public REST API endpoint                                      |
|-------------|---------------------------------------------------------------|
| Dallas (`US-South`)  | `https://us-south.monitoring.cloud.ibm.com/api`      |
| Frankfurt (`EU-DE`)     | `https://eu-de.monitoring.cloud.ibm.com/api`         |
| London (`EU-GB`)     | `https://eu-gb.monitoring.cloud.ibm.com/api`         |
| Madrid (`EU-ES`)     | `https://eu-es.monitoring.cloud.ibm.com/api`         |
| Osaka (`JP-OSA`)    | `https://jp-osa.monitoring.cloud.ibm.com/api`        |
| Sao Paulo (`BR-SAO`)    | `https://br-sao.monitoring.cloud.ibm.com/api`        |
| Sydney (`AU-SYD`)    | `https://au-syd.monitoring.cloud.ibm.com/api`        |
| Tokyo (`JP-TOK`)    | `https://jp-tok.monitoring.cloud.ibm.com/api`        |
| Toronto (`CA-TOR`)    | `https://ca-tor.monitoring.cloud.ibm.com/api`        |
| Washington (`US-East`)   | `https://us-east.monitoring.cloud.ibm.com/api`       |
{: caption="Table 3. Public REST API endpoints for the {{site.data.keyword.mon_full_notm}} service" caption-side="top"}




## Collector endpoints
{: #endpoints_ingestion}

Collector endpoints are ingestion endpoints that you can use to send data.


### Private Collector endpoints
{: #endpoints_ingestion_private}

To send metrics by using a private endpoint, you must [enable virtual routing and forwarding (VRF)](/docs/account?topic=account-vrf-service-endpoint) for your account.
{: note}

The following table lists the *Private Collector endpoints* that are available per region:

| Region      | Private ingestion endpoint       | Private IP addresses       | Monitoring  \n  agent ports   | Prometheus  \n  Remote Write  \n Ports|
|-------------|----------------------------------|----------------------------|-----------|---------|
| Dallas (`US-South`)  | `ingest.private.us-south.monitoring.cloud.ibm.com`   | 166.9.14.170  \n 166.9.48.41  \n 166.9.17.11    | TCP 6443  | TCP 443  |
| Frankfurt (`EU-DE`)     | `ingest.private.eu-de.monitoring.cloud.ibm.com`      | 166.9.32.51  \n 166.9.30.53  \n 166.9.28.71  | TCP 6443  | TCP 443  |
| London (`EU-GB`)     | `ingest.private.eu-gb.monitoring.cloud.ibm.com`      | 166.9.34.56  \n 166.9.36.71         |  TCP 6443 | TCP 443  |
| Madrid (`EU-ES`)     | `ingest.private.eu-es.monitoring.cloud.ibm.com`      | 166.9.96.31  \n 166.9.95.31  \n 166.9.94.31  |  TCP 6443 | TCP 443  |
| Osaka (`JP-OSA`)    | `ingest.private.jp-osa.monitoring.cloud.ibm.com`     | 166.9.72.14  \n 166.9.71.15  \n 166.9.70.14    | TCP 6443 |  TCP 443  |
| Sao Paulo (`BR-SAO`)  | `ingest.private.br-sao.monitoring.cloud.ibm.com`   | 166.9.84.19  \n 166.9.83.18  \n 166.9.82.19   | TCP 6443  |  TCP 443  |
| Sydney (`AU-SYD`)    | `ingest.private.au-syd.monitoring.cloud.ibm.com`     | 166.9.56.32  \n 166.9.52.27   \n 166.9.54.27    |  TCP 6443 |  TCP 443  |
| Tokyo (`JP-TOK`)    | `ingest.private.jp-tok.monitoring.cloud.ibm.com`     | 166.9.44.38  \n 166.9.40.35  \n 166.9.42.48      | TCP 6443  |  TCP 443  |
| Toronto (`CA-TOR`)  | `ingest.private.ca-tor.monitoring.cloud.ibm.com`   | 166.9.77.20  \n 166.9.76.23  \n 166.9.78.21    | TCP 6443  |  TCP 443  |
| Washington (`US-East`)   | `ingest.private.us-east.monitoring.cloud.ibm.com`    | 166.9.22.50  \n 166.9.24.43  \n 166.9.20.53       | TCP 6443  |  TCP 443  |
{: caption="Table 4. List of ingestion endpoints and private IP addresses to send data to the {{site.data.keyword.mon_full_notm}}" caption-side="top"}




### Public Collector endpoints
{: #endpoints_ingestion_public}

The following table lists the *Public Collector endpoints* that are available per region:

| Region      | Public ingestion endpoint      | Public IP addresses    | {{site.data.keyword.mon_short}} agent ports   | Prometheus Remote Write Ports|
|-------------|-------------------------------|-------------------------|----------|--------|
| Dallas (`US-South`)  | `ingest.us-south.monitoring.cloud.ibm.com`          | 169.60.151.174  \n 169.46.0.70  \n 169.48.214.70      | TCP 6443 | TCP 443  |
| Frankfurt (`EU-DE`)     | `ingest.eu-de.monitoring.cloud.ibm.com`             | 149.81.77.78  \n 161.156.102.206  \n 159.122.102.38   | TCP 6443 | TCP 443  |
| London (`EU-GB`)     | `ingest.eu-gb.monitoring.cloud.ibm.com`             | 158.175.98.206  \n 141.125.73.118  \n 159.122.210.174 | TCP 6443 | TCP 443  |
| Madrid (`EU-ES`)     | `ingest.eu-es.monitoring.cloud.ibm.com`             | 13.122.68.140  \n 13.120.68.187  \n  13.121.68.91 | TCP 6443 | TCP 443  |
| Sao Paulo (`BR-SAO`)    | `ingest.br-sao.monitoring.cloud.ibm.com`            | 163.107.66.98  \n 163.109.67.242  \n 169.57.141.43     | TCP 6443 | TCP 443  |
| Sydney (`AU-SYD`)    | `ingest.au-syd.monitoring.cloud.ibm.com`            | 135.90.73.100  \n 130.198.80.155  \n 168.1.213.78     | TCP 6443 | TCP 443  |
| Osaka (`JP-OSA`)    | `ingest.jp-osa.monitoring.cloud.ibm.com`            | 163.68.67.98  \n 163.69.66.170  \n 163.73.67.180 | TCP 6443 | TCP 443  |
| Toronto (`CA-TOR`)    | `ingest.ca-tor.monitoring.cloud.ibm.com`            | 163.74.69.186  \n 158.85.94.130  \n 163.75.65.237     | TCP 6443 | TCP 443  |
| Tokyo (`JP-TOK`)    | `ingest.jp-tok.monitoring.cloud.ibm.com`            | 165.192.84.14  \n 128.168.75.14  \n 169.56.51.238     | TCP 6443 | TCP 443  |
| Washington (`US-East`)   | `ingest.us-east.monitoring.cloud.ibm.com`           | 169.60.112.74  \n 169.55.109.114  \n 169.62.3.82      | TCP 6443 | TCP 443  |
{: caption="Table 5. List of ingestion endpoints and public IP addresses to send data to the {{site.data.keyword.mon_full_notm}}" caption-side="top"}



## Ingestion endpoints
{: #prometheus_remote_write_endpoints}

{{site.data.keyword.mon_full_notm}} has deprecated Prometheus client support of endpoints in the form `https://ingest.<region>` and `https://ingest.private.<region>` and replaced them with new endpoints. Customers need to migrate to use the new endpoints.
{: deprecated}

The following table lists the public {{site.data.keyword.mon_short}} ingestion endpoints that you can configure to collect metrics via Prometheus Remote Write:

| Region                | Endpoint                            |
|-----------------------|-------------------------------------|
| Dallas (`US-South`)            | `https://ingest.us-south.monitoring.cloud.ibm.com/prometheus/remote/write` [Deprecated]{: tag-deprecated}  \n `https://ingest.prws.us-south.monitoring.cloud.ibm.com/prometheus/remote/write` |
| Frankfurt (`EU-DE`)               | `https://ingest.eu-de.monitoring.cloud.ibm.com/prometheus/remote/write` [Deprecated]{: tag-deprecated}  \n `https://ingest.prws.eu-de.monitoring.cloud.ibm.com/prometheus/remote/write`    |
| London (`EU-GB`)               | `https://ingest.eu-gb.monitoring.cloud.ibm.com/prometheus/remote/write` [Deprecated]{: tag-deprecated}  \n `https://ingest.prws.eu-gb.monitoring.cloud.ibm.com/prometheus/remote/write`    |
| Madrid (`EU-ES`)               | `https://ingest.eu-es.monitoring.cloud.ibm.com/prometheus/remote/write` [Deprecated]{: tag-deprecated}  \n `https://ingest.prws.eu-es.monitoring.cloud.ibm.com/prometheus/remote/write`    |
| Osaka (`JP-OSA`)              | `https://ingest.jp-osa.monitoring.cloud.ibm.com/prometheus/remote/write` [Deprecated]{: tag-deprecated}  \n `https://ingest.prws.jp-osa.monitoring.cloud.ibm.com/prometheus/remote/write`   |
| Sao Paulo (`BR-SAO`)              | `https://ingest.br-sao.monitoring.cloud.ibm.com/prometheus/remote/write` [Deprecated]{: tag-deprecated}  \n `https://ingest.prws.br-sao.monitoring.cloud.ibm.com/prometheus/remote/write`   |
| Sydney (`AU-SYD`)              | `https://ingest.au-syd.monitoring.cloud.ibm.com/prometheus/remote/write` [Deprecated]{: tag-deprecated}  \n `https://ingest.prws.au-syd.monitoring.cloud.ibm.com/prometheus/remote/write`   |
| Tokyo (`JP-TOK`)              | `https://ingest.jp-tok.monitoring.cloud.ibm.com/prometheus/remote/write` [Deprecated]{: tag-deprecated}  \n `https://ingest.prws.jp-tok.monitoring.cloud.ibm.com/prometheus/remote/write`   |
| Toronto (`CA-TOR`)              | `https://ingest.ca-tor.monitoring.cloud.ibm.com/prometheus/remote/write` [Deprecated]{: tag-deprecated}  \n `https://ingest.prws.ca-tor.monitoring.cloud.ibm.com/prometheus/remote/write`   |
| Washington (`US-EAST`)             | `https://ingest.us-east.monitoring.cloud.ibm.com/prometheus/remote/write` [Deprecated]{: tag-deprecated}  \n `https://ingest.prws.us-east.monitoring.cloud.ibm.com/prometheus/remote/write`  |
{: caption="Table 6. Prometheus remote write public endpoints" caption-side="top"}

The following table lists the private {{site.data.keyword.mon_short}} ingestion endpoints that you can configure to collect metrics via Prometheus Remote Write:

| Region                | Endpoint                            |
|-----------------------|-------------------------------------|
| Dallas (`US-South`)            | `https://ingest.private.us-south.monitoring.cloud.ibm.com/prometheus/remote/write` [Deprecated]{: tag-deprecated}  \n `https://ingest.prws.private.us-south.monitoring.cloud.ibm.com/prometheus/remote/write` |
| Frankfurt (`EU-DE`)               | `https://ingest.private.eu-de.monitoring.cloud.ibm.com/prometheus/remote/write` [Deprecated]{: tag-deprecated}  \n `https://ingest.prws.private.eu-de.monitoring.cloud.ibm.com/prometheus/remote/write`  |
| London (`EU-GB`)               | `https://ingest.private.eu-gb.monitoring.cloud.ibm.com/prometheus/remote/write` [Deprecated]{: tag-deprecated}  \n `https://ingest.prws.private.eu-gb.monitoring.cloud.ibm.com/prometheus/remote/write`  |
| Madrid (`EU-ES`)               | `https://ingest.private.eu-es.monitoring.cloud.ibm.com/prometheus/remote/write` [Deprecated]{: tag-deprecated}  \n `https://ingest.prws.private.eu-es.monitoring.cloud.ibm.com/prometheus/remote/write`  |
| Osaka (`JP-OSA`)              | `https://ingest.private.jp-osa.monitoring.cloud.ibm.com/prometheus/remote/write` [Deprecated]{: tag-deprecated}  \n `https://ingest.prws.private.jp-osa.monitoring.cloud.ibm.com/prometheus/remote/write`  |
| Sao Paulo (`BR-SAO`)              |`https://ingest.private.br-sao.monitoring.cloud.ibm.com/prometheus/remote/write` [Deprecated]{: tag-deprecated}  \n `https://ingest.prws.private.br-sao.monitoring.cloud.ibm.com/prometheus/remote/write`  |
| Sydney (`AU-SYD`)              | `https://ingest.private.au-syd.monitoring.cloud.ibm.com/prometheus/remote/write` [Deprecated]{: tag-deprecated}  \n `https://ingest.prws.private.au-syd.monitoring.cloud.ibm.com/prometheus/remote/write` |
| Tokyo (`JP-TOK`)              | `https://ingest.private.jp-tok.monitoring.cloud.ibm.com/prometheus/remote/write` [Deprecated]{: tag-deprecated}  \n `https://ingest.prws.private.jp-tok.monitoring.cloud.ibm.com/prometheus/remote/write` |
| Toronto (`CA-TOR`)              | `https://ingest.private.ca-tor.monitoring.cloud.ibm.com/prometheus/remote/write` [Deprecated]{: tag-deprecated}  \n `https://ingest.prws.private.ca-tor.monitoring.cloud.ibm.com/prometheus/remote/write`  |
| Washington (`US-EAST`)             | `https://ingest.private.us-east.monitoring.cloud.ibm.com/prometheus/remote/write` [Deprecated]{: tag-deprecated}  \n `https://ingest.prws.private.us-east.monitoring.cloud.ibm.com/prometheus/remote/write` |
{: caption="Table 7. Prometheus remote write private endpoints" caption-side="top"}


## Subnets for webhook notifications from {{site.data.keyword.mon_full_notm}}
{: #endpoints_network_alert_subnets}

To receive alert notifications by using webhooks from the {{site.data.keyword.mon_full_notm}} service, you may need to define firewall rules for the subnets that are invoking your webhooks.
{: note}

| Region     | Alert Notification Source Subnets                                                                          |
|------------|------------------------------------------------------------------------------------------------------------|
| Dallas (`US-SOUTH`) | 150.239.180.0/25  \n 169.46.0.64/29  \n 169.46.39.48/28  \n 169.46.58.24/29  \n 169.47.115.192/28  \n 169.47.71.24/29  \n 169.48.214.64/29  \n 169.48.235.16/28  \n 169.60.151.168/29  \n 169.62.221.32/28  \n 174.36.68.96/27  \n 50.22.148.64/26  \n 52.116.222.192/27  \n 52.117.187.192/27  \n 52.118.158.0/25  \n 52.118.7.64/26  \n 67.228.207.64/26  \n 67.228.219.0/25 |
| Frankfurt (`EU-DE`)    | 149.81.151.128/27  \n 149.81.201.192/26  \n 149.81.77.72/29  \n 149.81.99.192/28  \n 158.177.44.192/26  \n 159.122.102.32/29  \n 161.156.1.224/27  \n 161.156.102.200/29  \n 161.156.69.144/28  \n 161.156.77.64/26  \n 169.50.36.64/27  \n 169.50.9.0/28    |
| London (`EU-GB`)    | 141.125.136.32/27  \n 141.125.73.112/29  \n 141.125.73.80/28  \n 158.175.124.224/27  \n 158.175.98.200/29  \n 159.122.210.168/29  \n 159.8.144.168/29  \n 159.8.149.208/28  \n 159.8.162.0/26  \n 161.156.209.192/26  \n 5.10.120.32/27  |
| Madrid (`EU-ES`) | 13.120.68.192/28  \n 13.120.68.224/27  \n 13.121.68.96/28  \n 13.122.68.160/28  |
| Osaka (`JP-OSA`)   | 163.68.67.128/28  \n 163.68.67.96/29  \n 163.68.79.32/27  \n 163.69.66.168/29  \n 163.69.67.112/28  \n 163.69.70.64/27  \n 163.73.67.176/29  \n 163.73.67.192/28  \n 163.73.69.96/27  |
| Sao Paulo (`BR-SAO`) | 163.107.66.96/29  \n 163.107.68.128/28  \n 163.107.71.32/27  \n 163.109.67.240/29  \n 163.109.73.128/27  \n 169.57.141.40/29  \n 169.57.186.0/27  \n 169.57.195.0/28 |
| Sydney (`AU-SYD`)   | 130.198.66.144/28  \n 130.198.80.152/29  \n 135.90.73.96/29  \n 135.90.78.192/28  \n 135.90.94.96/27  \n 168.1.115.192/27  \n 168.1.213.32/27  \n 168.1.213.72/29  \n 168.1.41.96/28  |
| Tokyo (`JP-TOK`)   | 128.168.75.32/28  \n 128.168.75.8/29  \n 128.168.98.0/27  \n 161.202.255.64/27  \n 165.192.84.8/29  \n 165.192.97.96/27  \n 169.56.11.208/28  \n 169.56.51.232/29  |
| Toronto (`CA-TOR`)   | 158.85.78.224/27  \n 158.85.94.128/29  \n 163.74.67.192/28  \n 163.74.69.184/29  \n 163.74.71.96/27  \n 163.75.65.232/29  \n 163.75.72.192/27  \n 169.55.129.208/28  |
| Washington (`US-EAST`)  | 169.47.20.160/27  \n 169.55.109.112/29  \n 169.55.122.192/28  \n 169.59.131.160/27  \n 169.59.146.192/26  \n 169.60.112.72/29  \n 169.60.82.240/28  \n 169.62.28.160/28  \n 169.62.3.80/29  \n 169.62.46.192/27  \n 52.116.95.64/26  \n 52.117.71.128/26  |
{: caption="Table 8. Source Subnets for Webhook notifications from {{site.data.keyword.mon_full_notm}}" caption-side="top"}
