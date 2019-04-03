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


# Benutzerberechtigungen erteilen
{: #grant_permissions}

In {{site.data.keyword.Bluemix}} können Sie Benutzern eine oder mehrere Rollen zuweisen. Diese Rollen definieren, welche Tasks für diesen Benutzer aktiviert sind, damit er mit dem {{site.data.keyword.monitoringshort}}-Service arbeiten kann. 
{:shortdesc}

Um eine Benutzerberechtigung für die Arbeit mit Metriken zu erteilen, müssen Sie eine Richtlinie für diesen Benutzer hinzufügen, die die Aktionen beschreibt, die dieser Benutzer mit dem {{site.data.keyword.monitoringshort}}-Service in dem Konto ausführen kann. Nur Kontoeigentümer können Benutzern einzelne Richtlinien zuweisen.


## Benutzern eine IAM-Richtlinie über die IBM Cloud-Benutzerschnittstelle zuweisen 
{: #assign_policy_ui}

Führen Sie die folgenden Schritte aus, um einem Benutzer die Berechtigung zum Arbeiten mit dem {{site.data.keyword.monitoringshort}}-Service zu erteilen:

1. Melden Sie sich bei der {{site.data.keyword.Bluemix_notm}}-Konsole an.

    Öffnen Sie einen Web-Browser und starten Sie das {{site.data.keyword.Bluemix_notm}}-Dashboard: [http://console.bluemix.net ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](http://bluemix.net){:new_window}
	
	Nach der Anmeldung mit Ihrer Benutzer-ID und Ihrem Kennwort wird die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle geöffnet.

2. Klicken Sie in der Menüleiste auf **Verwalten>Konto>Benutzer**. 

    Im Fenster *Benutzer* wird eine Liste der Benutzer mit ihren E-Mail-Adressen für das aktuell ausgewählte Konto angezeigt.
	
3. Wenn der Benutzer Mitglied des Kontos ist, wählen Sie den Benutzernamen in der Liste aus oder klicken Sie im Menü *Aktionen* auf **Benutzer verwalten**.

    Wenn der Benutzer kein Mitglied des Kontos ist, finden Sie weitere Informationen unter [Benutzer einladen](/docs/iam?topic=iam-iamuserinv#iamuserinv).

4. Klicken Sie auf **Servicerichtlinien zuweisen**.

5. Geben Sie Informationen zur Richtlinie ein. In der folgenden Tabelle sind die Felder aufgeführt, die für das Definieren einer Richtlinie erforderlich oder optional sind: 

    <table>
	  <caption>Liste der Felder zum Konfigurieren einer IAM-Richtlinie.</caption>
	  <tr>
	    <th>Feld</th>
		<th>Wert</th>
		<th>Status</th>
	  </tr>
	  <tr>
	    <td>Service</td>
		<td>{{site.data.keyword.monitoringlong}}</td>
		<td>Erforderlich</td>
	  </tr>
	  <tr>
	    <td>Rollen</td>
		<td>Wählen Sie eine oder mehrere IAM-Rollen aus. <br>Gültige Rollen sind: *Administrator*, *Operator*, *Editor* und *Viewer*. <br>Weitere Informationen zu den Aktionen, die für die jeweilige Rolle zulässig sind, finden Sie unter [IAM-Rollen](/docs/services/cloud-monitoring?topic=cloud-monitoring-security_ov#iam_roles).</td>
		<td>Erforderlich</td>
	  </tr>
	  <tr>
	    <td>Regionen</td>
		<td>Sie können die Regionen angeben, in denen einem Benutzer der Zugriff für die Arbeit mit Metriken erteilt wird. Wählen Sie **Optionalen Servicekontext angeben** aus. Fügen Sie anschließend eine oder mehrere Regionen einzeln hinzu oder wählen Sie **Alle aktuellen Regionen** aus, um Zugriff auf alle Regionen zu erteilen.</td>
		<td>Optional</td>
	  </tr>
	</table>
	
6. Klicken Sie auf **Richtlinie zuweisen**.
	
Die Richtlinie, die Sie konfigurieren, gilt für die ausgewählten Regionen. 

## Benutzern eine IAM-Richtlinie über die Befehlszeile zuweisen
{: #assign_policy_commandline}

Führen Sie die folgenden Schritte aus, um einen Benutzerzugriff für die Anzeige von Metriken über die Befehlszeile zu erteilen:

1. (Voraussetzung) Installieren Sie die {{site.data.keyword.Bluemix_notm}}-CLI.

   Weitere Informationen dazu finden Sie unter [Installing the {{site.data.keyword.Bluemix_notm}} CLI](/docs/cli?topic=cloud-cli-ibmcloud-cli#overview).
   
   Wenn die CLI installiert ist, fahren Sie mit dem nächsten Schritt fort.
	
2. Melden Sie sich bei einer Region, einer Organisation und einem Bereich in {{site.data.keyword.Bluemix_notm}} an. 

    Weitere Informationen finden Sie in [Wie melde ich mich bei {{site.data.keyword.Bluemix_notm}} an?](/docs/services/cloud-monitoring/qa?topic=cloud-monitoring-cli_qa#login).
	
3. Rufen Sie die Konto-ID ab. 

    Führen Sie den folgenden Befehl aus, um die Konto-ID abzurufen:

    ```
	ibmcloud iam accounts
	```
    {: codeblock}	

	Eine Liste der Konten mit den jeweiligen GUIDs wird angezeigt.
	
	Exportieren Sie die ID des Kontos, in dem Sie einem Benutzer Berechtigungen erteilen möchten. Konfigurieren Sie eine Shellvariable wie `$acct_id`. Beispiel:
	
	```
	export acct_id="1234567891234567812341234123412"
	```
	{: screen}

4. Rufen Sie die {{site.data.keyword.IBM_notm}}-ID des Benutzers ab, dem Sie Berechtigungen erteilen möchten.

    1. Zeigen Sie die Benutzer an, die dem Konto zugeordnet sind. Führen Sie folgenden Befehl aus:
	
	    ```
		ibmcloud iam account-users
		```
		{: codeblock}
		
	2. Rufen Sie die GUID des Benutzers ab. **Hinweis: Dieser Schritt muss von dem Benutzer ausgeführt werden, dem Sie die Berechtigung erteilen möchten.**
	
	    Fordern Sie zum Beispiel den Benutzer auf, die folgenden Befehle auszuführen, um seine Benutzer-ID abzurufen:
		
		Rufen Sie das IAM-Token ab. Weitere Informationen finden Sie unter [IAM-Token mithilfe der {{site.data.keyword.Bluemix_notm}}-CLI abrufen](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_iam#iam_token_cli).

        Rufen Sie die Daten aus dem IAM-Token ab, die sich zwischen den ersten 2 Punkten im IAM-Token befinden. Exportieren Sie die Daten in eine Shellvariable wie z. B. `$user_data` 
		
		```
	    export user_data="xxxxxxxxxxxxxxxxxxxxxxxxxxx"
	    ```
	    {: screen}
		
		Führen Sie den folgenden Befehl aus, um z. B. die Benutzer-ID abzurufen. Dieser Befehl verwendet 'jq' in diesem Beispiel, um die Informationen in einen Text mit JSON-Formatierung zu decodieren:
		
		```
		echo $user_data | base64 -d | jq
		```
		{: codeblock}
		
		Die Ausgabe nach Ausführung dieses Befehls ist folgende:
		
		```
		$ echo $user_data | base64 -d | jq
        {
        "iam_id": "IBMid-xxxxxxxxxx",
        "id": "IBMid-xxxxxxxxxx",
        "realmid": "IBMid",
        ......
		}
        ```
	    {: screen}
		
		Senden Sie die Benutzer-ID aus dem Feld *id* an den Kontoeigner. 
		
	3. Exportieren Sie die Benutzer-ID in eine Shellvariable wie z. B. `$user_ibm_id`.
	
		```
		export user_ibm_id="IBMid-xxxxxxxxxx"
		```
		{: codeblock}

3. Laden Sie den Benutzer zu dem Konto ein, wenn er noch kein Mitglied ist. Weitere Informationen finden Sie unter [Benutzer einladen](/docs/iam?topic=iam-iamuserinv#iamuserinv).

    Führen Sie z. B. den folgenden Befehl aus, um den Benutzer 'xxx@yyy.com' zum Konto 'zzz@ggg.com' einzuladen:
	
	```
	ibmcloud iam account-user-invite xxx@yyy.com zzz@ggg.com OrgAuditor dev SpaceDeveloper
	```
	{: codeblock}
		
4. Erstellen Sie einen Richtliniendateinamen. 

    Verwenden Sie beispielsweise die folgende Vorlage, um Berechtigungen in der Region 'USA (Süden)' zu erteilen:
	
	```
	{
		"roles" : [
			{
				"id": "crn:v1:bluemix:public:iam::::role:Editor" 
			}
		],
		"resources": [
			{
				"serviceName": "ibmcloud-monitoring",
				"region": "us-south"
			}
		]
	}
	```
	{: codeblock}
	
	Name der Richtliniendatei: `policy.json`
	
5. Rufen Sie das IAM-Token für Ihre Benutzer-ID ab.

    Weitere Informationen finden Sie unter [IAM-Token mithilfe der {{site.data.keyword.Bluemix_notm}}-CLI abrufen](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_iam#iam_token_cli).

    Exportieren Sie das IAM-Token in eine Shellvariable wie z. B. `$iam_token`. Beispiel:
	
	```
	export iam_token="xxxxxxxxxxxxxxxxxxxxx"
	```
	{: screen}
	
6. Erteilen Sie dem Benutzer Berechtigungen für die Arbeit mit dem {{site.data.keyword.monitoringshort}}-Service. 

   Führen Sie den folgenden cURL-Befehl aus, um Berechtigungen in der Region 'USA (Süden)' zu erteilen:
	
    ```
	curl -X POST --header "Authorization: $iam_token" --header "Content-Type: application/json" https://iampap.ng.bluemix.net/acms/v1/scopes/a%2F$acct_id/users/$user_ibm_id/policies -d @policy.json
	```
	{: codeblock}
	
	Führen Sie den folgenden cURL-Befehl aus, um Berechtigungen in der Region 'Vereinigtes Königreich' zu erteilen:
	
    ```
	curl -X POST --header "Authorization: $iam_token" --header "Content-Type: application/json" https://iampap.eu-gb.bluemix.net/acms/v1/scopes/a%2F$acct_id/users/$user_ibm_id/policies -d @policy.json
	```
	{: codeblock}

	





## Einem Benutzer eine CF-Rolle über die IBM Cloud-Benutzerschnittstelle zuweisen 
{: #grant_permissions_ui_space}


Um in der Bereichsdomäne oder der Organisationsdomäne mit Metriken arbeiten zu können, muss ein Benutzer über eine CF-Rolle (CF, Cloud Foundry) verfügen, die ihm in {{site.data.keyword.Bluemix_notm}} zugewiesen ist. Eine CF-Rolle beschreibt die Aktionen, die ein Benutzer mit dem {{site.data.keyword.monitoringshort}}-Service in einem Bereich oder einer Organisation ausführen kann. 

Führen Sie die folgenden Schritte aus, um einem Benutzer die Berechtigung zum Arbeiten mit dem {{site.data.keyword.monitoringshort}}-Service zu erteilen:

1. Melden Sie sich bei der {{site.data.keyword.Bluemix_notm}}-Konsole an.

    Öffnen Sie einen Web-Browser und starten Sie das {{site.data.keyword.Bluemix_notm}}-Dashboard: [http://bluemix.net ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](http://bluemix.net){:new_window}
	
	Nach der Anmeldung mit Ihrer Benutzer-ID und Ihrem Kennwort wird die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle geöffnet.

2. Klicken Sie in der Menüleiste auf **Verwalten>Konto>Benutzer**. 

    Im Fenster *Benutzer* wird eine Liste der Benutzer mit ihren E-Mail-Adressen für das aktuell ausgewählte Konto angezeigt.
	
3. Wenn der Benutzer Mitglied des Kontos ist, wählen Sie den Benutzernamen in der Liste aus oder klicken Sie im Menü *Aktionen* auf **Benutzer verwalten**.

    Wenn der Benutzer kein Mitglied des Kontos ist, finden Sie weitere Informationen unter [Benutzer einladen](/docs/iam?topic=iam-iamuserinv#iamuserinv).

4. Klicken Sie auf **Organisation zuweisen**.

5. Geben Sie Informationen zur Richtlinie ein. In der folgenden Tabelle sind die Felder aufgeführt, die für das Definieren einer Richtlinie erforderlich oder optional sind: 

    <table>
	  <caption>Liste der Felder zum Konfigurieren einer CF-Richtlinie.</caption>
	  <tr>
	    <th>Feld</th>
		<th>Wert</th>
	  </tr>
	  <tr>
	    <td>Organisation</td>
		<td>Wählen Sie eine Organisation aus der Liste aus.</td>
	  </tr>
	  <tr>
	    <td>Organisationsrollen</td>
		<td>Wählen Sie **Keine Organisationsrolle** aus. Wenn der Benutzer jedoch über eine Organisationsrolle verfügt, wählen Sie eine Organisationsrolle aus der Liste aus. <br>Gültige Werte sind: **Abrechnungsmanager**, **Auditor**, **Manager**.</td>
	  </tr>
	  <tr>
	    <td>Region</td>
		<td>Wählen Sie eine Region aus der Liste aus. <br>Gültige Werte sind: **Alle aktuellen Regionen**, **US South**, **United Kingdom**.</td>
	  </tr>
	  <tr>
	    <td>Bereich</td>
		<td>Standardmäßig ist **Alle aktuellen Bereiche** vordefiniert, wenn das Feld *Region* auf **Alle aktuellen Regionen** festgelegt ist. Um für einen einzelnen Bereich eine Berechtigung zu erteilen, wählen Sie eine bestimmte Region und anschließend einen Bereich aus der Liste aus.</td>
	  </tr>
	  <tr>
	    <td>Bereichsrollen</td>
		<td>Wählen Sie eine Bereichsrolle aus der Liste aus. <br>Gültige Werte sind: **Manager**, **Auditor**, **Entwickler** und **Keine Bereichsrolle**. Weitere Informationen finden Sie unter [Cloud Foundry-Rollen](/docs/services/cloud-monitoring?topic=cloud-monitoring-security_ov#bmx_roles).</td>
	  </tr>
	</table>
	
6. Klicken Sie auf **Richtlinie zuweisen**.
	
Die Richtlinie, die Sie konfigurieren, gilt für die ausgewählten Regionen. 


