---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, provision instance

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

# Provisionando uma instância
{: #provision}

Antes de poder monitorar e gerenciar métricas com o Sysdig, deve-se primeiro provisionar uma instância do serviço no {{site.data.keyword.Bluemix}}.
{:shortdesc}

Para provisionar uma instância do Sysdig em uma região de Nuvem pública, deve-se selecionar o plano de serviço que está associado à instância, a região em que suas métricas são coletadas e o plano que determina o número de métricas que é possível monitorar e seu período de retenção.



## Provisionando uma instância do Sysdig por meio do catálogo
{: #provision_ui}

Para provisionar uma instância do Sysdig por meio do catálogo do {{site.data.keyword.cloud_notm}}, conclua as etapas a seguir:

1. Efetue login em sua conta do  {{site.data.keyword.cloud_notm}} .

    Clique em [Painel do {{site.data.keyword.cloud_notm}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/login){:new_window} para ativar o painel do {{site.data.keyword.cloud_notm}}.

	Depois de efetuar login com seu ID de usuário e senha, a IU do {{site.data.keyword.cloud_notm}} é aberta.

2. Clique em  ** Catálogo **. A lista dos serviços que estão disponíveis no {{site.data.keyword.cloud_notm}} é aberta.

3. Para filtrar a lista de serviços exibida, selecione a categoria **Ferramentas do desenvolvedor**.

4. Clique no quadro  ** {{site.data.keyword.mon_full_notm}} ** . O painel *Observabilidade* é aberto.

5. Selecione **Criar instância**. 

6. Selecione um plano de serviço. Por padrão, o plano de **Experiência** é configurado.

    Para obter mais informações sobre os planos de serviços, veja [Planos de serviços](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-pricing_plans#pricing_plans).

7. Selecione um grupo de recursos. Por padrão, o grupo de recursos **Padrão** é configurado.

8. Clique em  ** Criar **.

Depois de provisionar uma instância, 

* O painel *Observabilidade* é aberto. 
* Um ID de serviço é criado automaticamente. É possível usar esse ID de serviço para obter a chave de acesso do Sysdig para sua instância.

Em seguida, configure uma origem de métrica incluindo um agente Sysdig. Esse agente é responsável por coletar e encaminhar métricas para o Sysdig. 



## Provisionando uma instância do Sysdig por meio da CLI
{: #provision_cli}

Para provisionar uma instância de Sysdig por meio da linha de comandos, conclua as etapas a seguir:

1. [ Pré-requisito ] Instale a CLI do  {{site.data.keyword.cloud_notm}} .

   Para obter mais informações, consulte [Instalando a CLI do {{site.data.keyword.cloud_notm}}](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli).

   Se a CLI estiver instalada, continue com a próxima etapa.

2. Efetue login na região no {{site.data.keyword.cloud_notm}} em que você deseja provisionar a instância. Execute o comando a seguir: [`ibmcloud login`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_login)

3. Configure o grupo de recursos no qual você deseja provisionar a instância. Execute o comando a seguir: [`ibmcloud target`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_target)

    Por padrão, o grupo de recursos `default` é configurado.

4. Crie a instância Sysdig. Execute o comando  [ ` ibmcloud resource service-instance-create ` ](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_instance_create) :

    ```
    ibmcloud resource service-instance-create NAME sysdig-monitor SERVICE_PLAN_NAME LOCATION
    ```
    {: codeblock}

    sendo

    * NAME é o nome da instância do Sysdig
    
    * *sysdig-monitor* é o nome do serviço {{site.data.keyword.mon_full_notm}} no {{site.data.keyword.cloud_notm}}
    
    * SERVICE_PLAN_NAME é o tipo de plano. Os valores válidos são:  * lite *,  * graduado-tier *
    
    * LOCATION é a região na qual a instância é criada

    Por exemplo, para provisionar uma instância com o plano pago, execute o comando a seguir:

    ```
    ibmcloud resource service-instance-create sysdig-instance-01 sysdig-monitor graduated-tier us-south
    ```
    {: screen}

