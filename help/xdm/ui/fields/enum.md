---
keywords: Experience Platform;accueil;rubriques populaires;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données;interface utilisateur;espace de travail;énumération;champ;
solution: Experience Platform
title: Définir les champs d’énumération et les valeurs suggérées dans l’interface utilisateur
description: Découvrez comment définir des énumérations et les valeurs suggérées pour les champs de chaîne dans l’interface utilisateur d’Experience Platform.
exl-id: 67ec5382-31de-4f8d-9618-e8919bb5a472
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1222'
ht-degree: 8%

---

# Définir des énumérations et des valeurs suggérées dans l’interface utilisateur {#enums-and-suggested-values}

>[!CONTEXTUALHELP]
>id="platform_xdm_enum_suggestedvalue"
>title="Énumérations et valeurs suggérées"
>abstract="Une **Énumération** limite un champ de chaîne pour autoriser uniquement l&#39;ingestion des données correspondant à un jeu prédéfini de valeurs à ingérer. Chaque limite d&#39;énumération peut se voir attribuer un **Nom d&#39;affichage** qui renseigne les listes déroulantes d&#39;attributs dans l&#39;interface utilisateur de segmentation. Les **valeurs suggérées** pour un champ ne limitent pas l&#39;ingestion et ne déterminent que les noms d&#39;affichage présents dans Segmentation. Si plusieurs schémas partagent un champ appartenant à une classe ou à un groupe de champs commun et que vous définissez différentes énumérations ou valeurs suggérées pour ce champ entre chaque schéma, ces valeurs sont fusionnées et ajoutées dans le schéma d&#39;union."

Dans le modèle de données d’expérience (XDM), un champ de chaîne peut recevoir un ensemble prédéfini de valeurs acceptées ou suggérées pour mieux contrôler les valeurs ingérées dans ce champ ou la manière dont il se comportera dans la segmentation.

**[!UICONTROL Enums]** contraindre les valeurs qui peuvent être ingérées pour un champ de chaîne à un ensemble prédéfini. Si vous tentez d’ingérer des données dans un champ d’énumération et que la valeur ne correspond à aucun de ceux définis dans sa configuration, l’ingestion est refusée.

Contrairement aux énumérations, l’option **[!UICONTROL Suggested values]** permet à d’indiquer un ensemble de valeurs recommandées pour un champ de chaîne qui ne contraignent pas les valeurs qu’il peut ingérer. Au lieu de cela, les valeurs suggérées affectent les valeurs prédéfinies disponibles dans l’[interface utilisateur de segmentation](../../../segmentation/ui/overview.md) lors de l’inclusion du champ de chaîne comme attribut.

Lorsque vous [définissez un nouveau champ](./overview.md#define) dans l’interface utilisateur de Adobe Experience Platform et définissez le type sur [!UICONTROL String], vous avez la possibilité de définir une [énumération](#enum) ou [valeurs suggérées](#suggested-values) pour ce champ.

![Image illustrant l’option Énumération et valeurs suggérées activée pour un champ de chaîne dans l’interface utilisateur](../../images/ui/fields/enum/enum-options-selected.png)

Ce document explique comment définir des énumérations et les valeurs suggérées dans l’espace de travail de l’interface utilisateur de [!UICONTROL Schemas]. Pour un aperçu rapide sur les énumérations et les valeurs suggérées, y compris sur la manière de les configurer dans l’interface utilisateur et leurs effets en aval, regardez la vidéo suivante :

>[!VIDEO](https://video.tv.adobe.com/v/3413677/?captions=fre_fr&quality=12&learn=on)

## Définition d’une énumération {#enum}

Sélectionnez **[!UICONTROL Enums and Suggested Values]**, puis sélectionnez **[!UICONTROL Enums]**. Des contrôles supplémentaires s’affichent, vous permettant de spécifier les contraintes de valeur pour l’énumération. Pour ajouter une contrainte, sélectionnez **[!UICONTROL Add row]**.

![Image affichant l’option Enums sélectionnée dans l’interface utilisateur](../../images/ui/fields/enum/enum-add-row.png)

Sous la **[!UICONTROL Value]** colonne, vous devez indiquer la valeur exacte à laquelle vous souhaitez contraindre le champ. Vous pouvez éventuellement fournir un lien convivial **[!UICONTROL Display Name]** pour la contrainte, ce qui affecte la façon dont la valeur sera représentée dans la segmentation.

Continuez à utiliser **[!UICONTROL Add row]** pour ajouter les contraintes et les libellés facultatifs de votre choix à l’énumération ou sélectionnez l’icône de suppression (![image de l’icône de suppression](/help/images/icons/remove-circle.png)) en regard d’une ligne ajoutée précédemment pour la supprimer. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Apply]** pour appliquer les modifications au schéma.

![Image montrant les valeurs d’énumération et les noms d’affichage renseignés pour le champ de chaîne dans l’interface utilisateur](../../images/ui/fields/enum/enum-confirm.png)

La zone de travail se met à jour pour prendre en compte les modifications. À l’avenir, lorsque vous explorerez ce schéma, vous pourrez afficher et modifier les contraintes du champ d’énumération dans le rail de droite.

## Définir les valeurs suggérées {#suggested-values}

Sélectionnez **[!UICONTROL Enums and Suggested Values]**, puis sélectionnez **[!UICONTROL Suggested Values]** pour faire apparaître d’autres contrôles. À partir de là, sélectionnez **[!UICONTROL Add row]** pour commencer à ajouter des valeurs suggérées.

![Image illustrant l’option Valeurs suggérées sélectionnée dans l’interface utilisateur](../../images/ui/fields/enum/suggested-add-row.png)

Sous la colonne **[!UICONTROL Display Name]** , indiquez un nom convivial pour la valeur telle que vous souhaitez qu’elle apparaisse dans l’interface utilisateur de segmentation. Pour ajouter d’autres valeurs suggérées, sélectionnez à nouveau **[!UICONTROL Add row]** et répétez le processus si nécessaire. Pour supprimer une ligne ajoutée précédemment, sélectionnez ![l’icône de suppression](/help/images/icons/remove-circle.png) en regard de la ligne en question.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Apply]** pour appliquer les modifications au schéma.

![Image montrant les valeurs d’énumération et les noms d’affichage renseignés pour le champ de chaîne dans l’interface utilisateur](../../images/ui/fields/enum/suggested-confirm.png)

>[!NOTE]
>
>Il existe un délai d’environ cinq minutes pour que les valeurs suggérées mises à jour d’un champ soient reflétées dans l’interface utilisateur de segmentation.

### Gérer les valeurs suggérées pour les champs standards

Certains champs des composants XDM standard contiennent leurs propres valeurs suggérées, telles que les `eventType` de la classe [[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md). Bien que vous puissiez créer des valeurs suggérées supplémentaires pour un champ standard, vous ne pouvez pas modifier ni supprimer des valeurs suggérées qui ne sont pas définies par votre organisation. Lors de l’affichage d’un champ standard dans l’interface utilisateur, les valeurs suggérées s’affichent mais sont en lecture seule.

![Image montrant les valeurs d’énumération et les noms d’affichage renseignés pour le champ de chaîne dans l’interface utilisateur](../../images/ui/fields/enum/suggested-standard.png)

Pour ajouter de nouvelles valeurs suggérées pour un champ standard, sélectionnez **[!UICONTROL Add row]**. Pour supprimer une valeur suggérée précédemment ajoutée par votre organisation, sélectionnez ![l’icône](/help/images/icons/remove-circle.png) Supprimer en regard de la ligne en question.

![Image montrant les valeurs d’énumération et les noms d’affichage remplis pour le champ de chaîne dans l’interface utilisateur](../../images/ui/fields/enum/suggested-standard-add.png)

<!-- ### Removing suggested values for standard fields

Only suggested values that you define can be removed from a standard field. Existing suggested values can be disabled so that they no longer appear in the segmentation dropdown, but they cannot be removed outright.

For example, consider a profile schema where the a suggested value for the standard `person.gender` field is disabled:

![Image showing the enum values and display names filled out for the string field in the UI](../../images/ui/fields/enum/standard-enum-disabled.png)

In this example, the display name "[!UICONTROL Non-specific]" is now disabled from being shown in the segmentation dropdown list. However, the value `non_specific` is still part of the list of enumerated fields and is therefore still allowed on ingestion. In other words, you cannot disable the actual enum value for the standard field as it would go against the principle of only allowing changes that make a field less restrictive.

See the [section below](#evolution) for more information on the rules for updating enums and suggested values for existing schema fields. -->

## Règles d’évolution pour les énumérations et valeurs suggérées {#evolution}

Une fois qu’un schéma avec un champ d’énumération a été utilisé pour ingérer des données dans Experience Platform, toutes les modifications ultérieures apportées à la définition du schéma doivent être conformes aux données déjà présentes dans le système. En règle générale, les modifications apportées à un champ existant ne peuvent que rendre ce champ **moins** restrictif. Un champ ne peut pas être rendu plus restrictif qu’il ne l’est déjà.

En ce qui concerne les énumérations et les valeurs suggérées, les règles suivantes s’appliquent après l’ingestion :

* Vous **POUVEZ** ajouter des valeurs suggérées pour les champs standard et personnalisés avec des valeurs suggérées existantes.
* Vous **POUVEZ** supprimer les valeurs suggérées des champs personnalisés avec les valeurs suggérées existantes.
* Vous **POUVEZ** ajouter de nouvelles valeurs d’énumération pour un champ d’énumération personnalisé existant.
* Vous **POUVEZ** basculer les valeurs d’énumération d’un champ personnalisé en valeurs suggérées uniquement, ou les convertir en une chaîne sans énumération ni valeurs suggérées. **Cette permutation ne peut pas être annulée une fois qu’elle a été appliquée.**
* Vous **NE POUVEZ PAS** supprimer les énumérations ou les valeurs suggérées des champs standard.
* Vous **IMPOSSIBLE** ajouter des valeurs d’énumération à un champ sans énumération existante.
* Vous **NE POUVEZ PAS** supprimer moins de toutes les valeurs d’énumération existantes pour un champ personnalisé.
* Vous **NE POUVEZ PAS** passer des valeurs suggérées à une énumération.

## Règles de fusion pour les énumérations et les valeurs suggérées {#merging}

Si plusieurs schémas utilisent le même champ d’énumération avec différentes configurations et que ces schémas sont inclus dans une union, certaines règles s’appliquent en ce qui concerne la manière dont les différences d’énumération sont réconciliées. Les règles exactes varient selon que les schémas référençant le même champ standard (comme `eventType`) ou s’ils référencent le même chemin de champ personnalisé dans différents groupes de champs.

Si vous référencez le même champ standard :

* Toute valeur supplémentaire suggérée **est** AJOUTÉE dans l’union.
* Les mises à jour apportées aux valeurs suggérées pour la même clé d’énumération sont **MISES à jour** dans l’union.

Si vous référencez le même chemin de champ personnalisé dans différents groupes de champs :

* Toute valeur supplémentaire suggérée **est** AJOUTÉE dans l’union.
* Si la même valeur suggérée supplémentaire est définie dans plusieurs schémas, ces valeurs sont **MERGED** dans l’union. En d’autres termes, la même valeur suggérée n’apparaîtra pas deux fois après la fusion.

## Limites de validation

En raison des limitations actuelles du système, il existe deux cas où une énumération n’est pas validée par le système lors de l’ingestion :

1. L’énumération est définie sur un [champ de tableau](./array.md).
1. L’énumération est définie à plusieurs niveaux de profondeur dans la hiérarchie du schéma.

## Étapes suivantes

Ce guide explique comment définir des énumérations et les valeurs suggérées pour les champs de chaîne dans l’interface utilisateur. Pour plus d’informations sur la gestion des énumérations et des valeurs suggérées à l’aide de l’API Schema Registry, consultez le [tutoriel](../../tutorials/suggested-values.md) suivant.

Pour savoir comment définir d’autres types de champs XDM dans l’[!DNL Schema Editor], consultez la présentation sur la [définition de champs dans l’interface utilisateur](./overview.md#special).
