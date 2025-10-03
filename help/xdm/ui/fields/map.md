---
title: Définir des champs de mappage dans l’interface utilisateur
description: Découvrez comment définir un champ de mappage dans l’interface utilisateur d’Experience Platform.
exl-id: 657428a2-f184-4d7c-b657-4fc60d77d5c6
source-git-commit: c0421974493884488e4d639278106835ad1d8b1b
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---

# Définir des champs de mappage dans l’interface utilisateur

Adobe Experience Platform vous permet de personnaliser entièrement la structure de vos classes de modèle de données d’expérience (XDM), groupes de champs de schéma et types de données personnalisés.

Vous pouvez également définir des champs de mappage dans l’éditeur de schémas pour stocker une collection de paires clé-valeur avec des clés dynamiques flexibles.

Lors de la définition d’un nouveau champ dans l’interface utilisateur (IU) d’Experience Platform, utilisez la liste déroulante **[!UICONTROL Type]** et sélectionnez « **[!UICONTROL Mapper]** » dans la liste.

![Éditeur de schémas avec la liste déroulante Type et la valeur Mapper mises en surbrillance.](../../images/ui/fields/special/map.png)

Une propriété [!UICONTROL Type de valeur map] s’affiche. Cette valeur est requise pour les types de données [!UICONTROL Map]. Les valeurs disponibles pour le mappage sont [!UICONTROL Chaîne] et [!UICONTROL Entier]. Sélectionnez une valeur dans la liste déroulante des options disponibles.

![Éditeur de schémas avec la liste déroulante [!UICONTROL Type de valeur de mappage] mise en surbrillance.](../../images/ui/fields/special/map-value-type.png)

Une fois le sous-champ configuré, vous devez l’affecter à un groupe de champs. Utilisez le menu déroulant **[!UICONTROL Groupe de champs]** ou le champ de recherche, puis sélectionnez **[!UICONTROL Appliquer]**. Vous pouvez continuer à ajouter des champs à l’objet en utilisant le même processus ou sélectionner **[!UICONTROL Enregistrer]** pour confirmer vos paramètres.

![Enregistrement de la sélection du groupe de champs et des paramètres appliqués.](../../images/ui/fields/special/assign-to-field-group.gif)

## Restrictions d’utilisation {#restrictions}

XDM place les restrictions suivantes sur l’utilisation de ce type de données :

* Les types de carte DOIVENT être de type `object`.
* Les propriétés des types de carte NE DOIVENT PAS ÊTRE définies (en d’autres termes, ils définissent des objets « vides »).
* Les types de mappage DOIVENT inclure un champ `additionalProperties.type` qui décrit les valeurs qui peuvent être placées dans le mappage, que ce soit `string` ou `integer`.
* La segmentation d’entités multiples peut uniquement être définie en fonction des clés de mappage et non des valeurs.
* Les mappages ne sont pas pris en charge pour les audiences de compte.
* Les mappages définis dans les objets XDM personnalisés sont limités à un seul niveau. Impossible de créer des mappages imbriqués. Cette restriction ne s’applique pas aux mappages définis dans les objets XDM standard.
* Les tableaux de mappages ne sont pas pris en charge.

Assurez-vous d’utiliser uniquement des champs de type carte lorsqu’ils sont absolument nécessaires, car ils présentent les inconvénients de performance suivants :

* Le temps de réponse de [Adobe Experience Platform Query Service](../../../query-service/home.md) passe de trois secondes à dix secondes pour 100 millions d’enregistrements.
* Les cartes doivent comporter moins de 16 clés, faute de quoi elles risquent d’être dégradées davantage.

>[!NOTE]
>
>L’interface utilisateur d’Experience Platform présente des limites dans la façon dont elle peut extraire les clés des champs de type carte. Alors que les champs de type objet peuvent être développés, les mappages s’affichent sous la forme d’un seul champ à la place. Les champs de mappage créés via l’API Schema Registry qui ne sont pas de type chaîne ou entier s’affichent sous la forme de types de données « [!UICONTROL Complexes] ».

## Étapes suivantes

Après lecture de ce document, vous êtes désormais en mesure de définir des champs de mappage dans l’interface utilisateur d’Experience Platform. N’oubliez pas que vous ne pouvez utiliser que des classes et des groupes de champs pour ajouter des champs aux schémas. Pour en savoir plus sur la gestion de ces ressources dans l’interface utilisateur, consultez les guides sur la création et la modification de [classes](../resources/classes.md) et de [groupes de champs](../resources/field-groups.md).

Pour plus d’informations sur les fonctionnalités de l’espace de travail [!UICONTROL Schémas], consultez la présentation de l’espace de travail [[!UICONTROL Schémas]](../overview.md).
