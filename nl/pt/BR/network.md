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

 
# Gerenciando o tráfego de rede para configurações de firewall customizado
{: #network}

Quando você tiver um firewall extra configurado ou customizar as configurações de firewall
em sua infraestrutura do {{site.data.keyword.cloud_notm}}, será necessário permitir o tráfego
de rede de saída para o serviço {{site.data.keyword.mon_full_notm}}.
{:shortdesc}


## Terminais de ingestão
{: #network_send}

Para enviar dados de métrica para o serviço {{site.data.keyword.mon_full_notm}}, deve-se definir a regra de firewall a seguir em seu host:

| Região      | Terminal de ingestão                                | Endereço IP público                                     | Portas    |
|-------------|---------------------------------------------------|---------------------------------------------------------|----------|
| `US South`  | ingest.us-south.monitoring.cloud.ibm.com          | 169.60.151.174 </br>169.46.0.70 </br>169.48.214.70      | TCP 6443 | 
| `EU DE`     | ingest.eu-de.monitoring.cloud.ibm.com             | 149.81.77.78 </br>161.156.102.206 </br>159.122.102.38   | TCP 6443 | 
| `EU GB`     | ingest.eu-gb.monitoring.cloud.ibm.com             | 158.175.98.206 </br>141.125.73.118 </br>159.122.210.174 | TCP 6443 | 
| `JP TOK`    | ingest.jp-tok.monitoring.cloud.ibm.com            | 165.192.84.14 </br>128.168.75.14 </br>169.56.51.238     | TCP 6443 | 
{: caption="Tabela 1. Endereços IP para enviar dados para o {{site.data.keyword.mon_full_notm}}" caption-side="top"}


## Terminais da IU da web
{: #network_ui}

Para acessar a IU da web do {{site.data.keyword.mon_full_notm}}, deve-se definir a regra de firewall a seguir em seu host:

| Região      | Terminal da IU da web                                   | Endereço IP público                                       | Portas   |
|-------------|---------------------------------------------------|-----------------------------------------------------------|---------|
| `US South`  | us-south.monitoring.cloud.ibm.com                 | 169.60.151.174 </br>169.46.0.70 </br>169.48.214.70        | https (TLS) 443 | 
| `EU DE`     | eu-de.monitoring.cloud.ibm.com                    | 149.81.77.78 </br>161.156.102.206 </br>159.122.102.38     | https (TLS) 443 | 
| `EU GB`     | eu-gb.monitoring.cloud.ibm.com                    | 158.175.98.206 </br>141.125.73.118 </br>159.122.210.174   | https (TLS) 443 | 
| `JP TOK`    | ingest.jp-tok.monitoring.cloud.ibm.com            | 165.192.84.14 </br>128.168.75.14 </br>169.56.51.238       | https (TLS) 443 |
{: caption="Tabela 2. Endereços IP para acessar a IU da web do {{site.data.keyword.mon_full_notm}}" caption-side="top"}


