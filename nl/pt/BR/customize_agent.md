---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-18"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# Customizando o agente Sysdig para controlar dados
{: #customize_agent}

Por padrão, o agente Sysdig coleta dados de um intervalo de plataformas e aplicativos. É possível editar o arquivo de configuração do agente para mudar seu comportamento padrão e incluir ou excluir dados. É possível customizar o arquivo de configuração do agente Sysdig para incluir métricas customizadas, como JMX, StatsD e Prometheus. Também é possível filtrar métricas, dados do evento e contêineres.
{:shortdesc}

## Customizando o agente Sysdig do Kubernetes
{: #kube}

O agente Sysdig do Kubernetes usa dois arquivos de configuração que especificam quais dados coletar automaticamente:

| Nome do arquivo                        | Ações           |
|----------------------------------|-------------------|
| `sysdig-agent-daemonset-v2.yaml` | Modifique o nível de log. |
| `sysdig-agent-configmap.yaml`    | Bloquear portas. </br>Inclua ou exclua dados de métrica. </br>Incluir ou remover eventos. </br>Filtrar contêineres. |
{: caption="Tabela 1. Arquivos de configuração do agente Sysdig do Kubernetes" caption-side="top"} 

Para editar um agente Sysdig do Kubernetes, pode ser necessário editar o *sysdig-agent-configmap.yaml*, o *sysdig-agent-daemonset-v2.yaml* ou ambos.

Há dois métodos que podem ser usados para modificar um arquivo de configuração:
* Método 1: modificar o arquivo diretamente no cluster no qual o agente está em execução. Para obter mais informações, consulte [Editando a configuração do agente Sysdig do Kubernetes usando kubectl edit](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_edit_kube_agent_method1).
* Método 2: modificar o arquivo localmente e aplicar as mudanças ao cluster. Para obter mais informações, consulte [Editando a configuração do agente Sysdig do Kubernetes usando kubectl apply](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_edit_kube_agent_method2).

É possível incluir tags nos dados que são coletados pelo agente. 
* Use essas tags para ajudar a gerenciar os dados que você monitora. 

    * Use rótulos para agrupar os recursos de infraestrutura em hierarquias lógicas, filtrar dados e dividir dados agregados em segmentos. 
    
    * Customize como os dados serão agregados quando você configurar um gráfico ou criar um alerta para uma métrica. 
    
    * Configure o escopo de um painel ou de um alerta para filtrar pontos de dados. 
    
    * Restrinja o acesso aos dados gerenciando o acesso a dados dos usuários por meio de equipes. 
    
    * Para obter mais informações sobre como gerenciar dados, consulte [Gerenciando dados](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-manage#manage).

* Para obter informações sobre como incluir tags, consulte [Incluindo mais tags em dados coletados de um agente Sysdig do Kubernetes](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_add_tags). 


**É possível customizar quais dados são coletados pelo agente Sysdig.** 

Ao excluir eventos, métricas e contêineres, considere as informações a seguir:
* É possível reduzir a carga de agente e de back-end.
* Você só coleta dados de contêineres que deseja monitorar.
* É possível controlar custos relatando contêineres importantes e filtrando contêineres desnecessários ou não críticos.
* É possível configurar os eventos do Kubernetes que você deseja monitorar. Para obter mais informações, consulte [Coletando um conjunto de eventos do Kubernetes](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_collect_events).

A lista a seguir descreve ações que podem ser executadas para controlar os dados que são coletados pelo agente Sysdig:
* [Desativando a coleta de eventos](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_disable_events)
* [Incluindo e excluindo métricas](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_inc_exc_metrics)
* [Filtrando objetos e contêineres do Kubernetes por meio dos quais os dados são coletados](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_filter_data)
* [Bloqueando portas](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_block_ports)
* [Filtrando eventos do Kubernetes por severidade](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_filterby_severity)

É possível customizar o tipo de log e as entradas coletadas também. Para obter mais informações. consulte  [ Mudando o nível de log ](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_log_level).

Também é possível registrar a lista de métricas para as quais o agente relata dados. Para obter mais informações, veja [Registrando em um arquivo quais métricas estão incluídas ou excluídas](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_log_metrics).

O agente Sysdig gera entradas de log em */opt/draios/logs/draios.log*. 
* O arquivo de log gira ao atingir 10 MB de tamanho.
* Os 10 arquivos de log mais recentes são mantidos. O registro de data anexado ao nome do arquivo é usado para determinar quais arquivos manter.
* Os níveis de log válidos são: *nenhum*, *erro*, *aviso*, *informações*, *depuração*, *rastreio*
* O nível de log padrão é *informações*, em que uma entrada é criada para cada transmissão de métricas agregadas para os servidores de backend, uma vez por segundo, além das entradas para quaisquer avisos e erros.

A tabela a seguir lista alguns cenários comuns e o valor que deve ser configurado em cada um deles:

| Casos de uso                                     | Entrada de seção de log           |
|-----------------------------------------------|-----------------------------|
| Solucionar problemas de comportamento do agente                   | `file_priority: debug`      |
| Reduza a saída de console do contêiner               | `console_priority: warning` |
| Filtrando eventos por severidade                  | `event_priority: warning`   |
| Verifique quais métricas estão incluídas ou excluídas  | `metrics_excess_log: true`  |

## Agente Sysdig do Contêiner
{: #container}


A lista a seguir descreve ações que podem ser executadas para controlar os dados que são coletados pelo agente Sysdig:
* [Desativando a coleta de eventos](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_disable_events)
* [Incluindo e excluindo métricas](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_inc_exc_metrics)
* [Filtrando contêineres por meio dos quais os dados são coletados](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_collect_docker_events)
* [Bloqueando portas](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_block_ports)
* [Filtrando eventos por severidade](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_filterby_severity)

É possível customizar o tipo de log e as entradas coletadas também. Para obter mais informações. consulte  [ Mudando o nível de log ](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_log_level).



## Agente Sysdig do Linux
{: #linux}

O agente Sysdig do Linux usa dois arquivos de configuração que especificam quais dados coletar automaticamente:

| Arquivo                   | Descrição                                                     | Localização                                |
|------------------------|-----------------------------------------------------------------|-----------------------------------------|
| `dragent.default.yaml` | Arquivo de configuração principal </br>**Nota:** **Não edite esse arquivo.  | `/opt/draios/etc/dragent.default.yaml`  |
| `dragent.yaml`         | Arquivo de configuração que você edita para customizar o agente Sysdig. | `/opt/draios/etc/dragent.yaml`          |
{: caption="Tabela 1. Arquivos de configuração do agente Sysdig" caption-side="top"} 

É possível editar o arquivo *dragent.yaml* para customizar os dados coletados. As mudanças entram em vigor imediatamente após o salvamento do arquivo. O agente detecta a mudança e reinicia automaticamente. É possível localizar a frequência e os arquivos verificados por um agente Sysdig no arquivo *dragent.default.yaml*. Para obter mais informações, consulte [Editando o arquivo dragent yaml](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_linux_agent#change_linux_agent_edit_agent).

Por exemplo, um *dragent.default.yaml* inclui as informações a seguir:

```
check_frequency_s: 5 arquivos: - /opt/draios/etc/dragent.yaml - /opt/draios/etc/kubernetes/config/dragent.yaml - /opt/draios/etc/kubernetes/secrets/access-key
```
{: screen}

A lista a seguir descreve ações que podem ser executadas para controlar os dados que são coletados pelo agente Sysdig:
* [Incluindo e excluindo métricas](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_linux_agent#change_linux_agent_inc_exc_metrics)
* [Bloqueando portas](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_linux_agent#change_linux_agent_block_ports)

É possível customizar o tipo de log e as entradas coletadas também. Para obter mais informações. consulte  [ Mudando o nível de log ](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_linux_agent#change_linux_agent_log_level).


