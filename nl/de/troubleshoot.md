---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, troubleshooting

subcollection: Sysdig

---

{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# Fehlerbehebung für {{site.data.keyword.mon_full_notm}}
{: #troubleshoot}

Hier erfahren Sie mehr über einige allgemeine Probleme, die bei der Verwendung des {{site.data.keyword.mon_full_notm}}-Service auftreten können. In vielen Fällen können Sie diese Probleme beheben, indem Sie ein paar einfache Schritte ausführen.
{:shortdesc}

## Erhalten Sie einen Fehler beim Erstellen einer Erfassung?
{: #troubleshoot-entry-1}

Es ist nicht möglich, eine [Erfassungsdatei](/docs/services/Monitoring-with-Sysdig/captures.html#captures) für einen Host in Ihrer Infrastruktur zu erstellen. 

Im Abschnitt *Erfassungen* der Webbenutzerschnittstelle erhalten Sie einen Fehler, wenn Sie versuchen, eine Erfassungsdatei für einen Host zu erstellen.
{: tsSymptoms}

Für den Sysdig-Agent, der auf dem Host ausgeführt wird, ist die Funktion **sysdig_capture_enabled** auf *false* festgelegt.
{: tsCauses}

Aktivieren Sie die Funktion **sysdig_capture_enabled** in dem Sysdig-Agenten, der auf dem Host ausgeführt wird.
{: tsResolve}


## Ist der Status Ihrer Erfassungsdatei auf *Angefordert* festgelegt und ändert sich nicht zum Status *Hochgeladen*?
{: #troubleshoot-entry-2}

Der Status einer [Erfassungsdatei](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures) ist auf *Angefordert* festgelegt und ändert sich nicht zum Status *Hochgeladen*. Sie warten darauf, dass die Erfassungsdatei für die Analyse verfügbar wird.

Im Abschnitt *Erfassungen* der Webbenutzerschnittstelle ändert sich der Status der Erfassungsdatei für einen Host nicht zu *Hochgeladen*.
{: tsSymptoms}

Der Host hat den TCP-Port 6443 inaktiviert.
{: tsCauses}


Überprüfen Sie, ob der Port 6443 geöffnet ist. Weitere Informationen finden Sie unter [Netzverkehr verwalten](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-network#network_send).
{: tsResolve}


