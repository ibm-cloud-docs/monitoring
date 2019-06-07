---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, ubuntu, analyze metrics

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


# Analisar métricas para um host Ubuntu
{: #ubuntu}

Use este tutorial para saber como configurar um host Ubuntu para encaminhar métricas para o serviço {{site.data.keyword.mon_full_notm}} no {{site.data.keyword.cloud_notm}}.
{:shortdesc}

Para configurar um servidor Ubuntu para encaminhar métricas, deve-se instalar um agente Sysdig. O agente usa uma chave de acesso (token) para autenticar com a instância do {{site.data.keyword.mon_full_notm}}. O agente Sysdig age como um coletor de dados. Ele coleta automaticamente as métricas.

Você visualiza métricas por meio da interface com o usuário baseada na web do Sysdig.

![Visão geral de componentes no {{site.data.keyword.cloud_notm}}](../images/ubuntu.png "Visão geral de componentes no {{site.data.keyword.cloud_notm}}")



## Antes de iniciar
{: #ubuntu_prereqs}

Trabalhe na região dos Estados Unidos da América. 

Leia sobre o {{site.data.keyword.mon_full_notm}}. Para obter mais informações, consulte [Sobre](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-about#about).

Use um ID do usuário que seja membro ou proprietário de uma conta do {{site.data.keyword.cloud_notm}}. Para obter um ID do usuário do {{site.data.keyword.cloud_notm}}, acesse [Registro ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/login){:new_window}.

Seu ID da {{site.data.keyword.IBM_notm}} deve ter designado políticas do IAM para cada um dos recursos a seguir: 

| Recurso                             | Escopo da política de acesso | Função    | Região    | Informações                  |
|--------------------------------------|----------------------------|---------|-----------|------------------------------|
| Grupo de recursos **Padrão**           |  Grupo de recursos            | Visualizador  | `Us-south`  | Essa política é necessária para permitir que o usuário veja instâncias de serviço no grupo de recursos Padrão.    |
| Serviço {{site.data.keyword.mon_full_notm}} |  Grupo de recursos            | Editor  | `Us-south`  | Essa política é necessária para permitir que o usuário provisione e administre o serviço {{site.data.keyword.mon_full_notm}} no grupo de recursos Padrão.   |
{: caption="Tabela 1. Lista de políticas do IAM necessárias para concluir o tutorial" caption-side="top"} 

Instale a CLI do {{site.data.keyword.cloud_notm}}. Para obter mais informações, consulte [Instalando a CLI do {{site.data.keyword.cloud_notm}}](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli).


## Etapa 1. Provisão de uma instância do {{site.data.keyword.mon_full_notm}}
{: #ubuntu_step1}

Para provisionar uma instância do {{site.data.keyword.mon_full_notm}} por meio da IU do {{site.data.keyword.cloud_notm}}, conclua as etapas a seguir:

1. [Efetue login em sua conta do {{site.data.keyword.cloud_notm}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/login){:new_window}.

	Depois de efetuar login com seu ID de usuário e senha, a IU do {{site.data.keyword.cloud_notm}} é aberta.

2. Clique em  ** Catálogo **. A lista dos serviços disponíveis no {{site.data.keyword.cloud_notm}} é aberta.

3. Para filtrar a lista de serviços exibida, selecione a categoria **Ferramentas do desenvolvedor**.

4. Clique no quadro  ** {{site.data.keyword.mon_full_notm}} **. O painel *Observabilidade* é aberto.

5. Selecione **Criar instância**. 

6. Insira um nome para a instância de serviço.

7. Selecione o grupo de recursos **Padrão**. 

    Por padrão, o grupo de recursos **Padrão** é configurado.

8. Selecione o plano de serviço  ** Lite **. 

    Por padrão, o plano **Lite** é configurado.

    Para obter mais informações sobre outros planos de serviços, consulte [Planos de precificação](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-pricing_plans#pricing_plans).

9. Para provisionar o serviço {{site.data.keyword.mon_full_notm}} no grupo de recursos do {{site.data.keyword.cloud_notm}} ao qual você está conectado, clique em **Criar**.

Depois que você provisiona uma instância, o painel *Observabilidade* é aberto. 


**Nota:** para provisionar uma instância por meio da CLI, consulte [Provisionando uma instância por meio da CLI do {{site.data.keyword.cloud_notm}}](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-provision#provision_cli).


## Etapa 2. Configurar seu servidor Ubuntu para enviar métricas para sua instância
{: #ubuntu_step2}

Para configurar seu servidor Ubuntu para enviar métricas para sua instância do {{site.data.keyword.mon_full_notm}}, deve-se instalar um agente Sysdig. 

Conclua as etapas a seguir por meio da linha de comandos:

1. Abra um terminal. Em seguida, efetue login no {{site.data.keyword.cloud_notm}}. Execute o comando a seguir e siga os prompts:

    ```
    ibmcloud login -a cloud.ibm.com
    ```
    {: codeblock}

    Selecione a conta na qual a instância do {{site.data.keyword.mon_full_notm}} está disponível.

2. Obtenha a chave de acesso do Sysdig. Para obter mais informações, consulte [Obtendo a chave de acesso por meio da IU do {{site.data.keyword.cloud_notm}}](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key_ibm_cloud_ui).

3. Obtenha a URL de ingestão. Para obter mais informações, consulte [Terminais do coletor Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-endpoints#endpoints_ingestion).

4. Implemente o agente Sysdig. Execute o seguinte comando:

    ```
    curl -s https://s3.amazonaws.com/download.draios.com/stable/install-agent | sudo bash -s -- --access_key SYSDIG_ACCESS_KEY --collector COLLECTOR_ENDPOINT --collector_port 6443 --secure false --check_certificate false --tags TAG_DATA --additional_conf 'sysdig_capture_enabled: false'
    ```
    {: codeblock}

    Em que

    * SYSDIG_ACCESS_KEY é a chave de ingestão para a instância.

    * COLLECTOR_ENDPOINT é a URL de ingestão da região na qual a instância de monitoramento está disponível.

    * TAG_DATA são tags separadas por vírgula formatadas como *TAG_NAME:TAG_VALUE*. É possível associar uma ou mais tags a seu agente Sysdig. Por exemplo, *role:serviceX,location:us-south*. Posteriormente, será possível usar essas tags para identificar métricas no ambiente em que o agente está em execução.

    * Configure **sysdig_capture_enabled** como *false* para desativar o recurso de captura de Sysdig. Por padrão, é configurado como *true*. Para obter mais informações, consulte [Trabalhando com capturas](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures).

Se o agente Sysdig falhar em ser instalado corretamente, instale os cabeçalhos de kernel manualmente. Escolha uma distribuição e execute o comando para essa distribuição. Em seguida, tente novamente a implementação do agente Sysdig.

* **Para distribuições Debian e Ubuntu do Linux**, execute o comando a seguir:

    ```
    apt-get -y install linux-headers-$(uname -r)
    ```
    {: codeblock}

* **Para distribuições RHEL, CentOS e Fedora do Linux**, execute o comando a seguir:

    ```
    yum -y install kernel-devel-$(uname -r)
    ```
    {: codeblock}



## Etapa 3. Ativar a IU da web do Sysdig
{: #ubuntu_step3}

Conclua as etapas a seguir para ativar a IU da web:

1. [Efetue login em sua conta do {{site.data.keyword.cloud_notm}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/login){:new_window}.

	Depois que você efetua login com seu ID do usuário e senha, o Painel do {{site.data.keyword.cloud_notm}} é aberto.

2. No menu de navegação, selecione **Observabilidade**. 

3. Selecione **Monitorando**. 

    A lista de instâncias disponíveis no {{site.data.keyword.cloud_notm}} é exibida.

4. Selecione sua instância. Em seguida, clique em **Visualizar Sysdig**.

Se o agente Sysdig for configurado com êxito, a visualização *EXPLORAR* será aberta.

No entanto, se o agente Sysdig não for instalado com êxito, apontar para o terminal de ingestão errado ou a chave de acesso estiver incorreta, a página aberta informará o que fazer a seguir.

É possível ter somente uma sessão da IU da web aberta por navegador.
{: tip}


## Etapa 4. Monitorar seu servidor Ubuntu
{: #ubuntu_step4}

É possível monitorar o seu servidor do Ubuntu na visualização **EXPLORAR** que está disponível por meio da IU da web. Essa visualização é o ponto de início para solucionar problemas e monitorar sua infraestrutura. É a página inicial padrão da IU da web para usuários.

Na seção *Host e contêineres*, é possível localizar a entrada para o seu servidor Ubuntu. Clique em **Host e contêineres** ![Host e contêineres](../images/switch_hosts.png) para alternar origens de dados. Em seguida, selecione seu servidor Ubuntu. Os dados que são exibidos correspondem ao servidor Ubuntu que você seleciona.

Por exemplo, para configurar a codificação de cores para uma coluna, conclua as etapas a seguir:

1. Selecione uma coluna. Passe o mouse sobre o título da coluna. Em seguida, selecione o ícone de lápis.
2. Alternar a barra para ativar a codificação de cores.
3. Configure valores para os diferentes limites.



## Próximos passos
{: #ubuntu_next_steps}

Crie um painel customizado. Para obter mais informações, consulte [Trabalhando com painéis](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-dashboards#dashboards).

Também é possível saber mais sobre alertas. Para obter mais informações, consulte [Trabalhando com alertas](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-monitoring#monitoring_alerts). 






