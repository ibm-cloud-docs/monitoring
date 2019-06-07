---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-06"

keywords: Sysdig, IBM Cloud, monitoring, customize, kubernetes agent

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

# Customizando os agentes Sysdig do Kubernetes
{: #change_kube_agent}

No {{site.data.keyword.mon_full_notm}}, é possível customizar a configuração do agente Sysdig para definir um nível de log, bloquear portas, incluir ou excluir dados de métrica, incluir ou remover eventos e filtrar contêineres. 
{:shortdesc}

Para customizar um agente Sysdig do Kubernetes, pode ser necessário configurar seções em qualquer um dos arquivos a seguir:

| Nome do arquivo                        | Ações       |
|----------------------------------|-------------------|
| `sysdig-agent-daemonset-v2.yaml` | Modifique o nível de log. |
| `sysdig-agent-configmap.yaml`    | Bloquear portas. </br>Incluir ou excluir dados de métrica. </br>Incluir ou remover eventos. </br>Filtrar contêineres. |
{: caption="Tabela 1. Arquivos de configuração do agente Sysdig do Kubernetes" caption-side="top"} 

Para editar um agente Sysdig do Kubernetes, pode ser necessário editar o *sysdig-agent-configmap.yaml*, o *sysdig-agent-daemonset-v2.yaml* ou ambos.
{: tip}

Há dois métodos que podem ser usados para modificar um arquivo de configuração:
* Método 1: modificar o arquivo diretamente no cluster no qual o agente está em execução.
* Método 2: modificar o arquivo localmente e aplicar as mudanças ao cluster.

## Editando a configuração do agente Sysdig do Kubernetes usando kubectl edit
{: #change_kube_agent_edit_kube_agent_method1}

Conclua as etapas a seguir para editar uma configuração do agente Sysdig do Kubernetes:

1. Configure o ambiente em cluster. Execute os comandos a seguir:

    Primeiro, obtenha o comando para configurar a variável de ambiente e fazer download dos arquivos de configuração do Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Quando o download dos arquivos de configuração estiver concluído, será exibido um comando que poderá ser usado para configurar o caminho para o seu arquivo de configuração local do Kubernetes como uma variável de ambiente.

    Em seguida, copie e cole o comando exibido em seu terminal para configurar a variável de ambiente KUBECONFIG.

    **Nota:** toda vez que você efetua login na CLI do {{site.data.keyword.containerlong}} para trabalhar com clusters, deve-se executar esses comandos para configurar o caminho para o arquivo de configuração do cluster como uma variável de sessão. O Kubernetes CLI usa essa variável para localizar um arquivo de configuração local e certificados que são necessárias para se conectar ao cluster no {{site.data.keyword.cloud_notm}}.

2. Edite o arquivo *sysdig-agent-configmap.yaml*. 

    Execute o seguinte comando:

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

    Faça mudanças. **Nota:** consulte as instruções do editor `vi` para saber como fazer mudanças.

    Salve as mudanças. As mudanças são aplicadas automaticamente. 

3. Edite o arquivo *sysdig-agent-daemonset-v2.yaml*. 

    Execute o seguinte comando: 

    ```
    kubectl edit daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

    Faça mudanças. **Nota:** consulte as instruções do editor `vi` para saber como fazer mudanças.

    Salve as mudanças. As mudanças são aplicadas automaticamente.

## Editando a configuração do agente Sysdig do Kubernetes usando kubectl apply
{: #change_kube_agent_edit_kube_agent_method2}

Use esse método se você tiver os arquivos yaml de configuração armazenados e gerenciados em um sistema de controle de origem.

Conclua as etapas a seguir para editar uma configuração do agente Sysdig do Kubernetes:

1. Obtenha a cópia mais recente de cada arquivo do controlador de origem. 

    Para criar um arquivo local com a configuração que está implementada em um cluster, é possível também executar o comando:
    
    ```
    kubectl get configmap sysdig-agent -n=ibm-observe -o=yaml > prod-sysdig-agent-configmap.yaml
    ```
    {: codeblock} 
    
    ou 
    
    ```
    kubectl get daemonset sysdig-agent -n=ibm-observe -o=yaml > prod-sysdig-agent-daemonset-v2.yaml
    ```
    {: codeblock}

2. Edite a configuração.

3. Aplique as mudanças usando os comandos a seguir:

    ```
    kubectl apply -f sysdig-agent-configmap.yaml
    ```
    {: codeblock}
    
    ou
    
    ```
    kubectl apply -f sysdig-agent-daemonset-v2.yaml
    ```
    {: codeblock}

Os agentes em execução selecionarão automaticamente a nova configuração após o Kubernetes enviar por push as mudanças em todos os nós no cluster.


## Incluindo mais tags em dados coletados de um agente Sysdig do Kubernetes
{: #change_kube_agent_add_tags}

Conclua as etapas a seguir para incluir mais tags em uma configuração do agente Sysdig do Kubernetes que você já implementou:

1. Configure o ambiente em cluster. Execute os comandos a seguir:

    Primeiro, obtenha o comando para configurar a variável de ambiente e fazer download dos arquivos de configuração do Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Quando o download dos arquivos de configuração estiver concluído, será exibido um comando que poderá ser usado para configurar o caminho para o seu arquivo de configuração local do Kubernetes como uma variável de ambiente.

    Em seguida, copie e cole o comando exibido em seu terminal para configurar a variável de ambiente KUBECONFIG.

    **Nota:** toda vez que você efetua login na CLI do {{site.data.keyword.containerlong}} para trabalhar com clusters, deve-se executar esses comandos para configurar o caminho para o arquivo de configuração do cluster como uma variável de sessão. O Kubernetes CLI usa essa variável para localizar um arquivo de configuração local e certificados que são necessárias para se conectar ao cluster no {{site.data.keyword.cloud_notm}}.

2. Edite o arquivo *sysdig-agent-configmap.yaml*. 

    Execute o seguinte comando:

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Faça mudanças. **Nota:** consulte as instruções do editor `vi` para saber como fazer mudanças.

    ```
    apiVersion: v1
      data:
        dragent.yaml: |
            k8s_cluster_name: marisa-production
            collector: ingest.us-south.monitoring.cloud.ibm.com
            collector_port: 6443
            ssl: true
            sysdig_capture_enabled: false
            new_k8s: true
            tags: department:finance,region:us-south
      ...
    ```
    {: codeblock}

4. Salve as mudanças. 

As mudanças são aplicadas automaticamente. 

Para a amostra fornecida, você obteria as tags **agent.tag.cluster_version** e **agent.tag.region**. Você poderia usá-las para definir alertas, customizar escopos e mais.



## Coletando um conjunto de eventos do Kubernetes
{: #change_kube_agent_collect_events}

O {{site.data.keyword.mon_full_notm}}  suporta integrações de eventos com Kubernetes. Os agentes Sysdig descobrem automaticamente esses serviços e coletam dados do evento deles. É possível editar o arquivo de configuração do agente para mudar seu comportamento padrão e incluir ou excluir dados do evento. 

Por padrão, somente um conjunto limitado de eventos é coletado. Para obter mais informações sobre os eventos que são coletados por padrão, consulte [Eventos do Kubernetes ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://sysdigdocs.atlassian.net/wiki/spaces/Platform/pages/234356795/Enable+Disable+Event+Data#Enable/DisableEventData-KubernetesEvents){:new_window}.

Para incluir ou remover eventos, deve-se customizar o arquivo *sysdig-agent-configmap.yaml* e especificar quais eventos incluir e quais filtrar. **Nota:** uma entrada em uma seção no *sysdig-agent-configmap.yaml* substitui a seção inteira na configuração padrão.
{: tip}

Para filtrar eventos de pods do Kubernetes, conclua as etapas a seguir:

1. Configure o ambiente em cluster. Execute os comandos a seguir:

    Primeiro, obtenha o comando para configurar a variável de ambiente e fazer download dos arquivos de configuração do Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Quando o download dos arquivos de configuração estiver concluído, será exibido um comando que poderá ser usado para configurar o caminho para o seu arquivo de configuração local do Kubernetes como uma variável de ambiente.

    Em seguida, copie e cole o comando exibido em seu terminal para configurar a variável de ambiente KUBECONFIG.

    **Nota:** toda vez que você efetua login na CLI do {{site.data.keyword.containerlong}} para trabalhar com clusters, deve-se executar esses comandos para configurar o caminho para o arquivo de configuração do cluster como uma variável de sessão. O Kubernetes CLI usa essa variável para localizar um arquivo de configuração local e certificados que são necessárias para se conectar ao cluster no {{site.data.keyword.cloud_notm}}.

2. Edite o arquivo *sysdig-agent-configmap.yaml*. 

    Execute o seguinte comando:

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Faça mudanças. Inclua a seção de *eventos* ou atualize a seção.

    **Nota:** consulte as instruções do editor `vi` para saber como fazer mudanças.

    Por exemplo, você pode desejar coletar eventos de pulling do pod do Kubernetes e filtrar outros eventos de pod que são coletados por padrão. Você deseja ainda coletar eventos padrão do Kubernetes para os nós e os replicationControllers.

    ```
    events: kubernetes: pod:
          - Pulling
    ```
    {: codeblock}

4. Salve as mudanças. 

As mudanças são aplicadas automaticamente. 


Outro exemplo no qual é possível ver como coletar um subconjunto de eventos do Kubernetes: você deseja monitorar somente eventos de pulling, pulled e failed para os pods.

* Opção 1: definir a sequência em entradas como uma lista com marcadores:

    ```
    events: kubernetes: pod: 
          - Pulling
          - Pulled
          - Failed
    ```
    {: codeblock}

* Opção 2: definir a sequência em entradas em uma única linha entre colchetes:

    ```
    events:
      kubernetes:
        pod: [Pulling, Pulled, Failed]
    ```
    {: codeblock}

Para obter mais informações sobre como trabalhar com eventos customizados, consulte [Trabalhando com eventos customizados ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/222822463/Custom+Events){:new_window}.


## Desativando a coleta de eventos
{: #change_kube_agent_disable_events}

Para desativar a coleta de eventos de um agente Sysdig do Kubernetes, deve-se modificar o arquivo *sysdig-agent-configmap.yaml*. Configure a entrada **Kubernetes** na seção **events** como *none*. 

Conclua as etapas a seguir:

1. Configure o ambiente em cluster. Execute os comandos a seguir:

    Primeiro, obtenha o comando para configurar a variável de ambiente e fazer download dos arquivos de configuração do Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Quando o download dos arquivos de configuração estiver concluído, será exibido um comando que poderá ser usado para configurar o caminho para o seu arquivo de configuração local do Kubernetes como uma variável de ambiente.

    Em seguida, copie e cole o comando exibido em seu terminal para configurar a variável de ambiente KUBECONFIG.

    **Nota:** toda vez que você efetua login na CLI do {{site.data.keyword.containerlong}} para trabalhar com clusters, deve-se executar esses comandos para configurar o caminho para o arquivo de configuração do cluster como uma variável de sessão. O Kubernetes CLI usa essa variável para localizar um arquivo de configuração local e certificados que são necessárias para se conectar ao cluster no {{site.data.keyword.cloud_notm}}.

2. Edite o arquivo *sysdig-agent-configmap.yaml*. 

    Execute o seguinte comando:

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Faça mudanças. Inclua a seção de *eventos* ou atualize a seção.

    ```
    events:
      kubernetes: none
    ```
    {: codeblock}

6. Salve as mudanças. 

As mudanças são aplicadas automaticamente. 






## Incluindo e excluindo métricas
{: #change_kube_agent_inc_exc_metrics}

Para filtrar as métricas customizadas, deve-se customizar a seção **metrics_filter** no arquivo *sysdig-agent-configmap.yaml*. É possível especificar quais métricas incluir e quais filtrar, configurando os parâmetros de filtragem **include** e **exclude**.

<p class="important">A ordem de regra de filtragem é configurada conforme a seguir: a primeira regra que corresponde a uma métrica é aplicada. As regras de acompanhamento para essa métrica são ignoradas.</p>

Conclua as etapas a seguir:

1. Configure o ambiente em cluster. Execute os comandos a seguir:

    Primeiro, obtenha o comando para configurar a variável de ambiente e fazer download dos arquivos de configuração do Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Quando o download dos arquivos de configuração estiver concluído, será exibido um comando que poderá ser usado para configurar o caminho para o seu arquivo de configuração local do Kubernetes como uma variável de ambiente.

    Em seguida, copie e cole o comando exibido em seu terminal para configurar a variável de ambiente KUBECONFIG.

    **Nota:** toda vez que você efetua login na CLI do {{site.data.keyword.containerlong}} para trabalhar com clusters, deve-se executar esses comandos para configurar o caminho para o arquivo de configuração do cluster como uma variável de sessão. O Kubernetes CLI usa essa variável para localizar um arquivo de configuração local e certificados que são necessárias para se conectar ao cluster no {{site.data.keyword.cloud_notm}}.

2. Edite o arquivo *sysdig-agent-configmap.yaml*. 

    Execute o seguinte comando:

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Faça mudanças. Inclua a seção de *metrics_filter* ou atualize a seção.

    Por exemplo, se a seção *metrics_filter* de um agente Sysdig for semelhante ao seguinte:

    ```
    metrics_filter:
      - include: metricA.*
      - excluir: metricA.*
      - include: metricB.*
      - include: haproxy.backend.*
      - exclude: haproxy.*
      - excluir: metricC.*
    ```
    {: screen}

    * Você está configurando o agente Sysdig para coletar todos os dados de métricas iniciadas com *metricA*, *metricB* e *haproxy.backend*. 

    * Você está filtrando métricas iniciadas com *metricC* e outras métricas iniciadas com *haproxy*. 

    * A entrada `exclude: metricA.*` é ignorada.

4. Salve as mudanças. 

As mudanças são aplicadas automaticamente. 




## Filtrando objetos e contêineres do Kubernetes por meio dos quais os dados são coletados
{: #change_kube_agent_filter_data}

Um agente Sysdig do Kubernetes coleta automaticamente as métricas de *todos os contêineres* que ele detecta em um cluster, incluindo Prometheus, StatsD, JMX, verificações de aplicativo e métricas integradas.
 
É possível customizar o agente Sysdig para excluir contêineres da coleção de métricas. 

Ao excluir contêineres, considere as informações a seguir:
* Você reduz o agente e o carregamento de backend.
* Você só coleta dados de contêineres que deseja monitorar.
* É possível controlar custos relatando contêineres importantes e filtrando contêineres desnecessários ou não críticos.

Para ativar o recurso no qual um agente Sysdig filtra contêineres, deve-se customizar o arquivo *sysdig-agent-configmap.yaml*. Configure a entrada **use_container_filter** na seção **containers** como *true*. **Nota:** por padrão, esse recurso está desativado. Em seguida, defina as regras que incluem uma ou mais condições e que você deseja aplicar.

A tabela a seguir descreve os parâmetros que podem ser definidos para configurar as regras de filtragem em um cluster:

| Parâmetro                          | Condição                                      |
|------------------------------------|------------------------------------------------|
| `container.image`                  | Nome da imagem do contêiner                           |
| `container.name`                   | Nome do contêiner                                 |
| `container.label.*`                | Rótulo do contêiner                                |
| `kubernetes.object.*`             | Objeto Kubernetes. Um objeto pode ser um pod, um namespace, etc.   |
| `kubernetes.object.annotation.*`  | Anotação de objeto do Kubernetes                   |
| `kubernetes.object.label.*`       | Rótulo do objeto Kubernetes                        |
| `all`                              | Regra padrão para especificar todos os objetos            |
{: caption="Tabela 2. Parâmetros para definir condições em contêineres" caption-side="top"} 

Considere as informações a seguir sobre como o agente Sysdig aplica as regras definidas na seção **container_filter**:
* Você define condições configurando-os com os parâmetros de filtragem **include** e **exclude**. 
* A primeira regra de correspondência na lista determina se o contêiner está incluído ou excluído.
* As condições consistem em um nome de chave e um valor. Se a chave fornecida para um contêiner corresponder ao valor, a regra será aplicada.
* Quando uma regra contém múltiplas condições, `todas as condições` precisam corresponder para que a regra seja aplicada.

Conclua as etapas a seguir para filtrar contêineres que um agente Sysdig monitora em um cluster:

1. Configure o ambiente em cluster. Execute os comandos a seguir:

    Primeiro, obtenha o comando para configurar a variável de ambiente e fazer download dos arquivos de configuração do Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Quando o download dos arquivos de configuração estiver concluído, será exibido um comando que poderá ser usado para configurar o caminho para o seu arquivo de configuração local do Kubernetes como uma variável de ambiente.

    Em seguida, copie e cole o comando exibido em seu terminal para configurar a variável de ambiente KUBECONFIG.

    **Nota:** toda vez que você efetua login na CLI do {{site.data.keyword.containerlong}} para trabalhar com clusters, deve-se executar esses comandos para configurar o caminho para o arquivo de configuração do cluster como uma variável de sessão. O Kubernetes CLI usa essa variável para localizar um arquivo de configuração local e certificados que são necessárias para se conectar ao cluster no {{site.data.keyword.cloud_notm}}.

2. Edite o arquivo *sysdig-agent-configmap.yaml*. 

    Execute o seguinte comando:

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Faça mudanças. Inclua a seção de *metrics_filter* ou atualize a seção.

    Por exemplo, consulte a extração a seguir de um mapa de configuração:

    ```
    containers:
        # Enable the feature
        use_container_filter: true
        #
        # Include or exclude conditions
        container_filter:
           - include:
                container.image: 
           - include:
                container.name: 
           - exclude:
                kubernetes.namespace.name: kube-system
    ```  
    {: codeblock}

6. Salve as mudanças. 

As mudanças são aplicadas automaticamente. 


## Bloqueando portas
{: #change_kube_agent_block_ports}

Para bloquear o tráfego de rede e as métricas de portas de rede, deve-se customizar a seção **blacklisted_ports** no arquivo *sysdig-agent-configmap.yaml*. Deve-se listar as portas das quais você deseja filtrar quaisquer dados.

**Nota:** a porta 53 (DNS) é sempre incluída na lista de bloqueio. 

Conclua as etapas a seguir:

1. Configure o ambiente em cluster. Execute os comandos a seguir:

    Primeiro, obtenha o comando para configurar a variável de ambiente e fazer download dos arquivos de configuração do Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Quando o download dos arquivos de configuração estiver concluído, será exibido um comando que poderá ser usado para configurar o caminho para o seu arquivo de configuração local do Kubernetes como uma variável de ambiente.

    Em seguida, copie e cole o comando exibido em seu terminal para configurar a variável de ambiente KUBECONFIG.

    **Nota:** toda vez que você efetua login na CLI do {{site.data.keyword.containerlong}} para trabalhar com clusters, deve-se executar esses comandos para configurar o caminho para o arquivo de configuração do cluster como uma variável de sessão. O Kubernetes CLI usa essa variável para localizar um arquivo de configuração local e certificados que são necessárias para se conectar ao cluster no {{site.data.keyword.cloud_notm}}.

2. Edite o arquivo *sysdig-agent-configmap.yaml*. 

    Execute o seguinte comando:

    ```
    kubectl edit configmap sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Faça mudanças. Inclua a seção de *metrics_filter* ou atualize a seção.

    Por exemplo, a amostra a seguir mostra como configurar a seção *blacklisted_ports* de um agente Sysdig para excluir dados vindos das portas 6666 e 6379:

    ```
    blacklisted_ports:
      - 6666
      - 6379
    ```
    {: screen}

6. Salve as mudanças. 

As mudanças são aplicadas automaticamente. 



## Mudando o nível de log
{: #change_kube_agent_log_level}

Para configurar o nível de log, deve-se customizar a seção **log** no arquivo *sysdig-agent-daemonset-v2.yaml*. 

O agente Sysdig gera entradas de log em */opt/draios/logs/draios.log*. 
* O arquivo de log gira ao atingir 10 MB de tamanho.
* Os 10 arquivos de log mais recentes são mantidos. O registro de data anexado ao nome do arquivo é usado para determinar quais arquivos manter.
* Os níveis de log válidos são: *nenhum*, *erro*, *aviso*, *informações*, *depuração*, *rastreio*
* O nível de log padrão é *informações*, em que uma entrada é criada para cada transmissão de métricas agregadas para os servidores de backend, uma vez por segundo, além das entradas para quaisquer avisos e erros.
* É possível customizar o tipo de log e as entradas coletadas, configurando o arquivo de configuração do agente Sysdig **/opt/draios/etc/dragent.yaml**. Depois de editar o arquivo, deve-se reiniciar o agente no shell com `service dragent restart` para ativar as mudanças.

A tabela a seguir lista alguns cenários comuns e o valor que deve ser configurado em cada um deles:

| Casos de uso                                     | Entrada de seção de log           |
|-----------------------------------------------|-----------------------------|
| Solucionar problemas de comportamento do agente                   | `file_priority: debug`      |
| Reduza a saída de console do contêiner               | `console_priority: warning` |
| Filtrando eventos por severidade                  | `event_priority: warning`   |
| Verifique quais métricas estão incluídas ou excluídas  | `metrics_excess_log: true`  |
{: caption="Tabela 2. Entradas de seção de log" caption-side="top"} 

Conclua as etapas a seguir para configurar o nível de log:

1. Configure o ambiente em cluster. Execute os comandos a seguir:

    Primeiro, obtenha o comando para configurar a variável de ambiente e fazer download dos arquivos de configuração do Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Quando o download dos arquivos de configuração estiver concluído, será exibido um comando que poderá ser usado para configurar o caminho para o seu arquivo de configuração local do Kubernetes como uma variável de ambiente.

    Em seguida, copie e cole o comando exibido em seu terminal para configurar a variável de ambiente KUBECONFIG.

    **Nota:** toda vez que você efetua login na CLI do {{site.data.keyword.containerlong}} para trabalhar com clusters, deve-se executar esses comandos para configurar o caminho para o arquivo de configuração do cluster como uma variável de sessão. O Kubernetes CLI usa essa variável para localizar um arquivo de configuração local e certificados que são necessárias para se conectar ao cluster no {{site.data.keyword.cloud_notm}}.

2. Edite o arquivo *sysdig-agent-daemonset-v2.yaml*. 

    Execute o seguinte comando:

    ```
    kubectl edit daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Faça mudanças. Inclua a seção de *log* ou atualize a seção.

    Por exemplo, para filtrar eventos de baixa severidade (*aviso*, *informações*, *depuração*), deve-se configurar a entrada **metrics_excess_log** na seção de **log** como *true*:

    ```
    log:
      file_priority: warning
      console_priority: info
      event_priority: warning
      metrics_excess_log: true
    ```
    {: codeblock}

6. Salve as mudanças. 

As mudanças são aplicadas automaticamente. 


## Filtrando eventos do Kubernetes por severidade
{: #change_kube_agent_filterby_severity}

Para filtrar eventos por severidade, deve-se modificar o arquivo *sysdig-agent-daemonset-v2.yaml*. Configure a entrada **event_priority** na seção **log** como *none*. 

O nível de log padrão é **informações**. Isso significa que apenas eventos de aviso e de severidade mais alta são transmitidos.

Os níveis válidos são: *emergencial*, *alerta*, *crítico*, *erro*, *aviso*, *aviso*, *informações*, *depuração* e *nenhum*. **Nota**: os valores são listados de alta prioridade para baixa prioridade.

Conclua as etapas a seguir:

1. Configure o ambiente em cluster. Execute os comandos a seguir:

    Primeiro, obtenha o comando para configurar a variável de ambiente e fazer download dos arquivos de configuração do Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Quando o download dos arquivos de configuração estiver concluído, será exibido um comando que poderá ser usado para configurar o caminho para o seu arquivo de configuração local do Kubernetes como uma variável de ambiente.

    Em seguida, copie e cole o comando exibido em seu terminal para configurar a variável de ambiente KUBECONFIG.

    **Nota:** toda vez que você efetua login na CLI do {{site.data.keyword.containerlong}} para trabalhar com clusters, deve-se executar esses comandos para configurar o caminho para o arquivo de configuração do cluster como uma variável de sessão. O Kubernetes CLI usa essa variável para localizar um arquivo de configuração local e certificados que são necessárias para se conectar ao cluster no {{site.data.keyword.cloud_notm}}.

2. Edite o arquivo *sysdig-agent-daemonset-v2.yaml*. 

    Execute o seguinte comando:

    ```
    kubectl edit daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Faça mudanças. Inclua a seção de *log* ou atualize a seção.

    Por exemplo, para filtrar eventos de baixa severidade (*aviso*, *informações*, *depuração*), deve-se configurar a seção de log **event_priority** como *aviso*:

    ```
    log: event_priority: warning
    ```
    {: codeblock}

6. Salve as mudanças. 

As mudanças são aplicadas automaticamente. 

## Registrando em um arquivo quais métricas estão incluídas ou excluídas
{: #change_kube_agent_log_metrics}

Para registrar em um arquivo as informações sobre quais métricas customizadas estão incluídas e quais estão excluídas, deve-se customizar o arquivo *sysdig-agent-daemonset-v2.yaml*. Configure a entrada **metrics_excess_log** como **true** na seção **log**.

* A criação de log é desativada por padrão. 
* A criação de log ocorre no nível INFO a cada 30 segundos e permanece por 10 segundos. 
* O arquivo de log está disponível em */opt/draios/logs/draios.log*.
* Os dados de criação de log são formatados conforme a seguir:

    ```
    +/-[ type ][metric included/excluded]: metric.name (filter: +/-[ metric.filter ])
    ```
    {: screen}

    * *+/-* é um símbolo que indica se a métrica está incluída ou excluída. Mais (*+*) indica que uma métrica está incluída. Menos (*-*) indica que uma métrica está excluída. 

    * *[type]* especifica o tipo de métrica, por exemplo, *statsd*.
    
    * *[metric included/excluded]* indica de uma maneira legível se a métrica está incluída ou excluída.

    *  * metric.name *  indica o nome da métrica.

    * *(filter: +/-[metric.filter])* fornece informações sobre quaisquer filtros que estão definidos na seção **metrics_filter** no arquivo *sysdig-agent-daemonset-v2.yaml*.

Uma entrada de amostra é semelhante à seguinte:

```
-[ statsd ] metric excluded: mongo.statsd.vsize (filter: -[mongo.statsd. * ])
+[statsd] metric included: mongo.statsd.netIn (filter: +[mongo.statsd.net*])
```
{: screen}

Conclua as etapas a seguir:

1. Configure o ambiente em cluster. Execute os comandos a seguir:

    Primeiro, obtenha o comando para configurar a variável de ambiente e fazer download dos arquivos de configuração do Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Quando o download dos arquivos de configuração estiver concluído, será exibido um comando que poderá ser usado para configurar o caminho para o seu arquivo de configuração local do Kubernetes como uma variável de ambiente.

    Em seguida, copie e cole o comando exibido em seu terminal para configurar a variável de ambiente KUBECONFIG.

    **Nota:** toda vez que você efetua login na CLI do {{site.data.keyword.containerlong}} para trabalhar com clusters, deve-se executar esses comandos para configurar o caminho para o arquivo de configuração do cluster como uma variável de sessão. O Kubernetes CLI usa essa variável para localizar um arquivo de configuração local e certificados que são necessárias para se conectar ao cluster no {{site.data.keyword.cloud_notm}}.

2. Edite o arquivo *sysdig-agent-daemonset-v2.yaml*. 

    Execute o seguinte comando:

    ```
    kubectl edit daemonset sysdig-agent -n ibm-observe
    ```
    {: codeblock}

3. Faça mudanças. Inclua a seção de *log* ou atualize a seção.

    Por exemplo, para filtrar eventos de baixa severidade (*aviso*, *informações*, *depuração*), deve-se configurar a entrada **metrics_excess_log** na seção de **log** como *true*:

    ```
    log:
      metrics_excess_log: true
    ```
    {: codeblock}

6. Salve as mudanças. 

As mudanças são aplicadas automaticamente. 


## Arquivo configmap yaml de amostra
{: #change_kube_agent_sample_configmap}

```
apiVersion: v1
data:
  dragent.yaml: | 
    ### Agent tags
    # tags: linux:ubuntu,dept:dev,local:nyc
    #### Sysdig Software related config 
    ####
    # Sysdig collector address
    # collector: 192.168.1.1
    # Collector TCP port
    # collector_port: 6666
    # Whether collector accepts ssl
    # ssl: true
    # collector certificate validation
    # ssl_verify_certificate: true
    #######################################
    #
    k8s_cluster_name: cluster12
    collector: ingest.us-south.monitoring.cloud.ibm.com
    collector_port: 6443
    ssl: true
    ssl_verify_certificate: true
    sysdig_capture_enabled: false
    new_k8s: true
    tags: type:mycluster,region:us-south
    blacklisted_ports:
      - 6666
      - 6379
    events:    
      kubernetes:
        node: 
          - Rebooted
      metrics_filter:
        - include: metricA.*
        - exclude: metricA.*
        - include: metricB.*
      use_container_filter: true
      container_filter: 
        - exclude:
          kubernetes.namespace.name: kube-system
kind: ConfigMap
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"v1","data":{"dragent.yaml":"### Agent tags\n# tags: linux:ubuntu,dept:dev,local:nyc\n#### Sysdig Software related config \n####\n# Sysdig collector address\n# collector: xxx.xxx.x.x\n# Collector TCP port\n# collector_port: 6666\n# Whether collector accepts ssl\n# ssl: true\n# collector certificate validation\n# ssl_verify_certificate: true\n#######################################\n#\nk8s_cluster_name: marisa-production\ncollector: ingest.us-south.monitoring.cloud.ibm.com\ncollector_port: 6443\nssl: true\nssl_verify_certificate: true\nsysdig_capture_enabled: true\nnew_k8s: true\ntags: cluster:mycluster,region:us-south\nevents:    \n  kubernetes:\n     node: \n       - Rebooted\nuse_container_filter: true\ncontainer_filter: \n      - exclude:\n         kubernetes.namespace.name: kube-system\n         container.image: \"registry.ng.bluemix.net/*\"\n"},"kind":"ConfigMap","metadata":{"annotations":{},"creationTimestamp":"2018-11-07T10:57:38Z","name":"sysdig-agent","namespace":"default","resourceVersion":"9999999","selfLink":"/api/v1/namespaces/default/configmaps/sysdig-agent","uid":"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"}}
  creationTimestamp: 2018-11-07T10:57:38Z
  name: sysdig-agent
  namespace: default
  resourceVersion: "9999999"
  selfLink: /api/v1/namespaces/default/configmaps/sysdig-agent
  uid: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```
{: codeblock}

## Arquivo yaml de daemonset de amostra
{: #change_kube_agent_sample_daemonset}

```
 Edite o objeto abaixo. Lines beginning with a '#' will be ignored,
# and an empty file will abort the edit. If an error occurs while saving this file will be
# reopened with the relevant failures.
#
apiVersion: extensions/v1beta1
kind: DaemonSet
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion ","kind": "DaemonSet": "DaemonSet": {1}{0}{2}{4}Mi ": {1}{0}{0}m", "memory ": "512Mi" } }, "segurityContext "": [ { }, "segurityContext "": [ {, "segurityContext "": [ {," readOnly ":false }, {, {, {, {, {, {, {, {, "name" :"dev-vol "}, {, {, "name ":" proc-vol "}, {, {th":{"path":"/boot"},"name":"boot-vol"},{"hostPath":{"path":"/lib/modules"},"name":"modules-vol"},{"hostPath":{"path":"/usr"},"name":"usr-vol"},{"configMap":{"name":"sysdig-agent","optional":true},"name":"sysdig-agent-config"},{"name":"sysdig-agent-secrets","secret":{"secretName":"sysdig-agent"}}]}},"updateStrategy":{"type":"RollingUpdate"}}}
  creationTimestamp: 2018-11-07T13:39:58Z
  generation: 2
  labels:
    app: sysdig-agent
  name: sysdig-agent
  namespace: default
  resourceVersion: "5980648"
  selfLink: /apis/extensions/v1beta1/namespaces/default/daemonsets/sysdig-agent
  uid: 9ea3353f-e292-11e8-b4b3-260d32136de0
spec:
  revisionHistoryLimit: 10
  selector:
    matchLabels:
      app: sysdig-agent
log:
  event_priority: warning
  file_priority: warning
  console_priority: info
  metrics_excess_log: true
```
{: codeblock}

