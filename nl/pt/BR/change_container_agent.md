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

# Customizando os agentes Sysdig do contêiner
{: #change_container_agent}

No {{site.data.keyword.mon_full_notm}}, é possível customizar a configuração do agente Sysdig para definir um nível de log, bloquear portas, incluir ou excluir dados de métrica, incluir ou remover eventos e filtrar contêineres. 
{:shortdesc}


## Editando o arquivo dragent yaml
{: #change_container_agent_edit_config}

O arquivo yaml está localizado em */opt/draios/etc/*.

Conclua as etapas a seguir para editar o arquivo e aplicar as mudanças:

1. Acesse o  * dragent.yaml *  diretamente em  ` /opt/draios/etc/dragent.yaml `.
2. Edite o arquivo. Use a sintaxe YAML válida.
3. Reinicie o agente. Execute o seguinte comando:

    ```
    docker restart sysdig-agent
    ```
    {: codeblock}



## Bloqueando portas
{: #change_container_agent_block_ports}

Para bloquear o tráfego de rede e as métricas de portas de rede, deve-se customizar a seção **blacklisted_ports** no arquivo *dragent.yaml*. Deve-se listar as portas das quais você deseja filtrar quaisquer dados.

**Nota:** a porta 53 (DNS) é sempre incluída na lista de bloqueio. 

Por exemplo, a amostra a seguir mostra como configurar a seção *blacklisted_ports* de um agente Sysdig para excluir dados vindos das portas 6666 e 6379:

```
blacklisted_ports: - 6666 - 6379
```
{: screen}



## Coletando um conjunto de eventos do Docker
{: #change_container_agent_collect_docker_events}

O {{site.data.keyword.mon_full_notm}}  suporta a integração de eventos com o Docker. Os agentes Sysdig descobrem automaticamente as origens do Docker e coletam dados de eventos delas. É possível editar o arquivo de configuração do agente para mudar seu comportamento padrão e incluir ou excluir dados do evento. 

Por padrão, somente um conjunto limitado de eventos é coletado. O arquivo de configuração */opt/draios/etc/dragent.default.yaml* de configurações padrão inclui os eventos que são coletados. Para obter mais informações sobre os eventos que são coletados por padrão, consulte [Eventos do Docker ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://sysdigdocs.atlassian.net/wiki/spaces/Platform/pages/234356795/Enable+Disable+Event+Data#Enable/DisableEventData-DockerEvents){:new_window}.

Para incluir ou remover eventos, deve-se customizar o arquivo *dragent.yaml* e especificar quais eventos incluir e quais filtrar. **Nota:** uma entrada em uma seção no *dragent.yaml* substitui a seção inteira na configuração padrão.
{: tip}

Por exemplo, para filtrar eventos de imagem do Docker e coletar somente eventos para as ações de anexar, confirmar e copiar, deve-se configurar a seção *docker* conforme a seguir:

* Opção 1: definir a sequência em entradas como uma lista com marcadores:

    ```
    events:
      docker:
        image: none
        container:
          - conexão
          - commit
          - cópia
    ```
    {: codeblock}

* Opção 2: definir a sequência em entradas em uma única linha entre colchetes:

    ```
    events:
      docker:
        image: none
        container: [attach, commit, copy]
    ```
    {: codeblock}


## Desativando a coleta de eventos
{: #change_container_agent_disable_events}

Para desativar a coleta de eventos de um agente Sysdig, modifique o arquivo *dragent.default.yaml*. Configure a seção **events** como *none* no arquivo *dragent.yaml*.

Por exemplo, para filtrar eventos do Docker, deve-se configurar a seção *events* no arquivo *dragent.yaml*, conforme a seguir:

```
eventos: docker: nenhum
```
{: codeblock}



## Filtrando eventos por severidade
{: #change_container_agent_filterby_severity}

Para filtrar eventos por severidade, também é possível mudar o tipo de entrada de log para eventos no arquivo *dragent.yaml*. 

O nível de log padrão é **informações**. Isso significa que apenas eventos de aviso e de severidade mais alta são transmitidos.

Os níveis válidos são: *emergencial*, *alerta*, *crítico*, *erro*, *aviso*, *aviso*, *informações*, *depuração* e *nenhum*. **Nota**: os valores são listados de alta prioridade para baixa prioridade.

Por exemplo, para filtrar eventos de baixa severidade (*aviso*, *informações*, *depuração*), deve-se configurar a seção de log **event_priority** como *aviso*:

```
log: event_priority: warning
```
{: codeblock}


Para bloquear a coleta de eventos, deve-se configurar a seção de log **event_priority** como *none*:

```
log: event_priority: none
```
{: codeblock}




## Incluindo e excluindo métricas
{: #change_container_agent_inc_exc_metrics}

Para filtrar as métricas customizadas, deve-se customizar a seção **metrics_filter** no arquivo *dragent.yaml*. É possível especificar quais métricas incluir e quais filtrar, configurando os parâmetros de filtragem **include** e **exclude**.

**Nota:** a ordem da regra de filtragem é configurada como a seguir: a primeira regra que corresponder a uma métrica será aplicada.

Por exemplo, se a seção *metrics_filter* de um agente Sysdig for semelhante ao seguinte:

```
metrics_filter:
  - include: metricA.*
  - exclude: metricA.*
  - include: metricB.*
  - include: haproxy.backend.*
  - exclude: haproxy.*
  - exclude: metricC.*
```
{: screen}

* Você está configurando o agente Sysdig para coletar todos os dados de métricas iniciadas com *metricA*, *metricB* e *haproxy.backend*. 
* Você está filtrando métricas iniciadas com *metricC* e outras métricas iniciadas com *haproxy*. 
* A entrada `exclude: metricA.*` é ignorada.


## Mudando o nível de log
{: #change_container_agent_log_level}

Para configurar o nível de log, deve-se customizar a seção de **log** no arquivo *dragent.yaml*. 

O agente Sysdig gera entradas de log em */opt/draios/logs/draios.log*. 
* O arquivo de log gira ao atingir 10 MB de tamanho.
* Os 10 arquivos de log mais recentes são mantidos. O registro de data anexado ao nome do arquivo é usado para determinar quais arquivos manter.
* Os níveis de log válidos são: *nenhum*, *erro*, *aviso*, *informações*, *depuração*, *rastreio*
* O nível de log padrão é *informações*, em que uma entrada é criada para cada transmissão de métricas agregadas para os servidores de backend, uma vez por segundo, além das entradas para quaisquer avisos e erros.
* É possível customizar o tipo de log e as entradas coletadas, configurando o arquivo de configuração do agente Sysdig **/opt/draios/etc/dragent.yaml**. Depois de editar o arquivo, deve-se reiniciar o agente no shell com `docker restart sysdig-agent` para ativar as mudanças.

| Casos de uso                                     | Entrada de seção de log           |
|-----------------------------------------------|-----------------------------|
| Solucionar problemas de comportamento do agente                   | `file_priority: debug`      |
| Reduza a saída de console do contêiner               | `console_priority: warning` |
| Filtrando eventos por severidade                  | `event_priority: warning`   |
| Verifique quais métricas estão incluídas ou excluídas  | `metrics_excess_log: true`  |
{: caption="Tabela 2. Entradas de seção de log" caption-side="top"} 


