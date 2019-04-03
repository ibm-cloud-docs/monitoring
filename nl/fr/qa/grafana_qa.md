---

copyright:
  years: 2017, 2019

lastupdated: "2019-03-06"

keywords: IBM Cloud, monitoring

subcollection: cloud-monitoring

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



# Foire aux questions liées à l'utilisation de Grafana
{: #grafana_qa}

Vous trouverez ci-après les réponses aux questions fréquentes concernant l'utilisation de Grafana avec le service {{site.data.keyword.monitoringshort}}. 
{:shortdesc}

* [Les alertes que j'ai définies à l'aide de l'API Alerts n'apparaissent pas dans mon tableau de bord Grafana](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-grafana_qa#alerts1)
* [Un message BXNMSAL41E s'affiche lorsque j'essaie de sauvegarder une modification que j'ai apportée à mon tableau de bord Grafana](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-grafana_qa#BXNMSAL41E)
* [Un message BXNMSAL36E s'affiche lorsque j'essaie de sauvegarder une modification après que j'ai ajouté une alerte à mon tableau de bord Grafana](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-grafana_qa#BXNMSAL36E)
* [Un message d'erreur 404 s'affiche lorsque je me connecte à l'interface utilisateur Web du service Monitoring](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-grafana_qa#404)
* [J'ai téléchargé des données json pour un tableau de bord Grafana ; pourquoi ai-je perdu ma barre de défilement ?](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-grafana_qa#2)


## Les alertes que j'ai définies à l'aide de l'API Alerts n'apparaissent pas dans mon tableau de bord Grafana
{: #alerts1}

Les alertes que vous définissez à l'aide de l'API Alerts n'apparaissent pas dans le tableau de bord Grafana. Pour voir des alertes dans Grafana, vous devez les définir directement dans un tableau de bord Grafana.

Pour plus d'informations, voir [Configuration d'alertes dans Grafana](/docs/services/cloud-monitoring/alerts?topic=cloud-monitoring-config_alerts_grafana#config_alerts_grafana).

## Un message BXNMSAL41E s'affiche lorsque j'essaie de sauvegarder une modification que j'ai apportée à mon tableau de bord Grafana
{: #BXNMSAL41E}

Vous pouvez définir des canaux et des alertes de notification dans Grafana. Si vous supprimez un canal de notification dans Grafana et que vous ne mettez pas à jour la règle de suppression de ce canal de notification, vous obtenez un message d'erreur **BXNMSAL41E** lorsque vous essayez de sauvegarder votre tableau de bord Grafana.

Pour résoudre le problème, mettez à jour la règle en utilisant l'API Alerts et faites une nouvelle tentative de sauvegarde du tableau de bord. Lorsque vous mettez à jour la règle, retirez le canal de notification qui a été supprimé.

Pour plus d'informations, voir [API Alerts](https://console.bluemix.net/apidocs/940-ibm-cloud-monitoring-alerts-api?&language=node#introduction).

## Un message BXNMSAL36E s'affiche lorsque j'essaie de sauvegarder une modification après que j'ai ajouté une alerte à mon tableau de bord Grafana
{: #BXNMSAL36E}

Si vous atteignez le quota du domaine où vous surveillez des métriques dans le service {{site.data.keyword.monitoringshort}}, le message d'erreur suivant s'affiche : **BXNMSAL36E**

Mettez à niveau votre plan, puis faites une nouvelle tentative.

Pour plus d'informations sur la mise à jour de votre plan, voir [Modification du plan](/docs/services/cloud-monitoring/plan?topic=cloud-monitoring-change_plan#change_plan).


## Un message d'erreur 404 s'affiche lorsque je me connecte à l'interface utilisateur Web du service Monitoring
{: #404}

Si vous obtenez une erreur 404 lorsque vous tentez de vous connecter à l'interface utilisateur Web du service {{site.data.keyword.monitoringshort}} (Grafana), vérifiez que l'espace existe et que vous y avez accès.

Lorsque vous utilisez le [modèle d'authentification UAA](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_uaa#auth_uaa) pour accéder au service {{site.data.keyword.monitoringshort}}, vous devez vous servir de l'ID utilisateur et du mot de passe que vous avez utilisés pour vous connecter à la console {{site.data.keyword.Bluemix_notm}}. 

Pour vérifier que vous avez accès au compte, à l'organisation et à l'espace auxquels vous voulez vous connecter, connectez-vous à la console {{site.data.keyword.Bluemix_notm}} et accédez à l'espace. 

Vous pouvez aussi utiliser la ligne de commande pour vérifier que vous avez accès à cet espace. Exécutez la commande suivante pour vous connecter à une région, une organisation et un espace dans {{site.data.keyword.Bluemix_notm}} :

```
ibmcloud login -a https://api.ng.bluemix.net
```
{: codeblock}

Suivez les instructions. Entrez vos données d'identification {{site.data.keyword.Bluemix_notm}} et sélectionnez une organisation et un espace.


## Je viens de télécharger des données JSON pour un tableau de bord Grafana ; pourquoi ai-je perdu ma barre de défilement ?
{: #2}

Un bogue dans Grafana masque la barre de défilement après l'importation d'un tableau de bord. 

Pour afficher la barre de défilement, sauvegardez le tableau de bord après l'avoir importé. 








