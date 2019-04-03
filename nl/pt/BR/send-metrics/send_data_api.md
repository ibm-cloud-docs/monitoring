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

# Enviando dados usando a API de Métricas
{: #send_data_api}

É possível enviar métricas para o serviço do {{site.data.keyword.monitoringshort}} usando a API de Métricas. 
{:shortdesc}


Para os contêineres do {{site.data.keyword.Bluemix_notm}} Docker, as métricas básicas do
sistema são coletadas automaticamente. Para os aplicativos Cloud Foundry e os apps em execução em uma Máquina virtual (VM), as métricas devem ser enviadas diretamente do app usando [a API de Métricas](https://console.bluemix.net/apidocs/927-ibm-cloud-monitoring-rest-api?&language=node#introduction){: new_window}. 



## Enviando métricas para um domínio do espaço
{: #space_uaa}

Para enviar métricas para um espaço usando cURL, conclua as etapas a seguir:

1. Efetue login em uma região, uma organização e um espaço no {{site.data.keyword.Bluemix_notm}}. 

    Para obter mais informações, veja [Como efetuar login no {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login).

2. Obtenha o token de segurança. É possível usar um token do UAA, um token do IAM ou uma chave API.

    Escolha um dos métodos a seguir para obter o token de segurança que você precisa para enviar métricas:
	
	* Para obter um token do UAA, consulte [Obtendo o token do UAA usando a CLI do {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_uaa#uaa_cli);
	
	* Para obter um token do IAM, consulte [Obtendo o token do IAM usando a CLI do {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_iam#auth_iam).
	
	* Para obter uma chave API, consulte
[Obtendo uma chave
API](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_api_key#auth_api_key).
	
	No mesmo terminal em que você efetuou login no {{site.data.keyword.Bluemix_notm}}, configure
a variável *Token* para o token.

    Por exemplo, configure um token do UAA e remova a parte *Bearer* do valor do token:

    ```
    export Token="kjshdgf.....ldkdjdj"
    ```
    {: screen}
		
3. Obtenha o GUID do espaço. O GUID deve ser prefixado com *s-* para identificar um espaço.

    Execute o seguinte comando:
	
	```
	ibmcloud iam espaço SpaceName -- guid
	```
	{: codeblock}
	
	Em que *SpaceName* é o nome do espaço em que você irá definir uma notificação.
	
	Por exemplo, para obter o GUID de um espaço com o nome *dev*, execute o comando a seguir:
	
	```
	ibmcloud iam espaço dev -- guid
	```
	{: screen}
	
	O resultado desse comando é o seguinte:
	
	```
	667fadfc-jhtg-1234-9f0e-cf4123451095
	```
	{: screen}
	
	Em seguida, exporte a variável *Space*. **Nota:** o GUID deve ser
prefixado com *s-* para identificar um espaço.
	
	Por exemplo:
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
5. Execute o comando cURL a seguir para enviar métricas:

    ```
	curl -XPOST -d @Metric_File --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" Endpoint/v1/metrics
	```
	{: codeblock}
	
	Em que
	
	* O Metrics_File representa o arquivo JSON que inclui a definição de métricas que são enviadas para o serviço {{site.data.keyword.monitoringshort}}.
	
	* O *X-Auth-User-Token* é um parâmetro que passa o token de segurança.
	
	* *Auth_Type* é o prefixo que define o tipo de token. Os valores válidos são: *uaa* para um token do UAA, *iam* para um token do IAM e *api* para uma chave API.
	
	* *X-Auth-Scope-Id* é um parâmetro que passa o GUID de espaço. O GUID deve ser prefixado com *s-* para identificar um espaço.
	
	* Token representa o token de segurança ou a chave API.
	
	* Espaço representa o GUID do espaço. 
	
	* Terminal representa o ponto de entrada para o serviço. Cada região possui uma URL diferente. Para obter a lista de terminais por região, consulte [Terminais](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints).
	
	Por exemplo, é possível executar o comando a seguir para enviar duas métricas, `myhost.cpu.idle` e `myapp.login.attempts`, para o serviço {{site.data.keyword.monitoringshort}}:
	
	```
	curl -XPOST @metric.json --header "X-Auth-User-Token: uaa ${Token}" https://metrics.ng.bluemix.net/v1/metrics
	```
	{: screen}
	
	O arquivo de amostra *metric.json* é definido como a seguir:

    ```
    [
      {
        "name" : "myhost.cpu.idle",
        "value" : 22.37
      },
      {
        "name": "myapp.login.retries",
        "value": 4
      }
    ]
	```
	{: screen}

 











 
