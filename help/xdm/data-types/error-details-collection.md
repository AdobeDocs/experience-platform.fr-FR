---
title: Type De Données De Collecte Des Détails D’Erreur
description: Découvrez le type de données Modèle de données d’expérience (XDM) de la collecte de détails d’erreur .
exl-id: 54b03147-9bca-46af-86c8-90e42b4de26b
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 10%

---

# Type de données de la collecte de [!UICONTROL Error Details]

La collecte de [!UICONTROL Error Details] est un type de données standard des modèles de données d’expérience (XDM) qui décrit les détails de l’erreur. Utilisez le type de données Collecte de [!UICONTROL Error Details] pour capturer les détails de la source de l’erreur et de l’identification. L’ID d’erreur identifie l’erreur et la source de l’erreur indique si elle provient du lecteur ou d’une source externe.

![Diagramme du type de données Informations sur les détails de l’erreur.](../images/data-types/error-details-collection.png)

| Nom d’affichage | Propriété | Type de données | Obligatoire | Description |
|----------------------------|--------------|-----------|----------|-----------------------------------------------|
| [!UICONTROL Error ID] | `name` | chaîne | Non | ID de l’erreur. |
| [!UICONTROL Error Source] | `source` | chaîne | Non | Source de l’erreur. Énumérées : « player », « external » avec les significations respectives. |

{style="table-layout:auto"}
