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


# Notificações do CRUD
{: #notifications}

Use a API Alerts para criar, excluir e atualizar uma notificação, para mostrar os detalhes de uma
notificação e para listar as notificações que são definidas em um espaço.
{:shortdesc}

## Criando uma Notificação
{: #notifications_create}

Para criar uma notificação, conclua as etapas a seguir:

1. Crie um arquivo de notificação.

    1. Use um modelo de notificação para criar um arquivo de notificação. Para obter mais informações, consulte [Modelos de notificação](/docs/services/cloud-monitoring/config_alerts_ov.html#notification_template).
	
	2. Atualize o arquivo:
	
	    * Insira um nome exclusivo no campo *name*. O valor desse campo é usado posteriormente para atualizar, excluir e mostrar os detalhes da notificação.
		* Digite uma descrição.
		* Insira um endereço de e-mail válido, uma URL de terminal ou a chave PagerDuty.
		
	3. Salve o arquivo. Por exemplo, use um prefixo como *s-* para notificações que você
define para as consultas em execução em um espaço.
	
	    **Dica:** crie seu arquivo de notificação no seguinte diretório: *~/cloud-monitoring/notifications/* para agrupar os recursos do serviço {{site.data.keyword.monitoringshort_notm}}. 
	
	4. Exporte a variável *NOTIFICATION_FILE*:
	
	```
	export NOTIFICATION_FILE="mynotificationfile.json"
	```
	{: screen}
	
2. Efetue login em uma região, uma organização e um espaço no {{site.data.keyword.Bluemix_notm}}. 

    Para obter mais informações, veja [Como efetuar login no {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login).

3. Obtenha o token de segurança. É possível usar um token do UAA, um token do IAM ou uma chave API. Escolha um dos métodos a seguir para obter o token de segurança:
	
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
	IAM token: Bearer djn.._l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ UAA token: Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	Em seguida, exporte a variável *Token*:
	
	```
	export Token="djn .. _l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ "
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
	
5. Registre uma notificação com o serviço {{site.data.keyword.monitoringshort}}.

    ```
	curl -XPOST -d @$NOTIFICATION_FILE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notification
	```
	{: codeblock}
	
	Em que
	
	* NOTIFICATION_FILE é o arquivo JSON que define a sua notificação.
	
	* O *X-Auth-User-Token* é um parâmetro que passa o token do UAA do {{site.data.keyword.Bluemix_notm}}, o token do IAM ou a chave API.
	
	* *Auth_Type* é o prefixo que define o tipo de token ou a chave API. A lista a seguir descreve os valores válidos: *apikey*, *iam* ou *uaa*, em que

        * *apikey* identifica que o token é uma chave API.
		* *iam* identifica que o token especificado é um token gerado pelo IAM.
		* *uaa* identifica que o token especificado é um token gerado pelo UAA
	
	* *X-Auth-Scope-Id* é um parâmetro que passa o GUID de espaço. O GUID deve ser prefixado com *s-* para identificar um espaço. Esse cabeçalho será necessário se você usar uma autenticação do token UAA. Se você usar um token de autenticação IAM, esse cabeçalho será opcional e as informações de domínio ligadas ao token serão usadas.
	
	* Token é o token do UAA, o token do IAM ou a chave API.
	
	* Espaço é o GUID do espaço. 
	
	* METRICS_ENDPOINT representa o ponto de entrada para o serviço. Cada região possui uma URL diferente. Para obter a lista de terminais por região, consulte [Terminais](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).
	
    Por exemplo, 	
	
	```
	curl -XPOST -d @$NOTIFICATION_FILE  --header "X-Auth-User-Token: iam ${Token}" https://metrics.ng.bluemix.net/v1/alert/notification
	```
	{: screen}

## Excluindo uma Notificação
{: #notifications_delete}

Para excluir uma notificação, conclua as etapas a seguir:

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
	IAM token: Bearer djn.._l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ UAA token: Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	Em seguida, exporte a variável *Token*:
	
	```
	export Token="djn .. _l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ "
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
	
4. Execute o comando cURL a seguir para excluir uma notificação:

    ```
	curl -XDELETE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notification/Notification_Name
	```
	{: codeblock}
	
	Em que
	
	* O *X-Auth-User-Token* é um parâmetro que passa o token do UAA, o token do IAM ou a chave API.
	
	* *Auth_Type* é o prefixo que define o tipo de token ou a chave API. A lista a seguir descreve os valores válidos: *apikey*, *iam* ou *uaa*, em que

        * *apikey* identifica que o token é uma chave API.
		* *iam* identifica que o token especificado é um token gerado pelo IAM.
		* *uaa* identifica que o token especificado é um token gerado pelo UAA
	
	* O *X-Auth-User-Token* é um parâmetro que passa o token do UAA do {{site.data.keyword.Bluemix_notm}}, o token do IAM ou a chave API. O token ou a chave API devem ter como prefixo um dos valores a seguir: *apikey*, *iam* ou *uaa*, em que

        * *apikey* identifica que o token é uma chave API.
		* *iam* identifica que o token especificado é um token gerado pelo IAM.
		* *uaa* identifica que o token especificado é um token gerado pelo UAA
		
	* Token é o token do UAA, o token do IAM ou a chave API.
	
	* Espaço é o GUID do espaço. 
	
	* Notification_Name é o nome da notificação, ou seja, o valor do campo *name* quando você lista as propriedades de uma notificação.
	
	* METRICS_ENDPOINT representa o ponto de entrada para o serviço. Cada região possui uma URL diferente. Para obter a lista de terminais por região, consulte [Terminais](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).
	


## Listando todas as notificações
{: #notifications_list}

Para listar todas as notificações, conclua as etapas a seguir:

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
	IAM token: Bearer djn.._l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ UAA token: Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	Em seguida, exporte a variável *Token*:
	
	```
	export Token="djn .. _l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ "
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
	
4. Execute o comando cURL a seguir para listar todas as notificações:

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notifications
	```
	{: codeblock}
	
	Em que
	
	* O *X-Auth-User-Token* é um parâmetro que passa o token do UAA do {{site.data.keyword.Bluemix_notm}}, o token do IAM ou a chave API.
	
	* *Auth_Type* é o prefixo que define o tipo de token ou a chave API. A lista a seguir descreve os valores válidos: *apikey*, *iam* ou *uaa*, em que

        * *apikey* identifica que o token é uma chave API.
		* *iam* identifica que o token especificado é um token gerado pelo IAM.
		* *uaa* identifica que o token especificado é um token gerado pelo UAA
		
	* O *X-Auth-User-Token* é um parâmetro que passa o token do UAA do {{site.data.keyword.Bluemix_notm}}, o token do IAM ou a chave API. O token ou a chave API devem ter como prefixo um dos valores a seguir: *apikey*, *iam* ou *uaa*, em que

        * *apikey* identifica que o token é uma chave API.
		* *iam* identifica que o token especificado é um token gerado pelo IAM.
		* *uaa* identifica que o token especificado é um token gerado pelo UAA
		
	* Token é o token do UAA, o token do IAM ou a chave API.
	
	* Espaço é o GUID do espaço. 
	
	* METRICS_ENDPOINT representa o ponto de entrada para o serviço. Cada região possui uma URL diferente. Para obter a lista de terminais por região, consulte [Terminais](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).

			

## Mostrando os detalhes de uma notificação
{: #show}


Para mostrar as informações sobre uma notificação, conclua as etapas a seguir:

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
	IAM token: Bearer djn.._l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ UAA token: Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	Em seguida, exporte a variável *Token*:
	
	```
	export Token="djn .. _l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ "
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
	
4. Execute o comando cURL a seguir para mostrar os detalhes de uma notificação:

    ```
	curl -XGET --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notification/NOTIFICATION_NAME
	```
	{: codeblock}
	
	Em que
	
	* O *X-Auth-User-Token* é um parâmetro que passa o token do UAA do {{site.data.keyword.Bluemix_notm}}, o token do IAM ou a chave API.
	
	* *Auth_Type* é o prefixo que define o tipo de token ou a chave API. A lista a seguir descreve os valores válidos: *apikey*, *iam* ou *uaa*, em que

        * *apikey* identifica que o token é uma chave API.
		* *iam* identifica que o token especificado é um token gerado pelo IAM.
		* *uaa* identifica que o token especificado é um token gerado pelo UAA
		
	* Token é o token do UAA, o token do IAM ou a chave API.
	
	* Espaço é o GUID do espaço. 
	
	* NOTIFICATION_NAME é o nome da notificação, ou seja, o valor do campo *name* quando você lista as propriedades de uma notificação.
	
	* METRICS_ENDPOINT representa o ponto de entrada para o serviço. Cada região possui uma URL diferente. Para obter a lista de terminais por região, consulte [Terminais](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).
	
     
		

			
## Testando uma Notificação
{: #test}	
			
Para testar uma notificação, conclua as etapas a seguir:

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
	IAM token: Bearer djn.._l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ UAA token: Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	Em seguida, exporte a variável *Token*:
	
	```
	export Token="djn .. _l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ "
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
	
4. Execute o comando cURL a seguir para testar uma notificação:

    ```
	curl -XPOST --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notification/test/NOTIFICATION_NAME
	```
	{: codeblock}
	
	Em que
	
	* O *X-Auth-User-Token* é um parâmetro que passa o token do UAA do {{site.data.keyword.Bluemix_notm}}, o token do IAM ou a chave API.
	
	* *Auth_Type* é o prefixo que define o tipo de token ou a chave API. A lista a seguir descreve os valores válidos: *apikey*, *iam* ou *uaa*, em que

        * *apikey* identifica que o token é uma chave API.
		* *iam* identifica que o token especificado é um token gerado pelo IAM.
		* *uaa* identifica que o token especificado é um token gerado pelo UAA
	
	* O *X-Auth-User-Token* é um parâmetro que passa o token do UAA do {{site.data.keyword.Bluemix_notm}}, o token do IAM ou a chave API. O token ou a chave API devem ter como prefixo um dos valores a seguir: *apikey*, *iam* ou *uaa*, em que

        * *apikey* identifica que o token é uma chave API.
		* *iam* identifica que o token especificado é um token gerado pelo IAM.
		* *uaa* identifica que o token especificado é um token gerado pelo UAA
		
	* Token é o token do UAA, o token do IAM ou a chave API.
	
	* Espaço é o GUID do espaço. 
	
	* NOTIFICATION_NAME é o nome da notificação, ou seja, o valor do campo *name* quando você lista as propriedades de uma notificação.
	
	* METRICS_ENDPOINT representa o ponto de entrada para o serviço. Cada região possui uma URL diferente. Para obter a lista de terminais por região, consulte [Terminais](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).
	


## Atualizando uma Notificação
{: #notifications_update}

Para atualizar uma notificação, conclua as etapas a seguir:

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
	IAM token: Bearer djn.._l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ UAA token: Bearer eyJhbGciOiJIUz..Ky6vagp3k_QcIcKJ-td83qXhO5Uze43KcplG6PzcGs8
	```
	{: screen}
	
	Em seguida, exporte a variável *Token*:
	
	```
	export Token="djn .. _l_HWtlNTibmcloudslBXs0qjBI9GqCnuQ "
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
	
4. Execute o comando cURL a seguir para atualizar uma notificação:

    ```
	curl -XPUT -d @$NOTIFICATION_FILE --header "X-Auth-User-Token: Auth_Type ${Token}" --header "X-Auth-Scope-Id: ${Space}" METRICS_ENDPOINT/v1/alert/notification
	```
	{: codeblock}
	
	Em que
	
	* NOTIFICATION_FILE é o arquivo JSON que define a sua notificação.
	
	* *Auth_Type* é o prefixo que define o tipo de token ou a chave API. A lista a seguir descreve os valores válidos: *apikey*, *iam* ou *uaa*, em que

        * *apikey* identifica que o token é uma chave API.
		* *iam* identifica que o token especificado é um token gerado pelo IAM.
		* *uaa* identifica que o token especificado é um token gerado pelo UAA
	
	* O *X-Auth-User-Token* é um parâmetro que passa o token do UAA do bluemix, o token do IAM ou a chave API. O token ou a chave API devem ter como prefixo um dos valores a seguir: *apikey*, *iam* ou *uaa*, em que

        * *apikey* identifica que o token é uma chave API.
		* *iam* identifica que o token especificado é um token gerado pelo IAM.
		* *uaa* identifica que o token especificado é um token gerado pelo UAA
		
	* Token é o token do UAA, o token do IAM ou a chave API.
	
	* Espaço é o GUID do espaço. 

	* METRICS_ENDPOINT representa o ponto de entrada para o serviço. Cada região possui uma URL diferente. Para obter a lista de terminais por região, consulte [Terminais](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#endpoints).
	
        

