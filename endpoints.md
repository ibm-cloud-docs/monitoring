---

copyright:
  years:  2018, 2025
lastupdated: "2025-08-05"

keywords:

subcollection: monitoring

---

{{site.data.keyword.attribute-definition-list}}


# Endpoints
{: #endpoints}

A list of supported public and private endpoints for the {{site.data.keyword.mon_full_notm}} service. Each endpoint section describes a different kind of endpoint connection, and the IP addresses associated with that endpoint by [IBM Cloud multizone regions](/docs/overview?topic=overview-locations).
{: shortdesc}


## Firewall infrastructure filtering
{: #endpoints_firewall_infra_filtering}

To access the {{site.data.keyword.mon_short}} endpoints on this page, you might need to define a firewall rule in your infrastructure. Some users maintain a list of trusted IP addresses or domains that are permitted to access a network or service. IP allowlisting restricts access to specific IP addresses, while domain allowlisting restricts access to specific domains or subdomains. This helps improve security by only allowing traffic from known safe sources and blocking others. If your infrastructure layout uses this filtering, you will need to use the IP and domain address information provided to set up those filters properly.


## Endpoint IP address changes
{: #endpoints_ipaddress_changes}

These IP addresses are static, but do change occasionally as infrastructure service hosting adjustments are made. IP address changes are taking place in 2025. These changes need to be added to infrastructure allowlists that users have in place to avoid service disruptions. `(*)` in the endpoint section tables indicate new IP addresses for endpoint connections. These new IP addresses are already available and they can all be added to any allowlists you have for all the MZRs in your infrastructure. The existing IP addresses listed for each MZR will be removed on the dates in the schedule table. Be sure to keep the current IP addresses in the allowlist, until the noted date, after which they can be removed.

See the [Endpoint IP address change schedule](#endpoints_ipaddress_change_schedule) for the roll out plan.



## Web UI endpoints
{: #endpoints_monitoring}

The following table lists the endpoints that are available per region:

Ports for every MZR:
- https (TLS): 443

| Region      | Web UI endpoint                                  | Public IP addresses                                       | 
|-------------|--------------------------------------------------|-----------------------------------------------------------|
| Dallas (`US-South`)  | `https://us-south.monitoring.cloud.ibm.com`      | 169.60.151.174  \n 169.46.0.70  \n 169.48.214.70  		\n 52.118.209.119 `(*)`  \n 67.18.94.56 `(*)`  		\n 52.116.135.250     `(*)`      |
| Frankfurt (`EU-DE`)     | `https://eu-de.monitoring.cloud.ibm.com`         | 149.81.77.78  \n 161.156.102.206  \n 159.122.102.38  \n 158.177.2.4 `(*)`  \n 161.156.87.239 `(*)`  		\n 149.81.238.82  `(*)`   |
| London (`EU-GB`)     | `https://eu-gb.monitoring.cloud.ibm.com`         | 158.175.98.206  \n 141.125.73.118  \n 159.122.210.174    \n 141.125.105.98 `(*)`  \n 161.156.203.133 `(*)`  	\n 158.176.179.72  `(*)` |
| Madrid (`EU-ES`)     | `https://eu-es.monitoring.cloud.ibm.com`         |  13.120.68.187  \n  13.121.68.91  \n 13.122.68.140  	 \n 13.121.91.87 `(*)`  \n 13.122.87.104 `(*)`  		\n 13.120.91.152   `(*)` |
| Montreal (`CA-MON`)    | `https://ca-mon.monitoring.cloud.ibm.com`        | 64.5.49.125  \n 64.5.42.185  \n 64.5.47.9 |
| Osaka (`JP-OSA`)    | `https://jp-osa.monitoring.cloud.ibm.com`        | 163.68.67.98  \n 163.69.66.170  \n 163.73.67.180  		 \n 163.68.83.196 `(*)`  \n 163.73.82.218 `(*)`  		\n 163.69.86.15   `(*)` |
| Sao Paulo (`BR-SAO`)    | `https://br-sao.monitoring.cloud.ibm.com`        | 163.107.66.98  \n 163.109.67.242  \n 169.57.141.43    \n 13.116.92.185 `(*)`  \n 163.107.92.212 `(*)`  	\n 163.109.84.195  `(*)`     |
| Sydney (`AU-SYD`)    | `https://au-syd.monitoring.cloud.ibm.com`        | 135.90.73.100  \n 130.198.80.155  \n 168.1.213.78  		 \n 130.198.10.95 `(*)`  \n 135.90.130.246 `(*)`  	\n 159.23.97.190   `(*)`     |
| Toronto (`CA-TOR`)    | `https://ca-tor.monitoring.cloud.ibm.com`        | 163.74.69.186  \n 158.85.94.130  \n 163.75.65.237  	 \n 163.66.86.89 `(*)`  \n 163.75.81.213 `(*)`  		\n 163.74.95.149  `(*)`     |
| Tokyo (`JP-TOK`)    | `https://jp-tok.monitoring.cloud.ibm.com`        | 165.192.84.14  \n 128.168.75.14  \n 169.56.51.238  		 \n 162.133.138.54 `(*)`  \n 128.168.143.56 `(*)`  	\n 165.192.128.220   `(*)`     |
| Washington (`US-East`)   | `https://us-east.monitoring.cloud.ibm.com`       | 169.60.112.74  \n 169.55.109.114  \n 169.62.3.82  	 \n 169.62.20.11 `(*)`  \n 169.63.183.86 `(*)`  		\n 150.239.110.137  `(*)`      |
{: caption="List of endpoints" caption-side="top"}




## REST API endpoints
{: #endpoints_rest_api}

### Private REST API endpoints
{: #endpoints_rest_api_private}

The following table lists the *Private API endpoints* that are available per region:

| Region      | Private REST API endpoint       | Private IP addresses       |
|-------------|----------------------------------|----------------------------|
| Dallas (`US-South`)  | `private.us-south.monitoring.cloud.ibm.com/api`   | 166.9.228.45    \n 166.9.229.45    \n 166.9.230.44  \n 166.9.228.235  `(*)`  \n 166.9.229.31 `(*)`  \n 166.9.251.30  `(*)`    |
| Frankfurt (`EU-DE`)     | `private.eu-de.monitoring.cloud.ibm.com/api`      | 166.9.248.88    \n 166.9.248.120    \n 166.9.248.152  \n 166.9.209.205 `(*)`  \n 166.9.209.227 `(*)`  \n 166.9.210.13 `(*)`       |
| London (`EU-GB`)     | `private.eu-gb.monitoring.cloud.ibm.com/api`      | 166.9.244.29    \n 166.9.244.59  \n 166.9.245.189 `(*)`  \n 166.9.245.221 `(*)`  \n 166.9.245.253 `(*)`    |
| Madrid (`EU-ES`)     | `private.eu-es.monitoring.cloud.ibm.com/api`      | 166.9.226.17    \n 166.9.227.16     \n 166.9.225.16  \n 166.9.226.56 `(*)`  \n 166.9.227.143 `(*)`  \n 166.9.225.35 `(*)`           |
| Montreal (`CA-MON`)  | `private.ca-mon.monitoring.cloud.ibm.com/api`   | 166.9.232.56  \n 166.9.233.54  \n 166.9.231.34 |
| Osaka (`JP-OSA`)    | `private.jp-osa.monitoring.cloud.ibm.com/api`     | 166.9.247.44    \n 166.9.247.77    \n 166.9.247.109  \n 166.9.247.59 `(*)`  \n 166.9.247.89 `(*)`  \n 166.9.247.123 `(*)`    |
| Sao Paulo (`BR-SAO`)  | `private.br-sao.monitoring.cloud.ibm.com/api`   | 166.9.246.77    \n 166.9.246.108    \n 166.9.246.133  \n 166.9.246.87 `(*)`  \n 166.9.246.120 `(*)`  \n 166.9.246.144 `(*)`     |
| Sydney (`AU-SYD`)    | `private.au-syd.monitoring.cloud.ibm.com/api`     | 166.9.244.114    \n 166.9.244.144    \n 166.9.244.177  \n 166.9.244.121 `(*)`  \n 166.9.244.153 `(*)`  \n 166.9.244.185 `(*)`        |
| Tokyo (`JP-TOK`)    | `private.jp-tok.monitoring.cloud.ibm.com/api`     | 166.9.249.112    \n 166.9.249.141    \n 166.9.249.177  \n 166.9.212.4 `(*)`  \n 166.9.214.5 `(*)`  \n 166.9.216.14 `(*)`      |
| Toronto (`CA-TOR`)  | `private.ca-tor.monitoring.cloud.ibm.com/api`   | 166.9.247.153    \n 166.9.247.185    \n 166.9.247.205  \n 166.9.209.13 `(*)`  \n 166.9.209.42 `(*)`  \n 166.9.209.72 `(*)`      |
| Washington (`US-East`)   | `private.us-east.monitoring.cloud.ibm.com/api`    | 166.9.231.240    \n 166.9.232.28    \n 166.9.233.17 \n 166.9.231.19 `(*)`  \n 166.9.232.40 `(*)`  \n 166.9.233.36 `(*)`      |
{: caption="Private REST API endpoints for the {{site.data.keyword.mon_full_notm}} service" caption-side="top"}



### Public REST API endpoints
{: #endpoints_rest_api_public}


| Region      | Public REST API endpoint                                      |
|-------------|---------------------------------------------------------------|
| Dallas (`US-South`)  | `https://us-south.monitoring.cloud.ibm.com/api`      |
| Frankfurt (`EU-DE`)     | `https://eu-de.monitoring.cloud.ibm.com/api`         |
| London (`EU-GB`)     | `https://eu-gb.monitoring.cloud.ibm.com/api`         |
| Madrid (`EU-ES`)     | `https://eu-es.monitoring.cloud.ibm.com/api`         |
| Montreal (`CA-MON`)    | `https://ca-mon.monitoring.cloud.ibm.com/api`        |
| Osaka (`JP-OSA`)    | `https://jp-osa.monitoring.cloud.ibm.com/api`        |
| Sao Paulo (`BR-SAO`)    | `https://br-sao.monitoring.cloud.ibm.com/api`        |
| Sydney (`AU-SYD`)    | `https://au-syd.monitoring.cloud.ibm.com/api`        |
| Tokyo (`JP-TOK`)    | `https://jp-tok.monitoring.cloud.ibm.com/api`        |
| Toronto (`CA-TOR`)    | `https://ca-tor.monitoring.cloud.ibm.com/api`        |
| Washington (`US-East`)   | `https://us-east.monitoring.cloud.ibm.com/api`       |
{: caption="Public REST API endpoints for the {{site.data.keyword.mon_full_notm}} service" caption-side="top"}




## Collector endpoints
{: #endpoints_ingestion}

Collector endpoints are ingestion endpoints that you can use to send data.


### Private Collector endpoints
{: #endpoints_ingestion_private}

To send metrics by using a private endpoint, you must [enable virtual routing and forwarding (VRF)](/docs/account?topic=account-vrf-service-endpoint) for your account.
{: note}

The following table lists the *Private Collector endpoints* that are available per region.

Ports for every MZR:
- Monitoring agent ports: TCP 6443
- Prometheus Remote Write Ports: TCP 443

| Region      | Private ingestion endpoint       | Private IP addresses       |
|-------------|----------------------------------|----------------------------|
| Dallas (`US-South`)  | `ingest.private.us-south.monitoring.cloud.ibm.com`   | 166.9.14.170  \n 166.9.48.41  \n 166.9.17.11  \n 166.9.228.235  `(*)`  \n 166.9.229.31 `(*)`  \n 166.9.251.30  `(*)`    |
| Frankfurt (`EU-DE`)     | `ingest.private.eu-de.monitoring.cloud.ibm.com`      | 166.9.32.51  \n 166.9.30.53  \n 166.9.28.71  \n 166.9.209.205 `(*)`  \n 166.9.209.227 `(*)`  \n 166.9.210.13 `(*)`  |
| London (`EU-GB`)     | `ingest.private.eu-gb.monitoring.cloud.ibm.com`      | 166.9.34.56  \n 166.9.36.71  \n 166.9.245.189 `(*)`  \n 166.9.245.221 `(*)`  \n 166.9.245.253 `(*)`     |
| Madrid (`EU-ES`)     | `ingest.private.eu-es.monitoring.cloud.ibm.com`      | 166.9.96.31  \n 166.9.95.31  \n 166.9.94.31  \n 166.9.226.56 `(*)`  \n 166.9.227.143 `(*)`  \n 166.9.225.35 `(*)`  |
| Montreal (`CA-MON`)  | `ingest.private.ca-mon.monitoring.cloud.ibm.com`   | 166.9.232.56  \n 166.9.233.54  \n 166.9.231.34 |
| Osaka (`JP-OSA`)    | `ingest.private.jp-osa.monitoring.cloud.ibm.com`     | 166.9.72.14  \n 166.9.71.15  \n 166.9.70.14  \n 166.9.247.59 `(*)`  \n 166.9.247.89 `(*)`  \n 166.9.247.123 `(*)`    |
| Sao Paulo (`BR-SAO`)  | `ingest.private.br-sao.monitoring.cloud.ibm.com`   | 166.9.84.19  \n 166.9.83.18  \n 166.9.82.19  \n 166.9.246.87 `(*)`  \n 166.9.246.120 `(*)`  \n 166.9.246.144 `(*)`   |
| Sydney (`AU-SYD`)    | `ingest.private.au-syd.monitoring.cloud.ibm.com`     | 166.9.56.32  \n 166.9.52.27   \n 166.9.54.27  \n 166.9.244.121 `(*)`  \n 166.9.244.153 `(*)`  \n 166.9.244.185 `(*)`    |
| Tokyo (`JP-TOK`)    | `ingest.private.jp-tok.monitoring.cloud.ibm.com`     | 166.9.44.38  \n 166.9.40.35  \n 166.9.42.48  \n 166.9.212.4 `(*)`  \n 166.9.214.5 `(*)`  \n 166.9.216.14 `(*)`    |
| Toronto (`CA-TOR`)  | `ingest.private.ca-tor.monitoring.cloud.ibm.com`   | 166.9.77.20  \n 166.9.76.23  \n 166.9.78.21  \n 166.9.209.13 `(*)`  \n 166.9.209.42 `(*)`  \n 166.9.209.72 `(*)`    |
| Washington (`US-East`)   | `ingest.private.us-east.monitoring.cloud.ibm.com`    | 166.9.22.50  \n 166.9.24.43  \n 166.9.20.53  \n 166.9.231.19 `(*)`  \n 166.9.232.40 `(*)`  \n 166.9.233.36 `(*)`     |
{: caption="List of ingestion endpoints and private IP addresses to send data to the {{site.data.keyword.mon_full_notm}}" caption-side="top"}





### Public Collector endpoints
{: #endpoints_ingestion_public}

The following table lists the *Public Collector endpoints* that are available per region.

Ports for every MZR:
- Monitoring agent ports: TCP 6443
- Prometheus Remote Write Ports: TCP 443

| Region      | Public ingestion endpoint      | Public IP addresses    |
|-------------|-------------------------------|-------------------------|
| Dallas (`US-South`)  | `ingest.us-south.monitoring.cloud.ibm.com`          | 169.60.151.174  \n 169.46.0.70  \n 169.48.214.70  \n 52.118.209.119 `(*)`  \n 67.18.94.56 `(*)`  \n 52.116.135.250     `(*)`      |
| Frankfurt (`EU-DE`)     | `ingest.eu-de.monitoring.cloud.ibm.com`             | 149.81.77.78  \n 161.156.102.206  \n 159.122.102.38  \n 158.177.2.4 `(*)`  \n 161.156.87.239 `(*)`  \n 149.81.238.82  `(*)`   |
| London (`EU-GB`)     | `ingest.eu-gb.monitoring.cloud.ibm.com`             | 158.175.98.206  \n 141.125.73.118  \n 159.122.210.174  \n 141.125.105.98 `(*)`  \n 161.156.203.133 `(*)`  \n 158.176.179.72  `(*)` |
| Madrid (`EU-ES`)     | `ingest.eu-es.monitoring.cloud.ibm.com`             | 13.122.68.140  \n 13.120.68.187  \n  13.121.68.91  \n 13.121.91.87 `(*)`  \n 13.122.87.104 `(*)`  \n 13.120.91.152   `(*)` |
| Montreal (`CA-MON`)    | `ingest.ca-mon.monitoring.cloud.ibm.com`            | 64.5.49.125  \n 64.5.42.185  \n 64.5.47.9 |
| Sao Paulo (`BR-SAO`)    | `ingest.br-sao.monitoring.cloud.ibm.com`            | 163.107.66.98  \n 163.109.67.242  \n 169.57.141.43  \n 13.116.92.185 `(*)`  \n 163.107.92.212 `(*)`  \n 163.109.84.195  `(*)`     |
| Sydney (`AU-SYD`)    | `ingest.au-syd.monitoring.cloud.ibm.com`            | 135.90.73.100  \n 130.198.80.155  \n 168.1.213.78  \n 130.198.10.95 `(*)`  \n 135.90.130.246 `(*)`  \n 159.23.97.190   `(*)`     |
| Osaka (`JP-OSA`)    | `ingest.jp-osa.monitoring.cloud.ibm.com`            | 163.68.67.98  \n 163.69.66.170  \n 163.73.67.180  \n 163.68.83.196 `(*)`  \n 163.73.82.218 `(*)`  \n 163.69.86.15   `(*)` |
| Toronto (`CA-TOR`)    | `ingest.ca-tor.monitoring.cloud.ibm.com`            | 163.74.69.186  \n 158.85.94.130  \n 163.75.65.237  \n 163.66.86.89 `(*)`  \n 163.75.81.213 `(*)`  \n 163.74.95.149  `(*)`     |
| Tokyo (`JP-TOK`)    | `ingest.jp-tok.monitoring.cloud.ibm.com`            | 165.192.84.14  \n 128.168.75.14  \n 169.56.51.238  \n 162.133.138.54 `(*)`  \n 128.168.143.56 `(*)`  \n 165.192.128.220   `(*)`     |
| Washington (`US-East`)   | `ingest.us-east.monitoring.cloud.ibm.com`           | 169.60.112.74  \n 169.55.109.114  \n 169.62.3.82  \n 169.62.20.11 `(*)`  \n 169.63.183.86 `(*)`  \n 150.239.110.137  `(*)`      |
{: caption="List of ingestion endpoints and public IP addresses to send data to the {{site.data.keyword.mon_full_notm}}" caption-side="top"}




## Prometheus Remote Write ingestion endpoints
{: #prometheus_remote_write_endpoints}

{{site.data.keyword.mon_full_notm}} deprecated Prometheus client support of endpoints in the form `https://ingest.<region>` and `https://ingest.private.<region>` and replaced them with new endpoints on 31 May 2024. End of support for the old endpoints is 31 August 2024. After that date, the old endpoints will stop working. Customers using Prometheus Remote Write need to migrate to use the new endpoints by 31 August 2024 to continue using Prometheus Remote Write.
{: deprecated}

The following table lists the public {{site.data.keyword.mon_short}} ingestion endpoints that you can configure to collect metrics via Prometheus Remote Write:

| Region                | Endpoint                            |
|-----------------------|-------------------------------------|
| Dallas (`US-South`)            | `https://ingest.us-south.monitoring.cloud.ibm.com/prometheus/remote/write` [Deprecated]{: tag-deprecated}  \n `https://ingest.prws.us-south.monitoring.cloud.ibm.com/prometheus/remote/write` |
| Frankfurt (`EU-DE`)               | `https://ingest.eu-de.monitoring.cloud.ibm.com/prometheus/remote/write` [Deprecated]{: tag-deprecated}  \n `https://ingest.prws.eu-de.monitoring.cloud.ibm.com/prometheus/remote/write`    |
| London (`EU-GB`)               | `https://ingest.eu-gb.monitoring.cloud.ibm.com/prometheus/remote/write` [Deprecated]{: tag-deprecated}  \n `https://ingest.prws.eu-gb.monitoring.cloud.ibm.com/prometheus/remote/write`    |
| Madrid (`EU-ES`)               | `https://ingest.eu-es.monitoring.cloud.ibm.com/prometheus/remote/write` [Deprecated]{: tag-deprecated}  \n `https://ingest.prws.eu-es.monitoring.cloud.ibm.com/prometheus/remote/write`    |
| Montreal (`CA-MON`)              | `https://ingest.ca-mon.monitoring.cloud.ibm.com/prometheus/remote/write`  |
| Osaka (`JP-OSA`)              | `https://ingest.jp-osa.monitoring.cloud.ibm.com/prometheus/remote/write` [Deprecated]{: tag-deprecated}  \n `https://ingest.prws.jp-osa.monitoring.cloud.ibm.com/prometheus/remote/write`   |
| Sao Paulo (`BR-SAO`)              | `https://ingest.br-sao.monitoring.cloud.ibm.com/prometheus/remote/write` [Deprecated]{: tag-deprecated}  \n `https://ingest.prws.br-sao.monitoring.cloud.ibm.com/prometheus/remote/write`   |
| Sydney (`AU-SYD`)              | `https://ingest.au-syd.monitoring.cloud.ibm.com/prometheus/remote/write` [Deprecated]{: tag-deprecated}  \n `https://ingest.prws.au-syd.monitoring.cloud.ibm.com/prometheus/remote/write`   |
| Tokyo (`JP-TOK`)              | `https://ingest.jp-tok.monitoring.cloud.ibm.com/prometheus/remote/write` [Deprecated]{: tag-deprecated}  \n `https://ingest.prws.jp-tok.monitoring.cloud.ibm.com/prometheus/remote/write`   |
| Toronto (`CA-TOR`)              | `https://ingest.ca-tor.monitoring.cloud.ibm.com/prometheus/remote/write` [Deprecated]{: tag-deprecated}  \n `https://ingest.prws.ca-tor.monitoring.cloud.ibm.com/prometheus/remote/write`   |
| Washington (`US-EAST`)             | `https://ingest.us-east.monitoring.cloud.ibm.com/prometheus/remote/write` [Deprecated]{: tag-deprecated}  \n `https://ingest.prws.us-east.monitoring.cloud.ibm.com/prometheus/remote/write`  |
{: caption="Prometheus remote write public endpoints" caption-side="top"}

The following table lists the private {{site.data.keyword.mon_short}} ingestion endpoints that you can configure to collect metrics via Prometheus Remote Write:

| Region                | Endpoint                            |
|-----------------------|-------------------------------------|
| Dallas (`US-South`)            | `https://ingest.private.us-south.monitoring.cloud.ibm.com/prometheus/remote/write` [Deprecated]{: tag-deprecated}  \n `https://ingest.prws.private.us-south.monitoring.cloud.ibm.com/prometheus/remote/write` |
| Frankfurt (`EU-DE`)               | `https://ingest.private.eu-de.monitoring.cloud.ibm.com/prometheus/remote/write` [Deprecated]{: tag-deprecated}  \n `https://ingest.prws.private.eu-de.monitoring.cloud.ibm.com/prometheus/remote/write`  |
| London (`EU-GB`)               | `https://ingest.private.eu-gb.monitoring.cloud.ibm.com/prometheus/remote/write` [Deprecated]{: tag-deprecated}  \n `https://ingest.prws.private.eu-gb.monitoring.cloud.ibm.com/prometheus/remote/write`  |
| Madrid (`EU-ES`)               | `https://ingest.private.eu-es.monitoring.cloud.ibm.com/prometheus/remote/write` [Deprecated]{: tag-deprecated}  \n `https://ingest.prws.private.eu-es.monitoring.cloud.ibm.com/prometheus/remote/write`  |
| Montreal (`CA-MON`)              | `https://ingest.private.ca-mon.monitoring.cloud.ibm.com/prometheus/remote/write` |
| Osaka (`JP-OSA`)              | `https://ingest.private.jp-osa.monitoring.cloud.ibm.com/prometheus/remote/write` [Deprecated]{: tag-deprecated}  \n `https://ingest.prws.private.jp-osa.monitoring.cloud.ibm.com/prometheus/remote/write`  |
| Sao Paulo (`BR-SAO`)              |`https://ingest.private.br-sao.monitoring.cloud.ibm.com/prometheus/remote/write` [Deprecated]{: tag-deprecated}  \n `https://ingest.prws.private.br-sao.monitoring.cloud.ibm.com/prometheus/remote/write`  |
| Sydney (`AU-SYD`)              | `https://ingest.private.au-syd.monitoring.cloud.ibm.com/prometheus/remote/write` [Deprecated]{: tag-deprecated}  \n `https://ingest.prws.private.au-syd.monitoring.cloud.ibm.com/prometheus/remote/write` |
| Tokyo (`JP-TOK`)              | `https://ingest.private.jp-tok.monitoring.cloud.ibm.com/prometheus/remote/write` [Deprecated]{: tag-deprecated}  \n `https://ingest.prws.private.jp-tok.monitoring.cloud.ibm.com/prometheus/remote/write` |
| Toronto (`CA-TOR`)              | `https://ingest.private.ca-tor.monitoring.cloud.ibm.com/prometheus/remote/write` [Deprecated]{: tag-deprecated}  \n `https://ingest.prws.private.ca-tor.monitoring.cloud.ibm.com/prometheus/remote/write`  |
| Washington (`US-EAST`)             | `https://ingest.private.us-east.monitoring.cloud.ibm.com/prometheus/remote/write` [Deprecated]{: tag-deprecated}  \n `https://ingest.prws.private.us-east.monitoring.cloud.ibm.com/prometheus/remote/write` |
{: caption="Prometheus remote write private endpoints" caption-side="top"}


## Subnets for webhook notifications from {{site.data.keyword.mon_full_notm}}
{: #endpoints_network_alert_subnets}


| Region     | Alert Notification Source Subnets                                                                          |
|------------|------------------------------------------------------------------------------------------------------------|
| Dallas (`US-SOUTH`) | 150.239.180.0/25  \n 169.46.0.64/29  \n 169.46.39.48/28  \n 169.46.58.24/29  \n 169.47.115.192/28  \n 169.47.71.24/29  \n 169.48.214.64/29  \n 169.48.235.16/28  \n 169.60.151.168/29  \n 169.62.221.32/28  \n 174.36.68.96/27  \n 50.22.148.64/26  \n 52.116.222.192/27  \n 52.117.187.192/27  \n 52.118.158.0/25  \n 52.118.7.64/26  \n 67.228.207.64/26  \n 67.228.219.0/25 \n 52.118.147.1 `(*)`  \n 52.118.250.131 `(*)`  \n 67.18.90.54 `(*)` |
| Frankfurt (`EU-DE`)    | 149.81.151.128/27  \n 149.81.201.192/26  \n 149.81.77.72/29  \n 149.81.99.192/28  \n 158.177.44.192/26  \n 159.122.102.32/29  \n 161.156.1.224/27  \n 161.156.102.200/29  \n 161.156.69.144/28  \n 161.156.77.64/26  \n 169.50.36.64/27  \n 169.50.9.0/28 \n 149.81.10.225 `(*)`  \n 161.156.83.162 `(*)`  \n 149.81.238.81 `(*)`    |
| London (`EU-GB`)    | 141.125.136.32/27  \n 141.125.73.112/29  \n 141.125.73.80/28  \n 158.175.124.224/27  \n 158.175.98.200/29  \n 159.122.210.168/29  \n 159.8.144.168/29  \n 159.8.149.208/28  \n 159.8.162.0/26  \n 161.156.209.192/26  \n 5.10.120.32/27 \n 161.156.201.6 `(*)`  \n 141.125.157.52 `(*)`  \n 158.176.191.3 `(*)`  |
| Madrid (`EU-ES`) | 13.120.68.192/28  \n 13.120.68.224/27  \n 13.121.68.96/28  \n 13.122.68.160/28 \n 13.120.91.148 `(*)`  \n 13.121.80.147 `(*)`  \n 13.122.87.98 `(*)`  |
| Montreal (`CA-MON`)   | 64.5.42.67  \n 64.5.49.47  \n 64.5.46.173 |
| Osaka (`JP-OSA`)   | 163.68.67.128/28  \n 163.68.67.96/29  \n 163.68.79.32/27  \n 163.69.66.168/29  \n 163.69.67.112/28  \n 163.69.70.64/27  \n 163.73.67.176/29  \n 163.73.67.192/28  \n 163.73.69.96/27 \n 163.68.91.237 `(*)`  \n 163.69.80.154 `(*)`  \n 163.73.86.222 `(*)`  |
| Sao Paulo (`BR-SAO`) | 163.107.66.96/29  \n 163.107.68.128/28  \n 163.107.71.32/27  \n 163.109.67.240/29  \n 163.109.73.128/27  \n 169.57.141.40/29  \n 169.57.186.0/27  \n 169.57.195.0/28 \n 13.116.91.143 `(*)`  \n 163.107.86.146 `(*)`  \n 163.109.84.191 `(*)` |
| Sydney (`AU-SYD`)   | 130.198.66.144/28  \n 130.198.80.152/29  \n 135.90.73.96/29  \n 135.90.78.192/28  \n 135.90.94.96/27  \n 168.1.115.192/27  \n 168.1.213.32/27  \n 168.1.213.72/29  \n 168.1.41.96/28 \n 159.23.99.159 `(*)`  \n 130.198.18.13 `(*)`  \n 135.90.142.230 `(*)`  |
| Tokyo (`JP-TOK`)   | 128.168.75.32/28  \n 128.168.75.8/29  \n 128.168.98.0/27  \n 161.202.255.64/27  \n 165.192.84.8/29  \n 165.192.97.96/27  \n 169.56.11.208/28  \n 169.56.51.232/29 \n 162.133.130.143 `(*)`  \n 128.168.137.83 `(*)`  \n 165.192.128.217 `(*)`  |
| Toronto (`CA-TOR`)   | 158.85.78.224/27  \n 158.85.94.128/29  \n 163.74.67.192/28  \n 163.74.69.184/29  \n 163.74.71.96/27  \n 163.75.65.232/29  \n 163.75.72.192/27  \n 169.55.129.208/28 \n 163.66.81.182 `(*)`  \n 163.74.95.147 `(*)`  \n 163.75.86.200 `(*)`  |
| Washington (`US-EAST`)  | 169.47.20.160/27  \n 169.55.109.112/29  \n 169.55.122.192/28  \n 169.59.131.160/27  \n 169.59.146.192/26  \n 169.60.112.72/29  \n 169.60.82.240/28  \n 169.62.28.160/28  \n 169.62.3.80/29  \n 169.62.46.192/27  \n 52.116.95.64/26  \n 52.117.71.128/26 \n 150.239.82.158 `(*)`  \n 169.63.176.251 `(*)`  \n 169.62.18.195 `(*)`  |
{: caption="Source Subnets for Webhook notifications from {{site.data.keyword.mon_full_notm}}" caption-side="top"}





## Endpoint IP address change schedule
{: #endpoints_ipaddress_change_schedule}

This is the planned roll out for the IP address changes in 2025. All new IP addresses in the endpoint section tables marked by `(*)` are already available for each MZR, and can be added to any firewall allowlists in your infrastructure.

This table lists the “Target Date” for cutover to adding the new IP addresses for any firewall allowlists. After a short period, when final testing is complete, and the status has changed to “Completed”, you can remove old IP addresses from any allowlists.

Any date listed that is “to be determined” (TBD) has not been finalized. However, the new IP addresses can and should be added to your allowlists now, or any time before the “Target Date”, to avoid disruptions.


As a newly supported region, Montreal (`CA-MON`) does not require IP address changes.
{: note}



| Region | Target Date | Status |
|-------|-------|-------|
| Sydney (`AU-SYD`)   | 5 May 2025 | Completed |
| Sao Paulo (`BR-SAO`) | 5 August 2025 | Target: 6 August 2025 |
| Toronto (`CA-TOR`)   | 12 August 2025 | Not started |
| Montreal (`CA-MON`)   | Not needed | Not needed |
| Madrid (`EU-ES`)     | TBD | Not planned yet |
| Washington (`US-East`) | TBD | Not planned yet |
| Dallas (`US-South`)  | TBD | Not planned yet |
| Frankfurt (`EU-DE`)  | TBD | Not planned yet |
| London (`EU-GB`)     | TBD | Not planned yet | 
| Osaka (`JP-OSA`)     | TBD | Not planned yet | 
| Tokyo (`JP-TOK`)     | TBD | Not planned yet | 
{: caption="MZR change over dates" caption-side="top"}
