---
title: Définition des champs de mappage dans l’interface utilisateur
description: Découvrez comment définir un champ de mappage dans l’interface utilisateur de l’Experience Platform.
source-git-commit: 8eea73c91d0671b1ddaeb8da0dc18b3e5e306f57
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# Définition des champs de mappage dans l’interface utilisateur

Adobe Experience Platform vous permet de personnaliser entièrement la structure de vos classes XDM (Experience Data Model) personnalisées, de groupes de champs de schéma et de types de données.

Vous pouvez également définir des champs de mappage dans l’éditeur de schémas pour modéliser des structures de données flexibles et dynamiques ou stocker une collection de paires clé-valeur. La structure de données de carte permet des recherches, des insertions et des suppressions efficaces et rapides lorsque des informations sont organisées et accessibles en fonction d’identifiants uniques.

Lors de la définition d’un nouveau champ dans l’interface utilisateur de Platform, utilisez le **[!UICONTROL Type]** , puis sélectionnez &quot;**[!UICONTROL Carte]**&quot; de la liste.

![Éditeur de schémas avec la liste déroulante Type et la valeur Carte mise en surbrillance.](../../images/ui/fields/special/map.png)

A [!UICONTROL Type de valeur de carte] s’affiche. Cette valeur est requise pour [!UICONTROL Carte] types de données. Les valeurs disponibles pour la carte sont les suivantes : [!UICONTROL Chaîne] et [!UICONTROL Entier]. Sélectionnez une valeur dans la liste déroulante des options disponibles.

![L’éditeur de schémas avec la méthode [!UICONTROL Type de valeur de carte] menu déroulant surligné.](../../images/ui/fields/special/map-value-type.png)

Une fois que vous avez configuré le sous-champ, vous devez l’affecter à un groupe de champs. Utilisez la variable **[!UICONTROL Groupe de champs]** menu déroulant ou champ de recherche, puis sélectionnez **[!UICONTROL Appliquer]**. Vous pouvez continuer à ajouter des champs à l’objet en utilisant le même processus, ou sélectionner **[!UICONTROL Enregistrer]** pour confirmer vos paramètres.

![Un enregistrement de la sélection et des paramètres du groupe de champs appliqués.](../../images/ui/fields/special/assign-to-field-group.gif)

>[!NOTE]
>
>L’interface utilisateur de Platform présente des limites quant à la manière dont elle peut extraire les clés des champs de type map. Bien que les champs de type objet puissent être développés, les mappages s’affichent sous la forme d’un champ unique. Les champs de mappage créés par le biais de l’API Schema Registry qui ne sont pas des types de données string ou integer s’affichent sous la forme &quot;[!UICONTROL Complexe]&quot; types de données.

## Étapes suivantes

Après avoir lu ce document, vous pouvez désormais définir des champs de mappage dans l’interface utilisateur de Platform. N’oubliez pas que vous ne pouvez utiliser que des classes et des groupes de champs pour ajouter des champs aux schémas. Pour en savoir plus sur la gestion de ces ressources dans l’interface utilisateur, consultez les guides sur la création et la modification [classes](../resources/classes.md) et [groupes de champs](../resources/field-groups.md).

Pour plus d’informations sur les fonctionnalités de la variable [!UICONTROL Schémas] workspace, voir [[!UICONTROL Schémas] présentation de workspace](../overview.md).
