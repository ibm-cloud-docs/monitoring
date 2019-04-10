---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, pricing

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


# Tarification
{: #pricing_plans}

Différents plans de tarification sont disponibles pour une instance {{site.data.keyword.mon_full_notm}}.
{:shortdesc}
 

| Plans            | Niveau         | Collecte des données  |
|------------------|--------------|------------------|
| `Essai`          |              | Les données sont collectées pour un maximum de 20 conteneurs par noeud ou pour 200 métriques personnalisées par noeud pendant 30 jours uniquement. |
| `Niveau gradué` | `De base`      | Les données sont collectées pour un maximum de 20 conteneurs par noeud ou pour 200 métriques personnalisées par noeud. |
| `Niveau gradué` | `Pro`        | Les données sont collectées pour un maximum de 50 conteneurs par noeud ou pour 500 métriques personnalisées par noeud. |
| `Niveau gradué` | `Avancé`   | Les données sont collectées pour un maximum de 110 conteneurs par noeud ou pour 1000 métriques personnalisées par noeud. |
{: caption="Tableau 1. Liste des plans de service" caption-side="top"} 


**Remarque :** Un noeud peut être un hôte, un conteneur, une machine virtuelle, un serveur bare metal, ou une source de métriques sur laquelle vous installez un agent Sysdig.

Lorsque le nombre de conteneurs par noeud ou le nombre de métriques dépasse le seuil du plan de niveau gradué sur une période, la détection automatique de niveau est appliquée. Une notification d'alerte est déclenchée en fonction de la configuration de votre notification de facturation d'utilisation si vous activez l'alerte  **[{{site.data.keyword.IBM_notm}}]: Usage Tier Change**.

Vous pouvez demander un **devis personnalisé** pour tous les éléments au-delà du *Plan de tarification avancé pour un niveau gradué payant* en ouvrant un ticket auprès du [Support IBM Cloud ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/unifiedsupport/supportcenter){:new_window}.
{: tip}

Les données sont collectées et conservées selon les instructions standard sur tous les plans. Pour plus d'informations, voir [Collecte de données](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-about#overview_collection) et [Conservation de données](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-about#overview_retention).


## Vérification de votre utilisation
{: #pricing_usage}

Pour surveiller la façon dont le service {{site.data.keyword.mon_full_notm}} est utilisé et les coûts associés à cette utilisation, voir
[Affichage de votre utilisation](/docs/billing-usage?topic=billing-usage-viewingusage#viewingusage).



## Activation de l'alerte avertissant d'un changement de niveau
{: #pricing_alert}

Pour être averti lors d'un changement de niveau, vous devez activer l'alerte suivante : **[{{site.data.keyword.IBM_notm}}]: Usage Tier Change**.

Pour activer une alerte, procédez comme suit :

1. Lancez l'interface utilisateur Web. Pour plus d'informations sur le lancement de l'interface utilisateur Web,
voir [Accès à l'interface utilisateur Web](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-launch#launch). 
2. Créez un canal de notification. Pour plus d'informations, voir [Configuration d'un canal de notification](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-notifications#notifications_create). 
3. Cliquez sur **ALERTS** pour accéder à la section *Alerts*.
2. Recherchez **[IBM]: Usage Tier Change**.
3. Editez l'alerte pour ajouter le canal de notification.
4. Cliquez sur **Save**.



## Génération d'alerte de plan de service
{: #pricing_how}

Pour être averti lors d'un changement de niveau, vous devez activer l'alerte suivante : **[{{site.data.keyword.IBM_notm}}]: Usage Tier Change**.

**Remarque :** Lorsque vous activez cette alerte, vous devez indiquer les canaux de notification sur lesquels vous souhaitez être averti.

L'utilisation est calculée en tant que moyenne du nombre de noeuds et de métriques échantillonnés toutes les 10 secondes au cours de l'heure précédente. Les petites fluctuations à court terme ne sont pas prises en compte. Il existe une différence entre l'utilisation précédente et l'utilisation actuelle une fois par heure.

Les seuils sont définis de la manière suivante :

``` 
usageTiers {
  containerDensity {
    Basic = [0, 20]
    Pro = [21, 50]
    Advanced = [51, 100]
  }
  metricDensity {
    Basic = [0, 200]
    Pro = [201, 500]
    Advanced = [501, 1000]
}
```
{: screen}

La notification d'alerte est générée comme suit :
1. Si le nombre de conteneurs par noeud dans un niveau augmente, un événement personnalisé est généré toutes les heures.
2. La condition d'alerte recherche les événements personnalisés qui vous informent de la présence de modifications dans le nombre de conteneurs par noeud. Si elle trouve un événement où le nombre de conteneurs dans un niveau augmente depuis le dernier calcul de l'utilisation, elle envoie une notification.

La fréquence de l'alerte est d'une par heure. Pour un noeud présentant des fluctuations, la fréquence de l'alerte est portée à toutes les deux heures au maximum.

Notez que l'alerte est uniquement générée si un noeud passe du niveau *De base* au niveau *Pro* ou *Avancé*. 



### Exemples
{: #pricing_examples}

**Exemple 1** 

Si le nombre moyen de conteneurs est le suivant : 

| Heure     | Nombre de conteneurs | Description                                                                   | Génération d'une alerte ? |
|----------|----------------------|-------------------------------------------------------------------------------|------------------------|
| 10:00    | 18                   | Le niveau est défini sur **De base**.                                                     | Non                     |
| 11:00    | 21                   | Le nombre de conteneurs est supérieur au niveau *De base*. Le niveau passe au niveau **Pro**.            | Oui                    |
| 12:00    | 19                   | Le nombre de conteneurs est inférieur au niveau *De base*. Le niveau repasse au niveau **De base**.     | Non                    |
| 13:00    | 20                   | Aucun changement de niveau. Le niveau est défini sur **De base**.                                     | Non                     |
{: caption="Tableau 2. Exemple 1" caption-side="top"} 


**Exemple 2**

Si le nombre moyen de conteneurs est le suivant : 

| Heure     | Nombre de conteneurs | Description                                                                   | Génération d'une alerte ? |
|----------|----------------------|-------------------------------------------------------------------------------|------------------------|
| 10:00    | 15                   | Le niveau est défini sur **De base**.                                                     | Non                     |
| 11:00    | 19                   | Le niveau est défini sur **De base**.                                                     | Non                     |
| 12:00    | 20                   | Le niveau est défini sur **De base**.                                                     | Non                    |
| 13:00    | 21                   | Le nombre de conteneurs est supérieur au niveau *De base*. Le niveau passe au niveau **Pro**.            | Oui                     |
{: caption="Tableau 3. Exemple 2" caption-side="top"}


**Exemple 3**

Si le nombre moyen de conteneurs est le suivant : 

| Heure     | Nombre de conteneurs | Description                                                                   | Génération d'une alerte ? |
|----------|----------------------|-------------------------------------------------------------------------------|------------------------|
| 10:00    | 15                   | Le niveau est défini sur **De base**.                                                     | Non                     |
| 11:00    | 20                   | Le niveau est défini sur **De base**.                                                     | Non                    |
| 12:00    | 21                   | Le niveau est défini sur **De base**.                                                     | Oui                    |
| 13:00    | 20                   | Le nombre de conteneurs revient au niveau *De base*. Le niveau passe au niveau **Pro**.          | Non                     |
{: caption="Tableau 3. Exemple 3" caption-side="top"}



