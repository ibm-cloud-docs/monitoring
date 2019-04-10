---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, iam

subcollection: Sysdig

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

 
# Benutzerzugriff in {{site.data.keyword.cloud_notm}} verwalten
{: #iam}

{{site.data.keyword.iamlong}} (IAM) ermöglicht es Ihnen, Benutzer sicher zu authentifizieren und den Zugriff auf alle Cloudressourcen konsistent in {{site.data.keyword.cloud_notm}} zu steuern. 
{:shortdesc}

**Jedem Benutzer, der auf den {{site.data.keyword.mon_full_notm}}-Service in Ihrem Konto zugreift, muss eine Zugriffsrichtlinie mit einer definierten IAM-Benutzerrolle zugeordnet werden.** Die Richtlinie bestimmt, welche Aktionen der Benutzer im Kontext des ausgewählten Service oder der ausgewählten Instanz ausführen kann. Die zulässigen Aktionen werden angepasst und als Operationen definiert, die für den Service ausgeführt werden dürfen. Die Aktionen werden dann IAM-Benutzerrollen zugeordnet.

Mit *Richtlinien* kann der Zugriff auf verschiedenen Ebenen erteilt werden. Zu den Optionen gehören unter anderem die folgenden: 

* Zugriff auf alle IAM-fähigen Services in Ihrem Konto
* Zugriff auf alle Instanzen des Service in einer einzigen Region in Ihrem Konto
* Zugriff auf eine einzelne Serviceinstanz in Ihrem Konto
* Zugriff auf alle Instanzen des Service im Kontext einer Ressourcengruppe
* Zugriff auf alle Instanzen des Service in einer einzelnen Region im Kontext einer Ressourcengruppe
* Zugriff auf alle IAM-fähigen Services im Kontext einer Ressourcengruppe

*Rollen* definieren die Aktionen, die ein Benutzer oder eine Service-ID ausführen kann. Es gibt verschiedene Typen von Rollen in {{site.data.keyword.cloud_notm}}:
* *Plattformmanagementrollen* ermöglichen es Benutzern, Tasks für Serviereressourcen auf Plattformebene auszuführen, z. B. Benutzerzugriff für den Service zuordnen, Service-IDs erstellen oder löschen, Instanzen erstellen, anderen Benutzern Richtlinien für Ihren Service zuordnen und Instanzen an Anwendungen binden.
* Mit *Servicezugriffsrollen* können Benutzern unterschiedliche Berechtigungsstufen zum Aufrufen der API des Service zugewiesen werden.

**Um eine Gruppe von Benutzern und Service-IDs in einer einzigen Entität zu organisieren, die es Ihnen vereinfacht, IAM-Berechtigungen zu verwalten, verwenden Sie **Zugriffsgruppen*.** Sie können der Gruppe eine einzelne Richtlinie zuordnen, anstatt den Zugriff jedem einzelnen Benutzer oder jeder einzelnen Service-ID mehrfach zuzuordnen.
{: tip}


## Zugriff verwalten, indem Zugriffsgruppen verwendet werden
{: #iam_groups}

Um den Zugriff zu verwalten oder neuen Zugriff für Benutzer mithilfe von Zugriffsgruppen zu erteilen, müssen Sie der Kontoeigner, der Administrator oder Editor für alle identitäts- und zugriffsfähigen Services im Konto oder der zugeordnete Administrator oder Editor für den IAM-Zugriffsgruppen-Service sein. 

Wählen Sie eine der folgenden Aktionen aus, um Zugriffsgruppen in {{site.data.keyword.cloud_notm}} zu verwalten:

* [Eine Zugriffsgruppe erstellen](/docs/iam?topic=iam-groups#create_ag)
* [Einer Gruppe Zugriff zuordnen](/docs/iam?topic=iam-groups#access_ag)


## Zugriff verwalten, indem Benutzern Richtlinien direkt zugeordnet werden
{: #iam_users}

Wenn Sie den Zugriff verwalten oder neuen Zugriff für Benutzer mithilfe von IAM-Richtlinien erteilen möchten, müssen Sie der Kontoeigner, der Administrator für alle Services im Konto oder der Administrator für den betreffenden Service oder die betreffende Serviceinstanz sein. 

Wählen Sie eine der folgenden Aktionen aus, um IAM-Richtlinien in {{site.data.keyword.cloud_notm}} zu verwalten:

* Informationen zum Ändern der Berechtigungen eines Benutzers finden Sie im Abschnitt [Vorhandenen Zugriff bearbeiten](/docs/iam?topic=iam-iammanidaccser#edit_existing).
* Informationen zum Erteilen von Berechtigungen für einen Benutzer finden Sie im Abschnitt [Neuen Zugriff zuordnen](/docs/iam?topic=iam-iammanidaccser#assign_new_access).
* Informationen zum Widerrufen von Berechtigungen finden Sie im Abschnitt [Zugriff entfernen](/docs/iam?topic=iam-iammanidaccser#removing_access).
* Wenn Sie die Berechtigungen eines Benutzers überprüfen möchten, lesen Sie die Informationen im Abschnitt [Zuteilten Zugriff prüfen](/docs/iam?topic=iam-iammanidaccser#review_your_access).


## {{site.data.keyword.cloud_notm}}-Plattformrollen
{: #iam_platform}

Verwenden Sie die folgende Tabelle, um die Plattformrolle anzugeben, die Sie einem Benutzer in {{site.data.keyword.cloud_notm}} erteilen können, und um eine der folgenden Plattformaktionen auszuführen:

| Plattformaktionen                                                        | {{site.data.keyword.cloud_notm}}-Plattformrollen    | 
|-------------------------------------------------------------------------|------------------------------------------------------|
| `Anderen Kontomitgliedern Zugriff auf die Arbeit mit dem Service erteilen`           | Administrator                                        | 
| `Eine Serviceinstanz bereitstellen`                                          | Administrator </br>Editor                            | 
| `Eine Serviceinstanz löschen`                                             | Administrator </br>Editor                            | 
| `Eine Service-ID erstellen`                                                   | Administrator </br>Editor                            |
| `Details einer Serviceinstanz anzeigen`                                    | Administrator </br>Editor </br>Operator </br>Anzeigeberechtigter  | 
| `Serviceinstanzen im Monitoring-Dashboard "Beobachtbarkeit" anzeigen`      | Administrator </br>Editor </br>Operator </br>Anzeigeberechtigter  | 
{: caption="Tabelle 1. IAM-Benutzerrollen und -Aktionen" caption-side="top"}



## Sysdig-Rollen
{: #iam_sysdig_roles}

In der folgenden Tabelle werden die Sysdig-Rollen und -Aktionen pro Rolle aufgeführt:

| Aktionen                                                                    | Sysdig-Rolle                                          | 
|----------------------------------------------------------------------------|------------------------------------------------------|
| `Sysdig-Zugriffsschlüssel zurücksetzen`                                              | Admin                                                |
| `Benutzer verwalten`                                                             | Admin                                                |
| `Teams erstellen, konfigurieren und löschen`                                      | Admin                                                |
| `Benachrichtigungskanäle konfigurieren und entfernen`                              | Admin                                                | 
| `Sysdig-Agenten konfigurieren und entfernen`                                       | Admin                                                |
| `Sysdig-Webbenutzerschnittstellen-Inhalt erstellen, löschen und bearbeiten`                    | Admin </br>Benutzer                                      |  
| `Metriken über die Sysdig-Webbenutzerschnittstelle anzeigen`                                   | Admin </br>Benutzer                                      |  
| `Alerts erstellen und löschen`                                                 | Admin </br>Benutzer                                      | 
| `Erfassungen erstellen und löschen`                                               | Admin </br>Benutzer                                      |   
{: caption="Tabelle 2. Sysdig-Rollen und -Aktionen" caption-side="top"}


## Sysdig-Rollen zu {{site.data.keyword.cloud_notm}}-Rollen zuordnen
{: #iam_sysdig}

Verwenden Sie die folgende Tabelle, wie einer Sysdig-Rolle eine {{site.data.keyword.cloud_notm}}-Rolle zugeordnet wird:

| Rollentyp        | Rolle               | Sysdig-Rolle                | Beschreibung                                 |
|---------------------|--------------------|----------------------------|---------------------------------------------|
| Plattformrolle       | Administrator      | Admin                      | Erteilt dem Benutzer Sysdig-Admin-Berechtigungen.   | 
| Servicerolle        | Manager            | Admin                      | Erteilt dem Benutzer Sysdig-Admin-Berechtigungen.   | 
| Servicerolle        | Schreibberechtigter             | Benutzer                       | Erteilt dem Benutzer Sysdig-Benutzerberechtigungen.    |
| Servicerolle        | Leseberechtigter             |                            | Es werden keine Berechtigungen erteilt.                 |
{: caption="Tabelle 3. Sysdig-Rollen" caption-side="top"}


