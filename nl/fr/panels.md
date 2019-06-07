---

copyright:
  years:  2018, 2019
lastupdated: "2019-05-09"

keywords: Sysdig, IBM Cloud, monitoring, panels

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


# Gestion des panneaux
{: #panels}

Un panneau permet d'afficher une métrique ou un groupe de métriques dans un tableau de bord. Vous pouvez copier, modifier la portée, dupliquer, supprimer, exporter et explorer des panneaux.
{:shortdesc}

Vous pouvez utiliser l'un des types de panneaux suivants :

| Type | Description |
|------|-------------|
| `Line` | Utilisez ce panneau pour afficher les tendances au fil du temps pour une ou plusieurs métriques.  |
| `Area` | Utilisez ce panneau pour afficher les tendances au fil du temps pour une ou plusieurs métriques.  |
| `Top list` | Utilisez ce panneau pour comparer une métrique sur un groupe d'entités. Le graphique à barres est trié par ordre décroissant.  |
| `Histogram` | Utilisez ce panneau pour afficher la distribution des fréquences d'une métrique dans des compartiments.  |
| `Topology` | Utilisez ce panneau pour visualiser l'infrastructure sous forme de mappe topologique, ainsi que les relations entre les entités de la mappe.  |
| `Number` | Utilisez ce panneau pour afficher un seul nombre qui représente la valeur d'une métrique agrégée au fil du temps pour une ou plusieurs entités.  |
| `Table` | Utilisez ce panneau pour afficher des données numériques pour votre infrastructure en fonction des métriques et segments.  |
| `Text` | Utilisez ce panneau pour ajouter du texte. Utilisez Markdown pour ajouter votre texte.  |
{: caption="Tableau 1. Types de panneaux" caption-side="top"} 



## Copie d'un panneau dans un tableau de bord
{: #panels_copy}

Pour copier un panneau, procédez comme suit :

1. Accédez à la section *TABLEAU DE BORD** dans l'interface utilisateur Web. Sélectionnez un tableau de bord. Identifiez ensuite le panneau qui affiche la métrique que vous voulez copier.

2. Sélectionnez l'icône *Plus d'options* ![icône des trois points](images/actions.png) puis sélectionnez **Copy panel** ![icône de copie](images/actions.png).

3. Sélectionnez l'un des tableaux de bord répertoriés, ou entrez un nom pour le nouveau tableau de bord. 

4. Cliquez sur **Copy and Open**.



## Modification de la portée d'un panneau
{: #panels_scope}

Procédez comme suit pour modifier la portée d'un panneau :

1. Accédez à la section *TABLEAU DE BORD** dans l'interface utilisateur Web. Sélectionnez un tableau de bord. Identifiez ensuite le panneau qui affiche la métrique dont vous voulez modifier la portée.

2. Dans le panneau, cliquez sur **Edit Scope** pour modifier la portée par défaut. 

    **Everywhere** est sélectionné par défaut.
    
3. Sélectionnez la portée. 

4. Cliquez éventuellement sur **Override the custom panel scopes** pour remplacer la portée de tous les panneaux avec une portée personnalisée définie.  

    **Remarque : cette action ne peut pas être annulée.** 

    Pour réinitialiser la portée du tableau de bord sur la totalité de l'infrastructure, ou pour mettre à jour la portée d'un tableau de bord existant sur l'ensemble de l'infrastructure, sélectionnez **Everywhere**.
    {: tip}

5. Cliquez sur **Save**.



## Duplication d'un panneau
{: #panels_duplicate}

Procédez comme suit pour dupliquer un panneau dans le tableau de bord en cours :

1. Accédez à la section *TABLEAU DE BORD** dans l'interface utilisateur Web. Sélectionnez un tableau de bord. Identifiez ensuite le panneau qui affiche la métrique que vous voulez copier.

2. Sélectionnez l'icône *Plus d'options* ![icône des trois points](images/actions.png) puis sélectionnez **Duplicate panel** ![icône de copie](images/duplicate.png).


## Suppression d'un panneau
{: #panels_delete}

Procédez comme suit pour supprimer un panneau dans le tableau de bord en cours :

1. Accédez à la section *TABLEAU DE BORD** dans l'interface utilisateur Web. Sélectionnez un tableau de bord. Identifiez ensuite le panneau qui affiche la métrique que vous voulez copier.

2. Sélectionnez l'icône *Plus d'options* ![icône de trois points](images/actions.png) puis sélectionnez **Delete panel** ![icône de suppression](images/delete.png).

3. Cliquez sur **Yes, delete panel** pour confirmer la suppression du panneau.



## Exportation de données à partir d'un panneau
{: #panels_export}

Prenez en compte les informations suivantes lorsque vous exportez des données :

* Vous pouvez exporter des données vers un **fichier JSON** à partir d'un graphique à courbes.
* Vous pouvez exporter des données vers un **fichier CSV** à partir d'un tableau ou d'un graphique à courbes.

Procédez comme suit pour exporter des données à partir d'un panneau :

1. Accédez à la section *TABLEAU DE BORD** dans l'interface utilisateur Web. Sélectionnez un tableau de bord. Identifiez ensuite le panneau qui affiche la métrique que vous voulez copier.

2. Sélectionnez l'icône *Plus d'options* ![icône des trois points](images/actions.png).

3. Sélectionnez l'une des options suivantes :

    * Sélectionnez **Export JSON** pour exporter les données vers un fichier JSON formaté.

    * Sélectionnez **Export CSV** pour exporter les données vers un fichier CSV formaté.

4. Cliquez sur **Save the file**.




## Création d'une alerte
{: #panels_alert}

Vous pouvez créer des alertes directement à partir d'un panneau.

Pour créer une alerte, procédez comme suit :

1. Accédez à la section *TABLEAU DE BORD** dans l'interface utilisateur Web. Sélectionnez un tableau de bord. Identifiez ensuite le panneau qui affiche la métrique que vous voulez copier.

2. Sélectionnez l'icône *Plus d'options* ![icône des trois points](images/actions.png).

3. Sélectionnez **Créer une alerte**.

4. Configurez l'alerte.

5. Cliquez sur **Créer**.


