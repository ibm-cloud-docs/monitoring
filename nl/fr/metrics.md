---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, metrics

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

# Utilisation des métriques
{: #metrics}

Après la mise à disposition d'une instance du service {{site.data.keyword.mon_full_notm}} dans {{site.data.keyword.Bluemix}} et la configuration d'un agent Sysdig pour une source de métriques, vous pouvez afficher, surveiller et gérer des métriques via l'interface utilisateur Web {{site.data.keyword.mon_full_notm}}. Utilisez des métriques pour analyser statistiquement des données comportant des valeurs numériques. 
{:shortdesc}


**Une métrique est une mesure quantitative comportant un ou plusieurs libellés pour définir ses caractéristiques.**

Une métrique est représentée par une série temporelle. 

Une série temporelle est un ensemble de points de données numériques sur une période de temps. 

Les métriques sont classées en deux groupes : 

* Métriques par défaut 
* Métriques personnalisées


## Libellés
{: #metrics_labels}

**Les libellés définissent les caractéristiques d'une métrique.**

Les libellés sont classés en tant que libellés d'infrastructure et libellés de descripteur de métrique. Chaque métrique possède un ensemble de libellés prédéfinis. Pour les métriques personnalisées, vous pouvez configurer davantage de libellés. 

Vous pouvez utiliser des libellés pour identifier et différencier les caractéristique d'une métrique, par exemple,
* Vous pouvez regrouper des objets d'infrastructure en hiérarchies logiques. 
* Vous pouvez filtrer des données. 
* Vous pouvez fractionner des données agrégées en segments. 


## Métriques par défaut 
{: #metrics_default}

**Les métriques par défaut génèrent des rapports sur le système, l'orchestrateur et l'infrastructure réseau.**

Le service de surveillance ajoute automatiquement des libellés à chaque métrique.


## Métriques personnalisées
{: #metrics_custom}

**Les métriques personnalisées varient en fonction du type d'infrastructure et des applications que vous surveillez. Par exemple, JMX, Prometheus et StatsD.**

Ces métriques possèdent un ensemble de libellés prédéfinis. Vous pouvez ajouter des libellés personnalisés supplémentaires.

Le service de surveillance conserve un index de tous les libellés et métriques personnalisés qui ont généré des données de rapport au cours des 14 derniers jours. Vous pouvez utiliser ces métriques pour configurer des tableaux de bord, des portées et des alertes.

Prenez en compte les informations suivantes sur la gestion des entrées d'index par le service de surveillance :
*  Une métrique est automatiquement supprimée de l'index du service de surveillance et marquée comme manquante lorsque l'une des conditions suivantes se produit :
    
    * Le service de surveillance ne reçoit pas de données pour une métrique ou un libellé pendant plus de 14 jours.
    
    * Une métrique ou un libellé n'a jamais généré de données de rapport.

* Vous ne pouvez pas configurer de nouveaux artefacts avec une métrique ou un libellé manquant. 
* Vous ne pouvez pas mettre à jour des artefacts existants tant que les métriques et les libellés manquants ne sont pas supprimés de la configuration en cours.
* Vous pouvez utiliser une métrique ou un libellé manquant sur des requêtes de données et graphiques. 
* Les artefacts existants ne sont pas affectés s'ils incluent une métrique ou un libellé manquant.
* Lorsque des données sont reçues pour une métrique ou un libellé manquant, la métrique ou le libellé est de nouveau ajouté à l'index.



