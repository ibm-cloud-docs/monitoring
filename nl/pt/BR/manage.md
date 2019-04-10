---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, manage

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

# Gerenciando dados
{: #manage}

Use rótulos para agrupar os recursos de infraestrutura em hierarquias lógicas, filtrar dados e dividir dados agregados em segmentos. Customize como os dados serão agregados quando você configurar um gráfico ou criar um alerta para uma métrica. Configure o escopo de um painel ou de um alerta para filtrar pontos de dados. Restrinja o acesso aos dados gerenciando o acesso a dados dos usuários por meio de equipes. 
{:shortdesc}



## Rótulos
{: #manage_labels}

Os **Rótulos** definem as características de uma métrica. É possível usar rótulos para identificar e diferenciar características de uma métrica. 

Os rótulos são classificados como rótulos de infraestrutura e rótulos do descritor de métrica. Cada métrica tem um conjunto de rótulos predefinidos. Para métricas customizadas, é possível configurar mais rótulos. 

* É possível usar **rótulos de infraestrutura** para identificar objetos dentro da infraestrutura. Esses rótulos são obtidos por meio da infraestrutura. Por exemplo, um rótulo pode ser *kubernetes.pod.name*.
* É possível usar **rótulos do descritor de métrica** para definir rótulos customizados. Esses rótulos são pares chave-valor que são aplicados diretamente às métricas e obtidos de integrações como StatsD, Prometheus e JMX. 

## Grupos
{: #manage_groups}

Os **Grupos** organizam objetos de infraestrutura em hierarquias lógicas. Use grupos para estruturar sua infraestrutura e facilitar como você monitora seu ambiente.

Na visualização *Explorar* da IU da web, é possível executar qualquer uma das ações a seguir:

| Tarefa                                                                                        | Descrição     |
|---------------------------------------------------------------------------------------------|-----------------|
| [Copiar um grupo](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-groups#copy_group)                | Copiar um grupo para outras equipes. |
| [Criar um grupo ](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-groups#create_group)            | Crie um novo grupo. |
| [Excluir um grupo](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-groups#delete_group)            | Excluir um grupo. |
| [Renomear um grupo](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-groups#rename_group)            | Renomear um grupo. |
| [Compartilhar um grupo](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-groups#share_group)              | Compartilhe um grupo com outros membros na equipe. |
{: caption="Tabela 1. Rótulos de agrupamento de tarefas" caption-side="top"} 



## Agregação
{: #manage_aggregation}

A **Agregação** de dados ocorre automaticamente quando você configura um gráfico ou cria um alerta para uma métrica. Há dois tipos de agregação: agregação de tempo e agregação de grupo. 
* A agregação de tempo é sempre executada antes da agregação de grupo.
* Para criar comparações de várias séries e múltiplos alertas, também é possível dividir os dados agregados em seções menores chamadas **segmentos** usando rótulos. 

A Sysdig agrega dados ao longo do tempo. Em seguida, usa esses pontos de dados e os agrupa para exibir os dados em métricas, painéis ou limites de cálculo de alerta. 
{: tip}

É possível customizar como os dados são agregados quando você configura um gráfico ou cria um alerta para uma métrica.

Há duas formas de agregação usadas para métricas: 
* Agregação de tempo
* Agregação de grupo

**A agregação de tempo é sempre executada antes da agregação de grupo.**


### Agregação de tempo
{: #manage_time_aggregation}

**Por padrão, um agente Sysdig coleta e relata métricas em uma resolução de 10 segundos.**

Em gráficos de séries temporais que incluem dados por cinco minutos ou menos, 
* Os pontos de dados são desenhados em resolução d 10 segundos
* A agregação de tempo não ocorre.

A agregação de tempo ocorre automaticamente em qualquer das situações a seguir:

* Em gráficos de séries temporais que incluem dados para uma quantia de tempo maior que cinco minutos, os pontos de dados são desenhados como um agregado para um intervalo de tempo apropriado. Por exemplo, para um gráfico que mostra dados por uma hora, cada ponto de dados representa um intervalo de um minuto.
* Quando você exibe dados históricos. Os dados são recuperados ao longo do tempo. É possível escolher quais pontos de dados utilizar ao visualizar dados mais antigos.

A tabela a seguir lista os diferentes tipos de agregação para gráficos de séries temporais:

| Tipo de Agregação | Descrição                                                              |
|------------------|--------------------------------------------------------------------------|
| average          | Média dos valores de métrica recuperados no período avaliado. |
| taxa (timeAvg)   | Valor médio da métrica no período avaliado.            |
| máximo	         | O valor mais alto durante o período avaliado.                          |
| mínimo	         | O valor mais baixo durante o período avaliado.                           |
| soma              | A soma combinada da métrica no período avaliado.             |
{: caption="Tabela 2. Tipos de agregação para gráficos de séries temporais" caption-side="top"} 

**Nota:** por padrão, a média é usada para exibir pontos de dados para um intervalo de tempo.

A taxa e a média são tipos de agregação muito semelhantes. Elas geralmente fornecem o mesmo resultado. No entanto, o cálculo de cada uma é diferente. Se a agregação de tempo for configurada para um minuto, o agente Sysdig será configurado para recuperar seis amostras, uma a cada 10 segundos. Observe que, em alguns casos, as amostras podem não estar lá devido a desconexões ou outras circunstâncias.


### Agregação de grupo
{: #manage_group_aggregation}

**Por padrão, as métricas que são aplicadas a um grupo de recursos, como vários contêineres, hosts ou nós, são medidas entre os membros do grupo.**

Por exemplo, se três hosts relatarem uso de CPU diferente para um intervalo de amostra, os três valores terão a média calculada e relatados no gráfico como um único ponto de dados para essa métrica.

A tabela a seguir lista os diferentes tipos de agregação de grupo:

| Tipo de Agregação | Descrição                                        |
|------------------|----------------------------------------------------|
| average          | Valor médio das amostras do intervalo.           |
| máximo	         | Valor mais alto das amostras do intervalo.           |
| mínimo	         | Valor mais baixo das amostras do intervalo.            |
| sum              | Valor combinado das amostras do intervalo.          |
{: caption="Tabela 3. Tipos de agregação para agregação de grupo" caption-side="top"} 


**A agregação de grupo é dependente da segmentação.** Para uma visualização que mostra as métricas para um grupo de itens, se a seleção *Segmentar por* for mudada para dividir os itens individuais, a agregação de grupo não ocorrerá.



## Escopo
{: #manage_scope}

O **Escopo** é uma coleção de rótulos que definem as condições para filtrar pontos de dados quando você cria painéis, configura alertas e customiza equipes. 

A tabela a seguir lista as tarefas que podem ser executadas para mudar o escopo no serviço de monitoramento:

| Tarefa                                                                                        | Descrição     |
|---------------------------------------------------------------------------------------------|-----------------|
| [Mudando o escopo de um painel](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards_scope) | Mude o escopo de um painel para filtrar pontos de dados para todas as métricas exibidas por meio de painéis no painel. |
| [Mudando o escopo de um painel](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-panels#panels_scope) | Mude o escopo de um painel para filtrar dados para uma métrica específica que é exibida por meio do painel. |
| [Mudando o escopo de uma equipe](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-teams#teams_scope) | Mude o escopo dos dados que são visíveis para usuários membros de uma equipe. |
{: caption="Tabela 4. Tarefas para mudar o escopo" caption-side="top"} 


## Equipes
{: #manage_teams}

As **Equipes** agrupam usuários e controlam os dados e as permissões para trabalhar com capturas do Sysdig e eventos de infraestrutura para esses usuários. 

Um administrador do Sysdig pode definir qualquer número de equipes. Para cada equipe, ele pode configurar as informações a seguir:
* A *equipe padrão*: é possível configurar essa equipe para ser a equipe que qualquer usuário que efetua login na IU da web pela primeira vez é designada por padrão.
* O *ponto de entrada padrão*: é possível especificar a visualização na IU da web que se abre toda vez que um usuário efetua login. Os pontos de entrada válidos são: visualização *Explorar*, visualização *Painéis*, visualização *Eventos*, visualização *Alertas* e visualização *Configurações*.
* O escopo: é possível limitar quais dados os usuários podem ver. É possível escolher *Host* ou *Contêiner* para definir o nível de dados que estão visíveis. Em seguida, é possível incluir uma ou mais condições. Se o escopo for configurado como *Host*, os usuários poderão ver todas as informações no nível do host e no nível do contêiner. Se o escopo for configurado como *Contêiner*, os usuários poderão ver somente informações de nível do contêiner.
* Permissões: é possível ativar ou desativar os recursos a seguir: *capturas do Sysdig* e *eventos de infraestrutura*. Os arquivos de captura serão visíveis somente para membros da equipe. **Nota:** as capturas incluem informações detalhadas de cada contêiner em um host, independentemente do escopo da equipe. Quando os eventos de infraestrutura estão ativados, os usuários podem visualizar todos os eventos customizados de infraestrutura de cada usuário e agente Sysdig na instância.

Por padrão, há uma equipe **Operações de monitor** que está predefinida para cada instância do {{site.data.keyword.mon_full_notm}}.
* Essa equipe não pode ser excluída.
* Os usuários são incluídos automaticamente como membros dessa equipe e a visibilidade integral é concedida a eles em todos os recursos que estão disponíveis na instância. 

** Nota: ** 
* Um administrador deve alternar para a equipe *Operações de monitor* antes de poder criar equipes ou mudar as configurações para outras equipes.
* Depois que um usuário efetua login no {{site.data.keyword.cloud_notm}} e ativa a IU da web do Sysdig, um administrador pode gerenciar esse usuário na IU da web do Sysdig. O usuário é criado no banco de dados do Sysdig quando o usuário efetua login na IU da web do Sysdig pela primeira vez. 

Para restringir os usuários a permissões de visualização, um administrador pode executar qualquer uma das ações a seguir:
* Mude a função do usuário na equipe *Operações de monitor* padrão para o Usuário de *Leitura*. 
* Crie uma equipe padrão com escopo e visibilidade limitados. Em seguida, designe manualmente os usuários a outras equipes. 

A tabela a seguir lista as tarefas que podem ser executadas quando você trabalha com equipes:

| Tarefa                                                                            | Descrição                 |
|---------------------------------------------------------------------------------|-----------------------------|
| [Criando uma equipe](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-teams#teams_create)      | Crie uma equipe para controlar a visibilidade de dados.  |
| [Excluindo uma equipe](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-teams#teams_delete)      | Exclua uma equipe. </br>**Nota:** quando você excluir uma equipe, os usuários que pertencerem apenas a essa equipe serão movidos para a equipe padrão. |
| [Incluindo membros da equipe](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-teams#teams_users)   | Incluir mais usuários em uma equipe. |
| [Editar uma equipe](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-teams#teams_scope)          | Mude o escopo dos dados que são visíveis para usuários membros de uma equipe.  |
{: caption="Tabela 5. Tarefas para trabalhar com equipes" caption-side="top"} 





    


