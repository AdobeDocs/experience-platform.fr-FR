---
keywords: Experience Platform ; accueil ; rubriques populaires ; service de requête ; service de Requête ; générer des jeux de données ; générer un jeu de données ; créer un jeu de données ;
solution: Experience Platform
title: Génération des jeux de données à partir de résultats de requête
topic: queries
type: Tutorial
description: 'Query Service permet de créer des jeux de données à partir de l’interface utilisateur. Une fois un jeu de données créé, il est accessible comme tout autre jeu de données du lac Data et utilisé pour divers cas d''utilisation. '
translation-type: tm+mt
source-git-commit: 0ba4e26927cdc96855f35d72a8a6de55f4a34bfa
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 50%

---


# Génération des jeux de données à partir de résultats de requête

La puissance réelle de [!DNL Query Service] est révélée lorsque des requêtes sont utilisées pour générer des jeux de données dans [!DNL Data Lake] à utiliser comme entrée dans plus de requêtes ou dans d&#39;autres services tels que [!DNL Data Science Workspace], [!DNL Real-time Customer Profile] ou [!DNL Analysis Workspace].

[!DNL Query Service] permet la création de jeux de données à partir de l’interface utilisateur. Procédez de la façon suivante :

1. Rédigez votre requête à l’aide d’un client connecté et validez la sortie.
2. Connectez-vous à l&#39;interface utilisateur [!DNL Platform] et accédez à Requêtes.
3. Cherchez votre requête dans la liste et survolez la ligne avec la souris.
4. Cliquez sur **[!UICONTROL Créer un jeu de données]**. ![Image](../images/ui/output-dataset.png)
5. Saisissez un nom de jeu de données, précédé de votre identifiant LDAP (il n’est pas nécessaire qu’il soit unique ou compatible avec SQL ; le système génère un « nom de table » basé sur le nom donné ici).
6. Saisissez une description de jeu de données, puis cliquez sur **[!UICONTROL Exécuter la requête]**.![Image](../images/ui/run-query.png)
7. Lorsque l’exécution de la requête est terminée, accédez à la page de liste du jeu de données pour voir le jeu de données que vous venez de créer.

Une fois un jeu de données créé, il est accessible comme tout autre jeu de données dans [!DNL Data Lake] et utilisé pour divers cas d&#39;utilisation.

>[!NOTE]
>
>Dans une implémentation en direct, vous devez appliquer des étiquettes [!DNL Data Governance] après la création du jeu de données.

## Générer des jeux de données avec un schéma prédéfini [!DNL Experience Data Model]

Pour générer un jeu de données avec un schéma prédéfini [!DNL Experience Data Model] (XDM), vous devez utiliser la syntaxe SQL. Pour plus d’informations sur la syntaxe à utiliser, consultez le [guide de syntaxe SQL](../sql/syntax.md#create-table-as-select).

## Jeux de données de sortie

Les jeux de données créés à l’aide de cette fonctionnalité sont générés avec un schéma ad hoc correspondant à la structure des données de sortie telle que définie dans l’instruction SQL. Certains services en aval nécessitent des jeux de données avec des schémas [!DNL Experience Data Model] (XDM) particuliers. Vérifiez les exigences de mise en forme des données pour les services en aval avant de rédiger votre requête.