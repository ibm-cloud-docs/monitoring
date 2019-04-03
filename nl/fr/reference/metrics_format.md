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


# Format général
{: #metrics_format}

Les requêtes que vous définissez dans Grafana pour surveiller un service {{site.data.keyword.Bluemix}} doivent être conformes au format suivant : 
{:shortdesc}

```
{Source}.{Cloud Type}.{Service Name}.{Region}.[service fields].{Metric type}.{Metric Subtype}.[Functions]
```
{: codeblock}

où [service fields] représentent les zones spécifiques de la requête de métrique d'un service ou d'une application CF. 

<table>
  <caption>Zones communes dans une requête</caption>
  <tr>
    <th>Zone</th>
	<th>Description</th>
	<th>Valeur</th>
  </tr>
  <tr>
    <td>Source</td>
	<td>Nom réservé. Les métriques sous cette hiérarchie proviennent des services {{site.data.keyword.Bluemix_notm}}.</td>
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
	  <td>Pour {{site.data.keyword.containershort}}, la valeur est *containers-kubernetes*</td>
  </tr>
  <tr>
    <td>Region</td>
	  <td>Définit la région dans laquelle le conteneur s'exécute.</td>
	  <td>Pour la région Sud des Etats-Unis, la valeur est *us-south* <br>Pour la région Royaume-Uni, la valeur est *united-kingdom*  <br>Pour l'Allemagne, la valeur est *frankfurt* <br>Pour Sydney, la valeur est *sydney* </td>
  </tr>
  <tr>
    <td>Metric Type</td>
	<td>Type de métrique.</td>
	<td>*cpu* <br>*load* <br>*memory*</td>
  </tr>
  <tr>
    <td>Metric Subtype</td>
	<td>Sous-type de la métrique.</td>
	<td>Par exemple : *usage*, *num-cores*, *usage-pct*, *usage-pct-container-requested*</td>
  </tr>
  <tr>
    <td>Functions</td>
    <td>Fonctions de requête que vous pouvez sélectionner pour visualiser une métrique de conteneur dans le panneau. </td>
    <td>[Fonctions ![(Icône de lien externe)](../../../icons/launch-glyph.svg "Icône de lien externe")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
   </tr>
</table>




