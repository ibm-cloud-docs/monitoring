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



# Excluindo Métricas
{: #delete_metrics}

É possível excluir métricas do serviço {{site.data.keyword.monitoringshort}} usando [a API de Métricas](https://console.bluemix.net/apidocs/monitoring-metrics-api).
{:shortdesc}

Depois de [efetuar login em uma região no {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login), conclua as etapas a seguir para excluir uma notificação:


## Etapa 1: Obter o token de segurança
{: #step1_delete_metrics}

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
IAM token:  Bearer djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ
    UAA token:  Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
```
{: screen}
	
Em seguida, exporte a variável *Token*:
	
```
export Token="djn.._l_HWtlNTbxslBXs0qjBI9GqCnuQ"
```
{: screen}
	
**Nota:** o token exclui *Bearer*.
	
## Etapa 2: Verificar as permissões para trabalhar com métricas 
{: #step2_delete_metrics}

Dependendo do domínio no qual as métricas estão disponíveis, considere as informações a seguir:

* Para trabalhar com as métricas disponíveis em um domínio de espaço, o usuário precisa da função de *desenvolvedor* no espaço do Cloud Foundry associado ao domínio. 
* Para trabalhar com as métricas disponíveis no domínio de contas, o usuário precisa de uma política do IAM com a função de *administrador*, *operador* ou *editor*.

Para verificar suas permissões de usuário, conclua as etapas a seguir:

1. Efetue login no console do {{site.data.keyword.Bluemix_notm}}.

    Abra um navegador da web e ative o painel do {{site.data.keyword.Bluemix_notm}}: [http://console.bluemix.net ![External link icon](../../../icons/launch-glyph.svg "External link icon")](http://bluemix.net){:new_window}
	
	Após você efetuar login com o seu ID do usuário e senha, a UI do {{site.data.keyword.Bluemix_notm}} será aberta.

2. Na barra de menus, clique em **Gerenciar > Conta > Usuários**. 

    A janela *Usuários* exibe uma lista de usuários com seus endereços de e-mail para a conta selecionada atualmente.
	
3. Verifique as permissões de acesso para trabalhar com o serviço {{site.data.keyword.monitoringshort}}.


## Etapa 3: Obter o ID do espaço 
{: #step3_delete_metrics}

Esta etapa se aplica apenas quando você deseja excluir as métricas disponíveis em um domínio de espaço.

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

	

## Etapa 4: Listar as métricas
{: #step4_delete_metrics}


Execute o comando cURL a seguir para listar as métricas disponíveis em um domínio de espaço:

```
curl -H "X-Auth-Scope-Id: ${Space}" -H “X-Auth-User-Token: Auth_Type ${TOKEN}" -XGET METRICS_ENDPOINT/v1/metrics/list?query=*

```
{: screen}

Execute o comando cURL a seguir para listar as métricas disponíveis no domínio de contas:

```
curl -H "X-Auth-User-Token: apikey ${TOKEN}" -XGET METRICS_ENDPOINT/v1/metrics/list?query=*
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

* *query* define o filtro aplicado. Por exemplo, `query=metric-service.*` lista todas as métricas existentes na hierarquia `metric-service.*` e `query=*` lista todas as métricas no domínio.


## Etapa 5 - Opção 1: Excluir todas as métricas
{: #step5_delete_metrics}
  

Execute o comando cURL a seguir para excluir todas as métricas em um domínio de espaço:

```
curl -XDELETE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/metrics/list?query=*
```
{: screen}

Execute o comando cURL a seguir para excluir todas as métricas do domínio de contas:

```
curl -H "X-Auth-User-Token: Auth_Type ${Token}" -XDELETE  METRICS_ENDPOINT/v1/metrics/list?query=*
```
{: screen}

Em que
	
* O *X-Auth-User-Token* é um parâmetro que passa o token do UAA do {{site.data.keyword.Bluemix_notm}}.
	
* Auth_Type é o prefixo que define o tipo de token. Os valores válidos são: *uaa* para um token do UAA, *iam* para um token do IAM e *api* para uma chave API.
	
* *X-Auth-Scope-Id* é um parâmetro que passa o GUID de espaço. O GUID deve ser prefixado com *s-* para identificar um espaço.
	
* *Token* representa o token de segurança.
	
* *Espaço* representa o GUID do espaço. 
	
* *METRICS_ENDPOINT* representa o ponto de entrada para o serviço. Cada região possui uma URL diferente. Para obter a lista de terminais por região, consulte [Terminais](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints).

* *query* define o filtro aplicado. `query=*` indica todas as métricas no domínio.


## Etapa 6 - Opção 2: exclua todas as métricas para um serviço
{: #step6_delete_metrics}
  

Execute o comando cURL a seguir para excluir todas as métricas de um serviço em um domínio de espaço:

```
curl -XDELETE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/metrics/list?query=metric-service.*
```
{: screen}

Execute o comando cURL a seguir para excluir todas as métricas do domínio de contas:

```
curl -H "X-Auth-User-Token: Auth_Type ${Token}" -XDELETE  METRICS_ENDPOINT/v1/metrics/list?query=metric-service.*
```
{: screen}

Em que
	
* O *X-Auth-User-Token* é um parâmetro que passa o token do UAA do {{site.data.keyword.Bluemix_notm}}.
	
* Auth_Type é o prefixo que define o tipo de token. Os valores válidos são: *uaa* para um token do UAA, *iam* para um token do IAM e *api* para uma chave API.
	
* *X-Auth-Scope-Id* é um parâmetro que passa o GUID de espaço. O GUID deve ser prefixado com *s-* para identificar um espaço.
	
* *Token* representa o token de segurança.
	
* *Espaço* representa o GUID do espaço. 
	
* *METRICS_ENDPOINT* representa o ponto de entrada para o serviço. Cada região possui uma URL diferente. Para obter a lista de terminais por região, consulte [Terminais](/docs/services/cloud-monitoring?topic=cloud-monitoring-send_retrieve_metrics_ov#endpoints).

* *query* define o filtro aplicado. `query=*` indica todas as métricas no domínio.

* *metric-service.** é o nome de um serviço. Por exemplo, `containers-kubernetes`.
