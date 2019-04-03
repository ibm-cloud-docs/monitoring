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



# Excluindo notificações
{: #delete_notifications}

É possível excluir notificações do serviço {{site.data.keyword.monitoringshort}} usando [a API de Alertas](https://console.bluemix.net/apidocs/940-ibm-cloud-monitoring-alerts-api?&language=node#introduction){: new_window}.
{:shortdesc}

Depois de [efetuar login em uma região no {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login), conclua as etapas a seguir para excluir uma notificação:


## Etapa 1: Obter o token de segurança
{: #step1_delete_notifications}

É possível usar um token do UAA, um token do IAM ou uma chave API. 

Escolha um dos métodos a seguir para obter o token de segurança:
	
* Para obter um token do UAA, consulte [Obtendo o token do UAA usando a CLI do {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_uaa#uaa_cli).
* Para obter um token do IAM, consulte [Obtendo o token do IAM usando a CLI do {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_iam#auth_iam).
* Para obter uma chave API, consulte [Recebendo uma chave API](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_api_key#auth_api_key).
	
Por exemplo, para usar o token IAM, execute o comando a seguir:

```
ibmcloud iam oauth-tokens
```
{: codeblock}
	
O resultado desse comando é o seguinte:
	
```
IAM token: Bearer djn.._l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ UAA token: Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
```
{: screen}
	
Em seguida, exporte a variável *Token*:
	
```
export Token="djn.._l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ"
```
{: screen}
	
**Nota:** o token exclui *Bearer*.
	

## Etapa 2: Obter o ID do espaço 
{: #step2_delete_notifications}

Esta etapa se aplica apenas quando você deseja excluir as notificações disponíveis em um domínio de espaço.

Para obter o GUID do espaço, execute o comando a seguir:
	
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
	
Em seguida, exporte a variável *Space*. O GUID deve ser prefixado com *s-* para identificar um espaço.
	
```
export Space="s-667fadfc-jhtg-1234-9f0e-cf4123451095"
```
{: screen}

	

## Etapa 3: Listar as notificações
{: #step3_delete_notifications}


Execute o comando cURL a seguir para listar as notificações em um domínio de espaço:

```
curl -H "X-Auth-Scope-Id: ${Space}" -H “X-Auth-User-Token: Auth_Type ${TOKEN}" -XGET METRICS_ENDPOINT/v1/alert/notifications

```
{: screen}

Execute o comando cURL a seguir para listar as notificações no domínio de contas:

```
curl -H "X-Auth-User-Token: apikey ${TOKEN}" -XGET METRICS_ENDPOINT/v1/alert/notifications
```
{: screen}

Em que
	
* O *X-Auth-User-Token* é um parâmetro que passa o token do UAA do {{site.data.keyword.Bluemix_notm}}, o token do IAM ou a chave API.
	
* *Auth_Type* é o prefixo que define o tipo de token ou a chave API. A lista a seguir descreve os valores válidos: *apikey*, *iam* ou *uaa*, em que

    * *apikey* identifica que o token é uma chave API.
	* *iam* identifica que o token especificado é um token gerado pelo IAM.
	* *uaa* identifica que o token especificado é um token gerado pelo UAA
	
* *X-Auth-Scope-Id* é um parâmetro que passa o GUID de espaço. O GUID deve ser prefixado com *s-* para identificar um espaço. 
	
* Token é o token de autenticação do UAA ou do IAM ou a chave API.
	
* Espaço é o GUID do espaço. 
	
* METRICS_ENDPOINT representa o ponto de entrada para o serviço. Cada região possui uma URL diferente. Para obter a lista de terminais por região, consulte [Terminais](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints).


## Etapa 4: Excluir uma notificação
{: #step4_delete_notifications}
  

Execute o comando cURL a seguir para excluir uma notificação em um domínio de espaço:

```
curl -H "X-Auth-Scope-Id: ${Space}" -H “X-Auth-User-Token: Auth_Type ${TOKEN}" -XDELETE METRICS_ENDPOINT/v1/alert/notification/{name} 
```
{: screen}

Execute o comando cURL a seguir para excluir uma notificação do domínio de contas:

```
curl -H "X-Auth-User-Token: apikey ${TOKEN}" -XDELETE METRICS_ENDPOINT/v1/alert/notification/{name} 
```
{: screen}

	
Em que
	
* O *X-Auth-User-Token* é um parâmetro que passa o token do UAA do {{site.data.keyword.Bluemix_notm}}, o token do IAM ou a chave API.
	
* *Auth_Type* é o prefixo que define o tipo de token ou a chave API. A lista a seguir descreve os valores válidos: *apikey*, *iam* ou *uaa*, em que

    * *apikey* identifica que o token é uma chave API.
	* *iam* identifica que o token especificado é um token gerado pelo IAM.
	* *uaa* identifica que o token especificado é um token gerado pelo UAA
	
* *X-Auth-Scope-Id* é um parâmetro que passa o GUID de espaço. O GUID deve ser prefixado com *s-* para identificar um espaço. 
	
* Token é o token de autenticação do UAA ou do IAM ou a chave API.
	
* Espaço é o GUID do espaço. 
	
* METRICS_ENDPOINT representa o ponto de entrada para o serviço. Cada região possui uma URL diferente. Para obter a lista de terminais por região, consulte [Terminais](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints).

* *name* é o nome da notificação que você deseja excluir.
	
