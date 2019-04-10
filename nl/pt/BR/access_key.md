---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, access key

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

# Trabalhando com Chaves de Acesso
{: #access_key}

A **Chave de acesso** é um token que deve ser usado para configurar agentes Sysdig para encaminhar dados com êxito para sua instância do {{site.data.keyword.mon_full_notm}} no {{site.data.keyword.Bluemix}}.   
{:shortdesc}


## Obtendo a chave de acesso por meio da IU do {{site.data.keyword.cloud_notm}}
{: #access_key_ibm_cloud_ui}

Para obter a chave de acesso para uma instância do {{site.data.keyword.mon_full_notm}} por meio da IU do {{site.data.keyword.cloud_notm}}, conclua as etapas a seguir:

1. Efetue login em sua conta do  {{site.data.keyword.cloud_notm}} .

    Clique em [Painel do {{site.data.keyword.cloud_notm}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/login){:new_window} para ativar o painel do {{site.data.keyword.cloud_notm}}.

	Depois de efetuar login com seu ID de usuário e senha, a IU do {{site.data.keyword.cloud_notm}} é aberta.

2. No menu de navegação, selecione **Observabilidade**. 

3. Selecione **Monitorando**. O painel do  {{site.data.keyword.mon_full_notm}}  é aberto. É possível ver a lista de instâncias de monitoramento que estão disponíveis no {{site.data.keyword.cloud_notm}}.

3. Identifique a instância para a qual você deseja obter a chave de acesso e clique em **Visualizar chave de acesso**.

4. Uma janela pop-up é aberta, na qual é possível clicar em **Mostrar** para visualizar a chave de acesso.



## Obtendo a chave de acesso por meio da CLI
{: #access_key_cli}

Para obter a chave de acesso para uma instância do Sysdig por meio da linha de comandos, conclua as etapas a seguir:

1. [ Pré-requisito ] Instale a CLI do  {{site.data.keyword.cloud_notm}} .

   Para obter mais informações, consulte [Instalando a CLI do {{site.data.keyword.cloud_notm}}](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli).

   Se a CLI estiver instalada, continue com a próxima etapa.

2. Efetue login na região no {{site.data.keyword.cloud_notm}} em que a instância do Sysdig está em execução. Execute o comando a seguir: [`ibmcloud login`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_login)

3. Configure o grupo de recursos no qual a instância do Sysdig está em execução. Execute o comando a seguir: [`ibmcloud target`](/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_target)

    Por padrão, o grupo de recursos `default` é configurado.

4. Obtenha o nome da instância. Execute o comando a seguir: [`ibmcloud resource service-instances`](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_instances)

    ```
    ibmcloud resource service-instances
    ```
    {: pre}

5. Obtenha o nome da chave de API que está associada à instância do Sysdig. Execute o comando  [ ` ibmcloud resource service-keys ` ](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_instances) :

    ```
    ibmcloud resource service-keys --instance-name INSTANCE_NAME
    ```
    {: pre}

    em que INSTANCE_NAME é o nome da instância obtida na etapa anterior.

6. Obtenha a chave de acesso. Execute o comando  [ ` ibmcloud resource service-key ` ](/docs/cli/reference/ibmcloud/cli_resource_group.html#ibmcloud_resource_service_key) :

    ```
    ibmcloud resource service-key APIKEY_NAME
    ```
    {: pre}

    em que APIKEY_NAME é o nome da chave de API.
 
    A saída desse comando inclui o campo **Chave de acesso do Sysdig**, que contém a chave de acesso para a instância.


Por exemplo, o comando a seguir mostra a saída de um ID de serviço de amostra:

```
$ ic resource service-key "{{site.data.keyword.mon_full_notm}}-shg-key-admin"
Retrieving service key {{site.data.keyword.mon_full_notm}}-shg-key-admin in resource group Default under account Sample's Account as sample@ibm.com...
OK
                  
Name:          {{site.data.keyword.mon_full_notm}}-shg-key-admin   
ID:            crn:v1:staging:public:sysdig-monitor:us-south:a/1234567891234567891212346461b066:6e2637ff-4548-47a6-bf30-063fbe49760e:resource-key:bb18c701-0dba-4c4e-bda5-74380e41c4bf   
Created At:    Fri Nov  2 13:40:39 UTC 2018   
State:         active   
Credentials:                                      
               iam_role_crn:                crn:v1:bluemix:public:iam::::role:Administrator      
               iam_serviceid_crn:           crn:v1:staging:public:iam-identity::a/1234567891234567891212346461b066::serviceid:ServiceId-88888888-4444-4444-4444-77777777777      
               Sysdig Access Key:           xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx      
               Sysdig Customer Id:          111      
               iam_apikey_description:      Auto generated apikey during resource-key operation for Instance - crn:v1:staging:public:sysdig-monitor:us-south:a/1234567891234567891212346461b066:6e2637ff-4548-47a6-bf30-063fbe49760e::      
               iam_apikey_name:             auto-generated-apikey-bb18c701-0dba-4c4e-bda5-74380e41c4bf      
               Sysdig Collector Endpoint:   ingest.us-south.monitoring.test.cloud.ibm.com      
               Sysdig Endpoint:             https://us-south.monitoring.test.cloud.ibm.com      
               apikey:                      xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx     
                  
Parameters:                      
               role_crn:   crn:v1:bluemix:public:iam::::role:Administrator      
```
{: screen}




## Reconfigurando a chave de acesso 
{: #access_key_reset}

Se a chave de acesso estiver comprometida ou se você tiver uma política para renová-la após um número de dias, será possível gerar uma nova chave e excluir a antiga.

Para renovar a chave de acesso para uma instância do {{site.data.keyword.mon_full_notm}}, conclua as etapas a seguir:

1. Ative a IU da web do  {{site.data.keyword.mon_full_notm}} . Para obter mais informações, consulte [Navegando para a IU da web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch).

2. No botão *Seletor* na barra de navegação, escolha **Configurações**.

2. Na seção *Gerenciamento de senha*, clique em **Reconfigurar a sua senha**.

**Nota:** depois de reconfigurar a chave de acesso do Sysdig, deve-se atualizar a chave de acesso para quaisquer origens de log configuradas para encaminhar métricas para essa instância do {{site.data.keyword.mon_full_notm}}.
