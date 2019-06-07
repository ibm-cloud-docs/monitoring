---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-10"

keywords: Sysdig, IBM Cloud, monitoring, kubernetes, analyze metrics

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


# Analisando métricas para um app que é implementado em um cluster Kubernetes
{: #kubernetes_cluster}

Use esse tutorial para aprender como configurar um cluster do {{site.data.keyword.containerlong}} para encaminhar métricas para o serviço do {{site.data.keyword.mon_full}}.
{:shortdesc}

Para configurar um cluster para encaminhar métricas, deve-se instalar um agente Sysdig em cada nó do trabalhador em seu cluster Kubernetes usando um [DaemonSet ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/). O agente Sysdig usa uma chave de acesso (token) para autenticar com a instância do {{site.data.keyword.mon_full_notm}}. O agente Sysdig age como um coletor de dados. Ele coleta automaticamente métricas como *CPU do nó do trabalhador* e uso de *memória do nó do trabalhador*, *tráfego HTTP dentro e fora de seus contêineres* e dados sobre vários componentes de infraestrutura. Além disso, o agente pode coletar métricas de aplicativos customizadas
usando um scraper compatível com o Prometheus ou uma fachada StatsD. 

Você visualiza métricas por meio da interface com o usuário baseada na web do Sysdig.

![Visão geral de componentes no {{site.data.keyword.cloud_notm}}](../images/kube.png "Visão geral de componentes no {{site.data.keyword.cloud_notm}}")

## Objetivos
{: #kubernetes_cluster_objectives}

Nesse tutorial, você configura métricas com o Sysdig em seu cluster do {{site.data.keyword.containerlong}}. Em particular, você:
*  Provisiona uma instância do {{site.data.keyword.mon_full_notm}}.
*  Configura o agente Sysdig em seu cluster para enviar métricas para o Sysdig.
*  Usa a IU da web Sysdig para analisar suas métricas de cluster.


## Antes de iniciar
{: #kubernetes_cluster_prereqs}

1. Leia sobre o {{site.data.keyword.mon_full_notm}}. Para obter mais informações, consulte [Sobre](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-about#about).

2. Tenha um ID do usuário que seja um membro ou um proprietário de uma conta do {{site.data.keyword.cloud_notm}}. Para obter um ID do usuário do {{site.data.keyword.cloud_notm}}, acesse: [Registro ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/login){:new_window}.

3. Instale a CLI do {{site.data.keyword.cloud_notm}} e o plug-in da CLI do Kubernetes. Para obter mais informações, consulte [Instalando a CLI do {{site.data.keyword.cloud_notm}}](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli).

4. [Crie um cluster](/docs/containers?topic=containers-clusters#clusters) ou use um
cluster existente do {{site.data.keyword.containerlong_notm}}.
    *  O cluster deve executar o Kubernetes versão 1.10 ou acima.
    *  O cluster não precisa estar no local **Dallas**, mas pode estar em qualquer [região do {{site.data.keyword.containerlong_notm}}](/docs/containers/cs_regions.html#regions-and-zones).

5. Certifique-se de que seu ID do usuário esteja designado às políticas do {{site.data.keyword.iamlong}} a seguir:

| Recurso                             | Escopo da política de acesso | Função    | Região    | Informações                  |
|--------------------------------------|----------------------------|---------|-----------|------------------------------|
| Grupo de recursos **padrão**           |  Grupo de recursos            | Visualizador  | Us-south  | Essa política é necessária para permitir que o usuário veja instâncias de serviço no grupo de recursos Padrão.    |
| Serviço {{site.data.keyword.mon_full_notm}} |  Grupo de recursos            | Editor  | Us-south  | Essa política é necessária para permitir que o usuário provisione e administre o serviço {{site.data.keyword.mon_full_notm}} no grupo de recursos padrão.   |
| Instância de cluster Kubernetes          |  Recurso                 | Editor  | Us-south  | Essa política é necessária para configurar o segredo e o agente Sysdig no cluster Kubernetes. |
{: caption="Tabela 1. Lista de políticas do IAM necessárias para concluir o tutorial" caption-side="top"}

Para obter mais informações sobre as funções do IAM do {{site.data.keyword.containerlong}}, consulte [Permissões de acesso de usuário](/docs/containers?topic=containers-access_reference#access_reference).



## Etapa 1. Provisão de uma instância do {{site.data.keyword.mon_full_notm}}
{: #kubernetes_cluster_step1}

Neste tutorial de obtenção, as instruções são fornecidas para provisionar uma instância do {{site.data.keyword.mon_full_notm}} na região sul dos EUA. Para obter mais informações sobre
regiões suportadas, veja [Regiões](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints).

Para provisionar uma instância do {{site.data.keyword.mon_full_notm}} por meio da IU do {{site.data.keyword.cloud_notm}}, conclua as etapas a seguir:

1. [Efetue login em sua conta do {{site.data.keyword.cloud_notm}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/login){:new_window}.

	Depois de efetuar login com seu ID de usuário e senha, a IU do {{site.data.keyword.cloud_notm}} é aberta.

2. Clique em  ** Catálogo **. A lista dos serviços disponíveis no {{site.data.keyword.cloud_notm}} é aberta.

3. Para filtrar a lista de serviços exibida, selecione a categoria **Ferramentas do desenvolvedor**.

4. Clique no quadro  ** {{site.data.keyword.mon_full_notm}} **. O painel *Observabilidade* é aberto.

5. Selecione **Criar instância**. 

6. Insira um nome para a instância de serviço.

7. Selecione o grupo de recursos **padrão**. 

    É possível provisionar a instância em qualquer grupo de recursos no qual tenha permissões
para criar recursos.

    Por padrão, o grupo de recursos **default** é configurado.

8. Selecione o plano de serviço  ** Experimental **. 

    Por padrão, o plano de **Experiência** é configurado.

    Para obter mais informações sobre outros planos de serviços, consulte [Planos de precificação](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-pricing_plans#pricing_plans).

9. Clique em  ** Criar **.

    Depois de provisionar uma instância, o painel *Observabilidade* é aberto e mostra
detalhes para suas instâncias de **Monitoramento**. 


Para provisionar uma instância por meio da CLI, veja [Provisionando
uma instância por meio da CLI do {{site.data.keyword.cloud_notm}}](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-provision#provision_cli).
{: note}


## Etapa 2. Configurar seu cluster Kubernetes para enviar métricas para sua instância
{: #kubernetes_cluster_step2}

Para configurar seu cluster Kubernetes para enviar métricas para sua instância do {{site.data.keyword.mon_full_notm}}, deve-se instalar um pod do agente Sysdig em cada nó de seu cluster. O agente Sysdig é instalado por meio de um DaemonSet, que assegura que uma instância do agente esteja em execução em cada nó do trabalhador. O agente Sysdig coleta métricas do pod no qual ele está instalado e encaminha os dados para sua instância.

Para fornecer o conjunto completo de métricas do sistema, o agente Sysdig precisa ter um status privilegiado.
{: note}

Para configurar seu cluster Kubernetes para encaminhar métricas para sua instância do {{site.data.keyword.mon_full_notm}}, conclua as etapas a seguir na linha de comandos:

1. Abra um terminal. Em seguida, efetue login no {{site.data.keyword.cloud_notm}}. Execute o comando a seguir e siga os prompts:

    ```
    ibmcloud login -a cloud.ibm.com
    ```
    {: codeblock}

    Selecione a conta na qual o cluster está disponível.

2. Configure o ambiente em cluster. Execute os comandos a seguir:

    Primeiro, obtenha o comando para configurar a variável de ambiente e fazer download dos arquivos de configuração do Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    Quando o download dos arquivos de configuração estiver concluído, será exibido um comando que poderá ser usado para configurar o caminho para o seu arquivo de configuração local do Kubernetes como uma variável de ambiente. Copie e cole o comando que é exibido em seu terminal para configurar a variável de ambiente `KUBECONFIG`.

    Toda vez que você efetua login na CLI do {{site.data.keyword.containerlong}} para trabalhar com clusters, deve-se executar esses comandos para configurar o caminho para o arquivo de configuração do cluster como uma variável de sessão. O Kubernetes CLI usa essa variável para localizar um arquivo de configuração local e certificados que são necessárias para se conectar ao cluster no {{site.data.keyword.cloud_notm}}.
    {: tip}

3. Obtenha a chave de acesso do Sysdig. Para obter mais informações, consulte [Obtendo a chave de acesso por meio da IU do {{site.data.keyword.cloud_notm}}](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui).

4. Obtenha a URL de ingestão nos [terminais
de coletor do Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion).

5. Implemente o agente Sysdig. Execute o seguinte comando:

    ```
    curl -sL https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/IBMCloud-Kubernetes-Service/install-agent-k8s.sh | bash -s -- -a SYSDIG_ACCESS_KEY -c COLLECTOR_ENDPOINT -t TAG_DATA -ac 'sysdig_capture_enabled: false'
    ```
    {: pre}

    Em que

    * **SYSDIG_ACCESS_KEY** é a chave de ingestão para a instância que você recuperou anteriormente.

    * **COLLECTOR_ENDPOINT** é a URL de ingestão para a região na qual a instância de monitoramento está disponível que você recuperou anteriormente.

    * **TAG_DATA** são tags separadas por vírgula formatadas como *TAG_NAME:TAG_VALUE*. É possível associar uma ou mais tags a seu agente Sysdig. Por exemplo: *role:serviceX,location:us-south*. Posteriormente, será possível usar essas tags para identificar métricas no ambiente em que o agente está em execução.

    * Configure **sysdig_capture_enabled** como *false* para desativar o recurso de captura de Sysdig. Por padrão, é configurado como *true*. Para obter mais informações, consulte [Trabalhando com capturas](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures).

6. Verifique se o agente Sysdig foi criado com êxito e seu status. Execute o seguinte comando:

    ```
    kubectl get pods -n ibm-observe
    ```
    {: codeblock}

    A implementação é bem-sucedida quando você vê um ou mais pods `sysdig-agent`. O número de pods `sysdig-agent` é igual ao número de nós do trabalhador em seu cluster. Todos os pods devem estar em um estado `Executando`.


## Etapa 3. Ativar a IU da web do Sysdig
{: #kubernetes_cluster_step3}

Para ativar a IU da web do Sysdig por meio do console do {{site.data.keyword.cloud_notm}},
conclua as etapas a seguir.

É possível ter apenas uma sessão de IU da web aberta por navegador.
{: imp}

1. [Efetue login em sua conta do {{site.data.keyword.cloud_notm}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/login){:new_window}.

	Depois que você efetua login com seu ID do usuário e senha, o Painel do {{site.data.keyword.cloud_notm}} é aberto.

2. No menu ![Ícone de link externo](../../../icons/icon_hamburger.svg "Ícone de menu"), selecione **Observabilidade**. 

3. Selecione **Monitorando**. A lista de instâncias disponíveis no {{site.data.keyword.cloud_notm}} é exibida.

4. Localize sua instância e clique em **Visualizar Sysdig**.

    * **Primeira vez**: como você já instalou o agente Sysdig, pode ignorar o assistente de instalação, iniciar e concluir a integração.
    
    * **Tempos subsequentes**: a visualização **Explorar** é aberta.


Se o agente Sysdig não for instalado com sucesso, apontar para o terminal de ingestão errado ou se
a chave de acesso estiver incorreta, a página que será aberta informará sobre o que fazer em seguida.

Por exemplo, se o agente Sysdig não for instalado com sucesso, não será possível ignorar o assistente de instalação. Você poderá ver uma mensagem semelhante à seguinte:
    
```
Aguardando o primeiro nó se conectar... Continue e siga as instruções abaixo.
```
{: screen}
    
É possível tentar as ações a seguir:
*  Verifique se você está usando o [terminal](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion) `ingest` e não o terminal do Sysdig. 
*  Verifique se a [chave de acesso](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key) está correta.
*  Siga todas as instruções adicionais e repita as etapas neste tutorial.



## Etapa 4. Monitorar seu cluster
{: #kubernetes_cluster_step4}

É possível monitorar seu cluster na visualização **EXPLORAR** que está disponível
por meio da IU da web do Sysdig. Essa visualização é a página inicial padrão e seu ponto de início para
solucionar problemas e monitorar a infraestrutura do cluster e os recursos.

Na seção *Host e contêineres*, é possível ver a *tabela Explorar*,
uma lista de trabalhadores em seu cluster que estão encaminhando métricas para a instância de monitoramento. Cada entrada do trabalhador representa um grupo de objetos de infraestrutura relacionados para esse trabalhador.

Clique em **Host e contêineres** ![Host e contêineres](../images/switch_hosts.png) para alternar origens de dados. Em seguida, selecione um trabalhador. Os dados que são exibidos correspondem ao trabalhador que você selecionou. Se você clicar em **Voltar para a tabela de exploração**, a *Tabela de exploração* será exibida. 

**Customizando a _tabela Explorar_**

É possível customizar a *tabela Explorar*. 

* Cada coluna mostra uma métrica diferente. 
* É possível configurar cada métrica individualmente. 
* É possível mudar a ordem das colunas. 

    Observe que ao fazer mudanças na ordem das colunas existentes, a mudança é persistente entre os diferentes agrupamentos enquanto você está com login efetuado. Se você incluir ou remover uma coluna, a
mudança será persistente. 

* Também é possível configurar cores para destacar valores e melhorar a capacidade de leitura. 

Por exemplo, para configurar a codificação de cores para uma coluna, conclua as etapas a seguir:

1. Selecione uma coluna. Passe o mouse sobre o título da coluna. Em seguida, selecione o ícone de lápis.
2. Alternar a barra para ativar a codificação de cores.
3. Configure valores para os diferentes limites.


**Customizando painéis**

Para visualizar mais detalhes sobre um nó do trabalhador específico, clique na entrada de infraestrutura
e o painel *Visão geral por host* será aberto na tabela. É possível explorar diferentes painéis
e métricas, clicando no ícone ![alternar painel](../images/switch_dashboards_1.png). Observe que é possível selecionar somente métricas e painéis que são relevantes para o
nó do trabalhador selecionado.

Para retornar para a _tabela Explorar_completa, clique no botão **X (Voltar para a tabela Explorar)**.


Para obter mais informações, verifique os [docs do Sysdig](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/222822446/The+Explore+Table).



## Próximos passos
{: #kubernetes_cluster_next_steps}

Crie um painel customizado. Para obter mais informações, consulte [Trabalhando com painéis](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards).

Também é possível saber mais sobre alertas. Para obter mais informações, consulte [Trabalhando com alertas](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-monitoring#monitoring_alerts). 






