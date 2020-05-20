---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Générer des jeux de données à partir des résultats de la requête
topic: queries
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 0%

---


# Générer des jeux de données à partir des résultats de la requête

La puissance réelle de Requête Service est révélée lorsque des requêtes sont utilisées pour générer des jeux de données dans le lac de données à utiliser comme entrée dans plus de requêtes ou dans d’autres services tels que Data Science Workspace, le Profil client en temps réel ou Analyse Workspace.

Requête Service permet la création de jeux de données à partir de l’interface utilisateur. Procédez comme suit :

1. Écrivez votre requête à l’aide d’un client connecté et validez la sortie.
2. Connectez-vous à l’interface utilisateur de la plateforme et accédez à Requêtes.
3. Recherchez votre requête dans la liste et placez le pointeur de la souris sur la ligne.
4. Cliquez sur **Créer un jeu de données**. ![Image](../images/queries/create-datasets/click-create-dataset.png)
5. Entrez un nom de jeu de données, précédé de votre ID LDAP (il n&#39;est pas nécessaire d&#39;être unique ou SQL-safe ; le système génère un &quot;nom de table&quot; basé sur le nom donné ici).
6. Saisissez une description de jeu de données et cliquez sur **Exécuter la Requête**.![Image](../images/queries/create-datasets/run-query.png)
7. Regardez la requête terminée, puis accédez à la page liste des jeux de données pour voir le jeu de données que vous venez de créer.

Une fois un jeu de données créé, il est accessible comme tout autre jeu de données dans le lac de données et utilisé pour divers cas d&#39;utilisation.

>[!NOTE] Dans une mise en oeuvre en direct, vous devez appliquer des étiquettes de gouvernance des données après la création du jeu de données.

## Générer des jeux de données avec un schéma de modèle de données d’expérience prédéfini

Pour générer un jeu de données avec un schéma XDM (Experience Data Model) prédéfini, vous devez utiliser la syntaxe SQL. Pour plus d&#39;informations sur la syntaxe à utiliser, consultez le guide [Syntaxe](../sql/syntax.md#create-table-as-select)SQL.

## Jeu de données de sortie

Les jeux de données créés à l&#39;aide de cette fonctionnalité sont générés avec un schéma ad hoc qui correspond à la structure des données de sortie telle que définie dans l&#39;instruction SQL. Certains services en aval nécessitent des jeux de données avec des schémas de modèle de données d’expérience (XDM) particuliers. Vérifiez les exigences de formatage des données pour les services en aval avant de rédiger vos requêtes.