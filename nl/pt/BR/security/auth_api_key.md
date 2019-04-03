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


# Trabalhando com chaves API
{: #auth_api_key}

É possível obter uma API usando a CLI do {{site.data.keyword.Bluemix}} ou a UI do {{site.data.keyword.Bluemix_notm}}. A chave API não expira. Se uma API estiver comprometida, será possível revogá-la e gerar uma nova.
{:shortdesc}

## Gerando uma chave API do IAM usando a CLI do IBM Cloud
{: #iam_apikey_cli}

Conclua as etapas a seguir para gerar uma chave API usando a CLI do {{site.data.keyword.Bluemix_notm}}:

1. (Pré-requisito) Instale a CLI do {{site.data.keyword.Bluemix_notm}}.

   Para obter mais informações, consulte [Instalando a CLI do {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#cli_qa).
   
   Se a CLI estiver instalada, continue com a próxima etapa.
	
2. Efetue login em uma região, uma organização e um espaço no {{site.data.keyword.Bluemix_notm}}. 

    Para obter mais informações, veja [Como efetuar login no {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login).
 
3. Execute o comando `ibmcloud iam api-key-create` para criar uma chave API.

    ```
    ibmcloud iam api-key-create NAME [-d DESCRIPTION][-f, --file FILE]
	```
	{: codeblock} 
	
	Em que
	
	* NAME é o nome da chave API a ser criada.
	* DESCRIPTION é o texto usado para descrever a chave API.
	* FILE é o nome do arquivo no qual a chave é salva.
	
    Por exemplo, para criar uma chave API *MyKey*, execute o comando a seguir:
	
	```
	ibmcloud iam api-key-create MyKey -d "This is my API key for service X" 
	```
	{: screen}
	
	
	
	
## Gerando uma chave API do IAM usando a IU do IBM Cloud
{: #iam_apikey_ui}

Conclua as etapas a seguir para gerar uma chave API por meio da IU do {{site.data.keyword.Bluemix_notm}}:

1. Efetue login no console do {{site.data.keyword.Bluemix_notm}}.

    Abra um navegador da web e ative o painel do {{site.data.keyword.Bluemix_notm}}: [http://console.bluemix.net ![External link icon](../../../icons/launch-glyph.svg "External link icon")](http://bluemix.net){:new_window}
	
	Após você efetuar login com o seu ID do usuário e senha, a UI do {{site.data.keyword.Bluemix_notm}} será aberta.

2. Na barra de menus do console, clique em **Gerenciar > Segurança > Chaves API do IBM Cloud**.

3. Clique em  ** Criar chave de API **.

4. Insira um nome e uma descrição para sua chave API. Em seguida, clique em  ** Criar chave de API **.

5. Salve a chave de API. Clique em  ** Fazer download da chave de API **.

    Clique em **Mostrar** para exibir a chave API.  

**Nota:** a chave API está disponível apenas para mostrar ou fazer download no momento da criação. Se a chave API for perdida, uma nova chave API deverá ser criada.  


	
## Revogando uma chave API usando a IU do IBM Cloud
{: #revoke_ui}
	
Conclua as etapas a seguir para revogar uma chave API do IAM por meio da IU do {{site.data.keyword.Bluemix_notm}}

1. Efetue login no console do {{site.data.keyword.Bluemix_notm}}.

    Abra um navegador da web e ative o painel do {{site.data.keyword.Bluemix_notm}}: [http://console.bluemix.net ![External link icon](../../../icons/launch-glyph.svg "External link icon")](http://bluemix.net){:new_window}
	
	Após você efetuar login com o seu ID do usuário e senha, a UI do {{site.data.keyword.Bluemix_notm}} será aberta.

2. Na barra de menus do console, clique em **Gerenciar > Segurança > Chaves API do IBM Cloud**.

3. Clique em **Ações** e, em seguida, em **Excluir chave**.





	

	
	
	
	
	
	
