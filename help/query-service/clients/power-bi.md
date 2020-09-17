---
keywords: Experience Platform;home;popular topics;query service;Query service;Power BI;power bi;connect to query service;
solution: Experience Platform
title: Connexion de Power BI
topic: connect
translation-type: tm+mt
source-git-commit: f9749dbc5f2e3ac15be50cc5317ad60586b2c07e
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 67%

---


# Se connecter avec [!DNL Power BI] (PC)

PC users can install [!DNL Power BI] from [https://powerbi.microsoft.com/en-us/desktop/](https://powerbi.microsoft.com/fr-fr/desktop/).

## Configuration [!DNL Power BI]

After you have [!DNL Power BI] installed, you need to set up the necessary components to support the PostgreSQL connector. Procédez de la façon suivante :

- Trouvez et installez `npgsql`, un package de pilotes .NET pour PostgreSQL qui constitue la méthode officielle pour connecter PowerBI.

- Sélectionnez v4.0.10 (les versions plus récentes génèrent actuellement une erreur).

- Sous « Installation du GAC Npgsql » de l’écran de configuration personnalisée, sélectionnez **[!UICONTROL Sera installé sur le disque dur local]**. Si vous n’installez pas le GAC, Power BI échouera ultérieurement.

- Redémarrez Windows.

- Find the [!DNL PowerBI] Desktop evaluation version.

## Se connecter [!DNL Power BI] à [!DNL Query Service]

After performing those preparatory steps, you can connect [!DNL Power BI] to [!DNL Query Service]:

- Ouvrir [!DNL Power BI].

- Cliquez sur **[!UICONTROL Obtenir des données]** dans le ruban du menu supérieur.

- Choisissez **[!UICONTROL Base de données PostgreSQL]**, puis cliquez sur **[!UICONTROL Connecter]**.

- Saisissez les valeurs du serveur et de la base de données. Le **[!UICONTROL serveur]** est l’hôte trouvé sous les détails de connexion. Pour la production, ajoutez le port `:80` à la fin de la chaîne d’hôte. La **[!UICONTROL base de données]** peut être « all » ou un nom de table de jeu de données. (Essayez l’un des jeux de données dérivés de CTAS.)

- Cliquez sur **[!UICONTROL Options avancées]**, puis décochez la case **[!UICONTROL Inclure les colonnes de relations]**. Ne cochez pas la case **[!UICONTROL Naviguer avec la hiérarchie complète]**.

- *(Facultatif mais recommandé lorsque « all » est déclaré comme base de données)* Saisissez une instruction SQL.

>[!NOTE]
>
>If a SQL statement is not provided, then [!DNL Power BI] will preview all of the tables in database. Pour les données hiérarchiques, vous devez utiliser une instruction SQL personnalisée. Si le schéma de table est plat, il fonctionne avec ou sans instruction SQL personnalisée. Compound types are yet not supported by [!DNL Power BI] - to get primitive types from compound types, you will need to write SQL statements to derive them.

```sql
SELECT web.webPageDetails.name AS Page_Name, 
SUM(web.webPageDetails.pageviews.value) AS Page_Views 
FROM _TABLE_ 
WHERE TIMESTAMP >= to_timestamp('2018-11-20')
GROUP BY web.webPageDetails.name 
ORDER BY SUM(web.webPageDetails.pageviews.value) DESC 
LIMIT 10
```

- Sélectionnez le mode **[!UICONTROL DirectQuery]** ou le mode **[!UICONTROL Importer]**. En mode **[!UICONTROL Importer]**, les données sont importées dans [!DNL Power BI]. En mode **[!UICONTROL DirectQuery]**, toutes les requêtes sont envoyées à pour exécution.[!DNL Query Service]

- Cliquez sur **[!UICONTROL OK]**. Now, [!DNL Power BI] connects to the [!DNL Query Service] and produces a preview if there are no errors. Il existe un problème connu avec les colonnes numériques de rendu de prévisualisation. Passez à l’étape suivante.

- Click **[!UICONTROL Load]** to bring the dataset into [!DNL Power BI].
