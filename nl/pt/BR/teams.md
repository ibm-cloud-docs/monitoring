---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, teams

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

# Trabalhando com equipes
{: #teams}

Um administrador ou um gerenciador de uma instância do {{site.data.keyword.mon_full_notm}} pode criar, excluir, incluir membros e mudar o escopo de equipes nessa instância. 
{:shortdesc} 

Um administrador ou um gerenciador de uma instância do {{site.data.keyword.mon_full_notm}} deve alternar para a equipe *Operações de monitor* antes de poder criar equipes e gerenciar equipes existentes.
{: tip}

## Criando uma Equipe
{: #teams_create}

Conclua as etapas a seguir para criar uma equipe:

1. Ative a IU da web. Para obter mais informações sobre como ativar a IU da web, consulte [Navegando para a IU da web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. No botão *Seletor* na barra de navegação, selecione **Monitorar operações**. Em seguida, escolha **Configurações**.

3. Selecione **Equipes**. A lista de equipes existentes é exibida.

4. Clique em  ** Incluir Equipe **. A página de configuração da equipe é exibida.

5. Configure os detalhes da equipe. 

    * Escolha uma cor.

    * Insira o nome da equipe

    * [Opcional] Insira uma descrição para essa equipe.

    * [Opcional] Configure o parâmetro **Default team** se desejar que essa equipe se torne a equipe padrão para novos usuários.

    * Configure o **Ponto de entrada padrão** para especificar a visualização na IU da web que se abre sempre que um usuário efetua login. Os pontos de entrada válidos são: visualização *Explorar*, visualização *Painéis*, visualização *Eventos*, visualização *Alertas* e visualização *Configurações*. Por padrão, a visualização *Explorar* está configurada.

6. Configure o escopo da equipe. 

    * [Opcional] Configure **Escopo por** para especificar o nível de dados aos quais os membros da equipe têm acesso. Os valores válidos são  * host *  e  * container *. Se o parâmetro for configurado como *Host*, os membros poderão ver todas as informações de nível do Host e de nível do Contêiner. Se o parâmetro for configurado como *Container*, os membros poderão ver somente informações de nível do Contêiner.

    * Configure o **Escopo** para limitar quais dados os usuários podem ver. É possível configurar uma ou mais condições especificando expressões para métricas. Por padrão, o escopo é configurado como *em todos os lugares*.
	
    * [ Opcional ] Ativar ou desativar  ** Capturas Sysdig **. Marque essa caixa para permitir que essa equipe obtenha Capturas do Sysdig. Os arquivos de captura serão visíveis somente para membros dessa equipe. **Nota:** as capturas incluem informações detalhadas de cada contêiner em um host, independentemente do escopo da equipe.

    * [Opcional] Ativar ou desativar **Eventos de infraestrutura**. Marque essa caixa para permitir que os membros visualizem todos os eventos de infraestrutura customizada de cada usuário e agente Sysdig. Quando não está marcada, os usuários podem ver eventos de infraestrutura que são enviados especificamente para essa equipe. 

6. Incluir membros na equipe. Clique em  ** Designar usuário **. Procure um usuário e inclua-o.



## Alterando o escopo de uma equipe
{: #teams_scope}

Para mudar o escopo dos dados que são visíveis para os membros de uma equipe, conclua as etapas a seguir: 

1. Ative a IU da web. Para obter mais informações sobre como ativar a IU da web, consulte [Navegando para a IU da web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. No botão *Seletor* na barra de navegação, selecione **Monitorar operações**. Em seguida, escolha **Configurações**.

3. Selecione **Equipes**. A lista de equipes existentes é exibida.

4. Identifique a equipe e selecione-a. Os detalhes da equipe são exibidos.

5. Mude os detalhes de configuração na seção *Visibilidade*.

6. Clique em **Salvar**. 


## Incluindo usuários em uma equipe
{: #teams_users}

Para incluir membros em uma equipe, conclua as etapas a seguir: 

1. Ative a IU da web. Para obter mais informações sobre como ativar a IU da web, consulte [Navegando para a IU da web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. No botão *Seletor* na barra de navegação, selecione **Monitorar operações**. Em seguida, escolha **Configurações**.

3. Selecione **Equipes**. A lista de equipes existentes é exibida.

4. Identifique a equipe e selecione-a. Os detalhes da equipe são exibidos.

5. Clique em **Designar usuário** na seção *Usuários da equipe*.

6. Clique em **Salvar**. 


## Excluindo uma Equipe
{: #teams_delete}

A equipe padrão, **Operações de monitor**, não pode ser excluída. 

Conclua as etapas a seguir para excluir uma equipe:

1. Ative a IU da web. Para obter mais informações sobre como ativar a IU da web, consulte [Navegando para a IU da web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. No botão *Seletor* na barra de navegação, selecione **Monitorar operações**. Em seguida, escolha **Configurações**.

3. Selecione **Equipes**. A lista de equipes existentes é exibida.

4. Identifique a equipe que você deseja excluir e selecione-a. Os detalhes da equipe são exibidos.

5. Clique em  ** Excluir equipe **.

**Nota:** quando você excluir uma equipe, os usuários que pertencerem apenas a essa equipe serão movidos para a equipe padrão.



