---
keywords: Experience Platform;accueil;rubriques populaires;service de requête;service de requête;générer des jeux de données;générer un jeu de données;créer un jeu de données ;
solution: Experience Platform
title: Génération de jeux de données à partir de résultats dans Query Service
topic-legacy: queries
type: Tutorial
description: Adobe Experience Platform Query Service permet la création de jeux de données à partir de l’interface utilisateur. Une fois qu’un jeu de données a été créé, il est accessible comme tout autre jeu de données du lac de données et utilisé pour divers cas d’utilisation.
exl-id: 6f6c049d-f19f-4161-aeb4-3a01eca7dc75
source-git-commit: 0c2cfe9b0bd839bdf662622283a7563c0417c9a9
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 12%

---

# Générer des jeux de données à partir des résultats dans [!DNL Query Service]

[!DNL Query Service] vous permet d’utiliser des requêtes pour générer des jeux de données dans la variable [!DNL Data Lake]. Ces jeux de données peuvent ensuite être utilisés comme entrée pour d’autres requêtes ou dans d’autres services tels que [!DNL Data Science Workspace], Real-time Customer Profile ou [!DNL Analysis Workspace].

## Génération de jeux de données à partir de l’interface utilisateur de Adobe Experience Platform

Pour créer des jeux de données à partir de l’interface utilisateur de Adobe Experience Platform, procédez comme suit :

1. Créez une requête à partir d&#39;un client connecté et validez la sortie. Pour savoir comment écrire des requêtes à l’aide de [!DNL Query Editor], lisez le [!DNL Query Editor] Guide de l’interface utilisateur [lors de l’écriture de requêtes](./user-guide.md#writing-queries).

2. Dans l’interface utilisateur de Platform, accédez à **[!UICONTROL Requêtes]** suivie de la fonction **[!UICONTROL Parcourir]** et sélectionnez la requête que vous avez créée. Pour plus d’informations sur la manière d’afficher les requêtes qui ont été créées et enregistrées pour votre organisation dans l’interface utilisateur de Platform, lisez le [[!DNL Query Service] aperçu](./overview.md#browse).

3. Dans le panneau Détails de la requête, sélectionnez **[!UICONTROL Jeu de données de sortie]**.

   ![Sélectionner le jeu de données de sortie](../images/ui/create-datasets/output-dataset.png)

4. Dans la boîte de dialogue qui s’affiche, saisissez un nom de jeu de données précédé de votre identifiant LDAP. Le nom du jeu de données ne doit pas nécessairement être unique ou compatible avec SQL. Notez que le nom de la table de votre jeu de données sera généré en fonction du nom du jeu de données que vous créez ici.

5. Ensuite, saisissez une description pour votre jeu de données dans le [!UICONTROL Description] champ et sélectionnez **[!UICONTROL Exécuter la requête]**.

   ![Exécuter la requête](../images/ui/create-datasets/run-query.png)

6. Une fois l’exécution de la requête terminée, accédez à **[!UICONTROL Jeux de données]** pour afficher le jeu de données que vous avez créé. Pour en savoir plus sur l’exécution d’actions courantes lors de l’utilisation de jeux de données dans l’interface utilisateur de Platform, voir la section [Guide de l’interface utilisateur des jeux de données](../../catalog/datasets/user-guide.md).

Une fois qu’un jeu de données est créé, il est accessible comme tout autre jeu de données dans le [!DNL Data Lake] et utilisés pour divers cas d’utilisation.

>[!NOTE]
>
>Dans une mise en œuvre en direct, vous devez appliquer des étiquettes de gouvernance des données après la création du jeu de données. Pour en savoir plus sur l’application de libellés d’utilisation des données aux jeux de données, voir la section [Présentation des libellés d’utilisation des données](../../data-governance/labels/overview.md).

## Génération de jeux de données avec une [!DNL Experience Data Model] schema

Utilisez la syntaxe SQL pour générer un jeu de données avec une variable prédéfinie [!DNL Experience Data Model] Schéma (XDM). Pour plus d’informations sur la syntaxe prise en charge par [!DNL Query Service], veuillez lire la [Guide de syntaxe SQL](../sql/syntax.md#create-table-as-select).

## Jeux de données de sortie

Les jeux de données créés à l’aide de cette fonctionnalité sont générés avec un schéma ad hoc correspondant à la structure des données de sortie telle que définie dans l’instruction SQL. Certains services en aval nécessitent des jeux de données avec des schémas XDM spécifiques. Vérifiez les exigences de mise en forme des données pour les services en aval avant de rédiger votre requête.

## Étapes suivantes

Après avoir lu ce document, vous devez maintenant comprendre comment utiliser [!DNL Query Service] pour générer des jeux de données à partir de l’interface utilisateur de Platform. Pour plus d’informations sur l’accès, l’écriture et l’exécution de requêtes dans l’interface utilisateur de Platform, voir la section [[!DNL Query Service] Présentation de l’interface utilisateur](./overview.md).
