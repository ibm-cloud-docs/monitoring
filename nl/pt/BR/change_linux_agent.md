---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, customize, linux agent

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

# Customizando os agentes Sysdig do Linux
{: #change_linux_agent}

Por padrão, o agente Sysdig coleta dados de um intervalo de plataformas e aplicativos. É possível editar o arquivo de configuração do agente para mudar seu comportamento padrão e incluir ou excluir dados. É possível customizar o arquivo de configuração do agente Sysdig para incluir métricas customizadas, como JMX, StatsD e Prometheus. Também é possível filtrar métricas e contêineres.
{:shortdesc}

O agente Sysdig usa dois arquivos de configuração que especificam quais dados serão coletados automaticamente:

| Arquivo                   | Descrição                                                     | Localização                                |
|------------------------|-----------------------------------------------------------------|-----------------------------------------|
| `dragent.default.yaml` | Arquivo de configuração principal </br>**Nota:** **Não edite esse arquivo.  | `/opt/draios/etc/dragent.default.yaml`  |
| `dragent.yaml`         | Arquivo de configuração que você edita para customizar o agente Sysdig. | `/opt/draios/etc/dragent.yaml`          |
{: caption="Tabela 1. Arquivos de configuração do agente Sysdig" caption-side="top"} 

É possível editar o arquivo *dragent.yaml* para customizar os dados coletados. As mudanças entram em vigor imediatamente após o salvamento do arquivo. O agente detecta a mudança e reinicia automaticamente. É possível localizar a frequência e os arquivos verificados por um agente Sysdig no arquivo *dragent.default.yaml*.

Por exemplo, um *dragent.default.yaml* inclui as informações a seguir:

```
check_frequency_s: 5 arquivos: - /opt/draios/etc/dragent.yaml - /opt/draios/etc/kubernetes/config/dragent.yaml - /opt/draios/etc/kubernetes/secrets/access-key
```
{: screen}



## Editando o arquivo dragent yaml
{: #change_linux_agent_edit_agent}

O arquivo yaml está localizado em */opt/draios/etc/*.

Conclua as etapas a seguir para editar o arquivo e aplicar as mudanças:

1. Acesse o  * dragent.yaml *  diretamente. O arquivo está localizado em  ` /opt/draios/etc/dragent.yaml `.
2. Edite o arquivo. Use a sintaxe YAML válida.
3. Reinicie o agente. Execute o seguinte comando:

    ```
    service dragent restart
    ```
    {: codeblock}


## Bloqueando portas
{: #change_linux_agent_block_ports}

Para bloquear o tráfego de rede e as métricas de portas de rede, deve-se customizar a seção **blacklisted_ports** no arquivo *dragent.yaml*. Deve-se listar as portas das quais você deseja filtrar quaisquer dados.

**Nota:** a porta 53 (DNS) é sempre incluída na lista de bloqueio. 

Por exemplo, a amostra a seguir mostra como configurar a seção *blacklisted_ports* de um agente Sysdig para excluir dados vindos das portas 6666 e 6379:

```
blacklisted_ports: - 6666 - 6379
```
{: screen}

## Incluindo e excluindo métricas
{: #change_linux_agent_inc_exc_metrics}

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
{: #change_linux_agent_log_level}

Para configurar o nível de log, deve-se customizar a seção de **log** no arquivo *dragent.yaml*. 

O agente Sysdig gera entradas de log em */opt/draios/logs/draios.log*. 
* O arquivo de log gira ao atingir 10 MB de tamanho.
* Os 10 arquivos de log mais recentes são mantidos. O registro de data anexado ao nome do arquivo é usado para determinar quais arquivos manter.
* Os níveis de log válidos são: *nenhum*, *erro*, *aviso*, *informações*, *depuração*, *rastreio*
* O nível de log padrão é *informações*, em que uma entrada é criada para cada transmissão de métricas agregadas para os servidores de backend, uma vez por segundo, além das entradas para quaisquer avisos e erros.
* É possível customizar o tipo de log e as entradas coletadas, configurando o arquivo de configuração do agente Sysdig **/opt/draios/etc/dragent.yaml**. Depois de editar o arquivo, deve-se reiniciar o agente no shell com `service dragent restart` para ativar as mudanças.

| Casos de uso                                     | Entrada de seção de log           |
|-----------------------------------------------|-----------------------------|
| Solucionar problemas de comportamento do agente                   | `file_priority: debug`      |
| Reduza a saída de console do contêiner               | `console_priority: warning` |
| Filtrando eventos por severidade                  | `event_priority: warning`   |
| Verifique quais métricas estão incluídas ou excluídas  | `metrics_excess_log: true`  |
{: caption="Tabela 2. Entradas de seção de log" caption-side="top"} 
