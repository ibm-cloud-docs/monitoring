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

# Traitement des incidents pour {{site.data.keyword.mon_full_notm}}
{: #troubleshoot}

Informations sur les problèmes généraux que vous pourriez rencontrer lorsque vous utilisez le service {{site.data.keyword.mon_full_notm}}. Dans de nombreux cas, ces problèmes peuvent être résolus en quelques opérations simples.
{:shortdesc}

## Obtenez-vous une erreur lorsque vous créez une capture ?
{: #troubleshoot-entry-1}

Vous ne parvenez pas à créer un [fichier de capture](/docs/services/Monitoring-with-Sysdig/captures.html#captures) pour un hôte dans votre infrastructure. 

Dans la section *Captures* de l'interface utilisateur Web, vous obtenez une erreur lorsque vous tentez de créer un fichier de capture pour un hôte.
{: tsSymptoms}

La fonction **sysdig_capture_enabled** est définie sur *false* pour l'agent Sysdig qui s'exécute sur l'hôte.
{: tsCauses}

Activez la fonction **sysdig_capture_enabled** dans l'agent Sysdig qui s'exécute sur l'hôte.
{: tsResolve}


## Est-ce que le statut de votre fichier de capture est défini sur *requested* (demandé) et ne passe pas à l'état *uploaded* (téléchargé) ?
{: #troubleshoot-entry-2}

Le statut d'un [fichier de capture](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures) est défini sur *requested* (demandé) et ne passe pas à l'état *uploaded* (téléchargé). Vous attendez que le fichier de capture soit disponible pour l'analyse.

Dans la section *Captures* de l'interface utilisateur Web, le statut du fichier de capture pour un hôte ne devient pas *uploaded* (téléchargé).
{: tsSymptoms}

Le port TCP 6443 est désactivé sur l'hôte.
{: tsCauses}


Vérifiez que le port 6443 est ouvert. Pour plus d'informations, voir [Gestion du trafic réseau](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-network#network_send).
{: tsResolve}


