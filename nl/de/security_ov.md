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


# Sicherheit
{: #security_ov}

Um zu steuern, welche {{site.data.keyword.monitoringshort}}-Serviceaktionen ein Benutzer ausführen darf, können Sie dem Benutzer eine oder mehrere Rollen zuweisen. Zur Authentifizierung eines Benutzers für die Arbeit mit Metriken und Alerts können Sie ein UAA-Token, ein IAM-Token oder einen API-Schlüssel verwenden. 
{:shortdesc}





## Authentifizierungsmodelle
{: #auth}

Für die Arbeit mit Metriken, die im {{site.data.keyword.monitoringshort}}-Service für einen Bereich gespeichert sind, benötigen Sie ein Authentifizierungstoken oder einen API-Schlüssel. 

Informationen zum Abrufen eines Sicherheitstoken finden Sie unter:

* [UAA-Token abrufen](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_uaa#auth_uaa)
* [IAM-Token abrufen](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_iam#auth_iam)

Informationen zum Abrufen eines API-Schlüssels finden Sie unter [API-Schlüssel generieren](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_api_key#auth_api_key). Wenn die Sicherheit des API-Schlüssels beeinträchtigt ist, können Sie ihn widerrufen, indem Sie ihn löschen. Anschließend können Sie einen neuen erstellen. Weitere Informationen finden Sie in [API-Schlüssel über die {{site.data.keyword.Bluemix_notm}}-Benuzterschnittstelle widerrufen](/docs/services/cloud-monitoring/security?topic=cloud-monitoring-auth_api_key#revoke_ui). 

Ein UAA-Token und ein IAM-Token laufen nach einem bestimmten Zeitraum ab. Der API-Schlüssel läuft nicht ab. 

In der folgenden Tabelle sind die Sicherheitsmodelle aufgelistet, die für die einzelnen Domänentypen unterstützt werden:

<table>
  <caption>Tabelle 1. Für die einzelnen Domänen unterstützte Sicherheitsmodelle</caption>
  <tr>
    <th></th>
	<th align="right">Konto</th>
    <th align="right">Organisation</th>
    <th align="right">Bereich</th>	
  </tr>
  <tr>
    <th align="left">UAA</th>
	<td align="center">Nein</td>
	<td align="center">Ja</td>
	<td align="center">Ja</td>
  </tr>
  <tr>
    <th align="left">IAM</th>
	<td align="center">Ja</td>
	<td align="center">Ja</td>
	<td align="center">Ja</td>
  </tr>
</table>

Der {{site.data.keyword.monitoringshort}}-Service verwendet die IAM-Zugriffssteuerungsfunktion, um zu regeln, welche Aktionen oder Operationen ein Benutzer oder Service mit der Domäne ausführen kann. Sie können zum Beispiel eine IAM-Richtlinie definieren, um einem Benutzer das Senden und Erstellen von Dashboards für eine Domäne zu erlauben, jedoch nicht das Abrufen der Metriken aus der Domäne.



## Cloud Foundry-Rollen
{: #bmx_roles}

In der folgenden Tabelle sind die Zugriffsrechte für jede Cloud Foundry-Rolle für die Arbeit mit dem {{site.data.keyword.monitoringshort}}-Service aufgelistet:

<table>
  <caption>Tabelle 2. Cloud Foundry-Rollen und Zugriffsrechte für die Arbeit mit dem {{site.data.keyword.monitoringshort}}-Service.</caption>
  <tr>
    <th>Rolle</th>
	<th>Domäne</th>
	<th>Zugriffsberechtigungen</th>
  </tr>
  <tr>
    <td>Manager</td>
	<td>Organisation <br>Bereich</td>
	<td>Alle REST-APIs</td>
  </tr>
  <tr>
    <td>Entwickler</td>
	<td>Bereich</td>
	<td>Alle REST-APIs</td>
  </tr>
  <tr>
    <td>Auditor</td>
	<td>Organisation <br>Bereich</td>
	<td>Nur RESTful-APIs, die schreibgeschützte Operationen wie Abfragen von Metriken ausführen.</td>
  </tr>
</table>

Informationen zum Zuordnen von Benutzerrollen in der Benutzerschnittstelle finden Sie unter [Cloud Foundry-Zugriff verwalten](/docs/iam?topic=iam-mngcf#mngcf).



## IAM-Rollen
{: #iam_roles}

In der folgenden Tabelle sind die {{site.data.keyword.monitoringshort}}-Serviceaktionen für die Arbeit mit Metriken sowie die IAM-Rollen aufgelistet, die einem Benutzer die Berechtigung zum Ausführen dieser Tasks erteilen:

<table>
  <caption>Tabelle 3. Mit Metriken arbeiten </caption>
  <tr>
	<th>Aktion</th>
	<th>IAM-Rolle</th>
  </tr>
  <tr>
    <td>Metriken an die Domäne senden</td>
	<td>Administrator, Editor, Operator</td>
  </tr>
  <tr>
    <td>Metriken abrufen/abfragen</td>
	<td>Administrator, Editor, Viewer</td>
  </tr>
  <tr>
    <td>In der Domäne nach Metriken suchen</td>
	<td>Administrator, Editor</td>
  </tr>
</table>

In der folgenden Tabelle sind die {{site.data.keyword.monitoringshort}}-Serviceaktionen für die Arbeit mit Alerts sowie die IAM-Rollen aufgelistet, die einem Benutzer die Berechtigung zum Ausführen dieser Tasks erteilen:

<table>
  <caption>Tabelle 4. Mit Alerts arbeiten. </caption>
  <tr>
	<th>Aktion</th>
	<th>IAM-Rolle</th>
  </tr>
  <tr>
    <td>Alertregeln erstellen, bearbeiten und löschen</td>
	<td>Administrator, Editor</td>
  </tr>
  <tr>
    <td>Alerts anzeigen</td>
	<td>Administrator, Editor, Viewer</td>
  </tr>
  <tr>
    <td>Alertbenachrichtigungen erstellen, bearbeiten und löschen</td>
	<td>Administrator, Editor</td>
  </tr>
  <tr>
    <td>Benachrichtigungen anzeigen</td>
	<td>Administrator, Editor, Viewer</td>
  </tr>
  <tr>
    <td>Ausgelöste Alertprotokollsätze anzeigen</td>
	<td>Administrator, Editor, Viewer</td>
  </tr>
</table>

Informationen zum Zuordnen von Benutzerrollen in der Benutzerschnittstelle finden Sie unter [IAM-Zugriff verwalten](/docs/iam?topic=iam-iammanidaccser#iammanidaccser).

