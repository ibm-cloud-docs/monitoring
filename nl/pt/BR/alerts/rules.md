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


# Regras do CRUD
{: #rules}

Use a API Alerts para criar, excluir ou atualizar uma regra, para mostrar os detalhes de uma regra
e para listar as regras que são definidas em um espaço.
{:shortdesc}


## Criando uma regra
{: #create}

Para configurar uma regra no serviço {{site.data.keyword.monitoringshort}}, crie um arquivo de regras que inclua os detalhes da regra e registre a regra com o serviço {{site.data.keyword.monitoringshort}}.

Conclua as etapas a seguir:

1. Crie um arquivo de regras que contenha JSON válido. Salve o arquivo. 

    Por exemplo, para salvar o arquivo, use um prefixo como *s-* para regras que você
define para as consultas em execução em um espaço.
	
	**Dicas:** 
	
	* Defina regras diferentes para uma consulta a fim de alertar sobre erros ou avisos usando um método de notificação diferente. 
	* Crie seu arquivo de regras no diretório a seguir: *~/cloud-monitoring/rules/* para agrupar os recursos do serviço {{site.data.keyword.monitoringshort_notm}}. 

    Insira as informações a seguir no arquivo de regras:
	
	* *Nome*: Insira um nome exclusivo. O valor desse campo é usado posteriormente para atualizar, excluir e mostrar os detalhes da regra.
	* *Descrição*: Insira uma descrição.
	* *expression*: insira a consulta que você deseja monitorar.
	* *enabled*: configure para *true* para ativar a regra.
	* *from*: momento inicial que é usado para analisar os dados com base nos valores de limite.
	* *until*: momento final que é usado para analisar os dados com base nos valores de limite.
	* *comparison*: a operação de comparação que é usada para identificar o tipo de verificação a ser feita, por exemplo, *below*.
	* *error_level*: define o limite que você configura para acionar um alerta de erro.
	* *warning_level*: define o limite que você configura para acionar um alerta de aviso.
	* *frequency*: define a frequência com que você verifica os dados.
	* *dashboard_url*: define uma URL que mostra um painel com a consulta no Grafana.
	* *notifications*: o método de notificação em caso de alerta descrito com essa regra é acionado.
	
	Por exemplo, o arquivo de regras myrulefile.json é semelhante ao seguinte:
	
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
      "emailXXX"
    ]
    }
    ```
	{: screen}
	
	Em seguida, exporte a variável *RULE_FILE*:
	
	```
	export RULE_FILE="myrulefile.json"
	```
	{: screen}
	
2. Efetue login em uma região, uma organização e um espaço no {{site.data.keyword.Bluemix_notm}}.

    Para obter mais informações, veja [Como efetuar login no {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login).

3. Obtenha o token de segurança. É possível usar um token do UAA, um token do IAM ou uma chave API. Escolha um dos métodos a seguir para obter o token de segurança:
	
	* Para obter um token do UAA, consulte [Obtendo o token do UAA usando a CLI do {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security/auth_uaa.html#uaa_cli.
	
	* Para obter um token do IAM, consulte [Obtendo o token do IAM usando a CLI do {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security/auth_iam.html#auth_iam).
	
	* Para obter uma chave API, consulte [Recebendo uma chave API](/docs/services/cloud-monitoring/security/auth_api_key.html#auth_api_key).
	
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
	
4. Obtenha o GUID do espaço. O GUID deve ser prefixado com *s-* para identificar um espaço.

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
	
5. Execute o comando cURL a seguir para registrar a regra no serviço do {{site.data.keyword.monitoringshort}}:

    ```
	curl -XPOST -d @$RULE_FILE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/rule
	```
	{: codeblock}
	
	Em que
	
	* RULE_FILE é o arquivo JSON que define a sua regra de alerta.
	
	* O *X-Auth-User-Token* é um parâmetro que passa o token do UAA do {{site.data.keyword.Bluemix_notm}}, o token do IAM ou a chave API.
	
	* *Auth_Type* é o prefixo que define o tipo de token ou a chave API. A lista a seguir descreve os valores válidos: *apikey*, *iam* ou *uaa*, em que

        * *apikey* identifica que o token é uma chave API.
		* *iam* identifica que o token especificado é um token gerado pelo IAM.
		* *uaa* identifica que o token especificado é um token gerado pelo UAA
	
	* *X-Auth-Scope-Id* é um parâmetro que passa o GUID de espaço. O GUID deve ser prefixado com *s-* para identificar um espaço. Esse cabeçalho será necessário se você usar uma autenticação do token UAA. Se você usar um token de autenticação IAM, esse cabeçalho será opcional e as informações de domínio ligadas ao token serão usadas.
	
	* Token é o token de autenticação do UAA ou do IAM ou a chave API.
	
	* Espaço é o GUID do espaço. 
	
	* METRICS_ENDPOINT representa o ponto de entrada para o serviço. Cada região possui uma URL diferente. Para obter a lista de terminais por região, consulte [Terminais](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).
	
    Por exemplo, 	
	
	```
	curl -XPOST -d @$RULE_FILE --header "X-Auth-User-Token:iam ${Token}" https://metrics.ng.bluemix.net/v1/alert/rule
	```
	{: screen}

## Excluindo uma Regra
{: #delete}

Para excluir uma regra, conclua as etapas a seguir:

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
		
4. Execute o comando cURL a seguir para excluir uma regra:

    ```
	curl -XDELETE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/rule/Rule_Name
	```
	{: codeblock}
	
	Em que
	
    * O *X-Auth-User-Token* é um parâmetro que passa o token do UAA, o token do IAM ou a chave API.
	
	* *Auth_Type* é o prefixo que define o tipo de token ou a chave API. A lista a seguir descreve os valores válidos: *apikey*, *iam* ou *uaa*, em que

        * *apikey* identifica que o token é uma chave API.
		* *iam* identifica que o token especificado é um token gerado pelo IAM.
		* *uaa* identifica que o token especificado é um token gerado pelo UAA
	
	* *X-Auth-Scope-Id* é um parâmetro que passa o GUID de espaço. O GUID deve ser prefixado com *s-* para identificar um espaço. Esse cabeçalho será necessário se você usar uma autenticação do token UAA. Se você usar um token de autenticação IAM, esse cabeçalho será opcional e as informações de domínio ligadas ao token serão usadas.
	
	* Token é o token de autenticação do UAA ou do IAM ou a chave API.
	
	* Espaço é o GUID do espaço. 
	
	* Rule_Name é o nome da regra conforme especificado no campo *name*.
	
	* METRICS_ENDPOINT representa o ponto de entrada para o serviço. Cada região possui uma URL diferente. Para obter a lista de terminais por região, consulte [Terminais](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).
	
    
	
## Listando todas as regras
{: #list}

Para listar todas as regras, conclua as etapas a seguir:

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
	
4. Execute o comando cURL a seguir para listar todas as regras em um espaço:

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/rules
	```
	{: codeblock}
	
	Em que
	
	* O *X-Auth-User-Token* é um parâmetro que passa o token do UAA, o token do IAM ou a chave API.
	
	* *Auth_Type* é o prefixo que define o tipo de token ou a chave API. A lista a seguir descreve os valores válidos: *apikey*, *iam* ou *uaa*, em que

        * *apikey* identifica que o token é uma chave API.
		* *iam* identifica que o token especificado é um token gerado pelo IAM.
		* *uaa* identifica que o token especificado é um token gerado pelo UAA
	
	* *X-Auth-Scope-Id* é um parâmetro que passa o GUID de espaço. O GUID deve ser prefixado com *s-* para identificar um espaço. Esse cabeçalho será necessário se você usar uma autenticação do token UAA. Se você usar um token de autenticação IAM, esse cabeçalho será opcional e as informações de domínio ligadas ao token serão usadas.
	
	* Token é o token de autenticação do UAA ou do IAM ou a chave API.
	
	* Espaço é o GUID do espaço. 
	
	* METRICS_ENDPOINT representa o ponto de entrada para o serviço. Cada região possui uma URL diferente. Para obter a lista de terminais por região, consulte [Terminais](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).
	

	
	

## Mostrando os Detalhes de uma Regra
{: show}

Para mostrar os detalhes de uma regra, conclua as etapas a seguir:

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
	
4. Execute o comando cURL a seguir para mostrar os detalhes de uma regra:

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/rule/Rule_Name
	```
	{: codeblock}
	
	Em que
	
	* O *X-Auth-User-Token* é um parâmetro que passa o token do UAA, o token do IAM ou a chave API.
	
	* *Auth_Type* é o prefixo que define o tipo de token ou a chave API. A lista a seguir descreve os valores válidos: *apikey*, *iam* ou *uaa*, em que

        * *apikey* identifica que o token é uma chave API.
		* *iam* identifica que o token especificado é um token gerado pelo IAM.
		* *uaa* identifica que o token especificado é um token gerado pelo UAA
	
	* *X-Auth-Scope-Id* é um parâmetro que passa o GUID de espaço. O GUID deve ser prefixado com *s-* para identificar um espaço. Esse cabeçalho será necessário se você usar uma autenticação do token UAA. Se você usar um token de autenticação IAM, esse cabeçalho será opcional e as informações de domínio ligadas ao token serão usadas.
	
	* Token é o token de autenticação do UAA ou do IAM ou a chave API.
	
	* Espaço é o GUID do espaço. 
	
	* Rule_Name é o nome da regra conforme especificado no campo *name*.
	
	* METRICS_ENDPOINT representa o ponto de entrada para o serviço. Cada região possui uma URL diferente. Para obter a lista de terminais por região, consulte [Terminais](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).
	

## Atualizando uma Regra
{: #update}

Para atualizar uma regra, atualize o arquivo de regras para modificá-la e, em seguida, conclua as etapas a seguir:

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
	
4. Execute o comando cURL a seguir para atualizar uma regra:

    ```
	curl -XPUT `-d @$RULE_FILE` --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/rule
	```
	{: codeblock}
	
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

	
	
