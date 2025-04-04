---
title: Modèles de requête
description: Les modèles de requête sont des requêtes SQL enregistrées réutilisables qui peuvent être réutilisées par d’autres utilisateurs et utilisatrices pour économiser du temps et des efforts. Ils peuvent être créés à l’aide de Query Editor ou de l’API Query Service et peuvent être utilisés sur tous les jeux de données Experience Platform.
exl-id: e74d058f-bb89-45ed-83cc-2e3a33401270
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 63%

---

# Modèles de requête

Adobe Experience Platform Query Service vous permet d’enregistrer et de réutiliser du code SQL sous la forme de modèles de requête. Les modèles économisent des efforts en évitant la répétition de tâches courantes. Vous pouvez partager des modèles au sein de votre organisation et modifier facilement les valeurs de requête sans avoir à accéder au SQL sous-jacent ni à le comprendre.

Ce document fournit les informations nécessaires à la création de modèles de requête dans Query Service.

## Conditions préalables

Vous devez avoir l’autorisation [!UICONTROL Gérer les requêtes] activée pour accéder à Query Editor et afficher le tableau de bord des requêtes dans l’interface utilisateur d’Experience Platform. L’autorisation est activée via l’[Admin Console](https://adminconsole.adobe.com/) d’Adobe. Contactez l’administrateur ou administratrice de votre organisation si vous ne disposez pas des privilèges d’administrateur pour activer cette autorisation. Consultez la documentation sur le contrôle d’accès pour des [instructions complètes sur l’ajout d’autorisations via Admin Console](../../access-control/home.md).

## Créer un modèle de requête

Vous pouvez créer des modèles de requête par le biais de deux méthodes, en adressant une requête POST au point d’entrée `query-templates` de l’API Query Service, ou en écrivant, en nommant et en enregistrant une requête via Query Editor.

### Utiliser Query Editor pour créer et enregistrer une requête en tant que modèle

Consultez la documentation pour obtenir des instructions sur l’utilisation de Query Editor pour [écrire](./user-guide.md#query-authoring) et [enregistrer des requêtes](./user-guide.md#saving-queries). Une fois que vous avez nommé et enregistré votre requête, elle peut être réutilisée en tant que modèle de requête à partir de l’onglet [!UICONTROL Modèles].

>[!TIP]
>
>Lorsque vous enregistrez une requête dans le Query Editor, un message de confirmation s’affiche pour vous informer de la réussite de l’action. Ce message contextuel contient un lien qui permet d&#39;accéder facilement à l&#39;espace de travail de planification des requêtes. Consultez la [documentation sur la planification des requêtes](./query-schedules.md) pour savoir comment exécuter des requêtes à une cadence personnalisée.

## Parcourir les modèles de requête {#browse}

Dans l’espace de travail Requêtes de l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Modèles]** pour afficher la liste des requêtes enregistrées disponibles.

![Espace de travail des requêtes avec l’onglet Modèles mis en surbrillance.](../images/ui/query-templates/query-templates.png)

Pour trouver les informations de modèle pertinentes, sélectionnez un modèle de requête dans la liste disponible afin d’ouvrir le panneau de détails.

![Panneau de détails de l’espace de travail des requêtes avec l’identifiant de requête en surbrillance.](../images/ui/query-templates/details-panel.png)

Dans le panneau des détails, vous pouvez exécuter les actions suivantes :

* Sélectionnez **[!UICONTROL Exécuter en tant que CTAS]** pour créer une table en sélectionnant les données d&#39;une ou de plusieurs tables existantes. Cette option n’est disponible que si vous disposez d’une requête SELECT.
* Sélectionnez **[!UICONTROL Ajouter un planning]** pour commencer à modifier le planning de votre modèle de requête.
* Sélectionnez **[!UICONTROL Afficher le planning]** pour accéder à l’onglet [!UICONTROL Plannings] du Query Editor. Cette vue contient toutes les informations de planification associées à la requête.
* Sélectionnez **[!UICONTROL Supprimer la requête]** pour supprimer le modèle.
* Sélectionnez le nom du modèle pour accéder à Query Editor où le code SQL est prérenseigné pour modification.

### Utiliser l’API Query Service pour créer un modèle

Consultez la documentation pour obtenir des instructions sur [comment créer un modèle de requête](../api/query-templates.md#create-a-query-template) à l’aide de l’API Query Service. Les détails d’un nouveau modèle de requête créé sont contenus dans le corps de la réponse.

>[!NOTE]
>
>Les modèles créés à l’aide de l’API sont également visibles dans l’onglet Modèles de Query Service de l’interface utilisateur d’Experience Platform .

## Étapes suivantes

En lisant ce document, vous avez maintenant une meilleure compréhension de la manière de créer des modèles de requête dans Query Service. Voir la [présentation de l’interface utilisateur](./overview.md), ou le [guide de l’API Query Service](../api/getting-started.md) pour en savoir plus sur les fonctionnalités de Query Service.

Voir le [guide de point de d’entrée des requêtes planifiées](../api/scheduled-queries.md) pour savoir comment planifier des requêtes à l’aide de l’API, ou le [guide de Query Editor](./user-guide.md#scheduled-queries) pour l’interface utilisateur.
