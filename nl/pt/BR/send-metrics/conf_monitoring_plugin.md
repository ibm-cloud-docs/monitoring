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

# Enviando dados usando o plug-in de Monitoramento (collectd)
{: #conf_monitoring_plugin}

É possível configurar o collectd para coletar métricas em um ambiente. Use o plug-in do {{site.data.keyword.monitoringshort}} para enviar essas métricas para um domínio do espaço de seu ambiente. 
{: shortdesc}

A figura a seguir mostra uma visualização de alto nível de como usar o plug-in do {{site.data.keyword.monitoringshort}} para enviar métricas para o serviço do {{site.data.keyword.monitoringshort}}:

![High level view on how to use the {{site.data.keyword.monitoringshort}} plugin](images/monitoring_plugin_ov.png "High level view on how to use the {{site.data.keyword.monitoringshort}} plugin")



## Instalar o plug-in de Monitoramento
{: #install}

Em um terminal, conclua as etapas a seguir: 

1. (Pré-requisito) Instale a CLI do {{site.data.keyword.Bluemix_notm}}.

   Para obter mais informações, consulte [Instalando a CLI do {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#cli_qa).
   
   Se a CLI estiver instalada, continue com a próxima etapa.
	
2. Efetue login em uma região, uma organização e um espaço no {{site.data.keyword.Bluemix_notm}}. 

    Para obter mais informações, veja [Como efetuar login no {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login).

    Por exemplo, para efetuar login na região sul dos EUA, execute o comando a seguir:
	
	```
    ibmcloud login -a https://api.ng.bluemix.net
	ibmcloud target -o MyOrg -s MySpace
    ```
    {: codeblock}

    Siga as instruções. Insira suas credenciais do {{site.data.keyword.Bluemix_notm}}, selecione uma organização e um espaço.

### Etapa 1: Instalar o collectd
{: #collectd}

Como administrador, conclua as etapas a seguir para instalar o collectd:

1.	Efetue login como usuário raiz. 

    ```
    sudo -s
    ```
    {: codeblock}

2.	Instale o pacote do Network Time Protocol (NTP) para sincronizar o horário dos logs. 

    Por exemplo, para um sistema Ubunutu, veja se `timedatectl status` mostra *Network time on: yes*. Em caso positivo, o sistema Ubuntu já está configurado para usar ntp e será possível ignorar esta etapa.
    
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
    
    Conclua as etapas a seguir para instalar ntp em um sistema Ubuntu:

    1.	Execute o comando a seguir para atualizar os pacotes. 

        ```
        apt-get update
        ```
        {: codeblock}
        
    2.	Execute o comando a seguir para instalar o pacote ntp. 

        ```
        apt-get install ntp
        ```
        {: codeblock}
        
    3.	Execute o comando a seguir para instalar o pacote ntpdate. 
    
        ```
        apt-get install ntpdate
        ```
        {: codeblock}
        
    4.	Execute o comando a seguir para parar o serviço 
        
        ```
        service ntp stop
        ```
        {: codeblock}
        
    5.	Execute o comando a seguir para sincronizar o relógio do sistema. 
    
        ```
        ntpdate -u 0.ubuntu.pool.ntp.org
        ```
        {: codeblock}
        
        O resultado confirma que o horário está ajustado, por exemplo:
        
        ```
        4 May 19:02:17 ntpdate[5732]: adjust time server 50.116.55.65 offset 0.000685 sec
        ```
        {: screen}
        
    6.	Execute o comando a seguir para iniciar o ntpd novamente. 
    
        ```
        service ntp start
        ```
        {: codeblock}
    
        O resultado confirma que o serviço está sendo iniciado.

3. Instale o collectd. Execute o seguinte comando:

    ```
	apt-get install collectd 
	```
	{: codeblock}


### Etapa 2: Instalar o plug-in de Monitoramento
{: #plugin}

Conclua as etapas a seguir para instalar o plug-in do {{site.data.keyword.monitoringshort}}:

1. 	Efetue login como usuário raiz. 

    ```
    sudo -s
    ```
    {: codeblock}
	
2. Inclua o repositório de serviço do  {{site.data.keyword.monitoringshort}} . Execute o seguinte comando:

    ```
    wget -O - https://downloads.opvis.bluemix.net/client/IBM_Logmet_repo_install.sh | bash
    ```
   {: codeblock}
   
3. Instale o plug-in. Execute o seguinte comando:

    ```
	apt-get install ibmcloud-monitoring
	```
	{: codeblock}


## Configurar o Plug-in de Monitoramento
{: #configure}

Para configurar o plug-in do {{site.data.keyword.monitoringshort}}, conclua as etapas a seguir:
	
### Etapa 1: Designar uma política do IAM para o usuário
{: #iam_policy}

Para enviar métricas para qualquer domínio, seu ID do usuário deve receber uma função do IAM com permissões para enviar métricas para o serviço de Monitoramento.
 
* Permissões são configuradas designando uma política do IAM para esse usuário no IBM Cloud. 
* As funções do IAM a seguir permitem que um usuário envie métricas: *Administrator*, *Editor*, *Operator*. 

Para designar um usuário a uma política do IAM, escolha um dos métodos a seguir:

* Por meio da IU do {{site.data.keyword.Bluemix_notm}}: para obter mais informações, consulte [Designando uma política de IAM a um usuário por meio da IU do {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-grant_permissions#assign_policy_ui).
* Usando a linha de comandos: para obter mais informações, consulte [Designando a um usuário uma política do IAM usando a linha de comandos](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-grant_permissions#assign_policy_commandline).
 
### Etapa 2: Obter uma chave API
{: #api_key}
 
Para enviar métricas para um espaço, deve-se obter uma chave API para autenticar com o serviço {{site.data.keyword.monitoringshort}}.

Para obter mais informações sobre como obter uma chave API, consulte [Obtendo uma chave API](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_api_key#auth_api_key).
	
From the same terminal where you logged in to the {{site.data.keyword.Bluemix_notm}}, set the APIKEY variable for the token.

Por exemplo,

```
export APIKEY="kjshdgf.....ldkdjdj"
```
{: screen}
	
### Etapa 3: Obter informações sobre o terminal
{: #endpoint}

Para determinar o terminal do {{site.data.keyword.monitoringshort}} no qual você enviará as métricas, consulte as lista de terminais por região, consulte [Terminais](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints) e identifique aquela para a região na qual você deseja enviar métricas.

No mesmo terminal no qual você efetuou login no {{site.data.keyword.Bluemix_notm}}, configure a variável **METRIC_ENDPOINT**. Por exemplo,

```
export METRIC_ENDPOINT="metrics.ng.bluemix.net"
```
{: screen}



### Etapa 4: Obter informações sobre o ID do domínio de espaço 
{: #domain}

Para obter o ID do domínio para um espaço, [obtenha o GUID do espaço](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#space_guid). Em seguida, configure o ID do domínio como a seguir: `s-SpaceID`, em que SpaceID é o GUID do espaço.

From the same terminal where you logged in to the {{site.data.keyword.Bluemix_notm}}, set the SpaceID variable:

```
export SpaceID="kjshdgf.....ldkdjdj"
```
{: screen}



### Etapa 5: Executar o Script de Configuração
{: #script}

Execute o script a seguir para configurar o plug-in do {{site.data.keyword.monitoringshort}} para enviar métricas para um espaço:

```
/opt/ibmcloud_monitoring/configure -e $METRIC_ENDPOINT -a $APIKEY -s s-$SpaceID
```
{: codeblock}


O script inclui automaticamente a sub-rotina de **Inclusão** no arquivo collectd.conf principal:

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


### Etapa 6: Reiniciar o daemon collectd
{: #restart}

Conclua as etapas a seguir:

1. 	Efetue login como usuário raiz. 

    ```
    sudo -s
    ```
    {: codeblock}
	
2.  Reinicie o collectd.

   Se o daemon collectd foi incluído como um serviço, execute o comando a seguir:
	
	```
	service collectd restart
	```
	{: codeblock}

As métricas que são ativadas em collectd são aquelas que estão disponíveis para análise no Grafana.


