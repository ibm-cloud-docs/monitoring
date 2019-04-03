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


# Sobre
{: #monitoring_ov}

Use o serviço do {{site.data.keyword.monitoringlong}} para expandir os seus recursos de coleta e retenção ao trabalhar com métricas, bem como para poder definir regras e alertas que notifiquem você sobre as condições que requerem atenção. Confira poderes às suas equipes do DevOps equipe com recursos que fornecem insight sobre como seus apps estão executando e consumindo recursos. Identifique tendências, detecte e diagnostique problemas rapidamente; todos com prazo de lançamento no mercado imediato e baixo custo total de propriedade. Use o Grafana para monitorar seu ambiente. 
{:shortdesc}

A figura a seguir mostra uma visualização de alto nível dos diferentes recursos em que é possível enviar métricas para o serviço {{site.data.keyword.monitoringshort}} para análise:

![Visão geral de alto nível de componentes no
serviço do {{site.data.keyword.monitoringlong}} ](images/cloud_monitoring_ov.png "Visão geral de alto nível de componentes noserviço do {{site.data.keyword.monitoringlong}} ")


Por padrão, o {{site.data.keyword.Bluemix}} coleta e exibe métricas para uso de CPU,
utilização de memória e E/S de rede para o {{site.data.keyword.containershort}}. É possível usar o
serviço do {{site.data.keyword.monitoringshort}} no {{site.data.keyword.Bluemix_notm}}
para coletar e medir automaticamente as métricas de chave de seu ambiente e aplicativos. Nenhuma instrumentação especial é necessária para coletar métricas. Por exemplo, é possível usar as informações fornecidas por métricas de desempenho para monitorar como um serviço está em execução na nuvem, detectar gargalos de recursos e manter-se atento ao acordo de nível de serviço (SLA). Ao analisar dados de desempenho para um serviço, é possível detectar situações que podem levar a um gargalo de recurso e, consequentemente, afetar seu SLA do serviço para seus clientes. Tomando uma ação antecipada, é possível evitar situações que podem impactar negativamente seus negócios.  

É possível enviar métricas dos aplicativos Cloud Foundry (CF) e das Máquinas virtuais (VMs) para o serviço {{site.data.keyword.monitoringshort}}. Para obter mais informações sobre como enviar métricas, veja [Enviando métricas para o serviço do {{site.data.keyword.monitoringshort}}](/docs/services/cloud-monitoring/send_retrieve_metrics_ov.html#send_retrieve_metrics_ov).

É possível fornecer o serviço do {{site.data.keyword.monitoringshort}} por meio do
catálogo {{site.data.keyword.Bluemix_notm}}.  

É possível visualizar e analisar as métricas coletadas pelo serviço
do {{site.data.keyword.monitoringshort}} por meio do painel do
{{site.data.keyword.Bluemix_notm}}.  

## Por que usar o serviço Monitoring
{: #value}

1. **Gaste menos tempo instrumentando seu aplicativo e mais tempo aprimorando seu valor**

    O serviço {{site.data.keyword.monitoringlong_notm}} coleta automaticamente dados de métrica dos serviços {{site.data.keyword.IBM_notm}} Cloud, eliminando a necessidade de agentes. As APIs facilitam a inclusão das métricas customizadas e a consulta de seus dados de monitoramento. 
	
	O serviço do {{site.data.keyword.monitoringlong_notm}} oferece a coleta de métrica de uma vez só por minuto.  O plano Lite retém as métricas de resolução integral por 15 dias.  O plano Premium retém as métricas de resolução integral por 45 dias.

2. **Estenda facilmente o monitoramento em seu aplicativo com APIs**

    Integre seus dados de monitoramento em seus aplicativos e em suas operações por meio das APIs do serviço {{site.data.keyword.monitoringshort}}. Use as APIs para incluir um aplicativo relevante e as métricas de negócios em seus dados de monitoramento de Nuvem. Também é possível usar as APIs para enviar dados de métrica externos à Nuvem do {{site.data.keyword.IBM_notm}}para o serviço do {{site.data.keyword.monitoringshort}}.

3. **Obtenha insights em seu ambiente para detectar, diagnosticar e identificar problemas rapidamente**

    Visualize o pulso do seu aplicativo e a infraestrutura com painéis flexíveis e customizáveis pelo usuário. O {{site.data.keyword.monitoringlong_notm}} oferece a potência, a flexibilidade e a familiaridade do Grafana para construir e adaptar rapidamente o seu painel às necessidades do aplicativo.
	
4. **Construa painéis reutilizáveis e torne-os interativos**

    O Grafana hospedado do serviço do {{site.data.keyword.monitoringlong_notm}} fornece suporte para construir painéis customizados com uma ampla gama de opções de visualização.  Faça seus painéis dinâmicos com modelos usando consultas de métrica com variáveis.

5. **Receber alertas**

    Defina regras para notificá-lo sobre as condições que requerem atenção. O serviço do {{site.data.keyword.monitoringlong_notm}} oferece uma API que pode ser usada para configurar limites de desempenho e para ser notificado quando os limites são violados. Defina regras de alerta para uma única instância de serviço ou instância de app e regras de alerta que sejam relatados em um conjunto de instâncias. Quando um alerta for acionado, obtenha uma notificação por meio de um e-mail, um evento de PagerDuty, uma notificação de webhook ou qualquer combinação dos três.

6. **Escolha o plano de serviço que se ajuste às suas necessidades** 

    É possível escolher o plano de serviços Lite ou o plano de serviços Premium para corresponder às suas necessidades de uso.  O plano Lite oferece a coleta de métrica de plataforma básica e alerta complementar.  Alternativamente, é possível selecionar o plano Premium para permitir um maior consumo de métrica com um período mais longo de retenção, para aumentar o número de alertas que podem ser definidos, incluindo alertas que sejam relatados em múltiplos serviços, bem como para obter acesso às APIs de serviços.

 
## Planos de serviço
{: #plan}

O {{site.data.keyword.monitoringshort}} serviço fornece vários planos. Cada plano tem diferentes recursos de métricas de coleta, de retenção e de definição de alerta. 

É possível mudar um plano por meio da UI do {{site.data.keyword.Bluemix_notm}} ou por meio da linha de comandos. É possível fazer upgrade ou reduzir seu plano a qualquer momento. Para obter mais informações sobre upgrades de plano de serviço no {{site.data.keyword.Bluemix_notm}}, veja [Mudando o plano](/docs/services/cloud-monitoring/plan/change_plan.html#change_plan). 

A tabela a seguir descreve os planos que estão disponíveis ao fornecer o
serviço do {{site.data.keyword.monitoringshort}} em um espaço:

<table>
    <caption>Tabela 1. Resumo de planos para o serviço do {{site.data.keyword.monitoringshort}}
por espaço.</caption>
      <tr>
        <th>Plan</th>
        <th>Enviando métricas usando a API</th>
        <th>Período de Retenção</th>
        <th>Alertas</th>
		    <th>Métodos de notificação</th>
      </tr>
      <tr>
        <td>Lite (padrão)</td>
        <td>Não está disponível</td>
        <td>15 dias</td>
        <td>É possível definir até 10 regras de alertas com consultas de métrica únicas ou 1 regra de alerta
que inclua um curinga.</td>
		    <td>Email</td>
      </tr>
      <tr>
        <td>Premium</td>
        <td>Disponíveis</td>
        <td>45 dias</td>
        <td>É possível definir regras de alerta incluindo regras com curingas.</td>
		    <td>E-mail, webhook, PagerDuty</td>
      </tr>
</table>

**Nota:** o plano Lite oferece os mesmos recursos que os recursos de monitoramento
integrados no {{site.data.keyword.Bluemix_notm}}. O domínio da conta oferece os mesmos recursos que o
plano Lite.


## Período de Retenção
{: #metrics_retention}

A tabela a seguir resume o período de retenção com base em seu plano de serviço:

<table>
    <caption>Tabela 2. Resumo de período de retenção para o serviço do {{site.data.keyword.monitoringshort}}.</caption>
      <tr>
        <th>Plan</th>
        <th>Período de Retenção</th>
      </tr>
      <tr>
        <td>Lite (padrão)</td>
        <td>As métricas são armazenadas a cada minuto por 15 dias. (1m:15d)</td>
      </tr>
      <tr>
        <td>Premium</td>
        <td>As métricas são armazenadas a cada minuto por 45 dias. (1m:45d)</td>
      </tr>
</table>

As métricas que não tiverem recebido dados nos últimos 7 dias serão excluídas. O serviço {{site.data.keyword.monitoringshort}} exclui todos os dados para um caminho de métrica que parece ser de natureza transitória, identificando as métricas que não foram gravadas nos últimos sete dias. Por exemplo:

* Quando um contêiner for excluído, as métricas associadas a esse contêiner existirão durante 7 dias e, depois desse tempo, elas serão excluídas.
* Se você tiver um gráfico statsd chamado `<space_id>.test.statsd.gauge-hello` e você não grava nele durante uma semana; a métrica será identificada como temporária e essa métrica será excluída junto a todas as suas informações históricas. 

## Fornecendo o serviço Monitoring
{: #provision1}

No catálogo do {{site.data.keyword.Bluemix_notm}}, é possível localizar o serviço {{site.data.keyword.monitoringshort}} na seção **DevOps**. Para obter mais informações sobre o fornecimento de um serviço no {{site.data.keyword.Bluemix_notm}},
consulte [Fornecendo o
serviço do {{site.data.keyword.monitoringshort}}](/docs/services/cloud-monitoring/how-to/provision.html#provision).

Considere as informações a seguir sobre o serviço do {{site.data.keyword.monitoringshort}}:

* É possível fornecer somente uma instância do serviço do {{site.data.keyword.monitoringshort}}
por espaço.
* Para coletar métricas para recursos em nuvem em execução em um espaço do Cloud Foundry, deve-se
fornecer o serviço no mesmo espaço em que os recursos estão em execução.




## Regiões
{: #regions}

O serviço {{site.data.keyword.monitoringshort}} está disponível nas regiões a seguir:

* Alemão
* Sydney
* Reino Unido
* Sul dos Estados Unidos




## URLs para o serviço Monitoring
{: #region}

O serviço do {{site.data.keyword.monitoringshort}} está disponível para qualquer pessoa com um
ID e permissões do {{site.data.keyword.Bluemix_notm}} para trabalhar com o serviço no
{{site.data.keyword.Bluemix_notm}}.

* Para cada região em que o serviço {{site.data.keyword.monitoringshort}} está disponível, há um conjunto diferente de terminais. 
* Há uma única URL que é compartilhada pelos terminais de ingestão e de API/UI da web.
* A porta 443 é a porta do TLS que é usada para acessar as métricas por meio da API e da UI da Web (Grafana).

A tabela a seguir lista as URLs por região:

<table>
  <caption>Tabela 3. Lista de terminais para trabalhar com o serviço {{site.data.keyword.monitoringshort}}</caption>
  <tr>
    <th>Região</th>
	<th>Nó de
extremidade</th>
  </tr>
  <tr>
    <td>Alemão</td>
	<td>[https://metrics.eu-de.bluemix.net](https://metrics.eu-de.bluemix.net)</td>
  </tr>
  <tr>
    <td>Sydney</td>
	<td>[https://metrics.au-syd.bluemix.net](https://metrics.au-syd.bluemix.net)</td>
  </tr>
  <tr>
    <td>Reino Unido</td>
	<td>[https://metrics.eu-gb.bluemix.net](https://metrics.eu-gb.bluemix.net)</td>
  </tr>
  <tr>
    <td>Sul dos Estados Unidos</td>
	<td>[https://metrics.ng.bluemix.net/](https://metrics.ng.bluemix.net/)</td>
  </tr>
</table>



