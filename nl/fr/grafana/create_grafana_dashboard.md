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


# Création d'un tableau de bord Grafana
{:#create_grafana_dashboard}

Vous pouvez créer un tableau de bord Grafana personnalisé afin d'afficher des métriques pour tous les conteneurs s'exécutant dans un espace de votre organisation {{site.data.keyword.Bluemix}}.
{:shortdesc}

Pour créer un tableau de bord Grafana, procédez comme suit :

1. Démarrez Grafana depuis un navigateur Web. Pour plus d'informations, voir [Accès au tableau de bord Grafana depuis un navigateur Web](/docs/services/cloud-monitoring/grafana/navigating_grafana.html#launch_grafana_from_browser).

2. Sauvegardez le tableau de bord par défaut.

    1. Dans la barre d'outils, cliquez sur l'icône Save.
    2. Entrez un nom pour le tableau de bord.
    3. En regard de la zone du nom, cliquez sur l'icône Save.
   
3. Désactivez l'actualisation automatique de page lorsque vous travaillez dans votre tableau de bord. 

    1. Cliquez sur le sélecteur de période situé dans l'en-tête.
    2. Sélectionnez **Auto-refresh**.
    3. Cliquez sur **Off**.
 
 5. Supprimez les lignes d'exemple.
 
     1. En regard de l'en-tête *Welcome to Grafana*, positionnez le curseur sur le menu Row et cliquez sur le menu Row qui apparaît.
     2. Cliquez sur **Delete row**, puis sur **Yes**.
     
     Répétez ces étapes pour supprimer les liens vers la documentation et les lignes associées à First Graph. 
     
     Dans l'en-tête de la page, modifiez le sélecteur d'heure pour vous assurer que vous pouvez voir les données. La valeur par défaut va de 6 heures à quelques secondes auparavant. Sélectionnez
**Last 30d**.
     
6. Ajoutez une visualisation.

    * Pour ajouter une visualisation d'UC inactive, voir [Ajout d'une visualisation d'UC inactive](/docs/services/cloud-monitoring/grafana/create_grafana_dashboard.html#grafana_add_cpu).
    * Pour ajouter une visualisation de la mémoire utilisée, voir [Ajout d'une visualisation de la mémoire utilisée](/docs/services/cloud-monitoring/grafana/create_grafana_dashboard.html#grafana_add_mem).
        
7. Sauvegardez le tableau de bord personnalisé.

    1. Dans la barre d'outils, cliquez sur l'icône Save.
    2. Entrez un nom pour le tableau de bord.
    3. En regard de la zone du nom, cliquez sur l'icône Save.
    

## Ajout d'une visualisation d'UC inactive
{:#grafana_add_cpu}

Pour ajouter un graphique d'UC inactive pour tous les conteneurs dans votre espace, procédez comme suit :

1. Cliquez sur le bouton **Add a row**. Un curseur de menu Row est affiché sur le côté de la ligne.
    
2. Positionnez-vous sur le curseur du menu ligne, puis cliquez sur l'icône de menu Row qui apparaît.

3. Cliquez sur **Add Panel**. Cliquez ensuite sur **graph**.

4. Cliquez sur le titre du graphique pour ouvrir le menu du panneau, puis cliquez sur **Edit**. 

    Le reste du tableau de bord est masqué ; seul l'éditeur de ce graphique et un aperçu de celui-ci sont affichés.
    
5. Dans l'onglet Metrics, construisez une requête pour collecter les données du graphique. 

    Par exemple lorsque vous travaillez sur des conteneurs déployés dans une infrastructure de cloud gérée par {{site.data.keyword.Bluemix_notm}}, le format de la requête inclut l'ID d'espace, un ID de groupe de conteneurs, et un ID d'instance de conteneur unique, au format suivant : `ID_espace.ID_groupe.ID_instance.métrique`
        
    1. Sur la ligne A, cliquez sur **Select metric**. Sélectionnez ensuite votre ID d'espace.
    2. Cliquez sur **Select metric** et sélectionnez l'astérisque (\*).
    
    Lorsque vous sélectionnez l'astérisque (\*), les données incluent des métriques de chaque groupe de conteneurs dans l'espace. Le cas échéant, vous pouvez adapter ce format en spécifiant une expression
régulière pour inclure
uniquement les métriques de certains conteneurs. Par exemple, si vous ne
désirez examiner que les métriques de conteneurs uniques et non de groupes de conteneurs, cliquez sur
**Select metric** et sélectionnez **0000**.
        
    3. Cliquez sur **Select metric** et sélectionnez à nouveau l'astérisque (\*). Ce format inclut des métriques pour chaque conteneur unique dans l'espace.
        
    4. Cliquez sur **Select metric**, puis sur **cpu-0**.
        
    5. Cliquez sur **Select metric**, puis sur **cpu-idle**. L'aperçu du graphique est actualisé et affiche les métriques correspondant à cette requête.
    
6. Facultatif : Personnalisez l'affichage du graphique.
    
    * Pour attribuer un nom au graphique, cliquez sur l'onglet General et dans la zone Title, entrez un nom pour le graphique (par exemple, CPU Idle).
    * Pour attribuer un libellé à l'axe vertical, cliquez sur l'onglet Axes and grid et dans la section Left Y Axis, dans l'onglet Label, entrez CPU.
    * Pour modifier la couleur d'arrière-plan du graphique, dans la section Grid thresholds, pour Level 2, cliquez sur l'icône de sélection de couleur d'arrière-plan en sélectionnant la couleur blanche ou gris clair.
    
    Dans l'en-tête, cliquez sur **Back to dashboard**.
    
7. Pour sauvegarder les modifications apportées à ce tableau de bord, dans l'en-tête, cliquez sur l'icône Save, puis cliquez sur l'icône Save dans le menu.


## Ajout d'une visualisation de la mémoire utilisée
{:#grafana_add_mem}

Pour ajouter une visualisation de la mémoire utilisée, procédez comme suit :

1. Cliquez sur le bouton Add a row. Un curseur de menu Row est affiché sur le côté de la ligne.
   
2. Positionnez-vous sur le curseur du menu ligne, puis cliquez sur l'icône de menu Row qui apparaît.

    1. Cliquez sur Add Panel > graph.
    2. Cliquez sur Edit. Le reste du tableau de bord est masqué ; seul l'éditeur de ce graphique et un aperçu de celui-ci sont affichés.
    
3. Dans l'onglet Metrics, construisez une requête pour collecter les données du graphique. 

    Par exemple, lorsque vous travaillez sur des conteneurs déployés dans une infrastructure de cloud gérée par {{site.data.keyword.Bluemix_notm}}, le format de la requête inclut l'ID d'espace, un ID de groupe de conteneurs, et un ID d'instance de conteneur unique, au format suivant : ID_espace,ID_groupe,ID_espace.métrique.
        
    1. Sur la ligne A, cliquez sur **Select metric**. Sélectionnez ensuite votre ID d'espace.
    2. Cliquez sur **Select metric** et sélectionnez l'astérisque (\*).
    
    Lorsque vous sélectionnez l'astérisque (\*), les données incluent des métriques de chaque groupe de conteneurs dans l'espace. Le cas échéant, vous pouvez adapter ce format en spécifiant une expression
régulière pour inclure
uniquement les métriques de certains conteneurs. Par exemple, si vous ne
désirez examiner que les métriques de conteneurs uniques et non de groupes de conteneurs, cliquez sur
**Select metric** et sélectionnez **0000**.
    
    3. Cliquez sur **Select metric** et sélectionnez à nouveau l'astérisque (\*). Ce format inclut des métriques pour chaque conteneur unique dans l'espace.
        
    4. Cliquez sur **Select metric** et sur **memory**.
        
    5. Cliquez sur **Select metric** et sur **memory-used**. L'aperçu du graphique est actualisé et affiche les métriques correspondant à cette requête.
    
6. Facultatif : Personnalisez l'affichage du graphique.
    
    * Pour attribuer un nom au graphique, cliquez sur l'onglet General et dans la zone Title, entrez un nom pour le graphique (par exemple, Memory used).
    *  Pour modifier le format des valeurs de l'axe X, cliquez sur l'onglet Axes and grid et dans la section Left Y Axis, pour Format, sélectionnez "bytes".
    * Pour attribuer un libellé à l'axe vertical, dans la zone Label, entrez Memory.
    * Pour modifier la couleur d'arrière-plan du graphique, dans la section Grid thresholds, pour Level 2, cliquez sur l'icône de sélection de couleur d'arrière-plan en sélectionnant la couleur blanche ou gris clair.
    
    Dans l'en-tête, cliquez sur **Back to dashboard**.

7. Pour sauvegarder les modifications apportées à ce tableau de bord, dans l'en-tête, cliquez sur l'icône Save, puis cliquez sur l'icône Save dans le menu.

