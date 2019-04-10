---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring,  predefined dashboards

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


# Tableaux de bord prédéfinis
{: #default_dashboards}
Vous pouvez choisir l'un des tableaux de bord prédéfinis ci-dessous pour surveiller votre infrastructure.
{:shortdesc}


## Applications
{: #default_dashboards_applications}

Le tableau suivant répertorie les tableaux de bord prédéfinis que vous pouvez sélectionner pour surveiller vos applications et les composants de l'infrastructure :

| Nom du tableau de bord        | Description                                                            | Utilisation             |
|-----------------------|------------------------------------------------------------------------|-------------------|
| HTTP Overview         | Utilisez ce tableau de bord pour surveiller la santé de votre serveur Web. Il présente la charge sur le serveur et sa capacité à traiter les demandes dans le délai imparti. | Utilisez les panneaux Number of Requests et Avg/Max Request Time pour évaluer l'occupation globale de votre serveur. </br>Recherchez les corrélations entre les URL pour trouver des opportunités d'améliorer les performances. </br>Utilisez la métrique Status Codes pour surveiller les codes d'erreur 4xx et 5xx. |  
| HTTP Top Requests  |  Utilisez ce tableau de bord pour surveiller les URL les plus demandées sur votre serveur Web, telles que le nombre total de demandes, les durées moyenne et maximale de traitement des demandes, ainsi que le volume de trafic contenu dans les demandes et les réponses. |   |
| MongoDB  | Utilisez ce tableau de bord pour surveiller l'occupation de votre service MongoDB, les collections les plus demandées et celles qui ont les plus mauvaises performances.  |  Recherchez les collections pouvant bénéficier de l'optimisation des performances de requêtes et d'index. |
| MySQL/PostgreSQL  | Utilisez ce tableau de bord pour surveiller la charge globale et le statut des performances de vos transactions de base de données SQL. Déterminez le nombre de demandes et leur vitesse de traitement.  | Améliorez les performances. Par exemple, surveillez les temps de réponse des requêtes les plus lentes et identifiez les modifications que vous apportez à la requête ou aux index sur les tables.  |
| MySQL/PostgreSQL Top  | Utilisez ce tableau de bord pour surveiller les requêtes SQL les plus utilisées. Affichez le nombre de requêtes reçues et le volume de trafic envoyé et reçu pour la requête.   | Recherchez les requêtes les plus lentes, celles exécutées le plus souvent et celles avec un trafic élevé.  |
| Nginx  | Utilisez ce tableau de bord pour surveiller les ressources hôte, les connexions HTTP, les URL les plus utilisées et les plus lentes, et les codes de réponse de l'hôte. | Identifiez les ajustements d'équilibrage de charge en surveillant les métriques suivantes : Writing (Ecriture), Reading (Lecture), Waiting connections (Connexions en attente), CPU Load by Machine (Charge d'UC par machine), Network Bytes Activity (Activité réseau en octets), Requests per Second (Demandes par seconde) </br>Recherchez les pages à optimiser en consultant la métrique Slowest URL (URL les plus lentes). </br>Recherchez les incidents en consultant les codes de réponse.  |
{: caption="Tableau 1. Liste des tableaux de bord prédéfinis pour les composants d'application et d'infrastructure" caption-side="top"} 


## Tableaux de bord d'hôte et de conteneur
{: #default_dashboards_host_container}

Le tableau suivant répertorie les tableaux de bord prédéfinis que vous pouvez utiliser pour surveiller l'utilisation des ressources et l'activité du système sur vos hôtes et dans vos conteneurs :


| Nom du tableau de bord        | Description                                                            | Utilisation             |
|-----------------------|------------------------------------------------------------------------|-------------------|
| *Container Limits*    | Utilisez ce tableau de bord pour afficher les métriques de mémoire et d'UC relatives aux ressources de l'hôte qui sont allouées à chaque conteneur. | |
| *File System*         | Utilisez ce tableau de bord pour afficher les points de montage de répertoire, les périphériques de système de fichiers, ainsi que les informations de capacité et d'utilisation pour les systèmes de fichiers qui sont montés sur l'instance.  </br>Les systèmes de fichiers qui sont montés à distance ne sont pas répertoriés par défaut. Pour afficher les données pour ces systèmes de fichiers, ajoutez l'entrée **remotefs.enabled = true** au fichier */opt/draios/bin/dragent.properties* sur chaque
instance. </br>Lorsque des groupes sont sélectionnés, les métriques représentent des moyennes pour les points de montage de système de fichiers similaires.| Recherchez les systèmes de fichiers qui sont saturés et ceux qui sont sous-utilisés. Triez-les à l'aide de *fs.bytes.used*.|
| *Overview by Container* | Utilisez ce tableau de bord pour afficher les statistiques d'utilisation des ressources telles que le pourcentage d'UC, le pourcentage d'utilisation de la mémoire, le nombre total d'octets de réseau et le nombre total d'octets de fichier pour les conteneurs qui s'exécutent sur l'instance ou le groupe sélectionné.  </br>Utilisez la fonction *Time Travel* avec la fonction *Compare* dans cette vue pour afficher les informations d'historique. En fonction des données, vérifiez si les processus s'exécutent comme prévu, ne se comportent pas correctement ou nécessitent davantage de ressources. | Découvrez les conteneurs qui consomment beaucoup de ressources.  </br>Utilisez ces informations pour déterminer si une application doit être déplacée vers un autre hôte. |
| *Overview by Container Image* | Utilisez ce tableau de bord pour obtenir une vue d'ensemble de la taille, des performances et des limitations des services qui est définie dans l'image de conteneur. | |
| Overview by Host | Utilisez ce tableau de bord pour afficher les statistiques générales d'utilisation des ressources telles que le pourcentage d'UC, le pourcentage d'utilisation de la mémoire, le nombre total d'octets de réseau, le nombre de connexions réseau, le nombre total d'octets de fichier et l'utilisation du disque, pour un hôte. </br>Vous pouvez également utiliser ce tableau de bord pour surveiller un groupe d'instances. </br>Utilisez la fonction *Time Travel* avec la fonction *Compare* dans cette vue pour afficher les informations d'historique. En fonction des données, vérifiez si les processus s'exécutent comme prévu, ne se comportent pas correctement ou nécessitent plus de ressources. | Recherchez les hôtes inutilisés ou surutilisés dans un groupe d'hôtes avec des fonctions de travail similaires. | 
| Overview by Process | Utilisez ce tableau de bord pour afficher les statistiques générales d'utilisation des ressources telles que le pourcentage d'UC, le pourcentage d'utilisation de la mémoire, le nombre total d'octets de réseau, le nombre de connexions réseau, le nombre total d'octets de fichier et l'utilisation du disque, pour les processus les plus utilisés sur un hôte. </br>Vous pouvez également utiliser ce tableau de bord pour surveiller un groupe d'instances. </br>Utilisez la fonction *Time Travel* avec la fonction *Compare* dans cette vue pour afficher les informations d'historique. En fonction des données, vérifiez si les processus s'exécutent comme prévu, ne se comportent pas correctement ou nécessitent plus de ressources. | Découvrez les processus qui consomment beaucoup de ressources.  </br>Utilisez ces informations pour déterminer si une application doit être déplacée vers un autre hôte. |
| Sysdig Agent Summary | Utilisez ce tableau de bord pour afficher le nombre d'agents Sysdig qui sont déployés dans votre environnement et leurs versions. |  | 
| Top Files | Utilisez ce tableau de bord pour afficher la liste des fichiers les plus utilisés. Vous pouvez voir le nom du fichier, le nombre total d'octets de fichier, le temps alloué à l'E-S de fichiers et le nombre d'erreurs de fichier. | Trouvez les principaux consommateurs de disque lorsque vous effectuez un tri par taille. </br>Recherchez les fichiers les plus utilisés lors du tri par E-S. </br>Identifiez les erreurs potentielles en surveillant les données de la colonne *File Error Count*. |
| Top Processes | Utilisez ce tableau de bord pour afficher la liste des processus les plus exécutés sur un hôte ou un groupe d'hôtes. Vous pouvez voir le nom du processus, son chemin d'accès et tous les arguments. </br>Utilisez la fonction de filtre pour limiter l'affichage des processus répertoriés. | Trouvez quels processus sont les principaux consommateurs de ressources dans un environnement où le même processus est généré plusieurs fois. |
| Top Server Processes | Utilisez ce tableau de bord pour afficher la consommation des ressources par les processus identifiés comme orientés serveur uniquement ((httpd, java, ntpd, etc.). | Recherchez l'utilisation des ressources pour les processus serveur. |
{: caption="Tableau 2. Liste des tableaux de bord prédéfinis de conteneur et d'hôte" caption-side="top"} 

## Réseau
{: #default_dashboards_network}

Le tableau suivant répertorie les tableaux de bord prédéfinis que vous pouvez sélectionner pour surveiller vos connexions réseau et votre activité :

| Nom du tableau de bord        | Description                                                            | Utilisation             |
|-----------------------|------------------------------------------------------------------------|-------------------|
| Connections Table     | Utilisez ce tableau de bord pour afficher les connexions entre vos instances et les noeuds distants. Surveillez le trafic pour chaque connexion. | Trouvez les utilisateurs qui consomment le plus de trafic réseau. |
| Overview              |  Utilisez ce tableau de bord pour afficher l'utilisation totale du réseau au fil du temps par direction, application, processus et hôte.| Identifiez les ressources qui ont le plus d'impact sur les performances de réponse. |
| Response Times vs Resource Usage | Utilisez ce tableau de bord pour afficher les métriques de ressource hôte au fil du temps par rapport au temps de réponse de l'hôte lors du traitement des demandes de réseau. |  |
| Top Ports             |  Utilisez ce tableau de bord pour afficher les octets entrants, sortants et leur nombre total par port, ainsi que le nombre de connexions à chaque numéro de port. |  |
{: caption="Tableau 3. Liste des tableaux de bord prédéfinis de réseau" caption-side="top"} 



## Service
{: #default_dashboards_service}


Le tableau suivant répertorie les tableaux de bord prédéfinis que vous pouvez utiliser pour surveiller les performances de vos services, même si ces derniers sont déployés dans des conteneurs orchestrés :

| Nom du tableau de bord        | Description                                                            | 
|-----------------------|------------------------------------------------------------------------|
| Overview by Service   | Utilisez ce tableau de bord pour afficher la taille, les performances et les limitations des services qui s'exécutent dans la même image de conteneur. | 
| Service Overview      | Utilisez ce tableau de bord pour afficher l'utilisation des ressources et les temps de réponse d'un seul service. | 
{: caption="Tableau 4. Liste des tableaux de bord prédéfinis de service" caption-side="top"} 



## Topologie
{: #default_dashboards_topology}

Le tableau suivant répertorie les tableaux de bord prédéfinis que vous pouvez utiliser pour surveiller les dépendances logiques de vos groupes de serveurs d'application :

| Nom du tableau de bord        | Description                                                            | 
|-----------------------|------------------------------------------------------------------------|
| CPU Usage             | Utilisez ce tableau de bord pour surveiller l'interaction entre l'hôte et le reste de l'infrastructure.  | 
| Network Traffic       | Utilisez ce tableau de bord pour surveiller l'utilisation de la bande passante de l'instance sélectionnée entre les processus locaux et les processus sur les noeuds distants. |
| Response Times        | Utilisez ce tableau de bord pour surveiller les métriques de communication et de réponse réseau entre tous les processus sur les hôtes sélectionnés. </br>Le nombre de réponses et les heures s'affichent dans des moyennes allant jusqu'à une granularité de 1 seconde.  |
{: caption="Tableau 5. Liste des tableaux de bord prédéfinis de topologie" caption-side="top"} 

**Remarque :** ces tableaux de bord contiennent des pointillés et des cases grises pour les instances sur lesquelles l'agent Sysdig n'est pas installé et pour lesquelles une communication est détectée.















