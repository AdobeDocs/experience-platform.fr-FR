---
title: Obsolescence d’un champ XDM dans l’interface utilisateur
description: Découvrez comment abandonner les champs de modèle de données d’expérience (XDM) à l’aide de l’éditeur de schémas dans Experience Platform.
source-git-commit: f791d32ae38dffe82723800aa9fb5b44bb4f0109
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 0%

---

# Obsolescence d’un champ XDM dans l’interface utilisateur

Le modèle de données d’expérience (XDM) vous offre la possibilité de gérer votre modèle de données à mesure que vos besoins changent en abandonnant les champs de schéma une fois les données ingérées. Les champs indésirables peuvent être abandonnés pour les supprimer de la vue de l’interface utilisateur et les masquer des interfaces utilisateur en aval. Une case à cocher dans l’éditeur de schémas vous permet facilement d’afficher les champs obsolètes et, si nécessaire, vous pouvez également les abandonner.

Comme les champs obsolètes sont masqués de l’interface utilisateur par défaut, cela simplifie votre schéma dans l’éditeur de schémas et empêche l’ajout de champs indésirables aux dépendances en aval telles que le créateur de segments, le concepteur de parcours, etc. L’obsolescence des champs est également rétrocompatible. D’autres systèmes qui utilisent des champs obsolètes, tels que les segments et les requêtes, continueront à les évaluer comme prévu. Si un champ obsolète est utilisé dans un segment existant, il est traité normalement, ce qui signifie que le champ s’affiche comme prévu dans le canevas du créateur de segments ou qu’il est évalué en fonction des données disponibles dans les champs obsolètes. Il s’agit d’une modification constante qui n’a aucune incidence négative sur les flux de données existants.

>[!NOTE]
>
>Avant que les données ne soient ingérées dans un schéma, vous pouvez supprimer les groupes de champs inutiles. Consultez la documentation relative à [Comment supprimer un groupe de champs d’un schéma](../ui/resources/schemas.md#remove-fields) pour plus d’informations.

Une fois les données ingérées dans votre schéma, vous ne pouvez plus supprimer les champs du schéma sans apporter de modifications avec rupture. Dans ce cas, vous pouvez abandonner un champ indésirable dans un schéma ou une ressource personnalisée à l’aide de la propriété [Éditeur de schéma](./create-schema-ui.md) ou le [API Schema Registry](https://developer.adobe.com/experience-platform-apis/references/schema-registry/).

Ce document explique comment abandonner les champs pour différentes ressources XDM à l’aide de l’éditeur de schémas dans l’interface utilisateur de l’Experience Platform. Pour savoir comment abandonner un champ XDM à l’aide de l’API, consultez le tutoriel sur [abandon d’un champ XDM à l’aide de l’API Schema Registry](./field-deprecation-api.md).

## Obsolescence d’un champ {#deprecate}

Pour abandonner un champ personnalisé, accédez à l’éditeur de schémas du schéma que vous souhaitez modifier. Sélectionnez le champ que vous souhaitez rendre obsolète dans le [!UICONTROL Structure] de la zone de travail, suivie de **[!UICONTROL Obsolète]** de la [!UICONTROL Propriétés du champ].

![L’éditeur de schémas avec un champ sélectionné et l’option Obsolète mise en surbrillance.](../images/tutorials/field-deprecation/deprecate-single-field.png)

Une boîte de dialogue s’affiche pour confirmer vos choix et vous informer que le champ sera supprimé de l’affichage de l’interface utilisateur du schéma d’union et masqué des interfaces utilisateur en aval. Pour terminer l’action, sélectionnez **[!UICONTROL Confirmer]**.

![La boîte de dialogue Champ obsolète avec Confirmer mise en surbrillance.](../images/tutorials/field-deprecation/deprecate-field-dialog.png)

Le champ est maintenant supprimé de la vue d’interface utilisateur.

>[!NOTE]
>
>Une fois obsolètes, les interfaces utilisateur en aval telles que les tableaux de bord de segmentation, les Customer Journey Analytics et Adobe Journey Optimizer n’affichent plus les champs obsolètes dans le cadre de leur workflow. Toutefois, les interfaces utilisateur en aval ont la possibilité d’afficher les champs obsolètes si nécessaire et de continuer à traiter le champ obsolète comme normal. Pour plus d’informations, consultez leur documentation respective. Les requêtes et les segments qui utilisent le champ obsolète continueront à s’exécuter comme prévu.

## Afficher les champs obsolètes {#show-deprecated}

Pour afficher les champs précédemment obsolètes, accédez au schéma approprié dans l’éditeur de schémas. Sélectionnez la **[!UICONTROL Afficher les champs obsolètes]** dans la [!UICONTROL Composition] de la zone de travail.

Le champ obsolète apparaît désormais dans la vue IU. Sélectionner **[!UICONTROL Enregistrer]** pour confirmer vos paramètres.

![L’éditeur de schémas avec un champ sélectionné, Afficher les champs obsolètes et Enregistrer en surbrillance.](../images/tutorials/field-deprecation/show-deprecated-fields.png)

## Champs obsolètes {#undeprecate-fields}

Pour annuler un champ obsolète, procédez comme suit : [afficher le champ obsolète ;](#show-deprecated) comme décrit ci-dessus, puis sélectionnez le champ obsolète dans le [!UICONTROL Structure] . Ensuite, sélectionnez **[!UICONTROL Undeprecate]** de la [!UICONTROL Propriétés du champ] barre latérale suivie de **[!UICONTROL Enregistrer]**.

![Éditeur de schéma avec les champs obsolètes, Non obsolète et Enregistrer en surbrillance.](../images/tutorials/field-deprecation/undeprecate-single-field.png)

Le [!UICONTROL Champ non obsolète] s’affiche. Pour confirmer vos modifications, sélectionnez **[!UICONTROL Confirmer]**.

![Le [!UICONTROL Champ non obsolète] avec l’option Confirmer mise en surbrillance.](../images/tutorials/field-deprecation/undeprecate-field-dialog.png)

Le champ s’affiche désormais en standard dans la vue IU et également dans les interfaces utilisateur en aval. Encore une fois, vous avez désormais la possibilité de rendre le champ obsolète.

## Étapes suivantes

Ce document explique comment abandonner les champs XDM à l’aide de l’interface utilisateur de l’éditeur de schémas. Pour plus d’informations sur la configuration des champs pour les ressources personnalisées, consultez le guide sur [définition des champs XDM dans l’API](./custom-fields-api.md). Pour plus d’informations sur la gestion des descripteurs, voir [guide de point de terminaison des descripteurs](../api/descriptors.md).
