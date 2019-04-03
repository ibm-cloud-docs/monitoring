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

# Configurando alertas no Grafana
{: #config_alerts_grafana}

O serviço {{site.data.keyword.monitoringshort}} fornece um sistema de alerta baseado em consulta. É possível configurar alertas no Grafana em painéis que não possuem variáveis de modelo. 
{:shortdesc}

Para configurar um alerta em uma consulta de métrica por meio da UI do Grafana, conclua as etapas a seguir:

1. Ative o Grafana.
2. Defina um ou mais canais de notificação.
3. Crie um painel do Grafana que inclua um gráfico e pelo menos uma métrica de consulta. 
4. Configure o alerta por meio da guia **Alertas** no gráfico do Grafana.

## Etapa 1: Ativar o Grafana
{: #step1_cag}

Ative o Grafana por meio de um navegador. Por exemplo, insira a URL a seguir para abrir o Grafana na
região Sul dos EUA: [https://metrics.ng.bluemix.net/](https://metrics.ng.bluemix.net/).

Para uma lista de URLs do Grafana por região, consulte [URLs para o serviço {{site.data.keyword.monitoringshort}}](/docs/services/cloud-monitoring?topic=cloud-monitoring-monitoring_ov#region).

## Etapa 2: Definir um ou mais canais de notificação
{: #step2_cag}

Conclua as etapas a seguir:

1. No Grafana, selecione a barra de menus lateral.

2. Selecione **Alertando > Canais de notificação > Novo canal**.

3. Insira os dados para o novo canal. Inclua um canal de notificação por e-mail, por exemplo.

<table>
  <caption>Método de notificação por e-mail e dados que devem ser inseridos para criar um novo canal</caption>
  <tr>
     <th>Campo</th>
     <th>Descrição</th>
  </tr>
  <tr>
    <td>Nome</td>
    <td>Nome do canal de notificação. Esse valor deve ser exclusivo.</td>
  </tr>
  <tr>
    <td>Descrição</td>
    <td>Informações adicionais que talvez você queira incluir para propósitos de documentação.</td>
  </tr>
  <tr>
    <td>Tipo</td>
    <td>Selecione: **E-mail**</td>
  </tr>
  <tr>
    <td>ID do e-mail</td>
    <td>Insira o endereço de e-mail do destinatário. </br>É possível inserir múltiplos endereços de e-mail
separados por vírgulas.</td>
  </tr>
</table>

<table>
  <caption>Método de notificação por webhook e dados que devem ser inseridos para criar um novo canal</caption>
  <tr>
     <th>Campo</th>
     <th>Descrição</th>
  </tr>
  <tr>
    <td>Nome</td>
    <td>Nome do canal de notificação. Esse valor deve ser exclusivo.</td>
  </tr>
  <tr>
    <td>Descrição</td>
    <td>Informações adicionais que talvez você queira incluir para propósitos de documentação.</td>
  </tr>
  <tr>
    <td>Tipo</td>
    <td>Selecione: **Webhook**</td>
  </tr>
  <tr>
    <td>URL de POST do webhook</td>
    <td>Insira a URL na qual o POST deve ser feito.</td>
  </tr>
  <tr>
    <td>Cabeçalhos do webhook</td>
    <td>Insira quaisquer cabeçalhos.</td>
  </tr>
  <tr>
    <td>Parâmetros de consulta do webhook</td>
    <td>Insira quaisquer parâmetros de consulta.</td>
  </tr>
</table>

<table>
  <caption>Método de notificação por PagerDuty e dados que devem ser inseridos para criar um novo canal</caption>
  <tr>
     <th>Campo</th>
     <th>Descrição</th>
  </tr>
  <tr>
    <td>Nome</td>
    <td>Nome do canal de notificação. Esse valor deve ser exclusivo.</td>
  </tr>
  <tr>
    <td>Descrição</td>
    <td>Informações adicionais que talvez você queira incluir para propósitos de documentação.</td>
  </tr>
  <tr>
    <td>Tipo</td>
    <td>Selecione: **PagerDuty**</td>
  </tr>
  <tr>
    <td>Chave API do PagerDuty</td>
    <td>Insira a chave do PagerDuty.</td>
  </tr>
</table>

## Etapa 3: Definir uma métrica
{: #step3_cag}

Conclua as etapas a seguir para criar um novo painel:

1. Selecione a alternância de barra de menus lateral ![Barra de menus lateral do Grafana](images/grafana_settings.gif "Barra de menus lateral do Grafana").
2. Selecione **Painéis**.
3. Clique em **Novo**

Um painel se abre. O painel inclui uma linha vazia que está pronta para configuração. 

Em seguida, inclua uma consulta de métrica:

1. Inclua um painel *Gráfico*.
2. Selecione **Gráfico**.
3. Clique no título do gráfico e, em seguida, selecione **Editar**.
    
    O *Métricas* guia é aberta. É possível ver aqui a origem de dados padrão.
    
4. Defina a consulta de métrica que filtra os dados que são exibidos no gráfico. 


## Etapa 4: Definir um alerta
{: #step4_cag}

Conclua as etapas a seguir para definir um alerta na UI do Grafana:

1. Selecione a guia **Alerta**.
2. Na seção **Configuração de alerta**, defina a regra que define as
condições sob as quais uma notificação de alerta é gerada.

    Configure o campo **Avaliar a cada** e a seção **Condições**.

3. Na seção **Notificações**, selecione um ou mais canais de notificação.

**Nota:** 

* Quando uma condição é configurada, é possível ver uma linha vermelha no gráfico para definir o
conjunto de limites. É possível arrastá-la no gráfico para mudá-la.
* Quando o alerta é criado, se você deseja modificá-lo, deve-se fazer isso usando a API Alerts.
* Se você selecionar **Excluir**, o alerta será excluído.

## Próximo: verifique se um alerta é gerado
{: #next_cag}

Por exemplo, se você criou um canal de notificação por e-mail, verifique seu e-mail.

Procure por e-mails com o remetente **IBM Cloud Monitoring**.

Um e-mail inclui informações sobre o alerta emitido e um link para o painel do Grafana no qual é
possível visualizar a situação.

Por exemplo:

```
Rule : grafana4_alerting-dashboard_1
Description : Alert created via Grafana 4 dashboard: alerting-dashboard on expression: ibmcloud.public.containers-kubernetes.eu-de.MyDemoCluster.worker.*.load.avg-15
Expression : ibmcloud.public.containers-kubernetes.eu-de.MyDemoCluster.worker.*.load.avg-15
Error Level : 0.8
Warn Level : 
Notification : email-channel
Dashboard URL : https://urldefense.proofpoint.com/v2/url?u=https-3A__metrics.eu-2Dde.bluemix.n......&s=Csta29jgJ8BsUZuJOeyX9G_6NoEnGi2RBbtIDFhjtfw&e=

Alerts:
Target: ibmcloud.public.containers-kubernetes.eu-de.MyDemoCluster.worker.kube-fra02-cr39f48d743e90451fa5a57d636796a489-w2.load.avg-15    From: WARN    To: OK    CurrentValue: 0.66    Comparison: above    Timestamp: 2018-02-06T17:34:14Z
```
{: screen}


