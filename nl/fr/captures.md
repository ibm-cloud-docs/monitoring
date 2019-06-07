---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, captures

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

# Gestion des captures
{: #captures}

Une capture est un fichier de trace que vous pouvez générer pour analyser les événements qui se produisent sur un hôte pendant une période donnée. Par exemple, vous pouvez l'utiliser pour analyser les goulots d'étranglement ou les interactions de composants. Le service {{site.data.keyword.mon_full_notm}} vous permet de créer, d'explorer, de télécharger et de supprimer des *captures* pour des noeuds individuels. 
{:shortdesc}

Pour plus d'informations, voir [Captures](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-captures#captures).


## Création d'une capture
{: #captures_create}

Une capture est créée dans la vue *Explorer*.

Pour créer un fichier de capture, procédez comme suit :

1. Accédez à la section *EXPLORE* dans l'interface utilisateur Web. [En savoir plus](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch).

2. Cliquez sur l'icône de changement d'hôte ![Icône de changement d'hôte](images/switch_hosts.png).

3. Sélectionnez un hôte ou un conteneur.

4. Cliquez sur l'icône Actions ![Icône des trois points](images/actions.png) et sélectionnez **Sysdig capture**.

    La fenêtre *Sysdig Capture* s'ouvre.

5. Dans la fenêtre *Sysdig Capture*, définissez les paramètres suivants :

    1. Dans la zone *Capture path and name*, saisissez le nom du fichier de capture. Vous pouvez laisser la valeur par défaut ou la modifier. Le nom par défaut comprend la date et l'heure auxquelles la capture est créée. 

    2. Définissez une *Période* pour indiquer le nombre de secondes pendant lequel collecter des données. La durée de capture par défaut est 15 secondes. La durée de capture maximale est 86 400 secondes (24 heures). 

    3. (Facultatif) Ajoutez un filtre pour limiter la quantité d'informations de trace collectées. 

6. Cliquez sur **Start capture**. L'agent Sysdig reçoit l'instruction de démarrer une capture et renvoie le fichier de trace généré. 

7. Cliquez sur **Go to captures page** pour afficher la liste des captures dans la section *Captures* de l'interface utilisateur Web. 

La page *Captures* affiche un tableau qui répertorie le nom du fichier de capture, l'hôte à partir duquel il a été extrait, la période et la taille de la capture. 

Le statut d'un fichier de capture peut être l'un des suivants :
* `Demandé` : un fichier est en cours de génération.
* `Téléchargé` : un fichier est disponible pour téléchargement et analyse.
* `Erreur` : un fichier n'est pas disponible en raison d'un dépassement de délai, de données qui n'ont jamais été reçues ou d'une erreur de l'agent.



## Suppression d'une capture
{: #captures_delete}

Pour supprimer un fichier de capture, procédez comme suit :

1. Accédez à la section *CAPTURES* dans l'interface utilisateur Web. [En savoir plus](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch).
2. Identifiez et sélectionnez le fichier de capture que vous voulez supprimer.
3. Cliquez sur **Supprimer**.



## Exploration d'une capture
{: #captures_explore}

Pour explorer un fichier de capture, procédez comme suit :

1. Accédez à la section *CAPTURES* dans l'interface utilisateur Web. [En savoir plus](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch).
2. Identifiez et sélectionnez le fichier de capture contenant les données de l'hôte que vous voulez analyser.
3. Cliquez sur **EXPLORE**.



## Téléchargement d'une capture
{: #captures_download}

Pour télécharger un fichier de capture, procédez comme suit :

1. Accédez à la section *CAPTURES* dans l'interface utilisateur Web. [En savoir plus](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch).
2. Identifiez et sélectionnez le fichier de capture contenant les données que vous voulez télécharger.
3. Cliquez sur **TELECHARGER**.


## Chisels
{: #captures_chisels}

Un chisel Sysdig est un script qui est écrit en langage de script Lua. Vous pouvez l'utiliser pour analyser les données d'un fichier de capture. 

Pour plus d'informations, voir [Chisels User Guide ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/draios/sysdig/wiki/Chisels-User-Guide){:new_window}.



## Csysdig
{: #captures_csysdig}

Csysdig est un outil open source pour Linux qui est conçu pour la surveillance et le débogage. Vous pouvez l'utiliser pour analyser des fichiers de capture. 

Pour plus d'informations, consultez les ressources suivantes :
* [Blogue Csysdig ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://sysdig.com/blog/csysdig-explained-visually/){:new_window}
* [Vidéo Csysdig ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.youtube.com/watch?v=UJ4wVrbP-Q8){:new_window}


