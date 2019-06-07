---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, launch web UI

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

# Navegando para a IU da web
{: #launch}

Depois de provisionar uma instância do serviço {{site.data.keyword.mon_full_notm}} no {{site.data.keyword.Bluemix}} e configurar um agente Sysdig para uma origem de métricas, é possível visualizar, monitorar e gerenciar métricas por meio da IU da web do {{site.data.keyword.mon_full_notm}}.
{:shortdesc}


## Conceder políticas do IAM a um usuário para visualizar dados 
{: #launch_step1}

**Nota:** deve-se ser um administrador do serviço {{site.data.keyword.mon_full_notm}}, um administrador da instância do {{site.data.keyword.mon_full_notm}} ou ter permissões do IAM de conta para conceder outras políticas de usuários.

A tabela a seguir lista as políticas mínimas que um usuário deve ter para ser capaz de ativar a IU da web do {{site.data.keyword.mon_full_notm}} e visualizar dados:

| Serviço                        | Função                      | Permissão concedida     |
|--------------------------------|---------------------------|------------------------|
| `{{site.data.keyword.mon_full_notm}}` | Função de plataforma: visualizador     | Permite que o usuário visualize a lista de instâncias de serviço no painel Monitoramento de observação. |
| `{{site.data.keyword.mon_full_notm}}` | Função de serviço: gravador      | Permite que o usuário ative a IU da web e visualize as métricas na IU da web.  |
{: caption="Tabela 1. Políticas do IAM" caption-side="top"} 

Para obter mais informações sobre como configurar essas políticas para um usuário, consulte [Concedendo permissões a um usuário para visualizar métricas](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-iam_work#user_sysdig).


## Ative a IU da web por meio da IU do {{site.data.keyword.cloud_notm}}
{: #launch_step2}

Você ativa a IU da web dentro do contexto de uma instância do {{site.data.keyword.mon_full_notm}} por meio da IU do {{site.data.keyword.cloud_notm}}. 

Conclua as etapas a seguir para ativar a IU da web:

1. Efetue login em sua conta do {{site.data.keyword.cloud_notm}}.

    Clique em [Painel do {{site.data.keyword.cloud_notm}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/login){:new_window} para ativar o painel do {{site.data.keyword.cloud_notm}}.

	Depois que você efetua login com seu ID do usuário e senha, o Painel do {{site.data.keyword.cloud_notm}} é aberto.

2. No menu de navegação, selecione **Observabilidade**. 

3. Selecione **Monitorando**. 

    A lista de instâncias disponíveis no {{site.data.keyword.cloud_notm}} é exibida.

4. Selecione uma instância. Em seguida, clique em **Visualizar Sysdig**.

A IU da web é aberta.


