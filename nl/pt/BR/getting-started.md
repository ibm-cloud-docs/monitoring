---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, getting started

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


# Tutorial de Introdução
{: #getting-started}

O {{site.data.keyword.mon_full_notm}} é um sistema de gerenciamento de terceiros de inteligência de contêiner e de nuvem nativa que pode ser incluído como parte de sua arquitetura {{site.data.keyword.cloud_notm}}. Use-o para obter visibilidade operacional para o desempenho e o funcionamento de seus aplicativos, serviços e plataformas. Ele oferece aos administradores, equipes do DevOps e desenvolvedores a telemetria de pilha integral com recursos avançados para monitorar e solucionar problemas, definir alertas e projetar painéis customizados. O {{site.data.keyword.mon_full_notm}} é operado pelo Sysdig em parceria com a {{site.data.keyword.IBM_notm}}.
{:shortdesc}

A figura a seguir mostra a visão geral dos componentes para o serviço {{site.data.keyword.mon_full_notm}} que está em execução no {{site.data.keyword.cloud_notm}}:

![Visão geral do componente do {{site.data.keyword.mon_full_notm}} no {{site.data.keyword.cloud_notm}}](images/components.png "Visão geral do componente do {{site.data.keyword.mon_full_notm}} no {{site.data.keyword.cloud_notm}}")


## Características
{: #features}

**Acelere o diagnóstico e a resolução de incidentes de desempenho.**

O {{site.data.keyword.mon_full_notm}} oferece visibilidade profunda em sua infraestrutura e aplicativos com a capacidade de solucionar problemas do nível de serviço até o nível do sistema. Os painéis e alertas predefinidos simplificam a identificação de ameaças ou problemas potenciais. Usando o {{site.data.keyword.mon_full_notm}}, os desenvolvedores e as equipes do DevOps monitoram e solucionam problemas de desempenho em tempo real, identificam a origem de erros e eliminam problemas. 

**Controle o custo de sua infraestrutura de monitoramento.**

O {{site.data.keyword.mon_full_notm}} inclui a funcionalidade que ajuda a controlar o custo de sua infraestrutura de monitoramento no {{site.data.keyword.cloud_notm}}. É possível configurar as origens de métricas para as quais você deseja monitorar seu desempenho. É possível ativar um alerta predefinido para avisar sobre as mudanças de uso que afetam seu faturamento. 

**Explore e visualize facilmente seu ambiente inteiro.**

O {{site.data.keyword.mon_full_notm}} facilita explorar visualmente o seu ambiente. Os mapas de topologia dinâmica fornecem uma visualização de dependências entre os serviços. As consultas multidimensionais em métricas de alta rotatividade, alta cardinalidade e alta frequência aceleram a resolução de problemas. Os painéis customizáveis permitem visualizar o que mais importa. 

**Obtenha insights críticos do Kubernetes e de contêiner para monitoramento de microsserviço dinâmico.**

O {{site.data.keyword.mon_full_notm}} descobre automaticamente ambientes do Kubernetes que fornecem painéis prontos para uso e alertas para clusters, nós, namespaces, serviços, implementações, pods e mais. Um único agente por nó descobre dinamicamente todos os microsserviços e coleta automaticamente as métricas e os eventos de várias origens, incluindo Kubernetes, hosts, redes, contêineres, processos, aplicativos e métricas customizadas como Prometheus, JMX e StatsD. 

**Minimize o impacto de situações anormais com notificações proativas.**

O {{site.data.keyword.mon_full_notm}} inclui alertas e notificações de diversos canais que podem ser usados para reduzir o impacto em suas operações do dia a dia e acelerar sua reação e o tempo de resposta a anomalias, tempo de inatividade e degradação de desempenho. Os canais de notificação que podem ser configurados facilmente incluem *e-mail*, *slack*, *PagerDuty*, *Webhooks*, *OpsGenie* e *VictorOps*.


## Antes de iniciar
{: #prereqs}

Deve-se ter um ID do usuário que seja um membro ou um proprietário de uma conta do {{site.data.keyword.cloud_notm}}. Para obter um ID do usuário do {{site.data.keyword.cloud_notm}}, acesse: [Registro ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/login){:new_window}.

O serviço está atualmente disponível no sul dos EUA. Conclua quaisquer etapas de introdução na região sul dos EUA.


## Etapa 1: Gerenciar o acesso de usuário
{: #step1}

A todo usuário que acessa o serviço {{site.data.keyword.mon_full_notm}} em sua conta deve ser designada uma política de acesso com uma função de usuário do IAM definida. A política determina quais ações o usuário pode executar no contexto do serviço ou da instância selecionada. As ações permitidas são customizadas e definidas como operações que têm permissão para serem executadas no serviço. As ações são então mapeadas para as funções de usuário do IAM. Para obter mais informações, consulte [Gerenciando o acesso de usuário no {{site.data.keyword.cloud_notm}}](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-iam#iam).

Quando um usuário tem permissões concedidas no {{site.data.keyword.cloud_notm}} para trabalhar com o serviço {{site.data.keyword.mon_full_notm}}, o usuário tem uma função do Sysdig concedida automaticamente. Essa função determina as ações que um usuário tem permissões para executar. As funções válidas são *Administrador do Sysdig* e *Usuário do Sysdig*. Para obter mais informações, consulte [Mapeamento de funções do Sysdig para funções do {{site.data.keyword.cloud_notm}}](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-iam#iam_sysdig).

Antes de poder provisionar uma instância, considere as informações a seguir:
* O proprietário da conta pode criar, visualizar e excluir uma instância de um serviço no {{site.data.keyword.cloud_notm}} e pode conceder permissões a outros usuários para trabalhar com o serviço {{site.data.keyword.mon_full_notm}}.
* Deve-se ter permissões para criar recursos no grupo de recursos *Padrão*.
* Outros usuários do {{site.data.keyword.cloud_notm}} com as permissões `administrator` ou `editor` podem gerenciar o serviço {{site.data.keyword.mon_full_notm}} no {{site.data.keyword.cloud_notm}}. Esses usuários também devem ter permissões de plataforma para criar recursos no contexto do grupo de recursos no qual planejam provisionar a instância.

Para conceder a um usuário a função de administrador para o serviço e para gerenciar instâncias dentro de um grupo de recursos na conta, o usuário deve ter uma política do IAM para o serviço {{site.data.keyword.mon_full_notm}} com a função da plataforma **Administrador** dentro do contexto do grupo de recursos. 

Conclua as etapas a seguir para designar uma função de administrador de usuário para o serviço {{site.data.keyword.mon_full_notm}} no contexto de um grupo de recursos: 

1. Na barra de menus, clique em **Gerenciar** &gt; **Acesso (IAM)** e, em seguida, selecione **Usuários**.
2. Na linha para o usuário que você deseja designar acesso, selecione o menu **Ações** e, em seguida, clique em **Designar acesso**.
3. Selecione **Designar acesso em um grupo de recursos**.
4. Selecione um grupo de recursos.
5. Se o usuário não tiver uma função já concedida para o grupo de recursos selecionado, escolha uma função para o campo **Designar acesso a um grupo de recursos**. 

    Dependendo da função selecionada, o usuário pode visualizar o grupo de recursos em seu painel, editar o nome do grupo de recursos ou gerenciar o acesso de usuário ao grupo. 
    
    Será possível selecionar **Sem acesso** se você desejar que o usuário tenha acesso somente ao serviço {{site.data.keyword.mon_full_notm}} no grupo de recursos.

6. Selecione **{{site.data.keyword.mon_full_notm}}**.
7. Selecione a função da plataforma **Administrador**.
8. Clique em **Designar**.

## Etapa 2: provisionar uma instância do serviço {{site.data.keyword.mon_full_notm}}
{: #step2}

Para incluir recursos de monitoramento com o {{site.data.keyword.mon_full_notm}} no {{site.data.keyword.cloud_notm}}, deve-se provisionar uma instância do serviço {{site.data.keyword.mon_full_notm}}. 

Quando você provisiona uma instância, seus dados são enviados a um terceiro.
{: tip}

Você provisiona uma instância no contexto de um grupo de recursos. Um grupo de recursos permite organizar seus serviços para propósitos de controle de acesso e faturamento. É possível provisionar a instância do {{site.data.keyword.mon_full_notm}} no grupo de recursos *padrão* ou em um grupo de recursos customizados.

Ao provisionar uma instância, você obtém automaticamente uma chave de ingestão, conhecida como *Chave de acesso do Sysdig*.

Para provisionar uma instância por meio da IU do {{site.data.keyword.cloud_notm}}, conclua as etapas a seguir:

1. Efetue login em sua conta do  {{site.data.keyword.cloud_notm}} .

    Clique em [Painel do {{site.data.keyword.cloud_notm}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/login){:new_window} para ativar o painel do {{site.data.keyword.cloud_notm}}.

	Depois de efetuar login com seu ID de usuário e senha, a IU do {{site.data.keyword.cloud_notm}} é aberta.

2. Clique em  ** Catálogo **. A lista dos serviços disponíveis no {{site.data.keyword.cloud_notm}} é aberta.

3. Para filtrar a lista de serviços exibida, selecione a categoria **Ferramentas do desenvolvedor**.

4. Clique no quadro  ** {{site.data.keyword.mon_full_notm}} ** .

5. Selecione um plano de serviço. Por padrão, o plano de **Experiência** é configurado.

    Para obter mais informações sobre os planos de serviço, consulte [Precificação](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-pricing_plans#pricing_plans).

6. Selecione um grupo de recursos. Por padrão, o **padrão** é configurado.

7. Clique em  ** Criar **  para provisionar uma instância.

A IU de serviço é aberta.

**Nota:** para provisionar uma instância do Sysdig por meio da CLI, consulte [Provisionando o Sysdig por meio da CLI do {{site.data.keyword.cloud_notm}}](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-provision#provision_cli).


## Etapa 3: configurar um agente Sysdig
{: #step3}

Depois de provisionar uma instância, deve-se configurar um agente Sysdig para cada origem de métrica que você deseja monitorar. Uma origem de métrica é um recurso de nuvem do qual você deseja monitorar e controlar seu desempenho e funcionamento. Por exemplo, uma origem de métrica pode ser um cluster Kubernetes.  

O agente Sysdig coleta e relata automaticamente as métricas predefinidas. Você usa a *Chave de acesso do Sysdig* para configurar o agente Sysdig que é responsável por coletar e encaminhar dados de métrica para sua instância. Para obter mais informações, consulte [Trabalhando com chaves de acesso](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key).

É possível configurar um agente Sysdig para qualquer um dos ambientes a seguir:

* Kubernetes, GKE, e OpenShift.
* Contêineres de Docker ou para serviços não conteinerizados.
* Mesos, Marathon, e DCOS.
* Instalações do Linux.

Por exemplo, para configurar seu cluster Kubernetes para enviar métricas para sua instância do Sysdig, deve-se instalar um pod `sysdig-agent` em cada nó de seu cluster. O agente Sysdig coleta dados do pod no qual ele está instalado e os encaminha para sua instância do Sysdig.

Conclua um dos tutoriais a seguir para saber como implementar um agente Sysdig:

| Recurso                |	Tutorial                        | Environment                | Cenário   |
|-------------------------|---------------------------------|----------------------------|------------|
| Contêineres em execução no {{site.data.keyword.containershort}} |[Analisar métricas para um app que é implementado em um cluster Kubernetes](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-kubernetes_cluster#kubernetes_cluster) | {{site.data.keyword.cloud_notm}} Public | ![{{site.data.keyword.containershort}} e {{site.data.keyword.mon_full_notm}}](images/kube.png "{{site.data.keyword.containershort}} e {{site.data.keyword.mon_full_notm}}") |
|Linux Ubuntu / Debian | [Analisar métricas para um servidor Ubuntu](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-ubuntu#ubuntu) | No local | ![Ubuntu e {{site.data.keyword.mon_full_notm}}](images/kube.png "Ubuntu e {{site.data.keyword.mon_full_notm}}") |
{: caption="Tabela 1. Tutoriais para começar a trabalhar com o {{site.data.keyword.mon_full_notm}}" caption-side="top"} 

Para obter mais informações, consulte [Configurando um agente Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-config_agent#config_agent) e [Removendo um agente Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-remove#remove).

Depois que o agente Sysdig é implementado, a coleta e o encaminhamento de métricas para a instância são automáticos. O agente Sysdig coleta e relata automaticamente as métricas predefinidas. Também é possível configurar quais métricas devem ser monitoradas em um ambiente. Os dados para as métricas customizadas também são coletados automaticamente.

## Etapa 4: Ativar a IU da web
{: #step4}

Depois de provisionar uma instância do serviço {{site.data.keyword.mon_full_notm}} no {{site.data.keyword.Bluemix}} e configurar um agente Sysdig para seu nó, é possível visualizar, monitorar e gerenciar dados por meio da IU da web do serviço.

Você ativa a IU da web dentro do contexto da instância do Sysdig por meio da IU do {{site.data.keyword.cloud_notm}}. 

Conclua as etapas a seguir para ativar a IU da web do Sysdig:

1. Efetue login em sua conta do  {{site.data.keyword.cloud_notm}} .

    Clique em [Painel do {{site.data.keyword.cloud_notm}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/login){:new_window} para ativar o painel do {{site.data.keyword.cloud_notm}}.

	Depois que você efetua login com seu ID do usuário e senha, o Painel do {{site.data.keyword.cloud_notm}} é aberto.

2. No menu de navegação, selecione **Observabilidade**. 

3. Selecione **Monitorando**. 

    A lista de instâncias de monitoramento que estão disponíveis no {{site.data.keyword.cloud_notm}} é exibida.

4. Selecione uma instância. Em seguida, clique em **Visualizar Sysdig**.

A IU da Web do  {{site.data.keyword.mon_full_notm}}  é aberta. Por padrão, a guia *Explorar* é exibida.

Por padrão, os usuários são incluídos automaticamente como membros da equipe **Operações de monitor** que é predefinida para cada instância do {{site.data.keyword.mon_full_notm}}. Os usuários têm permissões completas para ver todos os dados na IU da web. **Nota:** um administrador pode restringir o acesso a dados gerenciando usuários em equipes e controlando quais dados estão visíveis. Por exemplo, para restringir os usuários a permissões de visualização, um administrador pode criar uma equipe padrão com escopo e visibilidade limitados. Em seguida, designe manualmente os usuários a outras equipes. Para obter mais informações, consulte [Trabalhando com equipes](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-teams#teams).


## Etapa 5: Monitorar seu ambiente
{: #step5}

É possível analisar dados na guia *Explorar* e na guia *Painel* da IU da web. Você monitora os dados por meio de visualizações e painéis de métrica. 

* Use uma visualização de métrica para monitorar uma métrica individual.
* Use painéis para obter um insight especializado em dados de rede, dados do aplicativo, topologia, serviços, hosts e contêineres, monitorando dados por meio de painéis. Um painel exibe uma métrica ou um grupo de métricas em um painel.
{: tip}

Na guia *Explorar*, é possível monitorar dados usando métricas padrão e painéis padrão. É possível usar rótulos para definir novos grupos de infraestrutura que podem, então, ser usados para agregar dados de forma diferente e monitorar seu ambiente. Também é possível usar painéis customizados que você define por meio da guia *Painel*.

Na guia *Painéis*, é possível monitorar dados usando qualquer um dos painéis padrão ou criando novos painéis.

Para obter mais informações, consulte [Monitorando o seu ambiente](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-monitoring#monitoring)



## Etapa 6: Gerenciar dados
{: #step6}

É possível usar rótulos para agrupar os recursos de infraestrutura em hierarquias lógicas, filtrar dados e dividir dados agregados em segmentos. Customize como os dados serão agregados quando você configurar um gráfico ou criar um alerta para uma métrica. Configure o escopo de um painel ou de um alerta para filtrar pontos de dados. Restrinja o acesso aos dados gerenciando o acesso a dados dos usuários por meio de equipes. 

Por exemplo, para uma visualização de métrica, é possível definir o escopo dos dados, como agregar dados e quais filtros de horário e de grupo se aplicam aos dados. 

Para obter mais informações, consulte [Gerenciando dados](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-manage#manage).


## Próximas etapas: configurar alertas e explorar eventos
{: #next}

É possível usar eventos para revisar, rastrear e resolver problemas. Um evento é uma notificação que informa sobre algo que ocorreu em qualquer um dos nós que encaminha dados para sua instância do {{site.data.keyword.mon_full_notm}}. 

Há diferentes tipos de eventos: 

* *Eventos de alerta* são aqueles acionados por alertas configurados pelo usuário. Por exemplo, configure alertas para ser notificado sobre problemas que requerem atenção. Para obter mais informações, consulte [Trabalhando com alertas](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-monitoring#monitoring_alerts).
* *Eventos baseados em infraestrutura* são aqueles coletados dos nós do Docker e do Kubernetes. Por padrão, o agente Sysdig descobre e coleta automaticamente dados de um grupo de eventos selecionado. É possível editar o arquivo de configuração do agente para permitir mais eventos.
* *Eventos customizados* configurados por meio de qualquer uma das integrações a seguir: Slackbot, scripts Python pré-construídos, scripts Python customizados criados pelo usuário ou solicitações de cURL.

Ao definir um alerta, deve-se definir a condição que aciona a notificação, um ou mais canais de notificação pelos quais você deseja ser notificado, a severidade do alerta e o tipo de alerta. 

Você configura um ou mais canais de notificação na seção *Configurações* na IU da web. Os canais de notificação válidos são: *e-mail*, *slack*, *PagerDuty*, *Webhooks*, *OpsGenie* e *VictorOps*. Para obter mais informações, consulte [Trabalhando com canais de notificação](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-notifications#notifications).

A seção *Alertas* na IU da web mostra a lista de alertas predefinidos. Nessa visualização, é possível ativar e desativar alertas predefinidos, modificar alertas existentes e criar novos alertas. Para obter mais informações, consulte [Trabalhando com alertas ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/205324292/Alerts){:new_window}.

Em seguida, explore [Trabalhando com eventos customizados ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://sysdigdocs.atlassian.net/wiki/spaces/Monitor/pages/222822463/Custom+Events){:new_window}.


