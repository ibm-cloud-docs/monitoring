---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, launch web UI

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

# Zur Webbenutzerschnittstelle navigieren
{: #launch}

Nachdem Sie eine Instanz des {{site.data.keyword.mon_full_notm}}-Service in {{site.data.keyword.Bluemix}} bereitgestellt und einen Sysdig-Agenten für eine Metrikquelle konfiguriert haben, können Sie Metriken über die {{site.data.keyword.mon_full_notm}}-Webbenutzerschnittstelle anzeigen, überwachen und verwalten.
{:shortdesc}


## Einem Benutzer IAM-Richtlinien zum Anzeigen von Daten erteilen 
{: #launch_step1}

**Hinweis:** Sie müssen Administrator des {{site.data.keyword.mon_full_notm}}-Service oder Administrator der {{site.data.keyword.mon_full_notm}}-Instanz sein oder über IAM-Berechtigungen für das Konto besitzen, um anderen Benutzern Richtlinien zu erteilen.

In der folgenden Tabelle sind die Mindestrichtlinien aufgelistet, die ein Benutzer haben muss, um die {{site.data.keyword.mon_full_notm}}-Webbenutzerschnittstelle starten und Daten anzeigen zu können:

| Service                        | Rolle                      | Erteilte Berechtigung     |
|--------------------------------|---------------------------|------------------------|
| `{{site.data.keyword.mon_full_notm}}` | Plattformrolle: Anzeigeberechtigter     | Ermöglicht es dem Benutzer, die Liste der Serviceinstanzen im Monitoring-Dashboard "Beobachtbarkeit" anzuzeigen. |
| `{{site.data.keyword.mon_full_notm}}` | Servicerolle: Schreibberechtigter      | Ermöglicht es dem Benutzer, die Webbenutzerschnittstelle zu starten und Metriken in der Webbenutzerschnittstelle anzuzeigen.  |
{: caption="Tabelle 1. IAM-Richtlinien" caption-side="top"} 

Weitere Informationen zum Konfigurieren dieser Richtlinien für einen Benutzer finden Sie im Abschnitt [Berechtigungen für einen Benutzer zum Anzeigen von Metriken erteilen](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-iam_work#user_sysdig).


## Die Webbenutzerschnittstelle über die {{site.data.keyword.cloud_notm}}-Benutzerschnittstelle starten
{: #launch_step2}

Sie starten die Webbenutzerschnittstelle im Kontext einer {{site.data.keyword.mon_full_notm}}-Instanz über die {{site.data.keyword.cloud_notm}}-Benutzerschnittstelle. 

Führen Sie die folgenden Schritte aus, um die Webbenutzerschnittstelle zu starten:

1. Melden Sie sich bei Ihrem {{site.data.keyword.cloud_notm}}-Konto an.

    Klicken Sie auf das [{{site.data.keyword.cloud_notm}}-Dashboard ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/login){:new_window}, um das {{site.data.keyword.cloud_notm}}-Dashboard zu starten.

	Nachdem Sie sich mit Ihrer Benutzer-ID und Ihrem Kennwort angemeldet haben, wird das {{site.data.keyword.cloud_notm}}-Dashboard geöffnet.

2. Wählen Sie im Navigationsmenü die Option **Beobachtbarkeit** aus. 

3. Wählen Sie **Überwachung** aus. 

    Die Liste der Instanzen, die unter {{site.data.keyword.cloud_notm}} verfügbar sind, wird angezeigt.

4. Wählen Sie eine Instanz aus. Klicken Sie dann auf **Sysdig anzeigen**.

Die Webbenutzerschnittstelle wird geöffnet.


