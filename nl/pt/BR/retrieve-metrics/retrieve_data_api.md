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

# Recuperando métricas
{: #retrieve_data_api}

É possível recuperar métricas por meio do serviço do {{site.data.keyword.monitoringshort}} usando [a API de Métricas](https://console.bluemix.net/apidocs/927-ibm-cloud-monitoring-rest-api?&language=node#introduction){: new_window}.
{:shortdesc}


## Recuperando métricas de um espaço
{: #uaa}

Para recuperar métricas de um espaço, conclua as etapas a seguir:

1. Efetue login em uma região, uma organização e um espaço no {{site.data.keyword.Bluemix_notm}}. 

    Para obter mais informações, veja [Como efetuar login no {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login).

2. Configure o token de segurança ou a chave API
  
    Deve-se configurar o campo **X-Auth-User-Token** com um token de segurança ou
chave API. É possível usar um token do UAA, um token do IAM ou uma chave API.

    Primeiramente, escolha um dos métodos a seguir para obter o token de segurança que você precisa
para enviar métricas:
	
    * Para obter um token do UAA, consulte [Obtendo o token do UAA usando a CLI do {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security/auth_uaa.html#uaa_cli).
    
	* Para obter um token do IAM, consulte [Obtendo o token do IAM usando a CLI do {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security/auth_iam.html#auth_iam).
    
	* Para obter uma chave API, consulte
[Obtendo uma chave
API](/docs/services/cloud-monitoring/security/auth_api_key.html#auth_api_key). 

    Um token ou uma chave API deve ser prefixada com um dos valores a seguir: `apikey`, `iam` ou `uaa` 

    Em que 

    * *apikey* identifica que o token é uma chave API.
    * *iam* identifica que o token especificado é um token gerado pelo IAM.
    * *uaa* identifica que o token especificado é um token gerado pelo UAA.

    Por exemplo, é possível configurar o cabeçalho a seguir para uma chave API: `X-Auth-User-Token: apikey SomeIAMGeneratedKey`
	
	Em seguida, no mesmo terminal em que você efetuou login no
{{site.data.keyword.Bluemix_notm}}, configure a variável do Token para o token.

    Por exemplo, configure um token do UAA e remova a parte *Bearer* do valor do token:

    ```
    export Token="kjshdgf.....ldkdjdj"
    ```
    {: screen}
		
3. Obtenha o ID do espaço.

    Para recuperar métricas, o campo de cabeçalho **X-Auth-Scope-Id** é obrigatório
e deve ser configurado para o GUID do espaço. 

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

4. Execute o comando cURL a seguir para enviar métricas:

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/metrics?from=Start_Time&until=End_Time&target=string
	```
	{: codeblock}

	Em que
	
	* O *X-Auth-User-Token* é um parâmetro que passa o token do UAA do {{site.data.keyword.Bluemix_notm}}.
	
	* Auth_Type é o prefixo que define o tipo de token. Os valores válidos são: *uaa* para um token do UAA, *iam* para um token do IAM e *api* para uma chave API.
	
	* *X-Auth-Scope-Id* é um parâmetro que passa o GUID de espaço. O GUID deve ser prefixado com *s-* para identificar um espaço. Esse cabeçalho será necessário apenas se você usar a autenticação de UAA. Se você usar um token de autenticação IAM, esse cabeçalho será opcional e as informações de domínio ligadas ao token serão usadas.
	
	* *Token* representa o token de segurança.
	
	* *Espaço* representa o GUID do espaço. 
	
	* *Start_Time* define o início da solicitação. Essas informações são usadas para calcular o período de
tempo relativo ou absoluto. *End_Time* define o término da solicitação. Essas informações são usadas para calcular o período de
tempo relativo ou absoluto. Para obter mais informações, consulte [Configurando um período de tempo](/docs/services/cloud-monitoring/retrieve-metrics/retrieve_data_api.html#time).
	
	* *Path* identifica uma ou várias métricas. É possível, opcionalmente, aplicar funções em cada métrica. Caminhos também suportam curingas, o que permite que você identifique mais de uma métrica em um único caminho. Para obter mais informações, veja [Definindo as métricas](/docs/services/cloud-monitoring/retrieve-metrics/retrieve_data_api.html#metrics).
	
	* *METRICS_ENDPOINT* representa o ponto de entrada para o serviço. Cada região possui uma URL diferente. Para obter a lista de terminais por região, consulte [Terminais](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).
	

	
## Definindo métricas
{: #metrics}

Para recuperar dados para uma métrica, deve-se especificar o caminho da métrica da raiz da árvore de métricas até a métrica e deve-se separar cada etapa com um ponto (.).

O caminho é especificado no parâmetro **Target**. Um máximo de 5 destinos pode ser especificado por solicitação.  

É possível, opcionalmente, aplicar funções na métrica. Para obter mais informações sobre funções suportadas, veja [Funções do Graphite 0.9.15![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](http://graphite.readthedocs.io/en/latest/functions.html).

É possível usar curingas para definir um caminho. Usando curingas, é possível identificar mais de uma métrica em um único caminho. 

* **Asterisco**: é possível usar um asterisco (*) para corresponder zero ou mais caracteres. 

    É possível ter mais de um asterisco dentro de um único elemento de caminho, por exemplo: `servers.sp*aeg*r.cpu.total.*` Esse exemplo retorna dados sobre o total de CPU para todos os servidores que correspondem ao padrão.

* **Lista ou intervalo de caracteres**: é possível definir os caracteres entre colchetes ([...]) para especificar um único caractere na posição da sequência de caminho. 

    É possível definir um intervalo inclusivo de caracteres especificando dois caracteres separados por um hífen (-). Qualquer caractere entre esses dois caracteres corresponderá. 
	
	É possível definir um ou mais intervalos de caracteres entre colchetes. 
	
	Quando não for possível ler os caracteres entre um conjunto de colchetes como um intervalo, eles serão tratados como uma lista de valores. 
	
	É possível incluir um hífen (-) como um caractere em uma lista de valores colocando-o no início ou término entre colchetes.

* **Lista de valores**: é possível configurar valores separados por vírgula dentro de chaves para definir listas de valores. 

    Por exemplo, para fazer download de métricas para os caminhos a seguir: `servers.myserver.cpu.total.user` e `servers.myserver.cpu.total.system`, é possível configurar um único caminho para ambos os tipos: `servers.myserver.cpu.total.{user,system}`



## Configurando um período de tempo
{: #time}

É possível, opcionalmente, especificar um período de tempo usando um tempo relativo ou um tempo absoluto. Deve-se definir os parâmetros de consulta **From** e **Until**.  

* Quando o horário de início do período de tempo for omitido, o valor padrão será 24 horas atrás. 

* Quando o horário de encerramento do período de tempo for omitido, o valor padrão será o horário atual *agora*.

O **Tempo relativo** é sempre precedido por um sinal de menos (-) e seguido por uma unidade de tempo. 

A tabela a seguir lista as diferentes abreviações de tempo relativo que podem ser usadas:


| Abreviação | Descrição |
|--------------|-------------|
| s            | Segundos     |
| mínimo          | Minutos     |
| h            | Horas       |
| D            | Dias        |
| w            | Semanas       |
| Seg          | Meses      |
| agora          | Hora Atual |


É possível usar qualquer um dos formatos a seguir para definir um **Tempo absoluto**: `HH:MM_YYMMDD`, `YYYYMMDD`, `MM/DD/YY`

| Abreviação | Descrição |
|--------------|-------------|
| YYYY         | Ano com quatro dígitos |
| MM           | Dois dígitos de mês (01=Jan etc) |
| DD           | Dois dígitos de dia do mês (01 até 31) |
| hh           | Dois dígitos de hora (00 até 23) |
| mm           | Dois dígitos de minuto (00 até 59) |
| ss           | Dois dígitos de segundo (00 até 59) |

**Exemplo**

A tabela a seguir mostra diferentes exemplos de como configurar diferentes períodos de tempo, configurando os parâmetros *from* e *until*:

<table>
  <caption>Tabela 1. Exemplos diferentes que mostram como configurar períodos de tempo diferentes, configurando os parâmetros *from* e *until*</caption>
  <tr>
    <th>Exemplo</th>
	<th>Descrição</th>
  </tr>
  <tr>
    <td>&from=monday</td>
	<td>Período de tempo que inclui dados de segunda-feira passada até agora.</td>
  </tr>
  <tr>
    <td>&from=20171101&until=20171130</td>
	<td>Período de tempo configurado para um mês, por exemplo, novembro </td>
  </tr>
  <tr>
    <td>&from=02:00_20170701&until=14:00_20170701</td>
	<td>Para mostrar dados em um ciclo de 24 horas, por exemplo, das 02h às 14h no dia 1 de julho de 2017</td>
  </tr>
  <tr>
    <td>&from=-8d&until=-7d</td>
	<td>Para mostrar o mesmo dia da semana, por exemplo, na semana passada</td>
  </tr>
  
</table>


