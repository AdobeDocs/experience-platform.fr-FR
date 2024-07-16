---
title: Définition des champs de mappage dans l’interface utilisateur
description: Découvrez comment définir un champ de mappage dans l’interface utilisateur de l’Experience Platform.
exl-id: 657428a2-f184-4d7c-b657-4fc60d77d5c6
source-git-commit: ee27fc42a1ee23ef650d320df64e5970a84d0d38
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---

# Définition des champs de mappage dans l’interface utilisateur

Adobe Experience Platform vous permet de personnaliser entièrement la structure de vos classes XDM (Experience Data Model) personnalisées, de groupes de champs de schéma et de types de données.

Vous pouvez également définir des champs de mappage dans l’éditeur de schémas pour modéliser des structures de données flexibles et dynamiques ou stocker une collection de paires clé-valeur.

Lors de la définition d’un nouveau champ dans l’interface utilisateur de Platform, utilisez la liste déroulante **[!UICONTROL Type]** et sélectionnez &quot;**[!UICONTROL Map]**&quot; dans la liste.

![Éditeur de schémas avec liste déroulante Type et valeur de carte mise en surbrillance.](../../images/ui/fields/special/map.png)

Une propriété [!UICONTROL Type de valeur de carte] s’affiche. Cette valeur est requise pour les types de données [!UICONTROL Map]. Les valeurs disponibles pour la carte sont [!UICONTROL String] et [!UICONTROL Integer]. Sélectionnez une valeur dans la liste déroulante des options disponibles.

![La liste déroulante de l’éditeur de schémas avec le [!UICONTROL type de valeur de carte] mise en surbrillance.](../../images/ui/fields/special/map-value-type.png)

Une fois que vous avez configuré le sous-champ, vous devez l’affecter à un groupe de champs. Utilisez le menu déroulant **[!UICONTROL Groupe de champs]** ou champ de recherche, et sélectionnez **[!UICONTROL Appliquer]**. Vous pouvez continuer à ajouter des champs à l’objet à l’aide du même processus, ou sélectionner **[!UICONTROL Enregistrer]** pour confirmer vos paramètres.

![Enregistrement de la sélection et des paramètres de groupe de champs appliqués.](../../images/ui/fields/special/assign-to-field-group.gif)

## Restrictions d’utilisation {#restrictions}

XDM impose les restrictions suivantes à l’utilisation de ce type de données :

* Les types de carte DOIVENT être de type `object`.
* Les types de carte NE DOIVENT PAS avoir de propriétés définies (en d’autres termes, ils définissent des objets &quot;vides&quot;).
* Les types de carte DOIVENT inclure un champ `additionalProperties.type` qui décrit les valeurs qui peuvent être placées dans le mappage, `string` ou `integer`.
* La segmentation d’entités multiples ne peut être définie que sur la base des clés de mappage et non des valeurs.
* Les cartes ne sont pas prises en charge pour les audiences de compte.

Assurez-vous que vous utilisez uniquement des champs de type map lorsque cela est absolument nécessaire, car ils présentent les inconvénients suivants en termes de performances :

* Le temps de réponse de [Adobe Experience Platform Query Service](../../../query-service/home.md) se dégrade de trois secondes à dix secondes pour 100 millions d’enregistrements.
* Les cartes doivent comporter moins de 16 clés, sinon elles risquent d’être détériorées.

>[!NOTE]
>
>L’interface utilisateur de Platform présente des limites quant à la manière dont elle peut extraire les clés des champs de type map. Bien que les champs de type objet puissent être développés, les mappages s’affichent sous la forme d’un champ unique. Les champs de mappage créés par le biais de l’API Schema Registry qui ne sont pas des types de données string ou integer s’affichent sous la forme de types de données &quot;[!UICONTROL Complex]&quot;.

## Étapes suivantes

Après avoir lu ce document, vous pouvez désormais définir des champs de mappage dans l’interface utilisateur de Platform. N’oubliez pas que vous ne pouvez utiliser que des classes et des groupes de champs pour ajouter des champs aux schémas. Pour en savoir plus sur la gestion de ces ressources dans l’interface utilisateur, consultez les guides sur la création et la modification des [classes](../resources/classes.md) et des [groupes de champs](../resources/field-groups.md).

Pour plus d’informations sur les fonctionnalités de l’espace de travail [!UICONTROL Schémas], consultez la [[!UICONTROL présentation des schémas] de l’espace de travail](../overview.md).
