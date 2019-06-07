---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring,  predefined dashboards

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


# Painéis Predefinidos
{: #default_dashboards}
É possível escolher qualquer um dos painéis predefinidos a seguir para monitorar sua infraestrutura:
{:shortdesc}


## Aplicativos
{: #default_dashboards_applications}

A tabela a seguir lista os painéis predefinidos que podem ser selecionados para monitorar seus aplicativos e componentes de infraestrutura:

| Nome do painel        | Descrição                                                            | Uso             |
|-----------------------|------------------------------------------------------------------------|-------------------|
| `HTTP Overview`         | Use esse painel para monitorar o funcionamento de seu servidor da web. Ele mostra a carga no servidor e sua capacidade de atender as solicitações de serviço em tempo hábil. | Use os painéis Number of Requests e `Avg/Max Request Time` para medir a ocupação geral de seu servidor. </br>Procure correlações entre as URLs para localizar oportunidades para aprimorar o desempenho. </br>Use a métrica Códigos de status para monitorar os códigos de erro 4xx e 5xx. |  
| `HTTP Top Requests`  |  Use esse painel para monitorar as URLs mais solicitadas para o seu servidor da web. Por exemplo, o número total de solicitações, o tempo médio e o tempo máximo para atender a solicitações e a quantia de tráfego contida nas solicitações e nas respostas. |   |
| `MongoDB`  | Use esse painel para monitorar o quão ocupado seu serviço MongoDB está, quais coleções estão em maior demanda e quais coleções têm o desempenho mais lento.  |  Localize quais coleções podem se beneficiar do ajuste de desempenho de consulta e de índice. |
| `MySQL/PostgreSQL`  | Use esse painel para monitorar o status geral de carregamento e desempenho de suas transações do banco de dados SQL. Descubra o número de solicitações e a rapidez com que elas são manipuladas.  | Melhore o desempenho. Por exemplo, monitore os tempos de resposta para as consultas mais lentas e identifique as mudanças feitas na consulta ou nos índices nas tabelas.  |
| `MySQL/PostgreSQL Top`  | Use esse painel para monitorar as consultas SQL mais solicitadas. Visualize o número de consultas recebidas e a quantia de tráfego enviada e recebida para a consulta.   | Localize as consultas mais lentas, as consultas executadas na maioria das vezes, as consultas com tráfego alto.  |
| `Nginx`  | Use esse painel para monitorar recursos de host, conexões HTTP, URLs mais
lentas e códigos de resposta do host. | Identifique os ajustes de balanceamento de carga monitorando as
métricas a seguir: Gravação, Leitura, Conexões em espera, Carga da CPU por máquina, Atividade de bytes de
rede, Solicitações por segundo </br>Procure páginas que possam ser otimizadas consultando a métrica URLs mais lentas. </br>Localize problemas consultando os Códigos de resposta.  |
{: caption="Tabela 1. Lista de painéis predefinidos de componentes de aplicativo e de infraestrutura" caption-side="top"} 


## Painéis de host e de contêiner
{: #default_dashboards_host_container}

A tabela a seguir lista os painéis predefinidos que podem ser usados para monitorar a utilização de recursos e a atividade do sistema em seus hosts e em seus contêineres:


| Nome do painel        | Descrição                                                            | Uso             |
|-----------------------|------------------------------------------------------------------------|-------------------|
| `Limites de contêiner`    | Use esse painel para visualizar as métricas de CPU e de memória que são relativas aos recursos de host que estão alocados para cada contêiner. | |
| `Sistema de arquivos`         | Use esse painel para visualizar pontos de montagem de diretório, dispositivos do sistema de arquivos e informações de capacidade e de uso para os sistemas de arquivos que são montados na instância.  </br>Os sistemas de arquivos que são montados remotamente não são listados por padrão. Para visualizar dados para esses sistemas de arquivos, inclua a entrada **remotefs.enabled = true** a seguir no arquivo */opt/draios/bin/dragent.properties* em cada instância. </br>Quando os grupos são selecionados, as métricas são médias para pontos de montagem de sistema de arquivos semelhantes.| Localize quais sistemas de arquivos estão ficando cheios e quais estão sendo subutilizados. Classifique por  * fs.bytes.usado *.|
| `Visão geral por contêiner` | Use esse painel para visualizar estatísticas de uso de recurso, como porcentagem de CPU, porcentagem de uso de memória, total de bytes de rede e total de bytes de arquivo para contêineres que são executados no grupo ou instância selecionada.  </br>Use o recurso *Viagem no tempo* com a função *Comparar* nessa visualização para ver informações históricas. Com
base nos dados, verifique se os processos estão em execução conforme o esperado, se eles estão com comportamento inadequado ou se exigem mais recursos. | Descubra quais contêineres estão consumindo muitos recursos.  </br>Use as informações para determinar se um aplicativo deve ser movido para um host diferente. |
| `Visão geral por imagem de contêiner` | Use esse painel para obter uma visão geral do
tamanho, do desempenho e das limitações dos serviços que são definidos na imagem do contêiner. | |
| `Overview by Host` | Use esse painel para visualizar estatísticas de uso de recursos gerais, tais como a porcentagem de CPU, a porcentagem de uso de memória e o total de bytes de rede para um host. </br>Também é possível usar esse painel para monitorar um grupo de instâncias. </br>Use o recurso *Viagem no tempo* com a função *Comparar* nessa visualização para ver informações históricas. Com
base nos dados, verifique se os processos estão em execução conforme o esperado, se eles estão com comportamento inadequado ou se exigem mais recursos. | Descubra quais hosts estão sem uso ou estão sendo usados de forma excessiva dentro de um grupo de hosts com funções de tarefa semelhantes. | 
| `Overview by Process` | Use esse painel para visualizar estatísticas de uso de recursos gerais, tais como a porcentagem de CPU, a porcentagem de uso de memória e o total de bytes de rede para os processos principais
em um host. </br>Também é possível usar esse painel para monitorar um grupo de instâncias. </br>Use o recurso *Viagem no tempo* com a função *Comparar* nessa visualização para ver informações históricas. Com
base nos dados, verifique se os processos estão em execução conforme o esperado, se eles estão com comportamento inadequado ou se exigem mais recursos. | Descubra quais processos estão consumindo muitos recursos.  </br>Use as informações para determinar se um aplicativo deve ser movido para um host diferente. |
| `Sysdig Agent Summary` | Use esse painel para visualizar o número de agentes Sysdig que estão implementados em seu ambiente e suas versões. |  | 
| `Top Files` | Use esse painel para visualizar a lista de arquivos principais. É possível ver o nome do arquivo, o total de bytes de arquivo, o tempo gasto na E/S do arquivo e a contagem de erros de arquivo. | Localize os consumidores principais de disco ao classificar por tamanho. </br>Localize os arquivos mais ocupados quando
você classifica por E/S. </br>Identifique erros em potencial monitorando os dados na coluna *Contagem de
erros de arquivo*. |
| `Top Processes` | Use esse painel para visualizar a lista de processos principais que são executados em um host ou em um grupo de hosts. É possível ver o nome do processo, o seu caminho e todos os argumentos. </br>Use o recurso de filtro para restringir os processos que estão listados. | Localize quais processos são os consumidores principais em um ambiente no qual o spawn do mesmo processo ocorre várias vezes. |
| `Top Server Processes` | Use esse painel para visualizar o consumo de
recursos para processos identificados como sendo somente orientados ao servidor (httpd, java, ntpd, etc.). | Localize o uso de recurso para processos do servidor. |
{: caption="Tabela 2. Lista de painéis predefinidos de host e de contêiner" caption-side="top"} 

## Rede
{: #default_dashboards_network}

A tabela a seguir lista os painéis predefinidos que podem ser selecionados para monitorar as suas conexões de rede e a atividade:

| Nome do painel        | Descrição                                                            | Uso             |
|-----------------------|------------------------------------------------------------------------|-------------------|
| `Connections Table`     | Use esse painel para visualizar as conexões entre suas instâncias e nós remotos. Monitore o tráfego para cada conexão. | Localize os principais palestrantes que consomem a maioria do tráfego de rede em sua rede. |
| `Overview`              |  Use esse painel para visualizar a utilização total de rede
ao longo do tempo por direção, aplicativo, processo e host.| Identifique quais recursos afetam mais o desempenho da resposta. |
| `Response Times vs Resource Usage` | Use esse painel para visualizar métricas de recursos de host ao longo do tempo em comparação com o tempo de resposta do host no processamento de solicitações de rede. |  |
| `Top Ports`             |  Use esse painel para visualizar os bytes de entrada, de saída e
totais por porta, bem como para mostrar o número de conexões com cada número de porta. |  |
{: caption="Tabela 3. Lista de painéis predefinidos de rede" caption-side="top"} 



## Serviço
{: #default_dashboards_service}


A tabela a seguir lista os painéis predefinidos que podem ser usados para monitorar o desempenho de seus serviços, mesmo que esses serviços sejam implementados em contêineres orquestrados:

| Nome do painel        | Descrição                                                            | 
|-----------------------|------------------------------------------------------------------------|
| `Overview by Service`   | Use esse painel para visualizar o tamanho, o desempenho e as limitações de serviços que são executados na mesma imagem de contêiner. | 
| `Service Overview`      | Use esse painel para visualizar a utilização de recurso e os tempos de resposta de um único serviço. | 
{: caption="Tabela 4. Lista de painéis predefinidos do serviço" caption-side="top"} 



## Topologia
{: #default_dashboards_topology}

A tabela a seguir lista os painéis predefinidos que podem ser usados para monitorar as dependências lógicas de suas camadas do aplicativo:

| Nome do painel        | Descrição                                                            | 
|-----------------------|------------------------------------------------------------------------|
| `CPU Usage`             | Use esse painel para monitorar a interação entre seu host e o restante de sua infraestrutura.  | 
| `Network Traffic`       | Use esse painel para monitorar o uso da largura da banda da instância selecionada entre processos locais e processos em nós remotos. |
| `Response Times`        | Use esse painel para monitorar a comunicação e as métricas de resposta de rede entre todos os processos nos hosts selecionados. </br>As contagens de resposta e os tempos são mostrados em médias de granularidade de até um segundo.  |
{: caption="Tabela 5. Lista de painéis predefinidos de topologia" caption-side="top"} 

**Nota:** qualquer um desses painéis mostra linhas tracejadas e caixas cinza para instâncias sem um agente Sysdig e para as quais a comunicação é detectada.















