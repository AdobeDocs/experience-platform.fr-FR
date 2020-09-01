---
keywords: Experience Platform;home;popular topics;query service;Query service;generate datasets;generate dataset;create dataset;
solution: Experience Platform
title: Génération des jeux de données à partir de résultats de requête
topic: queries
translation-type: tm+mt
source-git-commit: 17ef6c1c6ce58db2b65f1769edf719b98d260fc6
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 56%

---


# Génération des jeux de données à partir de résultats de requête

The true power of [!DNL Query Service] is revealed when queries are used to generate datasets in the [!DNL Data Lake] to be used as input into more queries or in other services such as [!DNL Data Science Workspace], [!DNL Real-time Customer Profile], or [!DNL Analysis Workspace].

[!DNL Query Service] permet la création de jeux de données à partir de l’interface utilisateur. Procédez de la façon suivante :

1. Rédigez votre requête à l’aide d’un client connecté et validez la sortie.
2. Log in to the [!DNL Platform] UI and go to Queries.
3. Cherchez votre requête dans la liste et survolez la ligne avec la souris.
4. Cliquez sur **[!UICONTROL Créer un jeu de données]**. ![Image](../images/queries/create-datasets/click-create-dataset.png)
5. Saisissez un nom de jeu de données, précédé de votre identifiant LDAP (il n’est pas nécessaire qu’il soit unique ou compatible avec SQL ; le système génère un « nom de table » basé sur le nom donné ici).
6. Saisissez une description de jeu de données, puis cliquez sur **[!UICONTROL Exécuter la requête]**.![Image](../images/queries/create-datasets/run-query.png)
7. Lorsque l’exécution de la requête est terminée, accédez à la page de liste du jeu de données pour voir le jeu de données que vous venez de créer.

After a dataset is created, it can be accessed like any other dataset in the [!DNL Data Lake] and used for a variety of use cases.

>[!NOTE]
>
>In a live implementation, you must apply [!DNL Data Governance] labels after the dataset is created.

## Générer des jeux de données avec un [!DNL Experience Data Model] schéma prédéfini

In order to generate a dataset with a pre-defined [!DNL Experience Data Model] (XDM) schema, you will have to use the SQL syntax. Pour plus d’informations sur la syntaxe à utiliser, consultez le [guide de syntaxe SQL](../sql/syntax.md#create-table-as-select).

## Jeux de données de sortie

Les jeux de données créés à l’aide de cette fonctionnalité sont générés avec un schéma ad hoc correspondant à la structure des données de sortie telle que définie dans l’instruction SQL. Some downstream services require datasets with particular [!DNL Experience Data Model] (XDM) schemas. Vérifiez les exigences de mise en forme des données pour les services en aval avant de rédiger votre requête.