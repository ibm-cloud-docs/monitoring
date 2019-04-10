---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-18"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# Personnalisation de l'agent Sysdig pour le contrôle des données
{: #customize_agent}

Par défaut, l'agent Sysdig collecte des données provenant d'une large gamme de plateformes et d'applications. Vous pouvez éditer le fichier de configuration de l'agent pour modifier son comportement par défaut et inclure ou exclure des données. Vous pouvez personnaliser le fichier de configuration de l'agent Sysdig pour inclure des métriques personnalisées telles que JMX, StatsD et Prometheus. Vous pouvez également filtrer les métriques, les données d'événement et les conteneurs.
{:shortdesc}

## Personnalisation de l'agent Sysdig Kubernetes
{: #kube}

L'agent Sysdig Kubernetes utilise deux fichiers de configuration qui indiquent les données à collecter automatiquement :

| Nom de fichier                        | Actions           |
|----------------------------------|-------------------|
| `sysdig-agent-daemonset-v2.yaml` | Modification du niveau de journalisation. |
| `sysdig-agent-configmap.yaml`    | Blocage de ports. </br>Inclusion ou exclusion de données de métriques. </br>Ajout ou suppression d'événements. </br>Filtrage de conteneurs. |
{: caption="Tableau 1. Fichiers de configuration de l'agent Sysdig Kubernetes" caption-side="top"} 

Pour modifier un agent Sysdig Kubernetes, vous devrez peut-être éditer le fichier *sysdig-agent-configmap.yaml* et/ou le
fichier *sysdig-agent-daemonset-v2.yaml*.

Vous pouvez modifier un fichier de configuration de deux façons :
* Méthode 1 : Modification du fichier directement sur le cluster où l'agent est en cours d'exécution. Pour plus d'informations, voir [Modification de la configuration de l'agent Sysdig Kubernetes à l'aide de kubectl edit](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_edit_kube_agent_method1).
* Méthode 2 : Modification du fichier localement et application des modifications au cluster. Pour plus d'informations, voir [Modification de la configuration de l'agent Sysdig Kubernetes à l'aide de kubectl apply](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_edit_kube_agent_method2).

Vous pouvez ajouter des étiquettes aux données collectées par l'agent. 
* Utilisez ces étiquettes pour gérer plus facilement les données que vous surveillez. 

    * Utilisez des libellés pour regrouper des ressources d'infrastructure en hiérarchies logiques, filtrer des données et fractionner les données agrégées en segments. 
    
    * Personnalisez l'agrégation des données lorsque vous configurez un graphique ou créez une alerte pour une métrique. 
    
    * Définissez la portée d'un tableau de bord, d'un panneau ou d'une alerte pour filtrer des points de données. 
    
    * Limitez l'accès aux données en gérant l'accès aux données des utilisateurs via des équipes. 
    
    * Pour plus d'informations sur la gestion des données, voir [Gestion des données](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-manage#manage).

* Pour plus d'informations sur l'ajout d'étiquettes, voir [Ajout d'étiquettes supplémentaires aux données collectées à partir d'un agent Sysdig Kubernetes](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_add_tags). 


**Vous pouvez personnaliser les données collectées par l'agent Sysdig.** 

Lorsque vous excluez des événements, des métriques et des conteneurs, prenez en compte les informations suivantes :
* Vous pouvez réduire la charge de l'agent et du système de back end.
* Vous collectez uniquement les données provenant des conteneurs que vous souhaitez surveiller.
* Vous pouvez maîtriser les coûts en signalant les conteneurs importants et en filtrant les conteneurs inutiles ou non essentiels.
* Vous pouvez configurer les événements Kubernetes que vous souhaitez surveiller. Pour plus d'informations, voir [Collecte d'un ensemble d'événements Kubernetes](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_collect_events).

La liste suivante indique les actions que vous pouvez exécuter pour contrôler les données collectées par l'agent Sysdig :
* [Désactivation de la collecte d'événements](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_disable_events)
* [Inclusion et exclusion de métriques](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_inc_exc_metrics)
* [Filtrage de conteneurs et d'objets Kubernetes à partir desquels les données sont collectées](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_filter_data)
* [Blocage de ports](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_block_ports)
* [Filtrage des événements Kubernetes par gravité](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_filterby_severity)

Vous pouvez également personnaliser le type de journal et les entrées collectées. Pour plus d'informations, voir [Modification du niveau de journalisation](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_log_level).

Vous pouvez également consigner la liste des métriques pour lesquelles l'agent génère des données de rapport. Pour plus d'informations, voir [Journalisation des métriques incluses ou exclues dans un fichier](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_kube_agent#change_kube_agent_log_metrics).

L'agent Sysdig génère des entrées de journal dans */opt/draios/logs/draios.log*. 
* Le fichier journal pivote lorsque sa taille atteint 10 Mo.
* Les 10 derniers fichiers journaux sont conservés. L'horodatage qui est ajouté au nom de fichier permet de déterminer les fichiers à conserver.
* Les niveaux de journalisation valides sont les suivants : *none*, *error*, *warning*, *info*, *debug*, *trace*.
* Le niveau de journalisation par défaut est *info*, où une entrée est créée pour chaque transmission de métriques agrégées aux serveurs de back end, sur la base d'une par seconde, outre les entrées pour les avertissements et les erreurs.

Le tableau suivant répertorie certains scénarios courants, ainsi que la valeur que vous devez définir dans chacun d'eux :

| Cas d'utilisation                                     | Entrée de section de journal           |
|-----------------------------------------------|-----------------------------|
| Traitement des incidents liés au comportement de l'agent                   | `file_priority: debug`      |
| Réduction de la sortie de la console de conteneur               | `console_priority: warning` |
| Filtrage des événements par gravité                  | `event_priority: warning`   |
| Vérification de l'inclusion ou de l'exclusion de métriques  | `metrics_excess_log: true`  |

## Agent Sysdig de conteneur
{: #container}


La liste suivante indique les actions que vous pouvez exécuter pour contrôler les données collectées par l'agent Sysdig :
* [Désactivation de la collecte d'événements](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_disable_events)
* [Inclusion et exclusion de métriques](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_inc_exc_metrics)
* [Filtrage des conteneurs à partir desquels les données sont collectées](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_collect_docker_events)
* [Blocage de ports](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_block_ports)
* [Filtrage des événements par gravité](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_filterby_severity)

Vous pouvez également personnaliser le type de journal et les entrées collectées. Pour plus d'informations, voir [Modification du niveau de journalisation](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_container_agent#change_container_agent_log_level).



## Agent Sysdig Linux
{: #linux}

L'agent Sysdig Linux utilise deux fichiers de configuration qui indiquent les données à collecter automatiquement :

| Fichier                   | Description                                                     | Emplacement                                |
|------------------------|-----------------------------------------------------------------|-----------------------------------------|
| `dragent.default.yaml` | Fichier de configuration principal </br>**Remarque :****Ne modifiez pas ce fichier.  | `/opt/draios/etc/dragent.default.yaml`  |
| `dragent.yaml`         | Fichier de configuration que vous modifiez pour personnaliser l'agent Sysdig. | `/opt/draios/etc/dragent.yaml`          |
{: caption="Tableau 1. Fichiers de configuration de l'agent Sysdig" caption-side="top"} 

Vous pouvez éditer le fichier *dragent.yaml* pour personnaliser les données collectées. Les modifications sont immédiatement prises en compte après la sauvegarde du fichier. L'agent détecte la modification et redémarre automatiquement. Le fichier *dragent.default.yaml* indique la fréquence à laquelle un agent Sysdig vérifie les fichiers, ainsi que le nom de ces derniers. Pour plus d'informations, voir [Edition du fichier yaml dragent](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_linux_agent#change_linux_agent_edit_agent).

Par exemple, *dragent.default.yaml* inclut les informations suivantes :

```
check_frequency_s: 5
files:
- /opt/draios/etc/dragent.yaml
- /opt/draios/etc/kubernetes/config/dragent.yaml
- /opt/draios/etc/kubernetes/secrets/access-key
```
{: screen}

La liste suivante indique les actions que vous pouvez exécuter pour contrôler les données collectées par l'agent Sysdig :
* [Inclusion et exclusion de métriques](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_linux_agent#change_linux_agent_inc_exc_metrics)
* [Blocage de ports](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_linux_agent#change_linux_agent_block_ports)

Vous pouvez également personnaliser le type de journal et les entrées collectées. Pour plus d'informations, voir [Modification du niveau de journalisation](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-change_linux_agent#change_linux_agent_log_level).


