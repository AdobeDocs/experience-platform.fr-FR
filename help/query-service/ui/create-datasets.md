---
keywords: Experience Platform;accueil;rubriques populaires;service de requête;Service de requête;générer des jeux de données;générer un jeu de données;créer un jeu de données;
solution: Experience Platform
title: Générer des jeux de données de sortie à partir des résultats de requête
type: Tutorial
description: Le service de requête Adobe Experience Platform permet de créer des jeux de données à partir de l’interface utilisateur. Une fois qu’un jeu de données est créé, il est possible d’y accéder comme à tout autre jeu de données du lac de données et de l’utiliser pour divers cas d’utilisation.
exl-id: 6f6c049d-f19f-4161-aeb4-3a01eca7dc75
TQID: https://experienceleague.adobe.com/Qf1c-E8r6TmvcIHXO72sxQOev8q5BxfZoCYxb-F9gH4
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: c132d929-fa62-4271-803e-b823be07b914id: daec7ead-f475-492a-a3b3-02ae08565d6f
subfeature_v2: id: ee602049-8a18-43df-9299-a689a025a371
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c7d04a2c-412a-4c9d-9d7a-4456eaa5adeb
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 489
ht-degree: 62%

---

# Générer des jeux de données de sortie à partir des résultats de requête

[!DNL Query Service] vous permet d’utiliser des requêtes pour générer des jeux de données dans le [!DNL Data Lake]. Ces jeux de données peuvent ensuite être utilisés comme entrée pour d’autres requêtes ou dans d’autres services tels que [!DNL Data Science Workspace], Real-Time Customer Profile ou [!DNL Analysis Workspace].

## Générer des jeux de données à partir de l’interface utilisateur d’Adobe Experience Platform

Pour créer des jeux de données à partir de l’interface utilisateur d’Adobe Experience Platform, procédez comme suit :

1. Rédigez votre requête à l’aide d’un client connecté et validez la sortie. Pour savoir comment écrire des requêtes à l’aide de [!DNL Query Editor], lisez le guide de l’interface utilisateur [!DNL Query Editor] [sur l’écriture de requêtes](./user-guide.md#writing-queries).

2. Dans l’interface utilisateur d’Experience Platform, accédez à **[!UICONTROL Queries]** puis à l’onglet **[!UICONTROL Templates]** et sélectionnez la requête que vous avez créée. Pour plus d’informations sur l’affichage des requêtes qui ont été créées et enregistrées pour votre organisation dans l’interface utilisateur d’Experience Platform, lisez la [[!DNL Query Service] présentation](./overview.md#browse).

3. Dans le panneau Détails de la requête, sélectionnez **[!UICONTROL Run as CTAS]**.

   ![Onglet [!UICONTROL Templates] de l’espace de travail Requêtes avec l’[!UICONTROL Run as CTAS] Sélectionner en surbrillance.](../images/ui/create-datasets/run-as-ctas.png)

4. Dans la boîte de dialogue qui s’affiche, saisissez un nom de jeu de données précédé de votre identifiant LDAP. Le nom du jeu de données ne doit pas nécessairement être unique ou compatible avec SQL. Notez que le nom du tableau de votre jeu de données sera généré en fonction du nom du jeu de données que vous créez ici.

5. Ensuite, saisissez une description pour votre jeu de données dans le champ [!UICONTROL Description] et sélectionnez **[!UICONTROL Run as CTAS]**.

   ![La boîte de dialogue Jeu de données de sortie avec les détails du jeu de données et les [!UICONTROL Run as CTAS] en surbrillance](../images/ui/create-datasets/run-query.png)

6. Une fois l’exécution de la requête terminée, accédez à **[!UICONTROL Datasets]** pour afficher le jeu de données que vous avez créé. Pour en savoir plus sur l’exécution d’actions courantes lors de l’utilisation de jeux de données dans l’interface utilisateur d’Experience Platform, consultez le [guide de l’interface utilisateur des jeux de données](../../catalog/datasets/user-guide.md).

Une fois qu’un jeu de données est créé, il est possible d’y accéder comme à tout autre jeu de données du [!DNL Data Lake] et de l’utiliser pour divers cas d’utilisation.

>[!NOTE]
>
>Dans une implémentation en direct, vous devez appliquer des étiquettes de gouvernance des données après la création du jeu de données. Pour en savoir plus sur l’application de libellés d’utilisation des données aux jeux de données, voir la [présentation des libellés d’utilisation des données](../../data-governance/labels/overview.md).

## Générer des jeux de données avec un schéma [!DNL Experience Data Model] prédéfini

Utilisez la syntaxe SQL pour générer un jeu de données avec un schéma [!DNL Experience Data Model] (XDM) prédéfini. Pour plus d’informations sur la syntaxe prise en charge par [!DNL Query Service], veuillez lire le [guide de syntaxe SQL](../sql/syntax.md#create-table-as-select).

## Jeux de données de sortie

Les jeux de données créés à l’aide de cette fonctionnalité sont générés avec un schéma ad hoc correspondant à la structure des données de sortie telle que définie dans l’instruction SQL. Certains services en aval nécessitent des jeux de données avec des schémas XDM spécifiques. Vérifiez les exigences de mise en forme des données pour les services en aval avant de rédiger votre requête.

## Étapes suivantes

Vous êtes arrivé au bout de ce document. À présent, vous devez comprendre comment utiliser [!DNL Query Service] pour générer des jeux de données à partir de l’interface utilisateur d’Experience Platform. Pour plus d’informations sur l’accès, l’écriture et l’exécution de requêtes dans l’interface utilisateur d’Experience Platform, consultez la [[!DNL Query Service]  présentation de l’interface utilisateur](./overview.md).
