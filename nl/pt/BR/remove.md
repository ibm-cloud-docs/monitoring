---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, delete instance

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

# Removendo uma instância
{: #remove}

É possível remover uma instância do serviço {{site.data.keyword.mon_full_notm}} por meio da IU do {{site.data.keyword.Bluemix}} ou por meio da linha de comandos.
{:shortdesc}

Ao remover uma instância do {{site.data.keyword.cloud_notm}}, considere as informações a seguir para limpeza:

1. Anote a lista de origens que encaminham métricas para a instância do {{site.data.keyword.mon_full_notm}} que você deseja remover. Deve-se remover o agente Sysdig de cada origem.
2. Remover permissões que são concedidas aos usuários para que trabalhem com a instância. 

    Caso um grupo de acesso seja usado para gerenciar permissões para acessar a instância, deve-se
remover o grupo de acesso.

    Caso um grupo de acesso seja usado para gerenciar permissões para acessar instâncias de serviço diferentes, deve-se remover as políticas que concedem permissões para a instância que você deseja remover.
    
    Caso políticas individuais sejam concedidas aos usuários, deve-se reunir as informações de
cada usuário que tem acesso à instância. Em seguida, deve-se remover, uma a uma, as políticas relacionadas
à instância que você deseja excluir.


Em seguida, exclua a instância do Painel do {{site.data.keyword.cloud_notm}}.


## Removendo uma instância por meio da IU do {{site.data.keyword.cloud_notm}}
{: #remove_ui}

Para remover uma instância do {{site.data.keyword.mon_full_notm}} usando a IU do {{site.data.keyword.cloud_notm}}, conclua as etapas a seguir:

1. [Efetue login em sua conta do {{site.data.keyword.cloud_notm}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/login){:new_window}.

	Depois de efetuar login com seu ID de usuário e senha, a IU do {{site.data.keyword.cloud_notm}} é aberta.

2. Selecione  ** Observabilidade **. 

3. Selecione **Monitorando**. A lista das instâncias é exibida.

4. Selecione a instância que você deseja excluir.

5. A partir do menu  * Ação * , selecione  ** Remover **.


## Removendo uma instância por meio da CLI
{: #remove_cli}

Para remover uma instância do {{site.data.keyword.mon_full_notm}} por meio da linha de comandos, conclua as etapas a seguir:

1. [Pré-requisito] Instale a CLI do {{site.data.keyword.cloud_notm}}. Se a CLI estiver instalada, continue com a próxima etapa.

   Para obter mais informações, consulte [Instalando a CLI do {{site.data.keyword.cloud_notm}}](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli).

2. Efetue login na região no {{site.data.keyword.cloud_notm}} em que você deseja provisionar a instância. Execute o comando a seguir: [`ibmcloud login`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_login)

3. Configure o grupo de recursos no qual a instância é provisionada. Execute o comando a seguir: [`ibmcloud target`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_target)

    Por padrão, o grupo de recursos `default` é configurado.

4. Remova a instância. Execute o comando [`ibmcloud resource service-instance-delete`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_instance_delete):

    ```
    ibmcloud resource service-instance-delete NAME 
    ```
    {: codeblock}

    Em que NAME é o nome da instância

    Por exemplo, para remover uma instância, execute o comando a seguir:

    ```
    ibmcloud resource service-instance-delete sysdig-instance-01
    ```
    {: codeblock}
