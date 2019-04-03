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


# Applications CF
{: #cfapps_metrics_format}

Les requêtes que vous définissez dans Grafana pour surveiller une application Cloud Foundry qui s'exécute dans l'environnement de cloud {{site.data.keyword.Bluemix}} public doivent être conformes au format suivant : 
{:shortdesc}

```
{Source}.{Cloud Type}.{Service Name}.{Region}.{CFapp Name}.{CFapp Index}.{CFapp container}.{Metric Type}.{Metric Subtype}.[Functions]
```
{: codeblock}

où

<table>
  <caption>Zones communes dans une requête</caption>
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
	<td>Définit la région dans laquelle l'instance d'application CF s'exécute.</td>
	<td>Pour la région Sud des Etats-Unis, la valeur est *us-south* <br>Pour la région Royaume-Uni, la valeur est *eu-gb*  <br>Pour l'Allemagne, la valeur est *eu-de* <br>Pour Sydney, la valeur est *au-syd* </td>
  </tr>
  <tr>
    <td>CFapp Name</td>
	<td>Nom de l'application CF.</td>
	<td></td>
  </tr>
  <tr>
    <td>CFapp Index</td>
	  <td>Index de l'instance d'application CF.</td>
	  <td>Par exemple : *0* </br>Si vous avez une application CF avec une instance, seul l'index 0 existe. Si vous mettez à l'échelle l'application CF, par exemple, vers 10 instances, les valeurs d'index sont comprises entre 0 et 9.</td>
  </tr>
  <tr>
    <td>CFapp container</td>
	  <td>Valeur fixe.</td>
	  <td>*container*</td>
  </tr>
  <tr>
    <td>Metric Type</td>
	  <td>Type de métrique. Les métriques de disque, de mémoire et d'unité centrale représentent une série de métriques automatiquement collectées.</td>
	  <td>*UC*</td>
  </tr>
  <tr>
    <td>Metric Subtype</td>
	  <td>Métrique à afficher. </br>[Métriques d'unité centrale](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#cpu_metrics) </br>[Métriques de disque](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#disk_metrics) </br>[Métriques de mémoire](/docs/services/cloud-monitoring/cf/monitoring_cf_apps_ov.html#mem_metrics)</td>
	  <td></td>
  </tr>
  <tr>
    <td>Functions</td>
    <td>Fonctions de requête que vous pouvez sélectionner pour visualiser une métrique de conteneur dans le panneau. </td>
    <td>[Fonctions ![(Icône de lien externe)](../../../icons/launch-glyph.svg "Icône de lien externe")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
   </tr>
</table>




