---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, notification channel

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


# Trabalhando com canais de notificação
{: #notifications}

Configure os canais de notificação para ser notificado quando um alerta for acionado. Você gerencia canais de notificação por meio do painel *Configurações* na IU da web.
{:shortdesc}
 

## Configurando um canal de notificação
{: #notifications_create}

Conclua as etapas a seguir para incluir um canal de notificação:

1. Ative a IU da web. Para obter mais informações sobre como ativar a IU da web, consulte [Navegando para a IU da web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. No botão *Seletor* na barra de navegação, escolha **Configurações**.

3. Selecione **Canais de notificação**.

4. Clique em  ** MY CHANNELS **  ![add icon](../images/add.png). Em seguida, selecione um canal.

    **Nota:** na primeira vez que você configurar um canal de notificação, clique em qualquer um dos canais.

5. Configure um canal de notificação:

    * Insira o nome do canal.

    * Ative o campo *Notificar quando OK* para receber uma notificação quando a condição de alerta não for mais acionada.

    * Ative a condição *Notificar quando resolvido* para receber uma notificação quando o alerta for resolvido manualmente por um usuário.

    * Para um canal de notificação **e-mail**, inclua a lista de destinatários, separados por vírgula.

    * Para um canal de notificação **slack**, inclua o nome do *canal Slack*.

    * Para um canal de notificação **Webhook**, inclua a *URL do webhook*. **Nota:** quando um alerta é acionado, a notificação é enviada como um POST no formato JSON para seu terminal de webhook. Para obter mais informações, consulte [Configurando um canal Webhook ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://sysdigdocs.atlassian.net/wiki/spaces/Platform/pages/242843679/Configure+a+Webhook+Channel){:new_window}. Por exemplo, o Sysdig pode ser integrado ao ServiceNow usando um webhook customizado. Para saber sobre como configurar o Sysdig com o ServiceNow, consulte [Configurar o ServiceNow ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://sysdigdocs.atlassian.net/wiki/spaces/Platform/pages/242942035/Configure+ServiceNow){:new_window}.

    * Para um canal de notificação **VictorOps**, inclua a *chave de API* e a *Chave de roteamento*.

    * Para um canal de notificação **OpsGenie**, inclua a *chave de API do OpsGenie*. Observe que se deve configurar no OpsGenie a integração com o Sysdig. Para obter mais informações, consulte [Incluir a integração do Sysdig Cloud no Opsgenie ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://docs.opsgenie.com/v1.0/docs/sysdig-cloud-integration){:new_window}.

    * Para um canal de notificação **PagerDuty**, deve-se primeiro autorizar o Sysdig a integrar-se com sua conta. Quando você seleciona PagerDuty, um assistente para configurar a integração com o Sysdig é aberto. Clique em **Autorizar integração** ou **Conectar-se usando o seu provedor de identidade** para autorizar o PagerDuty. Escolha um serviço existente ou configure um novo serviço para notificações do Sysdig e, em seguida, clique em **Concluir integração**. Selecione a política de escalada a ser usada para incidentes do Sysdig. Em seguida, na guia *Notificações*, confirme sua conta do PagerDuty, seu nome do serviço e a chave de serviço. 

    * Opcionalmente, e para integrações que permitem um teste, ative a condição *Notificação de teste* para receber uma notificação de teste. Se você não receber uma notificação de teste em 10 minutos, revise sua configuração de canal. 

6. Clique em  ** CREATE CHANNEL **. 



## Modificando um canal de notificação
{: #notifications_update}

Conclua as etapas a seguir para modificar um canal de notificação:

1. Ative a IU da web. Para obter mais informações sobre como ativar a IU da web, consulte [Navegando para a IU da web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. No botão *Seletor* na barra de navegação, escolha **Configurações**.

3. Selecione **Canais de notificação**.

4. Identifique o canal de destino que deseja modificar e clique em **EDITAR**.

5. Depois de fazer mudanças, clique em **SALVAR MUDANÇAS**.



## Testando um canal de notificação
{: #notifications_test}

Conclua as etapas a seguir para testar um canal de notificação:

1. Ative a IU da web. Para obter mais informações sobre como ativar a IU da web, consulte [Navegando para a IU da web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. No botão *Seletor* na barra de navegação, escolha **Configurações**.

3. Selecione **Canais de notificação**.

4. Identifique o canal de destino que você deseja modificar e clique em **TESTE**.



## Desativando um canal de notificação
{: #notifications_disable}

Conclua as etapas a seguir para desativar temporariamente um canal de notificação:

1. Ative a IU da web. Para obter mais informações sobre como ativar a IU da web, consulte [Navegando para a IU da web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. No botão *Seletor* na barra de navegação, escolha **Configurações**.

3. Selecione **Canais de notificação**.

4. Na seção *Notificações*, ative *Tempo de inatividade* para desativar os alertas temporariamente e silenciar todas as notificações.

## Excluindo um canal de notificação
{: #notifications_delete}

Conclua as etapas a seguir para excluir um canal de notificação:

1. Ative a IU da web. Para obter mais informações sobre como ativar a IU da web, consulte [Navegando para a IU da web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. No botão *Seletor* na barra de navegação, escolha **Configurações**.

3. Selecione **Canais de notificação**.

4. Identifique o canal de destino que deseja modificar e clique em **EDITAR**.

5. Clique em  ** DELETE CHANNEL **.

6. Confirme a exclusão do canal. Clique em  ** SAVE CHANGES **.




