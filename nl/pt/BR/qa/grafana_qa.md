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



# FAQ usando Grafana
{: #grafana_qa}

Veja as respostas para as perguntas comuns sobre como usar o Grafana com o serviço {{site.data.keyword.monitoringshort}}. 
{:shortdesc}

* [Não posso ver alertas que eu
defini usando a API Alerts no meu painel do Grafana](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-grafana_qa#alerts1)
* [Recebo um BXNMSAL41E quando
tento salvar uma mudança que eu fiz no meu painel do Grafana](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-grafana_qa#BXNMSAL41E)
* [Recebo um BXNMSAL36E quando
tento salvar uma mudança depois de incluir um alerta no meu painel do Grafana](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-grafana_qa#BXNMSAL36E)
* [Aparece um erro 404 quando efetuo login na UI da web do serviço Monitoring](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-grafana_qa#404)
* [Acabei de transferir dados do json por upload para um painel do Grafana. Por que perdi minha barra de rolagem?](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-grafana_qa#2)


## Não consigo ver alertas que eu defini usando a API Alerts no meu painel do Grafana
{: #alerts1}

Os alertas que você define usando a API Alerts não são mostrados na guia de alertas no Grafana. Para ver
alertas no Grafana, eles devem ser definidos diretamente em um painel do Grafana.

Para obter mais informações, consulte [Configurando alertas no Grafana](/docs/services/cloud-monitoring/alerts?topic=cloud-monitoring-config_alerts_grafana#config_alerts_grafana).

## Recebo um BXNMSAL41E quando tento salvar uma mudança que eu fiz no meu painel do Grafana
{: #BXNMSAL41E}

É possível definir canais e alertas de notificação no Grafana. Se você excluir um canal de notificação
no Grafana e não atualizar a regra para remover esse canal de notificação, um erro
**BXNMSAL41E** será recebido ao tentar salvar o painel do Grafana.

Para corrigir o problema, atualize a regra usando a API Alerts e tente novamente salvar o painel. Ao
atualizar a regra, remova o canal de notificação que foi excluído.

Para obter mais informações, consulte
[API
Alerts](https://console.bluemix.net/apidocs/940-ibm-cloud-monitoring-alerts-api?&language=node#introduction).

## Recebo um BXNMSAL36E quando tento salvar uma mudança depois de incluir um alerta no meu painel do
Grafana
{: #BXNMSAL36E}

Se você atingir a cota para o domínio no qual está monitorando métricas no
serviço do {{site.data.keyword.monitoringshort}}, o erro a seguir será obtido:
**BXNMSAL36E**

Faça upgrade de seu plano e tente novamente.

Para obter mais informações sobre como fazer upgrade do seu plano, consulte
[Mudando o plano](/docs/services/cloud-monitoring/plan?topic=cloud-monitoring-change_plan#change_plan).


## Aparece um erro 404 quando efetuo login na UI da web do serviço Monitoring usando o modelo de autenticação do UUA
{: #404}

Se aparecer um erro 404 ao tentar efetuar login na UI da web do serviço {{site.data.keyword.monitoringshort}} (Grafana), verifique se existe espaço e se você tem acesso a ela.

Quando você usa o [modelo de autenticação do UAA](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_uaa#auth_uaa) para acessar o serviço {{site.data.keyword.monitoringshort}}, deve-se usar o mesmo ID do usuário e senha que você usa para efetuar login no console do
{{site.data.keyword.Bluemix_notm}}. 

Para verificar se você tem acesso à conta, à organização e ao espaço no qual você deseja efetuar login, efetue login no console do {{site.data.keyword.Bluemix_notm}} e alterne para o espaço. 

Também é possível usar a linha de comandos para verificar se você tem acesso a esse espaço. Execute o comando a seguir para efetuar login em uma região, uma organização e um espaço no {{site.data.keyword.Bluemix_notm}}:

```
logins ibmcloud -a https://api.ng.bluemix.net
```
{: codeblock}

Siga as instruções. Insira suas credenciais do {{site.data.keyword.Bluemix_notm}}, selecione uma organização e um espaço.


## Acabei de transferir dados JSON por upload para um painel do Grafana; por que perdi a minha barra de rolagem?
{: #2}

Há um erro no Grafana que oculta a barra de rolagem depois de importar um painel. 

Para ver a barra de rolagem, salve o painel depois de importá-lo. 








