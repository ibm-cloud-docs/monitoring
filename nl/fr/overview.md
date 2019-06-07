---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, overview

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


# {{site.data.keyword.mon_full_notm}}
{: #about}

{{site.data.keyword.mon_full}} est un système de gestion d'intelligence de conteneur, tiers et natif pour le cloud, que vous pouvez inclure dans votre architecture
{{site.data.keyword.cloud_notm}}. Il vous permet d'obtenir une visibilité opérationnelle des performances et de la santé de vos applications, services et plateformes. Il propose aux administrateurs, aux équipes DevOps et aux développeurs une télémétrie pour pile complète et des fonctions avancées permettant de surveiller et de traiter les incidents, de définir des alertes et de concevoir des tableaux de bord personnalisés. {{site.data.keyword.mon_full_notm}} est exploité par Sysdig en partenariat avec {{site.data.keyword.IBM_notm}}.
{:shortdesc}


Pour ajouter des fonctions de surveillance avec {{site.data.keyword.mon_full_notm}} dans {{site.data.keyword.cloud_notm}}, vous devez mettre à disposition une instance du service {{site.data.keyword.mon_full_notm}}.

Avant de mettre à disposition une instance, prenez en compte les informations suivantes :

* Vos données sont envoyées à un tiers.
* Le propriétaire du compte peut créer, visualiser et supprimer une instance d'un service dans {{site.data.keyword.cloud_notm}}. Cet utilisateur peut également autoriser d'autres utilisateurs à utiliser le service {{site.data.keyword.mon_full_notm}}.
* Les autres utilisateurs {{site.data.keyword.cloud_notm}} dotés de droits `administrateur` ou `éditeur`
peuvent gérer le service {{site.data.keyword.mon_full_notm}} dans {{site.data.keyword.cloud_notm}}. Ces utilisateurs doivent également disposer
de droits de plateforme pour créer des ressources dans le cadre du groupe de ressources où ils prévoient de mettre à disposition l'instance.

Vous pouvez mettre à disposition une instance dans le cadre d'un groupe de ressources. Vous pouvez utiliser un groupe de ressources afin d'organiser vos services à des fins de contrôle d'accès et de facturation. Vous pouvez mettre à disposition l'instance {{site.data.keyword.mon_full_notm}} dans le groupe de ressources *par défaut* ou dans un groupe de ressources personnalisé.

Lorsque vous [mettez à disposition une instance](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-provision#provision), vous obtenez automatiquement une clé d'ingestion, appelée [clé d'accès Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-access_key#access_key).

Après la mise à disposition d'une instance, vous devez configurer un agent {{site.data.keyword.mon_full_notm}} pour chaque source de métriques. Une source de métriques est une ressource de cloud dont vous souhaitez surveiller et contrôler les performances et la santé. Vous devez configurer un agent {{site.data.keyword.mon_full_notm}} dans chaque environnement à surveiller. Par exemple, il peut s'agir d'un cluster Kubernetes. Vous utilisez la clé d'accès pour configurer l'agent Sysdig qui est responsable de la collecte et de la transmission des données de métriques à votre instance.

Une fois que l'agent {{site.data.keyword.mon_full_notm}} est déployé dans une source de métriques, la collecte et la transmission des métriques à l'instance sont automatiques. L'agent {{site.data.keyword.mon_full_notm}} collecte automatiquement des métriques prédéfinies et génère des rapports les concernant. Vous pouvez configurer quelles métriques surveiller dans un environnement.

Vous pouvez [surveiller](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-monitoring#monitoring) et [gérer](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-manage#manage) des données via l'interface utilisateur
Web {{site.data.keyword.mon_full_notm}}.  

La figure suivante présente les composants du service {{site.data.keyword.mon_full_notm}} qui s'exécute sur {{site.data.keyword.cloud_notm}} :

![Présentation des composants {{site.data.keyword.mon_full_notm}} sur {{site.data.keyword.cloud_notm}}](images/components.png "Présentation des composants {{site.data.keyword.mon_full_notm}} sur {{site.data.keyword.cloud_notm}}")



## Collecte des données
{: #overview_collection}

Lorsque vous configurez un agent Sysdig pour collecter et transmettre des données à une instance {{site.data.keyword.mon_full_notm}}, elles sont automatiquement collectées et mises à disposition pour analyse via l'interface utilisateur Web.

Les données sont collectées à une fréquence de 10 secondes. 

## Disponibilité des données
{: #overview_availability}

Les données sont disponibles pendant 15 mois au maximum.

Après la suppression d'un agent Sysdig sur un hôte ou un conteneur, les données d'historique ne sont pas supprimées. Les données sont disponibles pour analyse via l'interface utilisateur Web pendant la période où l'agent était installé et générait des rapports.

Après la suppression d'une instance du service {{site.data.keyword.mon_full_notm}}, les données ne sont pas disponibles pour la recherche et l'analyse.



## Conservation des données
{: #overview_retention}

Les données sont conservées pour chaque instance selon une règle de *cumul*.

Au fur et à mesure, les données sont cumulées d'une granularité fine à une granularité plus grossière sur les 3 derniers mois.

La règle de cumul décrit la granularité des données au fil du temps :

* Les données sont conservées à une résolution de 10 secondes pendant les 6 premières heures.
* Les données sont conservées à une résolution d'une minute pendant 2 jours.
* Les données sont conservées à une résolution de 10 minutes pendant 2 semaines.
* Les données sont conservées à une résolution d'une heure pendant 3 mois.
* Les données sont conservées à une résolution d'un jour pendant un an.

## Suppression des données
{: #overview_data_deletion}

Lorsque vous supprimez une instance {{site.data.keyword.mon_full_notm}} d'{{site.data.keyword.cloud_notm}}, vous devez ouvrir un cas via le support pour demander la suppression des données. Pour plus d'informations, voir [Contacter le service de support](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-gettinghelp#gettinghelp).

Lorsque vous supprimez une capture, le fichier de données pour cette capture est automatiquement supprimé.

La suppression des données qui sont collectées à partir d'un agent Sysdig unique dans une instance {{site.data.keyword.mon_short}} n'est pas prise en charge.
{: note}



## Emplacement des données
{: #overview_data_location}

{{site.data.keyword.mon_full_notm}} collecte et agrège les métriques. 

* Les données de métriques sont hébergées sur {{site.data.keyword.cloud_notm}}.
* Chaque région multi-zone collecte et agrège des métriques pour chaque instance {{site.data.keyword.mon_full_notm}} qui s'exécute dans cet emplacement.
* Les données sont colocalisées dans la région où l'instance {{site.data.keyword.mon_full_notm}} est mise à disposition. Par exemple, les données de métriques pour une instance mise à disposition dans la région Sud des Etats-Unis sont hébergées dans cette région.



## Agents {{site.data.keyword.mon_full_notm}}
{: #overview_sysdig_agent}

L'agent {{site.data.keyword.mon_full_notm}} collecte automatiquement des métriques prédéfinies et génère des rapports les concernant. 

La liste suivante décrit les agents {{site.data.keyword.mon_full_notm}} disponibles :

* Agent {{site.data.keyword.mon_full_notm}} pour Kubernetes, GKE et OpenShift.
* Agent {{site.data.keyword.mon_full_notm}} pour des conteneurs Docker ou des services non conteneurisés.
* Agent {{site.data.keyword.mon_full_notm}} pour Mesos, Marathon et DCOS.
* Agent {{site.data.keyword.mon_full_notm}} pour les installations Linux manuelles.

Pour plus d'informations, voir [Configuration d'un agent Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-config_agent#config_agent) et [Suppression d'un agent Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-remove#remove).


## Affichage de l'utilisation
{: #overview_usage}

Pour surveiller l'utilisation et les coûts de votre service, voir [Affichage de votre utilisation](/docs/billing-usage/viewing_usage.html#viewingusage).


## Plans de service
{: #overview_plans}

Différents plans de tarification sont disponibles pour une instance {{site.data.keyword.mon_full_notm}}. [En savoir plus](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-pricing_plans#pricing_plans).


## Considérations relatives à la sécurité
{: #overview_security}

**Captures**

Une capture est un fichier de trace que vous pouvez générer pour analyser les événements qui se produisent sur un hôte pendant une période donnée. Les captures contiennent des appels système et d'autres événements de système d'exploitation. Vous pouvez activer ou désactiver cette fonction par noeud lorsque vous configurez l'agent Sysdig qui collecte des métriques à partir de ce noeud. Par défaut, les *captures* sont activées lorsque vous configurez un agent Sysdig. Un noeud peut être un hôte, un conteneur, une machine virtuelle, un serveur bare metal, ou une source de métriques sur laquelle vous installez un agent Sysdig.

Lorsque les captures sont activées, notez que Sysdig aura une visibilité complète de vos opérations. Pour éviter un incident de sécurité et éventuellement d'exposer des données à l'extérieur de votre organisation, vérifiez les règles de sécurité de votre organisation avant d'activer des captures sur un noeud. Pensez à désactiver la fonction *Capture* pour tous vos agents Sysdig.
{: important}

