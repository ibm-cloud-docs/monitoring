---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, iam

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

 
# Gerenciando o acesso de usuário no  {{site.data.keyword.cloud_notm}}
{: #iam}

O {{site.data.keyword.iamlong}} (IAM) permite que você autentique os usuários de forma segura e controle o acesso a todos os recursos de nuvem de forma consistente no {{site.data.keyword.cloud_notm}}. 
{:shortdesc}

**Uma política de acesso com uma função de usuário do IAM definida deve ser designada a cada usuário que acessa o serviço {{site.data.keyword.mon_full_notm}} em sua conta.** A política determina quais ações o usuário pode executar no contexto do serviço ou da instância selecionada. As ações permitidas são customizadas e definidas como operações que têm permissão para serem executadas no serviço. As ações são, então, mapeadas para funções de usuário do IAM.

As *Políticas* permitem que o acesso seja concedido em níveis diferentes. Algumas das opções incluem o seguinte: 

* Acesso a todos os serviços ativados pelo IAM em sua conta
* Acesso em todas as instâncias do serviço em uma única região em sua conta
* Acesso a uma instância de serviço individual em sua conta
* Acesso a todas as instâncias do serviço dentro do contexto de um grupo de recursos
* Acesso a todas as instâncias do serviço em uma única região dentro do contexto de um grupo de recursos
* Acesso a todos os serviços ativados pelo IAM dentro do contexto de um grupo de recursos

As *Funções* definem as ações que um usuário ou serviceID pode executar. Há diferentes tipos de funções no {{site.data.keyword.cloud_notm}}:
* As *Funções de gerenciamento de plataforma* permitem que os usuários executem tarefas em recursos de serviço no nível de plataforma, por exemplo, designar acesso de usuário para o serviço, criar ou excluir IDs de serviço, criar instâncias, designar políticas para seu serviço a outros usuários e ligar instâncias a aplicativos.
* As *Funções de acesso ao serviço* permitem que os usuários sejam designados a níveis variados de permissão para chamar a API do serviço.

**Para organizar um conjunto de usuários e IDs de serviço em uma única entidade que torne fácil gerenciar permissões do IAM, use **grupos de acesso*.** É possível designar uma única política ao grupo em vez de designar o mesmo acesso múltiplas vezes por usuário ou ID de serviço individual.
{: tip}


## Gerenciando o acesso usando grupos de acesso
{: #iam_groups}

Para gerenciar o acesso ou designar um novo acesso para os usuários usando grupos de acesso, deve-se ser o proprietário da conta, o administrador ou o editor em todos os serviços ativados de Identidade e Acesso na conta ou o administrador ou editor designado para o Serviço de grupos de acesso do IAM. 

Escolha qualquer uma das ações a seguir para gerenciar grupos de acesso no {{site.data.keyword.cloud_notm}}:

* [ Criando um grupo de acesso ](/docs/iam?topic=iam-groups#create_ag).
* [ Designando acesso a um grupo ](/docs/iam?topic=iam-groups#access_ag).


## Gerenciando o acesso designando políticas diretamente aos usuários
{: #iam_users}

Para gerenciar o acesso ou designar um novo acesso para usuários usando políticas do IAM, deve-se ser o proprietário da conta, o administrador em todos os serviços na conta ou um administrador para o serviço ou a instância de serviço específica. 

Escolha qualquer uma das ações a seguir para gerenciar políticas do IAM no {{site.data.keyword.cloud_notm}}:

* Para modificar as permissões de um usuário, consulte [Editando o acesso existente](/docs/iam?topic=iam-iammanidaccser#edit_existing).
* Para conceder permissões a um usuário, consulte [Designar novo acesso](/docs/iam?topic=iam-iammanidaccser#assign_new_access).
* Para revogar permissões, consulte  [ Removendo o acesso ](/docs/iam?topic=iam-iammanidaccser#removing_access).
* Para revisar as permissões de um usuário, consulte [Revisando o seu acesso designado](/docs/iam?topic=iam-iammanidaccser#review_your_access).


## {{site.data.keyword.cloud_notm}}  funções de plataforma
{: #iam_platform}

Use a tabela a seguir para identificar a função da plataforma que é possível conceder a um usuário no {{site.data.keyword.cloud_notm}} para executar qualquer uma das ações da plataforma a seguir:

| Ações da plataforma                                                        | Funções da plataforma {{site.data.keyword.cloud_notm}}    | 
|-------------------------------------------------------------------------|------------------------------------------------------|
| `Conceder a outros membros de conta acesso para trabalhar com o serviço`           | Administrador                                        | 
| `Provisionar uma instância de serviço`                                          | Administrador </br>Editor                            | 
| `Excluir uma instância de serviço`                                             | Administrador </br>Editor                            | 
| `Criar um ID de serviço`                                                   | Administrador </br>Editor                            |
| `Visualizar detalhes de uma instância de serviço`                                    | Administrador </br>Editor </br>Operador </br>Visualizador  | 
| `Visualizar instâncias de serviço no painel Monitoramento de observação`      | Administrador </br>Editor </br>Operador </br>Visualizador  | 
{: caption="Tabela 1. Funções e ações do usuário do IAM" caption-side="top"}



## Funções de Sysdig
{: #iam_sysdig_roles}

A tabela a seguir descreve as funções e ações do Sysdig por função:

| Ações                                                                    | Função do Sysdig                                          | 
|----------------------------------------------------------------------------|------------------------------------------------------|
| `Reconfigurar a chave de acesso do Sysdig `                                              | Administrador                                                |
| `Gerenciar usuários`                                                             | Administrador                                                |
| `Criar, configurar e excluir equipes`                                      | Administrador                                                |
| `Configurar e remover canais de notificação`                              | Administrador                                                | 
| `Configurar e remover agentes Sysdig`                                       | Administrador                                                |
| `Criar, excluir e editar o conteúdo na IU da web do Sysdig`                    | Administrador </br>Usuário                                      |  
| `Visualizar métricas por meio da IU da web do Sysdig`                                   | Administrador </br>Usuário                                      |  
| `Criar e excluir alertas`                                                 | Administrador </br>Usuário                                      | 
| `Criar e excluir capturas`                                               | Administrador </br>Usuário                                      |   
{: caption="Tabela 2. Funções e ações do Sysdig" caption-side="top"}


## Mapeamento de funções Sysdig para funções  {{site.data.keyword.cloud_notm}}
{: #iam_sysdig}

Use a tabela a seguir para ver como uma função do {{site.data.keyword.cloud_notm}} é mapeada para uma função do Sysdig:

| Tipo de Função        | Função               | Função do Sysdig                | Descrição                                 |
|---------------------|--------------------|----------------------------|---------------------------------------------|
| Função da plataforma       | Administrador      | Administrador                      | Concede privilégios de administrador do Sysdig ao usuário.   | 
| Função de serviço        | Gerente            | Administrador                      | Concede privilégios de administrador do Sysdig ao usuário.   | 
| Função de serviço        | Gravador             | Usuário                       | Concede ao usuário privilégios de usuário do Sysdig.    |
| Função de serviço        | Leitor             |                            | Nenhuma permissão é concedida.                 |
{: caption="Tabela 3. Funções de Sysdig" caption-side="top"}


