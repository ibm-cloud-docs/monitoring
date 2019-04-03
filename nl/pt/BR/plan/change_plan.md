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


# Alterando o plano
{: #change_plan}

É possível mudar o plano de serviço no painel do {{site.data.keyword.monitoringshort}}
{{site.data.keyword.monitoringlong_notm}} ou executando o comando `cf update-service`. É possível fazer upgrade ou reduzir seu plano a qualquer momento.
{:shortdesc}

## Mudando o plano de serviços por meio da UI
{: #change_plan_ui}

Para mudar seu plano de serviço no painel do {{site.data.keyword.monitoringlong_notm}},
conclua as etapas a seguir:

1. Efetue login no {{site.data.keyword.Bluemix_notm}} e, em seguida, clique no serviço do
{{site.data.keyword.monitoringshort}} no Painel. 

    O painel de serviço do {{site.data.keyword.monitoringshort}} é aberto.
    
2. Selecione a guia **Plano**.

    Informações sobre o plano atual são exibidas.
	
3. Selecione um novo plano para fazer upgrade do seu plano ou reduzi-lo. 

4. Clique em **Salvar**.



## Mudando o plano de serviços por meio da CLI
{: #change_plan_cli}

Para mudar seu plano de serviço no {{site.data.keyword.Bluemix_notm}} por meio da CLI, conclua
as etapas a seguir:

1. Efetue login em uma região, uma organização e um espaço no {{site.data.keyword.Bluemix_notm}}. 

    Para obter mais informações, veja [Como efetuar login no {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login).
	
2. Execute o comando `ibmcloud service list` para verificar seu plano atual e para obter o nome do serviço {{site.data.keyword.loganalysisshort}} na lista de serviços disponível no espaço. 

    O valor do campo **nome** é aquele que deve-se ser usado para mudar o plano. 

    Por exemplo,
	
	```
	$ ibmcloud service list
	Getting services in org MyOrg / space dev as xxx@yyy.com...
	OK
	name            service      plan   bound apps   last operation
	Monitoring-0c   Monitoring   premium             create succeeded
    ```
	{: screen}
    
3. Faça upgrade ou reduzir seu plano. Execute o comando  ` ibmcloud service update ` .
    
	```
	Atualização de serviço ibmcloud service_name [-p new_plan ]
	```
	{: codeblock}
	
	Em que 
	
	* *service_name* é o nome do seu serviço. 
	* *new_plan* é o nome do plano.
	
	A tabela a seguir lista os planos diferentes e seus valores suportados:
	
	<table>
	  <caption>Tabela 1.  Lista de planos.</caption>
	  <tr>
	    <th>Plan</th>
		<th>Recursos</th>
	    <th>Nome</th>
	  </tr>
	  <tr>
	    <td>Lite</td>
	    <td>Monitoramento de cortesia.</td>
		<td>Lite</td>
	  </tr>
	  <tr>
	    <td>Premium</td>
	    <td>Monitoramento Premium.</td>
		<td>Premium</td>
	  </tr>
	</table>
	
	Por exemplo, para reduzir seu plano para o plano *Lite*, execute o comando a seguir:
	
	```
	ibmcloud service update "Monitoring-0c" -p lite
    Updating service instance Monitoring-0c as xxx@yyy.com...
    OK
	```
	{: screen}

4. Verifique se o novo plano é alterado. Execute o comando  ` ibmcloud service list ` .

    ```
	ibmcloud service list
    Getting services in org MyOrg / space dev as xxx@yyy.com...
    OK

    name              service       plan   bound apps   last operation
    Monitoring-0c     Monitoring    lite                create succeeded
	```
	{: screen}






