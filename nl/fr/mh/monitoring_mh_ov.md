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



# {{site.data.keyword.messagehub}}
{: #monitoring_mh_ov}

Dans {{site.data.keyword.Bluemix}}, les métriques {{site.data.keyword.messagehub}} sont collectées automatiquement. Le nombre d'octets entrant et sortant d'une rubrique est indiqué. Un point de contrôle est effectué toutes les 15 minutes. Vous pouvez utiliser Grafana pour visualiser ces métriques. 
{:shortdesc}


**Remarque :** les métriques {{site.data.keyword.messagehub}} sont disponibles dans le plan {{site.data.keyword.messagehub}} Standard, uniquement dans le sud des Etats-Unis, le Royaume-Uni et Sydney. 




## Affichage et analyse des métriques
{: #view}

Pour surveiller les performances de {{site.data.keyword.messagehub}} dans {{site.data.keyword.Bluemix_notm}}, utilisez Grafana. {{site.data.keyword.messagehub}} fournit un tableau de bord que vous pouvez utiliser pour afficher et surveiller les performances de vos rubriques.

Le service {{site.data.keyword.monitoringlong}} utilise la plateforme de visualisation et d'analyse open source Grafana dont vous pouvez vous servir pour surveiller, rechercher, analyser et visualiser vos métriques dans différents graphiques, par exemple, dans des diagrammes et des tableaux. 

Vous pouvez démarrer Grafana de l'une des manières suivantes :

* Vous pouvez cliquer sur le bouton **Grafana** du tableau de bord {{site.data.keyword.messagehub}} dans la console {{site.data.keyword.Bluemix_notm}}.

    Grafana s'ouvre dans le contexte de l'espace {{site.data.keyword.Bluemix_notm}} où s'exécute {{site.data.keyword.messagehub}}.
    
* Vous pouvez lancer Grafana directement depuis un navigateur web.

    Assurez-vous de bien vous placer dans l'espace et l'organisation où s'exécute l'instance {{site.data.keyword.messagehub}}.
    
    Pour plus d'informations, voir [Accès au tableau de bord Grafana depuis un navigateur Web](/docs/services/cloud-monitoring/grafana?topic=cloud-monitoring-navigating_grafana#launch_grafana_from_browser).
    

Tenez compte des informations suivantes :

* Vous devez lancer Grafana dans la même région {{site.data.keyword.Bluemix_notm}} que celle dans laquelle l'instance {{site.data.keyword.messagehub}} s'exécute.
* Utilisez le tableau de bord Grafana fourni par défaut pour démarrer la surveillance de votre instance {{site.data.keyword.messagehub}}.
* Créez des tableaux de bord Grafana personnalisés afin de répondre à des besoins spécifiques. Vous pouvez définir une ou plusieurs requêtes de métrique dans un tableau de bord Grafana pour surveiller une instance {{site.data.keyword.messagehub}}. Pour plus d'informations, voir [Configuration d'une requête de métrique dans Grafana](/docs/services/cloud-monitoring/grafana?topic=cloud-monitoring-define_query#define_query).
* Vous pouvez également définir des alertes sur des requêtes. Pour plus d'informations, voir [Configuration d'alertes](/docs/services/cloud-monitoring?topic=cloud-monitoring-config_alerts_ov#config_alerts_ov).


## Métriques pour une rubrique Kafka
{: #kafka_topic_metrics}

Pour chaque rubrique Kafka qui est définie, les métriques suivantes sont collectées :


<table>
  <caption>Métriques par rubrique Kafka</caption>
  <tr>
    <th>Métrique</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>BytesInPerSec</td>
    <td>Nombre d'octets envoyés dans une rubrique par des applications client Kafka.</td>
  </tr>
  <tr>
    <td>BytesOutPerSec</td>
    <td>Nombre d'octets reçus depuis une rubrique par des applications client Kafka.</td>
  </tr>
</table>



## Métriques pour une partition Kafka
{: #kafka_partition_metrics}

Pour chaque partition Kafka disposant d'un pont Cloud Storage qui consomme des messages, les métriques suivantes sont collectées :


<table>
  <caption>Métriques de partition Kafka</caption>
  <tr>
    <th>Métrique</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>lastSeen</td>
    <td>Position du dernier enregistrement Kafka traité par le pont Cloud Storage.</td>
  </tr>
  <tr>
    <td>lastCommitted</td>
    <td>Position validée pour les enregistrements Kafka qui sont traités par le pont Cloud Storage.</td>
  </tr>
  <tr>
    <td>notParsedButProcessedMessages</td>
    <td>Nombre de messages qui sont reçus par une instance de pont Cloud Storage depuis une rubrique Kafka. Ne compte que les messages contenant des documents JSON valides qui ne peuvent pas être traités par le pont.</td>
  </tr>
  <tr>
    <td>notParsedIgnoredMessages</td>
    <td>Nombre de messages qui sont reçus par une instance de pont Cloud Storage depuis une rubrique Kafka. Ne compte que les messages contenant les données qui n'ont pas pu être analysées car les données ne se trouvaient pas dans un document JSON valide.</td>
  </tr>
</table>




## Références
{: #mhlinks}

* [Initiation à Message Hub](/docs/services/EventStreams?topic=eventstreams-getting_started#getting_started)
* [Surveillance et journalisation](/docs/services/EventStreams/messagehub072.html#monitoring)

