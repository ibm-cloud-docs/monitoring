---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring

subcollection: Sysdig

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

# Monitorando seu ambiente
{: #monitoring}

É possível monitorar sua infraestrutura e os aplicativos em execução nele com o serviço {{site.data.keyword.mon_full_notm}}. É possível solicitar uma captura para analisar o que acontece em um nó durante um prazo.
{:shortdesc}

Depois de provisionar uma instância do serviço {{site.data.keyword.mon_full_notm}} no {{site.data.keyword.Bluemix}} e configurar os agentes Sysdig para suas origens de métricas, é possível visualizar, monitorar e gerenciar dados por meio da IU da web do serviço.

Os dados para as métricas padrão são coletados automaticamente. É possível configurar métricas customizadas e incluir rótulos nessas métricas para descrever suas características. Os dados para essas métricas customizadas também são coletados automaticamente.

É possível analisar dados na guia *Explorar* e na guia *Painel* da IU da web. Você monitora os dados por meio de visualizações e painéis de métrica. 

* Use uma visualização de métrica para monitorar uma métrica individual.
* Use painéis para obter um insight especializado em dados de rede, dados do aplicativo, topologia, serviços, hosts e contêineres, monitorando dados por meio de painéis. Um painel exibe uma métrica ou um grupo de métricas em um painel.

Para cada visualização de métrica e painel, é possível definir o escopo dos dados, como agregar dados e quais filtros de tempo e de grupo se aplicam aos dados. Para obter mais informações, consulte [Gerenciando dados](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-manage#manage).

Na guia *Explorar*, é possível monitorar dados usando métricas padrão e painéis padrão. É possível usar rótulos para definir novos grupos de infraestrutura que podem, então, ser usados para agregar dados de forma diferente e monitorar seu ambiente. Também é possível usar painéis customizados que você define por meio da guia *Painel*.

Na guia *Painéis*, é possível monitorar dados usando qualquer um dos painéis padrão ou criando novos painéis.

É possível configurar um painel padrão como o ponto de entrada padrão para uma equipe, unificar a experiência de uma equipe e permitir que os usuários concentrem sua atenção imediata nas informações mais relevantes para eles. 
{: tip}

É possível usar alertas para notificar os usuários de problemas que requerem atenção por meio de um ou mais canais de notificação.
* A seção *Alertas* na IU da web mostra a lista de alertas predefinidos. Nessa visualização, é possível ativar e desativar alertas predefinidos, modificar alertas existentes e criar novos alertas.
* A seção *Configurações* na IU da web é onde você configura canais de notificação.
 
É possível solicitar uma captura em um nó para analisar o que acontece nesse nó durante um prazo. Por exemplo, é possível usá-lo para analisar interações de componentes ou gargalos.

## Métricas
{: #monitoring_metrics}

Uma métrica é uma medida quantitativa que tem um ou mais rótulos para definir suas características. Use métricas para analisar dados estatisticamente que têm valores numéricos. 

Uma métrica é representada por séries temporais. Uma série temporal é um conjunto de pontos de dados numéricos em um período de tempo. 

As métricas são classificadas em dois grupos: 

* [Métricas padrão](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-metrics#metrics_default) 
* [Métricas Customizadas](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-metrics#metrics_custom)

Os rótulos são classificados como rótulos de infraestrutura e rótulos de descritor de métrica. Cada métrica tem um conjunto de rótulos predefinidos. Para métricas customizadas, é possível configurar mais rótulos. 

É possível usar rótulos para identificar e diferenciar características de uma métrica, por exemplo,
* É possível agrupar objetos de infraestrutura em hierarquias lógicas. 
* É possível filtrar dados. 
* É possível dividir dados agregados em segmentos. 

Para obter mais informações, consulte  [ Rótulos ](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-metrics#metrics_labels).

## Painéis
{: #monitoring_panels}

Um painel exibe uma métrica ou um grupo de métricas em um painel. 

É possível usar qualquer um dos tipos de painel a seguir para visualizar métricas:

| Tipo | Descrição |
|------|-------------|
| Linha | Use esse painel para visualizar as tendências ao longo do tempo para uma ou mais métricas.  |
| Áreas | Use esse painel para visualizar as tendências ao longo do tempo para uma ou mais métricas.  |
| Lista superior | Use esse painel para comparar uma métrica entre grupos de entidades. O gráfico de barras é classificado em ordem decrescente.  |
| Histograma | Use esse painel para visualizar a distribuição de frequência de uma métrica em depósitos.  |
| Topologia | Use esse painel para visualizar a infraestrutura como um mapa de topologia e as relações entre entidades no mapa.  |
| Número | Use esse painel para visualizar um único número que representa o valor de uma métrica agregada ao longo do tempo para uma ou mais entidades.  |
| Tabela | Use esse painel para exibir dados numéricos para sua infraestrutura com base em métricas e segmentos.  |
| Texto | Use esse painel para incluir texto. Use redução para incluir seu texto.  |
{: caption="Tabela 3. Tipos de painéis" caption-side="top"} 

É possível copiar, mudar o escopo, duplicar, excluir, exportar e explorar painéis.

É possível exportar dados de um painel. Considere as informações a seguir ao exportar dados:

* É possível exportar dados para um **arquivo json** por meio de um gráfico de linha.
* É possível exportar dados para um **arquivo csv** por meio de um gráfico de tabela ou de um gráfico de linha.


A tabela a seguir lista as tarefas que podem ser executadas com painéis:

| Tarefa | Descrição |
|------|-------------|
| [Copiar painel](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_copy) | Copie um painel em um novo painel.  |
| [Mudar escopo](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_scope) | Mudar o escopo de um painel. |
| [Duplicar painel](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_duplicate) | Copie um painel no mesmo painel.  |
| [Excluir painel](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_delete) | Exclua um painel do painel.  |
| [Exportar dados](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_export) | Exporte dados de um painel para um arquivo csv ou um arquivo json.  |
| [Criar alerta](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_alert) | Defina um alerta em uma métrica. |
{: caption="Tabela 4. Tarefas do Painel" caption-side="top"} 


## Painéis
{: #monitoring_dashboards}

Um **painel** mostra os grupos de métricas que relatam o funcionamento, o desempenho e o estado de sua infraestrutura, aplicativos e serviços para um único host ou um grupo de hosts. Os painéis oferecem um insight especializado em dados da rede, dados do aplicativo, topologia, serviços, hosts e contêineres. Use painéis para monitorar sua infraestrutura, seus aplicativos e serviços.


Na seção **PAINÉIS** da IU da web, os painéis são organizados em três grupos principais:

* *Meus painéis*: são aqueles criados pelo usuário que está conectado atualmente.
* *Meus painéis compartilhados*: são aqueles criados pelo usuário que está conectado atualmente e que são compartilhados com outros usuários.
* *Painéis compartilhados comigo*: são aqueles criados por outros usuários e compartilhados com o usuário atual.

Na seção **EXPLORAR** da IU da web, os painéis são organizados em dois grupos:
* *Painéis padrão*: são os painéis predefinidos.
* *Meus painéis*: são aqueles criados pelo usuário que está conectado atualmente.

É possível usar painéis predefinidos. Também é possível criar painéis customizados por meio da IU da web ou programaticamente. É possível fazer backup e restaurar os painéis usando scripts Python ou a API de REST do Sysdig.

Também é possível copiar e compartilhar painéis por meio da IU da web. 

A tabela a seguir descreve as tarefas que podem ser executadas para trabalhar com painéis por meio da IU:

| Tarefa | Descrição |
|------|-------------|
| [Criar painel](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_create) | Crie um painel customizado na IU da web. |
| [Copiar um painel](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_copy) | Faça uma cópia de um painel na equipe atual na qual o painel está disponível ou copie um painel para outra equipe. |
| [Mudando o escopo](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_scope) | Mude o escopo de um painel.       |
| [Excluir painel](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_delete) |  Exclua um painel. |
| [Compartilhar um painel](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_share) | Compartilhe painéis entre usuários em uma equipe e externamente configurando uma URL pública para o painel. |
{: caption="Tabela 1. Tarefas de painel que podem ser executadas na IU da web" caption-side="top"} 

A tabela a seguir descreve tarefas que podem ser executadas programaticamente para trabalhar com painéis:

| Tarefa                    |	Usando a API de REST                |
|-------------------------|-------------------------------|
| Criar um painel      | [Criando um painel usando a API](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_create_dashboard) |
| Excluir um painel      | [Excluindo um painel usando a API](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_delete_dashboard) |
| Salvando painéis       | [Salvando os painéis de uma equipe usando a API](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_save_dashboard) |
{: caption="Tabela 2. Tarefas para gerenciar painéis programaticamente" caption-side="top"} 



## Eventos
{: #monitoring_events}

Um evento é uma notificação que informa sobre algo que ocorreu em qualquer um dos nós que encaminha dados para sua instância do {{site.data.keyword.mon_full_notm}}. Use eventos para revisar, rastrear e resolver problemas. 

Há diferentes tipos de eventos: 

* *Eventos de alerta* são aqueles acionados por alertas configurados pelo usuário. Para obter mais informações, consulte [Trabalhando com alertas](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-monitoring#monitoring_alerts).
* *Eventos baseados em infraestrutura* são aqueles coletados dos nós do Docker e do Kubernetes. Por padrão, o agente Sysdig descobre e coleta automaticamente dados de um grupo de eventos selecionado. É possível editar o arquivo de configuração do agente para permitir mais eventos.
* *Eventos customizados* configurados por meio de qualquer uma das integrações a seguir: Slackbot, scripts Python pré-construídos, scripts Python customizados criados pelo usuário ou solicitações de cURL.

Por padrão, um evento tem um estado: 
* *Ativo*: esse estado indica que as circunstâncias que acionaram o evento permanecem em vigor, por exemplo, um nó continua inativo.
* *OK*: esse estado indica que a situação está de volta ao normal, por exemplo, um nó está funcionando.

Você gerencia eventos na seção *Eventos* da IU da web. 
* É possível visualizar eventos de alerta por meio da guia *Eventos de alerta*.
* É possível visualizar eventos baseados em infraestrutura por meio da guia *Eventos customizados*.
* É possível visualizar eventos customizados por meio da guia *Eventos customizados*.
* É possível enviar eventos customizados para qualquer uma de suas equipes usando o [token de API para essa equipe](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token). Para obter mais informações, consulte [Eventos customizados ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/222822463/Custom+Events){:new_window}.

É possível resolver a situação que acionou um evento. Enquanto você espera que a condição que acionou o evento seja executada novamente e configura seu status como *OK*, é possível configurar o evento como **Resolvido** para exibir graficamente que o problema foi tratado. 
{: #tip}



## Alertas
{: #monitoring_alerts}

Um alerta é um evento de notificação que pode ser usado para avisar sobre situações que requerem atenção. Cada alerta tem um status de severidade. Esse status informa sobre o grau de severidade das informações sobre as quais ele relata. 

Ao definir um alerta, deve-se definir a condição que aciona a notificação, um ou mais canais de notificação pelos quais você deseja ser notificado, a severidade do alerta e o tipo de alerta. 

É possível definir alertas para qualquer um dos tipos de alerta a seguir:

| Tipo              | Descrição |
|-------------------|-------------|
| Detecção de Anomalias | Use para monitorar hosts com base em seus comportamentos históricos e alertar quando eles se desviarem. |
| Parada          | Use para monitorar qualquer tipo de entidade, por exemplo, host, contêiner, processo ou serviço e alertar quando a entidade ficar inativa. |
| Ocorrência             | Use para monitorar ocorrências de eventos específicos e alertar se o número total de ocorrências viola um limite. Por exemplo, é possível usá-la para alertar sobre reinicializações e implementações de contêineres, orquestrações e eventos de serviço.|
| Grupo de outlier     | Use para monitorar um grupo de hosts e ser notificado quando um agir diferentemente do restante. |
| Métrica            | Use para monitorar métricas de série temporal e alertar se elas violarem limites definidos pelo usuário. |
{: caption="Tabela 5. Tipos de alerta" caption-side="top"} 

Por padrão, a severidade é configurada como *warning*. É possível configurar a severidade de um alerta para qualquer um dos valores a seguir: *emergency*, *alert*, *critical*, *error*, *warning*, *notice*, *informational*, debug* 

É possível definir um ou mais canais de notificação para qualquer uma das integrações de notificação a seguir:
* Notificações por e-mail
* Notificações de PagerDuty
* Notificações de Slack
* Notificações de VictorOps
* Notificações OpsGenie
* Configurar um Canal Webhook

Para obter mais informações, consulte [Configurando um canal de notificação](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-notifications#notifications_create).


É possível ativar alertas predefinidos, modificar alertas e criar alertas customizados na IU da web e usando a API do Sysdig.

Você gerencia alertas na visualização *Alertas* da IU da web. É possível configurar as colunas da tabela que são exibidas na visualização *Alertas*. As opções de coluna válidas são: *Nome*, *Escopo*, *Alertar quando*, *Segmentar por*, *Notificações*, *Ativado*, *Modificado*, *Capturas*, *Canais*, *Criado*, *Descrição*, *Destinatários de e-mail*, *Por pelo menos*, *OpsGenie*, *PagerDuty*, *Severidade*, *Slack*, *WebHook*, *Tópicos SNS*, *Tipo*, *VictorOps*

A lista a seguir descreve as principais tarefas ao trabalhar com alertas:
* [Configurar um alerta ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-ConfigureanAlert){:new_window}
* [Ativar ou desativar um alerta ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-Enable/DisableAlerts){:new_window} 
* [Procurar um alerta ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-SearchforanAlert){:new_window}
* [Modificar um alerta ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-EditanExistingAlert){:new_window}
* [Copiar um alerta para a mesma equipe ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-CopyanAlerttothesameteam){:new_window}
* [Copiar um alerta para uma equipe diferente ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-CopyanAlerttoaDifferentTeam){:new_window}
* [Exportar um alerta ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-ExportAlertJSON){:new_window}
* [Excluir um alerta ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-DeleteAlerts){:new_window}
* [Definir limites de alerta como expressões booleanas customizadas ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts#Alerts-AdvancedAlertThresholds){:new_window}


## Capturas
{: #monitoring_captures}

Uma captura é um arquivo de rastreio que pode ser gerado para analisar o que acontece em um nó durante um prazo. O limite de tamanho do arquivo de captura é de 100 MB. Por exemplo, é possível usá-lo para analisar interações de componentes ou gargalos. 

As capturas contêm chamadas de sistema e outros eventos de S.O., como latências de nível de sistema, duração de tarefas em lote, tempos de interrupção de implementações, latências de ajuste automático de escala, tempos de inicialização de contêiner ou tempo da transação de aplicativo. As capturas incluem informações detalhadas de cada contêiner em um nó. 

Dependendo das diretrizes de sua organização, considere a desativação de capturas. Por padrão, as capturas são ativadas quando você configura um agente Sysdig em um nó.
{: tip}

É possível criar, explorar, fazer download e excluir *capturas* para nós individuais. Um nó pode ser um host, um contêiner, uma máquina virtual, um bare metal ou qualquer origem de métrica na qual você instala um agente Sysdig. 

* Na IU da web, você cria capturas na seção *Explorar* e gerencia arquivos de captura por meio da seção *Capturas*.
* É possível visualizar dados de uma captura usando a *Csysdig* (a IU da linha de comandos baseada em curses para sysdig) ou os utilitários Sysdig de software livre para analisar os dados em uma captura.
* É possível procurar dados em uma captura usando filtros.
* É possível manipular dados em uma captura usando chisels (scripts). 

Quando você ativa o recurso de captura para uma equipe, os arquivos de captura são visíveis somente para membros dessa equipe.

A lista a seguir descreve as principais tarefas quando você trabalha com capturas:
* [Criando uma Captura](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures_create)
* [Excluindo uma Captura](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures_delete)
* [ Explorar uma captura ](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures_explore)
* [ Fazer download de uma captura ](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures_download)

Para obter mais informações, consulte [Trabalhando com capturas](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures).


