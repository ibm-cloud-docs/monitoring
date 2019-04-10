---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, metrics

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

# Trabalhando com Métricas
{: #metrics}

Depois de provisionar uma instância do serviço {{site.data.keyword.mon_full_notm}} no {{site.data.keyword.Bluemix}} e configurar um agente Sysdig para uma origem de métricas, é possível visualizar, monitorar e gerenciar métricas por meio da IU da web do {{site.data.keyword.mon_full_notm}}. Use métricas para analisar dados estatisticamente que têm valores numéricos. 
{:shortdesc}


**Uma métrica é uma medida quantitativa que tem um ou mais rótulos para definir suas características.**

Uma métrica é representada por séries temporais. 

Uma série temporal é um conjunto de pontos de dados numéricos em um período de tempo. 

As métricas são classificadas em dois grupos: 

* Métricas padrão 
* Métricas customizadas


## Rótulos
{: #metrics_labels}

**Os rótulos definem as características de uma métrica.**

Os rótulos são classificados como rótulos de infraestrutura e rótulos do descritor de métrica. Cada métrica tem um conjunto de rótulos predefinidos. Para métricas customizadas, é possível configurar mais rótulos. 

É possível usar rótulos para identificar e diferenciar características de uma métrica, por exemplo,
* É possível agrupar objetos de infraestrutura em hierarquias lógicas. 
* É possível filtrar dados. 
* É possível dividir dados agregados em segmentos. 


## Métricas padrão 
{: #metrics_default}

**As métricas padrão relatam sobre o sistema, o orquestrador e a infraestrutura de rede.**

O serviço de monitoramento inclui automaticamente os rótulos em cada métrica.


## Métricas customizadas
{: #metrics_custom}

**As métricas customizadas variam com base no tipo de infraestrutura e nos aplicativos que você monitora. Alguns exemplos são JMX, Prometheus e StatsD.**

Essas métricas têm um conjunto de rótulos predefinidos. É possível incluir rótulos customizados adicionais.

O serviço de monitoramento mantém um índice de todas as métricas customizadas e rótulos customizados que têm dados relatados nos últimos 14 dias. É possível usar essas métricas para configurar painéis, escopos e alertas.

Considere as informações a seguir sobre como o serviço de monitoramento gerencia as entradas de índice:
*  Uma métrica é removida automaticamente do índice de serviço de monitoramento e marcada como ausente quando qualquer uma das condições a seguir ocorre:
    
    * O serviço de monitoramento não recebe nenhum dado para uma métrica ou um rótulo por mais de 14 dias.
    
    * Uma métrica ou rótulo nunca relatou dados.

* Não é possível configurar novos artefatos com uma métrica ausente ou um rótulo ausente. 
* Não é possível atualizar artefatos existentes até que as métricas e os rótulos ausentes sejam removidos da configuração atual.
* É possível usar uma métrica ausente ou um rótulo ausente em consultas de dados e gráficos. 
* Seus artefatos existentes não serão afetados se incluírem uma métrica ausente ou um rótulo ausente.
* Quando os dados são recebidos para uma métrica ou um rótulo ausente, a métrica ou o rótulo é incluído de volta no índice.



