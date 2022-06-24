---
title: Modèles de requête
description: Les modèles de requête sont des requêtes SQL enregistrées réutilisables qui peuvent être réutilisées par d’autres utilisateurs pour gagner du temps et des efforts. Ils peuvent être créés à l’aide de Query Editor ou de l’API Query Service et peuvent être utilisés sur tous les jeux de données Experience Platform.
source-git-commit: 5ed822ec16e8e8d38e93370440242ec4c1c01320
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 2%

---

# Modèles de requête

Adobe Experience Platform Query Service vous permet d’enregistrer et de réutiliser du code SQL sous la forme de modèles de requête. Les modèles économisent des efforts en évitant la répétition de tâches courantes. Vous pouvez partager des modèles au sein de votre organisation et modifier facilement les valeurs de requête sans avoir à accéder au SQL sous-jacent ni à le comprendre.

Ce document fournit les informations nécessaires à la création de modèles de requête dans Query Service.

## Conditions préalables

Vous devez avoir la variable [!UICONTROL Gestion des requêtes] l’autorisation d’accéder à Query Editor et d’afficher le tableau de bord des requêtes dans l’interface utilisateur de Platform. L’autorisation est activée via l’Adobe [Admin Console](https://adminconsole.adobe.com/). Contactez l’administrateur de votre entreprise si vous ne disposez pas des privilèges d’administrateur pour activer cette autorisation. Consultez la documentation sur le contrôle d’accès pour [instructions complètes sur l’ajout d’autorisations via Admin Console](../../access-control/home.md).

## Création d’un modèle de requête

Vous pouvez créer des modèles de requête par le biais de deux méthodes, en adressant une requête POST à l’API Query Service. `query-templates` point de terminaison ou en écrivant, en nommant et en enregistrant une requête via Query Editor.

### Utilisation de Query Editor pour créer et enregistrer une requête en tant que modèle

Consultez la documentation pour obtenir des instructions sur l’utilisation de Query Editor pour [write](./user-guide.md#query-authoring) et [enregistrement de requêtes](./user-guide.md#saving-queries). Une fois que vous avez nommé et enregistré votre requête, elle peut être réutilisée en tant que modèle de requête à partir du [!UICONTROL Parcourir] .

Dans l’espace de travail Requêtes de l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Parcourir]** pour afficher la liste des requêtes enregistrées disponibles.

![Espace de travail des requêtes avec l’onglet Parcourir surligné.](../images/ui/query-templates/query-templates.png)

Pour trouver les informations de modèle pertinentes, sélectionnez un modèle de requête dans la liste disponible afin d’ouvrir le panneau Détails.

![Panneau Détails de l’espace de travail des requêtes avec l’ID de requête en surbrillance.](../images/ui/query-templates/details-panel.png)

### Utilisation de l’API Query Service pour créer un modèle

Consultez la documentation pour obtenir des instructions sur [comment créer un modèle de requête](../api/query-templates.md#create-a-query-template) à l’aide de l’API Query Service. Les détails d’un nouveau modèle de requête sont contenus dans le corps de la réponse.

>[!NOTE]
>
>Les modèles créés à l’aide de l’API sont également visibles dans l’onglet Parcourir de l’interface utilisateur de Platform Query Service.

## Étapes suivantes

En lisant ce document, vous comprenez mieux comment créer des modèles de requête dans Query Service. Voir [Présentation de l’interface utilisateur](./overview.md), ou la variable [Guide de l’API Query Service](../api/getting-started.md) pour en savoir plus sur les fonctionnalités de Query Service.

Voir [guide de point de terminaison des requêtes planifiées](../api/scheduled-queries.md) pour savoir comment planifier des requêtes à l’aide de l’API, ou de l’API [Guide de Query Editor](./user-guide.md#scheduled-queries) pour l’interface utilisateur.
