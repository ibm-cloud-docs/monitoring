---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, iam, access groups

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

 
# Mit IAM-Richtlinien und Zugriffsgruppen arbeiten
{: #iam_work}

{{site.data.keyword.iamlong}} (IAM) ermöglicht es Ihnen, Benutzer sicher zu authentifizieren und den Zugriff auf alle Cloudressourcen konsistent in {{site.data.keyword.cloud_notm}} zu steuern. 
{:shortdesc}

Wenn Sie einem Benutzer Administratorberechtigungen für Sysdig erteilen möchten, können Sie dem Benutzer eine der folgenden Rollen zuordnen:

* Plattformrolle `Administrator`: Erteilen Sie diese Rolle, wenn der Benutzer auch ein Administrator für den Sysdig-Service in {{site.data.keyword.cloud_notm}} ist.
* Plattformrolle `Editor`: Erteilen Sie diese Rolle, wenn der Benutzer Sysdig-Instanzen in {{site.data.keyword.cloud_notm}} bereitstellen oder entfernen muss.
* Servicerolle `Manager`: Erteilen Sie diese Rolle, wenn der Benutzer den Sysdig-Service in {{site.data.keyword.cloud_notm}} nicht verwalten soll.

Wenn Sie einem Benutzer Benutzerberechtigungen für Sysdig erteilen möchten, können Sie dem Benutzer die Servicerolle `Schreibberechtigter` zuordnen.

**Hinweis:** Wenn Sie den Zugriff verwalten oder neuen Zugriff für Benutzer mithilfe von IAM-Richtlinien erteilen möchten, müssen Sie der Kontoeigner, der Administrator für alle Services im Konto oder der Administrator für den betreffenden Service oder die betreffende Serviceinstanz sein. 

Als **Kontoeigner** oder als **{{site.data.keyword.mon_full_notm}}-Serviceadministrator** müssen Sie über die Berechtigungen zum Ausführen der folgenden Plattformaktionen verfügen: 

* Anderen Kontomitgliedern Zugriff auf die Arbeit mit dem Service erteilen
* Eine Serviceinstanz bereitstellen
* Eine Serviceinstanz löschen
* Details einer Serviceinstanz anzeigen
* Eine Service-ID erstellen

Als **DevOps-Benutzer** müssen Sie über die Berechtigungen zum Ausführen der folgenden Plattformaktionen verfügen: 

* Eine Serviceinstanz bereitstellen
* Eine Serviceinstanz löschen
* Details einer Serviceinstanz anzeigen
* Eine Service-ID erstellen


## Berechtigungen für einen Benutzer erteilen, um Administrator des Service im {{site.data.keyword.cloud_notm}}-Konto zu werden
{: #admin_account}

Um einem Benutzer die Administratorrolle für die Verwaltung des Service im Konto zu erteilen, muss der Benutzer über eine IAM-Richtlinie für den {{site.data.keyword.mon_full_notm}}-Service mit der Plattformrolle **Administrator** verfügen. Sie müssen diesen Benutzerzugriff auf eine einzelne Ressource im Konto zuordnen. 

Führen Sie die folgenden Schritte aus, um einem Benutzer die Administratorrolle für den {{site.data.keyword.mon_full_notm}}-Service im Konto zuzuordnen: 

1. Klicken Sie in der Menüleiste auf **Verwalten** &gt; **Zugriff (IAM)** und wählen Sie dann **Benutzer** aus.
2. Wählen Sie in der Zeile für den Benutzer, dem Sie Zugriff zuweisen möchten, das Menü **Aktionen** aus und klicken Sie dann auf **Zugriff zuweisen**.
3. Wählen Sie **Zugriff auf Ressourcen zuweisen** aus.
4. Wählen Sie **{{site.data.keyword.mon_full_notm}}** aus.
5. Wählen Sie **Alle aktuellen Regionen** aus.
6. Wählen Sie **Alle aktuellen Serviceinstanzen** aus.
7. Wählen Sie die Plattformrolle **Administrator** aus.
8. Klicken Sie auf "Zuweisen".


## Berechtigungen für einen Benutzer erteilen, um Administrator des Service innerhalb einer Ressourcengruppe zu werden
{: #admin_rg}

Um einem Benutzer die Administratorrolle für die Verwaltung von Instanzen innerhalb einer Ressourcengruppe im Konto zu erteilen, muss der Benutzer über eine IAM-Richtlinie für den {{site.data.keyword.mon_full_notm}}-Service mit der Plattformrolle **Administrator** im Kontext der Ressourcengruppe verfügen. 

Führen Sie die folgenden Schritte aus, um dem {{site.data.keyword.mon_full_notm}}-Service im Kontext einer Ressourcengruppe eine Benutzeradministratorrolle zuzuordnen: 

1. Klicken Sie in der Menüleiste auf **Verwalten** &gt; **Zugriff (IAM)** und wählen Sie dann **Benutzer** aus.
2. Wählen Sie in der Zeile für den Benutzer, dem Sie Zugriff zuweisen möchten, das Menü **Aktionen** aus und klicken Sie dann auf **Zugriff zuweisen**.
3. Wählen Sie **Zugriff in einer Ressourcengruppe zuweisen** aus.
4. Wählen Sie eine Ressourcengruppe aus.
5. Wenn dem Benutzer noch keine Rolle für die ausgewählte Ressourcengruppe erteilt wurde, wählen Sie eine Rolle aus dem Feld **Zugriff für eine Ressourcengruppe zuweisen** aus. 

    Je nachdem, welche Rolle Sie auswählen, kann der Benutzer die Ressourcengruppe in seinem Dashboard anzeigen, den Namen der Ressourcengruppe bearbeiten oder den Benutzerzugriff auf die Gruppe verwalten. 
    
    Sie können **Kein Zugriff** auswählen, wenn der Benutzer ausschließlich Zugriff auf den {{site.data.keyword.mon_full_notm}}-Service in der Ressourcengruppe haben soll.

6. Wählen Sie **{{site.data.keyword.mon_full_notm}}** aus.
7. Wählen Sie die Plattformrolle **Administrator** aus.
8. Klicken Sie auf **Zuweisen**.


## Berechtigungen für einen DevOps-Benutzer erteilen, um den Service im {{site.data.keyword.cloud_notm}}-Konto zu verwalten
{: #devops_account}

Sie müssen über eine IAM-Richtlinie für den {{site.data.keyword.mon_full_notm}}-Service mit der Plattformrolle **Editor** verfügen.

Führen Sie die folgenden Schritte aus, um einem Benutzer die Editorrolle für den {{site.data.keyword.mon_full_notm}}-Service im Konto zuzuordnen: 

1. Klicken Sie in der Menüleiste auf **Verwalten** &gt; **Zugriff (IAM)** und wählen Sie dann **Benutzer** aus.
2. Wählen Sie in der Zeile für den Benutzer, dem Sie Zugriff zuweisen möchten, das Menü **Aktionen** aus und klicken Sie dann auf **Zugriff zuweisen**.
3. Wählen Sie **Zugriff auf Ressourcen zuweisen** aus.
4. Wählen Sie **{{site.data.keyword.mon_full_notm}}** aus.
5. Wählen Sie **Alle Serviceinstanzen** aus.
6. Wählen Sie die Plattformrolle **Editor** aus.
7. Klicken Sie auf "Zuweisen".

## Berechtigungen für einen DevOps-Benutzer erteilen, um eine Instanz im {{site.data.keyword.cloud_notm}}-Konto zu verwalten
{: #devops_account_instance}

Führen Sie die folgenden Schritte aus, um einem Benutzer die Editorrolle für eine Instanz des {{site.data.keyword.mon_full_notm}}-Service im Konto zuzuordnen: 

1. Klicken Sie in der Menüleiste auf **Verwalten** &gt; **Zugriff (IAM)** und wählen Sie dann **Benutzer** aus.
2. Wählen Sie in der Zeile für den Benutzer, dem Sie Zugriff zuweisen möchten, das Menü **Aktionen** aus und klicken Sie dann auf **Zugriff zuweisen**.
3. Wählen Sie **Zugriff auf Ressourcen zuweisen** aus.
4. Wählen Sie **{{site.data.keyword.mon_full_notm}}** aus.
5. Wählen Sie die Instanz aus.
6. Wählen Sie die Plattformrolle **Editor** aus.
7. Klicken Sie auf "Zuweisen".



## Berechtigungen für einen DevOps-Benutzer erteilen, um den Service innerhalb einer Ressourcengruppe zu verwalten
{: #devops_rg}

Sie müssen über eine IAM-Richtlinie für den {{site.data.keyword.mon_full_notm}}-Service mit der Plattformrolle **Editor** verfügen.

Führen Sie die folgenden Schritte aus, um einem Benutzer die Editorrolle für den {{site.data.keyword.mon_full_notm}}-Service im Kontext einer Ressourcengruppe zuzuordnen: 

1. Klicken Sie in der Menüleiste auf **Verwalten** &gt; **Zugriff (IAM)** und wählen Sie dann **Benutzer** aus.
2. Wählen Sie in der Zeile für den Benutzer, dem Sie Zugriff zuweisen möchten, das Menü **Aktionen** aus und klicken Sie dann auf **Zugriff zuweisen**.
3. Wählen Sie **Zugriff in einer Ressourcengruppe zuweisen** aus.
4. Wählen Sie eine Ressourcengruppe aus.
5. Wenn dem Benutzer noch keine Rolle für die ausgewählte Ressourcengruppe erteilt wurde, wählen Sie eine Rolle aus dem Feld **Zugriff für eine Ressourcengruppe zuweisen** aus. 

    Je nachdem, welche Rolle Sie auswählen, kann der Benutzer die Ressourcengruppe in seinem Dashboard anzeigen, den Namen der Ressourcengruppe bearbeiten oder den Benutzerzugriff auf die Gruppe verwalten. 
    
    Sie können **Kein Zugriff** auswählen, wenn der Benutzer ausschließlich Zugriff auf den {{site.data.keyword.mon_full_notm}}-Service in der Ressourcengruppe haben soll.

6. Wählen Sie **{{site.data.keyword.mon_full_notm}}** aus.
7. Wählen Sie die Plattformrolle **Editor** aus.
8. Klicken Sie auf **Zuweisen**.

## Berechtigungen zum Verwalten von Metriken und zum Konfigurieren von Alerts in Sysdig erteilen
{: #admin_user_sysdig}

Sie müssen als **Benutzer mit Administratorberechtigung** in Sysdig über die Berechtigungen zum Ausführen der folgenden Aktionen verfügen: 

* Metrikquellen hinzufügen
* Metriken anzeigen
* Metriken suchen
* Metriken filtern
* Alerts konfigurieren

Daher benötigen Sie die folgenden Richtlinien:

* Eine IAM-Richtlinie für den {{site.data.keyword.mon_full_notm}}-Service mit der Plattformrolle **Editor**. Mit dieser Richtlinie können Sie die Serviceinstanzdetails über die Befehlszeile und im {{site.data.keyword.cloud_notm}}-Dashboard anzeigen.
* Eine IAM-Richtlinie für den {{site.data.keyword.mon_full_notm}}-Service mit der Servicerolle **Manager**. Diese Richtlinie ermöglicht es Ihnen, Metriken zu überwachen, zu filtern und zu durchsuchen sowie Alerts über die Sysdig-Webbenutzerschnittstelle zu definieren.

**Hinweis:** Wenn Sie als Administrator des Service einem Benutzer diese Richtlinien erteilen, sollten Sie dies im Kontext einer Ressourcengruppe in Betracht ziehen. Eine {{site.data.keyword.mon_full_notm}}-Instanz wird im Kontext einer Ressourcengruppe bereitgestellt. Daher sollten Sie Zugriffsberechtigungen im Kontext der Ressourcengruppe erteilen.


Führen Sie die folgenden Schritte aus, um einem Benutzer beide Richtlinien für den {{site.data.keyword.mon_full_notm}}-Service im Kontext einer Ressourcengruppe zuzuordnen: 

1. Klicken Sie in der Menüleiste auf **Verwalten** &gt; **Zugriff (IAM)** und wählen Sie dann **Benutzer** aus.
2. Wählen Sie in der Zeile für den Benutzer, dem Sie Zugriff zuweisen möchten, das Menü **Aktionen** aus und klicken Sie dann auf **Zugriff zuweisen**.
3. Wählen Sie **Zugriff in einer Ressourcengruppe zuweisen** aus.
4. Wählen Sie eine Ressourcengruppe aus.
5. Wenn dem Benutzer noch keine Rolle für die ausgewählte Ressourcengruppe erteilt wurde, wählen Sie eine Rolle aus dem Feld **Zugriff für eine Ressourcengruppe zuweisen** aus. 

    Je nachdem, welche Rolle Sie auswählen, kann der Benutzer die Ressourcengruppe in seinem Dashboard anzeigen, den Namen der Ressourcengruppe bearbeiten oder den Benutzerzugriff auf die Gruppe verwalten. 
    
    Sie können **Kein Zugriff** auswählen, wenn der Benutzer ausschließlich Zugriff auf den {{site.data.keyword.mon_full_notm}}-Service in der Ressourcengruppe haben soll.

6. Wählen Sie **{{site.data.keyword.mon_full_notm}}** aus.
7. Wählen Sie die Plattformrolle **Editor** aus.
8. Wählen Sie die Servicerolle **Manager** aus.
8. Klicken Sie auf **Zuweisen**.

## Einem Benutzer Berechtigungen erteilen, um Metriken in Sysdig anzuzeigen
{: #user_sysdig}

Sie benötigen als **Benutzer**, **Prüfer** oder **Entwickler** möglicherweise Berechtigungen, um die folgenden Aktionen auszuführen: 

* Metriken anzeigen
* Metriken suchen
* Metriken filtern

Daher benötigen Sie die folgenden Richtlinien:

* Eine IAM-Richtlinie für den {{site.data.keyword.mon_full_notm}}-Service mit der Plattformrolle **Anzeigeberechtigter**. Mit dieser Richtlinie können Sie die Serviceinstanzdetails über die Befehlszeile und im {{site.data.keyword.cloud_notm}}-Dashboard anzeigen.
* Eine IAM-Richtlinie für den {{site.data.keyword.mon_full_notm}}-Service mit der Servicerolle **Schreibberechtigter**. Diese Richtlinie ermöglicht es Ihnen, Metriken über die Sysdig-Webbenutzerschnittstelle anzuzeigen, zu filtern und zu durchsuchen.

**Hinweis:** Wenn Sie als Administrator des Service einem Benutzer diese Richtlinien erteilen, sollten Sie dies im Kontext einer Ressourcengruppe in Betracht ziehen. Eine {{site.data.keyword.mon_full_notm}}-Instanz wird im Kontext einer Ressourcengruppe bereitgestellt. Daher sollten Sie Zugriffsberechtigungen im Kontext der Ressourcengruppe erteilen.

Führen Sie die folgenden Schritte aus, um einem Benutzer beide Richtlinien für den {{site.data.keyword.mon_full_notm}}-Service im Kontext einer Ressourcengruppe zuzuordnen: 

1. Klicken Sie in der Menüleiste auf **Verwalten** &gt; **Zugriff (IAM)** und wählen Sie dann **Benutzer** aus.
2. Wählen Sie in der Zeile für den Benutzer, dem Sie Zugriff zuweisen möchten, das Menü **Aktionen** aus und klicken Sie dann auf **Zugriff zuweisen**.
3. Wählen Sie **Zugriff in einer Ressourcengruppe zuweisen** aus.
4. Wählen Sie eine Ressourcengruppe aus.
5. Wenn dem Benutzer noch keine Rolle für die ausgewählte Ressourcengruppe erteilt wurde, wählen Sie eine Rolle aus dem Feld **Zugriff für eine Ressourcengruppe zuweisen** aus. 

    Je nachdem, welche Rolle Sie auswählen, kann der Benutzer die Ressourcengruppe in seinem Dashboard anzeigen, den Namen der Ressourcengruppe bearbeiten oder den Benutzerzugriff auf die Gruppe verwalten. 
    
    Sie können **Kein Zugriff** auswählen, wenn der Benutzer ausschließlich Zugriff auf den {{site.data.keyword.mon_full_notm}}-Service in der Ressourcengruppe haben soll.

6. Wählen Sie **{{site.data.keyword.mon_full_notm}}** aus.
7. Wählen Sie die Plattformrolle **Anzeigeberechtigter** aus.
8. Wählen Sie die Servicerolle **Schreibberechtigter** aus.
8. Klicken Sie auf **Zuweisen**.

