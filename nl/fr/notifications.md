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


# Utilisation des canaux de notification
{: #notifications}

Configurez les canaux de notification pour être averti lorsqu'une alerte est déclenchée. Vous pouvez gérer les canaux de notification via le panneau *Paramètres* dans l'interface utilisateur Web.
{:shortdesc}
 

## Configuration d'un canal de notification
{: #notifications_create}

Pour ajouter un canal de notification, procédez comme suit :

1. Lancez l'interface utilisateur Web. Pour plus d'informations sur le lancement de l'interface utilisateur Web,
voir [Accès à l'interface utilisateur Web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. A partir du bouton *Sélecteur* dans la barre de navigation, choisissez **Paramètres**.

3. Sélectionnez **Canaux de notification**.

4. Cliquez sur **MY CHANNELS** ![icône d'ajout](../images/add.png). Ensuite, sélectionnez un canal.

    **Remarque :** La première fois que vous configurez un canal de notification, cliquez sur n'importe lequel.

5. Configurez un canal de notification :

    * Saisissez le nom du canal.

    * Activez la zone *Notify when OK* pour recevoir une notification lorsque la condition d'alerte n'est plus déclenchée.

    * Activez la condition *Notify when Resolved* pour recevoir une notification lorsque l'alerte est résolue manuellement par un utilisateur.

    * Pour un canal de notification **Courrier électronique**, ajoutez la liste des destinataires, séparés par une virgule.

    * Pour un canal de notification **Slack**, ajoutez le nom du *Canal Slack*.

    * Pour un canal de notification **Webhook**, ajoutez l'*URL du webhook*. **Remarque :** Lorsqu'une alerte est déclenchée, la
notification est envoyée à votre noeud final webhook sous forme d'événement POST au format JSON. Pour plus d'informations, voir [Configure à Webhook Channel ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://sysdigdocs.atlassian.net/wiki/spaces/Platform/pages/242843679/Configure+a+Webhook+Channel){:new_window}. Par exemple,
Sysdig peut être intégré à ServiceNow à l'aide d'un webhook personnalisé. Pour en savoir plus sur la configuration de Sysdig avec ServiceNow, voir [Configure ServiceNow ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://sysdigdocs.atlassian.net/wiki/spaces/Platform/pages/242942035/Configure+ServiceNow){:new_window}.

    * Pour un canal de notification **VictorOps**, ajoutez la *clé d'API* et la *clé de routage*.

    * Pour un canal de notification **OpsGenie**, ajoutez la *clé d'API OpsGenie*. Notez que vous devez configurer l'intégration à Sysdig dans OpsGenie. Pour plus d'informations, voir [Add Sysdig Cloud Integration in Opsgenie ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://docs.opsgenie.com/v1.0/docs/sysdig-cloud-integration){:new_window}.

    * Pour un canal de notification **PagerDuty**, vous devez d'abord autoriser Sysdig à s'intégrer à votre compte. Lorsque vous sélectionnez PagerDuty, un assistant permettant de configurer l'intégration à Sysdig s'ouvre. Cliquez sur **Authorize Integration** ou **Sign In Using Your Identity Provider** pour autoriser PagerDuty. Choisissez un service existant ou configurez un nouveau service pour les notifications Sysdig, puis cliquez sur **Finish Integration**. Sélectionnez la règle d'escalade à utiliser pour les incidents Sysdig. Puis, sur l'onglet *Notifications*, confirmez votre compte PagerDuty, votre nom de service, ainsi que la clé de service. 

    * Activez éventuellement la condition *Test notification*, pour les intégrations qui autorisent un test, afin de recevoir une notification test. Si vous ne recevez pas de notification test au bout de 10 minutes, vérifiez votre configuration de canal. 

6. Cliquez sur **CREATE CHANNEL**. 



## Modification d'un canal de notification
{: #notifications_update}

Pour modifier un canal de notification, procédez comme suit :

1. Lancez l'interface utilisateur Web. Pour plus d'informations sur le lancement de l'interface utilisateur Web,
voir [Accès à l'interface utilisateur Web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. A partir du bouton *Sélecteur* dans la barre de navigation, choisissez **Paramètres**.

3. Sélectionnez **Canaux de notification**.

4. Identifiez le canal cible à modifier et cliquez sur **EDITER**.

5. Une fois les modifications effectuées, cliquez sur **ENREGISTRER LES MODIFICATIONS**.



## Test d'un canal de notification
{: #notifications_test}

Pour tester un canal de notification, procédez comme suit :

1. Lancez l'interface utilisateur Web. Pour plus d'informations sur le lancement de l'interface utilisateur Web,
voir [Accès à l'interface utilisateur Web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. A partir du bouton *Sélecteur* dans la barre de navigation, choisissez **Paramètres**.

3. Sélectionnez **Canaux de notification**.

4. Identifiez le canal cible à modifier et cliquez sur **TEST**.



## Désactivation d'un canal de notification
{: #notifications_disable}

Pour désactiver temporairement un canal de notification, procédez comme suit :

1. Lancez l'interface utilisateur Web. Pour plus d'informations sur le lancement de l'interface utilisateur Web,
voir [Accès à l'interface utilisateur Web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. A partir du bouton *Sélecteur* dans la barre de navigation, choisissez **Paramètres**.

3. Sélectionnez **Canaux de notification**.

4. Dans la section *Notifications*, activez *Downtime* pour désactiver temporairement les alertes et rendre silencieuses toutes les notifications.

## Suppression d'un canal de notification
{: #notifications_delete}

Pour supprimer un canal de notification, procédez comme suit :

1. Lancez l'interface utilisateur Web. Pour plus d'informations sur le lancement de l'interface utilisateur Web,
voir [Accès à l'interface utilisateur Web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
    
2. A partir du bouton *Sélecteur* dans la barre de navigation, choisissez **Paramètres**.

3. Sélectionnez **Canaux de notification**.

4. Identifiez le canal cible à modifier et cliquez sur **EDITER**.

5. Cliquez sur **SUPPRIMER LE CANAL**.

6. Confirmez la suppression du canal. Cliquez sur **ENREGISTRER LES MODIFICATIONS**.




