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


# {{site.data.keyword.containershort_notm}}
{: #metrics_format_containers}

Les requêtes que vous définissez dans Grafana pour surveiller un service {{site.data.keyword.containershort_notm}} doivent être conformes au format suivant : 
{:shortdesc}



## Format de requête des métriques d'unité centrale collectées pour les conteneurs
{: #cpu_containers}

Le format d'une requête que vous définissez dans Grafana dans le but de surveiller une métrique d'unité centrale pour un conteneur qui s'exécute dans le service {{site.data.keyword.containershort_notm}} est décrit comme suit : 

```
{Source}.{Cloud Type}.{Service Name}.{Region}.{Cluster Name}.{Namespace}.{Metric Source}.{Pod Name}.{Container Name}.{Metric Type}.{Metric Subtype}.[Functions]
```
{: codeblock}  

où

<table>
  <caption>Zones requises afin de définir une métrique d'unité centrale pour un conteneur </caption>
  <tr>
    <th>Zone</th>
	  <th>Description</th>
	  <th>Valeur</th>
  </tr>
  <tr>
    <td>Source</td>
	  <td>Nom réservé. Les métriques sous cette hiérarchie proviennent des applications et des services {{site.data.keyword.Bluemix_notm}}.</td>
	  <td>*ibmcloud*</td>
  </tr>
  <tr>
    <td>Cloud Type</td>
	  <td>Indique le type de cloud. </td>
	  <td>Pour le cloud public {{site.data.keyword.Bluemix_notm}}, la valeur est *public*</td>
  </tr>
  <tr>
    <td>Service Name</td>
	  <td>Définit le nom du service dans {{site.data.keyword.Bluemix_notm}}.</td>
	  <td>Pour les applications CF, la valeur est *cloud-foundry*</td>
  </tr>
  <tr>
    <td>Region</td>
	  <td>Définit la région dans laquelle le conteneur s'exécute.</td>
	  <td>Pour la région Sud des Etats-Unis, la valeur est *us-south* <br>Pour la région Royaume-Uni, la valeur est *united-kingdom*  <br>Pour l'Allemagne, la valeur est *frankfurt* <br>Pour Sydney, la valeur est *sydney* </td>
  </tr>
  <tr>
    <td>Cluster Name</td>
	  <td>Nom du cluster à surveiller.</td>
	  <td></td>
  </tr>
  <tr>
    <td>Metric Source</td>
	  <td>Source des données.</td>
	  <td>*container* </td>
  </tr>
  <tr>
    <td>Namespace</td>
	<td>Espace de noms où le conteneur est déployé dans un cluster Kubernetes.</td>
	<td></td>
  </tr>
   <tr>
    <td>Pod Name</td>
	<td>Nom du pod.</td>
	<td></td>
  </tr>
  <tr>
    <td>Container Name</td>
	<td>Nom du conteneur.</td>
	<td></td>
  </tr>
  <tr>
    <td>Metric Type</td>
	  <td>Type de métrique.</td>
	  <td>*UC*</td>
  </tr>
  <tr>
    <td>Metric Subtype</td>
	  <td>Métrique à afficher.</td>
	  <td>*usage*, *num-cores*, *usage-pct*, *usage-pct-container-requested*</td>
  </tr>
  <tr>
    <td>Functions</td>
    <td>Fonctions de requête que vous pouvez sélectionner pour visualiser une métrique de conteneur dans le panneau. </td>
    <td>[Fonctions ![(Icône de lien externe)](../../../icons/launch-glyph.svg "Icône de lien externe")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
   </tr>
</table>

Par exemple, une requête visant à surveiller l'utilisation de l'unité centrale pour un conteneur qui s'exécute dans un cluster Kubernetes dans la région Sud des Etats-Unis est définie comme suit :

```
ibmcloud.public.containers-kubernetes.us-south.myCluster.container.default.myPod.myContainer-1775968925-kfwfk.cpu.usage
```
{: screen}



## Format de requête des métriques de charge collectées pour les agents
{: #load_workers}

Le format d'une requête que vous définissez dans Grafana dans le but de surveiller une métrique de charge pour un agent qui s'exécute dans le service {{site.data.keyword.containershort_notm}} est décrit comme suit : 

```
{Source}.{Cloud Type}.{Service Name}.{Region}.{Cluster Name}.{Metric Source}.{Worker Name}.{Metric Type}.{Metric Subtype}.[Functions]
```
{: codeblock}  

où

<table>
  <caption>Zones requises afin de définir une métrique de charge pour un agent </caption>
  <tr>
    <th>Zone</th>
	<th>Description</th>
	<th>Valeur</th>
  </tr>
  <tr>
    <td>Source</td>
	  <td>Nom réservé. Les métriques sous cette hiérarchie proviennent des applications et des services {{site.data.keyword.Bluemix_notm}}.</td>
	  <td>*ibmcloud*</td>
  </tr>
  <tr>
    <td>Cloud Type</td>
	  <td>Indique le type de cloud. </td>
	  <td>Pour le cloud public {{site.data.keyword.Bluemix_notm}}, la valeur est *public*</td>
  </tr>
  <tr>
    <td>Service Name</td>
	  <td>Définit le nom du service dans {{site.data.keyword.Bluemix_notm}}.</td>
	  <td>Pour les applications CF, la valeur est *cloud-foundry*</td>
  </tr>
  <tr>
    <td>Region</td>
	  <td>Définit la région dans laquelle le conteneur s'exécute.</td>
	  <td>Pour la région Sud des Etats-Unis, la valeur est *us-south* <br>Pour la région Royaume-Uni, la valeur est *united-kingdom*  <br>Pour l'Allemagne, la valeur est *frankfurt* <br>Pour Sydney, la valeur est *sydney* </td>
  </tr>
  <tr>
    <td>Cluster Name</td>
	<td>Nom du cluster à surveiller.</td>
	<td></td>
  </tr>
  <tr>
    <td>Metric Source</td>
	<td>Source des données.</td>
	<td>*worker* </td>
  </tr>
   <tr>
    <td>Worker Name</td>
	<td>Nom de l'agent.</td>
	<td></td>
  </tr>
  <tr>
    <td>Metric Type</td>
	<td>Type de métrique.</td>
	<td>*load*</td>
  </tr>
  <tr>
    <td>Metric Subtype</td>
	  <td>Métrique à afficher.</td>
	  <td>*avg-1*, *avg-5*, *avg-15*</td>
  </tr>
  <tr>
    <td>Functions</td>
    <td>Fonctions de requête que vous pouvez sélectionner pour visualiser une métrique de conteneur dans le panneau. </td>
    <td>[Fonctions ![(Icône de lien externe)](../../../icons/launch-glyph.svg "Icône de lien externe")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
   </tr>
</table>

Par exemple, une requête visant à surveiller l'utilisation de l'unité centrale pour un agent qui s'exécute dans un cluster Kubernetes dans la région Sud des Etats-Unis est définie comme suit :

```
ibmcloud.public.containers-kubernetes.us-south.myCluster.worker.MyWorker.load.avg-1
```
{: screen}


## Format de requête des métriques de mémoire collectées pour les conteneurs
{: #mem_containers}

Le format d'une requête que vous définissez dans Grafana dans le but de surveiller une métrique de mémoire pour un conteneur qui s'exécute dans le service {{site.data.keyword.containershort_notm}} est décrit comme suit : 

```
{Source}.{Cloud Type}.{Service Name}.{Region}.{Cluster Name}.{Namespace}.{Metric Source}.{Pod Name}.{Container Name}.{Metric Type}.{Metric Subtype}.[Functions]
```
{: codeblock}  

où

<table>
  <caption>Zones requises afin de définir une métrique de mémoire pour un conteneur</caption>
  <tr>
    <th>Zone</th>
	<th>Description</th>
	<th>Valeur</th>
  </tr>
  <tr>
    <td>Source</td>
	  <td>Nom réservé. Les métriques sous cette hiérarchie proviennent des applications et des services {{site.data.keyword.Bluemix_notm}}.</td>
	  <td>*ibmcloud*</td>
  </tr>
  <tr>
    <td>Cloud Type</td>
	  <td>Indique le type de cloud. </td>
	  <td>Pour le cloud public {{site.data.keyword.Bluemix_notm}}, la valeur est *public*</td>
  </tr>
  <tr>
    <td>Service Name</td>
	  <td>Définit le nom du service dans {{site.data.keyword.Bluemix_notm}}.</td>
	  <td>Pour les applications CF, la valeur est *cloud-foundry*</td>
  </tr>
  <tr>
    <td>Region</td>
	  <td>Définit la région dans laquelle le conteneur s'exécute.</td>
	  <td>Pour la région Sud des Etats-Unis, la valeur est *us-south* <br>Pour la région Royaume-Uni, la valeur est *united-kingdom*  <br>Pour l'Allemagne, la valeur est *frankfurt* <br>Pour Sydney, la valeur est *sydney* </td>
  </tr>
  <tr>
    <td>Cluster Name</td>
	<td>Nom du cluster à surveiller.</td>
	<td></td>
  </tr>
  <tr>
    <td>Metric Source</td>
	<td>Source des données.</td>
	<td>*container* </td>
  </tr>
  <tr>
    <td>Namespace</td>
	<td>Espace de noms où le conteneur est déployé dans un cluster Kubernetes.</td>
	<td></td>
  </tr>
   <tr>
    <td>Pod Name</td>
	<td>Nom du pod.</td>
	<td></td>
  </tr>
  <tr>
    <td>Container Name</td>
	  <td>Nom du conteneur.</td>
	  <td></td>
  </tr>
  <tr>
    <td>Metric Type</td>
  	<td>Type de métrique.</td>
  	<td>*memory*</td>
  </tr>
  <tr>
    <td>Metric Subtype</td>
	  <td>Métrique à afficher.</td>
	  <td>*limit*, *current*, *usage-pct*</td>
  </tr>
  <tr>
    <td>Functions</td>
    <td>Fonctions de requête que vous pouvez sélectionner pour visualiser une métrique de conteneur dans le panneau. </td>
    <td>[Fonctions ![(Icône de lien externe)](../../../icons/launch-glyph.svg "Icône de lien externe")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
   </tr>
</table>

Par exemple, une requête visant à surveiller l'utilisation de la mémoire pour un conteneur qui s'exécute dans un cluster Kubernetes dans la région Sud des Etats-Unis est définie comme suit :

```
ibmcloud.public.containers-kubernetes.us-south.myCluster.container.default.myPod.myContainer-1775968925-kfwfk.memory.usage
```
{: screen}
