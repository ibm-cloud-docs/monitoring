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


# Extraction de l'historique d'une alerte dans Grafana
{: #retrieve_history_grafana}

Dans Grafana, vous pouvez afficher l'historique d'une alerte. 
{:shortdesc}


Pour extraire l'historique d'une alerte, procédez comme suit :

1. Sélectionnez le bouton de basculement de la barre de menus latérale ![Barre de menus latérale de Grafana](images/grafana_settings.gif "Barre de menus latérale de Grafana").
2. Sélectionnez **Dashboards**.
3. Sélectionnez le tableau de bord où l'alerte est définie.
4. Cliquez sur le titre du graphique, puis sélectionnez **edit**.
    
    L'onglet *Metrics* s'ouvre. 

5. Sélectionnez l'onglet **Alert**.
6. Sélectionnez **State history**.

    Chaque entrée répertoriée représente une instance de déclenchement de l'alerte.

![View of a Grafana dashboard with an alert defined on a query](images/alerthistory.png "Vue d'un tableau de bord Grafana avec une alerte définie sur une requête")


