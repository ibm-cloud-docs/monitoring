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


# Concedendo permissões a usuário
{: #grant_permissions}

No {{site.data.keyword.Bluemix}}, é possível designar uma ou mais funções para os usuários. Essas funções definem quais tarefas estão ativadas para esse usuário para trabalhar com o serviço {{site.data.keyword.monitoringshort}}. 
{:shortdesc}

Para conceder permissões a um usuário para trabalhar com métricas, deve-se incluir uma política para esse usuário que descreva as ações que o usuário pode executar com o serviço {{site.data.keyword.monitoringshort}} na conta. Somente proprietários da conta podem designar políticas individuais para usuários.


## Designando a um usuário uma política do IAM por meio da UI do IBM Cloud 
{: #assign_policy_ui}

Conclua as etapas a seguir para conceder permissões a um usuário para trabalhar com o serviço {{site.data.keyword.monitoringshort}}:

1. Efetue login no console do {{site.data.keyword.Bluemix_notm}}.

    Abra um navegador da web e ative o painel do {{site.data.keyword.Bluemix_notm}}: [http://console.bluemix.net ![External link icon](../../../icons/launch-glyph.svg "External link icon")](http://bluemix.net){:new_window}
	
	Após você efetuar login com o seu ID do usuário e senha, a UI do {{site.data.keyword.Bluemix_notm}} será aberta.

2. Na barra de menus, clique em **Gerenciar > Conta > Usuários**. 

    A janela *Usuários* exibe uma lista de usuários com seus endereços de e-mail para a conta selecionada atualmente.
	
3. Se o usuário é um membro da conta, selecione o nome do usuário na lista ou clique em **Gerenciar usuário** no menu *Ações*.

    Se o usuário não é um membro da conta, veja [Convidando usuários](/docs/iam/iamuserinv.html#iamuserinv).

4. Clique em **Designar políticas de serviço**.

5. Insira informações sobre a política. A tabela a seguir lista os campos que são necessários ou opcionais para definir uma política: 

    <table>
	  <caption>Lista de campos para configurar uma política do IAM.</caption>
	  <tr>
	    <th>Campo</th>
		<th>Valor</th>
		<th>Status</th>
	  </tr>
	  <tr>
	    <td>serviço</td>
		<td>{{site.data.keyword.monitoringlong}}</td>
		<td>Exigido</td>
	  </tr>
	  <tr>
	    <td>Funções</td>
		<td>Selecione uma ou mais funções do IAM. <br>As funções válidas são: *administrador*, *operador*, *editor* e *visualizador*. <br>Para obter mais informações sobre as ações que são permitidas por função, veja [Funções do IAM](/docs/services/cloud-monitoring/security_ov.html#iam_roles).</td>
		<td>Exigido</td>
	  </tr>
	  <tr>
	    <td>Regiões</td>
		<td>É possível especificar as regiões nas quais o acesso será concedido ao usuário para trabalhar com métricas. Selecione **Especificar contexto do serviço opcional**. Em seguida, inclua uma ou mais regiões individualmente ou selecione **Todas as regiões atuais** para conceder acesso a todas as regiões.</td>
		<td>Opcional</td>
	  </tr>
	</table>
	
6. Clique em **Designar política**.
	
A política que você configura é aplicável às regiões selecionadas. 

## Designando um usuário a uma política do IAM usando a linha de comandos
{: #assign_policy_commandline}

Conclua as etapas a seguir para conceder acesso a um usuário para visualizar métricas usando a linha de comandos:

1. (Pré-requisito) Instale a CLI do {{site.data.keyword.Bluemix_notm}}.

   Para obter mais informações, veja [Instalando a CLI do {{site.data.keyword.Bluemix_notm}}](/docs/cli/index.html#overview).
   
   Se a CLI estiver instalada, continue com a próxima etapa.
	
2. Efetue login em uma região, uma organização e um espaço no {{site.data.keyword.Bluemix_notm}}. 

    Para obter mais informações, veja [Como efetuar login no {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login).
	
3. Obtenha o ID da conta. 

    Execute o comando a seguir para obter o ID da conta:

    ```
	contas do ibmcloud iam
	```
    {: codeblock}	

	Uma lista de contas com seus GUIDs é exibida.
	
	Exporte o ID da conta na qual você planeja conceder permissões a um usuário. Configure uma variável shell, como `$acct_id`, por exemplo:
	
	```
	export acct_id="1234567891234567812341234123412"
	```
	{: screen}

4. Obtenha o ID da {{site.data.keyword.IBM_notm}} do usuário para quem você deseja conceder permissões.

    1. Exiba os usuários associados à conta. Execute o seguinte comando:
	
	    ```
		ibmcloud iam account-users
		```
		{: codeblock}
		
	2. Obtenha o GUID do usuário. **Nota: esta etapa deve ser concluída pelo usuário para o qual você planeja conceder permissões.**
	
	    Por exemplo, solicite ao usuário para executar os comandos a seguir para obter o ID do usuário:
		
		Obtenha o token do IAM. Para obter mais informações, consulte [Obtendo o token do IAM usando a CLI do {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security/auth_iam.html#iam_token_cli).

        Obtenha os dados do token do IAM que estão entre os primeiros 2 pontos no token do IAM. Exporte os dados para uma variável shell, como `$user_data`. 
		
		```
	    export user_data="xxxxxxxxxxxxxxxxxxxxxxxxxxx"
	    ```
	    {: screen}
		
		Execute o comando a seguir, por exemplo, para obter o ID do usuário. Este comando usa jq nessa amostra para decodificar as informações em texto formatado JSON:
		
		```
		echo $user_data | base64 -d | jq
		```
		{: codeblock}
		
		A saída da execução desse comando é a seguinte:
		
		```
		$ echo $user_data | base64 -d | jq
        {
        "iam_id": "IBMid-xxxxxxxxxx",
        "id": "IBMid-xxxxxxxxxx",
        "realmid": "IBMid",
        ......
		}
        ```
	    {: screen}
		
		Envie o ID do usuário, que é o valor do campo *id* para o proprietário da conta. 
		
	3. Exporte o ID do usuário para uma variável shell como `$user_ibm_id`.
	
		```
		export user_ibm_id="IBMid-xxxxxxxxxx"
		```
		{: codeblock}

3. Convide o usuário para a conta se ele ainda não for um membro. Para obter mais informações, veja [Convidando usuários](/docs/iam/iamuserinv.html#iamuserinv).

    Por exemplo, execute o comando a seguir para convidar o usuário xxx@yyy.com para a conta zzz@ggg.com:
	
	```
	ibmcloud iam account-user-invite xxx@yyy.com zzz@ggg.com OrgAuditor dev SpaceDeveloper
	```
	{: codeblock}
		
4. Crie um nome do arquivo de políticas. 

    Por exemplo, use o modelo a seguir para conceder permissões de visualização na região Sul dos EUA:
	
	```
	{
		"roles" : [
			{
				"id": "crn:v1:bluemix:public:iam::::role:Editor" 
			}
		],
		"resources": [
			{
				"serviceName": "ibmcloud-monitoring",
				"region": "us-south"
			}
		]
	}
	```
	{: codeblock}
	
	Nomeie o arquivo de políticas: `policy.json`
	
5. Obtenha o token do IAM para seu ID do usuário.

    Para obter mais informações, consulte [Obtendo o token do IAM usando a CLI do {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/security/auth_iam.html#iam_token_cli).

    Exporte o token do IAM para uma variável shell como `$iam_token`, por exemplo:
	
	```
	export iam_token="xxxxxxxxxxxxxxxxxxxxx"
	```
	{: screen}
	
6. Conceda ao usuário permissões para trabalhar com o serviço {{site.data.keyword.monitoringshort}}. 

   Execute o comando cURL a seguir para conceder permissões na região Sul dos EUA:
	
    ```
	curl -X POST --header "Authorization: $iam_token" --header "Content-Type: application/json" https://iampap.ng.bluemix.net/acms/v1/scopes/a%2F$acct_id/users/$user_ibm_id/policies -d @policy.json
	```
	{: codeblock}
	
	Execute o comando cURL a seguir para conceder permissões na região do Reino Unido:
	
    ```
	curl -X POST --header "Authorization: $iam_token" --header "Content-Type: application/json" https://iampap.eu-gb.bluemix.net/acms/v1/scopes/a%2F$acct_id/users/$user_ibm_id/policies -d @policy.json
	```
	{: codeblock}

	





## Concedendo a um usuário uma função do CF por meio da IU do IBM Cloud 
{: #grant_permissions_ui_space}


Para trabalhar com métricas no domínio de espaço ou no domínio da organização, um usuário deve ter uma função do Cloud Foundry (CF) designada no {{site.data.keyword.Bluemix_notm}}. Uma função CF descreve as ações que um usuário pode executar com o serviço {{site.data.keyword.monitoringshort}} em um espaço ou em uma organização. 

Conclua as etapas a seguir para conceder permissões a um usuário para trabalhar com o serviço {{site.data.keyword.monitoringshort}}:

1. Efetue login no console do {{site.data.keyword.Bluemix_notm}}.

    Abra um navegador da web e ative o painel do {{site.data.keyword.Bluemix_notm}}: [http://bluemix.net ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](http://bluemix.net){:new_window}
	
	Após você efetuar login com o seu ID do usuário e senha, a UI do {{site.data.keyword.Bluemix_notm}} será aberta.

2. Na barra de menus, clique em **Gerenciar > Conta > Usuários**. 

    A janela *Usuários* exibe uma lista de usuários com seus endereços de e-mail para a conta selecionada atualmente.
	
3. Se o usuário é um membro da conta, selecione o nome do usuário na lista ou clique em **Gerenciar usuário** no menu *Ações*.

    Se o usuário não é um membro da conta, veja [Convidando usuários](/docs/iam/iamuserinv.html#iamuserinv).

4. Clique em  ** Designar organização **.

5. Insira informações sobre a política. A tabela a seguir lista os campos que são necessários ou opcionais para definir uma política: 

    <table>
	  <caption>Lista de campos para configurar uma política CF.</caption>
	  <tr>
	    <th>Campo</th>
		<th>Valor</th>
	  </tr>
	  <tr>
	    <td>Organização</td>
		<td>Escolha uma organização na lista.</td>
	  </tr>
	  <tr>
	    <td>Funções de organização</td>
		<td>Selecione  ** Nenhuma função de organização **. No entanto, se o usuário tiver uma função organizacional, escolha uma função de organização na lista. <br>Os valores válidos são: **Billing manager**, **Auditor**, **Manager**</td>
	  </tr>
	  <tr>
	    <td>Região</td>
		<td>Escolha uma região na lista. <br>Os valores válidos são: **All current regions**, **US South**, **United Kingdom**</td>
	  </tr>
	  <tr>
	    <td>Espaço</td>
		<td>Por padrão, **Todos os espaços atuais** é predefinido quando o campo *Região* está configurado como **Todas as regiões atuais**. Para conceder permissão para um espaço individual, escolha uma região específica e, em seguida, escolha um espaço na lista.</td>
	  </tr>
	  <tr>
	    <td>Funções de espaço</td>
		<td>Escolha uma função de espaço na lista. <br>Os valores válidos são: **Manager**, **Auditor**, **Developer** e **No space role**. Para obter mais informações, consulte [Funções do Cloud Foundry](/docs/services/cloud-monitoring/security_ov.html#bmx_roles).</td>
	  </tr>
	</table>
	
6. Clique em **Designar política**.
	
A política que você configura é aplicável às regiões selecionadas. 


