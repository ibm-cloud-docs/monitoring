---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, dashboards

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


# Trabalhando com Painéis
{: #dashboards}

Use painéis para monitorar sua infraestrutura, seus aplicativos e serviços. É possível usar painéis predefinidos. Também é possível criar painéis customizados por meio da IU da web ou programaticamente. É possível fazer backup e restaurar painéis usando scripts Python.
{:shortdesc}

Um **painel** mostra os grupos de métricas que relatam o funcionamento, o desempenho e o estado de sua infraestrutura, aplicativos e serviços para um único host ou um grupo de hosts. Os painéis oferecem um insight especializado em dados da rede, dados do aplicativo, topologia, serviços, hosts e contêineres.

Na seção **PAINÉIS** da IU da web, os painéis são organizados em três grupos principais:

* *Meus painéis*: são aqueles criados pelo usuário que está conectado atualmente.
* *Meus painéis compartilhados*: são aqueles criados pelo usuário que está conectado atualmente e que são compartilhados com outros usuários.
* *Painéis compartilhados comigo*: são aqueles criados por outros usuários e compartilhados com o usuário atual.

Na seção **EXPLORAR** da IU da web, os painéis são organizados em dois grupos:
* *Painéis padrão*: são os painéis predefinidos.
* *Meus painéis*: são aqueles criados pelo usuário que está conectado atualmente.

É possível copiar e compartilhar painéis por meio da IU da web. 

É possível executar scripts para concluir qualquer uma das ações a seguir programaticamente:
* Salvar os painéis existentes em um arquivo local.
* Crie novos painéis que são idênticos aos painéis salvos.
* Restaurar painéis.



## Painéis predefinidos
{: #dashboards_predefined}

Os painéis predefinidos são projetados em torno de vários aplicativos, topologias de rede, layouts de infraestrutura e serviços suportados. 

Os painéis predefinidos incluem uma série de painéis que já estão configurados.

A tabela a seguir lista os diferentes tipos de painéis predefinidos:

| Tipo | Descrição | Mais informações | 
|------|-------------|------------------|
| Aplicativos | Painéis que podem ser usados para monitorar seus aplicativos e componentes de infraestrutura.  | [Painéis do aplicativo](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-default_dashboards#default_dashboards_applications) |
| Host e contêineres | Painéis que podem ser usados para monitorar a utilização de recurso e a atividade do sistema em seus hosts e em seus contêineres. | [Painéis de host e de contêiner](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-default_dashboards#default_dashboards_host_container) |
| Rede | Painéis que podem ser usados para monitorar suas conexões de rede e atividade. | [Painéis de rede](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-default_dashboards#default_dashboards_network) |
| Serviço | Painéis que podem ser usados para monitorar o desempenho de seus serviços, mesmo que esses serviços sejam implementados em contêineres orquestrados. | [Painéis de serviço](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-default_dashboards#default_dashboards_service) |
| Topologia | Painéis que podem ser usados para monitorar as dependências lógicas de suas camadas do aplicativo e métricas de sobreposição. | [Painéis de topologia](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-default_dashboards#default_dashboards_topology) |
{: caption="Tabela 1. Lista de Painéis Predefinidos" caption-side="top"} 



## Criando painéis customizados na IU da web
{: #dashboards_create}

Ao criar um painel customizado, é possível iniciar por meio de um modelo como um painel predefinido ou escolher um painel em branco. Um painel inclui painéis que são configurados para exibir dados específicos em vários formatos diferentes. Você também configura como os dados são agregados. O **escopo** define quais dados são usados para agregação e exibidos. É possível configurar o escopo em um nível de painel ou substituir por painéis individuais. 

Conclua as etapas a seguir para criar um painel customizado:

1. Navegue para a seção *PAINEL** na IU da web e selecione **Incluir painel**. A página *Criar um novo painel* é aberta.

    1. Selecione um painel predefinido ou escolha o *Painel em branco*. 

    2. Insira um nome para seu painel.

    3. Clique em  ** Criar painel **.

2. Configure o escopo do painel. Clique em **Editar escopo** para mudar o escopo padrão. Por padrão, **Em toda parte** é selecionado.
    
    1. Selecione o escopo. 

    2. Opcionalmente, clique em **Substituir os escopos do painel customizado** para substituir o escopo de todos os painéis que têm atualmente um escopo customizado definido. **Nota: não é possível desfazer essa ação.** 

    **Nota:** para reconfigurar o escopo do painel para a infraestrutura inteira ou para atualizar o escopo de um painel existente para a infraestrutura inteira, selecione **Em todo lugar**.

    3. Clique em **Salvar**.

3. Configure os painéis. Repita essa etapa para qualquer um dos painéis no painel que você deseja modificar.

    1. Identifique o painel que você deseja modificar.

    2. Selecione  ** Editar Painel **. Este é o ícone de lápis.
    
    3. Mude o tipo de gráfico.

    4. Mude a métrica e a taxa. A taxa define o tipo de agregação que é feito com os dados.

    5. Mude o escopo do painel. Clique em  ** Substituir o Escopo do Painel **. Em seguida, mude o escopo. Se for necessário restaurar o escopo do painel para o painel, selecione **Padrão para o escopo do painel**.

    6. No campo *Comparar a*, clique em **Configurar**. Configure o intervalo de tempo para a comparação.

    7. Configure a cor do plano de fundo do painel com base em limites de métrica. Clique em  ** Substituir Codificação de Cor **, em seguida,  ** Ativar **. Configure valores para os diferentes limites.

    8. Clique em **Salvar**.


## Alterando o escopo
{: #dashboards_scope}

Em vez de mudar o escopo de um painel predefinido, copie o painel e mude o escopo no painel copiado.
{: tip}

Conclua as etapas a seguir para mudar o escopo de um painel:

1. Navegue para a seção **PAINEL** na IU da web e selecione um painel.

2. Clique em **Editar escopo** para mudar o escopo padrão. 

    Por padrão, **Em toda parte** é selecionado.
    
3. Selecione o escopo. 

4. Opcionalmente, clique em **Substituir os escopos do painel customizado** para substituir o escopo de todos os painéis que têm atualmente um escopo customizado definido. 

    **Nota: não é possível desfazer essa ação.** 

    Para reconfigurar o escopo do painel para a infraestrutura inteira ou para atualizar o escopo de um painel existente para a infraestrutura inteira, selecione **Em toda parte**.
    {: tip}

5. Clique em **Salvar**.



## Copiando um painel
{: #dashboards_copy}

Ao copiar um painel, você cria uma duplicata.

A tabela a seguir descreve as diferentes ações e permissões de usuário que são necessárias para que os usuários copiem um painel:

| Ação     |	Quem pode copiar     |	Instância do painel	   | Quem pode visualizar o painel     | Quem pode editar o painel  |
|------------|-------------------|-------------------------|--------------------------------|-----------------------------|
| Copiar para a equipe atual    |	Usuários na equipe com permissões do editor | Nova instância do painel  | Membros da equipe com permissões de visualização	 | Usuários na equipe com permissões do editor |
| Copiar para outra Equipe    | Usuários na equipe com permissões do editor em ambas as equipes | Nova instância do painel  | Se o painel original não for compartilhado, somente o usuário que copiar o painel terá acesso. </br>Se o painel original for compartilhado, todos os membros da equipe terão acesso. | Se o painel original não for compartilhado, somente o usuário que copiar o painel. </br>Se o painel original for compartilhado, todos os membros da equipe da equipe com permissões de editor. |
{: caption="Tabela 2. Informações sobre usuários e painéis relacionadas à cópia de painéis" caption-side="top"} 

Conclua as etapas a seguir para copiar um painel na IU da web:

1. Navegue para a seção *PAINÉIS* na IU da web.
2. Selecione o painel no painel do lado esquerdo.
3. Clique em **Configurações** (ícone de três pontos) e selecione **Copiar painel**. 
4. Selecione onde copiar o painel.

    1. Escolha **Equipe atual** para copiar o painel para a equipe atual.
    
    2. Escolha **Outras equipes** para copiar o painel para outras equipes. Selecione as equipes nas quais você deseja copiar o painel.

    3. Insira um nome para o painel.

    4. Clique em **Enviar cópia**.
    
    5. Verifique se o escopo do painel na nova equipe está atualizado com base nas permissões da equipe de destino.

## Excluindo um painel
{: #dashboards_delete}

Conclua as etapas a seguir para excluir um painel na IU da web:

1. Navegue para a seção *PAINÉIS* na IU da web.
2. Selecione o painel no painel do lado esquerdo.
3. Clique em **Configurações** ![ícone de três pontos](images/actions.png) e selecione **Excluir painel**. 
4. Confirme a exclusão clicando em **Sim, excluir painel**.


## Compartilhando um painel
{: #dashboards_share}

É possível compartilhar painéis entre usuários em uma equipe e externamente configurando uma URL pública para o painel.  

A tabela a seguir descreve as diferentes ações e permissões de usuário que são necessárias para que os usuários compartilhem ou trabalhem com um painel compartilhado:

| Ação      |	Quem pode compartilhar        |	Instância do painel	       | Quem pode visualizar o painel        | Quem pode editar o painel  |
|-------------|-------------------|-----------------------------|------------------------------------|-----------------------------|
| Compartilhar com a Equipe atual |	Criador de painel         |	Compartilhe a mesma instância do painel   | Membros da equipe com permissões de visualização  | Membros da equipe com permissões de edição   |
| Compartilhar publicamente como URL	  | Qualquer usuário de edição da equipe |	Compartilhe a mesma instância do painel   | Qualquer um     | Ninguém                      |
{: caption="Tabela 3. Informações sobre usuários e painéis relacionadas ao compartilhamento de painéis" caption-side="top"} 


Conclua as etapas a seguir para compartilhar um painel na IU da web:

1. Navegue para a seção *PAINÉIS* na IU da web.
2. Selecione o painel no painel do lado esquerdo.
3. Clique em **Configurações** ![ícone de três pontos](images/actions.png) e selecione **Compartilhar**.
4. Escolha como você deseja compartilhar o painel:

    * Alterne a régua de controle **Compartilhar com a equipe** para compartilhar o painel com a equipe atual. A equipe na qual o painel é compartilhado é exibida.

    * Alterne a régua de controle **Compartilhar a URL pública** para revelar a URL pública customizada.

5. Clique em **Fechar**.

Compartilhe um painel externamente para permitir que os usuários externos visualizem as métricas de painel, enquanto restringe o acesso para alterar painéis e configurações.
{: tip}


## Gerenciando painéis programaticamente
{: #dashboards_programmatically}

Use a API de REST do Sysdig para automatizar tarefas de rotina e monitorar notificações. Também é possível usar a biblioteca Python do Sysdig. 

**Nota:** a biblioteca Python expõe a parte da funcionalidade da API de REST do Sysdig. 


Ao usar a API por meio de scripts ou programas customizados, deve-se usar um token do Sysdig para ser autenticado com a instância do {{site.data.keyword.mon_full_notm}}. Para obter mais informações, consulte [Trabalhando com tokens da API](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api_token#api_token).


| Tarefa                    | Usando a API de REST                |
|-------------------------|-------------------------------|
| Criar um painel      | [Criando um painel usando a API](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_create_dashboard) |
| Excluir um painel      | [Excluindo um painel usando a API](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_delete_dashboard) |
| Salvando painéis       | [Salvando os painéis de uma equipe usando a API](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-api#api_save_dashboard) |
{: caption="Tabela 4. Tarefas para gerenciar painéis programaticamente" caption-side="top"} 


