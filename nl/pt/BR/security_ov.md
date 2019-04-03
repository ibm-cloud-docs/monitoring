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


# Segurança
{: #security_ov}

Para controlar as ações de serviço do {{site.data.keyword.monitoringshort}} que um usuário tem permissão para executar, é possível designar uma ou mais funções a um usuário. Para autenticar um usuário para trabalhar com métricas e alertas, é possível usar um token do UAA, um token do IAM ou uma Chave API. 
{:shortdesc}





## Modelos de Autenticação
{: #auth}

Para trabalhar com métricas que são armazenadas no serviço do {{site.data.keyword.monitoringshort}}
para um espaço, você requer um token de autenticação ou uma chave API. 

Para obter um token de segurança, veja:

* [Obtendo um token do UAA](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_uaa#auth_uaa)
* [Obtendo um token do IAM](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_iam#auth_iam)

Para obter uma chave API, veja [Gerando uma chave API](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_api_key#auth_api_key). Se a chave API estiver comprometida, será possível revogá-la excluindo-a. Em seguida, será possível será possível uma nova. Para obter mais informações, consulte [Revogando uma chave de API usando a IU do {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_api_key#revoke_ui). 

Um token do UAA e um token do IAM expiram após um período de tempo. A chave API não expira. 

A tabela a seguir lista os modelos de segurança que são suportados para cada tipo de domínio:

<table>
  <caption>Tabela 1. Modelos de segurança suportados para cada domínio</caption>
  <tr>
    <th></th>
	<th align="right">Conta</th>
    <th align="right">Organização</th>
    <th align="right">Espaço</th>	
  </tr>
  <tr>
    <th align="left">UAA</th>
	<td align="center">Não</td>
	<td align="center">Sim</td>
	<td align="center">Sim</td>
  </tr>
  <tr>
    <th align="left">IAM</th>
	<td align="center">Sim</td>
	<td align="center">Sim</td>
	<td align="center">Sim</td>
  </tr>
</table>

O serviço {{site.data.keyword.monitoringshort}} usa o recurso de controle de acesso do IAM para controlar quais ações ou operações um usuário ou serviço pode executar em relação ao domínio. Por exemplo, é possível definir uma política do IAM para permitir que um usuário envie e crie painéis em um domínio, mas não para recuperar as métricas do domínio.



## Funções do Cloud Foundry
{: #bmx_roles}

A tabela a seguir lista os privilégios de cada função do Cloud Foundry para trabalhar com o
serviço do {{site.data.keyword.monitoringshort}}:

<table>
  <caption>Tabela 2. Funções e privilégios do Cloud Foundry para trabalhar com o serviço {{site.data.keyword.monitoringshort}}.</caption>
  <tr>
    <th>Atribuição</th>
	<th>Domain</th>
	<th>Privilégios de acesso</th>
  </tr>
  <tr>
    <td>Manager</td>
	<td>Organização <br>Espaço</td>
	<td>Todas as APIs RESTful</td>
  </tr>
  <tr>
    <td>Developer</td>
	<td>Espaço</td>
	<td>Todas as APIs RESTful</td>
  </tr>
  <tr>
    <td>Auditor</td>
	<td>Organização <br>Espaço</td>
	<td>Apenas APIs RESTful que executam operações somente leitura, como as métricas de consulta.</td>
  </tr>
</table>

Para obter informações sobre como designar funções de usuário na IU, consulte [Gerenciando o acesso ao Cloud Foundry](/docs/iam?topic=iam-mngcf#mngcf).



## Funções IAM
{: #iam_roles}

A tabela a seguir lista as ações de serviço do {{site.data.keyword.monitoringshort}} quando você trabalha com métricas e as funções do IAM que concedem permissões a um usuário para executar estas tarefas:

<table>
  <caption>Tabela 3. Trabalhando com métricas </caption>
  <tr>
	<th>Ação</th>
	<th>Função IAM</th>
  </tr>
  <tr>
    <td>Enviar métricas para o domínio</td>
	<td>Administrador, Editor, Operador</td>
  </tr>
  <tr>
    <td>Recuperar / consulta de métricas</td>
	<td>Administrador, Editor, Visualizador</td>
  </tr>
  <tr>
    <td>Procure métricas no domínio</td>
	<td>Administrador, Editor</td>
  </tr>
</table>

A tabela a seguir lista as ações de serviço do {{site.data.keyword.monitoringshort}} quando você trabalha com alertas e as funções do IAM que concedem permissões a um usuário para executar estas tarefas:

<table>
  <caption>Tabela 4. Trabalhando com alertas. </caption>
  <tr>
	<th>Ação</th>
	<th>Função IAM</th>
  </tr>
  <tr>
    <td>Criar, editar e excluir regras de alerta</td>
	<td>Administrador, Editor</td>
  </tr>
  <tr>
    <td>Visualizar alertas</td>
	<td>Administrador, Editor, Visualizador</td>
  </tr>
  <tr>
    <td>Criar, editar e excluir notificações de alerta</td>
	<td>Administrador, Editor</td>
  </tr>
  <tr>
    <td>Visualizar notificações</td>
	<td>Administrador, Editor, Visualizador</td>
  </tr>
  <tr>
    <td>Visualizar registros de histórico de alerta acionado</td>
	<td>Administrador, Editor, Visualizador</td>
  </tr>
</table>

Para obter informações sobre como designar funções de usuário na IU, consulte [Gerenciando o acesso ao IAM](/docs/iam?topic=iam-iammanidaccser#iammanidaccser).

