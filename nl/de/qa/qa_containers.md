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



# Häufig gestellte Fragen zur Überwachung von Kubernetes-Clustern
{: #qa_containers}

Hier sind die Antworten auf häufig gestellte Fragen zum {{site.data.keyword.monitoringshort}}-Service und zum {{site.data.keyword.containershort_notm}}-Service. 
{:shortdesc}

* [Die Grafana-Abfrage für meine Container enthält keine Daten oder ist fehlerhaft](/docs/services/cloud-monitoring/qa/qa_containers.html#metric_format_change)
* [Wie richte ich eine Clusterumgebung in meiner Terminalsitzung ein?](/docs/services/cloud-monitoring/qa/qa_containers.html#qa1)
* [Wo finde ich den Clusternamen und die Cluster-ID?](/docs/services/cloud-monitoring/qa/qa_containers.html#qa3)
* [Wie rufe ich die Liste der Namensbereiche ab?](/docs/services/cloud-monitoring/qa/qa_containers.html#qa7)
* [Wie rufe ich die Liste der Pods in einem Namensbereich in einem Kubernetes-Cluster ab?](/docs/services/cloud-monitoring/qa/qa_containers.html#qa8)
* [Wie rufe ich alle Pods in einem Cluster nach Namensbereich ab?](/docs/services/cloud-monitoring/qa/qa_containers.html#qa9)

## Die Grafana-Abfrage für meine Container enthält keine Daten oder ist fehlerhaft
{: #metric_format_change}

Das Format der Abfrage, die Sie für einen Container definieren können, hat sich geändert.

Das folgende Format ist veraltet: 

```
{Prefix}.{Version}.{Provider}.{Type}.{ServiceName}.{Region}.{Account}.{Cluster}.{Metric}.{Container in a pod}.{Functions}
```
{: screen}

Die neuen gültigen Formate sind wie folgt:

* [Abfrageformat für CPU-Metriken für einen Container](/docs/services/cloud-monitoring/reference/metrics_format_containers.html#cpu_containers)
* [Abfrageformat für Lademetriken für einen Worker](/docs/services/cloud-monitoring/reference/metrics_format_containers.html#load_workers)
* [Abfrageformat für Speichermetriken für einen Container](/docs/services/cloud-monitoring/reference/metrics_format_containers.html#mem_containers)

Migrieren Sie Ihre alten Abfragen auf das neue Format, um Ihre Daten in Grafana zu visualisieren.

Wenn Ihre Abfrage beispielsweise mit `crn.v1.bluemix.public.containers-kubernetes.us-south.` beginnt, müssen Sie auf das neue Format, d. h. auf `ibmcloud.public.containers-kubernetes.us-south`, migrieren.

In der folgenden Tabelle sind die Felder in dem veralteten Format aufgeführt:

 <table>
      <caption>Tabelle 1. Grafana-Abfragefelder für Container</caption>
      <tr>
        <th align="center">Feld</th>
        <th align="center">Beschreibung</th>
        <th align="center">Gültige Werte</th>
      </tr>
      <tr>
        <td>Präfix</td>
        <td>Präfix, das verwendet wird, um zu zeigen, dass es sich um eine {{site.data.keyword.IBM_notm}}-Cloud-Ressource handelt.</td>
        <td>`crn`</td>
      </tr>
      <tr>
        <td>Version</td>
        <td>Version, die das Format und die Felder der erfassten Metrikdaten angibt. </td>
        <td>`v1`</td>
      </tr>
      <tr>
        <td>Provider</td>
        <td>Cloud-Provider, bei dem die Daten erfasst werden. Dieses Feld ist eine alphanumerische ID.</td>
        <td>Für die öffentliche {{site.data.keyword.IBM_notm}} Cloud lautet der Wert `bluemix`</td>
      </tr>
      <tr>
        <td>Typ</td>
        <td>Cloudumgebung, in der die Daten erfasst werden.</td>
        <td>Für die öffentliche {{site.data.keyword.IBM_notm}} Cloud lautet der Wert `public`.</td>
      </tr>
      <tr>
        <td>Servicename</td>
        <td>Cloudinfrastruktur, in der Metriken erfasst werden.</td>
        <td>Für den {{site.data.keyword.monitoringshort}}-Service lautet der Wert `containers-kubernetes`</td>
      </tr>
      <tr>
        <td>Region</td>
        <td>Cloudregion, in der Metriken erfasst werden.</td>
        <td>Für die Region 'USA (Süden)' lautet der Wert `ng` <br>Für die Region 'Vereinigtes Königreich' lautet der Wert `eu-gb` <br>Für Deutschland lautet der Wert `eu-de` <br>Für Sydney lautet der Wert `au-syd` </td>
      </tr>
      <tr>
        <td>Konto</td>
        <td>GUID des Kontos, in dem Metriken erfasst werden. <br>Das Format dieses Feldes ist `a_ID`. Dabei ist ID die GUID des Kontos. <br>Informationen zum Abrufen der GUID für das Konto finden Sie unter [Vorgehensweise zum Abrufen der GUID eines Kontos](/docs/services/cloud-monitoring/qa/cli_qa.html#account_guid).</td>
        <td>a_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</td>
      </tr>
      <tr>
        <td>Cluster</td>
        <td>GUID des Clusters, in dem Metriken erfasst werden.</td>
        <td>xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</td>
      </tr>
      <tr>
        <td>Metrik</td>
        <td>Metrik, die automatisch für einen Container erfasst wird.</td>
        <td>Eine Liste der CPU-Metriken finden Sie unter [CPU-Metriken für Container](/docs/services/cloud-monitoring/containers/monitoring_containers_ov.html#cpu_metrics_containers). <br>Eine Liste der Speichermetriken finden Sie unter [Speichermetriken](/docs/services/cloud-monitoring/containers/monitoring_containers_ov.html#memory_metrics). </td>
      </tr>
      <tr>
        <td>Container in einem Pod</td>
        <td>Kombination von Kubernetes-Ressourcennamen und GUIDs, die für die eindeutige Kennzeichnung eines Containers erforderlich sind, der in einem Pod ausgeführt wird. <br>**Hinweis:** Wenn Sie die Liste verfügbarer Optionen für diesen Eintrag in der Abfrage anzeigen, beachten Sie, dass dort auch ein Eintrag mit folgendem Format vorhanden ist: {namespace}{pod_name}{deploymentname_name}_POD{container_ID}. Diese Einträge entsprechen den internen Container-IDs, die von Kubernetes erstellt wurden.</td>
		<td>{namespace}_{pod_name}_{deployment_name}_{container_id}</td>
      </tr>
      <tr>
        <td>Funktionen</td>
        <td>Abfragefunktionen, die Sie zur Visualisierung einer Containermetrik in der Anzeige auswählen können. <br>Weitere Informationen finden Sie unter [Funktionen ![(Symbol für externen Link)](../../icons/launch-glyph.svg "Symbol für externen Link") ](http://graphite.readthedocs.io/en/latest/functions.html){: new_window}</td>
        <td></td>
      </tr>
    </table>


## Wie richte ich eine Clusterumgebung in meiner Terminalsitzung ein?
{: #qa1}

Sie müssen den Kontext eines Kubernetes-Clusters festlegen, um diesen mithilfe von Befehlen zu verwalten.

**Hinweis:** Um einen Cluster zu verwalten, benötigen Sie eine IAM-Richtlinie für den {{site.data.keyword.containershort_notm}}-Service, der Ihren Benutzer mit Berechtigungen zum Ausführen der Task zugeordnet ist.

Führen Sie die folgenden Schritte aus, um den Kontext eines Clusters einzurichten:

1. Melden Sie sich bei der Region, der Organisation und dem Bereich in {{site.data.keyword.Bluemix_notm}} an, die/der dem von Ihnen erstellten Cluster zugeordnet ist. Weitere Informationen finden Sie unter [Wie melde ich mich bei {{site.data.keyword.Bluemix_notm}} an?](/docs/services/cloud-monitoring/qa/cli_qa.html#login).

2. Initialisieren Sie das {{site.data.keyword.containershort_notm}}-Service-Plug-in. Führen Sie folgenden Befehl aus:

	```
	ibmcloud cs init
	```
	{: codeblock}

3. Legen Sie den Kontext des Clusters in Ihrer Terminalsitzung fest. Führen Sie die folgenden Befehle aus:
    
	```
	ibmcloud cs cluster-config MyCluster
	```
	{: codeblock}

    Die Ausgabe dieses Befehls stellt den Befehl bereit, den Sie in Ihrem Terminal ausführen müssen, um den Pfad zur Konfigurationsdatei anzugeben. Beispiel:

	```
	export KUBECONFIG=/Users/ibm/.bluemix/plugins/container-service/clusters/MyCluster/kube-config-hou02-MyCluster.yml
	```
	{: codeblock}

    Kopieren Sie den Befehl und fügen Sie ihn ein, um die Umgebungsvariable in Ihrem Terminal festzulegen, und drücken Sie dann die **Eingabetaste**.

 
 

## Wo finde ich den Clusternamen und die Cluster-ID?
{: #qa3}

Führen Sie die folgenden Schritte aus, um den Clusternamen und die ID über die Benutzerschnittstelle abzurufen:

1. Melden Sie sich bei Ihrem {{site.data.keyword.Bluemix_notm}}-Konto an.

    Das {{site.data.keyword.Bluemix_notm}}-Dashboard finden Sie hier: [http://bluemix.net ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](http://bluemix.net){:new_window}.
    
	Nach der Anmeldung mit Ihrer Benutzer-ID und Ihrem Kennwort wird die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle geöffnet.

2. Wählen Sie im {{site.data.keyword.Bluemix_notm}}-*Dashboard* die Option **Menü > Container** aus.

    Die Liste der im Konto verfügbaren Cluster wird angezeigt.

3. Wählen Sie einen Clustereintrag aus, um die Cluster-ID abzurufen. 

    Die Übersichtsseite wird geöffnet. Auf dieser Seite können Sie die Cluster-ID abrufen.



Führen Sie die folgenden Schritte aus, um den Clusternamen und die ID über die Befehlszeile abzurufen:

1. Melden Sie sich bei der Region, der Organisation und dem Bereich in {{site.data.keyword.Bluemix_notm}} an, die/der dem von Ihnen erstellten Cluster zugeordnet ist. Weitere Informationen finden Sie unter [Wie melde ich mich bei {{site.data.keyword.Bluemix_notm}} an?](/docs/services/cloud-monitoring/qa/cli_qa.html#login).

2. Listen Sie die im Konto verfügbaren Cluster auf. Führen Sie folgenden Befehl aus: 

    ```
	ibmcloud cs clusters
	``` 
	{: codeblock}
	
	In der Ausgabe dieses Berichts sind alle Cluster im Konto mit ihren entsprechenden IDs aufgeführt.
	
3. Führen Sie den folgenden Befehl aus, um die Custer-ID abzurufen:

    ```
	ibmcloud cs cluster-get my_cluster
	```
    {: screen}	
 


## Wie rufe ich die Liste der Namensbereiche ab?
{: #qa7}

Führen Sie die folgenden Schritte aus, um eine Liste aller Namensbereiche in Ihrem Cluster abzurufen:

Führen Sie die folgenden Schritte aus:

1. Richten Sie den Clusterkontext ein. Weitere Informationen finden Sie unter [Wie richte ich eine Clusterumgebung in meiner Terminalsitzung ein?](/docs/services/cloud-monitoring/qa/qa_containers.html#qa1).

2. Listen Sie alle Namensbereiche auf. Führen Sie den folgenden 'kubectl'-Befehl aus:

    ```
    kubectl get namespaces
	```
	{: codeblock}

## Wie rufe ich die Liste der Pods für jeden Namensbereich in einem Kubernetes-Cluster ab?
{: #qa8}
		
Führen Sie die folgenden Schritte aus, um die Liste der Pods in einem Namensbereich abzurufen:

1. Richten Sie den Clusterkontext ein. Weitere Informationen finden Sie unter [Wie richte ich eine Clusterumgebung in meiner Terminalsitzung ein?](/docs/services/cloud-monitoring/qa/qa_containers.html#qa1).

2. Führen Sie den folgenden Befehl aus, um die Liste der Pods für jeden Namensbereich in einem Kubernetes-Cluster abzurufen:

    ```
	kubectl --namespace=NamespaceName get pods 
	```
	{: codeblock}
	
	Dabei ist 'Namespacename' der Name des Namensbereichs, z. B. *default*.

## Wie rufe ich alle Pods in einem Cluster nach Namensbereich ab?
{: #qa9}
		
Führen Sie die folgenden Schritte aus:

1. Richten Sie den Clusterkontext ein. Weitere Informationen finden Sie unter [Wie richte ich eine Clusterumgebung in meiner Terminalsitzung ein?](/docs/services/cloud-monitoring/qa/qa_containers.html#qa1).
	
2. Führen Sie den folgenden Befehl aus, um alle Pods in einem Cluster nach Namensbereich abzurufen:

	```
	kubectl get pods --all-namespaces
	```
	{: codeblock}
		


