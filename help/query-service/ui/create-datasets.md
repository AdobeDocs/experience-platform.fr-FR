---
keywords: Experience Platform;accueil;rubriques populaires;query service;Query service;générer des jeux de données;générer un jeu de données;créer un jeu de données;
solution: Experience Platform
title: Génération de jeux de données de sortie à partir des résultats de requête
type: Tutorial
description: Query Service d’Adobe Experience Platform permet de créer des jeux de données à partir de l’interface utilisateur. Une fois qu’un jeu de données est créé, il est possible d’y accéder comme à tout autre jeu de données du lac de données et de l’utiliser pour divers cas d’utilisation.
exl-id: 6f6c049d-f19f-4161-aeb4-3a01eca7dc75
source-git-commit: 59d2d74b2d77f3bbaca381af908de5295af24e5b
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 84%

---

# Générer des jeux de données de sortie à partir des résultats de requête

[!DNL Query Service] vous permet d’utiliser des requêtes pour générer des jeux de données dans le [!DNL Data Lake]. Ces jeux de données peuvent ensuite être utilisés comme entrée pour d’autres requêtes ou dans d’autres services tels que [!DNL Data Science Workspace], Real-Time Customer Profile ou [!DNL Analysis Workspace].

## Générer des jeux de données à partir de l’interface utilisateur d’Adobe Experience Platform

Pour créer des jeux de données à partir de l’interface utilisateur d’Adobe Experience Platform, procédez comme suit :

1. Rédigez votre requête à l’aide d’un client connecté et validez la sortie. Pour savoir comment écrire des requêtes à l’aide de [!DNL Query Editor], lisez le guide de l’interface utilisateur [!DNL Query Editor] [sur l’écriture de requêtes](./user-guide.md#writing-queries).

2. Dans l’interface utilisateur de Platform, accédez à **[!UICONTROL Requêtes]** puis à l’onglet **[!UICONTROL Modèles]** et sélectionnez la requête que vous avez créée. Pour plus d’informations sur la manière d’afficher les requêtes qui ont été créées et enregistrées pour votre organisation dans l’interface utilisateur de Platform, lisez la [[!DNL Query Service] présentation](./overview.md#browse).

3. Dans le panneau Détails de la requête, sélectionnez **[!UICONTROL Exécuter en tant que CTAS]**.

   ![ L&#39;onglet [!UICONTROL Modèles] de l&#39;espace de travail Requêtes avec l&#39;option [!UICONTROL Exécuter en tant que CTAS] mise en surbrillance.](../images/ui/create-datasets/run-as-ctas.png)

4. Dans la boîte de dialogue qui s’affiche, saisissez un nom de jeu de données précédé de votre identifiant LDAP. Le nom du jeu de données ne doit pas nécessairement être unique ou compatible avec SQL. Notez que le nom du tableau de votre jeu de données sera généré en fonction du nom du jeu de données que vous créez ici.

5. Ensuite, saisissez une description pour votre jeu de données dans le champ [!UICONTROL Description] et sélectionnez **[!UICONTROL Exécuter en tant que CTAS]**.

   ![La boîte de dialogue du jeu de données de sortie avec les détails du jeu de données et [!UICONTROL Exécuter en tant que CTAS] mise en surbrillance](../images/ui/create-datasets/run-query.png)

6. Une fois l’exécution de la requête terminée, accédez à **[!UICONTROL Jeux de données]** pour afficher le jeu de données que vous avez créé. Pour en savoir plus sur l’exécution d’actions courantes lors de l’utilisation de jeux de données dans l’interface utilisateur de Platform, voir le [guide de l’interface utilisateur des jeux de données](../../catalog/datasets/user-guide.md).

Une fois qu’un jeu de données est créé, il est possible d’y accéder comme à tout autre jeu de données du [!DNL Data Lake] et de l’utiliser pour divers cas d’utilisation.

>[!NOTE]
>
>Dans une implémentation en direct, vous devez appliquer des étiquettes de gouvernance des données après la création du jeu de données. Pour en savoir plus sur l’application de libellés d’utilisation des données aux jeux de données, voir la [présentation des libellés d’utilisation des données](../../data-governance/labels/overview.md).

## Générer des jeux de données avec un schéma [!DNL Experience Data Model] prédéfini

Utilisez la syntaxe SQL pour générer un jeu de données avec un schéma [!DNL Experience Data Model] (XDM) prédéfini. Pour plus d’informations sur la syntaxe prise en charge par [!DNL Query Service], veuillez lire le [guide de syntaxe SQL](../sql/syntax.md#create-table-as-select).

## Jeux de données de sortie

Les jeux de données créés à l’aide de cette fonctionnalité sont générés avec un schéma ad hoc correspondant à la structure des données de sortie telle que définie dans l’instruction SQL. Certains services en aval nécessitent des jeux de données avec des schémas XDM spécifiques. Vérifiez les exigences de mise en forme des données pour les services en aval avant de rédiger votre requête.

## Étapes suivantes

Après avoir lu ce document, vous devez maintenant comprendre comment utiliser [!DNL Query Service] pour générer des jeux de données à partir de l’interface utilisateur de Platform. Pour plus d’informations sur l’accès, l’écriture et l’exécution de requêtes dans l’interface utilisateur de Platform, voir la [[!DNL Query Service] présentation de l’interface utilisateur](./overview.md).
