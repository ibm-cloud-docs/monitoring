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

# Configurando um alerta de e-mail usando a API {{site.data.keyword.monitoringshort}}
{: #configure_email_alert}

Para configurar um alerta de e-mail em uma métrica, defina uma regra e uma notificação por e-mail. Em seguida, registre a regra e o método de notificação com o serviço {{site.data.keyword.monitoringshort}}.
{:shortdesc}

Conclua as etapas a seguir:

## Etapa 1: criar uma regra
{: #step11}

Crie uma regra para uma consulta de métrica que você definiu em Grafana. Para obter mais informações, consulte [Criando uma regra](/docs/services/cloud-monitoring/alerts/rules.html#create).

Por exemplo, crie o arquivo de regras `s-rule-1.json` no diretório `~/cloud-monitoring/rules/`. 

```
{
"name": "checkbytesin",
"description": "MH check Bytes In per second",
"expression": "movingAverage(messagehub.65qser11-8034-1234-5678-c82fb42wdfgh.1.kafka-java-console-sample-topic.BytesInPerSec.15MinuteRate,\"5min\")",
"enabled": true,
"from": "-5min",
"until": "now",
"comparison": "above",
"comparison_scope": "last",
"error_level" : 27,
"warning_level" : 25,
"frequency": "1min",
"dashboard_url": "https://metrics.ng.bluemix.net",
"notifications": [
"NOTIFICATION_NAME"
]
}
```
{: screen}

Em seguida, exporte a variável *RULE_FILE*:
	
```
export RULE_FILE="s-rule-1.json"
```
{: screen}

## Etapa 2: registrar a regra no Serviço de monitoramento
{: #step2}
	
Em um terminal, conclua as etapas a seguir:

1. Efetue login em uma região, uma organização e um espaço no {{site.data.keyword.Bluemix_notm}}. 

    Para obter mais informações, veja [Como efetuar login no {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login).

2. Obtenha o token de segurança. É possível usar um token do UAA, um token do IAM ou uma chave API. Escolha um dos métodos a seguir para obter o token de segurança:
	
	* Para obter um token do UAA, consulte [Obtendo o token do UAA usando a CLI do {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security/auth_uaa.html#uaa_cli).
	
	* Para obter um token do IAM, consulte [Obtendo o token do IAM usando a CLI do {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security/auth_iam.html#auth_iam).
	
	* Para obter uma chave API, consulte [Recebendo uma chave API](/docs/services/cloud-monitoring/security/auth_api_key.html#auth_api_key).
	
	Por exemplo, para usar o token IAM, execute o comando a seguir:

    ```
	ibmcloud iam oauth-tokens
	```
	{: codeblock}
	
	O resultado desse comando é o seguinte:
	
	```
	IAM token: Bearer djn.._l_HWtlNTibmcloudslibmclouds0qjBI9GqCnuQ UAA token: Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	Em seguida, exporte a variável *Token*:
	
	```
	export Token="djn .. _l_HWtlNTibmcloudslibmclouds0qjBI9GqCnuQ "
	```
	{: screen}
	
	**Nota:** o token exclui *Bearer*.
	
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
	
	Em seguida, exporte a variável *Space*:
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. Execute o comando cURL a seguir para registrar uma regra:
	
    ```
	curl -XPOST -d @$RULE_FILE --header "X-Auth-User-Token: Auth_Type ${Token}" METRICS_ENDPOINT/v1/alert/rule
	```
	{: screen}
	
	Em que
	
	* RULE_FILE é o arquivo JSON que define a sua regra de alerta.
	
	* O *X-Auth-User-Token* é um parâmetro que passa o token do UAA, o token do IAM ou a chave API.
	
	* *Auth_Type* é o prefixo que define o tipo de token ou a chave API. A lista a seguir descreve os valores válidos: *apikey*, *iam* ou *uaa*, em que

        * *apikey* identifica que o token é uma chave API.
		* *iam* identifica que o token especificado é um token gerado pelo IAM.
		* *uaa* identifica que o token especificado é um token gerado pelo UAA
	
	* *X-Auth-Scope-Id* é um parâmetro que passa o GUID de espaço. O GUID deve ser prefixado com *s-* para identificar um espaço. Esse cabeçalho será necessário se você usar uma autenticação do token UAA. Se você usar um token de autenticação IAM, esse cabeçalho será opcional e as informações de domínio ligadas ao token serão usadas.
	
	* Token é o token de autenticação do UAA ou do IAM ou a chave API.
	
	* Espaço é o GUID do espaço. 
	
	* METRICS_ENDPOINT representa o ponto de entrada para o serviço. Cada região possui uma URL diferente. Para obter a lista de terminais por região, consulte [Terminais](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).
	
	Para verificar se a regra foi criada com sucesso, execute o comando a seguir:
	
	```
	curl -XGET --header "X-Auth-User-Token:iam ${Token}" METRICS_ENDPOINT/v1/alert/rule/checkbytesin
	```
	{: codeblock}
	
	Por exemplo,

    ```
	curl -XGET --header "X-Auth-User-Token:iam ${Token}" https://metrics.ng.bluemix.net/v1/alert/rule/checkbytesin
	```
	{: screen}

## Etapa 3: Criar uma notificação por email
{: #step3}


Para criar um arquivo de notificação que envie um e-mail, considere as seguintes informações:

* Use o modelo de notificação para enviar e-mails. Para obter mais informações, consulte [Modelos de notificação](/docs/services/cloud-monitoring/config_alerts_ov.html#notification_template).
* Crie o arquivo em um diretório local, por exemplo, `~/cloud-monitoring/notifications`.

Por exemplo, crie o arquivo **email.json** usando o editor de vi: 
	
```
{
"name": "NOTIFICATION_NAME",
"type": "Email",
"description" : "Send email to manager of department X when ....",
"detail": "Enter email address, for example, xxx@yyy"
}
```
{: codeblock}	
	
Para obter mais informações, veja [Criando uma notificação](/docs/services/cloud-monitoring/alerts/notifications.html#notifications_create).
	
## Etapa 4: Registrar o método de notificação no serviço Monitoring
{: #step4}
	
Em um terminal, conclua as etapas a seguir:

1. Efetue login em uma região, uma organização e um espaço no {{site.data.keyword.Bluemix_notm}}. 

    Para obter mais informações, veja [Como efetuar login no {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login).

2. Obtenha o token de segurança. É possível usar um token do UAA, um token do IAM ou uma chave API. Escolha um dos métodos a seguir para obter o token de segurança:
	
	* Para obter um token do UAA, consulte [Obtendo o token do UAA usando a CLI do {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security/auth_uaa.html#uaa_cli).
	
	* Para obter um token do IAM, consulte [Obtendo o token do IAM usando a CLI do {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security/auth_iam.html#auth_iam).
	
	* Para obter uma chave API, consulte [Recebendo uma chave API](/docs/services/cloud-monitoring/security/auth_api_key.html#auth_api_key).
	
	Por exemplo, para usar o token IAM, execute o comando a seguir:

    ```
	ibmcloud iam oauth-tokens
	```
	{: codeblock}
	
	O resultado desse comando é o seguinte:
	
	```
	IAM token: Bearer djn.._l_HWtlNTibmcloudslibmclouds0qjBI9GqCnuQ UAA token: Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	Em seguida, exporte a variável *Token*:
	
	```
	export Token="djn .. _l_HWtlNTibmcloudslibmclouds0qjBI9GqCnuQ "
	```
	{: screen}
	
	**Nota:** o token exclui *Bearer*.
	
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
	
	Em seguida, exporte a variável *Space*:
	
	```
	export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
	```
	{: screen}
	
4. Execute o comando cURL a seguir para registrar uma notificação:

    ```
	curl -XPOST -d @$NOTIFICATION_FILE --header "X-Auth-User-Token: Auth_Type ${Token}" METRICS_ENDPOINT/v1/alert/notification
	```
	{: screen}
	
	Em que
	
	* NOTIFICATION_FILE é o arquivo JSON que define a sua notificação.
	
	* O *X-Auth-User-Token* é um parâmetro que passa o token do UAA do {{site.data.keyword.Bluemix_notm}}, o token do IAM ou a chave API.
	
	* *Auth_Type* é o prefixo que define o tipo de token ou a chave API. A lista a seguir descreve os valores válidos: *apikey*, *iam* ou *uaa*, em que

        * *apikey* identifica que o token é uma chave API.
		* *iam* identifica que o token especificado é um token gerado pelo IAM.
		* *uaa* identifica que o token especificado é um token gerado pelo UAA
	
	* *X-Auth-Scope-Id* é um parâmetro que passa o GUID de espaço. O GUID deve ser prefixado com *s-* para identificar um espaço. Esse cabeçalho será necessário se você usar uma autenticação do token UAA. Se você usar um token de autenticação IAM, esse cabeçalho será opcional e as informações de domínio ligadas ao token serão usadas.
	
	* Token é o token de autenticação do UAA ou do IAM ou a chave API.
	
	* Espaço é o GUID do espaço. 
	
	* METRICS_ENDPOINT representa o ponto de entrada para o serviço. Cada região possui uma URL diferente. Para obter a lista de terminais por região, consulte [Terminais](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).
	
    Para verificar se a notificação foi criada com sucesso, execute o comando a seguir:

	```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" METRICS_ENDPOINT/v1/alert/notification/NOTIFICATION_NAME
	```
	{: codeblock}
	
	Por exemplo:
	
    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" https://metrics.ng.bluemix.net/v1/alert/notification/NOTIFICATION_NAME
	```
	{: screen}
	


    
   
  


 
	  
