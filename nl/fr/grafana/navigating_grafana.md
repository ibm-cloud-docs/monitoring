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


# Accès au tableau de bord Grafana
{:#navigating_grafana}

Dans {{site.data.keyword.Bluemix}}, vous pouvez utiliser Grafana, plateforme de visualisation et d'analyse open source, pour surveiller, rechercher, analyser et visualiser vos métriques dans différents graphiques, par exemple, dans des diagrammes et des tableaux. Vous pouvez utiliser Grafana pour effectuer des tâches analytiques avancées.
{:shortdesc}

Vous pouvez démarrer Grafana de l'une des manières suivantes :

* Depuis {{site.data.keyword.Bluemix_notm}}

    Vous pouvez accéder dans Grafana à vos métriques de conteneur spécifiques à Docker, dans le contexte du conteneur concerné. Cette fonctionnalité ne s'applique qu'aux conteneurs déployés dans l'infrastructure gérée par {{site.data.keyword.Bluemix_notm}}. 
    
    Pour plus d'informations, voir [Accès au tableau de bord Grafana depuis le tableau de bord {{site.data.keyword.Bluemix_notm}}
    ](/docs/services/cloud-monitoring/grafana?topic=cloud-monitoring-navigating_grafana#launch_grafana_from_bluemix).

* A partir d'un lien de navigateur direct

    Vous pouvez démarrer Grafana afin que les données affichées agrègent les journaux des services dans l'espace {{site.data.keyword.Bluemix_notm}} désigné.
    
    Pour plus d'informations, voir [Accès au tableau de bord Grafana depuis un navigateur Web](/docs/services/cloud-monitoring/grafana?topic=cloud-monitoring-navigating_grafana#launch_grafana_from_browser).
    
Pour plus d'informations sur Grafana, reportez-vous au manuel [Grafana User Guide ![Icône de lien externe](../../../icons/launch-glyph.svg "Icône de lien externe")](http://docs.grafana.org/guides/getting_started/){: new_window}.


##  Accès au tableau de bord Grafana depuis le tableau de bord IBM Cloud
{: #launch_grafana_from_bluemix}

**Remarque :** cette fonctionnalité ne s'applique qu'aux conteneurs déployés dans l'infrastructure gérée par {{site.data.keyword.Bluemix_notm}}. 

La requête utilisée pour filtrer les données affichées dans Grafana extrait les données pour le conteneur {{site.data.keyword.Bluemix_notm}} depuis lequel vous démarrez Kibana. 

Pour examiner les métriques d'un conteneur Docker dans Grafana, procédez comme suit :

1. Connectez-vous à {{site.data.keyword.Bluemix_notm}}, puis cliquez sur le conteneur à partir du *tableau de bord*. 
    
2. Dans la barre de navigation, cliquez sur **Surveillance et journaux**. L'onglet Surveillance s'ouvre. 
    
3. Cliquez sur **Vue avancée**. Le tableau de bord **Grafana** s'ouvre.


##  Accès au tableau de bord Grafana depuis un navigateur Web
{: #launch_grafana_from_browser}

La requête utilisée pour filtrer les données affichées dans Grafana extrait les données relatives à un espace dans l'organisation {{site.data.keyword.Bluemix_notm}}. Les informations de métriques affichées par Grafana couvrent les enregistrements pour toutes les ressources déployées dans l'espace de l'organisation {{site.data.keyword.Bluemix_notm}} à laquelle vous êtes connecté.

Pour démarrer Grafana depuis un navigateur, procédez comme suit :

1. Ouvrez un navigateur web. 
2. Entrez l'adresse URL de la région dans laquelle vous voulez surveiller des métriques. 

    Le tableau suivant répertorie les adresses URL par région :
	<table>
      <caption>Adresses URL de démarrage de Grafana dans différentes régions</caption>
      <tr>
        <th>Région</th>
	    <th>Noeud final</th>
      </tr>
      <tr>
        <td>Allemagne</td>
	    <td>[https://metrics.eu-de.bluemix.net](https://metrics.eu-de.bluemix.net)</td>
      </tr>
      <tr>
        <td>Royaume-Uni</td>
	    <td>[https://metrics.eu-gb.bluemix.net](https://metrics.eu-gb.bluemix.net)</td>
      </tr>
      <tr>
        <td>Sud des Etats-Unis</td>
    	<td>[https://metrics.ng.bluemix.net](https://metrics.ng.bluemix.net)</td>
      </tr>
      <tr>
        <td>Royaume-Uni</td>
	    <td>[https://metrics.au-syd.bluemix.net](https://metrics.au-syd.bluemix.net)</td>
      </tr>
      
    </table>
	
2. Sélectionnez **Grafana**.
     

