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

# Personnalisation des agents de conteneur Sysdig
{: #change_container_agent}

Dans {{site.data.keyword.mon_full_notm}}, vous pouvez personnaliser la configuration de l'agent Sysdig pour définir un niveau de journalisation, des ports de bloc, inclure ou exclure des données de mesure, ajouter ou supprimer des événements, et filtrer des conteneurs. 
{:shortdesc}


## Edition du fichier yaml dragent
{: #change_container_agent_edit_config}

Le fichier yaml se trouve dans */opt/draios/etc/*.

Pour éditer le fichier et appliquer les modifications, procédez comme suit :

1. Accédez au fichier *dragent.yaml* directement à l'emplacement `/opt/draios/etc/dragent.yaml`.
2. Editez le fichier. Utilisez une syntaxe YAML valide.
3. Redémarrez l'agent. Exécutez la commande suivante :

    ```
    docker restart sysdig-agent
    ```
    {: codeblock}



## Blocage de ports
{: #change_container_agent_block_ports}

Pour bloquer le trafic réseau et les métriques provenant de ports réseau, vous devez personnaliser la section **blacklisted_ports** dans le fichier *dragent.yaml*. Vous devez répertorier les ports à partir desquels vous voulez filtrer les données.

**Remarque :** Le port 53 (DNS) se trouve toujours sur liste noire. 

Par exemple, l'exemple suivant montre comment définir la section *blacklisted_ports* d'un agent Sysdig pour exclure les données provenant des ports 6666 et 6379 :

```
blacklisted_ports:
    - 6666
    - 6379
```
{: screen}



## Collecte d'un ensemble d'événements Docker
{: #change_container_agent_collect_docker_events}

{{site.data.keyword.mon_full_notm}} prend en charge l'intégration d'événement avec Docker. Les agents Sysdig reconnaissent automatiquement les sources Docker et collectent les données d'événement qu'elles contiennent. Vous pouvez éditer le fichier de configuration de l'agent pour modifier son comportement par défaut et inclure ou exclure des données d'événement. 

Par défaut, seul un ensemble limité d'événements est collecté. Le fichier de configuration des paramètres par défaut */opt/draios/etc/dragent.default.yaml* inclut les événements qui sont collectés. Pour plus d'informations sur les événements qui sont collectés par défaut, voir [Evénements Docker ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://sysdigdocs.atlassian.net/wiki/spaces/Platform/pages/234356795/Enable+Disable+Event+Data#Enable/DisableEventData-DockerEvents){:new_window}.

Pour ajouter ou supprimer des événements, vous devez personnaliser le fichier *dragent.yaml* et spécifier les événements à inclure et ceux à filtrer. **Remarque :** Une entrée dans une section du fichier *dragent.yaml* remplace la totalité de la section dans la configuration par défaut.
{: tip}

Par exemple, pour filtrer les événements d'image Docker et collecter seulement les événements destinés à des actions de connexion, de validation et de copie, vous devez définir la section *docker* comme suit :

* Option 1 : Définissez la séquence d'entrées sous forme de liste à puces :

    ```
    events:
      docker:
        image: none
        container:
          - attach
          - commit
          - copy
    ```
    {: codeblock}

* Option 2 : Définissez la séquence d'entrées sur une seule ligne entre crochets :

    ```
    events:
      docker:
        image: none
        container: [attach, commit, copy]
    ```
    {: codeblock}


## Désactivation de la collecte d'événements
{: #change_container_agent_disable_events}

Pour empêcher un agent Sysdig de collecter des événements, modifiez le fichier *dragent.default.yaml*. Définissez la section **events** sur *none* dans le fichier *dragent.yaml*.

Par exemple, pour filtrer des événements Docker, vous devez définir la section *events* dans le fichier *dragent.yaml* comme suit :

```
events:
  docker: none
```
{: codeblock}



## Filtrage des événements par gravité
{: #change_container_agent_filterby_severity}

Pour filtrer des événements par gravité, vous pouvez également modifier le type d'entrée de journal pour les événements dans le fichier *dragent.yaml*. 

Le niveau de journalisation par défaut est **information**. Cela signifie que seuls les événements de type avertissement et de gravité supérieure sont transmis.

Les niveaux valides sont les suivants : *emergency*, *alert*, *critical*, *error*, *warning*, *notice*, *information*, *debug* et *none*. **Remarque** : Les valeurs sont répertoriées par ordre de priorité décroissant.

Par exemple, pour filtrer les événements de faible gravité (*notice*, *information*, *debug*), vous devez définir la section de journal **event_priority** sur *warning* :

```
log:
  event_priority: warning
```
{: codeblock}


Pour bloquer la collecte d'événements, vous devez définir la section de journal **event_priority** sur *none* :

```
log:
  event_priority: none
```
{: codeblock}




## Inclusion et exclusion de métriques
{: #change_container_agent_inc_exc_metrics}

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
{: #change_container_agent_log_level}

Pour configurer le niveau de journalisation, vous devez personnaliser la section **log** dans le fichier *dragent.yaml*. 

L'agent Sysdig génère des entrées de journal dans */opt/draios/logs/draios.log*. 
* Le fichier journal pivote lorsque sa taille atteint 10 Mo.
* Les 10 derniers fichiers journaux sont conservés. L'horodatage qui est ajouté au nom de fichier permet de déterminer les fichiers à conserver.
* Les niveaux de journalisation valides sont les suivants : *none*, *error*, *warning*, *info*, *debug*, *trace*.
* Le niveau de journalisation par défaut est *info*, où une entrée est créée pour chaque transmission de métriques agrégées aux serveurs de back end, sur la base d'une par seconde, outre les entrées pour les avertissements et les erreurs.
* Vous pouvez personnaliser le type de journal et les entrées collectées en configurant le fichier de configuration de l'agent Sysdig **/opt/draios/etc/dragent.yaml**. Une fois le fichier modifié, vous devez redémarrer l'agent sur le shell avec `docker restart sysdig-agent` pour activer les modifications.

| Cas d'utilisation                                     | Entrée de section de journal           |
|-----------------------------------------------|-----------------------------|
| Traitement des incidents liés au comportement de l'agent                   | `file_priority: debug`      |
| Réduction de la sortie de la console de conteneur               | `console_priority: warning` |
| Filtrage des événements par gravité                  | `event_priority: warning`   |
| Vérification de l'inclusion ou de l'exclusion de métriques  | `metrics_excess_log: true`  |
{: caption="Tableau 2. Entrée de la section de journal" caption-side="top"} 


