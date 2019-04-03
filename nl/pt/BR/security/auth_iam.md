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


# Obtendo um token do IAM
{: #auth_iam}

Use o modelo IAM do {{site.data.keyword.Bluemix}} para obter um token de autenticação que pode ser usado para trabalhar com o serviço {{site.data.keyword.monitoringshort}}. É possível obter o token de autenticação usando a CLI do {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

O token tem um tempo de expiração. 

## Obtendo o token do IAM usando a CLI do IBM Cloud 
{: #iam_token_cli}

Para obter o token de autorização usando a CLI do {{site.data.keyword.Bluemix_notm}}, conclua as etapas a seguir:

1. (Pré-requisito) Instale a CLI do {{site.data.keyword.Bluemix_notm}}.

   Para obter mais informações, veja [Instalando a CLI do {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#cli_qa).
   
   Se a CLI estiver instalada, continue com a próxima etapa.
    
2. Efetue login em uma região, uma organização e um espaço no {{site.data.keyword.Bluemix_notm}}. 

    Para obter mais informações, veja [Como efetuar login no {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login).
	
3. Execute o comando `ibmcloud iam oauth-tokens` para obter o token do IAM.

    ```
	ibmcloud iam oauth-tokens
	```
	{: codeblock}
	
	A saída retorna o token do IAM.

**Nota:** ao usar o token, remova *Bearer* do valor do token passado em chamadas API.
		



	

	
	
	
	
	
	
