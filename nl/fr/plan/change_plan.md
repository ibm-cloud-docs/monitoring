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


# Changement de plan
{: #change_plan}

Votre pouvez changer de plan de service {{site.data.keyword.monitoringshort}} via le tableau de bord {{site.data.keyword.monitoringlong_notm}}  ou en exécutant la commande `cf update-service`. Vous pouvez mettre à niveau ou rétrograder votre plan à tout moment.
{:shortdesc}

## Changement de plan de service dans l'interface utilisateur
{: #change_plan_ui}

Pour changer de plan de service dans le tableau de bord {{site.data.keyword.monitoringlong_notm}}, procédez comme suit :

1. Connectez-vous à {{site.data.keyword.Bluemix_notm}}, puis cliquez sur le service {{site.data.keyword.monitoringshort}} dans le tableau de bord. 

    Le tableau de bord du service {{site.data.keyword.monitoringshort}} s'ouvre.
    
2. Sélectionnez l'onglet **Plan**.

    Les informations relatives au plan en cours sont affichées.
	
3. Sélectionnez un nouveau plan pour mettre à niveau votre plan ou le rétrograder. 

4. Cliquez sur **Save**.



## Changement de plan de service via l'interface de ligne de commande
{: #change_plan_cli}

Pour changer de plan de service dans {{site.data.keyword.Bluemix_notm}} via l'interface de ligne de commande, procédez comme suit :

1. Connectez-vous à une région, une organisation et un espace dans {{site.data.keyword.Bluemix_notm}}. 

    Pour plus d'informations, voir [Comment se connecter à {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login).
	
2. Exécutez la commande `ibmcloud service list` pour identifier le plan en cours et pour obtenir le nom du service {{site.data.keyword.loganalysisshort}} depuis la liste des services disponible dans l'espace. 

    La valeur de la zone **nom** est celle que vous devez utiliser pour changer de plan. 

    Par exemple
	
	```
	$ ibmcloud service list
	Getting services in org MyOrg / space dev as xxx@yyy.com...
	OK
	name            service      plan   bound apps   last operation
	Monitoring-0c   Monitoring   premium             create succeeded
    ```
	{: screen}
    
3. Mettez à jour votre plan ou rétrogradez-le. Exécutez la commande `ibmcloud service update`.
    
	```
	ibmcloud service update service_name [-p new_plan]
	```
	{: codeblock}
	
	où 
	
	* *service_name* est le nom de votre service. 
	* *new_plan* est le nom du plan.
	
	Le tableau suivant répertorie les différents plans et les valeurs prises en charge :
	
	<table>
	  <caption>Tableau 1. Liste des plans</caption>
	  <tr>
	    <th>Plan</th>
		<th>Fonctions</th>
	    <th>Nom</th>
	  </tr>
	  <tr>
	    <td>Lite</td>
	    <td>Surveillance gratuite.</td>
		<td>lite</td>
	  </tr>
	  <tr>
	    <td>Premium</td>
	    <td>Surveillance premium.</td>
		<td>premium</td>
	  </tr>
	</table>
	
	Par exemple, pour rétrograder votre plan et passer au plan *Lite*, exécutez la commande suivante :
	
	```
	ibmcloud service update "Monitoring-0c" -p lite
    Updating service instance Monitoring-0c as xxx@yyy.com...
    OK
	```
	{: screen}

4. Vérifiez que le plan a été changé. Exécutez la commande `ibmcloud service list`.

    ```
	ibmcloud service list
    Getting services in org MyOrg / space dev as xxx@yyy.com...
    OK

    nom               service       plan   applications liées  dernière opération
    Monitoring-0c     Monitoring    lite                       create succeeded
	```
	{: screen}






