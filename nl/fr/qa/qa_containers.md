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



# Foire aux questions liées à la surveillance des clusters Kubernetes
{: #qa_containers}

Vous trouverez ci-après les réponses aux questions fréquentes concernant le service {{site.data.keyword.monitoringshort}} et le service {{site.data.keyword.containershort_notm}}. 
{:shortdesc}

* [La requête Grafana portant sur mes conteneurs ne renvoie aucune donnée ou est erronée](/docs/services/cloud-monitoring/qa/qa_containers.html#metric_format_change)
* [Comment configurer un environnement de cluster dans ma session de terminal ?](/docs/services/cloud-monitoring/qa/qa_containers.html#qa1)
* [Où le nom et l'ID du cluster sont-ils définis ?](/docs/services/cloud-monitoring/qa/qa_containers.html#qa3)
* [Comment obtenir la liste des espaces de noms ?](/docs/services/cloud-monitoring/qa/qa_containers.html#qa7)
* [Comment obtenir la liste des pods par espace de noms dans un cluster Kubernetes ?](/docs/services/cloud-monitoring/qa/qa_containers.html#qa8)
* [Comment obtenir tous les pods d'un cluster par espace de noms ?](/docs/services/cloud-monitoring/qa/qa_containers.html#qa9)

## La requête Grafana portant sur mes conteneurs ne renvoie aucune donnée ou est erronée
{: #metric_format_change}

Le format de la requête que vous pouvez définir pour un conteneur a changé.

Le format suivant est obsolète : 

```
{Prefix}.{Version}.{Provider}.{Type}.{ServiceName}.{Region}.{Account}.{Cluster}.{Metric}.{Container in a pod}.{Functions}
```
{: screen}

Les nouveaux formats valides sont les suivants :

* [Format de requête de métrique d'UC pour un conteneur](/docs/services/cloud-monitoring/reference/metrics_format_containers.html#cpu_containers)
* [Format de requête de métrique de charge pour un agent](/docs/services/cloud-monitoring/reference/metrics_format_containers.html#load_workers)
* [Format de requête de métrique de mémoire pour un conteneur](/docs/services/cloud-monitoring/reference/metrics_format_containers.html#mem_containers)

Faites migrer vos anciennes requêtes vers le nouveau format afin de visualiser vos données dans Grafana.

Par exemple, si votre requête commence par `crn.v1.bluemix.public.containers-kubernetes.us-south.`, vous devez faire migrer votre requête vers le nouveau format, autrement dit, vers `ibmcloud.public.containers-kubernetes.us-south`.

Le tableau suivant répertorie les zones dans le format qui est devenu obsolète :

 <table>
      <caption>Tableau 1. Zones de requête Grafana pour les conteneurs</caption>
      <tr>
        <th align="center">Zone</th>
        <th align="center">Description</th>
        <th align="center">Valeurs valides</th>
      </tr>
      <tr>
        <td>Prefix</td>
        <td>Préfixe utilisé pour indiquer qu'il s'agit d'une ressource {{site.data.keyword.IBM_notm}} Cloud.</td>
        <td>`crn`</td>
      </tr>
      <tr>
        <td>Version</td>
        <td>Version qui indique le format et les zones des données de métrique collectées. </td>
        <td>`v1`</td>
      </tr>
      <tr>
        <td>Provider</td>
        <td>Fournisseur de cloud dans lequel les données sont collectées. Cette zone est un identificateur alphanumérique.</td>
        <td>Pour l'environnement de cloud {{site.data.keyword.IBM_notm}} public, la valeur est : `bluemix`</td>
      </tr>
      <tr>
        <td>Type</td>
        <td>Environnement de cloud dans lequel les données sont collectées.</td>
        <td>Pour l'environnement de cloud {{site.data.keyword.IBM_notm}} public, la valeur est : `public`</td>
      </tr>
      <tr>
        <td>Service name</td>
        <td>Infrastructure de cloud dans laquelle les métriques sont collectées.</td>
        <td>Pour le service {{site.data.keyword.monitoringshort}}, la valeur est : `containers-kubernetes`</td>
      </tr>
      <tr>
        <td>Region</td>
        <td>Région de cloud dans laquelle les métriques sont collectées.</td>
        <td>Pour la région Sud des Etats-Unis, la valeur est : `ng` <br>Pour la région Royaume-Uni, la valeur est : `eu-gb` <br>Pour l'Allemagne, la valeur est : `eu-de` <br>Pour Sydney, la valeur est : `au-syd` </td>
      </tr>
      <tr>
        <td>Account</td>
        <td>Identificateur global unique du compte sur lequel les métriques sont collectées. <br>Le format de cette zone est le suivant : `a_ID` où ID est l'identificateur global unique du compte. <br>Pour obtenir l'identificateur global unique du compte, voir [Comment obtenir l'identificateur global unique d'un compte](/docs/services/cloud-monitoring/qa/cli_qa.html#account_guid).</td>
        <td>a_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</td>
      </tr>
      <tr>
        <td>Cluster</td>
        <td>Identificateur global unique du cluster dans lequel les métriques sont collectées.</td>
        <td>xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</td>
      </tr>
      <tr>
        <td>Metric</td>
        <td>Métrique automatiquement collectée pour un conteneur.</td>
        <td>Pour obtenir une liste de métriques d'unité centrale, voir [Métriques d'unité centrale pour les conteneurs](/docs/services/cloud-monitoring/containers/monitoring_containers_ov.html#cpu_metrics_containers). <br>Pour obtenir la liste des métriques de mémoire, voir [Métriques de mémoire](/docs/services/cloud-monitoring/containers/monitoring_containers_ov.html#memory_metrics). </td>
      </tr>
      <tr>
        <td>Container in a pod</td>
        <td>Combinaison d'identificateurs globaux uniques et de noms de ressource Kubernetes requis pour identifier de façon unique un conteneur s'exécutant dans un pod. <br>**Remarque :** lorsque vous consultez la liste des options disponibles pour cette entrée dans la requête, notez qu'il existe également une entrée au format suivant : {namespace}{pod_name}{deploymentname_name}_POD{container_ID}. Elle correspond aux ID de conteneur internes qui sont créés par Kubernetes.</td>
		<td>{namespace}_{pod_name}_{deployment_name}_{container_id}</td>
      </tr>
      <tr>
        <td>Functions</td>
        <td>Fonctions de requête que vous pouvez sélectionner pour visualiser une métrique de conteneur dans le panneau. <br>Pour plus d'informations, voir [Functions ![(Icône de lien externe)](../../icons/launch-glyph.svg "Icône de lien externe")](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
        <td></td>
      </tr>
    </table>


## Comment configurer un environnement de cluster dans ma session de terminal ?
{: #qa1}

Vous devez définir le contexte d'un cluster Kubernetes pour le gérer à l'aide de commandes.

**Remarque :** pour pouvoir gérer un cluster, votre utilisateur doit se voir affecter une règle IAM pour le service {{site.data.keyword.containershort_notm}}  avec les droits permettant d'effectuer la tâche.

Procédez comme suit pour configurer le contexte d'un cluster :

1. Connectez-vous à la région, l'organisation et l'espace dans l'environnement {{site.data.keyword.Bluemix_notm}} associé au cluster que vous avez créé. Pour plus d'informations, voir [Comment se connecter à {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login).

2. Initialisez le plug-in du service {{site.data.keyword.containershort_notm}}. Exécutez la commande suivante :

	```
	ibmcloud cs init
	```
	{: codeblock}

3. Définissez le contexte du cluster dans votre session de terminal. Exécutez les commandes suivantes :
    
	```
	ibmcloud cs cluster-config MyCluster
	```
	{: codeblock}

    La sortie de l'exécution de cette commande fournit la commande que vous devez exécuter dans votre terminal pour définir le chemin d'accès à votre fichier de configuration. Par exemple :

	```
	export KUBECONFIG=/Users/ibm/.bluemix/plugins/container-service/clusters/MyCluster/kube-config-hou02-MyCluster.yml
	```
	{: codeblock}

    Copiez et collez la commande afin de définir la variable d'environnement dans votre terminal, puis appuyez sur **Entrée**.

 
 

## Où le nom et l'ID du cluster sont-ils définis ?
{: #qa3}

Procédez comme suit pour obtenir le nom et l'ID du cluster à l'aide de l'interface utilisateur :

1. Connectez-vous à votre compte {{site.data.keyword.Bluemix_notm}}.

    Le tableau de bord {{site.data.keyword.Bluemix_notm}} se trouve à l'adresse suivante : [http://bluemix.net ![Icône de lien externe](../../../icons/launch-glyph.svg "Icône de lien externe")](http://bluemix.net){:new_window}.
    
	Après que vous vous êtes connecté avec votre ID utilisateur et votre mot de passe, l'interface utilisateur {{site.data.keyword.Bluemix_notm}} s'ouvre.

2. A partir du *tableau de bord* {{site.data.keyword.Bluemix_notm}}, sélectionnez **Menu > Conteneurs**.

    La liste des clusters disponibles dans le compte s'affiche.

3. Pour obtenir l'ID de cluster, sélectionnez une entrée de cluster. 

    La page de présentation s'ouvre. Sur cette page, vous pouvez obtenir l'ID de cluster.



Procédez comme suit pour obtenir le nom et l'ID du cluster à l'aide de la ligne de commande :

1. Connectez-vous à la région, l'organisation et l'espace dans l'environnement {{site.data.keyword.Bluemix_notm}} associé au cluster que vous avez créé. Pour plus d'informations, voir [Comment se connecter à {{site.data.keyword.Bluemix_notm}}](/docs/services/cloud-monitoring/qa/cli_qa.html#login).

2. Répertoriez les clusters qui sont disponibles dans le compte. Exécutez la commande suivante : 

    ```
	ibmcloud cs clusters
	``` 
	{: codeblock}
	
	La sortie de cette commande répertorie tous les clusters du compte accompagnés des ID correspondants.
	
3. Pour obtenir l'ID de cluster, exécutez la commande suivante :

    ```
	ibmcloud cs cluster-get my_cluster
	```
    {: screen}	
 


## Comment obtenir la liste des espaces de nom ?
{: #qa7}

Pour obtenir la liste de tous les espaces de nom de votre cluster, procédez comme suit :

Procédez comme suit :

1. Configurez le contexte de cluster. Pour plus d'informations, voir [Comment configurer un environnement de cluster dans ma session de terminal ?](/docs/services/cloud-monitoring/qa/qa_containers.html#qa1).

2. Répertoriez tous les espaces de nom. Exécutez la commande kubectl suivante :

    ```
    kubectl get namespaces
	```
	{: codeblock}

## Comment obtenir la liste des pods par espace de nom dans un cluster Kubernetes ?
{: #qa8}
		
Pour obtenir la liste des pods d'un espace de nom, procédez comme suit :

1. Configurez le contexte de cluster. Pour plus d'informations, voir [Comment configurer un environnement de cluster dans ma session de terminal ?](/docs/services/cloud-monitoring/qa/qa_containers.html#qa1).

2. Pour obtenir la liste des pods par espace de nom dans un cluster Kubernetes, exécutez la commande suivante :

    ```
	kubectl --namespace=NamespaceName get pods 
	```
	{: codeblock}
	
	où Namespacename est le nom de l'espace de noms, par exemple, *default*.

## Comment obtenir tous les pods d'un cluster par espace de nom ?
{: #qa9}
		
Procédez comme suit :

1. Configurez le contexte de cluster. Pour plus d'informations, voir [Comment configurer un environnement de cluster dans ma session de terminal ?](/docs/services/cloud-monitoring/qa/qa_containers.html#qa1).
	
2. Pour obtenir tous les pods d'un cluster par espace de nom, exécutez la commande suivante :

	```
	kubectl get pods --all-namespaces
	```
	{: codeblock}
		


