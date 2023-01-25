---
keywords: Experience Platform;accueil;rubriques les plus consultées;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données;ui;espace de travail;énumération;champ;
solution: Experience Platform
title: Définition des champs d’énumération et des valeurs proposées dans l’interface utilisateur
description: Découvrez comment définir des énumérations et des valeurs suggérées pour les champs de chaîne dans l’interface utilisateur de l’Experience Platform.
exl-id: 67ec5382-31de-4f8d-9618-e8919bb5a472
source-git-commit: f770ba8668c5154b2cf5a57ba61d771ca34ab2d8
workflow-type: tm+mt
source-wordcount: '1358'
ht-degree: 0%

---

# Définition d’énumérations et de valeurs suggérées dans l’interface utilisateur {#enums-and-suggested-values}

>[!CONTEXTUALHELP]
>id="platform_xdm_enum_suggestedvalue"
>title="Enumérations et valeurs proposées"
>abstract="Un **Enum** limite un champ de chaîne pour autoriser uniquement l’ingestion des données correspondant à un jeu prédéfini de valeurs. Chaque contrainte d’énumération peut se voir attribuer une **Nom d’affichage** qui renseigne les listes déroulantes d’attributs dans l’interface utilisateur de segmentation. **Valeurs proposées** pour un champ ne limite pas l’ingestion et ne détermine que les noms d’affichage affichés dans Segmentation. Si plusieurs schémas partagent un champ appartenant à une classe ou à un groupe de champs commun et que vous définissez différentes énumérations ou valeurs suggérées pour ce champ entre chaque schéma, ces valeurs sont fusionnées et ajoutées dans le schéma d’union."

Dans le modèle de données d’expérience (XDM), un champ de chaîne peut se voir attribuer un jeu prédéfini de valeurs acceptées ou suggérées afin de mieux contrôler les valeurs ingérées dans ce champ ou leur comportement dans la segmentation.

**[!UICONTROL Enumérations]** contraindre à un jeu prédéfini les valeurs pouvant être ingérées pour un champ de chaîne. Si vous tentez d’ingérer des données dans un champ d’énumération et que la valeur ne correspond à aucune de celles définies dans sa configuration, l’ingestion sera refusée.

Contrairement aux énumérations, la variable **[!UICONTROL Valeurs proposées]** permet de représenter un ensemble de valeurs recommandées pour un champ de chaîne qui ne limite pas les valeurs qu’il peut ingérer. Au lieu de cela, les valeurs suggérées affectent les valeurs prédéfinies disponibles dans la variable [Interface utilisateur de segmentation](../../../segmentation/ui/overview.md) lors de l’inclusion du champ de chaîne en tant qu’attribut.

When [définition d’un nouveau champ](./overview.md#define) dans l’interface utilisateur de Adobe Experience Platform et définissez le type sur [!UICONTROL Chaîne], vous avez la possibilité de définir une [enum](#enum) ou [valeurs suggérées](#suggested-values) pour ce champ.

![L’option Énumération et valeurs proposées est activée pour un champ de chaîne dans l’interface utilisateur.](../../images/ui/fields/enum/enum-options-selected.png)

Ce document explique comment définir des énumérations et des valeurs suggérées dans le [!UICONTROL Schémas] Espace de travail de l’interface utilisateur. Pour un aperçu rapide des énumérations et des valeurs suggérées, y compris la manière de les configurer dans l’interface utilisateur et de leurs effets en aval, regardez la vidéo suivante :

>[!VIDEO](https://video.tv.adobe.com/v/3409501/?quality=12&learn=on)

## Définition d’une énumération {#enum}

Sélectionner **[!UICONTROL Enumérations et valeurs proposées]**, puis sélectionnez **[!UICONTROL Enumérations]**. Des contrôles supplémentaires s’affichent, vous permettant de spécifier les contraintes de valeur pour l’énumération. Pour ajouter une contrainte, sélectionnez **[!UICONTROL Ajouter une ligne]**.

![L’option Enumérations sélectionnée dans l’interface utilisateur.](../../images/ui/fields/enum/enum-add-row.png)

Sous , **[!UICONTROL Valeur]** , vous devez indiquer la valeur exacte à laquelle vous souhaitez limiter le champ. Vous pouvez éventuellement fournir une **[!UICONTROL Nom d’affichage]** de la contrainte, qui affecte également la manière dont la valeur sera représentée dans la segmentation.

Continuer à utiliser **[!UICONTROL Ajouter une ligne]** pour ajouter les contraintes souhaitées et les libellés facultatifs à l’énumération, ou sélectionnez l’icône de suppression (![Image de l’icône de suppression](../../images/ui/fields/enum/remove-icon.png)) en regard d’une ligne précédemment ajoutée pour la supprimer. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Appliquer]** pour appliquer les modifications au schéma.

![Valeurs d’énumération et noms d’affichage renseignés pour le champ de chaîne de l’interface utilisateur.](../../images/ui/fields/enum/enum-confirm.png)

Le canevas se met à jour pour refléter les modifications. Lorsque vous explorez ce schéma à l’avenir, vous pouvez afficher et modifier les contraintes du champ d’énumération dans le rail de droite.

## Définir les valeurs suggérées {#suggested-values}

Sélectionner **[!UICONTROL Enumérations et valeurs proposées]**, puis sélectionnez **[!UICONTROL Valeurs proposées]** pour afficher des contrôles supplémentaires. À partir de là, sélectionnez **[!UICONTROL Ajouter une ligne]** pour commencer à ajouter des valeurs suggérées.

![L’option Valeurs proposées sélectionnée dans l’interface utilisateur.](../../images/ui/fields/enum/suggested-add-row.png)

Sous , **[!UICONTROL Nom d’affichage]** indiquez un nom convivial pour la valeur telle que vous souhaitez la voir apparaître dans l’interface utilisateur de segmentation. Pour ajouter d’autres valeurs suggérées, sélectionnez **[!UICONTROL Ajouter une ligne]** et répétez le processus selon vos besoins. Pour supprimer une ligne précédemment ajoutée, sélectionnez ![l’icône de suppression](../../images/ui/fields/enum/remove-icon.png) à côté de la ligne en question.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Appliquer]** pour appliquer les modifications au schéma.

![Valeurs d’énumération et noms d’affichage renseignés pour le champ de chaîne de l’interface utilisateur.](../../images/ui/fields/enum/suggested-confirm.png)

>[!NOTE]
>
>Il existe un délai d’environ cinq minutes pour que les valeurs suggérées d’un champ soient répercutées dans l’interface utilisateur de segmentation.

### Gestion des valeurs suggérées pour les champs standard {#standard-fields}

Certains champs des composants XDM standard contiennent leurs propres valeurs suggérées, telles que `eventType` de la [[!UICONTROL XDM ExperienceEvent] class](../../classes/experienceevent.md) et vous pouvez créer d’autres valeurs suggérées pour ces champs standard de la même manière que pour les champs personnalisés. Vous pouvez également désactiver l’une des valeurs suggérées standard qui ne correspond pas à vos cas d’utilisation, mais qui ne peut pas être directement supprimée de la définition du champ.

>[!IMPORTANT]
>
>Vous pouvez uniquement désactiver les valeurs suggérées pour les champs standard qui n’ont pas de contrainte d’énumération correspondante. En d’autres termes, si la variable **[!UICONTROL Enumérations]** est activée au lieu de **[!UICONTROL Valeurs proposées]**, alors le champ est limité en tant qu’énumération et ces contraintes ne peuvent pas être désactivées.
>
>Voir [section ci-dessous](#evolution) pour plus d’informations sur les règles de mise à jour des énumérations et des valeurs suggérées pour les champs de schéma existants.

Pour désactiver une valeur suggérée standard, sélectionnez la bascule en regard de la valeur en question. Vous pouvez désactiver toute combinaison de valeurs suggérées, y compris toutes celles-ci.

![Certaines des valeurs suggérées standard pour la variable [!UICONTROL Type d’événement] champ désactivé dans l’interface utilisateur.](../../images/ui/fields/enum/suggested-standard.png)

Pour ajouter de nouvelles valeurs suggérées pour un champ standard, sélectionnez **[!UICONTROL Ajouter une ligne]**. Pour supprimer une valeur suggérée précédemment ajoutée par votre organisation, sélectionnez ![l’icône de suppression](../../images/ui/fields/enum/remove-icon.png) à côté de la ligne en question.

![Valeurs suggérées personnalisées ajoutées à un champ de chaîne standard dans l’interface utilisateur.](../../images/ui/fields/enum/suggested-standard-add.png)

## Règles d’évolution pour les énumérations et les valeurs proposées {#evolution}

Une fois qu’un schéma avec un champ d’énumération a été utilisé pour ingérer des données dans Platform, toute modification supplémentaire apportée à la définition de schéma doit être conforme aux données déjà présentes dans le système. En règle générale, les modifications apportées à un champ existant ne peuvent que le faire. **less** restrictif. Un champ ne peut pas être rendu plus restrictif qu’il ne l’est déjà.

En ce qui concerne les énumérations et les valeurs proposées, les règles suivantes s’appliquent après l’ingestion :

* You **CAN** ajoutez des valeurs suggérées à n’importe quel champ avec des valeurs suggérées existantes.
* You **CAN** supprimer les valeurs suggérées personnalisées des champs avec des valeurs suggérées existantes.
* You **CAN** désactivez les valeurs suggérées standard des champs avec uniquement des valeurs suggérées et sans contraintes d’énumération.
* You **CAN** ajoutez de nouvelles valeurs d’énumération pour un champ d’énumération personnalisé existant.
* You **CAN** changer les valeurs d’énumération d’un champ personnalisé en valeurs suggérées uniquement ou les convertir en chaîne sans énumération ou valeurs suggérées. **Une fois appliqué, ce basculement ne peut pas être annulé.**
* You **CANNOT** ajouter ou supprimer des contraintes d’énumération des champs standard.
* You **CANNOT** supprimer les valeurs suggérées des champs standard (désactiver uniquement).
* You **CANNOT** ajoutez des contraintes d’énumération aux champs sans énumération existante.
* You **CANNOT** supprimez moins de contraintes d’énumération existantes pour un champ personnalisé.
* You **CANNOT** passer des valeurs suggérées à une énumération.

## Fusion de règles pour les énumérations et les valeurs proposées {#merging}

Si plusieurs schémas utilisent le même champ d’énumération avec des configurations différentes et que ces schémas sont inclus dans une union, certaines règles s’appliquent lorsqu’il s’agit de la manière dont les différences d’énumération sont réconciliées. Les règles exactes dépendent si les schémas référençant le même champ standard (comme `eventType`) ou s’ils référencent le même chemin d’accès personnalisé dans différents groupes de champs.

Si vous référencez le même champ standard :

* Toutes les autres valeurs suggérées sont **AJOUTÉ** dans l’union.
* Les mises à jour apportées aux valeurs suggérées pour la même clé d’énumération sont les suivantes : **MISE À JOUR** dans l’union.

Si vous référencez le même chemin de champ personnalisé dans différents groupes de champs :

* Toutes les autres valeurs suggérées sont **AJOUTÉ** dans l’union.
* Si la même valeur suggérée supplémentaire est définie dans plusieurs schémas, ces valeurs sont **FUSIONNÉ** dans l’union. En d’autres termes, la même valeur suggérée n’apparaîtra pas deux fois après la fusion.

## Limites de validation

En raison des limitations actuelles du système, il existe deux cas où une énumération n’est pas validée par le système lors de l’ingestion :

1. L’énumération est définie sur une [champ de tableau](./array.md).
1. L’énumération est définie à plusieurs niveaux au sein de la hiérarchie des schémas.

## Étapes suivantes

Ce guide explique comment définir des énumérations et des valeurs suggérées pour les champs de chaîne dans l’interface utilisateur. Pour plus d’informations sur la gestion des énumérations et des valeurs suggérées à l’aide de l’API Schema Registry, reportez-vous aux sections suivantes : [tutoriel](../../tutorials/suggested-values.md).

Pour savoir comment définir d’autres types de champ XDM dans [!DNL Schema Editor], consultez la présentation sur [définition de champs dans l’interface utilisateur.](./overview.md#special).
