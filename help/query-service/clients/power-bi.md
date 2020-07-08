---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Connexion à Power BI
topic: connect
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---


# Connexion avec Power BI (PC)

Les utilisateurs de PC peuvent installer Power BI à partir de [https://powerbi.microsoft.com/en-us/desktop/](https://powerbi.microsoft.com/en-us/desktop/).

## Configuration de la barre d&#39;alimentation

Une fois Power BI installé, vous devez configurer les composants nécessaires pour prendre en charge le connecteur PostgreSQL. Procédez comme suit :

- Trouvez et installez `npgsql`, un package de pilotes .NET pour PostgreSQL qui est la méthode officielle de connexion de PowerBI.

- Sélectionnez v4.0.10 (les nouvelles versions entraînent actuellement une erreur).

- Sous &quot;Installation GAC Npgsql&quot; dans l&#39;écran Configuration personnalisée, sélectionnez **Sera installé sur le disque** dur local. Si vous n&#39;installez pas le GAC, Power BI échouera ultérieurement.

- Redémarrez Windows.

- Recherchez la version d&#39;évaluation de PowerBI Desktop.

## Connexion de Power BI au service de Requête

Après avoir exécuté ces étapes préparatoires, vous pouvez connecter Power BI à Requête Service :

- Ouvrez Power BI.

- Cliquez sur **Obtenir des données** dans le ruban du menu supérieur.

- Sélectionnez **PostgreSQL database**, puis cliquez sur **Connect**.

- Saisissez les valeurs du serveur et de la base de données. **Serveur** est l&#39;hôte trouvé sous les détails de la connexion. Pour la production, ajoutez le port `:80` à la fin de la chaîne Host. **La base de données** peut être &quot;all&quot; ou un nom de table de jeu de données. (Essayez l&#39;un des jeux de données dérivés du CTAS.)

- Cliquez sur Options **** avancées, puis désactivez la case à cocher **inclure des colonnes** de relations. Ne cochez pas la case **Naviguer à l’aide de la hiérarchie** complète.

- *(Facultatif mais recommandé lorsque &quot;all&quot; est déclaré pour la base de données)* Saisissez une instruction SQL.

>[!NOTE]
>
>Si une instruction SQL n&#39;est pas fournie, Power BI prévisualisation toutes les tables de la base de données. Pour les données hiérarchiques, une instruction SQL personnalisée doit être utilisée. Si le schéma de table est plat, il fonctionnera avec ou sans instruction SQL personnalisée. Les types composés ne sont pas encore pris en charge par Power BI - pour obtenir des types primitifs à partir de types composés, vous devrez écrire des instructions SQL pour les dériver.

```sql
SELECT web.webPageDetails.name AS Page_Name, 
SUM(web.webPageDetails.pageviews.value) AS Page_Views 
FROM _TABLE_ 
WHERE _ACP_YEAR=2018 AND _ACP_MONTH=11 AND _ACP_DAY=20 
GROUP BY web.webPageDetails.name 
ORDER BY SUM(web.webPageDetails.pageviews.value) DESC 
LIMIT 10
```

- Sélectionnez le mode **DirectQuery** ou **Importer** . En mode **Importation** , les données seront importées dans Power BI. En mode **DirectQuery** , toutes les requêtes seront envoyées à Requête Service pour exécution.

- Cliquez sur **OK**. Désormais, Power BI se connecte au service de Requête et produit une prévisualisation s&#39;il n&#39;y a aucune erreur. Un problème connu se produit lorsque la Prévisualisation restitue des colonnes numériques. Passez à l’étape suivante.

- Cliquez sur **Charger** pour importer le jeu de données dans Power BI.
