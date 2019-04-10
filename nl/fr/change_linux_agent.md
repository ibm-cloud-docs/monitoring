---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring, customize, linux agent

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

# Personnalisation des agents Sysdig Linux
{: #change_linux_agent}

Par défaut, l'agent Sysdig collecte des données provenant d'une large gamme de plateformes et d'applications. Vous pouvez éditer le fichier de configuration de l'agent pour modifier son comportement par défaut et inclure ou exclure des données. Vous pouvez personnaliser le fichier de configuration de l'agent Sysdig pour inclure des métriques personnalisées telles que JMX, StatsD et Prometheus. Vous pouvez également filtrer les métriques et les conteneurs.
{:shortdesc}

L'agent Sysdig utilise deux fichiers de configuration qui indiquent les données à collecter automatiquement :

| Fichier                   | Description                                                     | Emplacement                                |
|------------------------|-----------------------------------------------------------------|-----------------------------------------|
| `dragent.default.yaml` | Fichier de configuration principal </br>**Remarque :****Ne modifiez pas ce fichier.  | `/opt/draios/etc/dragent.default.yaml`  |
| `dragent.yaml`         | Fichier de configuration que vous modifiez pour personnaliser l'agent Sysdig. | `/opt/draios/etc/dragent.yaml`          |
{: caption="Tableau 1. Fichiers de configuration de l'agent Sysdig" caption-side="top"} 

Vous pouvez éditer le fichier *dragent.yaml* pour personnaliser les données collectées. Les modifications sont immédiatement prises en compte après la sauvegarde du fichier. L'agent détecte la modification et redémarre automatiquement. Le fichier *dragent.default.yaml* indique la fréquence à laquelle un agent Sysdig vérifie les fichiers, ainsi que le nom de ces derniers.

Par exemple, *dragent.default.yaml* inclut les informations suivantes :

```
check_frequency_s: 5
files:
- /opt/draios/etc/dragent.yaml
- /opt/draios/etc/kubernetes/config/dragent.yaml
- /opt/draios/etc/kubernetes/secrets/access-key
```
{: screen}



## Edition du fichier yaml dragent
{: #change_linux_agent_edit_agent}

Le fichier yaml se trouve dans */opt/draios/etc/*.

Pour éditer le fichier et appliquer les modifications, procédez comme suit :

1. Accédez au fichier *dragent.yaml* directement. Il se trouve dans `/opt/draios/etc/dragent.yaml`.
2. Editez le fichier. Utilisez une syntaxe YAML valide.
3. Redémarrez l'agent. Exécutez la commande suivante :

    ```
    service dragent restart
    ```
    {: codeblock}


## Blocage de ports
{: #change_linux_agent_block_ports}

Pour bloquer le trafic réseau et les métriques provenant de ports réseau, vous devez personnaliser la section **blacklisted_ports** dans le fichier *dragent.yaml*. Vous devez répertorier les ports à partir desquels vous voulez filtrer les données.

**Remarque :** Le port 53 (DNS) se trouve toujours sur liste noire. 

Par exemple, l'exemple suivant montre comment définir la section *blacklisted_ports* d'un agent Sysdig pour exclure les données provenant des ports 6666 et 6379 :

```
blacklisted_ports:
    - 6666
    - 6379
```
{: screen}

## Inclusion et exclusion de métriques
{: #change_linux_agent_inc_exc_metrics}

Pour filtrer des métriques personnalisées, vous devez personnaliser la section **metrics_filter** dans le fichier *dragent.yaml*. Vous pouvez indiquer les métriques à inclure et celles à filtrer en configurant les paramètres de filtrage **include** et **exclude**.

**Remarque :** L'ordre des règles de filtrage est défini comme suit : la première règle correspondant à une métrique est appliquée.

Par exemple, si la section *metrics_filter* d'un agent Sysdig se présente comme suit :

```
metrics_filter:
  - include: metricA.*
  - exclude: metricA.*
  - include: metricB.*
  - include: haproxy.backend.*
  - exclude: haproxy.*
  - exclude: metricC.*
```
{: screen}

* Vous configurez l'agent Sysdig pour qu'il collecte toutes les données provenant des métriques commençant par *metricA*, *metricB* et *haproxy.backend*. 
* Vous filtrez les métriques commençant par *metricC* et d'autres métriques commençant par *haproxy*. 
* L'entrée `exclude: metricA.*` est ignorée.


## Modification du niveau de journalisation
{: #change_linux_agent_log_level}

Pour configurer le niveau de journalisation, vous devez personnaliser la section **log** dans le fichier *dragent.yaml*. 

L'agent Sysdig génère des entrées de journal dans */opt/draios/logs/draios.log*. 
* Le fichier journal pivote lorsque sa taille atteint 10 Mo.
* Les 10 derniers fichiers journaux sont conservés. L'horodatage qui est ajouté au nom de fichier permet de déterminer les fichiers à conserver.
* Les niveaux de journalisation valides sont les suivants : *none*, *error*, *warning*, *info*, *debug*, *trace*.
* Le niveau de journalisation par défaut est *info*, où une entrée est créée pour chaque transmission de métriques agrégées aux serveurs de back end, sur la base d'une par seconde, outre les entrées pour les avertissements et les erreurs.
* Vous pouvez personnaliser le type de journal et les entrées collectées en configurant le fichier de configuration de l'agent Sysdig **/opt/draios/etc/dragent.yaml**. Une fois le fichier modifié, vous devez redémarrer l'agent sur le shell avec `service dragent restart` pour
activer les modifications.

| Cas d'utilisation                                     | Entrée de section de journal           |
|-----------------------------------------------|-----------------------------|
| Traitement des incidents liés au comportement de l'agent                   | `file_priority: debug`      |
| Réduction de la sortie de la console de conteneur               | `console_priority: warning` |
| Filtrage des événements par gravité                  | `event_priority: warning`   |
| Vérification de l'inclusion ou de l'exclusion de métriques  | `metrics_excess_log: true`  |
{: caption="Tableau 2. Entrée de la section de journal" caption-side="top"} 
