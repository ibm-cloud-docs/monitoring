---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, iam, access groups

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

 
# Trabalhando com políticas do IAM e grupos de acesso
{: #iam_work}

O {{site.data.keyword.iamlong}} (IAM) permite que você autentique os usuários de forma segura e controle o acesso a todos os recursos de nuvem de forma consistente no {{site.data.keyword.cloud_notm}}. 
{:shortdesc}

Para conceder privilégios de administrador do Sysdig a um usuário, é possível designar ao usuário qualquer uma das funções a seguir:

* Função da plataforma `Administrador`: conceda essa função se o usuário também for um administrador para o serviço Sysdig no {{site.data.keyword.cloud_notm}}.
* Função da plataforma `Editor`: conceda essa função se o usuário deve ser capaz de provisionar ou remover instâncias do Sysdig no {{site.data.keyword.cloud_notm}}.
* Função de serviço `Gerenciador`: conceda essa função se o usuário não deve ser capaz de gerenciar o serviço Sysdig no {{site.data.keyword.cloud_notm}}.

Para conceder privilégios de usuário do Sysdig a um usuário, é possível designar a um usuário a função de serviço `Gravador`.

**Nota:** para gerenciar o acesso ou designar um novo acesso para usuários usando políticas do IAM, deve-se ser o proprietário da conta, o administrador em todos os serviços na conta ou um administrador para o serviço ou a instância de serviço específica. 

Como o **proprietário da conta** ou como um **administrador de serviço do {{site.data.keyword.mon_full_notm}}**, deve-se ter permissões para executar as ações da plataforma a seguir: 

* Conceder a outros membros de conta acesso para trabalhar com o serviço
* Provisione uma instância de serviço
* Excluir uma instância de serviço
* Visualize detalhes de uma instância de serviço
* Criar um ID de serviço

Como um **Usuário do Devops**, deve-se ter permissões para executar as ações de plataforma a seguir: 

* Provisione uma instância de serviço
* Excluir uma instância de serviço
* Visualize detalhes de uma instância de serviço
* Criar um ID de serviço


## Concedendo permissões a um usuário para se tornar um administrador do serviço na conta do {{site.data.keyword.cloud_notm}}
{: #admin_account}

Para conceder a um usuário a função de administrador para gerenciar o serviço na conta, o usuário deve ter uma política do IAM para o serviço {{site.data.keyword.mon_full_notm}} com a função da plataforma **Administrador**. Deve-se designar esse acesso de usuário a um recurso individual na conta. 

Conclua as etapas a seguir para designar uma função de administrador de usuário para o serviço {{site.data.keyword.mon_full_notm}} na conta: 

1. Na barra de menus, clique em **Gerenciar** &gt; **Acesso (IAM)** e, em seguida, selecione **Usuários**.
2. Na linha para o usuário que você deseja designar acesso, selecione o menu **Ações** e, em seguida, clique em **Designar acesso**.
3. Selecione **Designar acesso a recursos**.
4. Selecione **{{site.data.keyword.mon_full_notm}}**.
5. Selecione  ** Todas as regiões atuais **.
6. Selecione  ** Todas as instâncias de serviço atuais **.
7. Selecione a função da plataforma **Administrador**.
8. Clique em Designar.


## Concedendo permissões a um usuário para se tornar um administrador do serviço dentro de um grupo de recursos
{: #admin_rg}

Para conceder a um usuário a função de administrador para gerenciar instâncias dentro de um grupo de recursos na conta, o usuário deve ter uma política do IAM para o serviço {{site.data.keyword.mon_full_notm}} com a função da plataforma **Administrador** dentro do contexto do grupo de recursos. 

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


## Concedendo permissões a um usuário do Devops para gerenciar o serviço na conta do {{site.data.keyword.cloud_notm}}
{: #devops_account}

É necessário ter uma política do IAM para o serviço {{site.data.keyword.mon_full_notm}} com a função da plataforma **Editor**.

Conclua as etapas a seguir para designar a um usuário a função de editor para o serviço {{site.data.keyword.mon_full_notm}} na conta: 

1. Na barra de menus, clique em **Gerenciar** &gt; **Acesso (IAM)** e, em seguida, selecione **Usuários**.
2. Na linha para o usuário que você deseja designar acesso, selecione o menu **Ações** e, em seguida, clique em **Designar acesso**.
3. Selecione **Designar acesso a recursos**.
4. Selecione **{{site.data.keyword.mon_full_notm}}**.
5. Selecione  ** Todas as instâncias de serviço **.
6. Selecione a função da plataforma **Editor**.
7. Clique em Designar.

## Concedendo permissões a um usuário do Devops para gerenciar uma instância na conta do {{site.data.keyword.cloud_notm}}
{: #devops_account_instance}

Conclua as etapas a seguir para designar a um usuário a função de editor em uma instância do serviço {{site.data.keyword.mon_full_notm}} na conta: 

1. Na barra de menus, clique em **Gerenciar** &gt; **Acesso (IAM)** e, em seguida, selecione **Usuários**.
2. Na linha para o usuário que você deseja designar acesso, selecione o menu **Ações** e, em seguida, clique em **Designar acesso**.
3. Selecione **Designar acesso a recursos**.
4. Selecione **{{site.data.keyword.mon_full_notm}}**.
5. Selecione a instância.
6. Selecione a função da plataforma **Editor**.
7. Clique em Designar.



## Concedendo permissões a um usuário do Devops para gerenciar o serviço dentro de um grupo de recursos
{: #devops_rg}

Você precisa de uma política do IAM para o serviço {{site.data.keyword.mon_full_notm}} com a função da plataforma **Editor**.

Conclua as etapas a seguir para designar um usuário a função de editor para o serviço {{site.data.keyword.mon_full_notm}} dentro do contexto de um grupo de recursos: 

1. Na barra de menus, clique em **Gerenciar** &gt; **Acesso (IAM)** e, em seguida, selecione **Usuários**.
2. Na linha para o usuário que você deseja designar acesso, selecione o menu **Ações** e, em seguida, clique em **Designar acesso**.
3. Selecione **Designar acesso em um grupo de recursos**.
4. Selecione um grupo de recursos.
5. Se o usuário não tiver uma função já concedida para o grupo de recursos selecionado, escolha uma função para o campo **Designar acesso a um grupo de recursos**. 

    Dependendo da função selecionada, o usuário pode visualizar o grupo de recursos em seu painel, editar o nome do grupo de recursos ou gerenciar o acesso de usuário ao grupo. 
    
    Será possível selecionar **Sem acesso** se você desejar que o usuário tenha acesso somente ao serviço {{site.data.keyword.mon_full_notm}} no grupo de recursos.

6. Selecione **{{site.data.keyword.mon_full_notm}}**.
7. Selecione a função da plataforma **Editor**.
8. Clique em **Designar**.

## Concedendo permissões para gerenciar métricas e configurar alertas no Sysdig
{: #admin_user_sysdig}

Como um **usuário administrativo** no Sysdig, deve-se ter permissões para executar as ações a seguir: 

* Incluir origens de métrica
* Visualizar Métricas
* Métricas de procura
* Filtrar métricas
* Configurar alertas

Portanto, você precisa das políticas a seguir:

* Uma política do IAM para o serviço {{site.data.keyword.mon_full_notm}} com a função da plataforma **Editor**. Essa política permite visualizar os detalhes da instância de serviço por meio da linha de comandos e no painel do {{site.data.keyword.cloud_notm}}.
* Uma política do IAM para o serviço {{site.data.keyword.mon_full_notm}} com a função de serviço **Gerenciador**. Essa política permite monitorar, filtrar e pesquisar métricas e definir alertas por meio da IU da web do Sysdig.

**Nota:** como um administrador do serviço, ao conceder essas políticas a um usuário, considere fazê-lo no contexto de um grupo de recursos. Uma instância do {{site.data.keyword.mon_full_notm}} é provisionada no contexto de um grupo de recursos. Portanto, é necessário conceder permissões de acesso no contexto do grupo de recursos.


Conclua as etapas a seguir para designar a um usuário ambas as políticas para o serviço {{site.data.keyword.mon_full_notm}} no contexto de um grupo de recursos: 

1. Na barra de menus, clique em **Gerenciar** &gt; **Acesso (IAM)** e, em seguida, selecione **Usuários**.
2. Na linha para o usuário que você deseja designar acesso, selecione o menu **Ações** e, em seguida, clique em **Designar acesso**.
3. Selecione **Designar acesso em um grupo de recursos**.
4. Selecione um grupo de recursos.
5. Se o usuário não tiver uma função já concedida para o grupo de recursos selecionado, escolha uma função para o campo **Designar acesso a um grupo de recursos**. 

    Dependendo da função selecionada, o usuário pode visualizar o grupo de recursos em seu painel, editar o nome do grupo de recursos ou gerenciar o acesso de usuário ao grupo. 
    
    Será possível selecionar **Sem acesso** se você desejar que o usuário tenha acesso somente ao serviço {{site.data.keyword.mon_full_notm}} no grupo de recursos.

6. Selecione **{{site.data.keyword.mon_full_notm}}**.
7. Selecione a função da plataforma **Editor**.
8. Selecione a função de serviço **Gerenciador**.
8. Clique em **Designar**.

## Concedendo permissões a um usuário para visualizar métricas no Sysdig
{: #user_sysdig}

Como um **usuário**, **auditor** ou **desenvolvedor**, você pode precisar de permissões para executar as ações a seguir: 

* Visualize métricas
* Métricas de procura
* Filtrar métricas

Portanto, você precisa das políticas a seguir:

* Uma política do IAM para o serviço {{site.data.keyword.mon_full_notm}} com a função da plataforma **Visualizador**. Essa política permite visualizar os detalhes da instância de serviço por meio da linha de comandos e no painel do {{site.data.keyword.cloud_notm}}.
* Uma política do IAM para o serviço {{site.data.keyword.mon_full_notm}} com a função de serviço **Gravador**. Essa política permite visualizar, filtrar e procurar métricas por meio da IU da web do Sysdig.

**Nota:** como um administrador do serviço, ao conceder essas políticas a um usuário, considere fazê-lo no contexto de um grupo de recursos. Uma instância do {{site.data.keyword.mon_full_notm}} é provisionada no contexto de um grupo de recursos. Portanto, é necessário conceder permissões de acesso no contexto do grupo de recursos.

Conclua as etapas a seguir para designar a um usuário ambas as políticas para o serviço {{site.data.keyword.mon_full_notm}} no contexto de um grupo de recursos: 

1. Na barra de menus, clique em **Gerenciar** &gt; **Acesso (IAM)** e, em seguida, selecione **Usuários**.
2. Na linha para o usuário que você deseja designar acesso, selecione o menu **Ações** e, em seguida, clique em **Designar acesso**.
3. Selecione **Designar acesso em um grupo de recursos**.
4. Selecione um grupo de recursos.
5. Se o usuário não tiver uma função já concedida para o grupo de recursos selecionado, escolha uma função para o campo **Designar acesso a um grupo de recursos**. 

    Dependendo da função selecionada, o usuário pode visualizar o grupo de recursos em seu painel, editar o nome do grupo de recursos ou gerenciar o acesso de usuário ao grupo. 
    
    Será possível selecionar **Sem acesso** se você desejar que o usuário tenha acesso somente ao serviço {{site.data.keyword.mon_full_notm}} no grupo de recursos.

6. Selecione **{{site.data.keyword.mon_full_notm}}**.
7. Selecione a função de plataforma  ** Visualizador **.
8. Selecione a função de serviço  ** Gravador **.
8. Clique em **Designar**.

