---
keywords: Experience Platform;accueil;rubriques populaires;service de requête;service de requête;générer des jeux de données;générer un jeu de données;créer un jeu de données ;
solution: Experience Platform
title: Génération de jeux de données à partir de résultats dans Query Service
topic-legacy: queries
type: Tutorial
description: Adobe Experience Platform Query Service permet la création de jeux de données à partir de l’interface utilisateur. Une fois qu’un jeu de données a été créé, il est accessible comme tout autre jeu de données du lac de données et utilisé pour divers cas d’utilisation.
exl-id: 6f6c049d-f19f-4161-aeb4-3a01eca7dc75
source-git-commit: 03e7863f38b882a2fbf6ba0de1755e1924e8e228
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 44%

---

# Génération de jeux de données à partir de résultats dans Query Service

La vraie puissance de [!DNL Query Service] s’affiche lorsque des requêtes sont utilisées pour générer des jeux de données dans la variable [!DNL Data Lake] à utiliser comme entrée dans d’autres requêtes ou dans d’autres services tels que [!DNL Data Science Workspace], [!DNL Real-time Customer Profile]ou [!DNL Analysis Workspace].

[!DNL Query Service] permet la création de jeux de données à partir de l’interface utilisateur. Procédez de la façon suivante :

1. Rédigez votre requête à l’aide d’un client connecté et validez la sortie.
2. Connectez-vous au [!DNL Platform] Interface utilisateur et accédez à Requêtes.
3. Cherchez votre requête dans la liste et survolez la ligne avec la souris.
4. Sélectionner **[!UICONTROL Créer un jeu de données]**. ![Image](../images/ui/create-datasets/output-dataset.png)
5. Saisissez un nom de jeu de données, précédé de votre identifiant LDAP (il n’est pas nécessaire qu’il soit unique ou compatible avec SQL ; le système génère un « nom de table » basé sur le nom donné ici).
6. Saisissez une description de jeu de données et sélectionnez **[!UICONTROL Exécuter la requête]**.![Image](../images/ui/create-datasets/run-query.png)
7. Lorsque l’exécution de la requête est terminée, accédez à la page de liste du jeu de données pour voir le jeu de données que vous venez de créer.

Une fois qu’un jeu de données est créé, il est accessible comme tout autre jeu de données dans le [!DNL Data Lake] et utilisés pour divers cas d’utilisation.

>[!NOTE]
>
>Dans une mise en œuvre en direct, vous devez appliquer des étiquettes de gouvernance des données après la création du jeu de données.

## Génération de jeux de données avec une [!DNL Experience Data Model] schema

Pour générer un jeu de données avec une valeur prédéfinie [!DNL Experience Data Model] (XDM), vous devez utiliser la syntaxe SQL. Pour plus d’informations sur la syntaxe à utiliser, consultez le [guide de syntaxe SQL](../sql/syntax.md#create-table-as-select).

## Jeux de données de sortie

Les jeux de données créés à l’aide de cette fonctionnalité sont générés avec un schéma ad hoc correspondant à la structure des données de sortie telle que définie dans l’instruction SQL. Certains services en aval nécessitent des jeux de données spécifiques. [!DNL Experience Data Model] schémas (XDM). Vérifiez les exigences de mise en forme des données pour les services en aval avant de rédiger votre requête.
